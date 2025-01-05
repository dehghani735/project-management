To model the `$lookup` aggregation in Spring Boot, you will use the **MongoTemplate** provided by Spring Data MongoDB. This allows you to run complex aggregation pipelines, including joins, using the `$lookup` stage in MongoDB.

Let’s walk through an example where you will:
1. Define the **Customer** and **Order** models.
2. Set up the **MongoTemplate** to perform the `$lookup` aggregation.
3. Implement a service to query and aggregate the data.

### 1. Define the Models (Customer and Order)

First, you define the entities for `Customer` and `Order`.

```java
// Customer.java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection = "customers")
public class Customer {
    @Id
    private String id;
    private String name;
    private String email;
    private String address;

    // Getters and Setters
}

// Order.java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection = "orders")
public class Order {
    @Id
    private String id;
    private String orderDate;
    private double totalAmount;
    private String customerId; // Foreign key reference to Customer

    // Getters and Setters
}
```

### 2. Create a DTO for the Aggregated Result

This is the result that will be returned after performing the `$lookup` operation, combining data from both `Order` and `Customer`.

```java
// OrderWithCustomerInfo.java
package com.example.demo.dto;

import com.example.demo.model.Customer;
import com.example.demo.model.Order;

public class OrderWithCustomerInfo {
    private Order order;
    private Customer customer;

    // Constructor, Getters, and Setters
}
```

### 3. Set up the Aggregation Query Using MongoTemplate

In Spring Boot, you can use `MongoTemplate` to execute the MongoDB aggregation query with `$lookup`.

Here is how you can perform the aggregation in a service class:

```java
// OrderService.java
package com.example.demo.service;

import com.example.demo.dto.OrderWithCustomerInfo;
import com.example.demo.model.Customer;
import com.example.demo.model.Order;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.aggregation.Aggregation;
import org.springframework.data.mongodb.core.aggregation.AggregationResults;
import org.springframework.stereotype.Service;

import static org.springframework.data.mongodb.core.aggregation.Aggregation.*;

import java.util.List;

@Service
public class OrderService {

    @Autowired
    private MongoTemplate mongoTemplate;

    public List<OrderWithCustomerInfo> getOrdersWithCustomerInfo() {
        // Define the $lookup stage
        Aggregation aggregation = newAggregation(
            lookup("customers", "customerId", "_id", "customer_info"),
            unwind("customer_info", true), // Unwind the array of customer_info
            project()
                .andExclude("_id") // Exclude the internal _id field (optional)
                .and("customer_info").as("customer") // Project customer_info to customer field
                .and("orderDate").as("orderDate")
                .and("totalAmount").as("totalAmount")
                .and("customerId").as("customerId")
        );

        // Run the aggregation
        AggregationResults<OrderWithCustomerInfo> results = mongoTemplate.aggregate(aggregation, "orders", OrderWithCustomerInfo.class);

        // Return the results as a list
        return results.getMappedResults();
    }
}
```

### Explanation of the Aggregation:
1. **lookup("customers", "customerId", "_id", "customer_info")**: This is the `$lookup` stage, where:
   - `"customers"` is the collection we want to join.
   - `"customerId"` is the field from the `orders` collection to match on.
   - `"_id"` is the field in the `customers` collection to match against.
   - `"customer_info"` is where the results from the `customers` collection will be stored.

2. **unwind("customer_info", true)**: This flattens the `customer_info` array, so we don’t get an array of customers in the result. The `true` argument ensures that if there is no match, it will still return the order.

3. **project()**: This stage reshapes the output to include specific fields. Here, we map `customer_info` to `customer` and exclude the internal MongoDB `_id` field.

### 4. Implement a Controller

Now, you can expose the service via a REST endpoint to fetch the aggregated data.

```java
// OrderController.java
package com.example.demo.controller;

import com.example.demo.dto.OrderWithCustomerInfo;
import com.example.demo.service.OrderService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/orders")
public class OrderController {

    @Autowired
    private OrderService orderService;

    @GetMapping("/with-customer-info")
    public List<OrderWithCustomerInfo> getOrdersWithCustomerInfo() {
        return orderService.getOrdersWithCustomerInfo();
    }
}
```

### 5. Result Example

When you call the `/orders/with-customer-info` endpoint, you will receive the following result:

```json
[
  {
    "order": {
      "orderDate": "2024-10-01",
      "totalAmount": 150.0,
      "customerId": "1001"
    },
    "customer": {
      "id": "1001",
      "name": "John Doe",
      "email": "john.doe@example.com",
      "address": "123 Main St, Cityville"
    }
  },
  {
    "order": {
      "orderDate": "2024-10-02",
      "totalAmount": 250.0,
      "customerId": "1002"
    },
    "customer": {
      "id": "1002",
      "name": "Jane Smith",
      "email": "jane.smith@example.com",
      "address": "456 Oak St, Townsville"
    }
  }
]
```

### Summary:
- We created two collections: `orders` and `customers`.
- We used the **MongoTemplate** in Spring Boot to perform an aggregation with `$lookup` to join data from these two collections.
- The result contains each order along with the related customer’s information, demonstrating how to perform a join-like operation in MongoDB using Spring Boot.

This shows how `$lookup` can be used at the Spring level to implement join queries, while still leveraging the flexibility and speed of MongoDB.

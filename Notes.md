# API-first design

is a methodology where APIs are treated as first-class citizens in the software development process. This approach emphasizes designing and defining APIs before writing any code for the application itself. The goal is to ensure that the API is well-defined, well-documented, and meets the needs of its consumers from the outset.
Key Principles of API-First Design

    Design Before Implementation: The API is designed before any code is written. This involves defining endpoints, request and response formats, error handling, and authentication mechanisms upfront.

    Consumer-Driven: The API design process starts with understanding the needs and requirements of the API consumers (e.g., frontend developers, third-party services). The API should be intuitive and easy to use for its intended audience.

    Consistency and Standards: APIs should adhere to consistent design principles and standards, such as RESTful principles, naming conventions, and HTTP status codes. This ensures that APIs are predictable and easier to work with.

    Documentation and Contracts: Comprehensive documentation is created alongside the API design. This often includes API specifications (e.g., OpenAPI/Swagger), which act as a contract between the API provider and consumers. The documentation should be clear, concise, and up-to-date.

    Mocking and Testing: Before the actual implementation, mock servers and testing tools are used to validate the API design. This allows for early feedback from consumers and helps identify potential issues early in the development process.

    Iterative Feedback and Refinement: The API design is iteratively refined based on feedback from stakeholders and early adopters. This ensures that the API evolves to meet the needs of its users effectively.

Benefits of API-First Design

    Improved Collaboration: Clear API contracts and documentation facilitate better communication between backend and frontend teams, as well as with third-party developers.
    Faster Development: By having a well-defined API, frontend and backend teams can work in parallel. Mock APIs enable frontend development to proceed without waiting for backend completion.
    Better API Quality: Early design and feedback lead to more thoughtful and robust API design, reducing the likelihood of breaking changes and ensuring a more stable API.
    Enhanced Flexibility: A clear API contract allows for easier integration with other services and future extensions.

Example Workflow

    Gather Requirements: Understand the needs of API consumers. Identify the key functionalities and use cases for the API.

    Design the API: Use API specification tools like OpenAPI/Swagger to design the API endpoints, request and response formats, and error handling.

    Create Documentation: Generate comprehensive API documentation using tools like Swagger UI or Redoc. This documentation acts as a reference for developers.

    Mock the API: Use tools like Postman, SwaggerHub, or WireMock to create mock versions of the API. This allows for early testing and feedback from consumers.

    Implement the API: Start the actual implementation of the API based on the agreed-upon design. Backend developers can begin coding while frontend developers use the mock API.

    Test and Iterate: Continuously test the API with real and simulated data. Iterate on the design based on feedback from tests and stakeholders.

Tools and Technologies

    OpenAPI/Swagger: Standard for defining and documenting RESTful APIs.
    Postman: Tool for API development, testing, and documentation.
    SwaggerHub: Platform for API design, documentation, and collaboration.
    WireMock: Tool for mocking HTTP services.
    Redoc: Tool for generating API documentation from OpenAPI specifications.

Example: Designing an API with OpenAPI

Here's a simple example of an OpenAPI specification for a hypothetical user management API:

openapi: 3.0.0
info:
  title: User Management API
  version: 1.0.0
paths:
  /users:
    get:
      summary: Get a list of users
      responses:
        '200':
          description: A JSON array of user objects
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
    post:
      summary: Create a new user
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/NewUser'
      responses:
        '201':
          description: User created successfully
  /users/{id}:
    get:
      summary: Get a user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: A user object
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: User not found
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: string
        name:
          type: string
        email:
          type: string
    NewUser:
      type: object
      properties:
        name:
          type: string
        email:
          type: string


This OpenAPI specification can be used to generate documentation, create mock APIs, and guide the implementation process.
Conclusion

API-first design is a powerful approach that ensures APIs are well-designed, documented, and meet the needs of their consumers from the start. By focusing on the API as a primary asset, teams can improve collaboration, accelerate development, and create more robust and user-friendly APIs.

# Spring Rest Docs

https://dev.to/noelopez/document-your-api-with-spring-rest-docs-3jfo

https://github.com/spring-projects/spring-restdocs-samples

https://spring.io/guides/gs/testing-restdocs

[text](https://docs.spring.io/spring-restdocs/docs/current/reference/htmlsingle/#working-with-asciidoctor)


[text](https://spring.io/guides/gs/testing-restdocs)


> asciidoctor -v index.adoc 



# RestClient

https://docs.spring.io/spring-framework/reference/integration/rest-clients.html



# Swagger

EnableSwagger2   what is this?
https://medium.com/@akshitaswami248/swagger-configuration-in-spring-boot-application-8558492df54b


https://springdoc.org/#migrating-from-springfox


# Mongodb

https://www.mongodb.com/docs/manual/reference/sql-aggregation-comparison/
https://www.mongodb.com/docs/manual/reference/operator/aggregation-pipeline/
https://www.practical-mongodb-aggregations.com/front-cover.html



docker run --name mongodbdocker -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=mongopass -e MONGO_INITDB_DATABASE=vmed -d mongodb/mongodb-community-server:latest

https://www.mongodb.com/docs/mongodb-shell/run-commands/
https://howtodoinjava.com/mongodb/command-failed-with-error-18/



https://www.mongodb.com/resources/products/compatibilities/spring-boot

chatgpt:
Using an embedded MongoDB for testing Spring Boot applications is a great way to ensure your tests run consistently across different environments without the need for an external MongoDB server. de.flapdoodle.embed.mongo is a popular library for this purpose. Here's how you can set it up:
Step-by-Step Guide
1. Add Dependencies

First, you need to add the necessary dependencies to your pom.xml if you're using Maven, or build.gradle if you're using Gradle.

Maven:

xml

<dependency>
    <groupId>de.flapdoodle.embed</groupId>
    <artifactId>de.flapdoodle.embed.mongo</artifactId>
    <version>4.3.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>

Gradle:

groovy

testImplementation 'de.flapdoodle.embed:de.flapdoodle.embed.mongo:4.3.1'
implementation 'org.springframework.boot:spring-boot-starter-data-mongodb'
testImplementation 'org.springframework.boot:spring-boot-starter-test'

2. Configure Embedded MongoDB for Tests

Create a configuration class for the embedded MongoDB. This class will be annotated with @Configuration and will configure an embedded MongoDB instance for your tests.

java

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.SimpleMongoClientDatabaseFactory;
import org.springframework.data.mongodb.core.SimpleMongoClientDbFactory;
import org.springframework.data.mongodb.core.convert.DefaultMongoTypeMapper;
import org.springframework.data.mongodb.core.convert.MappingMongoConverter;
import org.springframework.data.mongodb.core.convert.MongoCustomConversions;
import org.springframework.data.mongodb.core.mapping.MongoMappingContext;
import org.springframework.data.mongodb.repository.config.EnableMongoRepositories;

import com.mongodb.client.MongoClients;
import de.flapdoodle.embed.mongo.MongodExecutable;
import de.flapdoodle.embed.mongo.MongodStarter;
import de.flapdoodle.embed.mongo.config.IMongodConfig;
import de.flapdoodle.embed.mongo.config.MongodConfigBuilder;
import de.flapdoodle.embed.mongo.config.RuntimeConfigBuilder;
import de.flapdoodle.embed.mongo.distribution.Version;
import de.flapdoodle.embed.process.runtime.Network;

@Configuration
@EnableMongoRepositories(basePackages = "com.example.yourpackage")
public class EmbeddedMongoConfig {

    @Bean
    public MongodExecutable embeddedMongoServer() throws Exception {
        int port = 27017;
        IMongodConfig mongodConfig = new MongodConfigBuilder()
            .version(Version.Main.PRODUCTION)
            .net(new de.flapdoodle.embed.mongo.config.Net(port, Network.localhostIsIPv6()))
            .build();

        MongodStarter starter = MongodStarter.getDefaultInstance();
        MongodExecutable mongodExecutable = starter.prepare(mongodConfig);
        mongodExecutable.start();
        return mongodExecutable;
    }

    @Bean
    public MongoTemplate mongoTemplate() {
        return new MongoTemplate(MongoClients.create("mongodb://localhost:27017"), "test");
    }
}

3. Use Embedded MongoDB in Tests

Annotate your test classes with @SpringBootTest and include the embedded MongoDB configuration.

java

import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import com.example.yourpackage.YourRepository;

import static org.assertj.core.api.Assertions.assertThat;

@ExtendWith(SpringExtension.class)
@SpringBootTest
public class YourRepositoryTest {

    @Autowired
    private YourRepository yourRepository;

    @Test
    public void testSaveAndFind() {
        // Given
        YourEntity entity = new YourEntity();
        entity.setName("Test");

        // When
        yourRepository.save(entity);
        YourEntity found = yourRepository.findByName("Test");

        // Then
        assertThat(found).isNotNull();
        assertThat(found.getName()).isEqualTo("Test");
    }
}

4. Cleanup Embedded MongoDB

Ensure that the embedded MongoDB server is stopped after your tests are done. This can be achieved using a shutdown hook.

java

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class EmbeddedMongoConfig {

    @Bean(destroyMethod = "stop")
    public MongodExecutable embeddedMongoServer() throws Exception {
        int port = 27017;
        IMongodConfig mongodConfig = new MongodConfigBuilder()
            .version(Version.Main.PRODUCTION)
            .net(new de.flapdoodle.embed.mongo.config.Net(port, Network.localhostIsIPv6()))
            .build();

        MongodStarter starter = MongodStarter.getDefaultInstance();
        MongodExecutable mongodExecutable = starter.prepare(mongodConfig);
        mongodExecutable.start();
        return mongodExecutable;
    }

    @Bean
    public MongoTemplate mongoTemplate() {
        return new MongoTemplate(MongoClients.create("mongodb://localhost:27017"), "test");
    }
}

Summary

    Dependencies: Add de.flapdoodle.embed.mongo and Spring Data MongoDB dependencies.
    Configuration: Create a configuration class to start the embedded MongoDB and configure MongoTemplate.
    Testing: Write tests annotated with @SpringBootTest, injecting repositories and using them as you would with a real MongoDB instance.
    Cleanup: Ensure the embedded MongoDB instance is stopped after tests.

By following these steps, you can effectively use an embedded MongoDB instance for testing your Spring Boot applications.


## mongodb the definitive guide

Queries return a database cursor, which lazily returns batches of documents as
you need them
There are a lot of metaoperations you can perform on a cursor, including skip‐
ping a certain number of results, limiting the number of results returned, and
sorting results.

Introduction to find
An empty query document (i.e., {}) matches everything in the collection. If find isn’t
given a query document, it defaults to {}. For example, the following:
> db.c.find()
> db.prescription.find({"patientName": "4420123456"});

Specifying Which Keys to Return
> db.prescription.find({"patientName": "4420123456"}, {"status":1, "singleDrugs": 1, "_id": 0});

Limitations

Query Criteria
such as ranges, OR-clauses, and negation.
Query Conditionals
"$lt", "$lte", "$gt", and "$gte"

> db.users.find({"age" : {"$gte" : 18, "$lte" : 30}})
This would find all documents where the "age" field was greater than or equal to 18
AND less than or equal to 30.

> start = new Date("01/01/2007")
> db.users.find({"registered" : {"$lt" : start}})

"$ne", which stands for “not equal.”

> db.users.find({"username" : {"$ne" : "joe"}})

OR Queries
two ways to do an OR query in MongoDB.
"$in" can be used to query for a variety of values for a single key.
"$or" is more general; it can be used to query for any of the given values across multiple keys.

> db.raffle.find({"ticket_no" : {"$in" : [725, 542, 390]}})
> db.users.find({"user_id" : {"$in" : [12345, "joe"]}})

The opposite of "$in" is "$nin"

> db.raffle.find({"ticket_no" : {"$nin" : [725, 542, 390]}})

> db.raffle.find({"$or" : [{"ticket_no" : 725}, {"winner" : true}]})
> db.raffle.find({"$or" : [{"ticket_no" : {"$in" : [725, 542, 390]}},
...  {"winner" : true}]})

$not
"$not" is a metaconditional: it can be applied on top of any other criteria.

> db.users.find({"id_num" : {"$mod" : [5, 1]}})
> db.users.find({"id_num" : {"$not" : {"$mod" : [5, 1]}}})

Type-Specific Queries
null
> db.c.find({"y" : null})
> db.c.find({"z" : null})
> db.c.find({"z" : {"$eq" : null, "$exists" : true}})

Regular Expressions
case-insensitive matching:
> db.users.find( {"name" : {"$regex" : /joe/i } })
> db.users.find({"name" : /joey?/i})

Querying Arrays
> db.food.insertOne({"fruit" : ["apple", "banana", "peach"]})
> db.food.find({"fruit" : "banana"})

“$all”
> db.food.insertOne({"_id" : 1, "fruit" : ["apple", "banana", "peach"]})
> db.food.insertOne({"_id" : 2, "fruit" : ["apple", "kumquat", "orange"]})
> db.food.insertOne({"_id" : 3, "fruit" : ["cherry", "banana", "apple"]})

> db.food.find({fruit : {$all : ["apple", "banana"]}})

“$size”
> db.food.find({"fruit" : {"$size" : 3}})
> db.food.update(criteria, {"$push" : {"fruit" : "strawberry"}})
> db.food.update(criteria,
... {"$push" : {"fruit" : "strawberry"}, "$inc" : {"size" : 1}})
> db.food.find({"size" : {"$gt" : 3}})

“$slice”
> db.blog.posts.findOne(criteria, {"comments" : {"$slice" : 10}})
> db.blog.posts.findOne(criteria, {"comments" : {"$slice" : -10}})
> db.blog.posts.findOne(criteria, {"comments" : {"$slice" : [23, 10]}})
This would skip the first 23 elements and return the 24th through 33rd.

> db.blog.posts.findOne(criteria, {"comments" : {"$slice" : -1}})

Limits, Skips, and Sorts
> db.c.find().limit(3)
> db.c.find().skip(3)

sort takes an object: a set of key/value pairs where the keys are key names and the
values are the sort directions. The sort direction can be 1 (ascending) or −1 (descend‐
ing)
> db.c.find().sort({username : 1, age : -1})
> db.stock.find({"desc" : "mp3"}).limit(50).sort({"price" : -1})

Comparison order
1. Minimum value
2. Null
3. Numbers (integers, longs, doubles, decimals)
4. Strings
5. Object/document
6. Array
7. Binary data
8. Object ID
9. Boolean
10. Date
11. Timestamp
12. Regular expression
13. Maximum value


Paginating results without skip
var latest = null;
// display first page
while (page1.hasNext()) {
latest = page1.next();
display(latest);
}
// get next page
var page2 = db.foo.find({"date" : {"$lt" : latest.date}});
page2.sort({"date" : -1}).limit(100);

Finding a random document
> db.people.insertOne({"name" : "joe", "random" : Math.random()})

> var random = Math.random()
> result = db.people.findOne({"random" : {"$gt" : random}})

just make sure to have an index that includes the random key:
> db.people.ensureIndex({"profession" : 1, "state" : 1, "random" : 1})


Indexes
> for (i=0; i<1000000; i++) {
...db.users.insertOne(
...{
..."i" : i,
..."username" : "user"+i,
..."age" : Math.floor(Math.random()*120),
..."created" : new Date()
...}
...);
...}

> db.users.find({"username": "user101"}).explain("executionStats")

Creating an Index
> db.users.createIndex({"username" : 1})

> db.currentOp()

Introduction to Compound Indexes
> db.users.createIndex({"age" : 1, "username" : 1})

db.users.find({"age" : 21}).sort({"username" : -1})
Note that sort direction doesn’t matter: MongoDB can traverse the index in either
direction.

db.users.find({"age" : {"$gte" : 21, "$lte" : 30}})

db.users.find({"age" : {"$gte" : 21, "$lte" : 30}}).sort({"username" : 1})
MongoDB will need to sort the results in memory before returning them

https://www.mongodb.com/docs/manual/reference/method/cursor.sort/#sort-index-use
To achieve a consistent sort, add a field which contains exclusively unique values to the sort. The following command uses the sort() method to sort on both the borough field and the _id field:
> db.restaurants.find().sort( { "borough": 1, "_id": 1 } )

How MongoDB Selects an Index
To win the race, a query thread must be the first to either return all the query results or return a trial number of results in sort order.

The server maintains a cache of query plans. Over time, as a collection changes and as the indexes change, eventually a query plan might be evicted from the cache and MongoDB will, again, experiment with possible query plans to find the one that works best for the current collection and set of indexes.

Using Compound Indexes
{
  "_id" : ObjectId("585d817db4743f74e2da067c"),
  "student_id" : 0,
  "scores" : [
    {
    "type" : "exam",
    "score" : 38.05000060199827
    },
    {
    "type" : "quiz",
    "score" : 79.45079445008987
    },
    {
    "type" : "homework",
    "score" : 74.50150548699534
    },
    {
    "type" : "homework",
    "score" : 74.68381684615845
    }
  ],
  "class_id" : 127
}

> db.students.createIndex({"class_id": 1})
> db.students.createIndex({student_id: 1, class_id: 1})

> db.students.find({student_id:{$gt:500000}, class_id:54})
...          .sort({student_id:1})
...          .explain("executionStats")



CHAPTER 7 Introduction to the Aggregation Framework

MongoDB provides powerful support for running analytics natively using the aggregation framework
• The aggregation framework
• Aggregation stages
• Aggregation expressions
• Aggregation accumulators

Pipelines, Stages, and Tunables
The aggregation framework is a set of analytics tools within MongoDB that allow you to do analytics on documents in one or more collections.
The aggregation framework is based on the concept of a pipeline.
With an aggregation pipeline we take input from a MongoDB collection and pass the documents from that collection through one or more stages, each of which performs a different operation on its inputs

![alt text](image.png)

Each stage provides a set of knobs, or tunables, that we can control to parameterize
the stage to perform whatever task we’re interested in doing.

match, project, sort, skip, and limit stages

db.companies.aggregate([
  {$match: {founded_year: 2004}},
])
equivalent to:
db.companies.find({founded_year: 2004})

let’s add a project stage to our pipeline to reduce the output to just a few fields per document:
db.companies.aggregate([
  {$match: {founded_year: 2004}},
  {$project: {
    _id: 0,
    name: 1,
    founded_year: 1
  }}
])

db.companies.aggregate([
  {$match: {founded_year: 2004}},
  {$limit: 5},
  {$project: {
    _id: 0,
    name: 1}}
])

db.companies.aggregate([
  { $match: { founded_year: 2004 } },
  { $sort: { name: 1} },
  { $limit: 5 },
  { $project: {
    _id: 0,
    name: 1 } }
])

db.companies.aggregate([
  {$match: {founded_year: 2004}},
  {$sort: {name: 1}},
  {$skip: 10},
  {$limit: 5},
  {$project: {
    _id: 0,
    name: 1}},
])

Expressions

$project

db.companies.aggregate([
  {$match: {"funding_rounds.investments.financial_org.permalink": "greylock" }},
  {$project: {
    _id: 0,
    name: 1,
    ipo: "$ipo.pub_year",
    valuation: "$ipo.valuation_amount",
    funders: "$funding_rounds.investments.financial_org.permalink"
  }}
]).pretty()

db.companies.aggregate([
  {$match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  {$project: {
    _id: 0,
    name: 1,
    amount: "$funding_rounds.raised_amount",
    year: "$funding_rounds.funded_year"
  }}
])

$unwind
When working with array fields in an aggregation pipeline, it is often necessary to include one or more unwind stages.

![unwind](image-1.png)

db.companies.aggregate([
  {$match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  {$project: {
    _id: 0,
    name: 1,
    amount: "$funding_rounds.raised_amount",
    year: "$funding_rounds.funded_year"
  }}
])

db.companies.aggregate([
  { $match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  { $unwind: "$funding_rounds" },
  { $project: {
    _id: 0,
    name: 1,
    amount: "$funding_rounds.raised_amount",
    year: "$funding_rounds.funded_year"
  } }
])

db.companies.aggregate([
  { $match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  { $unwind: "$funding_rounds" },
  { $project: {
    _id: 0,
    name: 1,
    funder: "$funding_rounds.investments.financial_org.permalink",
    amount: "$funding_rounds.raised_amount",
    year: "$funding_rounds.funded_year"
  } }
])

For efficiency, we want to match as early as possible in our pipeline

in order to select only those funding rounds in which Greylock participated:

db.companies.aggregate([
  { $match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  { $unwind: "$funding_rounds" },
  { $match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  { $project: {
    _id: 0,
    name: 1,
    individualFunder: "$funding_rounds.investments.person.permalink",
    fundingOrganization: "$funding_rounds.investments.financial_org.permalink",
    amount: "$funding_rounds.raised_amount",
    year: "$funding_rounds.funded_year"
  } }
])

Array Expressions
filter expression:
A filter expression selects a subset of the elements in an array based on filter criteria.
we specify the name we’d like to use for this "funding_rounds" array throughout the rest of our filter expression.
We use $$ to reference a variable defined within the expression we’re working in.

db.companies.aggregate([
  { $match: {"funding_rounds.investments.financial_org.permalink": "greylock"} },
  { $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    rounds: { $filter: {
      input: "$funding_rounds",
      as: "round",
      cond: { $gte: ["$$round.raised_amount", 100000000] } } }
    } },
    { $match: {"rounds.investments.financial_org.permalink": "greylock" } },
]).pretty()

db.companies.aggregate([
  { $match: { "founded_year": 2010 } },
  { $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    first_round: { $arrayElemAt: [ "$funding_rounds", 0 ] },
    last_round: { $arrayElemAt: [ "$funding_rounds", -1 ] }
  } }
]).pretty()

db.companies.aggregate([
  { $match: { "founded_year": 2010 } },
  { $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    early_rounds: { $slice: [ "$funding_rounds", 1, 3 ] }
  } }
]).pretty()

db.companies.aggregate([
  { $match: { "founded_year": 2004 } },
  { $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    total_rounds: { $size: "$funding_rounds" }
  } }
]).pretty()


Accumulators

They calculate values from field values found in multiple documents.

The primary difference between the accumulators in the group stage and the
project stage is that in the project stage accumulators such as $sum and $avg must
operate on arrays within a single document, whereas accumulators in the group stage, as we’ll see in a later section, provide you with the ability to perform calculations on values across multiple documents.

db.companies.aggregate([
  { $match: { "funding_rounds": { $exists: true, $ne: [ ]} } },
  { $project: {
    _id: 0,
    name: 1,
    largest_round: { $max: "$funding_rounds.raised_amount" }
  } }
])

Remember that in project stages accumulators must work on an array-valued field.

db.companies.aggregate([
  { $match: { "funding_rounds": { $exists: true, $ne: [ ]} } },
  { $project: {
    _id: 0,
    name: 1,
    total_funding: { $sum: "$funding_rounds.raised_amount" }
  } }
])

Introduction to Grouping
In a group stage, we can aggregate together values from multiple documents and perform some type of aggregation operation on them, such as calculating an average

db.companies.aggregate([
  { $group: {
    _id: { founded_year: "$founded_year" },
    average_number_of_employees: { $avg: "$number_of_employees" }
  } },
  { $sort: { average_number_of_employees: -1 } }
])

We use this field to define what the group stage uses to organize the documents that it sees.

db.companies.aggregate( [
  { $match: { "relationships.person": { $ne: null } } },
  { $project: { relationships: 1, _id: 0 } },
  { $unwind: "$relationships" },
  { $group: {
    _id: "$relationships.person",
    count: { $sum: 1 }
  } },
  { $sort: { count: -1 } }
]).pretty()

The _id Field in Group Stages:

db.companies.aggregate([
  { $match: { founded_year: { $gte: 2013 } } },
  { $group: {
    _id: { founded_year: "$founded_year"},
    companies: { $push: "$name" }
  } },
  { $sort: { "_id.founded_year": 1 } }
]).pretty()

db.companies.aggregate([
  { $match: { founded_year: { $gte: 2010 } } },
  { $group: {
    _id: { founded_year: "$founded_year", category_code: "$category_code" },
    companies: { $push: "$name" }
  } },
  { $sort: { "_id.founded_year": 1 } }
]).pretty()

db.companies.aggregate([
  { $group: {
    _id: { ipo_year: "$ipo.pub_year" },
    companies: { $push: "$name" }
  } },
  { $sort: { "_id.ipo_year": 1 } }
]).pretty()

a $push expression will add the resulting value to an array that it builds throughout its run.

db.companies.aggregate( [
  { $match: { "relationships.person": { $ne: null } } },
  { $project: { relationships: 1, _id: 0 } },
  { $unwind: "$relationships" },
  { $group: {
    _id: "$relationships.person",
    count: { $sum: 1 }
  } },
  { $sort: { count: -1 } }
] )

In general, bear in mind that what we want to do here is make sure that in our output, the semantics of our _id value are clear.

Group Versus Project

db.companies.aggregate([
  { $match: { funding_rounds: { $ne: [ ] } } },
  { $unwind: "$funding_rounds" },
  { $sort: { "funding_rounds.funded_year": 1,
    "funding_rounds.funded_month": 1,
    "funding_rounds.funded_day": 1 } },
  { $group: {
    _id: { company: "$name" },
    funding: {
      $push: {
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } }
  } },
] ).pretty()
























# Spring Security Test

https://docs.spring.io/spring-security/reference/servlet/test/mockmvc/authentication.html#test-mockmvc-securitycontextholder-rpp

https://docs.spring.io/spring-security/reference/servlet/test/method.html


# maven

19 Jun 2024

I could not download the asciidoctor-maven-plugin plugin.

I commented the registry.vaslapp.com from pom.xml
I moved the settings.xml from .m2 to not authorize.
I changed the proxy setting of intellij to use proxy.
I turned on my vpn.

Then it was downloaded!

[ERROR] Failed to execute goal org.asciidoctor:asciidoctor-maven-plugin:3.0.0:process-asciidoc (generate-docs) on project vmedcore: The plugin org.asciidoctor:asciidoctor-maven-plugin:3.0.0 requires Maven version 3.8.5 -> [Help 1]
[ERROR] 




[INFO] --- asciidoctor-maven-plugin:1.5.8:process-asciidoc (generate-docs) @ vmedcore ---
[INFO] sourceDirectory /home/detafti/Projects/vmed/src/main/asciidoc does not exist. Skip processing


# k8s

> kubectl get pod -n vmed
> kubectl describe pod demo-pod
> kubectl logs -f -n vmed vmed-core-55fdcb67d6-psdfr --tail=200

# DDD with java

## Chapter 1: the rationale for ddd

Immutables -> value objects and ddd
Axon and Lagom => ddd framewords

![alt text](image-3.png)
![alt text](image-2.png)



# Prometheus

**Recording rules** in Prometheus are a mechanism for precomputing frequently used or computationally expensive queries and storing the results as new time series. These rules enable you to simplify dashboards and alerting configurations while improving query performance.

---

### **Key Features of Recording Rules**
1. **Precomputing Results**:
   - Recording rules evaluate queries at regular intervals and store the result as a new time series.
   - This reduces the computational overhead of repeatedly evaluating the same query.

2. **Custom Time Series**:
   - The results of recording rules are stored as new time series with a specified metric name and optional labels.

3. **Improved Performance**:
   - By storing precomputed results, Prometheus can retrieve them directly during dashboard rendering or alerting, improving response times.

4. **Simplification**:
   - Complex queries are reduced to simpler metrics, making configurations easier to understand and maintain.

---

### **Use Cases for Recording Rules**
1. **Dashboard Optimization**:
   - Store results of expensive or frequently queried metrics to improve dashboard performance.

2. **Alerting**:
   - Precompute metrics used in alerting rules to reduce latency and computational load.

3. **Derived Metrics**:
   - Create new metrics by combining or transforming existing metrics.

---

### **How to Define Recording Rules**
Recording rules are defined in a **Prometheus rules file** (YAML format) and loaded into Prometheus through the configuration.

#### Example: Recording Rule Definition
```yaml
groups:
  - name: example-rules
    interval: 1m  # Optional: The interval at which rules are evaluated
    rules:
      - record: node:cpu_usage:rate
        expr: rate(node_cpu_seconds_total[5m])
        labels:
          environment: production
```

#### Explanation:
- **`record`**: Specifies the name of the new time series (`node:cpu_usage:rate`).
- **`expr`**: The query expression to evaluate (`rate(node_cpu_seconds_total[5m])`).
- **`labels`**: (Optional) Adds or overrides labels for the new time series (`environment=production`).
- **`interval`**: (Optional) How often the rule is evaluated (default is the global `scrape_interval`).

---

### **Loading Recording Rules**
To load recording rules into Prometheus:
1. Add the rules file to your Prometheus configuration under the `rule_files` section.
   ```yaml
   rule_files:
     - 'rules/*.yml'
   ```
2. Restart Prometheus or reload the configuration using the HTTP API (`/-/reload` endpoint).

---

### **Using Recorded Metrics**
Once defined and evaluated, the results of recording rules can be queried like any other metric in Prometheus. For example:
```promql
node:cpu_usage:rate
```

---

### **Benefits**
- **Efficiency**: Precomputing reduces query evaluation time during high load.
- **Scalability**: Simplifies dashboards and alerting systems by avoiding repeated evaluations of complex queries.
- **Flexibility**: Derived metrics allow you to store meaningful data tailored to your needs.

---

### **Best Practices**
1. **Avoid Overloading Rules**:
   - Do not define too many recording rules to prevent increased storage usage and evaluation load.

2. **Use Descriptive Names**:
   - Use clear and consistent naming for recorded metrics to improve readability and maintainability.

3. **Organize Rule Files**:
   - Group related rules in separate files for better organization.

4. **Test Expressions**:
   - Test the query expressions in the Prometheus console before defining them in recording rules.

---

Recording rules are an essential feature for enhancing the efficiency and usability of Prometheus, especially in large-scale monitoring setups.


# sonarqube

/home/detafti/.sdkman/candidates/java/21.0.2-oracle/bin/java -Dmaven.multiModuleProjectDirectory=/home/detafti/Projects/vmed -Djansi.passthrough=true -Dmaven.home=/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/plugins/maven/lib/maven3 -Dclassworlds.conf=/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/plugins/maven/lib/maven3/bin/m2.conf -Dmaven.ext.class.path=/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/plugins/maven/lib/maven-event-listener.jar -javaagent:/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/lib/idea_rt.jar=34961:/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/bin -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath /home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/plugins/maven/lib/maven3/boot/plexus-classworlds.license:/home/detafti/utilities/ideaIC-2024.1.2/idea-IC-241.17011.79/plugins/maven/lib/maven3/boot/plexus-classworlds-2.8.0.jar org.codehaus.classworlds.Launcher -Didea.version=2024.3 clean verify -- add token here




# ActiveMQ Artemis
https://www.javatodev.com/how-to-use-activemq-with-spring-boot-rest-api/

https://docs.spring.io/spring-boot/reference/messaging/jms.html

https://spring.io/guides/gs/messaging-jms



# CQRS and CDC

https://ibm-cloud-architecture.github.io/refarch-eda

https://ibm-cloud-architecture.github.io/refarch-eda/patterns/cqrs/

https://ibm-cloud-architecture.github.io/refarch-eda/patterns/event-sourcing/

https://debezium.io/blog/2020/02/10/event-sourcing-vs-cdc/

https://martinfowler.com/bliki/CQRS.html

https://developer.ibm.com/learningpaths
https://developer.ibm.com/learningpaths/develop-kafka-apps/
https://developer.ibm.com/learningpaths/kubernetes-learning-path/

https://developer.ibm.com/articles/event-streams-kafka-fundamentals/?mhsrc=ibmsearch_a&mhq=kafka#topics-and-partitions4

https://developer.ibm.com/search/?q=kafka


# Kafka

using callback or onCompletion to log or handle the exception on the producer side in send() method.

Configuring Producers

client.id
acks = 0, 1, all => will impact latency, reliability guarantees. it's a tradeoff.
end-to-end latency is is measured from the time a record was produced until it is available for consumers to read and is identical for all three options. The reason is that, in order to maintain consistency, Kafka will not allow consumers to read records until they are written to all in sync replicas. Therefore, if you care about end-to-end latency, rather than just the producer latency, there is no trade-off to make: you will get the same end-to-end latency if you choose the most reliable option.

Message Delivery Time
max.block.ms => 
delivery.timeout.ms => 
You can configure the delivery timeout to the maximum time you’ll want to wait for a message to be sent, typically a few minutes, and then leave the default number of retries (virtually infinite). With this configuration, the producer will keep retrying for as long as it has time to keep trying (or until it succeeds). This is a much more reasonable way to think about retries.

request.timeout.ms

retries and retry.backoff.ms => Not all errors will be retried by the producer. Some errors are not transient and will not cause retries (e.g., “message too large” error). In general, because the producer handles retries for you, there is no point in handling retries within your own application logic. You will want to focus your efforts on handling nonretriable errors or cases where retry attempts were exhausted.

linger.ms
linger.ms controls the amount of time to wait for additional messages before send‐
ing the current batch. KafkaProducer sends a batch of messages either when the cur‐
rent batch is full or when the linger.ms limit is reached. By default, the producer will
send messages as soon as there is a sender thread available to send them, even if
there’s just one message in the batch. By setting linger.ms higher than 0, we instruct
the producer to wait a few milliseconds to add additional messages to the batch
before sending it to the brokers. This increases latency a little and significantly
increases throughput—the overhead per message is much lower, and compression, if
enabled, is much better.

buffer.memory
This config sets the amount of memory the producer will use to buffer messages waiting to be sent to brokers.
If messages are sent by the application faster than they can
be delivered to the server, the producer may run out of space, and additional send()
calls will block for max.block.ms and wait for space to free up before throwing an
exception. Note that unlike most producer exceptions, this timeout is thrown by
send() and not by the resulting Future.

compression.type
snappy, gzip, lz4, or zstd
you reduce network utilization and storage, which is often a bottleneck when sending messages to Kafka

batch.size
When multiple records are sent to the same partition, the producer will batch them together. This parameter controls the amount of memory in bytes (not messages!) that will be used for each batch. When the batch is full, all the messages in the batch will be sent. However, this does not mean that the producer will wait for the batch to become full. The producer will send half-full batches and even batches with just a single message in them. Therefore, setting the batch size too large will not cause delays in sending messages; it will just use more memory for the batches. Setting the batch size too small will add some overhead because the producer will need to send messages more frequently.

max.in.flight.requests.per.connection
Apache Kafka preserves the order of messages within a partition.
This means that if messages are sent from the producer in a specific order, the broker will write them to a partition in that order and all
consumers will read them in that order. For some use cases, order is very important. There is a big difference between depositing
$100 in an account and later withdrawing it, and the other way around! However, some use cases are less sensitive.
Setting the retries parameter to nonzero and the max.in. flight.requests.per.connection to more than 1 means that it is
possible that the broker will fail to write the first batch of messages, succeed in writing the second (which was already in-flight), and
then retry the first batch and succeed, thereby reversing the order. Since we want at least two in-flight requests for performance rea‐
sons, and a high number of retries for reliability reasons, the best solution is to set enable.idempotence=true. This guarantees message ordering with up to five in-flight requests and also guarantees that retries will not introduce duplicates. Chapter 8 discusses the idempotent producer in depth.

max.request.size
message.max.bytes
It is usually a good idea to have these configurations match, so the producer will not attempt to send messages of a size that will be rejected by the broker.

receive.buffer.bytes and send.buffer.bytes:
These are the sizes of the TCP send and receive buffers used by the sockets when writing and reading data. If these are set to –1, the OS defaults will be used. It is a good idea to increase these when producers or consumers communicate with brokers in a different datacenter, because those network links typically have higher latency and lower bandwidth.

enable.idempotence
exactly once semantics: Exactly once is a fairly large topic, and we’ll dedicate an entire chapter to it, but idempotent producer is a simple and highly beneficial part of it.
When the idempotent producer is enabled, the producer will attach a sequence number to each record it sends.
If the broker receives records with the same sequence number, it will reject the sec‐
ond copy and the producer will receive the harmless DuplicateSequenceException.

Enabling idempotence requires max.in.flight.requests.per.connection to be less than or equal to 5, retries to be greater than 0, and acks=all. If incompatible values are set, a ConfigException will be thrown.




# Scrum

Five ideas to encourage an agile culture: courage, focus, commitment, respect, and openness

Sprint Goal
Sprint Planning of every Spring
Team members
Stakeholders
product Increment
refinement meeting
Product Backlog
Sprint Backlog
Features 
Sprint Review
Daily Scrum
User Stories
Story Points
Commitment
Refinement
Backlog refinement
Product Backlog item
Product Backlog refinement
Sprint Burndown
releasable product Increment
Sprint Retrospective


scrum teams: self-organizing and cross-functional
Self-organization will happen only when there is no predefined solution to a problem.
The litmus test of whether a Scrum Team is truly cross-functional is its ability to deliver a valuable working product Increment every Sprint.

Don’t Separate Business and IT
us-versus-them mentality





podcast:
teams velocity does not equal success - inflated estimates
why vision in team
what intermediate goals
last responsible moments -> learning windows
releasable product increment -> mindset behind devops too
sprint ends with sth tangible - readiness
you need a cross functional teams to achieve that
from scatch to a fully working products. you have one team to handle it all. no waiting. faster problem solving, ownership.
needs mindset shift
to own their work withougt needing manager. moving a way from directing to leading. not micromanaging
transparency. open communication.
constatnly releasable -> fits devops CI/CD
catchs error way earlier
being ok with trying new things
embracing failure. safe env to experiment
valueable data points

conflict resolution: sharing concerns without worrying
disagree
try to things objective, not personal
finding common ground -> 
consencus decision making -> every one has a say
self organizing teams. more engaged more productive
shift mindset
big picture, freedom to make decision, responsible

measuring success
how to use data to get better
metrics that show the 
key value areas kvas
current value: is providing to users right now - customer satisfaction, revenue
unrealized value: potentiall. finding gaps
ability to innovate: how well a team adapts to change.
time to market: speed is key

are you delivering value?
choose the metrics that really matters

use this data to get better: closed loop system
sprint retrospective: totally honest with each other, solving problems. env for people to be safe
continuous improvement

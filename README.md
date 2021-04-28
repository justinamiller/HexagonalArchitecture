# HexagonalArchitecture

A Hexagonal architectural style (ports & adapters) is a variation of the layered architectural style which makes clear the separation between:

* Application: which cotains the rules of the application
* Adapters: which abstract the inputs to the application and the outputs
* Ports: which are the purposeful conversations' between the actor, via the adapter, and the domain model.


The idea of Hexagonal Architecture is to put inputs and outputs at the edges of our design. Business logic should not depend on whether we expose a REST or a GraphQL API, and it should not depend on where we get data from — a database, a microservice API exposed via gRPC or REST, or just a simple CSV file.

The pattern allows for isolating the core logic of the application from outside concerns. Having core logic isolated means that it can easily change data source details without a significant impact or major code rewrites to the codebase.

One of the main advantages in having an app with clear boundaries is the testing strategy — the majority of the tests can verify the business logic without relying on protocols that can easily change.

## Defining the core concepts
Leveraged from the Hexagonal Architecture, the three main concepts that define our business logic are Entities, Repositories, and Interactors.
 * Entities are the domain objects — they have no knowledge of where they’re stored (unlike Active Record in Ruby on Rails or the Java Persistence API).
 * Repositories are the interfaces to getting entities as well as creating and changing them. They keep a list of methods that are used to communicate with data sources and return a single entity or a list of entities. (e.g. UserRepository)
 * Interactors are classes that orchestrate and perform domain actions — think of Service Objects or Use Case Objects. They implement complex business rules and validation logic specific to a domain action (e.g., onboarding a production)

With these three main types of objects, we are able to define business logic without any knowledge or care where the data is kept and how business logic is triggered. Outside of the business logic are the Data Sources and the Transport Layer:

 * Data Sources are adapters to different storage implementations. A data source might be an adapter to a SQL database (an Active Record class in Rails or JPA in Java), an elastic search adapter, REST API, or even an adapter to something simple such as a CSV file or a Hash. A data source implements methods defined on the repository and stores the implementation of fetching and pushing the data.
 * Transport Layer can trigger an interactor to perform business logic. We treat it as an input for our system. The most common transport layer for microservices is the HTTP API Layer and a set of controllers that handle requests. By having business logic extracted into interactors, we are not coupled to a particular transport layer or controller implementation. Interactors can be triggered not only by a controller, but also by an event, a cron job, or from the command line.

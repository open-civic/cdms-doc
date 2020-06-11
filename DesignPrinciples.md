## Microservices to break up monolithic applications (and mindset!)
- Aimed to address numerous woes associated with monolithic applications
- Easier development
- Better performance and scalability
- Better monitoring/testing
- _Spring Boot_ is well suited to make micro-service components with its auto-configuration, dependence management and
bootable jar.
- Containerization and orchestration platform like Kubernetes to reign in the complexity of microservices

## Multitenancy architecture from the ground-up
- Each agency can build a **complete** datasource profile, with shared or **independent** components (RMDS, mongoDB for 
auditing, ElasticSearch for search etc).
- Shared computing resource for economy/efficiency, segregated data for privacy and security
- Dynamic tenant on-boarding/decommissioning without interruption for high service availability
- One model for both on-premise and in-cloud configuration
- Enabled by a configuration datastore:
  - Redis' roles in OpenCivic Cloud:
    1. Datasource repository, for building an agency's datasource profile and its real-time management.
    2. Data storage for distributed (or you may call it centralized) caching service
    3. User session management integrated with Spring Security and Spring Session
    4. Pub/Sub queues for system integration
  - Redis' characteristics and data privacy
    1. Redis is high performant (up to a million read/wirte per second, with a dual-sever setup).
    2. Redis is versatile (offers a useful _data structure_ sever, caching with TTL, as well as a blocking or Pub/Sub 
    queues), which makes it well suited to be our "cloud hub". 
    3. We use Redis only for system and configuration purpose, not user data, with transient cache bound by a configurable TTL.

## Flexible AND performant integration/UI technology with GraphQL
- Flexibility and performance no longer at odds, but complementary, with each other
- Greatly simplified UI development with tailor-made dataset, requested and controlled by the client.
- Normalized object caching on UI made easy (Apollo Client) for responsive UI
- Resolvers on backend work seamlessly with JPA and lazy loading for server performance.
- Structured GraphQL allows for better pattern recognition and organization, fostering more modular code development with Spring AOP.   

## One-Data model with cloud-wide reactive data-binding
- One mutable datastore in RDBMS (the single truth)
- Many incarnations, all synced reactively:
  1. Mongo for auditing/history
  2. Elasticsearch for full-text/global searching
  3. Neo4j for relationship graph
  4. AdHoc report for reporting
  5. web/mobile UI for real-time data visualization
- Subscription in GraphQL for UI notification/binding
- One consistent architecture/mechanics of data flow and coordination, no ad-hoc piecemeal integration.
- Unification is the tool to rein in complexity.
- One redis server (or one configuration of clustered redis servers) defines one topography of _OpenCivic Cloud_.
- Strives for the "eventual data consistency" across the cloud than ubiquitous transactions that are either
unattainable or unnecessary in a micro-service environment.

## An integrated deployment model to foster scalability, dependability and CI/CD
- Kubernetes (a data center OS!) as the target deployment **platform** for UDMS
- Kubernetes service and infrastructure for microservice discovery and load balancing
- Independent scaling of UI, data service, and supporting service components
- Optimized infrastructure utilization with on-demand automatic scaling up (and down)
- QoS with service self-healing and recovery in response to hardware and software malfunction
- Live roll-out (and roll-back) with software updates with no or minimal downtime
- Unified deployment (and CI/CD) model across OpenCivic Hosting, On-premise, Dev/QA/Support environments
- "data center in a workstation" - integrated DevOps to minimize (or eliminate) gaps between DEV/QA/Production 

## Modular development and quality code practice
- Better code organization with AOP (for cross-cutting features like logging, auditing, data synchronization, 
datasource routing etc.)
- Think in _Reactive_ and in _Stream_ for performance (particularly for dealing with large datasets and file uploading)
- Unified data access model with _JPA_ and _Spring Data_ (try not to write SQL anymore)
- Unified One-Data model with cloud-wide binding 
- Make use of modern language features in Java8 to write better code
  1. lamda expression for anonymous functions
  2. Optional to replace null check
  3. Stream API for collection processing
- Unit testing
  1. Make unit tests count, and test-driven-development an ally than a hindrance or an afterthought
  2. Consider to include performance tests
  3. Consider to load real data using our data-manger's versioning feature and/or in-memory/local database
  4. Consider to make best use of our unified deployment model and containerization for portable and repeatable tests
  5. Make use of more flexible and capable test framework like Spock
 
# What is a Microservice?

A monolithic architecture looks similar like this:

![MonolithicArchitecture](img/microservice/monoArch.png)

A Monolith normally contains following functions to implement **all features** of our app:

- Routing
- Middlewares
- Business Logic
- Database access

In contrast a Microservice contains all these functions to implement **one feature!**

So a Microservice Architecture might look like this:

![MicroserviceArchitecture](img/microservice/microArch.png)

Every feature has is own personalized service and they are totally self-contained. So even if one features crashes, the other features are still working.

# Data Management between services

The Data Management is **THE** big problem of microservices, because we want to produce self-contained services there exists some restrictions regarding database access.

![DBMicro](img/microservice/DBMicro.png)

**Why Databse-Per-Service is necessary**

- We want each service to run independently of other services
- Database schema/structure might change unexpectedly (if different teams work on different Microservices)
- Some services might function more efficiently with different types of DB's (sql vs nosql)

# Communication Strategy between Services 

We use two different strategies to communicate between different Microservices.

![DBMicro](img/microservice/sync.png)

**Synchronouse Communication**

![DBMicro](img/microservice/SyncCom.png)
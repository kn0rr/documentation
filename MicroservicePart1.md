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

![sync](img/microservice/sync.png)

## Synchronous Communication

A possible example how synchronous communication may work in a mciroservice environement:

![SyncCom](img/microservice/SyncCom.png)

This leads to the following Pro's and Con's of Synchronous Communication:

![SyncComProsCons.png](img/microservice/SyncComProsCons.png)

The more a Microservice needs to communicate to other Services the more complex the whole architecture might become:

![SyncReq](img/microservice/SyncReq.png)

## Asynchronous Communication

There exists two different ways of asyncronous communcation.

**First Way: Event-Based Communication**

The event-based communication is not a good way for communication because it shares all the downsides of synchronous communcation and has additional downsides (like enhanced complexity).

![Event](img/microservice/event.png)

**Second Way: Event-Based Enhanced**

First of all specify what exactly is necessary for each service to provide the functionality, for example: 

![ServiceD](img/microservice/ServiceD.png)

Then you can use the event-based communication to get changed data into your individual services: 

![Async2](img/microservice/Async2.png)

![Async3](img/microservice/Async3.png)

![Async3](img/microservice/Async4.png)

In this way you make sure, that Service D always has the right data to show the ordered products for each user without relying on other services during the execution of Service D.

![AsyncComProsCons.png](img/microservice/AsyncComProsCons.png)
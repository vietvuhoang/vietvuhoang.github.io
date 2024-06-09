# Disavantage of Micro-services

## Dependency

Using Micro-Services, we will have multiple services work together with complex dependencies and we need to manage the dependency.
Services will communicate toghether via sync and async the methods
- Sync that means when Service A call to Sevice B, the Service A will wait for the response of Service B, the protocol may be HTTPS (REST/SOAP) or GRPC
- Async that means when Service A send a message to Service B, no response will be expected.

When Service A call to Service B by someway, we can see the Service A depends on Service B,  and if Services B going down or being changed, Service A will be impacted.
If we have more services call to other services by someway, the dependency complexities will be increased, and big ball of mud will be occurred, the system could not be well maintained.

## Tracibility

In Microservices, business flow will go through multiple services, this causes we need a traceability system to allow us monitor what happens in the system beside the logging system. Compare with monolithic system, seem we need the logging system is enough to undertand the business workflow on runtime.

## Monitoring

When we have multiple services, that means we need to understand the health of the services, compare to monolithic, we just need to manage only 1 application.

## Cost 

Microservice will be more expensive than monolithic. 
When you have multiple services and multiple instances for each one, that means you need to have more resource to run them (CPU, Memory, disk space, network bandwidth)
In best practice on Microservices, most of services have their own database, so now we have mulltiple database instances instead only one of using monolithic.
With monolithic, in normal state on workload, maybe you need to keep only more than 1 instance of the application (for high avaibility) to run the system, but for Microservices, you always needs to keep for than 1 instances for each service, this cost your cloud resource even you using small configuration of docker container.
And for microservices, if you use docker images to deploy the system, you need to pull multiple images over network, will spend more network cost for deployment.

Beside that, Microservices will require many tools as messaging, tracing... rather than monolithic, so we need to pay more for infrastructure.
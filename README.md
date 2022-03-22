
This part of the course will be served to manage and explore about Docker containers for all microservices for this application, using Zipkin and Sleuth tools for the architecture for this app, with Spring Rabbit framework, the idea is implement a queue for our distributed server between DB and Microservices.

# Part2-Microservices-With-Eureka

Currency Exchange Service
http://localhost:8000/currency-exchange/from/USD/to/INR

Currency Conversion Service
http://localhost:8100/currency-conversion/from/USD/to/INR/quantity/10
http://localhost:8100/currency-conversion-feign/from/USD/to/INR/quantity/10

Can see all server up and running together in Eureka Server: http://localhost:8761/


Zipkin Server
http://localhost:9411/zipkin/

# Some errors solutions

Building a image Currency-Exchange with Naming-Server, I got the follow error>

2022-03-22 11:20:42.963  WARN [currency-exchange,,] 1 --- [nfoReplicator-0] c.n.d.s.t.d.RetryableEurekaHttpClient    : Request execution failed with message: I/O error on POST request for "http://localhost:8761/eureka/apps/CURRENCY-EXCHANGE": Connection refused (Connection refused); nested exception is java.net.ConnectException: Connection refused (Connection refused)
currency-exchange_1  | 2022-03-22 11:20:42.964  WARN [currency-exchange,,] 1 --- [nfoReplicator-0] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_CURRENCY-EXCHANGE/83d181ec3d65:currency-exchange:8000 - registration failed Cannot execute request on any known server

Solution:

1 - I can change the currency-properties file. name of Eureka server with 'naming-server', but here I wld have to build a new image.
 or
2 - I can go to yaml file docker compose and configure the environment variable in currency-exchange service, with property (eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka)
like...
environment:
eureka.client.serviceUrl.defaultZone: http://naming-server:8761/eureka
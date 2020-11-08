# Ordering microservice

#### Starting the microservice:

To start the microservicde system locally, from the project root execute
`docker-compose -f docker/cloud/compose.yml up`

<br>

<p align="center">
<img src="https://github.com/alexvaitsekhovich/images/blob/main/mqdelay.png" width="100%" height="100%" alt="MQ-delay">

<br>

<p align="center">
<img src="https://github.com/alexvaitsekhovich/images/blob/main/ordering-ms.png" width="100%" height="100%" alt="Ordering microservice">


#### Components:

1. [Order API service](https://github.com/alexvaitsekhovich/order-api) - order API, accessible at the port 8080. The list of endpoints is in the project.
2. [Eureka server](https://github.com/alexvaitsekhovich/ordering-eureka-server) - Eureka discovery service,  accessible at the port 8761.
3. [Failover service](https://github.com/alexvaitsekhovich/ordering-failover-service) - Failover service, will be used if the Order API is not reachable. Only one endpoint _'orders-failover'_ is accessible at the port 8093, it shows "Order API is not available" message. Can be extended with cached values for GET request and messaging to Kafka for POST, PATCH and DELETE to be executed as soon as the Order API is reachable again.
4. [Gateway](https://github.com/alexvaitsekhovich/ordering-gateway) - main entry point for the API. Redirects to the Order API or to Failover service is Order API is not reachable.
5. [Configuration server](https://github.com/alexvaitsekhovich/ordering-config-server) - Configuration used by the Order API, accessible at the port 8888
6. [Configuration files](https://github.com/alexvaitsekhovich/ordering-ms-config) - Configuration file, used only for cloud profile.


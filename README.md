1. `com.vivvo.services.support.config-server` - Eureka, Config Server
2. `com.vivvo.services.support.discovery-server` - Eureka Server, Config Client
3. `com.vivvo.services.support.edge-server` - Eureka, Config Client, Zuul
4. `com.vivvo.services.core.maintenance-service` - Eureka, Config Client, Web

## Config-Server
```java
@EnableConfigServer
@EnableDiscoveryClient
```
#### bootstrap.properties
```java
server.port=8888
spring.application.name=config
spring.cloud.config.server.git.uri=file//${user.home}/application-config-demo
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.registryFetchIntervalSeconds=5
```

## Discovery-Server
```java
@EnableEurekaServer
```
#### bootstrap.properties
```java
spring.application.name=discovery
spring.cloud.config.uri=http://localhost:8888
```

## Edge-Server
```java 
@EnableZuulProxy
@EnableDiscoveryClient
```
#### bootstrap.properties
```java
spring.application.name=gateway
spring.cloud.config.discovery.service-id=config
spring.cloud.config.discovery.enabled=true
```

## Maintenance-Service
```java
@EnableDiscoveryClient 
@RestController
```
#### bootstrap.properties
```java
spring.application.name=maintenance
spring.cloud.config.discovery.service-id=config
spring.cloud.config.discovery.enabled=true
```

## Couple ressources:

http://callistaenterprise.se/blogg/teknik/2015/05/20/blog-series-building-microservices/

https://spring.io/guides/tutorials/spring-security-and-angular-js/

http://www.baeldung.com/spring-cloud-bootstrapping

https://spring.io/guides/gs/centralized-configuration/

http://start.spring.io/
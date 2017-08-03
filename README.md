1. `com.vivvo.services.support.config-server` - Eureka, Config Server
2. `com.vivvo.services.support.discovery-server` - Eureka Server, Config Client
3. `com.vivvo.services.support.edge-server` - Eureka, Config Client, Zuul
4. `com.vivvo.services.core.maintenance-service` - Eureka, Config Client, Web

*Config-Server*
`@EnableConfigServer` `@EnableDiscoveryClient`
server-port=8888
spring.application.name=config
spring.clud.config.server.git.uri=file//${user.home}/application-config-demo
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.registryFetchIntervalSeconds=5

*Discovery-Server*
`@EnableEurekaServer`
spring.application.name=discovery
spring.cloud.config.uri=http://localhost:8888

*Edge-Server*
`@EnableZuulProxy` `@EnableDiscoveryClient`
spring.application.name=gateway
spring.cloud.config.discovery.service-id=config
spring.cloud.config.discovery.enabled=true

*Maintenance-Service*
`@EnableDiscoveryClient` `@RestController`
spring.application.name=maintenance
spring.cloud.config.discovery.service-id=config
spring.cloud.config.discovery.enabled=true

Couple ressources:
http://callistaenterprise.se/blogg/teknik/2015/05/20/blog-series-building-microservices/

https://spring.io/guides/tutorials/spring-security-and-angular-js/

http://www.baeldung.com/spring-cloud-bootstrapping

https://spring.io/guides/gs/centralized-configuration/

http://start.spring.io/
# Modifications to Spring PetClinic Microservices

This fork (`kdavenpo/spring-petclinic-microservices`, branch `subject-system`) supplies the **`vets`** service of the starting system for a CS 8674 master's project at Khoury College, Northeastern University. The other half, `clinic-core`, is in `kdavenpo/spring-petclinic`, branch `subject-system`; see its `MODIFICATIONS.md`.

Upstream: [spring-petclinic/spring-petclinic-microservices](https://github.com/spring-petclinic/spring-petclinic-microservices), Apache License 2.0 (see `LICENSE`). The branch starts at tag **`v3.4.1`** (`f9fd559`), which stays untouched and is the project's ground-truth decomposition. Only `spring-petclinic-vets-service` is built and run; the other modules are unused.

**No Java code is changed.** Both commits add settings only, in `spring-petclinic-vets-service/src/main/resources/application-subject.yml` (`--spring.profiles.active=production,subject`):

| Commit | Change |
|---|---|
| `304b4aa` | Run on its own against the shared schema: config server, Eureka and Zipkin turned off; datasource `localhost:3306/petclinic`; `spring.sql.init.mode=never`; port 8083; cache values (ttl 60, heap-size 100) and JPA settings copied from `spring-petclinic-microservices-config`. |
| `04c0877` | Data collection: Tomcat access log to `./logs/access-vets.<date>.log` (same format as `clinic-core`; `%D` is microseconds), and actuator endpoints exposed as in the published config repo, so `GET /actuator/mappings` lists the endpoint. `.gitignore`: `logs/`. |

Endpoint: `GET /vets`.

Run:
```
.\mvnw.cmd -pl spring-petclinic-vets-service -am package
java -jar spring-petclinic-vets-service\target\spring-petclinic-vets-service-3.4.1.jar --spring.profiles.active=production,subject
```

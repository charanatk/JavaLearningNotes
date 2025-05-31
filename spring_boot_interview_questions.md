
# Spring Boot Interview Questions and Answers

## ✅ Beginner Level

### 1. What is Spring Boot?
**Answer:**  
Spring Boot is a project from Spring that simplifies the development of new Spring applications by minimizing configuration and setup. It allows developers to create stand-alone, production-grade Spring applications with minimal effort.

---

### 2. What are the main features of Spring Boot?
**Answer:**
- Auto-configuration
- Standalone applications
- Embedded servers (Tomcat, Jetty, etc.)
- Production-ready features (Actuator)
- No XML configuration

---

### 3. How do you create a Spring Boot application?
**Answer:**  
You can create a Spring Boot application using:
- Spring Initializr (https://start.spring.io)
- Spring CLI
- Manually by setting up Maven/Gradle and adding dependencies

---

### 4. What is `@SpringBootApplication`?
**Answer:**  
It is a convenience annotation that combines:
- `@Configuration`
- `@EnableAutoConfiguration`
- `@ComponentScan`

---

### 5. What is the default server in Spring Boot?
**Answer:**  
**Tomcat** is the default embedded web server in Spring Boot.

---

## 🔁 Intermediate Level

### 6. What is Spring Boot Auto-Configuration?
**Answer:**  
Spring Boot attempts to automatically configure your Spring application based on the dependencies present in the classpath.

---

### 7. What is the use of `application.properties` or `application.yml`?
**Answer:**  
Used to define application-level configuration such as server port, database configuration, logging, etc.

Example:
```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
```

---

### 8. What is Spring Boot Starter?
**Answer:**  
Starters are dependency descriptors that simplify Maven or Gradle configuration.  
Example:  
- `spring-boot-starter-web`
- `spring-boot-starter-data-jpa`

---

### 9. What is Spring Boot DevTools?
**Answer:**  
DevTools provides features for rapid development, like automatic restart, live reload, and configurations for dev environments.

---

### 10. How can you change the default port of a Spring Boot application?
**Answer:**  
By setting it in `application.properties`:

```properties
server.port=9090
```

---

## 🚀 Advanced Level

### 11. What is Spring Boot Actuator?
**Answer:**  
Spring Boot Actuator provides production-ready features like health checks, metrics, environment info, and more.

Example endpoints:
- `/actuator/health`
- `/actuator/metrics`

---

### 12. How do you secure Spring Boot applications?
**Answer:**
- Use Spring Security
- Add authentication/authorization mechanisms
- Configure HTTPS and CSRF protection

---

### 13. How does Spring Boot support Microservices?
**Answer:**
- Simplifies RESTful service development
- Works well with Spring Cloud for service discovery, config, and resilience
- Lightweight and easy to deploy

---

### 14. How do you handle exceptions in Spring Boot REST APIs?
**Answer:**
Using `@ControllerAdvice` with `@ExceptionHandler` for global exception handling.

---

### 15. What is the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?
**Answer:**
All are specializations of `@Component`, but used for specific layers:
- `@Controller` – Web layer
- `@Service` – Service layer
- `@Repository` – Data access layer

---

### 16. How do you connect Spring Boot with a database?
**Answer:**
Add the required JDBC driver and use `spring.datasource.*` properties in `application.properties`. Use Spring Data JPA or JdbcTemplate for interaction.

---

### 17. What is a Spring Boot profile?
**Answer:**
Profiles allow you to configure different environments (dev, test, prod). Use `@Profile` and define `spring.profiles.active=dev` in properties.

---

### 18. What is the use of `CommandLineRunner` and `ApplicationRunner`?
**Answer:**
These interfaces allow code to run at application startup.

```java
@Component
public class StartupRunner implements CommandLineRunner {
    public void run(String... args) {
        // startup logic here
    }
}
```

---

### 19. What is the difference between Spring Boot and Spring MVC?
**Answer:**
Spring Boot is a framework built on top of Spring that makes development faster with auto-configuration, embedded servers, and starters. Spring MVC is a module for building web apps with Spring.

---

### 20. How do you create a custom banner in Spring Boot?
**Answer:**
Create a `banner.txt` file in the `resources` folder.

---


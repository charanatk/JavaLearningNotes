
# Java RESTful Web Services Interview Questions and Answers

## ✅ Beginner Level

### 1. What is a RESTful Web Service?
**Answer:**  
RESTful Web Service is a service based on REST (Representational State Transfer) architecture. It uses standard HTTP methods like GET, POST, PUT, DELETE to perform CRUD operations on resources.

---

### 2. What are the key principles of REST?
**Answer:**
- **Statelessness**
- **Client-server architecture**
- **Cacheability**
- **Uniform interface**
- **Layered system**
- **Code on demand (optional)**

---

### 3. Which HTTP methods are commonly used in REST?
**Answer:**
- **GET** – Retrieve resource  
- **POST** – Create resource  
- **PUT** – Update entire resource  
- **PATCH** – Update partial resource  
- **DELETE** – Delete resource

---

### 4. What is the difference between @RestController and @Controller in Spring?
**Answer:**
- `@Controller` returns views (typically for web apps using JSP/Thymeleaf).  
- `@RestController` is a combination of `@Controller` and `@ResponseBody`, used for REST APIs returning JSON or XML.

---

### 5. How do you consume JSON data in Spring Boot?
**Answer:**
By using `@RequestBody` annotation on a method parameter:

```java
@PostMapping("/user")
public ResponseEntity<?> createUser(@RequestBody User user) {
    // logic here
}
```

---

## 🔁 Intermediate Level

### 6. What are path variables and how are they handled in Spring?
**Answer:**
Path variables are dynamic parts of a URI. In Spring:

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    // logic here
}
```

---

### 7. What is the difference between @RequestParam and @PathVariable?
**Answer:**
- `@RequestParam` is used for query parameters (`?key=value`).  
- `@PathVariable` is used for dynamic URI segments (`/users/{id}`).

---

### 8. How do you handle exceptions in REST APIs?
**Answer:**
Using `@ControllerAdvice` and `@ExceptionHandler`:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

---

### 9. What is HATEOAS in REST?
**Answer:**
HATEOAS (Hypermedia as the Engine of Application State) means that a REST API should return links with responses to guide clients in interacting with the API.

---

### 10. How do you version a REST API?
**Answer:**
Common ways:
- URI versioning: `/api/v1/users`
- Header versioning: `X-API-VERSION: 1`
- Media type versioning: `Accept: application/vnd.company.v1+json`

---

## 🚀 Advanced Level

### 11. How do you secure REST APIs?
**Answer:**
- Use **HTTPS** for transport security  
- Implement **authentication** (Basic, JWT, OAuth2)  
- Use **Spring Security** for method-level access control

---

### 12. Explain idempotency in REST.
**Answer:**
An operation is **idempotent** if multiple identical requests have the same effect as a single request.  
E.g., **GET, PUT, DELETE** are idempotent, while **POST** is not.

---

### 13. What is the role of HTTP status codes in REST APIs?
**Common ones:**
- `200 OK` – Success  
- `201 Created` – Resource created  
- `204 No Content` – Successful, no body  
- `400 Bad Request` – Client error  
- `401 Unauthorized`, `403 Forbidden` – Auth errors  
- `404 Not Found`  
- `500 Internal Server Error`

---

### 14. What is the difference between PUT and PATCH?
**Answer:**
- `PUT` replaces the entire resource.  
- `PATCH` updates partial fields of the resource.

---

### 15. How do you implement pagination in a REST API?
**Answer:**
Via query params:

```
GET /users?page=1&size=10
```

In Spring:

```java
@GetMapping("/users")
public Page<User> getUsers(Pageable pageable) {
    // logic here
}
```

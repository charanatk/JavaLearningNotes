
# Spring Data JPA and SQL Interview Questions and Answers

## ✅ Spring Data JPA

### 1. What is Spring Data JPA?
**Answer:**  
Spring Data JPA is part of the larger Spring Data family. It simplifies the development of JPA-based data access layers by reducing boilerplate code through repositories.

---

### 2. What is the difference between JPA and Hibernate?
**Answer:**
- **JPA** is a specification.
- **Hibernate** is an implementation of JPA.
Spring Data JPA uses JPA APIs, typically backed by Hibernate as the default provider.

---

### 3. What is the role of the `@Entity` annotation?
**Answer:**  
`@Entity` marks a class as a JPA entity, meaning it will be mapped to a database table.

---

### 4. What is the use of `@Id` and `@GeneratedValue`?
**Answer:**
- `@Id` marks the primary key field.
- `@GeneratedValue` defines how the primary key is generated (AUTO, IDENTITY, SEQUENCE, TABLE).

---

### 5. How do you create a Spring Data JPA Repository?
**Answer:**
Extend `JpaRepository` or `CrudRepository`.

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

---

### 6. What is the difference between `CrudRepository` and `JpaRepository`?
**Answer:**
- `CrudRepository` provides basic CRUD operations.
- `JpaRepository` extends `CrudRepository` and adds JPA-specific features like pagination and sorting.

---

### 7. How do you define a custom query in Spring Data JPA?
**Answer:**
Using `@Query` annotation.

```java
@Query("SELECT u FROM User u WHERE u.email = ?1")
User findByEmail(String email);
```

---

### 8. What is the use of `@Modifying` and `@Transactional`?
**Answer:**
- `@Modifying` marks a query method as modifying data (update/delete).
- `@Transactional` is used to wrap operations in a transaction.

---

### 9. How do you handle pagination and sorting in Spring Data JPA?
**Answer:**
Use `Pageable` and `Sort` parameters.

```java
Page<User> findAll(Pageable pageable);
```

---

### 10. What is the N+1 select problem and how to solve it?
**Answer:**
N+1 happens when lazy loading fetches one parent and then runs a query per child.  
Solution: use `fetch join` or `@EntityGraph` to load associations eagerly.

---

## 📚 SQL & Database

### 11. What is normalization?
**Answer:**
Normalization is the process of organizing data to reduce redundancy and improve data integrity through multiple normal forms (1NF, 2NF, 3NF, etc.).

---

### 12. What are indexes and why are they important?
**Answer:**
Indexes speed up data retrieval at the cost of extra writes and storage.

---

### 13. What is a primary key and foreign key?
**Answer:**
- **Primary Key**: Uniquely identifies a record.
- **Foreign Key**: References a primary key in another table.

---

### 14. What is the difference between INNER JOIN, LEFT JOIN, and RIGHT JOIN?
**Answer:**
- **INNER JOIN**: Returns rows with matching keys in both tables.
- **LEFT JOIN**: Returns all rows from the left table, even without matches.
- **RIGHT JOIN**: Returns all rows from the right table, even without matches.

---

### 15. What are transactions in SQL?
**Answer:**
A transaction is a sequence of operations treated as a single unit of work. Follows ACID properties.

---

### 16. What is the difference between DELETE and TRUNCATE?
**Answer:**
- **DELETE**: Removes rows with optional WHERE clause; logs each row.
- **TRUNCATE**: Removes all rows; faster and cannot be rolled back in most databases.

---

### 17. How do you perform a GROUP BY query?
**Answer:**
Used to group rows that have the same values.

```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

---

### 18. What is a subquery?
**Answer:**
A subquery is a query within another query.

```sql
SELECT name FROM employees WHERE department_id IN (SELECT id FROM departments WHERE location = 'NY');
```

---

### 19. How do you create a relationship between tables?
**Answer:**
Using foreign keys and defining relationships like OneToOne, OneToMany, ManyToOne, ManyToMany in JPA.

---

### 20. What is a view in SQL?
**Answer:**
A view is a virtual table based on the result of an SQL query.

```sql
CREATE VIEW active_users AS SELECT * FROM users WHERE status = 'active';
```

---

# OOPS Java Interview Questions and Answers

## 1. What are the four pillars of OOPS?

**Answer:**
- **Encapsulation**: Hiding internal details and exposing functionality (using classes, getters/setters).
- **Inheritance**: Reusing code from existing classes (parent → child relationship).
- **Polymorphism**: Same method behaving differently (overloading and overriding).
- **Abstraction**: Hiding complex implementation details and showing only necessary features (interfaces and abstract classes).

---

## 2. What is Encapsulation in Java?

**Answer:**
Encapsulation means binding data (variables) and methods (functions) together in a class, and restricting direct access to some of the object’s components.

```java
public class Employee {
    private String name;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

---

## 3. What is the difference between Abstraction and Encapsulation?

| Aspect         | Abstraction                                    | Encapsulation                          |
|----------------|------------------------------------------------|----------------------------------------|
| **Purpose**    | Hides complexity, shows only essentials        | Protects data, controls access         |
| **How**        | Using interfaces or abstract classes           | Using access modifiers (private, etc.) |
| **Focus**      | On what an object does                         | On how to protect the object's data    |

---

## 4. What is Inheritance in Java?

**Answer:**
Inheritance allows a class (child) to acquire properties and behaviors (methods) from another class (parent).

```java
class Animal {
    void eat() { System.out.println("This animal eats food."); }
}

class Dog extends Animal {
    void bark() { System.out.println("Dog barks."); }
}
```

---

## 5. What is Polymorphism in Java?

**Answer:**
Polymorphism means the same method name behaves differently based on the context.
- **Compile-time Polymorphism** → Method Overloading
- **Runtime Polymorphism** → Method Overriding

```java
class Animal {
    void sound() { System.out.println("Animal makes a sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Dog barks"); }
}
```

---

## 6. What is Method Overloading and Method Overriding?

| Aspect             | Overloading                                  | Overriding                          |
|--------------------|----------------------------------------------|-------------------------------------|
| **When**           | Same method name, different parameters       | Same method signature, different class |
| **Compile Time / Run Time** | Compile-time                        | Runtime                             |
| **Inheritance**    | Not required                                | Required                            |

---

## 7. Can you achieve Multiple Inheritance in Java?

**Answer:**
- Java **does NOT support multiple inheritance** with classes (to avoid ambiguity — the diamond problem).
- Java **supports multiple inheritance through interfaces**.

```java
interface A { void methodA(); }
interface B { void methodB(); }

class C implements A, B {
    public void methodA() { System.out.println("A"); }
    public void methodB() { System.out.println("B"); }
}
```

---

## 8. What is the difference between Abstract Class and Interface?

| Feature              | Abstract Class                     | Interface                         |
|----------------------|-------------------------------------|-----------------------------------|
| **Methods**          | Can have both abstract and concrete methods | Only abstract methods (Java 8+ allows default/static) |
| **Variables**        | Instance variables allowed         | Only `public static final` constants |
| **Inheritance**      | Single inheritance                 | Multiple inheritance supported    |

---

## 9. What is Constructor Overloading?

**Answer:**
Having **multiple constructors** in a class with different sets of parameters.

```java
public class Person {
    private String name;
    private int age;

    public Person() {}
    public Person(String name) { this.name = name; }
    public Person(String name, int age) { this.name = name; this.age = age; }
}
```

---

## 10. What is the `super` keyword in Java?

**Answer:**
- Refers to the **immediate parent class object**.
- Used to call parent class methods or constructors.

```java
class Animal {
    void eat() { System.out.println("Animal eats"); }
}

class Dog extends Animal {
    void eat() {
        super.eat(); // calls Animal's eat
        System.out.println("Dog eats");
    }
}
```

---

## 11. What is the `this` keyword in Java?

**Answer:**
- Refers to the **current object** inside a method or constructor.
- It is used to avoid confusion between instance variables and parameters.

```java
public class Student {
    private String name;

    public Student(String name) {
        this.name = name;
    }
}
```

---

## 12. What is an Abstract Class in Java?

**Answer:**
- An abstract class cannot be instantiated directly.
- It can contain both **abstract** (without body) and **non-abstract** (with body) methods.

```java
abstract class Vehicle {
    abstract void start();

    void fuel() {
        System.out.println("Vehicle is fueling");
    }
}

class Car extends Vehicle {
    void start() {
        System.out.println("Car starts with a key");
    }
}
```

---

## 13. What is an Interface in Java?

**Answer:**
- Interface is a blueprint of a class.
- It can contain **abstract methods** and **default/static methods** (since Java 8).

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}
```

---

## 14. What is the Diamond Problem in Java?

**Answer:**
- When a class inherits from two classes that have a method with the same signature, it causes ambiguity.
- Java solves this by **not allowing multiple inheritance** with classes.
- It allows multiple inheritance with **interfaces** because the implementing class must override the conflicting method.

---

## 15. What is a Marker Interface in Java?

**Answer:**
- A marker interface is an interface with **no methods or fields**.
- It is used to provide **metadata** to classes.

✅ Example: `Serializable`, `Cloneable` are marker interfaces.

```java
interface Marker {}

class Test implements Marker {
    // no methods to implement
}
```

---

# Serialization Interview Questions and Answers

## 1. What is Serialization in Java?

**Answer:**
Serialization is the process of converting an object's state into a byte stream so that the byte stream can be reverted back into a copy of the object.
This stream can then be saved to a file, sent across a network, or even stored in a database. Later on, this stream of bytes can be used to recreate the exact same Java object, restoring it to its previous state.

## 2. What is Deserialization in Java?

**Answer:**
Deserialization is the process of converting the serialized byte stream back into an object.

## 3. Why is Serialization used in Java?

**Answer:**
- To persist object states (saving to a file or database).
- To send objects over a network (e.g., in RMI, sockets).

## 4. How do you make a Java class Serializable?

**Answer:**
- A class must implement the `java.io.Serializable` interface.
- This is a marker interface (no methods).

```java
import java.io.Serializable;

public class Employee implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int id;
}
```

## 5. What is `serialVersionUID`?

**Answer:**
- It is a unique ID to identify the version of a class.
- It helps during deserialization to verify that the sender and receiver of a serialized object have loaded classes for that object that are compatible.

## 6. What happens if `serialVersionUID` is not declared?

**Answer:**
- JVM will generate one automatically.
- But if the class changes and no matching ID exists, `InvalidClassException` will be thrown during deserialization.

## 7. What is transient keyword in Java?

**Answer:**
- Variables declared as `transient` are **not serialized**.
- Useful when you don't want to save sensitive information.

```java
class User implements Serializable {
    private String name;
    private transient String password;
}
```

## 8. Can static variables be serialized?

**Answer:**
No, static variables belong to the class, not the object, and hence are not serialized.

## 9. Can we serialize a parent class if the child class implements Serializable?

**Answer:**
- Only the fields of the child class will be serialized.
- If the parent class is not serializable, its fields will not be saved unless handled manually.


---

# Garbage Collection, JVM, JDK, and JRE Interview Questions and Answers

## 1. What is Garbage Collection in Java?

**Answer:**
Garbage Collection is the process by which Java programs perform automatic memory management. The Garbage Collector reclaims memory from objects that are no longer reachable.

## 2. How does Garbage Collection work in Java?

**Answer:**
- JVM automatically identifies objects that are no longer used and removes them.
- Common algorithms: Mark and Sweep, Generational GC.

## 3. What are the different parts of JVM memory?

**Answer:**
- **Heap Memory**: Stores objects.
- **Stack Memory**: Stores method calls and local variables.
- **Method Area**: Stores class metadata.
- **Program Counter Register**: Points to current instruction.
- **Native Method Stack**: Supports native methods.

## 4. What are JDK, JRE, and JVM?

| Component | Description |
|-----------|-------------|
| **JVM**   | Java Virtual Machine; runs Java bytecode |
| **JRE**   | Java Runtime Environment; JVM + libraries needed to run Java applications |
| **JDK**   | Java Development Kit; JRE + compilers and tools to develop Java applications |

## 5. What is the difference between JDK, JRE, and JVM?

**Answer:**
- **JVM** is just the engine that runs Java bytecode.
- **JRE** provides libraries + JVM to run programs.
- **JDK** provides JRE + development tools (javac, javadoc, etc).

## 6. What are Garbage Collection roots (GC Roots)?

**Answer:**
GC Roots are special objects that are always reachable and act as starting points for GC algorithms.
Examples:
- Active threads
- Static fields
- Local variables in stack frames

## 7. What are types of Garbage Collectors in Java?

**Answer:**
- Serial GC
- Parallel GC
- CMS (Concurrent Mark Sweep) GC
- G1 (Garbage First) GC
- ZGC and Shenandoah (for low latency)

## 8. How to request Garbage Collection manually?

```java
System.gc();
```
> (Note: This is just a request; JVM may ignore it.)

## 9. What is Minor GC and Major GC?

**Answer:**
- **Minor GC**: Garbage Collection in Young Generation.
- **Major GC** (or Full GC): Garbage Collection in Old Generation (slower and impacts performance).

## 10. What is OutOfMemoryError?

**Answer:**
Occurs when the JVM cannot allocate memory for an object because it has run out of heap space.

---

# Java OOPs Concepts

Object-Oriented Programming (OOP) in Java is a paradigm that uses "objects" to design software. Java follows four main principles of OOP:

## 1. Class and Object

### Class
A class is a blueprint for creating objects. It defines properties and methods.

```java
class Car {
    String color;
    void drive() {
        System.out.println("Car is driving");
    }
}
```

### Object
An object is an instance of a class.

```java
Car myCar = new Car();
myCar.drive();
```

---

## 2. Inheritance

Inheritance allows a class to inherit fields and methods from another class using the `extends` keyword.

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}
```

**Types of Inheritance in Java**:
- Single
- Multilevel
- Hierarchical  
*(Note: Java does not support multiple inheritance with classes directly to avoid ambiguity)*

---

## 3. Encapsulation

Encapsulation means wrapping data (variables) and code (methods) together as a single unit and restricting access to some of the object’s components.

Use of:
- `private` access modifier
- Public getter and setter methods

```java
class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

---

## 4. Polymorphism

Polymorphism means the ability to take many forms.

### Compile-time Polymorphism (Method Overloading)

```java
class MathUtils {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

### Runtime Polymorphism (Method Overriding)

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow");
    }
}
```

---

## 5. Abstraction

Abstraction hides internal implementation and shows only the functionality.

Can be achieved by:
- Abstract classes
- Interfaces

### Abstract Class Example

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}
```

### Interface Example

```java
interface Drawable {
    void draw();
}

class Rectangle implements Drawable {
    public void draw() {
        System.out.println("Drawing Rectangle");
    }
}
```

---

## Access Modifiers in Java

| Modifier   | Class | Package | Subclass | World |
|------------|-------|---------|----------|--------|
| public     | Yes   | Yes     | Yes      | Yes    |
| protected  | Yes   | Yes     | Yes      | No     |
| default    | Yes   | Yes     | No       | No     |
| private    | Yes   | No      | No       | No     |

---

## Conclusion

Java OOPs principles help build modular, maintainable, and reusable code by modeling real-world entities into code.

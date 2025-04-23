# 🚀 Java 8 Features for Beginners

Java 8 introduced many powerful features that made Java programming more expressive, concise, and functional. Here are the most essential ones for beginners:

---

## 1. 🔥 Lambda Expressions
Write functional-style code using concise syntax.

```java
// Before Java 8
new Thread(new Runnable() {
    public void run() {
        System.out.println("Hello");
    }
}).start();

// With Lambda
new Thread(() -> System.out.println("Hello")).start();
```
##2 🧩 Functional Interfaces
A functional interface has exactly one abstract method. It can also have multiple default or static methods.
```java
@FunctionalInterface
interface MyFunction {
    void apply();
}
```
You can use them with lambda expressions or method references.

##3. 🔁 Stream API
The Stream API lets you process collections like Lists and Sets in a functional and readable way.

``java
List<String> names = Arrays.asList("Tom", "Jerry", "Spike");

names.stream()
     .filter(n -> n.startsWith("J"))
     .map(String::toUpperCase)
     .forEach(System.out::println);
 ``` 
##4. ⚙️ Default and Static Methods in Interfaces
Interfaces can now include default method implementations and static methods.

``java
interface MyInterface {
    default void sayHi() {
        System.out.println("Hi");
    }

    static void sayHello() {
        System.out.println("Hello");
    }
}
    ```
##5. 📌 Method References
Method references offer a shorter syntax for calling methods.

``java
List<String> list = Arrays.asList("Apple", "Banana", "Cherry");

// Using lambda
list.forEach(fruit -> System.out.println(fruit));

// Using method reference
list.forEach(System.out::println);
**##6. ❓ Optional Class**
Optional is a container object that may or may not contain a non-null value. It helps avoid NullPointerException.
``java
Optional<String> name = Optional.of("John");

name.ifPresent(System.out::println); // prints "John"

// or provide a default
String result = name.orElse("Default");
```
**##7. 🕒 New Date and Time API**
Java 8 introduced a new java.time package that provides a better and immutable way to handle dates and times.
```java
import java.time.LocalDate;
import java.time.Month;

LocalDate today = LocalDate.now();
LocalDate birthday = LocalDate.of(1990, Month.JANUARY, 1);

System.out.println("Today: " + today);
System.out.println("Birthday: " + birthday);
```
**##✅ Summary**
Java 8 brought modern, functional programming features to Java:

✔ Lambda Expressions

✔ Functional Interfaces

✔ Stream API

✔ Default & Static Methods in Interfaces

✔ Method References

✔ Optional API

✔ New Date & Time API

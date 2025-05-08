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

# Overloading and Overriding Advanced Interview FAQs

## 1. When should you prefer Method Overloading?

**Answer:**
- When you want the **same method name** to perform **similar tasks** but with different input parameters.
- Example: constructors, utility classes like `Math` class.

## 2. When should you prefer Method Overriding?

**Answer:**
- When you want to **change behavior** of a method in the child class.
- Overriding helps in achieving **runtime polymorphism**.

## 3. Can private methods be overridden?

**Answer:**
- ❌ No. Private methods are **not inherited** by subclasses, so they cannot be overridden.

## 4. What happens if you change only the return type during overloading?

**Answer:**
- ❌ It will cause a compilation error.
- You must **change parameters** too for valid overloading.

## 5. Can final methods be overridden?

**Answer:**
- ❌ No. Methods declared as `final` cannot be overridden.

## 6. Can constructors be overloaded and overridden?

**Answer:**
- **Constructors can be overloaded** (different signatures).
- **Constructors cannot be overridden** (they are not inherited).

## 7. What is covariant return type in Java?

**Answer:**
- In method overriding, the return type of the overriding method can be a **subclass** of the return type declared in the original overridden method.

```java
class Animal {}
class Dog extends Animal {}

class Parent {
    Animal getAnimal() { return new Animal(); }
}

class Child extends Parent {
    @Override
    Dog getAnimal() { return new Dog(); }
}
```

--- 
# Wrapper Classes Interview Questions and Answers

## 1. What are wrapper classes in Java?
**Answer:**  
Wrapper classes are used to **wrap primitive data types** (like `int`, `char`, `double`) into **objects**.  
Examples: `Integer`, `Character`, `Double`, etc.

---

## 2. Why do we need wrapper classes?
**Answer:**  
- To use primitives in **collections** (e.g., `ArrayList<Integer>`)  
- For **utility methods** (like parsing Strings to numbers)  
- For **autoboxing/unboxing** (automatic conversion between primitives and objects)

---

## 3. What is autoboxing and unboxing?
**Answer:**  
- **Autoboxing**: Automatically converting a primitive to its wrapper object.  
  Example: `Integer a = 5;` (5 is `int`, automatically boxed into `Integer`)  
- **Unboxing**: Automatically converting a wrapper object to its primitive.  
  Example: `int b = new Integer(10);` (unboxed to `int`)

---

## 4. Name a few commonly used wrapper classes.
**Answer:**  
- `Byte`, `Short`, `Integer`, `Long`  
- `Float`, `Double`  
- `Character`, `Boolean`

---

## 5. Are wrapper classes immutable?
**Answer:**  
Yes, all wrapper classes in Java are **immutable**. Once created, their values **cannot be changed**.

---

## 6. How do you convert a String to a primitive type using wrapper classes?
**Answer:**  
Use parsing methods:  
Example: `int x = Integer.parseInt("123");`

---

## 7. What happens when you compare wrapper objects using `==` and `.equals()`?
**Answer:**  
- `==` checks **reference equality** (whether they are the same object).  
- `.equals()` checks **value equality** (whether they have the same content).

**Special note**: Between `-128` and `127`, Java **caches** Integer objects, so `==` may return true.

Example:
```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);  // true (cached)
Integer c = 200;
Integer d = 200;
System.out.println(c == d);  // false (different objects)
```

---

## 8. What is the default value of a wrapper class?
**Answer:**  
For wrapper **objects** (like `Integer`), the default is `null`, **not 0**.

---

## 9. Can you extend a wrapper class?
**Answer:**  
No. Wrapper classes are **final**. They **cannot be extended**.

---

## 10. What are the differences between `Integer.parseInt()` and `Integer.valueOf()`?
**Answer:**  
- `parseInt(String)` returns a **primitive** `int`.  
- `valueOf(String)` returns an **Integer** object (may use caching).

Example:
```java
int x = Integer.parseInt("123");   // primitive
Integer y = Integer.valueOf("123"); // object
```

---

# String Interview Questions and Answers

## 1. What is the String class in Java?
**Answer:**  
String is a final class that represents an immutable sequence of characters.

---

## 2. Why is String immutable?
**Answer:**  
Security, thread-safety, and performance optimizations like String pooling.

---

## 3. What is the String Pool?
**Answer:**  
String literals are stored in a common pool for reusability.

---

## 4. How to create a String object?
**Answer:**  
Via literals or using the `new` keyword.

---

## 5. Difference between `==` and `.equals()` in Strings?
**Answer:**  
`==` checks reference, `.equals()` checks value.

---

## 6. Can you extend the String class?
**Answer:**  
No. String is final.

---

## 7. Important String methods?
**Answer:**  
`length()`, `charAt()`, `substring()`, `equals()`, `toUpperCase()`, `toLowerCase()`, `trim()`, `replace()`

---

## 8. Difference between StringBuffer and StringBuilder?
**Answer:**  
StringBuffer is synchronized, StringBuilder is not.

---

## 9. Convert String to other types?
**Answer:**  
Use parse methods like `Integer.parseInt()`, etc.

---

## 10. What happens internally in substring()?
**Answer:**  
Creates a new character array from Java 7u6 onward.

---

## 11. How does `intern()` work?
**Answer:**  
Places the string in the String Pool if not already present.

---

## 12. What is the output of `"abc" + 1 + 2`?
**Answer:**  
Output is `abc12`.

---

## 13. What is a mutable alternative to String?
**Answer:**  
StringBuilder or StringBuffer.

---

## 14. Is String thread-safe?
**Answer:**  
Yes, because it’s immutable.

---

## 15. How to reverse a String?
**Answer:**  
Use StringBuilder’s `reverse()` method.

---

## 16. How to check if two Strings are anagrams?
**Answer:**  
Sort and compare or use a frequency counter.

---

## 17. How to split a String?
**Answer:**  
Use `split()` method with a regex.

---

## 18. Difference between `concat()` and `+`?
**Answer:**  
Both do concatenation, `+` is compiled to `StringBuilder` operations.

---

## 19. How are Strings stored in memory?
**Answer:**  
As objects in the heap or String Pool.

---

## 20. How to make String case insensitive?
**Answer:**  
Use `equalsIgnoreCase()` or convert both to lower/upper case.

---

## 21. What happens with `null` in String concatenation?
**Answer:**  
It gets converted to "null".

---

## 22. Can a String be null or empty?
**Answer:**  
Yes, use checks like `s == null || s.isEmpty()`.

---

## 23. What is `String.format()`?
**Answer:**  
Formats a String using format specifiers.

---

## 24. Difference between `substring(0,0)` and `substring(0,1)`?
**Answer:**  
First returns empty String, second returns first character.

---

## 25. What is Unicode in Java Strings?
**Answer:**  
Java Strings use Unicode to support internationalization.

---

## 26. How to remove whitespaces from a String?
**Answer:**  
Use `replaceAll("\\s", "")`.

---

## 27. How to convert char array to String?
**Answer:**  
Use `new String(charArray)`.

---

## 28. How to find occurrences of a character in a String?
**Answer:**  
Loop through and count.

---

## 29. How to join multiple Strings?
**Answer:**  
Use `String.join()` or `StringBuilder`.

---

## 30. What is the effect of `trim()`?
**Answer:**  
Removes leading and trailing spaces.

# String Programming Questions and Answers

## 1. Write a Java program to reverse a String.
**Answer:**
```java
public class ReverseString {
    public static void main(String[] args) {
        String input = "hello";
        String reversed = new StringBuilder(input).reverse().toString();
        System.out.println(reversed);
    }
}
```

---

## 2. Write a Java program to check if a String is a palindrome.
**Answer:**
```java
public class PalindromeCheck {
    public static void main(String[] args) {
        String str = "madam";
        String reversed = new StringBuilder(str).reverse().toString();
        System.out.println(str.equals(reversed));
    }
}
```

---

## 3. Write a Java program to count vowels and consonants in a String.
**Answer:**
```java
public class VowelConsonantCount {
    public static void main(String[] args) {
        String str = "hello world";
        int vowels = 0, consonants = 0;
        str = str.toLowerCase();
        for (char c : str.toCharArray()) {
            if ("aeiou".indexOf(c) != -1) vowels++;
            else if (Character.isLetter(c)) consonants++;
        }
        System.out.println("Vowels: " + vowels);
        System.out.println("Consonants: " + consonants);
    }
}
```

---

## 4. Write a Java program to remove all duplicate characters from a String.
**Answer:**
```java
import java.util.LinkedHashSet;

public class RemoveDuplicates {
    public static void main(String[] args) {
        String str = "programming";
        LinkedHashSet<Character> set = new LinkedHashSet<>();
        for (char c : str.toCharArray()) {
            set.add(c);
        }
        for (char c : set) {
            System.out.print(c);
        }
    }
}
```

---

## 5. Write a Java program to find the first non-repeated character in a String.
**Answer:**
```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatedChar {
    public static void main(String[] args) {
        String str = "swiss";
        Map<Character, Integer> countMap = new LinkedHashMap<>();
        for (char c : str.toCharArray()) {
            countMap.put(c, countMap.getOrDefault(c, 0) + 1);
        }
        for (Map.Entry<Character, Integer> entry : countMap.entrySet()) {
            if (entry.getValue() == 1) {
                System.out.println("First non-repeated character: " + entry.getKey());
                break;
            }
        }
    }
}
```

---

## 6. Write a Java program to check if two Strings are anagrams.
**Answer:**
```java
import java.util.Arrays;

public class AnagramCheck {
    public static void main(String[] args) {
        String str1 = "listen";
        String str2 = "silent";
        char[] a = str1.toCharArray();
        char[] b = str2.toCharArray();
        Arrays.sort(a);
        Arrays.sort(b);
        System.out.println(Arrays.equals(a, b));
    }
}
```

---

## 7. Write a Java program to count the occurrence of each character in a String.
**Answer:**
```java
import java.util.HashMap;
import java.util.Map;

public class CharacterCount {
    public static void main(String[] args) {
        String str = "programming";
        Map<Character, Integer> map = new HashMap<>();
        for (char c : str.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        System.out.println(map);
    }
}
```

---

## 8. Write a Java program to remove a given character from a String.
**Answer:**
```java
public class RemoveCharacter {
    public static void main(String[] args) {
        String str = "hello world";
        char ch = 'l';
        String result = str.replace(Character.toString(ch), "");
        System.out.println(result);
    }
}
```

---

## 9. Write a Java program to find duplicate characters in a String.
**Answer:**
```java
import java.util.HashSet;

public class DuplicateCharacters {
    public static void main(String[] args) {
        String str = "programming";
        HashSet<Character> set = new HashSet<>();
        for (char c : str.toCharArray()) {
            if (!set.add(c)) {
                System.out.println("Duplicate: " + c);
            }
        }
    }
}
```

---

## 10. Write a Java program to check if a String contains only digits.
**Answer:**
```java
public class DigitsOnly {
    public static void main(String[] args) {
        String str = "12345";
        System.out.println(str.matches("\\d+"));
    }
}
```

---

## 11. Write a Java program to remove all vowels from a String.
**Answer:**
```java
public class RemoveVowels {
    public static void main(String[] args) {
        String str = "hello world";
        str = str.replaceAll("[aeiouAEIOU]", "");
        System.out.println(str);
    }
}
```

---

## 12. Write a Java program to convert a String to a char array.
**Answer:**
```java
public class StringToCharArray {
    public static void main(String[] args) {
        String str = "hello";
        char[] chars = str.toCharArray();
        for (char c : chars) {
            System.out.println(c);
        }
    }
}
```

---

## 13. Write a Java program to find the longest substring without repeating characters.
**Answer:**
```java
import java.util.HashSet;

public class LongestUniqueSubstring {
    public static void main(String[] args) {
        String str = "abcabcbb";
        int maxLength = 0;
        String longest = "";
        for (int i = 0; i < str.length(); i++) {
            HashSet<Character> set = new HashSet<>();
            String temp = "";
            for (int j = i; j < str.length(); j++) {
                if (set.contains(str.charAt(j))) break;
                else {
                    set.add(str.charAt(j));
                    temp += str.charAt(j);
                }
            }
            if (temp.length() > maxLength) {
                longest = temp;
                maxLength = temp.length();
            }
        }
        System.out.println("Longest substring: " + longest);
    }
}
```

---

## 14. Write a Java program to capitalize the first letter of each word in a String.
**Answer:**
```java
public class CapitalizeWords {
    public static void main(String[] args) {
        String str = "hello world";
        String[] words = str.split(" ");
        StringBuilder capitalized = new StringBuilder();
        for (String word : words) {
            capitalized.append(Character.toUpperCase(word.charAt(0))).append(word.substring(1)).append(" ");
        }
        System.out.println(capitalized.toString().trim());
    }
}
```

---

## 15. Write a Java program to check if a String is a valid palindrome ignoring special characters.
**Answer:**
```java
public class ValidPalindrome {
    public static void main(String[] args) {
        String str = "A man, a plan, a canal, Panama";
        str = str.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        String reversed = new StringBuilder(str).reverse().toString();
        System.out.println(str.equals(reversed));
    }
}
```

# Java Exception Handling – Interview Questions & Answers

## 1. What is an Exception in Java?
An exception is an event that disrupts the normal flow of the program. It is an object which is thrown at runtime when an error occurs.

## 2. What are the types of Exceptions in Java?
- **Checked Exceptions** – Checked at compile time (e.g., `IOException`, `SQLException`).
- **Unchecked Exceptions** – Checked at runtime (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`).
- **Errors** – Serious issues like `OutOfMemoryError`, usually not handled by applications.

## 3. Difference between `throw` and `throws`?
- `throw` is used to **actually throw** an exception.
- `throws` is used to **declare** exceptions a method may throw.

## 4. What is the purpose of the `finally` block?
It contains code that always executes after the `try` and `catch`, regardless of whether an exception occurred.

## 5. Can we have try block without catch or finally?
No, a `try` block must be followed by either a `catch`, a `finally`, or both.

## 6. What happens if an exception is not handled?
The program terminates, and the JVM prints the stack trace of the exception.

## 7. What is a custom exception and how to create one?
A user-defined exception created by extending `Exception` or `RuntimeException`.

```java
class MyException extends Exception {
    public MyException(String msg) {
        super(msg);
    }
}
```
## 8. What is the difference between `final`, `finally`, and `finalize()`?
- `final`: Used to declare constants, prevent method overriding, and inheritance.
- `finally`: A block that always executes after try/catch, used for cleanup.
- `finalize()`: A method called by the garbage collector before object destruction (now deprecated in Java 9+).

## 9. What is exception chaining?
It is the practice of wrapping one exception within another to preserve the original cause. Useful for debugging complex issues.

```java
throw new Exception("Main exception", originalException);

```

## 10. What is a try-with-resources statement?
Introduced in Java 7, it is used to automatically close resources like files or streams that implement the `AutoCloseable` interface.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // use the resource
}
```

## 11. Can you catch multiple exceptions in a single catch block?
Yes. Java 7 introduced multi-catch to handle different exception types in one block.

```java
catch (IOException | SQLException ex) {
    ex.printStackTrace();
}
```

## 12. Can a finally block override a return statement?
Yes. If a return statement exists in both try and finally, the one in finally will override the others.

```java
public int test() {
    try {
        return 1;
    } finally {
        return 2; // This will be returned
    }
}
```

## 13. What are suppressed exceptions in Java?
In try-with-resources, if an exception is thrown in both try and resource closing, the latter is suppressed and attached to the main exception.

```java
Throwable[] suppressed = primaryException.getSuppressed();
```

## 14. Can you catch Throwable? Should you?
Technically yes, but it's discouraged. `Throwable` includes `Error`s like `OutOfMemoryError` which are not meant to be caught by applications.

## 15. What’s the difference between Error and Exception?
- **Error**: Serious problems that are usually not handled by applications (e.g., JVM crash, memory issues).
- **Exception**: Conditions that a program might want to catch and handle (e.g., I/O errors, invalid input).

## 16. Why should you avoid catching general Exception?
- It masks specific issues.
- Makes debugging difficult.
- Can catch unintended exceptions like `NullPointerException`.

## 17. What’s the role of stack trace in exceptions?
The stack trace helps in debugging by showing the sequence of method calls that led to the exception.


# Try-With-Resources – Interview Questions & Answers

## 1. What is try-with-resources in Java?
Try-with-resources is a try statement that automatically closes resources like files, streams, or sockets that implement the `AutoCloseable` interface.

## 2. When was try-with-resources introduced?
It was introduced in Java 7 to simplify resource management and avoid boilerplate `finally` blocks.

## 3. What are the advantages of try-with-resources?
- Automatic resource management
- Cleaner and more readable code
- No need for explicit `finally` block
- Fewer chances of resource leaks

## 4. Which interface must a resource implement to be used in try-with-resources?
The resource must implement the `AutoCloseable` interface (or `Closeable`, which extends `AutoCloseable`).

## 5. Can you use multiple resources in a single try-with-resources statement?
Yes, multiple resources can be declared in a single statement, separated by semicolons.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"));
     PrintWriter pw = new PrintWriter(new FileWriter("output.txt"))) {
    // Use both resources
}
```

## 6. What happens if an exception is thrown while closing a resource?
The exception thrown while closing is **suppressed** and attached to the primary exception using `getSuppressed()`.

## 7. What are suppressed exceptions?
Exceptions thrown in the `close()` method during try-with-resources are not lost; they are added as suppressed exceptions to the main one.

```java
for (Throwable t : primaryException.getSuppressed()) {
    t.printStackTrace();
}
```

## 8. Can variables declared outside the try-with-resources be used as resources?
Yes, from Java 9 onwards, **effectively final** variables can be used inside the try-with-resources.

```java
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
try (br) {
    // Allowed in Java 9+
}
```

## 9. How is try-with-resources better than finally block?
It ensures that all resources are closed reliably and automatically, while `finally` requires manual closure and is more error-prone.

## 10. What if both try block and close method throw exceptions?
The exception in the try block is thrown, and the one from close is suppressed and added to the primary exception.

## 11. Can custom classes be used in try-with-resources?
Yes, as long as the class implements `AutoCloseable`.

```java
class MyResource implements AutoCloseable {
    public void close() {
        System.out.println("Closing resource");
    }
}
```

## 12. Is try-with-resources compatible with older Java versions?
No. It was introduced in Java 7 and enhanced in Java 9. It is not available in Java 6 or earlier.

## 13. What is the difference between AutoCloseable and Closeable?
- `Closeable` is for IO classes and throws `IOException`.
- `AutoCloseable` is more general and can throw any exception.

## 14. Can we suppress exceptions in try-with-resources manually?
No, suppressed exceptions are handled automatically, but you can access them using `getSuppressed()`.

## 15. Does try-with-resources support custom error logging while closing?
You can override the `close()` method in your resource and log errors manually inside it.


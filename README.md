# JavaCheatSheet_byRDG
Comprehensive Java Cheatsheet by Rahul Dev Ghosh
# Ultimate Core Java Complete Reference — With Examples

---

## 1. Java Basics & Syntax

### JDK, JRE, JVM
- **JVM** — Runs bytecode. Platform-dependent.
- **JRE** — JVM + libraries. Runs Java programs.
- **JDK** — JRE + compiler + dev tools. Used to develop Java programs.

### Program Structure
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```
- `public class Main` — class declaration (filename must match class name)
- `public static void main(String[] args)` — entry point

### Compilation & Execution
```
javac Main.java    // compiles to Main.class (bytecode)
java Main          // JVM executes bytecode
```

### Identifiers, Keywords, Literals
- **Identifiers** — names for variables, methods, classes. Must start with letter, `_`, or `$`.
- **Keywords** — reserved words (`class`, `if`, `int`, `return`, etc.)
- **Literals** — fixed values: `10`, `3.14`, `'A'`, `"hello"`, `true`, `null`

### Data Types
**Primitive:**
| Type    | Size   | Example         |
|---------|--------|-----------------|
| byte    | 1 byte | `byte b = 10;`  |
| short   | 2 bytes| `short s = 100;`|
| int     | 4 bytes| `int i = 1000;` |
| long    | 8 bytes| `long l = 100000L;`|
| float   | 4 bytes| `float f = 3.14f;`|
| double  | 8 bytes| `double d = 3.14;`|
| char    | 2 bytes| `char c = 'A';` |
| boolean | 1 bit  | `boolean b = true;`|

**Reference:** Objects, arrays, strings — store memory addresses.

### Variables & Scope
```java
public class Demo {
    static int classVar = 10;       // static variable — belongs to class
    int instanceVar = 20;           // instance variable — belongs to object

    void method() {
        int localVar = 30;          // local variable — exists only inside method
    }
}
```

### Constants
```java
final double PI = 3.14159;  // cannot be changed after assignment
```

### Type Casting
```java
// Widening (implicit) — small to big
int i = 100;
double d = i;               // 100.0

// Narrowing (explicit) — big to small
double x = 9.78;
int y = (int) x;            // 9
```

### Operators
```java
// Arithmetic
int sum = 10 + 5;           // 15
int mod = 10 % 3;           // 1

// Relational
boolean result = (10 > 5);  // true

// Logical
boolean r = (true && false); // false
boolean s = (true || false); // true

// Bitwise
int a = 5 & 3;              // 1  (0101 & 0011 = 0001)
int b = 5 | 3;              // 7  (0101 | 0011 = 0111)

// Ternary
String res = (10 > 5) ? "Yes" : "No";  // "Yes"

// instanceof
String str = "hello";
boolean check = str instanceof String;  // true
```

### Operator Precedence
Highest to lowest (simplified): `()` → unary → `* / %` → `+ -` → relational → logical → ternary → assignment

### Command-Line Arguments
```java
public class Main {
    public static void main(String[] args) {
        System.out.println(args[0]);  // first argument passed
    }
}
// Run: java Main Hello
// Output: Hello
```

### Pass-by-Value
Java always passes by value. For objects, it passes the **reference value** (copy of address), not the object itself.
```java
void change(int x) {
    x = 100;  // does NOT affect original
}

void change(int[] arr) {
    arr[0] = 100;  // DOES affect original (reference copy points to same array)
}
```

### Numeric Literals (Java 7+)
```java
int million   = 1_000_000;          // underscores for readability
long card     = 1234_5678_9012_3456L;
int hexColor  = 0xFF_EC_D2_9E;

int binary    = 0b1010;             // binary literal  = 10
int hex       = 0xFF;               // hex literal     = 255
int octal     = 017;                // octal literal   = 15
```

---

## 2. Control Flow

### if-else
```java
int x = 10;
if (x > 0) {
    System.out.println("Positive");
} else if (x < 0) {
    System.out.println("Negative");
} else {
    System.out.println("Zero");
}
```

### switch
```java
int day = 3;
switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    case 3: System.out.println("Wed"); break;
    default: System.out.println("Other");
}

// Enhanced switch (Java 14+)
String result = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    case 3 -> "Wed";
    default -> "Other";
};
```

### Loops
```java
// for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// enhanced for-each
int[] nums = {1, 2, 3};
for (int n : nums) {
    System.out.println(n);
}

// while loop
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// do-while — runs at least once
int j = 10;
do {
    System.out.println(j);
    j++;
} while (j < 5);  // prints 10, then exits
```

### Labeled Loops
```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) break outer;   // breaks out of BOTH loops
        System.out.println(i + " " + j);
    }
}
// Output: 0 0
```

### break, continue, return
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;       // exits loop entirely
    if (i % 2 == 0) continue; // skips current iteration
    System.out.println(i);   // prints 1, 3
}

// return — exits the method
int add(int a, int b) {
    return a + b;
}
```

---

## 3. Methods

### Declaration & Invocation
```java
public class Calculator {
    // method declaration
    int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calculator c = new Calculator();
        int result = c.add(5, 3);  // method invocation
        System.out.println(result); // 8
    }
}
```

### Method Overloading — same name, different parameters
```java
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
int add(int a, int b, int c) { return a + b + c; }
```

### Recursion
```java
int factorial(int n) {
    if (n <= 1) return 1;        // base case
    return n * factorial(n - 1);  // recursive call
}
// factorial(5) → 5 * 4 * 3 * 2 * 1 = 120
```

### Varargs
```java
int sum(int... numbers) {     // accepts 0 or more ints
    int total = 0;
    for (int n : numbers) total += n;
    return total;
}
sum(1, 2, 3);     // 6
sum(10, 20);      // 30
sum();            // 0
```

### Static Methods vs Instance Methods
```java
class Demo {
    static void greet() {           // called via class name
        System.out.println("Hello");
    }

    void sayBye() {                 // called via object
        System.out.println("Bye");
    }
}

Demo.greet();          // static — no object needed
new Demo().sayBye();   // instance — needs object
```

---

## 4. OOP Concepts

### Class & Object
```java
class Car {
    String color;
    int speed;

    void drive() {
        System.out.println("Driving at " + speed);
    }
}

Car myCar = new Car();   // object creation using new
myCar.color = "Red";
myCar.speed = 100;
myCar.drive();           // Driving at 100
```

### Constructors
```java
class Student {
    String name;
    int age;

    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy constructor
    Student(Student s) {
        this.name = s.name;
        this.age = s.age;
    }

    // Private constructor — used in Singleton
    // private Student() { }
}
```

### Constructor Chaining
```java
class Employee {
    String name;
    int id;

    Employee() {
        this("Default", 0);  // calls parameterized constructor
    }

    Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }
}
```

### this & super
```java
class Animal {
    String type = "Animal";
    Animal() { System.out.println("Animal constructor"); }
    void sound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    String type = "Dog";

    Dog() {
        super();  // calls Animal constructor — must be first line
    }

    void show() {
        System.out.println(this.type);   // Dog
        System.out.println(super.type);  // Animal
    }

    void sound() {
        super.sound();                   // calls Animal's sound()
        System.out.println("Bark");
    }
}
```

### Encapsulation
```java
class Account {
    private double balance;  // hidden from outside

    public double getBalance() { return balance; }        // getter
    public void setBalance(double b) {                    // setter with validation
        if (b >= 0) this.balance = b;
    }
}
```

### Inheritance
```java
class Vehicle {                    // parent / superclass
    void start() { System.out.println("Vehicle started"); }
}

class Bike extends Vehicle {      // child / subclass
    void ride() { System.out.println("Bike riding"); }
}

Bike b = new Bike();
b.start();  // inherited from Vehicle
b.ride();   // own method

// Types: single, multilevel, hierarchical
// Java does NOT support multiple inheritance via classes (uses interfaces instead)
```

### Polymorphism
```java
// Compile-time (method overloading)
class Calc {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Runtime (method overriding)
class Shape {
    void draw() { System.out.println("Drawing shape"); }
}
class Circle extends Shape {
    void draw() { System.out.println("Drawing circle"); }  // overridden
}

Shape s = new Circle();  // upcasting
s.draw();                // "Drawing circle" — runtime decision
```

### Abstraction
```java
// Abstract class — can have abstract + concrete methods
abstract class Animal {
    abstract void sound();               // no body — subclass MUST implement
    void breathe() { System.out.println("Breathing"); }  // concrete
}

class Cat extends Animal {
    void sound() { System.out.println("Meow"); }
}

// Interface — 100% abstraction (before Java 8)
interface Flyable {
    void fly();                          // implicitly public abstract

    default void glide() {              // default method (Java 8+)
        System.out.println("Gliding");
    }

    static void info() {               // static method (Java 8+)
        System.out.println("Flyable interface");
    }
}

```java
class Bird implements Flyable {
    public void fly() { System.out.println("Bird flying"); }
}
```

### Interface Default Method Conflict (Diamond Problem)
```java
interface A { default void hello() { System.out.println("A"); } }
interface B { default void hello() { System.out.println("B"); } }

class C implements A, B {
    // Must override to resolve conflict
    public void hello() { A.super.hello(); } // explicitly choose A's version
}
```

### Abstract Class vs Interface
| Feature                      | Abstract Class              | Interface (Java 8+)         |
|------------------------------|-----------------------------|-----------------------------|
| Instantiation                | ❌                          | ❌                          |
| Multiple inheritance         | ❌ (single extends)         | ✅ (multiple implements)    |
| Constructors                 | ✅                          | ❌                          |
| Instance fields              | ✅                          | ❌ (only `public static final`) |
| Concrete methods             | ✅                          | ✅ (`default`/`static`)     |
| Abstract methods             | ✅                          | ✅ (implicitly)             |
| Access modifiers on methods  | Any                         | `public` only               |
| Use when                     | Sharing code among related classes | Defining a contract/capability |

### Dynamic Method Dispatch
```java
Animal a = new Cat();   // parent reference, child object
a.sound();              // "Meow" — resolved at runtime
```

### Marker Interfaces
```java
// Interfaces with no methods — serve as a tag
// Serializable, Cloneable, Remote
class Data implements Serializable { }  // marks class as serializable
```

### Association, Aggregation, Composition
```java
// Association — general relationship
class Teacher { }
class Student { }  // Teacher teaches Student

// Aggregation — HAS-A (weak) — child can exist independently
class Department {
    List<Teacher> teachers;  // Department has teachers, but teachers exist without dept
}

// Composition — HAS-A (strong) — child cannot exist without parent
class House {
    private Room room;       // Room cannot exist without House
    House() { room = new Room(); }
}
class Room { }
```

### Upcasting & Downcasting
```java
Animal a = new Dog();          // upcasting — automatic
Dog d = (Dog) a;               // downcasting — explicit, risky

// Safe downcasting
if (a instanceof Dog) {
    Dog d2 = (Dog) a;
}
```

### Covariant Return Types
```java
class Parent {
    Parent get() { return this; }
}
class Child extends Parent {
    Child get() { return this; }  // return type can be subclass — covariant
}
```

### Method Hiding vs Overriding
- **Overriding**: instance method in subclass replaces parent's (runtime polymorphism).
- **Hiding**: if you declare a `static` method with same signature in subclass, the PARENT version is called if accessed via parent reference — this is NOT polymorphism.

```java
class Parent {
    static void staticMethod()   { System.out.println("Parent static"); }
    void instanceMethod()        { System.out.println("Parent instance"); }
}
class Child extends Parent {
    static void staticMethod()   { System.out.println("Child static"); }  // HIDES, not overrides
    void instanceMethod()        { System.out.println("Child instance"); } // overrides
}

Parent p = new Child();
p.staticMethod();    // "Parent static"  — hiding: resolved at compile-time
p.instanceMethod();  // "Child instance" — overriding: resolved at runtime
```

---

## 5. Access Modifiers & Packages

### Access Levels
| Modifier    | Class | Package | Subclass | World |
|-------------|-------|---------|----------|-------|
| `public`    | ✅    | ✅      | ✅       | ✅    |
| `protected` | ✅    | ✅      | ✅       | ❌    |
| default     | ✅    | ✅      | ❌       | ❌    |
| `private`   | ✅    | ❌      | ❌       | ❌    |

### Packages
```java
package com.myapp.utils;      // package declaration — first line

import java.util.ArrayList;   // importing specific class
import java.util.*;            // importing all classes in package
import static java.lang.Math.PI;  // static import

public class Helper {
    double area(double r) {
        return PI * r * r;     // using static import
    }
}
```

### Classpath
```
javac -cp lib/mylib.jar Main.java    // compile with external jar
java -cp .:lib/mylib.jar Main        // run with classpath
```

---

## 6. JVM Architecture & Memory

### Memory Areas
```
┌─────────────────────────────────────────────┐
│ JVM Memory                                  │
├──────────────┬──────────────────────────────┤
│ Heap         │ Objects, instance variables  │
│ Stack        │ Method calls, local vars     │
│ Method Area  │ Class metadata, static vars  │
│ (Metaspace)  │ (replaced PermGen in Java 8) │
│ PC Register  │ Current instruction address  │
│ Native Stack │ Native method calls          │
└──────────────┴──────────────────────────────┘
```

### Stack vs Heap
```java
void method() {
    int x = 10;               // x stored on STACK
    String s = new String("Hi"); // reference 's' on STACK, object "Hi" on HEAP
}
// When method() ends, x and s are popped from stack
// Object "Hi" stays on heap until garbage collected
```
```
  Stack (per-thread)            Heap (shared)
  ┌─────────────────┐          ┌──────────────────────────┐
  │ Frame: main()   │          │  Object: new Dog()       │
  │  args → ────────┼──────→  │  name: "Buddy"           │
  │  dog  → ────────┼──────→  │  age:  3                 │
  ├─────────────────┤          └──────────────────────────┘
  │ Frame: method() │
  │  x = 5          │   (primitives live directly on stack)
  │  y = 10         │
  └─────────────────┘
  (LIFO — grows downward, auto-cleaned on return)
```

### ClassLoader Hierarchy
```
Bootstrap ClassLoader  → loads core Java (rt.jar / java.* classes)
    ↓                    written in NATIVE code (C/C++), not Java itself
Extension ClassLoader  → loads ext/ directory (java.ext.dirs)
    ↓
Application ClassLoader → loads classpath classes (your code + libs)
```
**Delegation Model**: When a class is requested, the ClassLoader first delegates to its *parent*. Only if the parent cannot find the class does the child attempt to load it (parent-first / bootstrap-first principle).  
Custom ClassLoaders (extend `ClassLoader`, override `findClass()`) are used for hot-deploy, plugin systems, and bytecode transformation.

### Garbage Collection
```java
// Objects with no references are eligible for GC
Object obj = new Object();
obj = null;                    // now eligible for GC

System.gc();                   // REQUEST to run GC (not guaranteed)

// finalize() — called before GC collects object (deprecated since Java 9)
// Prefer java.lang.ref.Cleaner API (Java 9+) for cleanup actions:
// Cleaner cleaner = Cleaner.create();
// cleaner.register(obj, () -> System.out.println("Cleaning up"));
protected void finalize() {
    System.out.println("Object being collected");
}
```

**Generational GC — Heap Layout:**
```
┌─────────────────────────── Heap ────────────────────────────┐
│  Young Generation                    │   Old Generation      │
│  ┌────────┬──────────┬──────────┐   │  ┌─────────────────┐ │
│  │  Eden  │Survivor0 │Survivor1 │→→→│  │   Long-lived    │ │
│  │(allocs)│   (S0)   │   (S1)   │   │  │    objects      │ │
│  └────────┴──────────┴──────────┘   │  └─────────────────┘ │
│         Minor GC (frequent)         │  Major/Full GC (rare) │
└─────────────────────────────────────┴───────────────────────┘
        Metaspace (off-heap): class metadata, static variables
```
- **Minor GC** — collects Young Gen (Eden + Survivors); short pause, frequent.
- **Major GC** — collects Old Gen; longer pause, infrequent.
- **Full GC** — collects entire heap + Metaspace; avoid in production.

| Algorithm    | Java default | Notes |
|--------------|--------------|-------|
| Serial GC    | single-core / small heaps | `-XX:+UseSerialGC` |
| Parallel GC  | Java 8 default | throughput-focused, stop-the-world |
| G1 GC        | Java 9+ default | balanced latency/throughput, region-based |
| ZGC          | Java 15+ production | sub-millisecond pauses, scalable |
| Shenandoah   | OpenJDK 15+  | concurrent compaction, low pause |

### Stack Overflow vs OOM
```java
// StackOverflowError — infinite recursion
void infinite() { infinite(); }

// OutOfMemoryError — heap full
List<byte[]> list = new ArrayList<>();
while (true) { list.add(new byte[1000000]); }
```

### Java Memory Model (JMM) & Happens-Before
The JMM defines rules that guarantee **visibility** of changes across threads.  
A **happens-before** relationship means: if action A happens-before action B, all writes by A are visible to B.

Key happens-before rules:
- **Program order**: each action in a thread happens-before the next action in that thread.
- **Monitor lock**: `unlock` of a monitor happens-before every subsequent `lock` of that monitor.
- **Volatile**: a write to a `volatile` field happens-before every subsequent read of that field.
- **Thread start**: `Thread.start()` happens-before any action in the started thread.
- **Thread join**: all actions in a thread happen-before `Thread.join()` returns.
- **Transitivity**: if A h-b B, and B h-b C, then A h-b C.

### JIT Compilation (HotSpot)
```
Source (.java) → Bytecode (.class) → JVM Interpreter → JIT Compiler → Native Machine Code
```
- **C1 (Client compiler)** — fast startup, light optimizations (used for short-lived code).
- **C2 (Server compiler)** — deep optimizations (inlining, escape analysis) for hot paths.
- HotSpot detects "hot" methods (called ≥10 000 times) and compiles them natively.
- `-XX:+PrintCompilation` shows JIT activity. `-Xint` disables JIT (interpreter only).

---

## 7. Initialization & Blocks

### Execution Order
```java
class Demo {
    // 1. Static block — runs ONCE when class is loaded
    static {
        System.out.println("Static block");
    }

    // 2. Instance block — runs EVERY TIME an object is created, BEFORE constructor
    {
        System.out.println("Instance block");
    }

    // 3. Constructor — runs after instance block
    Demo() {
        System.out.println("Constructor");
    }

    public static void main(String[] args) {
        new Demo();
        new Demo();
    }
}
/*
Output:
Static block
Instance block
Constructor
Instance block
Constructor
*/
```

### Use Cases
```java
class Config {
    static Map<String, String> settings;

    // Static block — one-time initialization of static fields
    static {
        settings = new HashMap<>();
        settings.put("env", "production");
        settings.put("debug", "false");
    }

    List<String> logs;

    // Instance block — common initialization shared across all constructors
    {
        logs = new ArrayList<>();
        logs.add("Object created at " + System.currentTimeMillis());
    }
}
```

### Double-Brace Initialization (Anti-pattern)
```java
// Creates anonymous inner class — avoid in production
List<String> list = new ArrayList<>() {{
    add("A");
    add("B");
}};
// Prefer: List.of("A", "B") or Arrays.asList("A", "B")
```

---

## 8. Object Class Deep Dive

Every class in Java implicitly extends `Object`.

```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // equals — compare content, not reference
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person p = (Person) o;
        return age == p.age && name.equals(p.name);
    }

    // hashCode — MUST override if equals is overridden
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    // toString — human-readable representation
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }

    // clone — creates a copy (class must implement Cloneable)
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();  // shallow copy
    }
}

// getClass()
Person p = new Person("Alice", 25);
System.out.println(p.getClass().getName());  // Person

// == vs equals
Person p1 = new Person("Alice", 25);
Person p2 = new Person("Alice", 25);
System.out.println(p1 == p2);       // false — different references
System.out.println(p1.equals(p2));  // true — same content
```

---

## 9. Strings & Internals

### String Pool
```java
String s1 = "Hello";         // stored in String pool
String s2 = "Hello";         // reuses same pool reference
String s3 = new String("Hello"); // creates new object on heap

System.out.println(s1 == s2);      // true — same pool reference
System.out.println(s1 == s3);      // false — different objects
System.out.println(s1.equals(s3)); // true — same content
```

### Immutability
```java
String s = "Hello";
s.concat(" World");         // creates new string, original unchanged
System.out.println(s);      // "Hello"

s = s.concat(" World");     // reassigning reference
System.out.println(s);      // "Hello World"
```

### StringBuilder vs StringBuffer
```java
// StringBuilder — mutable, NOT thread-safe, faster
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
sb.insert(5, ",");
sb.reverse();
sb.delete(0, 3);
System.out.println(sb);

// StringBuffer — mutable, thread-safe (synchronized), slower
StringBuffer sbuf = new StringBuffer("Hello");
sbuf.append(" World");
```

### intern()
```java
String s1 = new String("Hello").intern(); // forces into pool
String s2 = "Hello";
System.out.println(s1 == s2);  // true — both point to pool
```

### Common String Methods
```java
String s = "Hello World";
s.length();              // 11
s.charAt(0);             // 'H'
s.substring(0, 5);       // "Hello"
s.indexOf("World");      // 6
s.contains("World");     // true
s.toUpperCase();         // "HELLO WORLD"
s.toLowerCase();         // "hello world"
s.trim();                // removes leading/trailing spaces
s.replace("World", "Java"); // "Hello Java"
s.split(" ");            // ["Hello", "World"]
s.toCharArray();         // char array
s.isEmpty();             // false
s.startsWith("He");      // true
s.endsWith("ld");        // true
String.valueOf(123);     // "123"
String.format("Hi %s, age %d", "Alice", 25); // "Hi Alice, age 25"
```

### Regular Expressions
```java
import java.util.regex.*;

String text = "My phone is 123-456-7890";
Pattern p = Pattern.compile("\\d{3}-\\d{3}-\\d{4}");
Matcher m = p.matcher(text);
if (m.find()) {
    System.out.println(m.group());  // 123-456-7890
}

// Simple checks
"hello123".matches("[a-z]+\\d+");  // true
"hello world".replaceAll("\\s", "-"); // "hello-world"
```

### String Comparison Pitfalls
| Comparison           | What it checks          | Use for                        |
|----------------------|-------------------------|--------------------------------|
| `==`                 | Reference equality      | ⚠️ Never for string value check |
| `.equals()`          | Content equality        | ✅ Always for string value check |
| `.equalsIgnoreCase()`| Content, case-insensitive | ✅ Case-insensitive check      |
| `.compareTo()`       | Lexicographic order     | ✅ Sorting / ordering          |

```java
String a = new String("hello");
String b = new String("hello");

a == b;              // false — different heap objects
a.equals(b);         // true  — same content
a.compareTo(b);      // 0     — same lexicographic order

// Safe null-first comparison (avoids NPE)
Objects.equals(a, b);           // true (null-safe)
"literal".equals(variable);     // NPE-safe: literal on the left
```

---

## 10. Arrays

### Declaration & Initialization
```java
// Static initialization
int[] nums = {1, 2, 3, 4, 5};

// Dynamic initialization
int[] arr = new int[5];     // all elements default to 0
arr[0] = 10;

// Multi-dimensional
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

// Jagged array — rows of different lengths
int[][] jagged = new int[3][];
jagged[0] = new int[2];
jagged[1] = new int[4];
jagged[2] = new int[1];

// Array of objects
String[] names = new String[3];
names[0] = "Alice";
```

### Array Utilities
```java
import java.util.Arrays;

int[] a = {5, 3, 1, 4, 2};

Arrays.sort(a);                          // [1, 2, 3, 4, 5]
int idx = Arrays.binarySearch(a, 3);     // 2 (index)
Arrays.fill(a, 0);                       // [0, 0, 0, 0, 0]
int[] copy = Arrays.copyOf(a, 3);        // first 3 elements
int[] range = Arrays.copyOfRange(a, 1, 4);
boolean eq = Arrays.equals(a, copy);     // content comparison
System.out.println(Arrays.toString(a));  // pretty print: [0, 0, 0, 0, 0]
System.out.println(Arrays.deepToString(matrix)); // for 2D arrays
```

---

## 11. Generics

### Generic Class
```java
class Box<T> {
    private T value;
    void set(T value) { this.value = value; }
    T get() { return value; }
}

Box<String> strBox = new Box<>();
strBox.set("Hello");
String val = strBox.get();  // no casting needed

Box<Integer> intBox = new Box<>();
intBox.set(42);
```

### Generic Method
```java
<T> void printArray(T[] arr) {
    for (T item : arr) System.out.println(item);
}
```

### Bounded Types
```java
// Upper bound — T must be Number or subclass
<T extends Number> double sum(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}

// Multiple bounds
<T extends Comparable<T> & Serializable> void process(T item) { }
```

### Wildcards
```java
void printList(List<?> list) { }              // unbounded — any type
void printNums(List<? extends Number> list) { } // upper — Number or subclass (read)
void addNums(List<? super Integer> list) { }    // lower — Integer or superclass (write)
```

### Type Erasure
```java
// At compile time: Box<String> → At runtime: Box<Object>
// Generics are erased at runtime — cannot do:
// new T(), T.class, instanceof T

// Unchecked cast warnings can be suppressed when you are certain of type safety:
@SuppressWarnings("unchecked")
<T> T castTo(Object obj) { return (T) obj; }
```

---

## 12. Collections Framework

### Hierarchy
```
Iterable
  └── Collection
        ├── List     (ordered, allows duplicates)
        │     ├── ArrayList
        │     ├── LinkedList
        │     └── Vector → Stack
        ├── Set      (no duplicates)
        │     ├── HashSet
        │     ├── LinkedHashSet
        │     └── TreeSet (sorted)
        └── Queue
              ├── PriorityQueue
              └── Deque → ArrayDeque

Map (separate hierarchy, NOT Collection)
  ├── HashMap
  ├── LinkedHashMap
  ├── TreeMap (sorted)
  ├── Hashtable
  └── ConcurrentHashMap
```

### List
```java
// ArrayList — dynamic array, fast random access, slow insert/delete in middle
ArrayList<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add(1, "C");          // insert at index 1
list.get(0);               // "A"
list.set(0, "Z");          // replace
list.remove("B");          // remove by object
list.remove(0);            // remove by index
list.size();               // size
list.contains("C");        // true

// LinkedList — doubly-linked, fast insert/delete, slow random access
LinkedList<String> ll = new LinkedList<>();
ll.addFirst("A");
ll.addLast("B");
ll.getFirst();
ll.removeLast();
```
```
LinkedList internal structure (doubly-linked nodes):

null ← [prev|"A"|next] ↔ [prev|"B"|next] ↔ [prev|"C"|next] → null
        head                                  tail
```

### Set
```java
// HashSet — no duplicates, no order, O(1) add/remove/contains
HashSet<String> set = new HashSet<>();
set.add("Apple");
set.add("Banana");
set.add("Apple");          // ignored — duplicate
System.out.println(set);   // [Apple, Banana] — unordered

// LinkedHashSet — maintains insertion order
LinkedHashSet<String> lhs = new LinkedHashSet<>();

// TreeSet — sorted (natural ordering or Comparator)
TreeSet<Integer> ts = new TreeSet<>();
ts.add(30); ts.add(10); ts.add(20);
System.out.println(ts);   // [10, 20, 30]
```

### Map
```java
// HashMap — key-value pairs, no order, allows one null key
HashMap<String, Integer> map = new HashMap<>();
map.put("Alice", 90);
map.put("Bob", 85);
map.get("Alice");          // 90
map.containsKey("Bob");    // true
map.remove("Bob");
map.putIfAbsent("Alice", 100); // won't replace existing

// Iterating
for (Map.Entry<String, Integer> e : map.entrySet()) {
    System.out.println(e.getKey() + " = " + e.getValue());
}
map.forEach((k, v) -> System.out.println(k + " = " + v));

// LinkedHashMap — maintains insertion order
// TreeMap — sorted by keys
TreeMap<String, Integer> tm = new TreeMap<>(map);
```

### HashMap Internals
```
- Uses array of buckets (Node[])
- Key → hashCode() → index via (hash & (n-1))
- null keys are stored at bucket index 0
- Collision → linked list → treeify to Red-Black tree when bucket size >= 8
- Default capacity: 16, load factor: 0.75
- Resizes (doubles) when size > capacity * load factor
```

### Queue & Deque
```java
// PriorityQueue — min-heap by default
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(30); pq.offer(10); pq.offer(20);
pq.poll();     // 10 (smallest)
pq.peek();     // 20 (next smallest)

// ArrayDeque — double-ended queue (faster than Stack/LinkedList)
// ⚠️ Prefer ArrayDeque over the legacy Stack class (Stack extends Vector — synchronized/legacy)
ArrayDeque<String> deque = new ArrayDeque<>();
deque.push("A");           // stack: push
deque.push("B");
deque.pop();               // "B" — stack: pop
deque.offerFirst("X");     // queue operations
deque.offerLast("Y");
```
```
Queue — FIFO (First-In, First-Out):
  Enqueue →  [ A | B | C | D ]  → Dequeue
             rear             front
             (offer/add)      (poll/remove)

Stack — LIFO (Last-In, First-Out):
  push →  ┌───┐  ← pop
           │ D │  ← top
           │ C │
           │ B │
           │ A │
           └───┘  ← bottom
```

### Iterator & ListIterator
```java
List<String> list = new ArrayList<>(List.of("A", "B", "C"));

// Iterator — forward only
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String s = it.next();
    if (s.equals("B")) it.remove();  // safe removal during iteration
}

// ListIterator — bidirectional
ListIterator<String> lit = list.listIterator();
while (lit.hasNext()) {
    lit.next();
    lit.add("D");  // can add during iteration
}
```

### Fail-fast vs Fail-safe
```java
// Fail-fast — throws ConcurrentModificationException
List<String> list = new ArrayList<>(List.of("A", "B"));
for (String s : list) {
    list.remove(s);  // ConcurrentModificationException!
}

// Fail-safe — works on a copy, no exception
CopyOnWriteArrayList<String> safeList = new CopyOnWriteArrayList<>(List.of("A", "B"));
for (String s : safeList) {
    safeList.remove(s);  // no exception
}
```

### Comparable vs Comparator
```java
// Comparable — natural ordering, implemented IN the class
class Student implements Comparable<Student> {
    String name; int marks;
    public int compareTo(Student o) {
        return this.marks - o.marks;  // ascending by marks
    }
}
Collections.sort(studentList);  // uses compareTo

// Comparator — external ordering, separate class/lambda
Collections.sort(studentList, (a, b) -> a.name.compareTo(b.name)); // by name
studentList.sort(Comparator.comparingInt(s -> s.marks).reversed()); // descending
// ⚠️ Avoid (this.marks - o.marks) for int comparison — can overflow!
// Use Integer.compare(this.marks, o.marks) instead
```

### Collections Utility Methods
```java
import java.util.Collections;

List<Integer> nums = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9));

Collections.sort(nums);                        // [1, 1, 3, 4, 5, 9]
Collections.sort(nums, Comparator.reverseOrder()); // descending
Collections.reverse(nums);                     // reverses in-place
Collections.shuffle(nums);                     // random order
Collections.min(nums);                         // smallest element
Collections.max(nums);                         // largest element
Collections.frequency(nums, 1);               // count occurrences of 1 → 2

List<String> repeated = Collections.nCopies(3, "Hi"); // ["Hi", "Hi", "Hi"]

// Wrap as unmodifiable (throws UnsupportedOperationException on mutation)
List<Integer> immutable = Collections.unmodifiableList(nums);

// Wrap as synchronized (thread-safe — still need external sync for compound ops)
List<Integer> synced = Collections.synchronizedList(nums);
```

### Special Maps
```java
// EnumMap — keys are enum constants, extremely fast
enum Day { MON, TUE, WED }
EnumMap<Day, String> em = new EnumMap<>(Day.class);
em.put(Day.MON, "Monday");

// WeakHashMap — keys are weak references, GC can collect them
WeakHashMap<Object, String> wm = new WeakHashMap<>();

// IdentityHashMap — uses == instead of equals() for key comparison
IdentityHashMap<String, Integer> im = new IdentityHashMap<>();
```

---

## 13. Exception Handling

### Hierarchy
```
Throwable
  ├── Error (unchecked — JVM issues, don't catch)
  │     ├── StackOverflowError
  │     └── OutOfMemoryError
  └── Exception
        ├── Checked (must handle — IOException, SQLException)
        │     ├── IOException
        │     ├── FileNotFoundException
        │     └── ClassNotFoundException
        └── RuntimeException (unchecked — programming bugs)
              ├── NullPointerException
              ├── ArrayIndexOutOfBoundsException
              ├── ClassCastException
              ├── NumberFormatException
              ├── ArithmeticException
              └── IllegalArgumentException
```

### try-catch-finally
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero: " + e.getMessage());
} catch (Exception e) {            // more general catch AFTER specific
    System.out.println("Error: " + e);
} finally {
    System.out.println("Always executes");  // cleanup code
}
```

### Multi-catch (Java 7+)
```java
try {
    // risky code
} catch (IOException | SQLException e) {
    System.out.println("Error: " + e.getMessage());
}
```

### throw & throws
```java
// throw — manually throw an exception
void validate(int age) {
    if (age < 18) throw new IllegalArgumentException("Too young");
}

// throws — declares that method might throw
void readFile(String path) throws IOException {
    FileReader fr = new FileReader(path);  // may throw FileNotFoundException
}
```

### try-with-resources (Java 7+)
```java
// AutoCloseable resources are closed automatically
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
    System.out.println(line);
}  // br.close() called automatically, even if exception occurs
```

### Custom Exception
```java
class InsufficientFundsException extends Exception {
    private double amount;

    InsufficientFundsException(double amount) {
        super("Insufficient funds: " + amount);
        this.amount = amount;
    }

    double getAmount() { return amount; }
}

// Usage
void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) throw new InsufficientFundsException(amount);
    balance -= amount;
}
```

### Exception Propagation
```java
void method3() { throw new RuntimeException("Error"); }
void method2() { method3(); }  // propagates up
void method1() { method2(); }  // propagates up
// If uncaught, JVM terminates with stack trace
```

---

## 14. Input / Output (I/O)

### Byte Streams — for binary data (images, audio, etc.)
```java
// FileInputStream / FileOutputStream
try (FileInputStream fis = new FileInputStream("input.bin");
     FileOutputStream fos = new FileOutputStream("output.bin")) {
    int data;
    while ((data = fis.read()) != -1) {
        fos.write(data);
    }
}

// BufferedInputStream / BufferedOutputStream — faster with buffer
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("input.bin"));
     BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("output.bin"))) {
    byte[] buffer = new byte[1024];
    int bytesRead;
    while ((bytesRead = bis.read(buffer)) != -1) {
        bos.write(buffer, 0, bytesRead);
    }
}

// DataInputStream / DataOutputStream — read/write primitives
try (DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.bin"))) {
    dos.writeInt(42);
    dos.writeDouble(3.14);
    dos.writeUTF("Hello");
}
try (DataInputStream dis = new DataInputStream(new FileInputStream("data.bin"))) {
    int i = dis.readInt();        // 42
    double d = dis.readDouble();  // 3.14
    String s = dis.readUTF();     // "Hello"
}
```

### Character Streams — for text data
```java
// FileReader / FileWriter
try (FileWriter fw = new FileWriter("output.txt")) {
    fw.write("Hello World\n");
    fw.write("Second line");
}
try (FileReader fr = new FileReader("output.txt")) {
    int ch;
    while ((ch = fr.read()) != -1) {
        System.out.print((char) ch);
    }
}

// BufferedReader / BufferedWriter — most common for text files
try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
    bw.write("Line 1");
    bw.newLine();
    bw.write("Line 2");
}
try (BufferedReader br = new BufferedReader(new FileReader("output.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
}

// PrintWriter — convenient formatted output
try (PrintWriter pw = new PrintWriter(new FileWriter("output.txt"))) {
    pw.println("Hello");
    pw.printf("Name: %s, Age: %d%n", "Alice", 25);
}

// InputStreamReader / OutputStreamWriter — bridge (byte → char)
try (BufferedReader br = new BufferedReader(
        new InputStreamReader(new FileInputStream("file.txt"), "UTF-8"))) {
    System.out.println(br.readLine());
}
```

### Console & User Input
```java
// Scanner — most common for user input
Scanner sc = new Scanner(System.in);
System.out.print("Enter name: ");
String name = sc.nextLine();
System.out.print("Enter age: ");
int age = sc.nextInt();
sc.nextLine();  // consume leftover newline
System.out.print("Enter salary: ");
double salary = sc.nextDouble();
sc.close();

// BufferedReader — faster for large input
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String input = br.readLine();
int num = Integer.parseInt(br.readLine());

// Console — for password input (doesn't work in IDEs)
Console console = System.console();
if (console != null) {
    char[] password = console.readPassword("Enter password: ");
}

// System.out, System.err
System.out.println("Standard output");
System.err.println("Error output");
```

### File Class
```java
File file = new File("test.txt");
file.exists();               // true/false
file.createNewFile();        // creates file
file.mkdir();                // creates directory
file.mkdirs();               // creates nested directories
file.delete();               // deletes file
file.getName();              // "test.txt"
file.getAbsolutePath();      // full path
file.length();               // size in bytes
file.isFile();               // true if file
file.isDirectory();          // true if directory
file.canRead();
file.canWrite();
file.renameTo(new File("renamed.txt"));

// List files in directory
File dir = new File("/path/to/dir");
File[] files = dir.listFiles();
for (File f : files) {
    System.out.println(f.getName());
}
```

### Serialization & Deserialization
```java
// Object → byte stream (save/send)
class Employee implements Serializable {
    private static final long serialVersionUID = 1L; // version control
    String name;
    int id;
    transient String password;  // NOT serialized
}

// Serialize
try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("emp.ser"))) {
    Employee emp = new Employee();
    emp.name = "Alice"; emp.id = 101; emp.password = "secret";
    oos.writeObject(emp);
}

// Deserialize
try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("emp.ser"))) {
    Employee emp = (Employee) ois.readObject();
    System.out.println(emp.name);      // Alice
    System.out.println(emp.password);  // null (transient)
}

// Externalizable — full control over serialization
class Custom implements Externalizable {
    String data;
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(data);
    }
    public void readExternal(ObjectInput in) throws IOException {
        data = in.readUTF();
    }
}
```

### Properties Files
```java
// config.properties:
// db.host=localhost
// db.port=3306

Properties props = new Properties();
try (InputStream is = new FileInputStream("config.properties")) {
    props.load(is);
}
String host = props.getProperty("db.host");     // "localhost"
String port = props.getProperty("db.port");     // "3306"
String missing = props.getProperty("db.user", "root"); // default value

// Save properties
props.setProperty("db.user", "admin");
try (OutputStream os = new FileOutputStream("config.properties")) {
    props.store(os, "Database Config");
}
```

---

## 15. NIO (New I/O)

```java
import java.nio.file.*;

// Path
Path path = Paths.get("src/main/file.txt");
path.getFileName();           // file.txt
path.getParent();             // src/main
path.toAbsolutePath();

// Files utility class
Files.exists(path);
Files.createFile(path);
Files.createDirectories(Paths.get("a/b/c"));
Files.delete(path);
Files.copy(source, target, StandardCopyOption.REPLACE_EXISTING);
Files.move(source, target);

// Read/Write files — simple one-liners
String content = Files.readString(Path.of("file.txt"));         // Java 11+
List<String> lines = Files.readAllLines(Path.of("file.txt"));
byte[] bytes = Files.readAllBytes(Path.of("file.bin"));

Files.writeString(Path.of("file.txt"), "Hello World");          // Java 11+
Files.write(Path.of("file.txt"), List.of("Line1", "Line2"));

// Walk directory tree
Files.walk(Paths.get("src"))
     .filter(Files::isRegularFile)
     .forEach(System.out::println);

// Find files
Files.find(Paths.get("src"), 10,
    (p, attr) -> p.toString().endsWith(".java"))
    .forEach(System.out::println);

// Channels & Buffers (low-level, high-performance)
try (FileChannel channel = FileChannel.open(Path.of("data.txt"), StandardOpenOption.READ)) {
    ByteBuffer buffer = ByteBuffer.allocate(1024);
    while (channel.read(buffer) > 0) {
        buffer.flip();  // switch from write mode to read mode
        while (buffer.hasRemaining()) {
            System.out.print((char) buffer.get());
        }
        buffer.clear();
    }
}
```

---

## 16. Multithreading & Concurrency

### Creating Threads
```java
// Method 1: Extend Thread
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread: " + Thread.currentThread().getName());
    }
}
new MyThread().start();

// Method 2: Implement Runnable (preferred)
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable: " + Thread.currentThread().getName());
    }
}
new Thread(new MyRunnable()).start();

// Method 3: Lambda
new Thread(() -> System.out.println("Lambda thread")).start();

// Method 4: Callable — returns a result
Callable<Integer> task = () -> {
    Thread.sleep(1000);
    return 42;
};
```

### Thread Lifecycle
```
NEW → (start()) → RUNNABLE → (scheduler) → RUNNING
  → BLOCKED/WAITING (synchronized/wait/sleep/join)
  → TERMINATED (run() completes or exception)
```

### start() vs run()
```java
Thread t = new Thread(() -> System.out.println("Running"));
t.start();   // creates new OS thread, executes run() in that new thread
t.run();     // executes run() in the CURRENT thread — no new thread created at all!
// ⚠️ Calling run() directly is a common bug: the code runs but gives NO concurrency benefit
```

### Thread Methods
```java
Thread.sleep(1000);           // pause for 1 second
Thread.yield();               // hint: give other threads a chance
thread.join();                // wait for thread to finish
thread.join(5000);            // wait max 5 seconds
thread.setPriority(Thread.MAX_PRIORITY);  // 1-10, default 5
thread.setDaemon(true);       // daemon thread — dies when main thread dies
thread.isAlive();             // true if started and not yet terminated
```

### Synchronization
```java
class Counter {
    private int count = 0;

    // Synchronized method — only one thread at a time
    // Lock is the current object instance (object-level lock)
    synchronized void increment() { count++; }

    // Synchronized block — finer control (object-level lock on 'this')
    void incrementBlock() {
        synchronized (this) {   // lock on current object
            count++;
        }
    }

    // Class-level lock — locks on the Class object (shared across all instances)
    static synchronized void staticMethod() { }
    // OR equivalent:
    static void staticMethod2() {
        synchronized (Counter.class) { }
    }
    // ⚠️ Object-level and class-level locks are INDEPENDENT — they don't block each other
}
```

### Volatile
```java
class Flag {
    volatile boolean running = true;  // visible to all threads immediately

    void run() {
        while (running) { /* work */ }  // without volatile, might cache and never stop
    }

    void stop() { running = false; }
}
// ⚠️ volatile ensures VISIBILITY but NOT ATOMICITY
// volatile int i; i++; — is still NOT atomic (read + increment + write = 3 steps)
// Use AtomicInteger for atomic compound operations
```

### Inter-thread Communication
```java
class SharedResource {
    private int data;
    private boolean available = false;

    synchronized void produce(int value) throws InterruptedException {
        while (available) wait();      // wait until consumed
        data = value;
        available = true;
        notify();                      // wake up consumer
    }

    synchronized int consume() throws InterruptedException {
        while (!available) wait();     // wait until produced
        available = false;
        notify();                      // wake up producer
        return data;
    }
}
```

### ExecutorService
```java
// Thread pool — reuse threads instead of creating new ones
ExecutorService executor = Executors.newFixedThreadPool(3);

// Submit Runnable
executor.submit(() -> System.out.println("Task 1"));

// Submit Callable — returns Future
Future<Integer> future = executor.submit(() -> 42);
int result = future.get();  // blocks until result available
System.out.println(result); // 42

// ScheduledExecutorService
ScheduledExecutorService ses = Executors.newScheduledThreadPool(1);
ses.schedule(() -> System.out.println("Delayed"), 2, TimeUnit.SECONDS);
ses.scheduleAtFixedRate(() -> System.out.println("Periodic"), 0, 1, TimeUnit.SECONDS);

executor.shutdown();  // always shut down
```

### CompletableFuture
```java
CompletableFuture<String> cf = CompletableFuture
    .supplyAsync(() -> "Hello")              // runs in ForkJoinPool
    .thenApply(s -> s + " World")            // transform result
    .thenApply(String::toUpperCase);         // chain more

System.out.println(cf.get());               // "HELLO WORLD"

// Combine two futures
CompletableFuture<String> f1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> f2 = CompletableFuture.supplyAsync(() -> "World");
CompletableFuture<String> combined = f1.thenCombine(f2, (a, b) -> a + " " + b);
```

### Locks
```java
ReentrantLock lock = new ReentrantLock();

lock.lock();
try {
    // critical section
} finally {
    lock.unlock();  // ALWAYS unlock in finally
}

// ReadWriteLock — multiple readers, single writer
ReadWriteLock rwLock = new ReentrantReadWriteLock();
rwLock.readLock().lock();     // multiple threads can read
rwLock.writeLock().lock();    // exclusive write access
```

### Concurrency Utilities
```java
// CountDownLatch — wait for N tasks to complete
CountDownLatch latch = new CountDownLatch(3);
// In each task: latch.countDown();
latch.await();  // blocks until count reaches 0

// CyclicBarrier — all threads wait for each other
CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("All arrived"));
// In each thread: barrier.await();

// Semaphore — limit concurrent access
Semaphore sem = new Semaphore(3);  // max 3 threads
sem.acquire();  // get permit
// do work
sem.release();  // return permit

// Atomic classes — lock-free thread-safe operations
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet();    // atomic ++
counter.compareAndSet(1, 2);  // CAS operation

AtomicReference<String> ref = new AtomicReference<>("initial");
ref.compareAndSet("initial", "updated");  // atomically swap reference

LongAdder adder = new LongAdder();  // better throughput than AtomicLong under high contention
adder.increment();
adder.add(5);
adder.sum();   // retrieve total
```

### ThreadLocal
```java
ThreadLocal<String> threadLocal = new ThreadLocal<>();
threadLocal.set("Thread-specific data");
String value = threadLocal.get();
threadLocal.remove();  // prevent memory leaks
```

### Deadlock Example
```java
// Thread 1: locks A, then tries B
// Thread 2: locks B, then tries A
// Both wait forever — DEADLOCK

// Prevention techniques:
// 1. Lock ordering  — always acquire locks in a globally consistent order
// 2. tryLock with timeout — use ReentrantLock.tryLock(timeout, unit) and back off
// 3. Lock hierarchy — assign numeric levels; never lock a lower-level lock while holding higher
// 4. Avoid nested locks — minimize holding multiple locks simultaneously
ReentrantLock lockA = new ReentrantLock();
ReentrantLock lockB = new ReentrantLock();
if (lockA.tryLock(1, TimeUnit.SECONDS)) {
    try {
        if (lockB.tryLock(1, TimeUnit.SECONDS)) {
            try { /* critical section */ } finally { lockB.unlock(); }
        }
    } finally { lockA.unlock(); }
}
```

### Java Memory Model (JMM) & Happens-Before (Concurrency)
See **Section 6** for the full JMM explanation. Quick reference:
- `volatile` write → happens-before subsequent `volatile` read of same variable.
- `synchronized` unlock → happens-before any subsequent lock of same monitor.
- Use `volatile` for single-variable visibility; `synchronized`/`Lock` for compound operations.

### Virtual Threads (Java 21)
```java
// Virtual threads are lightweight — millions can exist vs thousands of platform threads
Thread vThread = Thread.ofVirtual().start(() -> {
    System.out.println("Virtual thread: " + Thread.currentThread().isVirtual());
});
vThread.join();

// With ExecutorService
try (ExecutorService exec = Executors.newVirtualThreadPerTaskExecutor()) {
    exec.submit(() -> System.out.println("Task in virtual thread"));
}
// Virtual threads are managed by JVM (carrier threads from a pool)
// Ideal for blocking I/O workloads — no need for async/reactive boilerplate
```

### Common Concurrency Pitfalls
```java
// 1. Spurious wakeups — always use while (not if) around wait()
synchronized (lock) {
    while (!condition) lock.wait();  // ✅ re-checks after wakeup
    // if (!condition) lock.wait(); // ❌ unsafe — may proceed without condition
}

// 2. Double-checked locking — requires volatile for correctness
class Singleton {
    private static volatile Singleton instance;
    static Singleton getInstance() {
        if (instance == null) {                  // first check (no lock)
            synchronized (Singleton.class) {
                if (instance == null) {          // second check (with lock)
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

// 3. Forgetting to release locks (use try-finally)
lock.lock();
try { /* work */ } finally { lock.unlock(); }  // ✅ always released

// 4. Using HashMap in concurrent context — use ConcurrentHashMap instead
// 5. Calling blocking operations inside synchronized — causes other threads to wait
// 6. Thread.stop() / Thread.suspend() — deprecated and unsafe, use flags instead
```

---

## 17. Java 8+ Features

### Lambda Expressions
```java
// Before lambda
Runnable r = new Runnable() {
    public void run() { System.out.println("Hello"); }
};

// With lambda
Runnable r2 = () -> System.out.println("Hello");

// With parameters
Comparator<String> comp = (a, b) -> a.compareTo(b);

// Multi-line
Comparator<String> comp2 = (a, b) -> {
    System.out.println("Comparing");
    return a.compareTo(b);
};
```

### Functional Interfaces
```java
// Predicate — takes T, returns boolean
Predicate<Integer> isEven = n -> n % 2 == 0;
isEven.test(4);  // true

// Function — takes T, returns R
Function<String, Integer> length = s -> s.length();
length.apply("Hello");  // 5

// Consumer — takes T, returns nothing
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Hello");

// Supplier — takes nothing, returns T
Supplier<Double> random = () -> Math.random();
random.get();

// BiFunction — takes T, U, returns R
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
add.apply(3, 4);  // 7

// UnaryOperator — takes T, returns T
UnaryOperator<String> upper = s -> s.toUpperCase();
```

### Streams API
```java
List<String> names = List.of("Alice", "Bob", "Charlie", "David", "Anna");

// Filter + Map + Collect
List<String> result = names.stream()
    .filter(n -> n.startsWith("A"))       // [Alice, Anna]
    .map(String::toUpperCase)             // [ALICE, ANNA]
    .sorted()                             // [ALICE, ANNA]
    .collect(Collectors.toList());

// Intermediate operations (lazy — don't execute until terminal op)
// filter, map, flatMap, sorted, distinct, peek, limit, skip

// Terminal operations (trigger execution)
// collect, forEach, reduce, count, findFirst, findAny, anyMatch, allMatch, noneMatch, toArray

// reduce
int sum = List.of(1, 2, 3, 4, 5).stream()
    .reduce(0, Integer::sum);  // 15

// flatMap — flatten nested collections
List<List<Integer>> nested = List.of(List.of(1, 2), List.of(3, 4));
List<Integer> flat = nested.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList());  // [1, 2, 3, 4]

// Collectors
Map<Character, List<String>> grouped = names.stream()
    .collect(Collectors.groupingBy(n -> n.charAt(0)));
// {A=[Alice, Anna], B=[Bob], C=[Charlie], D=[David]}

String joined = names.stream().collect(Collectors.joining(", "));
// "Alice, Bob, Charlie, David, Anna"

Map<Boolean, List<String>> partitioned = names.stream()
    .collect(Collectors.partitioningBy(n -> n.length() > 3));

// Parallel streams
long count = names.parallelStream()
    .filter(n -> n.length() > 3)
    .count();
```

### Optional
```java
// Avoid NullPointerException
Optional<String> opt = Optional.of("Hello");
Optional<String> empty = Optional.empty();
Optional<String> nullable = Optional.ofNullable(null);

opt.isPresent();              // true
opt.get();                    // "Hello"
opt.ifPresent(System.out::println); // prints "Hello"

String value = nullable.orElse("Default");           // "Default"
String value2 = nullable.orElseGet(() -> "Computed"); // lazy default
String value3 = nullable.orElseThrow(() -> new RuntimeException("Missing"));

Optional<Integer> len = opt.map(String::length);     // Optional[5]
Optional<String> filtered = opt.filter(s -> s.startsWith("H")); // Optional[Hello]
```

### Method References
```java
// Static method reference
Function<String, Integer> parse = Integer::parseInt;

// Instance method reference (specific object)
String str = "Hello";
Supplier<Integer> len = str::length;

// Instance method reference (arbitrary object)
Function<String, String> upper = String::toUpperCase;

// Constructor reference
Supplier<ArrayList<String>> listFactory = ArrayList::new;
Function<String, File> fileFactory = File::new;
```

### Date/Time API (java.time)
```java
LocalDate date = LocalDate.now();               // 2026-03-23
LocalDate birthday = LocalDate.of(2000, 1, 15);
date.getYear();
date.getMonth();
date.getDayOfMonth();
date.plusDays(10);
date.minusMonths(2);

LocalTime time = LocalTime.now();               // 14:30:00
LocalTime t = LocalTime.of(14, 30, 0);

LocalDateTime dateTime = LocalDateTime.now();   // 2026-03-23T14:30:00
ZonedDateTime zoned = ZonedDateTime.now(ZoneId.of("America/New_York"));

Duration duration = Duration.between(t, LocalTime.of(16, 0));
Period period = Period.between(birthday, date);

DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = date.format(fmt);            // "23-03-2026"
LocalDate parsed = LocalDate.parse("23-03-2026", fmt);
```

### var — Local Variable Type Inference (Java 10+)
```java
var list = new ArrayList<String>();  // type inferred as ArrayList<String>
var map  = new HashMap<String, Integer>();
var i    = 42;                       // inferred as int

// Works in for-each and try-with-resources
for (var entry : map.entrySet()) {
    System.out.println(entry.getKey() + "=" + entry.getValue());
}

// var is NOT dynamic — type is fixed at compile time (NOT like JavaScript 'var')
// Cannot use: var x = null; (ambiguous type)
// Cannot use in method signatures or fields
```

### Text Blocks (Java 15+)
```java
// Traditional multi-line string
String json = "{\n  \"name\": \"Alice\",\n  \"age\": 30\n}";

// Text block — readable multi-line string
String jsonBlock = """
        {
          "name": "Alice",
          "age": 30
        }
        """;

// Trailing """ position controls final newline
// Incidental whitespace (common indent) is stripped automatically
String html = """
        <html>
            <body>Hello</body>
        </html>
        """;
```

### Records (Java 16+)
```java
// Records — immutable data carriers, auto-generates constructor, getters, equals, hashCode, toString
record Point(int x, int y) { }

Point p = new Point(3, 4);
p.x();        // 3  — accessor (not getX())
p.y();        // 4
System.out.println(p);  // Point[x=3, y=4]

// Records can have compact constructors for validation
record Range(int min, int max) {
    Range {  // compact constructor — no parameter list
        if (min > max) throw new IllegalArgumentException("min > max");
    }
}

// Records can implement interfaces but cannot extend classes (implicitly extend Record)
record NamedPoint(String name, int x, int y) implements Comparable<NamedPoint> {
    public int compareTo(NamedPoint o) { return this.name.compareTo(o.name); }
}
```

### Sealed Classes (Java 17+)
```java
// Sealed class restricts which classes can extend it
sealed class Shape permits Circle, Rectangle, Triangle { }

final class Circle    extends Shape { double radius; }
final class Rectangle extends Shape { double width, height; }
non-sealed class Triangle extends Shape { }  // Triangle can be freely extended

// Works great with pattern matching switch
String describe(Shape s) {
    return switch (s) {
        case Circle c    -> "Circle r=" + c.radius;
        case Rectangle r -> "Rect " + r.width + "x" + r.height;
        case Triangle t  -> "Triangle";
    };
}
```

### Pattern Matching instanceof (Java 16+)
```java
// Old style
if (obj instanceof String) {
    String s = (String) obj;  // redundant cast
    System.out.println(s.length());
}

// Pattern matching — binding variable declared inline
if (obj instanceof String s) {
    System.out.println(s.length());  // s is available and typed here
}

// Combine with conditions
if (obj instanceof String s && s.length() > 5) {
    System.out.println("Long string: " + s);
}
```

### Switch Expressions & yield (Java 14+)
```java
// Switch expression with arrow labels (no fall-through)
int day = 3;
String name = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Other";
};

// yield — return value from a block in switch expression
String result = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> {
        System.out.println("Weekend!");
        yield "Weekend";   // yield instead of return inside switch block
    }
    default -> "Unknown";
};
```

### Stream Improvements (Java 16+)
```java
// Stream.toList() — Java 16+, returns unmodifiable List (shorter than Collectors.toList())
List<String> names = Stream.of("Alice", "Bob", "Carol").toList();

// Stream.takeWhile / dropWhile (Java 9+)
Stream.of(1, 2, 3, 4, 5)
      .takeWhile(n -> n < 4)    // [1, 2, 3]
      .forEach(System.out::println);

Stream.of(1, 2, 3, 4, 5)
      .dropWhile(n -> n < 3)    // [3, 4, 5]
      .forEach(System.out::println);

// Stream.iterate with predicate (Java 9+)
Stream.iterate(0, n -> n < 10, n -> n + 2)  // [0, 2, 4, 6, 8]
      .forEach(System.out::println);

// Collectors.teeing (Java 12+) — split stream into two collectors, merge results
Map.Entry<Long, Double> stats = Stream.of(1, 2, 3, 4, 5)
    .collect(Collectors.teeing(
        Collectors.counting(),
        Collectors.averagingInt(Integer::intValue),
        Map::entry
    ));
```

---

## 18. Wrapper Classes & Autoboxing

```java
// Autoboxing — primitive → wrapper (automatic)
Integer a = 10;              // int → Integer
Double b = 3.14;             // double → Double

// Unboxing — wrapper → primitive (automatic)
int x = a;                   // Integer → int

// parseInt vs valueOf
int p = Integer.parseInt("123");     // returns primitive int
Integer v = Integer.valueOf("123");  // returns Integer object

// Integer Caching (-128 to 127)
Integer i1 = 127;
Integer i2 = 127;
System.out.println(i1 == i2);       // true — cached

Integer i3 = 128;
Integer i4 = 128;
System.out.println(i3 == i4);       // false — NOT cached
System.out.println(i3.equals(i4));  // true — always use equals for wrappers

// Useful methods
Integer.MAX_VALUE;           // 2147483647
Integer.MIN_VALUE;           // -2147483648
Integer.toBinaryString(10);  // "1010"
Double.isNaN(0.0 / 0);      // true
Character.isDigit('5');      // true
Character.isLetter('A');     // true
Boolean.parseBoolean("true"); // true
```

---

## 19. Keywords & Language Advanced

### static
```java
class MathUtil {
    static int count = 0;          // shared across all objects

    static void increment() {       // called via class name
        count++;
    }

    static {                        // static block — runs once when class loads
        System.out.println("Class loaded");
    }

    // Static nested class
    static class Helper {
        void help() { System.out.println("Helping"); }
    }
}
MathUtil.increment();
MathUtil.Helper h = new MathUtil.Helper();
```

### final
```java
final int X = 10;               // constant — cannot reassign
// X = 20; // ERROR

final class ImmutableClass { }   // cannot be extended
// class Sub extends ImmutableClass { } // ERROR

class Parent {
    final void show() { }        // cannot be overridden
}
```

### transient
```java
class User implements Serializable {
    String name;
    transient String password;   // excluded from serialization
}
```

### volatile
```java
volatile boolean flag = true;    // always read from main memory, not CPU cache
```

### strictfp
```java
strictfp class Calculator {      // ensures consistent floating-point across platforms
    strictfp double compute(double a, double b) { return a * b; }
}
```

### native
```java
public native void nativeMethod();  // implemented in C/C++ via JNI
```

### assert
```java
int age = 15;
assert age >= 18 : "Age must be 18+";  // throws AssertionError if false
// Run with: java -ea Main (enable assertions)
```

---

## 20. Enums

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

Day today = Day.MONDAY;
System.out.println(today);            // MONDAY
System.out.println(today.ordinal());  // 0 (position)

// Iterate
for (Day d : Day.values()) {
    System.out.println(d);
}

// String to enum
Day d = Day.valueOf("FRIDAY");

// Switch with enum
switch (today) {
    case MONDAY: System.out.println("Start of week"); break;
    case FRIDAY: System.out.println("Almost weekend"); break;
}

// Enum with fields, constructors, methods
enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    EARTH(5.976e+24, 6.37814e6);

    private final double mass;
    private final double radius;

    Planet(double mass, double radius) {  // constructor is always private
        this.mass = mass;
        this.radius = radius;
    }

    double surfaceGravity() {
        return 6.67300E-11 * mass / (radius * radius);
    }
}

// Enum implementing interface
interface Printable { void print(); }
enum Color implements Printable {
    RED, GREEN, BLUE;
    public void print() { System.out.println(this.name()); }
}
```

---

## 21. Inner Classes

```java
class Outer {
    int x = 10;

    // 1. Member Inner Class — access outer members
    class Inner {
        void show() { System.out.println("Outer x = " + x); }
    }

    // 2. Static Nested Class — no access to outer instance members
    static class StaticNested {
        void show() { System.out.println("Static nested"); }
    }

    void method() {
        // 3. Local Inner Class — defined inside a method
        class LocalInner {
            void show() { System.out.println("Local inner"); }
        }
        new LocalInner().show();

        // 4. Anonymous Inner Class — no name, one-time use
        Runnable r = new Runnable() {
            public void run() { System.out.println("Anonymous"); }
        };
        r.run();
    }
}

// Usage
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();          // member inner
Outer.StaticNested sn = new Outer.StaticNested(); // static nested
```

---

## 22. Reflection API

```java
import java.lang.reflect.*;

class Person {
    private String name = "Alice";
    public int age = 25;
    public void greet() { System.out.println("Hi, I'm " + name); }
    private void secret() { System.out.println("Secret method"); }
}

// Get Class object
Class<?> clazz = Class.forName("Person");
// OR: Person.class
// OR: new Person().getClass()

// Inspect fields
Field[] fields = clazz.getDeclaredFields();
for (Field f : fields) {
    System.out.println(f.getName() + " : " + f.getType());
}

// Access private field
Person p = new Person();
Field nameField = clazz.getDeclaredField("name");
nameField.setAccessible(true);  // bypass private
String val = (String) nameField.get(p);  // "Alice"
nameField.set(p, "Bob");                 // change private field

// Invoke methods
Method greet = clazz.getMethod("greet");
greet.invoke(p);

---

## 23. Common Pitfalls

### == vs equals() for Strings and Wrappers
```java
String a = new String("hello");
String b = new String("hello");
a == b;          // false — different heap objects
a.equals(b);     // true  — same content ✅

Integer x = 200;
Integer y = 200;
x == y;          // false — outside cache range (-128 to 127), new objects created
x.equals(y);     // true  ✅
```

### Integer Cache Trap (-128 to 127)
```java
Integer i1 = 127;  Integer i2 = 127;
i1 == i2;   // true  — JVM caches integers in [-128, 127]

Integer i3 = 128;  Integer i4 = 128;
i3 == i4;   // false — outside cache, new Integer objects allocated
i3.equals(i4);  // true ✅ — always use equals() for wrapper comparison
```

### Mutable Objects as HashMap Keys
```java
class Key { int id; }
Key k = new Key(); k.id = 1;
Map<Key, String> map = new HashMap<>();
map.put(k, "one");

k.id = 2;               // ⚠️ mutating key changes its hashCode
map.get(k);             // null! — wrong bucket, contract broken
// Use immutable keys (String, Integer, records)
```

### ConcurrentModificationException
```java
List<String> list = new ArrayList<>(List.of("A", "B", "C"));
for (String s : list) {
    if (s.equals("B")) list.remove(s);  // ❌ ConcurrentModificationException
}

// Fix 1: use Iterator.remove()
Iterator<String> it = list.iterator();
while (it.hasNext()) { if (it.next().equals("B")) it.remove(); }

// Fix 2: use removeIf (Java 8+)
list.removeIf(s -> s.equals("B"));  // ✅
```

### String Concatenation in Loops
```java
// ❌ Creates a new String object on every iteration — O(n²) memory
String result = "";
for (int i = 0; i < 10000; i++) result += i;

// ✅ StringBuilder — single mutable buffer — O(n)
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) sb.append(i);
String result2 = sb.toString();
```

### NullPointerException from Unboxing
```java
Integer value = null;
int x = value;     // ❌ NullPointerException — unboxing null triggers NPE

// Fix: null check before unboxing
int x = (value != null) ? value : 0;
// Or use Optional<Integer>
```

### float/double Precision (Use BigDecimal for Money)
```java
System.out.println(0.1 + 0.2);   // 0.30000000000000004 — floating-point imprecision

// ✅ Use BigDecimal for exact decimal arithmetic
BigDecimal a = new BigDecimal("0.1");
BigDecimal b = new BigDecimal("0.2");
System.out.println(a.add(b));   // 0.3 — exact
// ⚠️ Never use: new BigDecimal(0.1) — the double 0.1 is already imprecise
```

### Swallowing Exceptions Silently
```java
// ❌ Exception is hidden — bugs become impossible to diagnose
try {
    riskyOperation();
} catch (Exception e) {
    // empty catch — swallowed silently
}

// ✅ Always log or rethrow
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Operation failed", e);  // log
    throw new RuntimeException("Operation failed", e);  // or rethrow with context
}
```

### static Fields Are Shared Across All Instances
```java
class Counter {
    static int count = 0;  // shared by ALL instances
    Counter() { count++; }
}
new Counter(); new Counter(); new Counter();
System.out.println(Counter.count);  // 3 — not per-instance!
// Use instance fields if you need per-object state
```

### switch Fall-Through / Missing break
```java
int day = 2;
switch (day) {
    case 1: System.out.println("Mon");  // missing break!
    case 2: System.out.println("Tue");  // missing break!
    case 3: System.out.println("Wed"); break;
}
// Prints: Tue AND Wed — fall-through from case 2 to case 3

// ✅ Prefer switch expressions (Java 14+) — no fall-through by default
String name = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    case 3 -> "Wed";
    default -> "Other";
};
```
---

## 24. Naming Conventions

Java naming conventions follow a set of widely adopted rules (Oracle/Google style). They make code readable and consistent.

---

### Classes & Abstract Classes
- **Style:** `PascalCase` (UpperCamelCase) — every word starts with a capital letter.
- **Rule:** Use a noun or noun phrase. Abstract classes may be prefixed with `Abstract`.
```java
class BankAccount {}
class LinkedList {}
abstract class AbstractShape {}
```

---

### Interfaces
- **Style:** `PascalCase`
- **Rule:** Use an adjective (ability/contract) or noun. Prefer `-able` suffix for capability interfaces.
```java
interface Runnable {}
interface Serializable {}
interface PaymentGateway {}
```

---

### Methods
- **Style:** `camelCase` — first word lowercase, subsequent words capitalized.
- **Rule:** Use a verb or verb phrase describing the action.
```java
void calculateTax() {}
String getUserName() {}
boolean isActive() {}
```

---

### Variables (Local & Instance)
- **Style:** `camelCase`
- **Rule:** Use a meaningful noun. Single-letter names only for short-lived loop counters.
```java
int totalAmount = 0;
String firstName = "Rahul";
for (int i = 0; i < 10; i++) { }  // 'i' is acceptable here
```

---

### Constants (`static final`)
- **Style:** `UPPER_SNAKE_CASE` — all uppercase with underscores between words.
```java
static final int MAX_SIZE = 100;
static final double PI = 3.14159;
static final String DEFAULT_CURRENCY = "INR";
```

---

### Packages
- **Style:** All lowercase, no underscores. Use reverse domain name as prefix.
- **Rule:** Each segment should be a single lowercase word.
```java
package com.company.project.module;
package org.apache.commons.lang;
```

---

### Enums (Type & Constants)
- **Type name:** `PascalCase` (same as a class).
- **Enum constants:** `UPPER_SNAKE_CASE`.
```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

enum HttpStatus {
    OK, NOT_FOUND, INTERNAL_SERVER_ERROR
}
```

---

### Generic Type Parameters
- **Style:** Single uppercase letter (or short uppercase name for clarity).

| Letter | Conventional meaning        |
|--------|-----------------------------|
| `T`    | Type (general purpose)      |
| `E`    | Element (collections)       |
| `K`    | Key (maps)                  |
| `V`    | Value (maps)                |
| `N`    | Number                      |
| `R`    | Return type (functions)     |
| `S`,`U`,`W` | Additional type params |

```java
class Box<T> {}
class Pair<K, V> {}
<T extends Comparable<T>> T max(T a, T b) { return a.compareTo(b) > 0 ? a : b; }
```

---

### Annotations
- **Style:** `PascalCase` (same as a class/interface).
```java
@interface NotNull {}
@interface Deprecated {}   // built-in example
@interface RequestMapping {}
```

---

### Getters & Setters
- **Getter:** prefix `get` + `PascalCase` field name. For `boolean` fields, use `is` prefix.
- **Setter:** prefix `set` + `PascalCase` field name.
```java
private String name;
private boolean active;

public String getName() { return name; }          // getter
public void setName(String name) { this.name = name; } // setter
public boolean isActive() { return active; }      // boolean getter
public void setActive(boolean active) { this.active = active; }
```

---

### Boolean Variables & Methods
- **Rule:** Name them so they read like a yes/no question. Use prefixes: `is`, `has`, `can`, `should`, `was`, `will`.
```java
boolean isLoggedIn = true;
boolean hasPermission = false;
boolean canEdit() { return role.equals("ADMIN"); }
boolean shouldRetry = attempts < 3;
```

---

### Factory & Builder Methods (Common Conventions)
| Pattern          | Method name examples                          |
|------------------|-----------------------------------------------|
| Static factory   | `of()`, `from()`, `valueOf()`, `parse()`      |
| Instance factory | `create()`, `newInstance()`, `getInstance()`  |
| Builder pattern  | `builder()`, `build()`                        |
| Conversion       | `toList()`, `toString()`, `asMap()`           |

```java
Optional.of("value");
Integer.valueOf(42);
LocalDate.parse("2026-01-01");
List.of(1, 2, 3);
```

---

### Records (Java 16+)
- **Style:** `PascalCase` (same as a class).
- **Accessor methods:** automatically generated as the **field name itself** (no `get` prefix).
```java
record Point(int x, int y) {}
// Accessors: point.x()  point.y()   (NOT getX() / getY())

record UserProfile(String name, int age) {}
```

---

### Quick Reference Summary

| Element             | Convention          | Example                   |
|---------------------|---------------------|---------------------------|
| Class               | `PascalCase`        | `BankAccount`             |
| Interface           | `PascalCase`        | `Serializable`            |
| Abstract Class      | `PascalCase`        | `AbstractShape`           |
| Method              | `camelCase`         | `calculateTax()`          |
| Variable            | `camelCase`         | `totalAmount`             |
| Constant            | `UPPER_SNAKE_CASE`  | `MAX_SIZE`                |
| Package             | `lowercase`         | `com.company.module`      |
| Enum type           | `PascalCase`        | `Day`                     |
| Enum constant       | `UPPER_SNAKE_CASE`  | `MONDAY`                  |
| Generic parameter   | Single uppercase    | `T`, `E`, `K`, `V`        |
| Annotation          | `PascalCase`        | `NotNull`                 |
| Record              | `PascalCase`        | `Point`                   |
| Boolean variable    | `is`/`has`/`can`+camelCase | `isActive`        |

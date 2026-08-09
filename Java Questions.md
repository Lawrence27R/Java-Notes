**What is a base Class:**

A base class is a class whose properties and methods are inherited by another class.

It is also commonly called a superclass or parent class.

class Animal { --parent

&#x20;   void eat() {

&#x20;       System.out.println("This animal eats food.");

&#x20;   }

}

class Dog extends Animal { --child

&#x20;   void bark() {

&#x20;       System.out.println("The dog barks.");

&#x20;   }

}

A base class allows you to:

Reuse common code.

Avoid duplication.

Create a hierarchy of related classes.

Support polymorphism.



**Which is parent class of all classes in java and how many methods does it has:**

The parent class of all classes in Java is: Object

Every class in Java directly or indirectly extends Object.

The Object class provides 11 methods (some overloaded):

Why is Object class parent of all classes?

Because Java needs common methods (equals, hashCode, toString, etc.) available to every object.



**Java Main Method:**

1\. Can static be written before public?

Yes.

In Java, the order of modifiers (like public, static, final, abstract, etc.) generally does not matter. The compiler treats them the same.



2\. Can we change the return type (void)?

Yes, but with a condition.

The JVM looks specifically for this signature:

the code compiles, but when you try to run the class, you'll get an error similar to:



3\. Can we change the parameter?

The JVM accepts:



4\. Can we overload the main() method?

Yes.

JVM Specifically looks for public static void main(String args\[]) or String\[] args



5\. Can main() be overridden?

No.

main() is static.

Static methods belong to the class, not the object.



6\. Can main() be non-static?

No.

no object of your class has been created yet.

A static method belongs to the class, not to an instance (object), so the JVM can invoke it directly.

Compilation succeeds, but running the class fails because the JVM requires a public static void main(String\[] args) method.



7\. Can main() be private?

It compiles, but the JVM cannot access it.

Error: Main method not found in class



8\. Can main() be final?

Yes.



9\. Can main() be synchronized?

Yes.



10\. Can main() throw exceptions?

Yes.



**REST API:**

GET     → "Give me something"

POST    → "Here is something / perform this action"

PUT     → "Replace this resource with this version"

PATCH   → "Change part of this resource"

DELETE  → "Remove this resource"



Because sometimes we need to send a lot of information to tell the server what data we want. Complex Search

Get Expose the complex query search in the url

POST is used for updating when the API is designed that way. It's not because PUT cannot update data.



java.util.function

filter() → Predicate

forEach() → Consumer

Stream.generate() → Supplier

**Predicate<T>:**

A Predicate is a functional interface that accepts one input and returns a boolean value.

It is mainly used for filtering or testing conditions.

Validate age

Check email format



**Consumer<T>:**

A Consumer accepts one input and does not return any value.

It is mainly used for performing actions such as printing, logging, saving data, or updating values.

Send email

Save audit logs



**Supplier<T>:**

A Supplier does not take any input but returns a value.

It is mainly used when data needs to be generated or fetched on demand.

Generate OTP

Generate UUID

Fetch current timestamp



**Function<T, R>:**

A Function accepts one input and returns one output.

It is commonly used for mapping or converting one type of object into another.

Returns any type



**BiFunction<T, U, R>:**

A BiFunction accepts two inputs and returns one output.



Predicate → Checks → Returns true/false.

Consumer → Consumes → Takes input, returns nothing.

Supplier → Supplies → No input, returns a value.

Function → Transforms → One input → One output.

BiFunction → Transforms using two inputs → Two inputs → One output.



**We want to use an Employee object as a key in a HashMap. Which methods should we override and why?**

A HashMap uses these methods internally:

hashCode()

Determines which bucket the key should be stored in.

If two objects represent the same employee, they must return the same hash code.

equals()

Used to compare keys within the same bucket.

Determines whether two keys are actually equal.



If we return 1 in hashcode():

This means every Employee object has the same hash code.



Is e2.equals(e1)?  -> false

Is e2.equals(e2)?  -> true

So it still works, provided equals() is implemented correctly.

Worst case O(n)



**BeanFactory:**

BeanFactory is the basic IoC container provided by Spring.

It is responsible for:

Creating beans

Managing bean lifecycle

Performing Dependency Injection

Lightweight

Suitable for simple applications



**ApplicationContext:**

ApplicationContext is an advanced IoC container that extends BeanFactory.

Eager initialization for singleton beans by default

Dependency Injection + Enterprise features

Most commonly used in Spring Boot





**What is @Transactional?**

@Transactional tells Spring that a method should execute inside a database transaction.

A transaction follows the ACID properties:

Atomicity – All operations succeed or all fail.

Consistency – Database remains valid.

Isolation – Concurrent transactions don't interfere.

Durability – Once committed, data is permanently stored.

**If anything fails rollback everything.**

Spring does not modify your class directly.

Instead it creates a Proxy.

JDK Dynamic Proxy → Interface exists

Method Called

↓

Begin Transaction

↓

Execute SQL

↓

Flush

↓

Commit

↓

Close Connection

By default it doesn't rollback for Checked Exception

Force Rollback @Transactional(rollbackFor = Exception.class)

No Rollback for @Transactional(noRollbackFor = ArithmeticException.class)

Even if exception occurs

Transaction commits.



**Propagation**

**REQUIRED:**

If transaction exists

Reuse it.

Else

Create new.

**REQUIRES\_NEW**

Always create a new transaction.

**NOT\_SUPPORTED**

Suspend transaction.

@Transactional(timeout = 5)

Rollback if method exceeds 5 seconds.

Not in a single transaction.

A transaction is atomic. If all three operations are in the same transaction, they either all commit or all roll back.

**If you want to commit/save that method you need to create a separate transaction of that method you cannot save it within the same transaction.**

It uses Spring AOP proxies. The proxy starts a transaction before invoking the method, commits it if the method completes successfully, or rolls it back based on the rollback rules if an exception occurs.

Doesn't work on private and static method:

Because proxies intercept external method calls. Private methods cannot be overridden or intercepted by the proxy.

No. Static methods are not invoked on the Spring-managed bean instance, so the proxy cannot intercept them.



**AOP (Aspect-Oriented Programming)** is a programming paradigm used to separate cross-cutting concerns from your business logic. @Aspect

Logging

Security

Transactions

Exception Handling

Instead of writing this code repeatedly, Spring applies it automatically.

**What is a Proxy?**

A Proxy is an object that sits between the client and the actual object.

The proxy can:

Check security

Start transaction

Log request

Measure execution time

Handle exceptions

before calling the actual method.

**@Transactional**

Used for database transaction management.

If exception occurs:

Rollback transaction

Spring creates proxy around method.

@Transactional ensures that a group of database operations either all succeed or all fail together.

Transaction Propagation Types

| Type         | Meaning                   |

| ------------ | ------------------------- |

| REQUIRED     | Default                   |

| REQUIRES\_NEW | New transaction           |

| SUPPORTS     | Use existing if available |





**HashSet:**

A HashSet in Java is a collection that stores unique elements and does not maintain any insertion or sorting order. It is part of the Java Collections Framework and is implemented in the java.util package.

Stores only unique values (no duplicates).

Allows one null value.

Provides fast insertion, deletion, and lookup (average O(1) time).



Internal Working of HashSet

Internally, HashSet is backed by a HashMap.

When you create:

HashSet<String> set = new HashSet<>();

Java internally creates:

HashMap<String, Object> map = new HashMap<>();

Each element in the HashSet becomes a key in the HashMap, and all keys share the same dummy value.

Key      Value

\----     -----

Apple -> PRESENT

Banana -> PRESENT



When you execute:

set.add("Apple");

Internally it becomes:

map.put("Apple", PRESENT);



Step 1: Calculate hashCode()

"Apple".hashCode();

Step 2: Compute Bucket Index

The hash code is converted into a bucket index.

Step 4: Check for Duplicate

If bucket 5 already contains data:

Java checks -> equals()

returns true, insertion is rejected.

Otherwise it stores the new element.



**HashMap:**

**Default Size of HashMap/HashSet is 16, loadfactor is 0.75, Threshold = 16 × 0.75 = 12**

When the 13th entry is added, the capacity doubles from 16 to 32.

A HashMap is a data structure that stores data as key-value pairs. It provides average O(1) time complexity for put(), get(), and remove() operations by using hashing.

A HashMap stores these entries in an array of buckets.

Each bucket contains a Node.



Step 1: Calculate hashCode()

Step 3: Calculate Bucket Index

The bucket index is computed as:

Step 4: Check the Bucket

If bucket 5 is empty:

For getting the value it finds bucket and compare the value using equals()



Reading: ✅ ArrayList (O(1)) (For Insertion All elements shift one position O(n))

Insertion at beginning: ✅ LinkedList (O(1))

Deletion at beginning: ✅ LinkedList (O(1))

In real-world Java applications, ArrayList is often preferred over LinkedList for insertions after a certain size because of CPU cache locality and memory overhead

LinkedList insertion at the middle is O(n)



**Garbage Collector:**

Garbage Collector (GC) is an automatic memory management system that frees memory by removing objects that are no longer being used. This helps prevent memory leaks and eliminates the need for programmers to manually deallocate memory.

Garbage Collector Finds Unused Objects

The JVM periodically runs the Garbage Collector.

After removing unreachable objects, the memory becomes available for new objects.

1\. Nullifying the Reference

2\. Reassigning Reference

4\. Local Variable Goes Out of Scope



**Heap Memory and String Constant Pool (SCP):**

What is an Object? -> Whenever you write:

Student s = new Student();

Java creates an object in Heap Memory.

s is a reference variable stored in the stack.

The actual object is stored in the heap.

The Garbage Collector (GC) removes heap objects that are no longer referenced.



Strings are used very frequently.

String s1 = "Java";

String s2 = "Java";

String s3 = "Java";

If Java created three separate "Java" objects, it would waste memory.

**The String Constant Pool is a special area inside the heap that stores string literals.**

When Java sees a string literal, it first checks:

"Does this string already exist in the pool?"

Yes → Reuse it.

No → Create it.



String s1 = "Hello";

String s2 = "Hello";

Line 1

"Hello" is not in the pool.

Java creates it.

Java checks the pool.

"Hello" already exists.

No new object is created.

Only 1 object.



String s1 = new String("Hello");

Java sees the literal.

Creates "Hello" in the String Pool.

Because of new, Java creates another object in the heap.

Total Objects

Pool → 1

Heap → 1

Total = 2



String s1 = "Java";

String s2 = "Java";



System.out.println(s1 == s2); //true

Because both point to the same pooled object.



String s1 = new String("Java");

String s2 = new String("Java");



System.out.println(s1 == s2); //false



intern() -> only points to SCP if object exist instead of heap

String s1 = new String("Java");

String s2 = s1.intern();

s2 points to the pooled "Java". //points to SCP



String s1 = "HELLO";

String s3 = "hello".toUpperCase();

S1 Creates one object in the String Pool.

S2 "hello" -> Java creates another pooled string.

Since String is immutable, Java cannot modify "hello".

Instead, it creates a new String object in the heap containing "HELLO".

Because methods like toUpperCase(), concat(), replace(), etc., create a new String object



**REST:**

Stateless API gives response in json,xml,html,binary format



**What is singleton how to make class singleton:**

A Singleton is a design pattern that ensures only one object of a class is created throughout the application and provides a global access point to that object.

Why do we need Singleton?



Some resources should have only one instance:

Database Connection

Logger

Configuration Manager

Cache Manager



**How to Make a Class Singleton**

Step 1: Make constructor private

Prevent external object creation.

Step 2: Create a static instance

Store the only object.

Step 3: Provide a public method to access it

class Singleton {



&#x20;   private static Singleton instance = new Singleton();



&#x20;   private Singleton() {

&#x20;   }



&#x20;   public static Singleton getInstance() {

&#x20;       return instance;

&#x20;   }

}



**What is mutable and immutable class in java how to make class immutable:**

**Mutable Class**

A mutable class is a class whose object's state can be changed after creation.

Using setters we can set the values



**Immutable Class**

An immutable class is a class whose object's state cannot be changed after it is created.

String str = "Hello";

str.concat(" World");

System.out.println(str); --Hello

Benefits

✅ Thread-safe

✅ Secure

✅ Easy caching

✅ No synchronization required

✅ Safe to share between multiple threads

**How to Make a Class Immutable:**

1\. Make the class final

Prevents inheritance.

public final class Employee {

}

2\. Make all fields private and final

private final String name;

private final int id;

3\. Initialize fields through constructor

public Employee(int id, String name) {

&#x20;   this.id = id;

&#x20;   this.name = name;

}

4\. Do not provide setters only getters

public void setName(String name) {

}



**Java 8 Features:**

1\. Lambda Expressions

Runnable r = () -> System.out.println("Hello");

Less boilerplate code

More readable

2\. Functional Interfaces

An interface having exactly one abstract method.

3\. Stream API

Used to process collections efficiently.

4\. Method References - used in streams

Short form of lambda expressions.

5\. Default Methods in Interface

Adding a method to an interface broke all implementations.

interface Vehicle {

&#x20;   default void start() {

&#x20;       System.out.println("Vehicle Started");

&#x20;   }

}

6\. Static Methods in Interface

7\. Optional Class

Used to avoid NullPointerException.

8\. Date and Time API

11\. Parallel Streams

Process data using multiple CPU cores.



**HashMap**

HashMap stores data in key-value pairs.

HashMap is NOT thread-safe.

Two threads updating simultaneously can cause:

Data inconsistency

Lost updates



**ConcurrentHashMap is a thread-safe version of HashMap.**

ConcurrentHashMap<Integer, String> map =

&#x20;       new ConcurrentHashMap<>();

Used in multithreaded applications.

Used Segment Locking.

Only the segment being modified was locked.

Better than locking the whole map.

Does NOT allow null. value and key

To avoid ambiguity in concurrent environments.

Slightly slower because of synchronization mechanisms.



A **Fail-Fast** iterator immediately throws a ConcurrentModificationException if the collection is modified while it is being iterated (except through the iterator's own remove() method).

List<Integer> list = new ArrayList<>();



A **Fail-Safe** iterator does not throw ConcurrentModificationException.

Instead, it works on a copy (snapshot) of the collection.

CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();

CopyOnWriteArraySet

ConcurrentHashMap



**Can an ArrayList itself be immutable?**

No. The ArrayList class is designed to be mutable. If you need immutability, use:

List.of(...) (Java 9+)

List.copyOf(...) (Java 10+)

Immutable collections from libraries like Guava (ImmutableList)

final prevents reassignment.

List.of() prevents modification of the contents.



**== and equals():**

For primitive types, == compares values.

int a = 10;

int b = 10;

System.out.println(a == b); // true

For objects, == compares references (memory addresses).

String s1 = new String("Java");

String s2 = new String("Java");

System.out.println(s1 == s2); // false



equals() compares the contents (logical equality) of objects.



**Why is String immutable in Java?**

Immutable means once a String object is created, its value cannot be changed.

String s = "Hello";

s.concat(" World");

System.out.println(s);

concat() creates a new string; it does not modify the existing one.

1\. Security

Strings are widely used for sensitive information:

Database URLs

Usernames/passwords

File paths

2\. String Pool Optimization

Java maintains a String Pool to save memory.

3\. Thread Safety

Immutable objects are naturally thread-safe.

Multiple threads can read msg simultaneously without synchronization because nobody can modify it.



| Feature     | String            | StringBuilder | StringBuffer           |

| ----------- | ----------------- | ------------- | ---------------------- |

| Mutability  | ❌ Immutable       | ✅ Mutable     | ✅ Mutable              |

| Thread-safe | ✅ Yes             | ❌ No          | ✅ Yes                  |

| Performance | Slow (new object) | Fast 🚀       | Slower (sync overhead) |

| Memory      | More usage        | Efficient     | Efficient              |

| Introduced  | Java 1.0          | Java 5        | Java 1.0               |



**Java 8 Features explain in one sentence why how it created**

**1. Lambda Expressions**

**2. Functional Interfaces**

**3. Stream API**

**4. Method References**

**5. Optional Class**

**6. New Date API**

**Java 11**

**var keyword**

**String methods**

**HttpClient**

**Java 17**

**1. Sealed Classes**

**2. Pattern Matching for instanceof**

**3. Records**

**Java 21**

**1. Virtual Threads**



**Java 8**

1\. Lambda Expressions (->)

Why created: To reduce boilerplate code and enable functional programming by writing anonymous functions in a concise way.

list.forEach(name -> System.out.println(name));

2\. Functional Interfaces

A functional interface is an interface that contains exactly one abstract method.

Why created: To support lambda expressions by providing interfaces with exactly one abstract method.

Because a lambda expression represents a single behavior (single method implementation).

If there are two methods compiler doesn't know which method to implement for particular lambda expression

c = (a,b) -> a+b;

method add(int a, int b)

For this shortcut to work, Java needs an interface with only one abstract method.

It may also contain:

default methods

static methods

methods inherited from Object

@FunctionalInterface

interface Calculator {

&#x20;   int add(int a, int b);

}

3\. Stream API

Why created: To process collections declaratively and efficiently without writing complex loops.

4\. Method References (::)

Why created: To make lambda expressions shorter when an existing method can be reused directly.

5\. Optional Class

Why created: To reduce NullPointerException and explicitly represent the presence or absence of a value.

Optional is a container object introduced in Java 8 that may or may not contain a value.

It is used to avoid NullPointerException and make null handling more explicit.

String name = null;

System.out.println(name.length()); // NullPointerException

If name is null, the program crashes.

Optional<String> name = Optional.ofNullable(null);

System.out.println(name.isPresent()); // false

Optional<String> name = Optional.of("John");

It shifts the responsibility of handling empty values to the developer by forcing them to safely check and unwrap the container

6\. New Date \& Time API (java.time)

Why created: To replace the old Date and Calendar APIs, which were mutable, confusing, and not thread-safe.

**Java 11**

1\. var (Local Variable Type Inference)

Why created: To reduce repetitive type declarations while keeping code readable.

3\. HttpClient API

Why created: To provide a modern, built-in HTTP client replacing the older HttpURLConnection.

**Java 17**

1\. Sealed Classes

Why created: To control which classes can inherit from a parent class, improving security and maintainability.

public sealed class Vehicle

&#x20;   permits Car, Bike { }

2\. Pattern Matching for instanceof

Why created: To eliminate explicit casting after type checks.

if (obj instanceof String s) {

&#x20;   System.out.println(s.length());

}

3\. Records

Why created: To reduce boilerplate code for immutable data-carrying classes.

record Employee(int id, String name) {}

Automatically generates:

Constructor

Getters

toString()

equals()

hashCode()

**Java 21**

1\. Virtual Threads

Why created: To support millions of lightweight concurrent tasks without creating expensive OS threads.

Traditional platform threads consume significant memory and resources; virtual threads make high-concurrency applications much more scalable.



**Difference between Comparable and Comparator**

Both are used for sorting objects.



Comparable	Comparator

Present in java.lang	Present in java.util

Uses compareTo()	Uses compare()

Defines natural sorting	Defines custom sorting

Class itself modified	Separate class/lambda used

Comparable

class Employee implements Comparable<Employee> {

&#x20;   int id;



&#x20;   public int compareTo(Employee e) {

&#x20;       return this.id - e.id;

&#x20;   }

}

Collections.sort(list);

Comparator

Comparator<Employee> byName =

&#x20;   (e1, e2) -> e1.name.compareTo(e2.name);

Comparable provides a single natural ordering using compareTo(), whereas Comparator provides multiple custom orderings using compare().



**Marker Interface**

A marker interface is an interface with no methods and no fields.

It simply provides metadata to the JVM/framework.

Serializable

Cloneable



**Shallow Copy vs Deep Copy**

Shallow copy creates a new object, but nested objects are shared. child are same of both object if one change value it reflect in other also.

Deep copy creates a new object and also creates copies of all nested objects. create new child object also.



**Stream API (map, filter, flatMap)**

Filters data based on conditions.

map() Transforms data n\*2

flatMap() -> flattens nested structures (list of list)



**Explain parallel stream in java**

Parallel Stream splits data processing across multiple threads to improve performance on large datasets.

Faster for large datasets

Uses multiple CPU cores



explain equals and hashcode

Generates an integer hash value.

Then uses equals to confirm match.



**ArrayList vs LinkedList**

| ArrayList                | LinkedList               |

| ------------------------ | ------------------------ |

| Dynamic Array            | Doubly Linked List       |

| Fast random access       | Slow random access       |

| Slow insertion in middle | Fast insertion in middle |

| Less memory              | More memory              |

Use ArrayList when reads are frequent; use LinkedList when insertions and deletions are frequent.



**Abstract Class vs Interface**

| Abstract Class              | Interface                |

| --------------------------- | ------------------------ |

| Can have constructors       | Cannot have constructors |

| Can have instance variables | Only constants           |

| Single inheritance          | Multiple inheritance     |

| `extends`                   | `implements`             |

Abstract classes provide partial implementation and state, whereas interfaces define a contract and support multiple inheritance.4



**Explain N+1 query problem:**

N+1 Query Problem: When one query fetches parent records and then N additional queries are executed to fetch related child records for each parent, causing unnecessary database calls and performance issues.

List<Customer> customers = customerRepo.findAll(); // 1 query



for(Customer c : customers){

&#x20;   c.getOrders(); // N queries

}

1 query (Customers)

\+ 100 queries (Orders)

\-------------------

101 queries

Use Fetch Join,



**What is Data Consistency?**

Data Consistency means all microservices have correct and synchronized data after a business operation completes.



Example

Suppose you have:

Order Service

Payment Service

Inventory Service



Customer places an order.

Since each microservice has its own database, we cannot use a single database transaction across all services.

1\. Saga Pattern ⭐⭐⭐⭐⭐

The Saga Pattern is used to maintain data consistency across multiple microservices without using distributed transactions

Instead of one large transaction, a Saga breaks it into multiple local transactions.

If one step fails, compensating transactions are executed to undo the previous successful steps.

Each service has its own database.

A single database transaction cannot span all services.

Order Service

&#x20;   ↓

Payment Service

&#x20;   ↓

Inventory Service

If Inventory fails:

Inventory Failed

&#x20;      ↓

Refund Payment

&#x20;      ↓

Cancel Order

These are called Compensating Transactions.

Fegin Client

It is a declarative REST client where we define an interface and Spring generates the implementation.



Idempotency is a design principle where performing an operation multiple times produces the exact same system state as executing it a single time


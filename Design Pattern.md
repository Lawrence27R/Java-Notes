**Design Pattern**

Design patterns are proven, reusable solutions to common software design problems. They are not ready-made code but rather templates or best practices that help developers write flexible, maintainable, and scalable code.

Think of a design pattern as a blueprint for solving a recurring problem in software design.



**Singleton (Creational Design Pattern):**

**Singleton Class**

A Singleton Class is a class that allows only one object (instance) to be created throughout the application's lifecycle.

Singleton Pattern is the blueprint; Singleton Class is the implementation of that blueprint.



**What is Singleton Design Pattern?**

The Singleton Pattern ensures that:

Only one instance of a class exists throughout the application.

A global access point is provided to access that instance.

Helps save memory by reusing the same object



**Creating a Singleton Class in Java**

To create a Singleton class in Java, follow these steps:



Create a private constructor to prevent direct object creation from outside the class.

Declare a private static variable to store the single instance of the class.

Create a public static method (commonly getInstance()) that returns the same instance every time using the Lazy Initialization approach.

This ensures that only one object of the class is created throughout the application.



public class DatabaseConnection {



&#x20;   private static DatabaseConnection instance;



&#x20;   private DatabaseConnection() {}



&#x20;   public static DatabaseConnection getInstance() {



&#x20;       if(instance == null) {



&#x20;           synchronized (DatabaseConnection.class) {



&#x20;               if(instance == null) {

&#x20;                   instance =

&#x20;                           new DatabaseConnection();

&#x20;               }

&#x20;           }

&#x20;       }



&#x20;       return instance;

&#x20;   }

}



**Another way is Eager Initialization**

Object created during class loading.

Thread Safe. Cons: Object is created even if not used

public class DatabaseConnection {



&#x20;   private static final DatabaseConnection INSTANCE =

&#x20;           new DatabaseConnection();



&#x20;   private DatabaseConnection() {}



&#x20;   public static DatabaseConnection getInstance() {

&#x20;       return INSTANCE;

&#x20;   }

}



**Where Singleton is used:**

**Database Connection Pool**

One pool shared across application.

**Logger**

One logger writes all logs.

**Configuration Manager**

Loads config file once.

**Cache Manager**

Shared cache.



**Advantages:**

Saves Memory

Shared Resource

Global Access

Better Resource Management



**Disadvantage:**

Global State - Harder to manage.



**Can Singleton be broken?**

Yes

Reflection

Cloning



**Factory (Creational Design Pattern):**

Factory Pattern is a Creational Design Pattern that provides an interface for creating objects while hiding the object creation logic from the client.

The client requests an object, and the Factory decides which concrete class to instantiate.

Why Do We Need Factory Pattern?

Vehicle vehicle = new Car();

Later business changes:

Vehicle vehicle = new Bike();

Now you must modify code everywhere.

Object creation becomes scattered throughout the application.

Factory centralizes it.

One place manages creation.

Add new classes easily.

Open Closed Principle - SOLID

Usually yes if stateless. - Thread Safe



Payment System

Payment payment =

&#x20;       PaymentFactory.getPayment("UPI");

Factory creates the correct payment object.

interface Payment {

&#x20;   void pay();

}

class UPIPayment implements Payment {



&#x20;   @Override

&#x20;   public void pay() {

&#x20;       System.out.println("UPI Payment");

&#x20;   }

}

class Card implements Payment {



&#x20;   @Override

&#x20;   public void pay() {

&#x20;       System.out.println("Card Payment");

&#x20;   }

}



class PaymentFactory {



&#x20;   public static Payment getPayment(String type) {



&#x20;       if(type.equalsIgnoreCase("UPI")) {

&#x20;           return new UPIPayment();

&#x20;       }



&#x20;       if(type.equalsIgnoreCase("CARD")) {

&#x20;           return new Card();

&#x20;       }



&#x20;       throw new IllegalArgumentException(

&#x20;               "Invalid vehicle type");

&#x20;   }

}



Used:

JDBC

Spring Framework :ApplicationContext.getBean("userService");

Logger

Banking Application

Notification System



Disadvantages:

Large factories become difficult to maintain.



**Builder** **(Creational Design Pattern):**

The Builder Design Pattern is a creational design pattern that provides a step-by-step approach to constructing complex objects. It separates the construction process from the object’s representation, enabling the same method to create different variations of an object.



Encapsulates object construction logic in a separate Builder class, enabling flexible and controlled creation.

Instead of using a complex constructor with many parameters, the Builder pattern allows you to construct it step by step:

To avoid large constructor use builder.



Main Class

public class User {



&#x20;   private String name;

&#x20;   private int age;

&#x20;   private String email;



&#x20;   private User(Builder builder) {

&#x20;       this.name = builder.name;

&#x20;       this.age = builder.age;

&#x20;       this.email = builder.email;

&#x20;   }

Builder Class

&#x20;   public static class Builder {



&#x20;       private String name;

&#x20;       private int age;

&#x20;       private String email;



&#x20;       public Builder name(String name) {

&#x20;           this.name = name;

&#x20;           return this;

&#x20;       }



&#x20;       public Builder age(int age) {

&#x20;           this.age = age;

&#x20;           return this;

&#x20;       }



&#x20;       public Builder email(String email) {

&#x20;           this.email = email;

&#x20;           return this;

&#x20;       }



&#x20;       public User build() {

&#x20;           return new User(this);

&#x20;       }

&#x20;   }

}

User user =

&#x20;       new User.Builder()

&#x20;               .name("Lawrence")

&#x20;               .age(24)

&#x20;               .email("law@gmail.com")

&#x20;               .build();



Uses:

StringBuilder

Lombok Builder

HTTP Request Creation



Advantages:

Supports Optional Parameters

Immutable Objects

Easier Maintenance



Thread Safe



**Strategy (Behavioral Design Pattern):**

Strategy Pattern is a Behavioral Design Pattern that defines a family of algorithms, encapsulates each algorithm into a separate class, and allows them to be selected at runtime.

Change behavior without changing the client code.

A behavioral pattern that allows selecting an algorithm at runtime.

It is used when multiple ways of performing the same task exist, such as payment methods, authentication mechanisms, route calculations, or notification channels.

**Problem :** Large if-else or switch-case statements.

Open Closed Principle



Strategy Interface

interface PaymentStrategy {

&#x20;   void pay(double amount);

}

Concrete Strategies

class UpiPayment implements PaymentStrategy {



&#x20;   @Override

&#x20;   public void pay(double amount) {

&#x20;       System.out.println(

&#x20;           "Paid " + amount + " using UPI");

&#x20;   }

}

class CardPayment implements PaymentStrategy {



&#x20;   @Override

&#x20;   public void pay(double amount) {

&#x20;       System.out.println(

&#x20;           "Paid " + amount + " using Card");

&#x20;   }

}

Context Class

class PaymentContext {



&#x20;   private PaymentStrategy paymentStrategy;



&#x20;   public PaymentContext(

&#x20;           PaymentStrategy paymentStrategy) {



&#x20;       this.paymentStrategy = paymentStrategy;

&#x20;   }



&#x20;   public void makePayment(double amount) {



&#x20;       paymentStrategy.pay(amount);

&#x20;   }

}



Client Code

&#x20;       PaymentStrategy strategy =

&#x20;               new UpiPayment();



&#x20;       PaymentContext context =

&#x20;               new PaymentContext(strategy);



&#x20;       context.makePayment(1000);

**Client selects strategy.**



**Used:**

Payment Systems

Sorting Algorithms

Notification Systems

Navigation Systems

**Advantages**

Removes if-else Chains

Easy to Extend

**Disadvantages**

More Classes

Client Must Choose Strategy



**Observer (Behavioral Design Pattern):**

Observer is a Behavioral Design Pattern that defines a one-to-many dependency between objects.

When one object (Subject) changes its state, all dependent objects (Observers) are automatically notified and updated.

Observer Pattern is a Behavioral Design Pattern that establishes a one-to-many relationship between a Subject and multiple Observers. When the Subject's state changes, it automatically notifies all registered Observers. It is commonly used in event-driven systems such as Spring Events, notification systems, GUI event listeners, stock market applications, and microservices architectures.



**Problem:**

Suppose an order is placed.

Multiple systems must react:

Order Service

&#x20;     |

&#x20;     +--> Email Service

&#x20;     +--> SMS Service

&#x20;     +--> Inventory Service

&#x20;     +--> Analytics Service

Every new service requires modifying OrderService.

Observer removes this dependency.

**Used:**

YouTube Subscription

Subject:

YouTube Channel

Observers:

Subscriber A

Subscriber B

Subscriber C

When channel uploads a video:

Notify all subscribers



Observer Interface

interface Observer {



&#x20;   void update(String message);

}

Concrete Observer

class Subscriber implements Observer {



&#x20;   private String name;



&#x20;   public Subscriber(String name) {

&#x20;       this.name = name;

&#x20;   }



&#x20;   @Override

&#x20;   public void update(String message) {



&#x20;       System.out.println(

&#x20;               name + " received: " + message);

&#x20;   }

}

Subject Interface

interface Subject {



&#x20;   void subscribe(Observer observer);



&#x20;   void unsubscribe(Observer observer);



&#x20;   void notifyObservers();

}

Concrete Subject

import java.util.ArrayList;

import java.util.List;



class YouTubeChannel implements Subject {



&#x20;   private List<Observer> observers =

&#x20;           new ArrayList<>();



&#x20;   private String latestVideo;



&#x20;   @Override

&#x20;   public void subscribe(

&#x20;           Observer observer) {



&#x20;       observers.add(observer);

&#x20;   }



&#x20;   @Override

&#x20;   public void unsubscribe(

&#x20;           Observer observer) {



&#x20;       observers.remove(observer);

&#x20;   }



&#x20;   @Override

&#x20;   public void notifyObservers() {



&#x20;       for(Observer observer : observers) {



&#x20;           observer.update(

&#x20;                   latestVideo);

&#x20;       }

&#x20;   }



&#x20;   public void uploadVideo(

&#x20;           String title) {



&#x20;       this.latestVideo = title;



&#x20;       notifyObservers();

&#x20;   }

}

Client Code

public class Main {



&#x20;   public static void main(String\[] args) {



&#x20;       YouTubeChannel channel =

&#x20;               new YouTubeChannel();



&#x20;       Observer lawrence =

&#x20;               new Subscriber("Lawrence");



&#x20;       Observer john =

&#x20;               new Subscriber("John");



&#x20;       channel.subscribe(lawrence);

&#x20;       channel.subscribe(john);



&#x20;       channel.uploadVideo(

&#x20;               "Observer Pattern Tutorial");

&#x20;   }

}



**Used:**

Spring Events

ApplicationEventPublisher

Kafka Consumers



**Advantages:**

Easy to Extend

Supports Open-Closed Principle

One-to-Many Communication

**Disadvantages:**

Performance Issues



**Proxy (Structural Design Pattern):**

Proxy is a Structural Design Pattern that provides a placeholder or surrogate for another object to control access to it.

The Proxy implements the same interface as the Real Object and intercepts requests before forwarding them.

The client talks to the Proxy instead of the Real Object.

A structural design pattern that provides a surrogate object to control access to another object.

Problem:

Suppose loading an image takes 10 seconds.

Image loads immediately.

Even if user never views it.

Waste of resources.

Actual image loads only when needed.

Expensive Object Creation

Database Connection

Large Image

Remote Service

PDF Document

Creating them is costly.

Proxy delays creation.

Only authorized users should access resources.

Proxy checks permissions.

Need to track:

Who accessed?

When?

How many times?

Proxy can handle this.



Subject Interface

interface Image {



&#x20;   void display();

}

Real Object

class RealImage implements Image {



&#x20;   private String fileName;



&#x20;   public RealImage(String fileName) {



&#x20;       this.fileName = fileName;

&#x20;       loadFromDisk();

&#x20;   }



&#x20;   private void loadFromDisk() {



&#x20;       System.out.println(

&#x20;           "Loading image from disk...");

&#x20;   }



&#x20;   @Override

&#x20;   public void display() {



&#x20;       System.out.println(

&#x20;           "Displaying " + fileName);

&#x20;   }

}

Proxy Object

class ImageProxy implements Image {



&#x20;   private RealImage realImage;



&#x20;   private String fileName;



&#x20;   public ImageProxy(String fileName) {



&#x20;       this.fileName = fileName;

&#x20;   }



&#x20;   @Override

&#x20;   public void display() {



&#x20;       if(realImage == null) {



&#x20;           realImage =

&#x20;               new RealImage(fileName);

&#x20;       }



&#x20;       realImage.display();

&#x20;   }

}

Client

public class Main {



&#x20;   public static void main(String\[] args) {



&#x20;       Image image =

&#x20;           new ImageProxy("photo.jpg");



&#x20;       System.out.println(

&#x20;           "Image not loaded yet");



&#x20;       image.display();



&#x20;       image.display();

&#x20;   }

}

**Used:**

Spring AOP

@Transactional

Spring creates a Proxy around your bean.

Proxy manages:



Transactions

Logging

Security



**Advantages:**

Lazy Loading

Logging

Caching



**Disadvantages:**

Additional Layer

Extra complexity.

More Classes


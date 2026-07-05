**What is Spring Security?**

Spring Security is a security framework for Spring applications that provides:

Authentication (Who are you?)

Authorization (What can you access?)

Protection against common attacks like CSRF, Session Fixation, Clickjacking, etc.

Spring Security is a powerful authentication and authorization framework for Spring applications. It secures REST APIs and web applications by providing features like authentication, role-based authorization, password encryption, OAuth2, JWT support, CSRF protection, and session management.



Authentication (Who are you?)

Verifies the user's identity.

Example:

Username \& Password

OTP

Authorization (What can you do?)

Determines what the authenticated user is allowed to access.

BCryptPasswordEncoder

**Spring Security Architecture**

Client



↓



Security Filter Chain



↓



Authentication Filter



↓



Authentication Manager



↓



Authentication Provider



↓



UserDetailsService



↓



Database



**JWT Structure**

Header



.



Payload



.



Signature



**What is OAuth?**

OAuth is an Authorization Framework.

It allows users to log in using another provider without sharing their password with your application.

HttpSecurity http

How to Read Claims?

Example using a JWT library:

@PreAuthorize (Role checking)

@PostAuthorize

Checks authorization after the method executes.

@Secured

Role-based authorization.

@EnableWebSecurity

Enables Spring Security configuration.

@EnableMethodSecurity

Enables method-level security.





**What is Kafka?**

Apache Kafka is a distributed event streaming platform used for sending and receiving messages between applications.

It enables asynchronous communication between services.

Instead of services calling each other directly, they communicate through Kafka.

Apache Kafka is a distributed, fault-tolerant, high-throughput messaging platform used for publishing and consuming real-time events. It enables asynchronous communication between microservices.

Payment Service directly calls Notification Service.

If Notification Service is down, Payment Service may fail or need retry logic.

**With Kafka:**

Payment Service only sends a message to Kafka.

Notification Service reads the message whenever it's available.

This is asynchronous communication.

Order Service

&#x20;     |

&#x20;     V

&#x20;  Kafka Topic

&#x20;     |

&#x20;     +--> Payment Service

&#x20;     |

&#x20;     +--> Inventory Service

&#x20;     |

&#x20;     +--> Email Service

&#x20;     |

&#x20;     +--> Analytics Service

The Order Service publishes one event.

Multiple services consume it independently.

**Kafka Architecture:**

Producer

&#x20;    |

&#x20;    V

&#x20; Kafka Broker

&#x20;    |

&#x20;    V

&#x20;  Topic

&#x20;    |

&#x20;    V

Consumer



**Producer**

Produces messages.

**Consumer**

Reads messages.

**Topic**

A Topic is a logical channel where messages are stored.

**Broker**

A Kafka server.

It stores messages.

Together they form a Kafka Cluster.(B1,B2,B3)

**Partition**

A Topic is divided into multiple partitions.

Parallel processing

Scalability

High throughput

Three consumers can process messages simultaneously.

**Offset**

Every message has a unique Offset inside a partition.

Kafka distributes partitions among consumers in the same group.

If Leader crashes,

Follower becomes Leader.

spring.kafka.consumer.group-id=group1

spring.kafka.consumer.auto-offset-reset=earliest

spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer

@KafkaListner



1\. What happens if a Broker crashes?

A Broker is a Kafka server that stores messages.

Kafka keeps multiple copies (replicas) of each partition on different brokers.

If one broker crashes, Kafka automatically elects another replica as the Leader, and producers and consumers continue working with minimal interruption.



2\. What happens if a Consumer crashes?

Kafka keeps track of the last message read using an Offset.

If a consumer crashes:

It stops reading messages.

Another consumer in the same Consumer Group takes over its partitions.

The new consumer resumes reading from the last committed offset.

This process is called Consumer Rebalancing.





@RetryableTopic(attempts = "3")

Retry with Backoff (retry after particular time and try)

Dead Letter Topic

If retries fail,

Instead of losing the message,

Kafka sends it to another topic.

Developers can later inspect or reprocess messages from the DLT.

If a key is provided: Kafka hashes the key (hash(key) % number\_of\_partitions) so that all messages with the same key go to the same partition, preserving order for that key.





| Kafka                                               | RabbitMQ                                                   |

| --------------------------------------------------- | ---------------------------------------------------------- |

| Event streaming platform                            | Message broker                                             |

| High throughput                                     | Lower throughput for streaming workloads                   |

| Stores messages for a configurable retention period | Typically removes messages after successful acknowledgment |

| Best for event-driven systems                       | Best for task queues and traditional messaging             |

| Partition-based scalability                         | Queue-based messaging                                      |





**Circuit Breaker:**

Circuit Breaker is a fault tolerance design pattern that prevents an application from repeatedly calling a failing service. It detects failures, temporarily blocks requests, and automatically retries after a configured time, improving system stability.



**Why Do We Need Circuit Breaker?**

Order Service

&#x20;     |

&#x20;     |

&#x20;     V

Payment Service

If Payment Service crashes,



Order Service keeps calling it.



Result:

Timeout

CPU usage increases

Threads become blocked

Entire application becomes slow

This is called Cascading Failure.



Circuit Breaker immediately returns a fallback response instead of waiting for timeouts.

Circuit Breaker States

1\. Closed State

Everything works.

2\. Open State

Failures exceed the configured threshold.

3\. Half-Open State

After a configured wait time,

Circuit allows a few requests.

Resilience4j - Library used in circuit breaker design pattern

&#x20;   @CircuitBreaker(

&#x20;       name = "paymentService",

&#x20;       fallbackMethod = "paymentFallback"

&#x20;   )

Annotation and configuration



**What is a Microservice?**

A Microservice is an architectural style where a large application is divided into small, independent services, and each service is responsible for one specific business functionality.

Each microservice:

Has its own business logic

Can have its own database

Can be developed independently

Can be deployed independently

Entire application must be redeployed for small changes.

Scaling one module means scaling everything.

One failure can affect the entire application.



**Microservices Architecture:**

&#x20;               Client

&#x20;                 |

&#x20;                 |

&#x20;            API Gateway

&#x20;                 |

&#x20;  ---------------------------------

&#x20;  |       |       |       |       |

User   Product   Order  Payment  Notification

Service Service Service Service    Service



**What is an API Gateway? (It uses Route Matching configured in ymal file)**

An API Gateway is the single entry point for all client requests in a microservices architecture.

Clients do not communicate directly with individual services.

Why do we need:

The client needs to know every service URL.

If a service changes, the client must also change.

The client only knows the Gateway URL.

**Responsibility:**

Route requests

Authentication

Authorization

JWT validation

Rate limiting

Logging

Load balancing (often integrated with service discovery or infrastructure)

Request/Response transformation

CORS handling





**Multi-Threading:**



**What is a Process?**

A Process is an independent program in execution.

Examples:

Chrome Browser

VS Code

Spotify

Each process has:

Separate memory

Separate resources

One or more threads

**What is a Thread?**

A thread is the smallest unit of execution within a process. Multiple threads can run concurrently, allowing better CPU utilization and improved application responsiveness.

A process can have multiple threads running simultaneously.

Chrome Process

&#x20;   ├── UI Thread

&#x20;   ├── Download Thread

&#x20;   ├── Render Thread

&#x20;   └── Network Thread

**What is Multithreading?**

Running multiple threads concurrently within the same process.

Music Player

Thread 1 → Play Music

Thread 2 → Download Song

Thread 3 → Update UI

W/O - Everything waits.

Better CPU utilization

Faster execution

Responsive applications

Parallel task execution (on multi-core CPUs)



| Process                    | Thread                               |

| -------------------------- | ------------------------------------ |

| Independent program        | Part of a process                    |

| Separate memory            | Shared memory within process         |

| Heavyweight                | Lightweight                          |

| Slow creation              | Fast creation                        |

| Communication is expensive | Easy communication via shared memory |



**Ways to Create a Thread:**

Method 1: Extend Thread

Method 2: Implement Runnable

Why preferred?

Java supports only single inheritance.

Runnable allows extending another class.

Method 3: Lambda

Method 4: Executor Framework (Most Preferred)

ExecutorService executor =

&#x20;       Executors.newFixedThreadPool(5);



executor.submit(() ->

&#x20;       System.out.println("Task"));



executor.shutdown();

This is how threads are usually managed in enterprise applications.



**Thread Lifecycle:**

NEW (Thread created {new keyword})



↓



RUNNABLE (t.start() Thread is ready to run.)



↓



RUNNING (CPU executes the thread)



↓



WAITING / BLOCKED / TIMED\_WAITING (Waiting indefinitely Thread.sleep(1000))



↓



TERMINATED (Execution completed)



t.start() - create a new thread

t.run() - Runs like a normal method. No new thread is created.

| Runnable                        | Callable                     |

| ------------------------------- | ---------------------------- |

| No return value                 | Returns value                |

| Cannot throw checked exceptions | Can throw checked exceptions |

| `run()`                         | `call()`                     |

| Used with `Thread`              | Used with `ExecutorService`  |



**What is Executor Framework?**

Problem

Creating threads manually:

Too many threads:

High memory usage

Slow creation

Poor performance



Executor Framework

Manages thread creation, reuse, and scheduling.

Application



↓



ExecutorService



↓



Thread Pool



↓



Worker Threads



↓



Tasks

**Why Executor Framework?**

Instead of creating 100 threads,

Thread Pool

5 Threads

Tasks are executed using these reusable threads.



Benefits:



Thread reuse

Better performance

Less memory

Easier management

submit()

execute()

shutdown()

Fixed Thread Pool

Executors.newFixedThreadPool(5);

Cached Thread Pool

Creates threads as needed and reuses idle ones.

Executors.newCachedThreadPool();

Single Thread Executor

Only one worker thread.

Tasks execute sequentially.

Executors.newSingleThreadExecutor();



Synchronization

Multiple threads may access shared data.

Both update simultaneously.

synchronized

Race Condition

Two threads update shared data simultaneously.



start()

What is it?

start() creates a new thread and then calls the run() method internally.

run()

Contains the actual work performed by the thread.

run() should not be called directly when you want concurrency.

sleep()

Pauses the current thread for a specified amount of time.

Thread does not execute.

yield()

yield() tells the scheduler:

"I'm willing to let another thread run now if one is ready."

It is only a hint. Thread A waits Thread B may run or A may continue

join()

Makes the current thread wait until another thread finishes.

wait()

wait() causes the current thread to:

Release the object's monitor lock.

Wait until another thread calls notify() or notifyAll().

notify()

Wakes one thread waiting on the same object's monitor.

notifyAll() (One gets lock)

Wakes all threads waiting on the object's monitor.

interrupt()

Used to interrupt a thread.



**Deadlock:**

A deadlock happens when two or more processes (or people) are waiting for each other, so nobody can continue.

A Deadlock occurs when two or more threads wait forever for resources held by each other.

Example

Thread 1

Locks A

Needs B



Thread 2

Locks B

Needs A



Thread1



Lock A



↓



Waiting Lock B



\-------------------



Thread2



Lock B



↓



Waiting Lock A

Both wait forever.



Prevent Deadlock:

**Acquire locks in a consistent order**

**Use ReentrantLock.tryLock()**

A ReentrantLock is a special lock in Java that controls access to shared data, just like the synchronized keyword, but it gives you more control.

if (lock.tryLock()) {

&#x20;   try {

&#x20;       System.out.println("Got the lock!");

&#x20;   } finally {

&#x20;       lock.unlock();

&#x20;   }

} else {

&#x20;   System.out.println("Lock is busy. Try again later.");

}

Instead of waiting forever for a lock, try to get it.

If the lock is available → use it.

If it's not available → stop trying, release any locks you already have, and try again later.

This avoids getting stuck forever.Always take locks in the same order.

**Reduce nested locking**

Don't hold one lock while trying to get another lock unless it's really necessary.





**Concurrent Collections**

ConcurrentHashMap

CopyOnWriteArrayList


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



1\. application.properties

Uses key-value pairs.

Advantages

Simple and familiar.

Easy for small projects.



2\. application.yml

Uses YAML (Yet Another Markup Language) with indentation to represent hierarchy.

Advantages

Cleaner and more readable.

Better for complex and nested configurations.

You can keep multiple profiles in a single file using document separators:



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

Limitation: run() returns void and can't throw checked exceptions — no way to get a result back or propagate a failure cleanly.

Method 3: Lambda -uses runnable method internally

Method 4: Executor Framework (Most Preferred) - Uses Callable

Return Result and throws checked exceptions

It's the recommended way to manage threads rather than creating raw Thread objects yourself.

ExecutorService executor =

&#x20;       Executors.newFixedThreadPool(5);



executor.submit(() ->

&#x20;       System.out.println("Task"));



executor.shutdown();

This is how threads are usually managed in enterprise applications.



Thread creation/destruction is expensive (OS-level). Pools reuse threads, bound resource usage, and provide lifecycle management, task queuing, and structured error handling — critical for something like a transaction banking system processing bursts of requests.

It reuses a fixed set of threads instead of creating/destroying them per task, so your app stays fast and doesn't run out of resources under load.

ExecutorService is a Java framework that manages a pool of reusable worker threads, so you can submit tasks to run concurrently without manually creating and destroying threads yourself.

Pool size = Number of CPU cores + 1 (1 extra thread to keep it alive)





execute() takes only Runnable, returns nothing, exceptions propagate to the thread's uncaught exception handler. submit() takes Runnable/Callable, returns a Future, and captures exceptions inside it.



Q3: How do you decide thread pool size for a CPU-bound vs I/O-bound task?

CPU-bound: roughly number of CPU cores + 1. I/O-bound (like DB/network calls, common in your iCashPro/payment gateway context): higher, since threads spend time waiting — often calculated as cores \* (1 + waitTime/computeTime).



ThreadPoolExecutor

Executor (interface) — just execute(Runnable)

&#x20;  └── ExecutorService (interface) — adds lifecycle mgmt, submit(), Future

&#x20;       └── ScheduledExecutorService — adds delayed/periodic scheduling



**Thread Lifecycle:**

NEW (Thread created {new keyword})

Thread object is created, but start() hasn't been called yet. No thread exists at OS level yet — just a Java object.

↓



RUNNABLE (t.start() Thread is ready to run.)

After start() is called. This is actually two sub-states combined that Java doesn't distinguish:

Ready — waiting for the OS scheduler to give it CPU time

Running — actually executing on a CPU core right now

↓



RUNNING (CPU executes the thread)



↓



WAITING / BLOCKED / TIMED\_WAITING (Waiting indefinitely Thread.sleep(1000))

(BLOCKED) Thread is alive but stuck waiting to acquire a monitor lock (i.e., trying to enter a synchronized block/method that another thread already holds).

(WAITING)Thread is waiting indefinitely for another thread to explicitly wake it up. It won't proceed until someone calls notify(), notifyAll(), or the joined thread finishes.

Caused by:

object.wait() (no timeout)

thread.join() (no timeout)

(TIMED\_WAITING)Same as WAITING, but with a timeout — the thread will wake up on its own after the specified time, even without being notified.

Caused by:

Thread.sleep(ms)

object.wait(ms)

↓



TERMINATED (Execution completed)

The thread has finished executing — run() completed normally, or it exited due to an uncaught exception. Once terminated, it cannot be restarted



t.start() - create a new thread at the OS level

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

Creates a new OS-level thread and calls run() on that new thread asynchronously. Returns immediately — doesn't wait for run() to finish.run()

Contains the actual work performed by the thread.

run() should not be called directly when you want concurrency.

Just a normal method containing the code you want executed. If you call run() directly (not via start()), it executes synchronously on the current thread — no new thread is created at all.

sleep()

Pauses the current thread for a specified amount of time.

Thread does not execute.

Pauses the current thread for the given time. Does not release any locks it holds. Throws checked InterruptedException.

yield()

yield() tells the scheduler:

"I'm willing to let another thread run now if one is ready."

It is only a hint. Thread A waits Thread B may run or A may continue

A hint to the scheduler that the current thread is willing to give up its CPU turn so other threads of the same priority can run. Purely advisory — the JVM/OS may ignore it entirely.

join()

Makes the current thread wait until another thread finishes.

Makes the calling thread wait until the thread you called join() on finishes execution.

wait()

wait() causes the current thread to:

Release the object's monitor lock.

Wait until another thread calls notify() or notifyAll().

Releases the lock on the object and puts the thread into WAITING (or TIMED\_WAITING with a timeout), until another thread calls notify()/notifyAll() on the same object.

notify()

Wakes one thread waiting on the same object's monitor.

That thread moves from WAITING back to RUNNABLE — but it still needs to reacquire the lock before continuing, so it doesn't run immediately if the notifying thread still holds the lock.

notifyAll() (One gets lock)

Wakes all threads waiting on the object's monitor.

Wakes up all threads waiting on the object's monitor. They all compete to reacquire the lock, one at a time. Generally safer than notify() — with notify(), if you accidentally wake the "wrong" waiting thread (one that still can't proceed), you get a stuck program. notifyAll() avoids this at a small performance cost.

interrupt()

Used to interrupt a thread.

Sets the interrupt flag on a thread. Doesn't forcibly stop it — it's a cooperative signal. If the thread is in sleep(), wait(), or join(), it throws InterruptedException immediately and clears the flag. If the thread is doing normal computation, it must manually check isInterrupted() and decide to stop.



Deprecated methods — stop(), suspend(), resume()



Why are wait()/notify() on Object instead of Thread?

Because locking is associated with any object's monitor, not specifically with a Thread — any object can be a synchronization point. Since synchronized can lock on any object, wait/notify needed to live where the lock lives: on Object.



Difference between sleep() and wait()?

sleep() is a static Thread method, doesn't release locks, doesn't need synchronization, wakes up after the given time. wait() is an Object method, must be called inside synchronized, releases the lock, and needs another thread to call notify()/notifyAll() (or a timeout) to wake up.



**Deadlock:**

A Deadlock occurs when two or more threads wait forever for resources held by each other.

A deadlock happens when two or more threads are each waiting for a lock the other one holds, so none of them can ever proceed — they're stuck forever in a circular wait.

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

**1. Lock Ordering**

Always acquire locks in the same, fixed global order, regardless of which thread or direction the operation goes.

**Acquire locks in a consistent order**

**2. Lock Timeout (breaks Hold and Wait — using tryLock())**

Instead of blocking forever waiting for a lock, try to acquire it with a timeout; if it fails, back off, release what you're holding, and retry.

This is the standard way ReentrantLock is used to avoid deadlock — synchronized has no equivalent timeout mechanism, which is a key reason Lock exists.



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



Does ReentrantLock prevent deadlock automatically?

No — it doesn't prevent deadlock by itself; you still need to apply lock ordering or tryLock() with timeout deliberately.



**3. Avoid Nested Locks**

Don't hold one lock while trying to get another lock unless it's really necessary.



4\. Use a Single Lock for Related Operations

If two resources are frequently locked together, sometimes it's simpler to use one coarser lock covering both, instead of two fine-grained locks. Trades some concurrency for eliminating the deadlock risk entirely.



**synchronized** Keyword Provides mutual exclusion (only one thread executes the block at a time) AND visibility (changes made inside are guaranteed visible to other threads after they acquire the same lock).



**volatile** just guarantees that all threads always see the latest value of a variable — nothing more, nothing less



**What is a Daemon Thread**

A daemon thread is a low-priority, background thread that runs in service of user (non-daemon) threads. The JVM does not wait for daemon threads to finish before exiting — as soon as all non-daemon (user) threads finish, the JVM shuts down immediately, killing any daemon threads mid-execution, no matter what they were doing.

Simple analogy: think of daemon threads like background music at a party. The party (JVM) doesn't wait for the music to naturally end — the moment all the guests (user threads) leave, the venue shuts down and the music just cuts off, mid-song.



Ways to create - setDaemon(true) must be called before start()



&#x09;			User Thread		Daemon Thread

JVM waits for it to finish?	Yes			No

Priority in JVM lifecycle	Keeps JVM alive		Doesn't keep JVM alive

Typical use			Main application logic	Background support tasks (GC, monitoring, cleanup)

Example				main() thread, worker  Garbage Collector thread, a heartbeat/logging thread

&#x09;			threads doing actual

&#x09;			business logic



**What is ThreadLocal?**

ThreadLocal<T> gives each thread its own independent copy of a variable. Even though multiple threads might reference the same ThreadLocal object, when they call get()/set(), they're each reading/writing to their own isolated value — no sharing, no race conditions, no synchronization needed.



This is exactly how transaction IDs, logged-in user info, or correlation IDs are typically propagated through a web request in Spring-based systems — without passing them as a parameter through every single method call.

private static final ThreadLocal<String> transactionId = new ThreadLocal<>();





A **virtual thread** is a lightweight thread managed by the JVM itself, not the OS. Traditional threads (platform threads) map 1:1 to an OS thread — expensive to create, limited in number (thousands, maybe). Virtual threads let you spin up millions of them cheaply, because many virtual threads share a small pool of actual OS threads underneath.

**Concurrent Collections**

ConcurrentHashMap

Used segment-based locking — the map was divided into 16 segments by default, each with its own lock. Two threads could write simultaneously as long as they hit different segments. Still a form of lock striping, but coarse-grained.

CopyOnWriteArrayList / CopyOnWriteArraySet How it works: every write operation (add, remove, set) creates a brand new copy of the entire underlying array, and swaps the reference. Reads always operate on a stable, unchanging snapshot — no locking needed for reads at all.


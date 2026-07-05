A Statement is used to execute simple SQL queries where the SQL is created dynamically as a string.

String sql = "SELECT \* FROM employee WHERE id = 1";

Prone to SQL Injection



PreparedStatement

A PreparedStatement is a precompiled SQL statement that uses placeholders (?) for parameters.

Faster

More secure

Prevents SQL Injection

String sql = "SELECT \* FROM employee WHERE id = ?";

PreparedStatement ps = connection.prepareStatement(sql);

ps.setInt(1, 1);



CallableStatement

Used to call Stored Procedures in the database.



Hibernate is an open-source ORM framework that maps Java objects to relational database tables. It eliminates most JDBC boilerplate code by automatically generating SQL, managing object persistence, caching, and transactions.



**Why Hibernate?**



Problems with JDBC:



Too much boilerplate code

Manual ResultSet mapping

Manual connection handling

SQL written everywhere

Database-dependent code

Hard to maintain



Hibernate solves these by:



ORM mapping

Automatic SQL generation

Caching

Transaction management

Lazy loading

Database independence



**Hibernate Architecture:**

Application



↓



SessionFactory



↓



Session



↓



Hibernate



↓



JDBC



↓



Database

**Hibernate Lifecycle:**

Java Object



↓



Transient (Object created)



↓



Persistent (Saved in database)



↓



Detached (Session closed)



↓



Removed (Deleted)



**Cache in Hibernate:**

**First Level Cache (L1 Cache):**

The First Level Cache is a cache associated with a single Hibernate Session.

Every Session has its own cache.

It is enabled by default.

It cannot be shared with other sessions.

It exists only until the session is closed.

For first call it execute the query and fetch and store in the cache for second call it check cache and return.



**Second Level Cache (L2 Cache):**

The Second Level Cache is shared across multiple Hibernate sessions.



Unlike the First Level Cache:

Shared by all sessions created from the same SessionFactory.

Disabled by default.

Requires configuration with a cache provider (such as Ehcache or Infinispan).

Session



↓



L1 Cache



↓



Not Found



↓



L2 Cache



↓



Found



↓



Return Object



**N+1 Query Problem:**

The N+1 Query Problem occurs when Hibernate executes one query to fetch parent entities and then one additional query for each parent entity to fetch its related child entities.

As a result, instead of executing 1 query, Hibernate executes N+1 queries, which causes unnecessary database calls and degrades performance.

Increased network latency

Slower response time

Higher database load

**Solution:**

Use JOIN FETCH

Instead of fetching customers and accounts separately, fetch them together.

SELECT DISTINCT c FROM Customer c JOIN FETCH c.accounts

Use Entity Graphs

Batch Fetching





**What is Cascade?**PERSIST

Cascade defines what operations performed on a parent entity should automatically be applied to its child entities.

Without Cascade:

You must save/update/delete both parent and child manually.

With Cascade:

Hibernate performs those operations automatically on related entities.



What is Hibernate Dialect?

A Hibernate Dialect tells Hibernate which SQL syntax to generate for a specific database.

PostgreSQLDialect

MySQLDialect

OracleDialect



What is HQL?

HQL (Hibernate Query Language) is an object-oriented query language provided by Hibernate.

It operates on entity classes, not database tables.

FROM Employee (class)



| HQL                         | JPQL                  | Native SQL            |

| --------------------------- | --------------------- | --------------------- |

| Hibernate-specific          | JPA standard          | Database SQL          |

| Uses entity names           | Uses entity names     | Uses table names      |

| Database independent        | Database independent  | Database dependent    |

| Supports Hibernate features | Standard JPA features | Full SQL capabilities |



**Optimistic Locking (@Version):**

Optimistic Locking assumes that conflicts are rare.

It does not lock the database row. Instead, before updating, Hibernate checks whether someone else has already modified the data.

A and B reads A update the record version change to 2 B tries to update throw error

Optimistic Locking doesn't lock the record. It uses a version field (@Version) to check whether another user has updated the record before saving. If the version has changed, Hibernate throws an OptimisticLockException.



**Pessimistic Locking:**

Pessimistic Locking assumes conflicts are likely.

As soon as one user starts updating a row, Hibernate locks that row in the database.

Other users must wait until the first user finishes.

only after A completes the B can read. Only after User A commits can User B continue.

Pessimistic Locking locks the database row while a transaction is in progress. Other users cannot update the same row until the lock is released. It is useful when concurrent updates are expected frequently.



**What is JPA?**

JPA (Java Persistence API) is a Java Specification that defines a standard way to map Java objects to relational database tables.

It is not a framework and not an implementation.

JPA only defines interfaces, annotations, and rules.

Actual implementation is provided by ORM frameworks like:

Hibernate (Most Popular)

Why do we need JPA?

Different ORM frameworks had different APIs.

If you switched to another ORM, you had to rewrite your code.



| JPA                             | Hibernate              |

| ------------------------------- | ---------------------- |

| Specification                   | ORM Framework          |

| Defines rules                   | Implements those rules |

| Cannot run alone                | Can run independently  |

| Database-independent API        | ORM implementation     |

| Uses `EntityManager`            | Uses `Session`         |

| Uses `persist()`                | Uses `save()`          |

| Standard API                    | Hibernate-specific API |

| Portable across implementations | Vendor-specific        |




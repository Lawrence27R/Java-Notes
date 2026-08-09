**Spring and Spring Boot:**

@SpringBootApplication

Combination of:

@Configuration

@EnableAutoConfiguration

@ComponentScan

@EnableAutoConfiguration

Automatically configures beans based on dependencies.

Example:

If MySQL dependency exists → datasource configured automatically.

If Spring MVC exists → DispatcherServlet configured.



@ComponentScan

Scans packages for Spring beans.



@ConfigurationProperties

Used to map properties file values into Java object.



@Component

Generic Spring bean.

Spring automatically creates bean.

For generic utility/helper classes.



@Service

Specialized component for business logic.



@Repository

Used for DAO/database layer.



@Configuration

Marks configuration class.



@Bean

Manually creates bean.(Method-level)

Third-party classes

Custom bean creation



@Autowired

Automatic dependency injection.



@Qualifier

Used when multiple beans of same type exist.

@Autowired

@Qualifier("upiPaymentService")

private PaymentService service;



@Scope

Defines bean scope.

| Scope     | Meaning          |

| --------- | ---------------- |

| singleton | One object       |

| prototype | Multiple objects |

| request   | Per HTTP request |

| session   | Per session      |



@Lazy

Bean created only when needed.



@Primary

Default bean selected when multiple exist.



@RequestMapping

Maps URL to method/class.

GET

POST

PUT

DELETE



@RequestParam

Reads query parameters.

/user?id=10



@PathVariable

Reads value from URL path.

/user/10



@RequestBody

Converts JSON → Java object.



@ResponseBody

Converts Java object → JSON response.



| `@Controller` | `@RestController` |

| ------------- | ----------------- |

| Returns View  | Returns JSON      |

| MVC apps      | REST APIs         |

| JSP/HTML      | Microservices     |



@Transactional

@Transactional ensures that a group of database operations either all succeed or all fail together.

Spring creates proxy around method.

Used for database transaction management.

Uses:

AOP

Proxy pattern

| Type         | Meaning                   |

| ------------ | ------------------------- |

| REQUIRED     | Default                   |

| REQUIRES\_NEW | New transaction           |

| SUPPORTS     | Use existing if available |


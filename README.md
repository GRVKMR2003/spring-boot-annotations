# Spring Boot Important Annotations

Spring Boot provides several annotations that simplify development by handling configurations, dependency injections, and data handling. Below is a list of key annotations with examples.

## Core Spring Boot Annotations

### `@SpringBootApplication`
This annotation combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan` to enable the Spring Boot application.
```java
@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

### `@Configuration`
Used to define a configuration class, often with `@Bean` methods.
```java
@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

### `@ComponentScan`
Enables component scanning within a specified package.
```java
@SpringBootApplication
@ComponentScan(basePackages = "com.example")
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

## Dependency Injection

### `@Component`
Marks a class as a Spring-managed component.
```java
@Component
class ProductService {}
```

### `@Autowired`
Injects dependencies automatically.
```java
@Service
public class MyService {
    private final MyRepository myRepository;

    @Autowired
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }
}
```

### `@Qualifier`
Disambiguates between multiple beans of the same type.
```java
@Service
public class MyService {
    @Autowired
    @Qualifier("myRepositoryImpl")
    private MyRepository myRepository;
}
```

## Web Annotations

### `@Controller`
Marks a class as a Spring MVC controller.
```java
@Controller
public class MyController {
    @RequestMapping("/hello")
    @ResponseBody
    public String hello() {
        return "Hello, World!";
    }
}
```

### `@RestController`
A combination of `@Controller` and `@ResponseBody`.
```java
@RestController
public class MyRestController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }
}
```

### HTTP Method Mapping
```java
@GetMapping("/get")
@PostMapping("/post")
@PutMapping("/put")
```

### `@RequestBody`
Maps the body of an HTTP request to a Java object.
```java
@PostMapping("/user")
public ResponseEntity<String> createUser(@RequestBody User user) {
    return ResponseEntity.ok("User Created");
}
```

## Persistence Annotations

### `@Entity`
Marks a class as a JPA entity.
```java
@Entity
public class User {
    @Id
    @GeneratedValue
    private Long id;
    
    @Column(name = "username")
    private String username;
}
```

### `@Table`
Specifies the table name for an entity.
```java
@Entity
@Table(name = "users")
public class User {}
```

### `@Column`
Specifies column details in a database.
```java
@Column(name = "email", nullable = false, unique = true)
private String email;
```

### Relationship Mapping
```java
@OneToOne
@OneToMany
@ManyToMany
```

### `@Query` and `@Param`
Defines custom queries.
```java
@Query("SELECT u FROM User u WHERE u.username = :username")
User findByUsername(@Param("username") String username);
```

### `@Transactional`
Manages transactions in a Spring application.
```java
@Transactional
public void updateUser(User user) {
    userRepository.save(user);
}
```

## Configuration and Property Handling

### `@PropertySource`
Loads properties from external files.
```java
@PropertySource("classpath:application.properties")
public class AppConfig {}
```

### `@Value`
Injects values from properties.
```java
@Value("${server.port}")
private int serverPort;
```

### `@EnableWebMvc`
Enables Spring MVC in a Spring Boot application.
```java
@EnableWebMvc
@Configuration
public class WebConfig {}
```

### `@EnableAutoConfiguration`
Enables auto-configuration.
```java
@EnableAutoConfiguration
public class MyApplication {}
```

### `@ConditionalOnProperty`
Enables a component only if a property is set.
```java
@ConditionalOnProperty(name = "feature.enabled", havingValue = "true")
public class FeatureComponent {}
```

## Lifecycle Annotations

### `@EntityListeners`
Hooks into entity lifecycle events.
```java
@EntityListeners(AuditListener.class)
@Entity
public class User {}
```

### `@PrePersist`, `@PostPersist`, `@PreUpdate`, `@PostUpdate`, `@PreRemove`, `@PostRemove`
Used for lifecycle callbacks.
```java
@PrePersist
public void prePersist() {
    System.out.println("Before saving entity");
}
```

## Conclusion
These annotations help streamline Spring Boot development by handling configurations, dependency injections, web mappings, and database interactions efficiently. 🚀


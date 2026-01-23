### springboot

- Using **RestTemplate** for simple , direct communication between inter-service communication
- for more complex interations , we can use Feign client to make code cleaner
- for asynchronous communication we can use message brokers like RabitMQ or kafka
-  Spring cache abstraction can be used have like smar memory layer, we can implement this by adding @EnableCaching annotation 
   - @Cacheable	Triggers cache population. Use this for "Get" methods.
   - @CacheEvict	Removes data from the cache. Use this when data is deleted or updated.
   - @CachePut	Updates the cache without interfering with the method execution.
- For Performance , we can use springboot Actuator (spring-boot-starter-actuator -> dependencies) or splunk
   - to enable enbpoint we have to configure yaml with specific properties
   - To improve performance:
      - Implement caching for frequently accesses data
      - optimize database queries
      - use asynchronous methods for operations like sending emails using @EnableAsync
      - load balancer if traffic is high
      - Optimize the time complexity of the code
      - use webFlux to handle a large number of concurrent connections
      - 
- Best practices for versioing REST apis
   - URL versioning
     ```
          // Access via: GET /v1/person
           @GetMapping("v1/person")
           public PersonV1 getFirstVersion() {
               return new PersonV1("John Doe");
           }
         ```
   - Header versioning
       ```
         // Access via: GET /person with Header "X-API-VERSION=1"
        @GetMapping(value = "/person", headers = "X-API-VERSION=1")
        public PersonV1 getHeaderV1() {
            return new PersonV1("John Doe");
        }
       ```
   - Media Type versioning
     ```
       `// Access via: GET /person with Accept: application/vnd.company.app-v1+json
      @GetMapping(value = "/person", produces = "application/vnd.company.app-v1+json")
      public PersonV1 getMediaV1() {
          return new PersonV1("John Doe");
      }
     ```
   - Parameter Versioning
    ```
      // Access via: GET /person?version=1
      @GetMapping(value = "/person", params = "version=1")
      public PersonV1 getParamV1() {
          return new PersonV1("John Doe");
      }
    ```
  ---
  - Data access layer implementation by -> auto configures essentials like data cource and JPA/Hibername, it provides with built in repository support such as JPARepository
  - **basic implementations**
     ```
           // 1. DATA LAYER: Entity with Jackson annotations
         @Entity
         public class Product {
             @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
             private Long id;
             
             @JsonProperty("product_name") // Jackson customization
             private String name;
             
             @JsonIgnore // Jackson: Hide sensitive data
             private String secretInternalCode;
             
             // Getters/Setters...
         }
         
         // 2. DATA LAYER: Repository (Auto-configured JPA)
         @Repository
         public interface ProductRepository extends JpaRepository<Product, Long> {
             // Built-in: save(), findById(), findAll(), delete()
         }
         
         // 3. SERVICE LAYER: Logic + Smart Memory (Caching)
         @Service
         public class ProductService {
             @Autowired private ProductRepository repository;
         
             @Cacheable(value = "products", key = "#id") // Spring Cache
             public Product getProduct(Long id) {
                 // This runs only if the product isn't in memory
                 return repository.findById(id).orElseThrow();
             }
         }
         
         // 4. API LAYER: Versioned Controller (URL Versioning)
         @RestController
         @RequestMapping("/api/v1/products") // URL Versioning (Best Practice)
         public class ProductController {
             @Autowired private ProductService service;
         
             @GetMapping("/{id}")
             public Product getProduct(@PathVariable Long id) {
                 // Returns JSON via Jackson automatically
                 return service.getProduct(id);
             }
         }
         
         // 5. CONFIGURATION: Enable the features
         @SpringBootApplication
         @EnableCaching // Turns on the "Smart Memory" layer
         public class DemoApplication {
             public static void main(String[] args) {
                 SpringApplication.run(DemoApplication.class, args);
             }
         }
     ```
  - **Conditional annotation** -> enables only if certain condition are met

  ```
        // This interface defines the behavior
         public interface MessageService {
             void send(String message);
         }
         
         // CONDITION 1: This bean ONLY loads if "app.system.mode" is set to "prod"
         @Service
         @ConditionalOnProperty(name = "app.system.mode", havingValue = "prod")
         public class EmailService implements MessageService {
             public void send(String message) {
                 System.out.println("Sending real email: " + message);
             }
         }
         
         // CONDITION 2: This bean ONLY loads if "app.system.mode" is set to "dev"
         @Service
         @ConditionalOnProperty(name = "app.system.mode", havingValue = "dev")
         public class DummyService implements MessageService {
             public void send(String message) {
                 System.out.println("DEV MODE: Logging message to console: " + message);
             }
         }
  ```
- @EnableAutoConfiguration in springboot tells the framework to automatically set up the application based on its dependencies
- we can use spring security to configure requires authentication for accessing actuattor endpoint
- @Qualifier we can say which bean to use if there are multiple beans of same type, alternatively we can use @Primary over class implementation to make it default choice for spring
- User @transactional annotation on methods or class
- we canuse @springBootTest and @MockBean for doing unit testing and integaration testing
- using YAML supports hierarchical configuration , which is more readable and easier to manage , especially for complex structures
- Springboot profile are like having different settings for  our app depending onthe situation
   ```
      application-{profile}.properties
   ```
   -You can use the @Value annotation to pull the specific setting for the active profile into your Java classes.
   ```
      @RestController
      public class WelcomeController {
      
          @Value("${app.message}")
          private String welcomeMessage;
      
          @GetMapping("/welcome")
          public String getMessage() {
              return welcomeMessage;
          }
      }
```
- ,

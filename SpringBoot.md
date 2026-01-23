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
   

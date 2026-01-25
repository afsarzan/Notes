### System Design
**System design is extremely practival and there is a structured way to tackle the situtation**
 - ## Approach:
   - Understanding problem statement
   - Breaking down into components
   - Disecting each component - know the boundaries
   - For each-subcomponent look into
     1) Database and chaching
     2) Scaling and fault tolerance
     3) Async processing ( Delegation )
     4) Commmunication -> TCP,gRPC etc between component
 - ## How do you know that you have built a good system
    1) You broke your system into component
    2) Every component has a clear set of responsibilities like a webserver take request and read the database and serve reponse, its not his responsibility to know where is data is coming from who is inserting the data into.
    3) For each component, you've slight technical details figured out
    4) Each component in isolation is , scalable , falut tolerant , and available
---  
## Relational Databases:
 - Database were developed to support accounting , hence , key properties were
     1) Data consistency
     2) data durability
     3) data integrity
     4) constraints
     5) everything in one place
- relational databases provides "Transactions" - ACID
  -  Atomicity: 
    - All statemens within a transaction takes effect or none
    - eg 
        ```
        start transactions
        ... do some insert queries or update
        commit;
        ```
  -  Consistency:
    - Data will never go incorrect, no matter what constraints , cascades ( delete all related rows , foreign keys ) , triggers ( what to do at what time)
  -  Isolation:
    -  when multiple transactions are executing parallely the isolation level determines how much changes of one transaction are visibile to other
      1. **Repeatable Reads**: consistent reads within same transactions even if other transaction committed 1st transaction would not see the changes ( if value already read).
      2. **Read committed**; Reads within the same transaction always reads fresh value
          - con: Multiple reads within same transaction are inconsistent
      3. **Read uncommitted**: Read even uncommitted values from other txns -> dirty read eg: it is used systems like tracking dashboard, live data count where accuracy don't count only nearest value of those numbers mattered
      4. Serializable: Every read is locking read and while one is txn read, others will have to wait     
  -  Durability: 
    - when transactions commits , the changes outlive the outage
--- 
## Database scaling
 1) **Vertical Scaling**: add more cpu , ram disk -> requires downtime during reboot
 2) **Horizontal Scaling**: Read replicas
  - when read: write = 90:10
  - You move reads to other database, so that "master" is free to do writes
  - APi servers should know which DB to connect to get things done
 3)  **Replications**: Changs on one database ( master) Needs to be sent to replica to maintain consistency, there are two modes of replciation
     1) Synchronous replication: API pushes data to master, then master pushes to slave/replica then only API will respond to request
     2) Asynchronous replication APi pushes data to master then master reply back to API to serve request, but replica after configuration pulls the data
 4) **Horizontal scaling: sharding**
     - because one node cannot handle the data/ load we split it into multiple exclusive subsets writes on a particular row/ document will go to one particular shard.
 ---
 ## Sharding and Partitioning 
 - **Sharding:** method of distibuting data across multiple machines
 - **Partitioning:** spilitting a subset of data within the same instance
 ## Non -relational Databases
 - It is a very broad generatization of databases that are non-relational

# Distributed Systems and Related Concepts
## Distributed Systems
- **Characteristics**:
  - No shared clocks
  - No shared memory
  - Shared resources
  - Concurrency and consistency challenges
  - Different parts of the system need to communicate
  - Requires agreed-upon format or protocol
- **Potential Issues**:
  - Client can't find server
  - Server crash mid-request
  - Server response is lost
  - Client crashes
- **Benefits**:
  - More reliable, fault-tolerant
  - Scalability
  - Lower latency, increased performance
  - Cost-effective

## Performance Metrics
- **Scalability**:
  - Ability of a system to grow and manage increased traffic
  - Handles increased volume of data or requests
- **Reliability**:
  - Probability a system will fail during a period of time
  - Slightly harder to define than hardware reliability
- **Availability**:
  - Amount of time a system is operational during a period of time
  - Poorly designed software requiring downtime for updates is less available
- **Efficiency**:
  - How well the system performs
  - Latency and throughput often used as metrics
- **Manageability**:
  - Speed and difficulty involved with maintaining the system
  - Observability: how hard it is to track bugs
  - Difficulty of deploying updates
  - Aim to abstract away infrastructure so product engineers don't need to manage it
- **Manage Memory**:
  - (No further details provided)

## Load Balancers
- **Purpose**:
  - Balance incoming traffic to multiple servers
  - Used to improve reliability and scalability of applications
- **Types**:
  - Software-based (e.g., Nginx, HAProxy)
  - Hardware-based (e.g., F5, Citrix)
- **Note**: Two types of load balancers exist (details not specified)

## Distributed Cache
- **Functionality**:
  - Works like a traditional cache
  - Built-in functionality to replicate data, shard data across servers, and locate the proper server for each key

## Cache Eviction
- **Purpose**:
  - Prevent stale data
  - Cache only the most valuable data to save resources
- **Methods**:
  - **TTL (Time to Live)**:
    - Set a time period before a cache entry is deleted to prevent stale data
  - **LRU/LFU**:
    - **Least Recently Used (LRU)**: Once cache is full, remove the last accessed key and add a new key
    - **Least Frequently Used (LFU)**: Track the number of times a key is accessed, drop the least used when the cache is full

## Database Scaling
- **Indexes**:
  - Index based on a column
  - Speeds up read performance
  - Writes and updates become slightly slower
  - More storage required for the index
- **Denormalization**:
  - Add redundant data to tables to reduce joins
  - Boosts read performance
  - Slows down writes
  - Risks inconsistent data across tables
  - Code is harder to write
- **Connection Pooling**:
  - Allows multiple application threads to use the same database connection
  - Saves on the overhead of independent database connections
- **Caching**:
  - Tools: Redis, Memcached
 
## CAP Theorem:
- Parameters to evaluate a distributed system
  - **Consistency**: the system should deliver the same results no matter how and from where we query.
  - **Availability**: the system should always return some response or result
  - **Partition Tolerance**: The system should be functional even if one partition is disconnected.

## Rate Limiter:
- Implementing algorithm will be using token bucket , like how many can process at a time with refillers(amount of request at a time)
- another is fixed window counter allowing specified amount of request for a minute
- Sliding window log , takes memory
- Race Conditions : to void it use Lua scripts in Radis or atimic counters to ensure check and increment operation is thread-safe

## 

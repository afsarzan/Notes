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

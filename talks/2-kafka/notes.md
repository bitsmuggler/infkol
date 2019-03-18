# Sources

James Ward, Introduction to Apache Kafka, Devoxx Converence 2017, https://www.youtube.com/watch?v=UEg40Te8pnE
"A distributed streaming platform", Apache Foundation, https://kafka.apache.org/

- Problem
    - data integration is a challenge
    - complex integration systems
    - objects are no longer single records, but from different data sources
    - synchronization is hard
    - ETL (Extract, Transform, Load) is hard to scale
- events instead of tables (dynamic instead of static)
- go back in time is needed
- not only event stream, but a ledger to go back to a specific point in time
- message systems are not enough
    - ordering not necessarily guaranteed
    - do not scale horizontally
    - "push" is not always the answer
- Kafka: central hub of integration architecture
    - "event ledger"
    - keeping track of events
    - distributed and redundant
    - "distributed commit log"
    - linear scaling performance
- fundamentals
    - looks like a messaging system, uses that terminology
    - clustering is always used
    - durability
    - ordering guarantee
- use cases
    - integration hub for all data
    - etl (extract transform load) & cdc (change data capture)
    - hook search index, machine learning, data storage into that hub
        - producers/consumers (data pipeline)
    - big data ingest
        - data buffer for later consumption
- all clients are consumers (cli, web ui)
- records (events, messages) as the basic entity
    - key, value, timestamp
    - immutable (only insert/append)
- persistent ledger (on disks, not in memory)
    - broker: node in the cluster
    - producer writes records to a broker
    - consumer reads records from a broker
    - consumer asks for records, they are not pushed towards him
    - leader/follower (distribution)
    - disk cache is extremely fast nowadays
- topic: logical name for 1+ partitions
- replication on partition level, not topic level
- ordering guaranteed within partition
    - ordering/synchronization across partitions using timestamps
    - timestamp: time generated, time received, whatever... not clearly defined
- offset: unique sequential ID (per partition) of record
    - consumer asks Kafka for offset (starts at 0)
    - reconnect: > 0 (where left off)
    - benefits: replay (go back in time)
        - different consumers can work together (divide and conquer using offsets)
- produce message -> send to the leader partition of a topic
    - followers replicate that data (manually, key-based automatically)
    - replication factor: n copies of leader
    - auto rebalancing
    - production & consumption always against the leader
- consumer groups: dealing with partitions on consumer side
    - logical name for 1+ consumers (load balanced)
    - within the same consumer group, no message should be consumed more than once
- message delivery guarantees
    - producing messages
        - async (no delivery guarantee), fastest
        - committed to leader
        - committed to leader & followers (quorum), safest
        - IoT sensors: async
        - Banking: committed to l&f
    - consuming messages
        - at least once (default)
        - at most once
        - effectively once (1+ delivery, make sure it's not reprocessed)
        - exactly once
- log compaction (dealing with offset gaps) as a background process
- possible to tunnel data through sockets (not through JVM processes)
- partition balancing
- quotas for producers/consumers
- clients
    - JVM (official client)
    - polling based on consumption side (not pushed)
    - API: Producer.send(data), Consumer.fetch(Request), Consumer.getOffsetsBefore(topic, partition, ?)
    - AKKA streams: reactive streams (source/sink stream processing)
        - back-pressure (tell producer to slow down)
- text-based serialization (JSON, XML, YAML) too slow for intended loads

# Questions

1. Have you any experience running Kafka on a Kubernetes/OpenShift cluster?
2. Does Kafka behave well on a network file system like glusterfs?
3. Who (companies, institutions) do use it for what (use cases)?
4. Is Kafka the ultimate interface for interconnecting microservices?
5. What kinds of messages/payloads can you send? Also media files?

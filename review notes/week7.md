# Lecture 7: Big Data and CouchDB

#### "Big data Challenges and Architectures"
* **4V**
    1. **Volume** 数据量
    2. **Velocity** 新数据来的速度
    3. **Variety** 数据多样性
    4. **Veracity** 数据真实性
* Ad hoc solution
    * Relational model
        * tables and relationships amongst tables
    * Problem
        * relational DBMSs are extremely good at ensuring consistency, but rely on **normalised data models** (not granted in a world of big data: Veracity and Variety)
    * Solution: 
        * NoSQL DBMSs
* (NoSQL) DBMSs for distributed environments
    1. **key-value DMBS**
        * Allow the retrieval of **a chunk of data** given a key
        * Fast, but crude (粗糙)
        * E.g. Redis, PostgreSQL, Hstore, Berkeley
    2. **BigTable DMBS**
        * Stores data in columns, grouped into column families, with rows potentially containing different columns of the same family
        * E.g. Apache Cassandra, Apache Accumulo
    3. **Document-oriented DMBS**
        * Stores data as structured documents, usually in XML or JSON
        * E.g. Apache CouchDB, MongoDB
* Distributed databases are run over "clusters" (set of connected computers)
    * Clusters are needed to:
        * Distribute the computing load over multiple computers (e.g. improve **availability**)
        * Storing multiple copies of data (e.g. achieve **redundancy**)
    * Consider two document-oriented DBMs and their typical cluster architecture
        * CouchDB and MongoDB

#### CouchDB Cluster Architecture
* Answer requests
    * **All nodes answer requests** (read/write) at the same time
* Sharding
    * **Sharding** (splitting of data across nodes) is done on every node
* When a node does not contain a document"
    * the node **request it from another node** and returns it to the client
* Nodes can be added/removed easily
    * Their shards are **_re-balanced_** automatically upon addition/deletion of nodes

<img src="pic/couchdb.png" width="250">

#### MongoDB Cluster Architecture
* Sharing
    * **Sharding** is done at the _replica set_ level
    * Hence involve more than one cluster
    * (a shard is on the top of a replica set)
* Read/write requests
    * only **primary node** in a replica set answer **write** request
    * but **read** requests can (depending on the specific configuration) be answered by **every node** (including secondary nodes) in the set
* Updates
    * updates flow only from the primary to the secondary (node)
* Primary node fails
    * if a primary node fails, or discovers it is connected to a minority of nodes
    * a secondary of the same replica set is **elected as the primary**
* Arbiters (用来break tie的)
    * Arbiters: MongoDB instances without data
    * can assist in **breaking a tie** in the **election**
* Data are balanced across replica sets
* It is better to have an **odd** number of voting members

<img src="pic/mongodb.png" width="400">

#### MongoDB v.s. CouchDB Clusters
* MongoDB clusters are considerably **more complex**
* MongoDB clusters are **less available**
    * By default, only primary nodes can talk to clients for read operations (and exclusively so for write operations)
* MongoDB software **routers** (MongoS) must be embeded in the application
    * while **any HTTP client** can connect to CouchDB
* Losing 2 nodes out of 3
    * In CouchDB example, means losing access to 1/4 of data
    * In MongoDB example, means losing access to 1/2 of data
* Some features not supported in MongoDB shard environment
    * E.g. unique indexes

#### Consistency, Availablility, Partition-Tolerance (CAP)
1. Consistency (C)
    * every client receiving an answer **receives the same answer** from all nodes in the cluster
2. Availability (A)
    * every client **receives an answer** from any node in the cluster
3. Partition-Tolerance (P)
    * the cluster **keep on operating** when on or more nodes **cannot communicate** with the rest of the cluster
* Pick any 2, the intersection of 3 sets is **empty** !
* Brewer's CAP theorem
    * All three qualities are symmetrical
        * Consistency and Availability are at odds (争执/不一致) when a Partition happens
    * Network partitions
        * "Hard" ones may be rare
        * "Soft" ones not rare
            * slow node
        * Utimately (最后), every partition is detected by a timeout
        * Can have consequences (of partitions) that impact the cluster as a whole
            * E.g. a distributed join is only complete when all sub-queries return
        * Traditional DBMS architecture were not concerned with network partitions
            * since all data were supposed (在traditional的DBMS) to be in a small, co-located cluster of servers
        * The emphasis on numerous commodity (有益的) servers, can result in an increased number of **hardware failures**
    * CAP theorem forces us to consider **trade-offs** among different options

#### Classification of distributed processing algorithms
1. Two-phase commit
    * Consistency & Availbility
    * usual algorithm used in relational DBMS's (and MongoDB, to some extent)
    * Enforce **Consistency** by:
        * 锁定要用的数据，预写log，所有node都perform了才commit，如果有partition就rollback
        * locking data that are within the trasaction scope
        * Performing transactions on write-ahead (预写) logs
        * Completing transactions (commit) **only** when all nodes in the cluster have performed the transaction
        * **Abort** transactions (rollback) when a partition is detected
    * The procedure entails (意味着):
        * reduced availbility (data lock, **stop in case of partition**)
        * enforced consistency
    * A good solution when the cluster is co-located, less good when it is distributed
2. Paxos
    * Consistency & Partition-Tolerance
3. Muti-Version Concurrency Control (MVCC)
    * Availability & Partition-Tolerance

<img src="pic/cap.png" width="400">

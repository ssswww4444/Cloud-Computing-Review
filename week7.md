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
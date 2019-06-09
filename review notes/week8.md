# Lecture 8: Big Data Analytics

#### Intro to Big Data Analytics
* Challenges of Big Data Analytics:
    1. Reading & writing distributed datasets
    2. Preserving data in the presence of failing data nodes
    3. Supporting the execution of MapReduce tasks
    4. Being fault-tolerant
    5. Coordinating the execution of tasks across a cluster
* Tools for analytics:
    * Examples:
        * Statistical packages (R, Stata, SAS, ...)
        * Business Intelligence tools (Tableau, Business Objects, ...)
        * Information retrieval tool (ElasticSearch, IBM, ...)
    * In big data, most applications built on top of an **open-source framework**: **Apache Hadoop**

#### Apache Hadoop
* Started as a way to **distribute files over a cluster** and **execute MapReduce** tasks, but many tools have now been built on that foundation to add further functionality
* Hadoop Distributed File System (HDFS)
    * Core of Hadoop: **fault tolerant** file system that has been explicitly designed to span many nodes
    * HDFS blocks are **much larger blocks** used by an orginary file system (e.g. 4KB v.s. 128MB), reasons for this unusual size:
        * 减少储存block位置所需的内存，减少network使用，减少seek，如果每个block的大部分数据都被用到的话更efficient
        1. Reduced need for memory to store **information about where** the blocks are (meta)
        2. More efficient use of the network (a **reduced number of network connects** needs to kept open)
        3. Reduced need for **seek operations** on big files
        4. **Efficient** when most data of a block have to be processed
* HDFS file
    * a collection of blocks stored in **datanodes**, with metadata (such as position of those blocks) that is stored in **namenodes**

<img src="pic/hdfs.png" width="400">

#### Hadoop Resource Manager (YARN)
* 管理MapReduce的
* Another main component of Hadoop: **MapReduce task manager**, **YARN** (Yet Another Resource Negotiator)
* **YARN**: 
    * deals with executing MapReduce job on a cluster
    * composed of: 
        * a **central Resource Manager** on the master
        * many **Node Managers** that reside on slave machines
    * Steps:
        1. a MapReduce job scheduled for execution on a Hadoop cluster
        2. YARN starts an **Application Master** that negotiate resources with the **Resource Manager** and starts **Containers on the slave nodes**
            * Containers: processes where the actual processing is done, not Docker containers

#### HDFS Shell
* **Managing the files on a HDFS cluster** cannot be done on the operating system shell, hence a **custom HDFS shell** must be used
* HDFS file system shell replicates many of the usual command (ls, rm, etc.), with some **other commands** dedicated to loading files from the operating system to the cluster (and back):
    * `$HADOOP_HOME/bin/hadoop fs -copyFromLocal <localsrc> <dst>`
* Status of HDFS cluster and its content can be seen on a web application

#### Programming on Hadoop
* Main language for MapReduce on Hadoop: **Java**
    * other languages can be used via different APIs
    * indeed, any language that can read from standard input and write to standard output can be used
* `hadoop` command is used to: 
    * load the program and sent it to the cluster
        * with the `-file` option
    * the mapper and reducer can be specified by:
        * `-mapper` and `-reducer`
        * `aggregate` use the Hadooop internal _aggregator_ library
    * Example:
    
    ```BASH
    $HADOOP_HOME/bin/hadoop jar \
    $HADOOP_HOME/hadoop-streaming.jar \
    -D mapreduce.job.reduces=12 \
    -input myInputDir \
    -output myOutputDir \
    -mapper myAggregatorForKeyCount.py \
    -reducer aggregate \
    -file myAggregatorForKeyCount.py
    ```

#### Apache Spark
* Why Spark?
    * Hadoop is geared toward performing **relatively simple jobs on large datasets**
    * complex jobs (e.g. machine learning or graph-based algorithms) -> there is strong incentive (动机) for: 
        1. **caching** data in memory
        2. having **finer-grained control** on the execution of jobs
    * **Advantage:** 
        * designed to **reduce the latency** inherent (天生) in the Hadoop Approach for the execution of MapReduce jobs
    * Spark can **operate within the Hadoop architecture**: 
        1. Using **YARN and Zookeeper** to manage:      computing resources
        2. Storing data on **HDFS**
* Spark Architecture
    * One of the strong points of Spark is the **tighjtly-coupled** nature of its main components
    <img src="pic/spark.png" width="400">
    * Spark ships with a cluster manager of its own, but it can work with other cluster managers, such as **YARN or MESOS**
* Programming on Spark
    * mostly written in **Scala**, and uses this language by default in its interactive shell
        * however, APIs of Spark can be accessed by different languages: R, Python, and Java
    * Scala
        * multi-paradigm language: both functional and object-oriented
        * runs on JVM and can use Java libraries and Java objects
    * Most popular language used to develop Spark: Python and Java
        * other than Scala, there is a shell for Python (pySpark)
* Getting data in/out of Spark
    * Spark can read/write data in many formats, from text file to database, and it can use different file systems and DBMSs
    * Simplest way to get data into Spark (csv):
        * reading data from a csv file from the local file system
        * with a small change, Spark can be made to read from HDFS file system
        * `csv = sc.textFile("hdfs://file.csv")`
    * Another popular format: JSON
    * An efficient data format that is **unqiue** to Hadoop is: **sequence file**
        * a flat file composed of key/value pairs
    * Another option to load/save data:
        * serialised Java objects (Kryo library)
        * simple to implement, but neither faster nor robust
    * **HDFS or distributed DBMSs** can be used in conjunction with Spark
    * SQL queries can also be used to extract data
        * `df = sqlContext.sql("SELECT * FROM table")`
    * Relational DBMSs can be a source of data too
        * e.g. via JDBC
    * CouchDB, MangoDB, and ElasticSearch connectors are available
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
        1. Reduced need for memory to store **information about where** the blocks are (meta)
        2. More efficient use of the network (a **reduced number of network connects** needs to kept open)
        3. Reduced need for **seek operations** on big files
        4. **Efficient** when most data of a block have to be processed
* HDFS file
    * a collection of blocks stored in **datanodes**, with metadata (such as position of those blocks) that is stored in **namenodes**

<img src="pic/hdfs.png" width="400">

#### Hadoop Resource Manager (YARN)
* Another main component of Hadoop: **MapReduce task manager**, **YARN** (Yet Another Resource Negotiator)
* **YARN**: 
    * deals with executing MapReduce job on a cluster
    * composed of: 
        * a **central Resource Manager** on the master
        * many **Node Managers** that reside on slave machines
    * Steps:
        1. a MapReduce job scheduled for execution on a Hadoop cluster
        2. YARN starts an **Application Master** that negotiate resources with the **Resource Manager** and starts **Containers on the slave nodes**
    * 
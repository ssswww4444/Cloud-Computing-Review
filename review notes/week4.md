# Lecture 4: HPC and MPI

#### Supercomputers
* 任何有**高处理力**的计算机系统
* Any single computer system that has exceptional processing power for its time.

#### High Performance Computing (HPC)
* 任何有**可以达到高性能的架构**的计算机系统
* Any computer system whose architecture allows for above average performance
* Clustered computing: two or more computers serve a single resource
    * Improve performance and provide redundancy
    * Typically a collection of smaller computers strapped together with a high-speed local network 
* Clustered HPC
    * More **efficient, economical, and scalable** method -> dominates supercomputing

#### Parallel and Research Programming
* Parallel Computing
    * 数据和task分给多个processors处理
    * Submission of jobs or processors over multiple processors and by **splitting up data or tasks** between them
* Research Computing
    * 研究人员用的，问题：数据产生的越来越：快，多，多样
    * Software applications used by a research community to aid research
    * Major problem: volume/velocity(产生速度)/variety (3V) of datasets increases, the researchers will need to be able to process this data

#### HPC Cluster Design
<img src="pic/hpc_design.png" width="400">

#### Limitations of Parallel Computation
* Speedup (p) = Time (Serial) / Time (Parallel)
* Amdahl's law establishes the maximum improvement to a system (assumed fixed problem size)
<img src="pic/amdahl3.png" width="400">

#### Unimelb's HPC: Spartan
* A model of a HPC-Cloud Hybrid
* Featured in OpenStack and HPC Workload Management
* Environment Module
    * 用来改用户的environment
    * Dynamic **modification** of the user's **environment** via module files (e.g. paths)
    * Contains the necessary configuration info for user's session to operate according to the module loaded
    * Advantage: 
        * 给用户共享，并且可以安装同个应用的**不同版本**
        1. Shared with many users on a system
        2. Easily allowing multiple installations of the **same applications with different versions** and compilation options
* Module commands
    1. `module help` provides a list of switches, subcommands, and subcommand arguments
    2. `module avail` lists **all modules** which are available to be loaded
    3. `module whatis <modulefile>` description of the module
    4. `module display <modulefile>` to see exactly what a given modulefile will do to your environment (e.g. what will be added to PATH)
    5. `module load <modulefile>` add one or more module files to user's current environment
    6. `module unload <modulefile>` remove module from user's current environment
    7. `module purge` remove **all** modules from user's current environment
    8. In Spartan: `module spider` search for all possible modules (not just those in the existing module path)

#### Batch Systems and Wordload Managers
* Portable Batch System (PBS)
    * a utility software that **perform job scheduling** by assigning unattended background tasks expressed as **batch jobs** among the available resources
* Slurm Workload Manager
    * a popular job scheduler
    * also use **batch script** (very similar in intent and style to PBS script)
* Job scripts can be translated between PBS & Slurm

#### X-Windows Forwarding
* Cluster上做计算，用local来visualise结果
* Do computation on the cluster, visualisation on a local system
* Login with -Y option for security, then login with -X to the login node
* Compute node will then pass through the graphics via login node to the desktop system
* Need an X-window client on your desktop for the visualisation

#### Parallel Programmming
1. Shared Memory
    * Multithreading
        * Master thread forks sub-threads and divides tasks between them
        * Threads run concurrently, then joined at a subsequent point to resume normal serial application
    * One implementation: OpenMP
        * Application Program Interface
        * Include directives (指示) for **multi-threaded, shared memory** parallel programming
    * Easier, but limited to a single system unit (no distributed memory)
    * **Thread-based** rather than message passing
2. Distributed Memory
    * **Message passing** paradigm
    * Most popular standards: Message Passing Interface (MPI)
        * 互相发message来一起解决一个问题
        * A popular implementation: OpenMPI
        * Core principle: processors **cooperate to solve a problem by passing messages** to each other through a common communications network
        * Programmer is responsible for identifying opportunities for parallelism & implementing algorithms for parallelism using MPI

#### MPI Communication
* Managing communications
    1. `MPI_Status()`
    2. `MPI_Request()`
    3. `MPI_Barrier()`
    4. `MPI_Wtime()`
* Collective communications
    1. `MPI_Broadcast`
        * 从"root"广播一条信息，大家收到内容都一样，自己也会收到
        * Broadcast a message from "root" to all other processes of the communicator, **including itself**
    2. `MPI_Scatter`
        * 把"root"的一份数据拆分成N份分给processes，自己也会收到一份
        * Send data from one task to all tasks in a group
    3. `MPI_Gather`
        * 数据都收集到"root"
        * The inverse operation of MPI_Scatter
    4. `MPI_Allreduce`
        * 把reduce的结果发给所有的进程
        * Return reduced result to all processors
* Reduction Communications
    1. `MPI_Reduce`
        * 对communication group里所有进程（的数据）进行reduce的操作（比如sum，max等），结果返回给"root"
        * Perform a reduce operation (e.g. sum, max, logic AND) across all the members of a communication group
    2. `MPI_Allreduce`
        * 把reduce的结果发给所有的进程
        * Return reduced result to all processors

#### MPI Programming Basics
* Many parallel programs can be written using just these six functions:
    1. MPI_INIT
    2. MPI_FINALISE
    3. MPI_COMM_SIZE
    4. MPI_COMM_RANK
    5. MPI_SEND
    6. MPI_RECV
* MPI_SEND and MPI_RECV functions can be substituted with collective operations such as MPI_BCAST and MPI_REDUCE (improve simplicity and efficiency)
* Collective Operations
    1. MPI_BCAST: **distributes** data from one process (root) to all others in the communicator
    2. MPI_REDUCE: **combines** data from all processes in communicator and returns it to one process
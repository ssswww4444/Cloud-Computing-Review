# Lecture 4: Cloud Computing & NeCTAR/Unimelb Cloud & Scripting

#### Cloud Computing
* Defininition: 
    > a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction
* Most common cloud models
    1. Deployment models
        1. Private
        2. Community
        3. Public
        4. Hybrid (of above)
    2. Delivery Models
        1. **Software** as a Service (SaaS)
        2. **Platform** as a Service (PaaS)
        3. **Infrastructure** as a Service (IaaS)
    3. Essential Characteristics (5 characteristics in week1)
        1. On-demand self-service
        2. Broad network access
        3. Resource pooling
        4. Rapid elasticity
        5. Measured service

#### Deployment models (部署Cloud的模型)
1. Public Cloud
    * Pros
        * Utility (公用) computing
        * Can focus on core business (不需要关心intrastructure building和维护)
        * Cost-effective
        * "Right-sizing" (应该是指elasticity)
        * Democratisation (民主化) of computing
    * Cons
        * Security
        * Loss of control
        * Possible lock-in (占据)
        * Dependency of Cloud provider continused existence
2. Private Cloud
    * Pros
        * Control
        * Consolidation (巩固/合并) of resources
        * Easier to secure
        * More trust
    * Cons
        * Relevance to core business?
        * Staff / Management overheads
        * Hardware obsolescence (废弃/过时)
        * Over/under utilisation challenges
3. Hybrid Clouds (Public + Private)
    * Pros
        * 平时在private里跑，需要的时候用public
        * Cloud-bursting
            * Use private cloud, but **burst** into public cloud when needed
    * Cons
        * 怎么移动数据，怎么实时决定移动什么数据
        * How do you move data / resources when needed
        * How to decide (in real time) what data can go to public cloud
        * Is the public cloud compliant (遵从) with PCI-DSS (Payment Card Industry - Data Security Standard)
4. Community Cloud (没讲)

#### Delivery Models (提供service的模型)
* 不同模型的separation of responsbilities不同 
    * 每一块是你还是service provider来manage
<img src="pic/delivery_models.png" width="500">
* Software as a Service (SaaS)
    * 整个software打包好了来使用
    * public Saas examples: Gmail, Sharepoint, Microsoft 365, ...
* Infrastructure as a Service (IaaS)
    * 这门课的要点
    * 提供了Server和Storage之类的，自己选择操作系统，管理数据和开发应用
    * Many providers: AWS, Orable Public Cloud, Rackspace Cloud, Nectar/Openstack Research Cloud....
* Platform as a Service (PaaS)
    * 只能管理数据和自己开发应用
    * public Paas Examples: Google App Engine, Microsoft Azure, Amazon Elastic MapReduce, ...

#### NeCTAR
* Instances 主机
* Volumes 硬盘
    * Can be attached / detached
    * Must be in the same availability zone as the instance
* Images 映像
    * 
* Flavor
    * Defines the **compute, memory and storage** capacity
* Snapshot
    * 
* Ephemeral Disk
* Launching a new VM
    1. Choose Flavor
    2. Ephemeral Disk
    3. Create Key pair
    4. Copy pub key
    5. Select key pair
    6. Select security group
    7. Availability zone

#### Ansible

# Lecture 1: Cloud Computing

### Distributed System
> A system in which hardware or software components located at networked computers communicate and coordinate their actions only by message passing

### Cloud Computing
* Definition
    * jargon term without a commonly accepted non-ambiguous definition
    * a synonym for distributed computing
* 5 Characteristics:
    1. On-demand self-service
        * 顾客自主请求computing capabilities
        * consumer can provision computing capabilities as needed **without requiring human interaction** with each service provider.
    2. Networked access
        * 通过网络提供各种capabilities，使用标准机制，可用于不同客户平台
        * capabilities are **available over the network** and accessed through standard mechanisms that promote use by **heterogenous client platforms**
    3. Resource pooling
        * 服务供应商的计算资源给多个客户共用，使用multi-tenant model，各种virtual和physical的资源都可以根据客户需求分配/重分配
        * provider's computing resources are **pooled** to serve **multiple consumers** using multi-tenant model 
        * potentially with **different physical and virtual resources** that can be dynamically assigned and re-assigned according to consumer demand
    4. Rapid elasticity
        * capabilities 可以灵活快速的请求和释放（量多也可以）
        * capabilities can be **elastically  provisioned and released**, in some cases automatically, to **scale rapidly** upon demand.
    5. Measured service
        * 云系统使用metering capability来自动控制和最优化资源，根据资源类型
        * cloud systems automatically control and optimise resource use by leveraging a **metering capability** at some level of abstraction appropriate to the type of service.
* Flavours (types)
    1. Compute Clouds
    2. Data Clouds
    3. Application Clouds
    4. Private / Public / Hybrid / Mobile / ...  Clouds
    5. ...



# Lecture 2: Why we need CCC

Scaling:
1. Compute Scaling
2. Network Scaling

Data Deluge!!

Researcher need tools and methodologies to:
1. Search / Discover data
2. Use / Analyse data
3. Share data
4. Store data
5. Track data
6. Destroy data
7. Move data around
8. ...

Solution: HPC
* Security solutions involved integration of multiple technologies
* Secure, distributed file-based data management
* Meta-data capture through REST-based solution
* Job Submission to massive HPC systems
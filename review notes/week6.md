# Lecture 6: Web Services, REST Services, Twitter, Docker, and Containerisation

#### Architecture and Service-oriented Architecture
* System Architecture
    * Software component 怎么分布和交互的
    > The way different software components are **distributed** on computers, and the way which they **interact** with each other.
* Service-oriented Architecture (SoA)
    * When components are distributed (on different machine), cannot communicate directly
        * therefore components **interact** in more loosely-coupled ways
    * **Services** are often used for this
    * Typically, combinations and commonality (公共性) of services can be used to form a **SoA**
* SoA can serve many goals 可以达到各种目标
    * 提供一组对外的服务 (客户，或合作伙伴)
    * A set of externally facing services that a business wants to provide to their customers or parterns / collaborators
    * 一种基于服务供应商，中间人，和服务器请求者之间的协定的architecture pattern
    * An architecture pattern based on service providers, one or more brokers, and service requestors based on agreed service descriptions 
    * A programming model complete with standards, tools, and technologies that supports development and support of service
    * A middleware solution optimized for service assembly, orchestration, monotoring, and management
        * Can include tools and approaches that combine services together (e.g. as workflows)
* SoA
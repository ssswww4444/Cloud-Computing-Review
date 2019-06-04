# Lecture 3: Distributed & Parallel Computing Systems

#### Compute Scaling
* Vertical Scaling (速度)
    * Faster Processors
    * Limits of fundamental physics/matter
* Horizontal Scaling (量)
    * More Processors
        * Easier to get mroe
        * Harder to design, develop, test, debug, deploy, manage, understand, ...
        * For many / most folks: High-Throughput Computing (HTC) much more important than High-Performance Computing (HPC)
            * HPC 高性能计算机群(短期) -> characterized as needing large amounts of computing power for short periods of time
            * HTC 高通量计算机(长期) -> require large amounts of computing, but for much longer times (months and years, rather than hours and days)

#### (Types of) Adding More
1. Single machine multiple cores
2. Losely coupled cluster of machines (单纯共享资源)
    * Pooling / sharing of resources
3. Tighly coupled cluster of machines (机房那种，比loose更快)
    * Typical HPC / HTC set-up
    * Many server in same rack / server room (often with fast message passing interconnects)
4. Widely distributed clusters of machines (意义不明)
5. Hybrid combinations of the above

#### Adding more: limitations (Amdahl's Law)
* 因为有程序有non-parallizable (sequential) 的部分, 用再多的processor，加速（倍数）都会有上限
* 比如95%的程序都能被parallelized，**理论上**最多可以加速20倍 (1/alpha = 1/0.05 = 20, 可parallel的部分的计算时间无限接近于0)
![Amdahl's Law](amdahl.png)
![Amdahl's Law2](amdahl2.png)
* Over simplification of Amdahl's Law
    * 例子
        * 比如一个program要跑单个loop，现在每个processor负责一个iteration
        * 那每个processor现在就需要处理loop overheads (检查guard, loop completion, etc.), 有多少个process, 这个overheads就有多少
        * 所以这些loop overheads又可以看作跑这段代码的 **serial overhead**
    * Also assumed a fixed problem size
        * Sometimes can't **predict length of time required** for jobs

### Gaustafson-Barsis's Law
* Gives Scaled Speed-up
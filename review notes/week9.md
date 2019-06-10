# Lecture 9.1: Virtualisation (VM)

#### Terminology
* Virtual Machine (VM) Monitor/Hypervisor
    * the **virtualisation layer** between:
        1. underlying hardware
        2. VMs and the guest OS it supports
    * The environment of VM should appear to be the same as the physical machine
    *  Minor decrease in performance only
    * Appear as though in control of system resources

    <img src="pic/hypervisor.png" width="200">
* Virtual Machine (VM)
    * a **representation of a real machine** using hardware/software that can **host a guest OS**
* Guest Operating System (Guest OS)
    * an OS that runs in a **virtual machine environment** that would otherwise run directly on a separate physical system

#### Kernel-User mode separation
* process在user mode跑，kernel在kernel space跑，OS通常会虚拟化memory，CPU，和disk等，给process一种能使用一部分/整个资源的错觉，实际上processes之间要share资源
* Processes run in lower priviledged mode (user mode)
* OS typically _**virtualises**_ memory/CPU/disk, ...
    * **giving appearance of complete access** to CPU/memory/disk to application process
    * each process has **illusion** of access to some/all of the memory or the CPU
        * but actually shared across multiple processes
* **Context switches** can catch (trap) "sensitive" calls
    * sensitive calls: instruction sets are typically **device specific**
    * (Context switch: 换个thread来运行)

<img src="pic/kernal-user.png" width="400">

#### What happens in a VM
* Guest OS apps "think" they write to hard disk but **translated to virtualised** host hard drive **by VMM**
<img src="pic/in_vm.png" width="450">

#### Motivation of VM
1. Server Consolidation (合并)
    * increased utilisation
    * reduced energy consumption
2. Personal VM can be created on demand
    * No hardware purchase needed
    * public cloud computing
3. Security / Isolation
    * Share a single machine with multiple users
4. Hardware Independence
    * VM可以转移到别的hardware
    * Relocate to different hardware

#### Origins - Principles
* Properties of interest
    1. Fidelity (忠诚)
        * 在VMM跑和直接在机器上跑没两样，除了慢点
        * Software on the VMM executes behaviour **identical** to that demonstrated when running on the machine directly, barring (除了) timing effects
    2. Performance
        * VMM不介入的情况下，硬件跑很多guest intructions
        * An overwhelming majority of **guest instructions** executed by hardware without VMM intervention
    3. Safety
        * VMM管理所有硬件
        * The VMM manages all hardware resources

#### Classification of instructions
1. Privileged Instructions
    * 只能在kernel mode跑的
    * trap (中断执行) if the processor is in user mode and do not trap in kernel mode
2. Sensitive Instructions
    * 在不同hardware或者不同mode的情况下，instruction的behaviour不同
    * whose behaviour depends on the **mode** or **configuration** of the hardware
        * Different behaviour depending on whether in user/kernel mode
3. Innocuous (平淡) Instruction
    * Instructions that are neither privileged nor sensitive

#### Theorem: 
## 1 引论

### 1.1 What's OS

- GUI 和 shell 都不是OS的一部分。
- 重要区别：内核态 和 用户态
    - OS运行在内核态
    - 用户态底层：用户接口程序 GUI和shell

代码量：500万行：一个书架：仅仅是内核中的代码

加上基础应用：windows超过7000万行

- win95/98/Me
- winNT/2000/XP/Vista/7

#### OS历史：PC：

Digital Reasearch: CP/M: Control Program for Microcomputer: Gary Kildall

IBM - Gates: BASIC解释器

Seatle Computer Products: DOS: Disk Operating System: Tim Paterson: MS-DOS

Microsoft早期卖过UNIX：叫做XENIX

Doug Engelbart: 1960s: Stanford Research Institue: GUI(Windows, icon, menu, mouse): Xerox PARC研究员采用

Steve Jobs访问PARC，GUI：《探索未来》1988Smith和Alexander

第一个GUI：Lisa，太贵了，失败

第二个GUI：Macintosh，成功，user friendly

1999，Mac采用一种内核，本是为替换BSD UNIX内核而开发的CMU的Mach微核。因此macOS基于UNIX。

Mac -> Windows出现，运行在DOS上层，1985-1995十年间，win只是运行在DOS上的一个图形环境。

win95：第一个独立的windows版本。不过95和98大量使用16为Intel汇编语言。

winNT: David Cutler: 同时也是VAX VMS操作系统的设计师之一，VMS概念用到了NT上。VMS所有者是DEC公司。XP六年，成功。2007.1 Vista是个失败。win7小且稳定。2012，win8，失败。

FreeBSD: Berkeley的BSD项目，流行。

UNIX基本都支持X Window（MIT开发），X11之上还提供一个完整的GUI，比如Gnome或者KDE，使得UNIX可以像Mac或者windows。

#### OS历史：Mobile:

### 1.3 计算机硬件

推荐书：
- Tanenbaum和Austin 2012
- Patterson和Hennessy 2013

概念：
- 程序计数器：下一条指令的内存地址
- 堆栈指针：指向内存中当前栈的顶端。该栈包含了每个执行过程的栈帧。一个过程的栈帧保存了有关的输入参数、局部变量以及那些没有保存在寄存器中的临时变量。
- 程序状态字 Program Status Word：PSW寄存器：这个寄存器包含了条件码位（由比较指令设置）、CPU优先级、模式（内核态或者用户态）、以及各种其他控制位。用户程序通常读入整个PSW，但很少字段写入 。在系统调用和I/O中，PSW作用很重要。

流水线Pipeline v.s 超标量CPU

#### 系统调用

多数CPU有两种模式：内核态和用户态。PSW有一位控制。

系统调用Sytem call：为了从OS获得服务，用户程序通过系统调用以陷入内核并调用操作系统。用户程序位于用户态，仅允许执行子集，IO和内存保护的所有指令是禁止的。而内核态可以执行所有指令集，使用硬件的每一项功能。

TRAP指令把用户态切换到内核态。

#### 多线程 Multithreading 超线程 Hyperthreading

晶体管数量怎加，功能部件增多，控制逻辑也出现多个。多线程允许CPU保持两个不同的线程状态，然后在纳秒级的时间尺度内来回切换。（线程是一种轻量级的进程，即一个运行中的程序）。

忙等待 busy waiting

中断 

### 1.4 操作系统大观园

### 1.5 OS概念

#### 进程 process

正在执行的一个程序，有一个地址空间（address space），比如0-2MB。在这个地址空间，进程可以读写。地址空间放有可执行程序、程序的数据、程序的堆栈。进程还有资源集，通常包括寄存器（含有程序计数器和堆栈指针）、打开文件的清单、突出的报警、有关的进程清单，以及运行该程序所需要的所有其他信息。进程基本上是容纳运行一个程序需要所有信息的容器。

进程表 process table ：数组（或者链表）结构。

一个（挂起的）进程包括：进程的地址空间（往往称作**磁芯映像**，core image），以及对应的进程表项（其中包括寄存器以及稍后重启动该进程需要的其他信息）。

进程可创建子进程 -> 进程树

他们之间的通信 -> 进程间通信

系统管理器 给 每个进程 一个UID：User IDentification。 子进程和父进程一样UID。进程用户可以是某个进程组的成员，每个组也有一个GID。

- UNIX UID：superuser超级用户
- WIN UID: administrator管理员

#### 文件

目录 Directory

路径 win: 反斜线\ ; unix: 正斜线/

#### shell

sh csh ksh bash

推荐书：
- Kernighan和Pike 1984
- Quigley 2004
- Robbins 2005

#### 个体重复系统发育

鱼-哺乳动物-人

大型机-小型机-PC-PDA-智能手机

无论硬件软件，都要经过它们前辈的发展阶段。

CS，技术驱动。CPU远快于存储器，有了高速缓存。如果有一天存储器快于CPU，高速缓存小时。如果新技术使得CPU又快于存储器，高速缓存又出现。

生物学上，消失是永远的，但在计算机科学中，这种消失有时只是几年时间。

保护硬件 -> 多道程序处理：

早期大型机没有，IBM360有

8086没有，80286才有

这种重复系统发育例子有：
- 大型内存和汇编与高级语言的流行
- 保护硬件与多道程序处理
- 硬盘 从磁带到硬盘
- 虚拟内存

### 1.6 系统调用

以read系统调用为例，三个参数：
- 指定文件
- 指向缓冲区
- 要读出的字节数

UNIX 系统调用和系统调用的库过程之间几乎是一一对应的关系。

WIN几乎是不对应的。WIN32API，程序员用这套过程获得OS服务。win32有数千个，包含只在用户空间的调用。并不全是系统调用。

### 1.7 操作系统结构

单体：
- 主过程
- 服务过程
- 实用过程

可装载的拓展：UNIX叫做共享库shared library；  windows中叫做动态链接库 Dynamic link library，DLL C:\Windows\system32 1000多个

层次式系统

微内核：为了实现高可靠性

MINIX 3微内核只有12000行C代码和1400低层次汇编代码：用于捕获中断、进程切换等。

虚拟机
 
type 1 hypervisor 第一类虚拟机

VMware
VirtualBox
Hyper-V
KVM（linux）

第二类虚拟机

Java虚拟机

### 1.8 依靠C 的世界

显式指针：C有，而Java和Python没有。

.c -> 编译器 -> .o 目标文件

make 确定哪些文件要重新编译

.o -> linker -> .exe 可执行二进制文件

### 1.10 本书概要

第二章 进程与线程
第三章 地址空间和内存管理
第四章 文件系统
第五章 IO
第六章 死锁

第七章 虚拟化
第八章 多处理机系统 分布式系统 并行计算机
第九章 OS安全
第十章 案例 UNIX linux 和 android
第十一章 win8案例
第十二章 思考OS设计

### 1.11 单位

### 1.12 小结


































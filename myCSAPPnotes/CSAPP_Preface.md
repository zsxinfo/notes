# Preface
Our aim is to explain enduring concepts underlying all computer systems, and to show you the concrete ways that these ideas affect the correctness, performance, and utility of your application programs.

- enduring 经久不衰的
- concrete 具体的;混凝土
- utility 功用,效用;公共事业

## Assumption about the Reader's Backgroud

This book focuses on systems that execute x86-64 machine code. 

- colloquially 用白话;通俗语说.
- semiconductor 半导体
- transistor 晶体管

Microproocessor
- 16-bit words : 
    - 8086 (1978)
    - 80286 (1982)
- 32-bit words : ***IA32*** processors
    - 80386 (1985)
    - 80486 (1989)
    - Pentium (80586) (1993)
    - Pentium Pro (80686) (1995)
    - Pentium 4 (80786) (2000)
- 64-bit words : ***x86-64*** processors
    - AMD K8 (2003.09-2008)
    - Core 2 (2006)
    - Core i7/i5/i3 (2008)

We consider how these machines execute C programs on Linux.

We assum that you have access to Linux machine and be able to log in and do simple things like listing files and changing directories. If your computer runs MS Windows, we recommend that you install one of the many different virtual machine environments (such as Virtual Box or VMWare) that allow programs written for one OS (the guest OS) to run under another (the host OS).

We also assume that you have some familiarity with C or C++.

There are aspects of C (particularly pointers, explicit dynamic memory allocation, and formatted I/O) that do not exist in Java.

- pointers 指针
- explicit dynamic memory allocation 显式动态内存分配
- formatted I/O 格式化输入输出

反义词
- explicit 显然的;
- implicit 暗示的;

Early chapters explore the interactiions between C programs and their machine-language counterparts.
- counterpart 相应物;

We do not assume any prior experience with hardware, machine language, or assembly-language programming.

<br>

## How to Read the Book

In fact, we believe that the only way to learn systems is to do systems, either working concrete problems or writing and running programs on real systems.

- pervade 遍及;弥漫

When a new concept is introduced, it is followed in the text by one or more *practice problems* that you should work immediately to test your understanding.

As you read, try to solve each problem on your own and then check the solution to make sure you are on the right track. 

Each chapter is followed by a set of *homework* problems of varying difficulty. Your instructor has the solutions to the homework problems in an instructor's manual. For each homework problem, we show a rating of the amount of effort we feel it will require:

| Difficulty | Effort Requirement |
| ----:      | :----              |
|       \*   | Should require just a few minutes. Little or no programming required. |
|     \*\*   | Might require up to 20 minutes. Often involves writing and testing some code. (Many of these are derived from problems we have given on exams.) |
|   \*\*\*   | Requires a significant effort, perhaps 1-2 hours. Generally involves writing and testing a significant amount of code. |
| \*\*\*\*   | A lab assignment, requiring up to 10 hours of effort. |


- intervention 介入;干涉;干预
- manual 用手的;手工的;手册;指南
- encounter 遇到;

All of the source code is available from the CS:APP Web page at csapp.cs.cmu.edu.

Int the text, the filenames of the source programs are documented in horizontal bars that surround the formatted code. 

We encourage you to try running the example programs on your system as you encounter them.

To avoid having a book that is overwhelming, both in bulk and in content, we have created a number of *Web asides* containing material that supplements the main presentation of the book.

- overwhelming 压倒性的;巨大的;势不可挡的
- bulk 大小;体积;容量
- content 内容;目录;容量
- aside 在一旁;离开,撇开;(adv)旁白;私语,悄悄话;离题的话(n)
- supplement 补充物n;增补,补充v

These asides are referenced within the book with a notation of the form CHAP:TOP, where CHAP is a short encoding of the chapter subject, and TOP is a short code for the topic that is covered.

For example, Web Aside DATA:BOOL contains supplementary material on Boolean algebra for the presentation on data representions in Chapter 2, while Web Aside ARCH:VLOG contains material describing processor designs using the Verilog hardware description language, supplementing the presentation of processor design in Chapter 4. All of these Web asides are available from the CS:APP Web page.

## Book Overview

- capture 获得;捕获v;战利品;俘虏n
- overview 概述;综述
- computer arithmetic 计算机算术
- two's-complement 二进制补码
- encode 编码;译码
- novice 新手;初学者n
- parenthetical 插句的;附加说明的

12 chapters designed to capture the core ideas in the computer systems. Here is an overview.

- *Ch1: A Tour of Computer Systems.* 
    - This chapter introduces the major ideas and themes in computer systems by tracing the life cycle of a simple hello-world program.
- *Ch2: Representing and Manipulating Information.* 
    - We cover computer arithmetic, emphasizing the properties of unsigned and two's-complement number representaions that affect programmers. 
    - We consider how numbers are represented and therefore what range of values can be encoded for a given word size. 
    - We consider the effect of casting between signed and unsigned numbers. 
    - We cover the mathmatical properties and arithmetic operations.
    - Novice programmers are often surprised to learn that the (two's-complement) sum or product of two positive numbers can be negative.
    - On the other hand, two's-complement arithmetic satisfies many of the algebraic properties of integer arithmetic, and hence a compiler can safely transform multiplication by a constant into a sequence of shifts and adds.
    - We use the bit-level operations of C to demonstrate the principles and applications of Boolean algebra. 
    - We cover the IEEE floating-point format in terms of how it represents values and the mathematical properties of floating-point operations.
        - in terms of 就...而言;在...方面;
    - next paragragh<br> 
    - Having a solid understanding of computer arithmetic is critical to writing reliable programs. 
    - For example, programmers and compilers cannot replace the expresssion (x \< y) with (x - y \< 0), due to the possibility of overflow. 
    - They cannot even replace it with the expression (-y \< -x), due to the asymmetric range of negative and positive numbers in the two's-complement representation. 
        - asymmetric 不对称的
    - Arithmetic overflow is a common source of programming errors and security vulnerabilities, yet few other books cover the properties of computer arithmetic from a programmer's perspective.
        - vulnerability 弱点;漏洞
- *Ch3: Machine-Level Representatation of Programs.*
    - We teach you how to read the x86-64 machine code generated by a C compiler. 
    - We cover the basic instruction patterns generated for different control constructs, such as conditionals, loops, and switch statements.
        - generate 生成v计算机词汇
    - We cover the implementation (实行;执行;实现) of procedures (程序), including 
        - stack allocation, 
        - register usage conventions,
        - and parameter passing.
    - We cover the way different data structures such as structures, unions, and arrays are allocated and accessed. 
    - We cover the instructions that implement both integer and floating-point arithmetic. 
    - We alse use the machine-level view of programs as a way to understand common code security vulnerabilities, such as buffer overflow, and steps that the programmer, the compiler, and the operating system can take to reduce these threats. 
    - Learning the concepts in this chapter helps you become a better programmer, because you will understand how programs are represented on a machine. 
    - One certain benefit is you will develop a thorough and concrete understanding of pointers.
        - thorough 十分的;彻底的;周密的
- *Ch4: Processor Architecture.* 
    - This topic covers basic combinational and sequential logic elements, and then shows how these elements can be combined in a datapath that executes a simplified subset of the x86-64 instruction set called "Y86-64".
    - We begin with the design of a single-cycle datapath.
    - This design is conceptually very simple, but it would not be very fast. 
    - We then introduce *pipelining*, where the different steps required to process an instruction are implemented as separate stages.
    - At any given time, each stage can work on a different instruction. 
    - Our five-stage processor pipeline is much more realistic.
    - The control logic for the processor designs is described using a simple hardware description language called HCL.
    - Hardware designs written in HCL can be compiled and linked into simulators provided with the textbook, and they can be used to generate Verilog descriptions suitable for synthesis into working hardware.
        - synthesis <化学>合成;综合法
- *Ch5: Optimizing Program Performance.* 
    - This chapter introduces a number of techniques for improving code performance, with the idea being that programmers learn to write their C code in such a way that compiler can then generate efficient machine code.
    - We start with transformations that reduce the work to be done by a program and hence should be standard practice when writing any program for any machine.
    - We then progress to transformations that enhance the degree of instruction-level parallelism in the generated machine code, thereby improving their performance on modern "superscalar" processor.
    - To motivate these tansformations, we introduce a simple operational model of how modern out-of-order processor work, and show how to measure the potential performance of a program in terms of the critial paths through a graphical representation of a program. 
    - You will be surprised how much you can speed up a program by simple transformations of the C code.
- *Ch6: The Memory Hierarchy.*
    - The memory system is one of the most visible parts of a computer system to application programmers. 
    - To this point, you have relied on a conceptual model of the memory system as a linear array with uniform access times. 
    - In practice, a memory system is a hierachy of storage devices with different capacities, costs, and access times.
    - We cover the different types of RAM and ROM memories and the geometry and organizaiton of magnetic-disk and solid state drives. 
    - We describe how these storage devices are arranged in a hierarchy. 
    - We show how this hierachy is made possible by locality of reference. 
    - We make these ideas concrete by introducing a unique view of a memory system sa a "memory mountain" withe ridges of temporal locality and slopes of spatial locality.
        - ridge
        - temporal
        - locality
        - slope
        - spatial
    - Finally, we show you how to improve the performance of application programs by improving their temporal and spatial locality.
- *Ch7: Linking.* 
    - This chapter covers both static and dynamic linking, including the ideas of 
        - relocatable and executable object files, 
        - symbol resolution,
        - relocation,
        - static libraries,
        - shared object libraries,
        - position-independent code,
        - and library interpositioning.
    - Linking is not covered in most systems texts, but we cover it for two reasns.
    - First, some of the most confusing errors that programmers can encounter are related to glitches during linking, especially for large software packages.
        - glitches
    - Second, the object files produced by linkers are tied to concepts such as loading, virtual memory, and memory mapping.
        - loading
        - virtual memory
        - memory mapping
- *Ch8: Exceptional Control Flow.*
    - In this part of the presentation, we step beyond the single-program model by introducing the general concept of exceptional control flow (i.e. changes in control flow that are outside the normal branches and procedure calls).
    - We cover examples of exceptional control flow that exist at all levels of the system, 
        - from low-level hardware exceptions and interrupts, 
        - to context switches between concurrent processes, 
        - to abrupt changes in control flow caused by the receipt of Linux signals, 
        - to the nonlocal jumps in C that break the stack discipline.
            - concurrent 同时发生的
            - abrupt 突然的
            - nonlocal 非局部的
            - discipline 纪律
    - next paragraph<br>
    - This is the part of the book where we introduce the fundamental idea of a *process*, an abstraction of an excuting program.
    - You will learn processes work and how they can be created and manipulated from application programs.
    - We show how application programmer can make use of multiple processes via Linux system calls. 
    - When you finish this chapter, you will be able to write a simple Linux shell with job control.
    - It is also your first introduction to the nondeterministic behavior that arises with concurrent program excution.
- *Ch9: Virtual Memory.*
    - Our presentation of the virual memory system seeks to give some understanding of how it works and its characteristics.
        - characteristic 特性
    - We want you to know how it is that the different simultaneous processes can each use an identical range of addresses, sharing some pages but having individual copies of others.
        - simultaneous 同时的
    - We also cover issues involved in managing and manipulating virtual memory.
    - In particular, we cover the operation of storage allocators such as the standard-livrary malloc and free operations. 
    - Covering this material serves several purposes. 
    - It reinforces the concept that the virutal memory space is just an array of bytes that the program can subdivide into different storage units. 
        - reinforce
        - subdivide
    - It helps you understand the effects fo programs containing memory referencing errors such as storage leaks adn invalid pointer references. 
    - Finally, many application programmers write their own storage allocators optimized toward the needs and characteristics of the application. 
    - This chapter, more than any other, demonstrates the benefit of covering both the hardware and the software aspects of computer systems in a unified way. 
        - demonstrate
        - unified
    - Traditional computer architecture and operating systems texts present only part of the virtual memory story.
- *Ch11: Network Programming.*
    - Netwroks are interesting I/O devices to program, trying together many of the ideas that we study earlier in the text, suach as processed, signals, byte ordering, memoty mapping, and dynamic storage allocation. 
    - Network programs also provide a compelling context for concurrency, which is the topic of the next chapter.
        - compelling
    - This chapter is a thin slice through network programming that gets you to the point where you can write a simple Web server. 
    - We cover the client-server model that underlies all network applications.
    - We present a programmer's view of the Internet and show how to write Internet clients and serves using the sockets interface.
    - Finally, we introduce HTTP and develop a simple iterative Web server.
- *Ch12 Concurrent Programming.*
    - This chapter introduces concurerent programming using Internet server design as the running motivational example.
    - We compare adn contrast the three basic mechanisms for writing concurrent programs--processer, I/O multiplexing, and threads--and show how to use them to build concurrent Internet servers.
    - We cover basic principles of synchronization using 
        - *P* and *V* semaphore operations, 
        - thread safety and reentrancy,
        - race conditions,
        - and deadlocks.
    - We also describe the use of thread-level programming to express parallelism in an application program, enabling faster execution on multi-core processors.
    - Getting all of the cores working on a single computational problem requires a careful coordination of the concurrent threads, both for correctness and to achieve high performance.

<br>

## New to this edition

- emcompass 包围;包含;
- prompt 促进;提示;
- substantial 实质上的;大量的;可观的;
- revision 修订版;复习;
- exclusively 专门地;专有地;独占地;
- shift in focus 焦点转移

Summary of significant changes:
- *Ch1: A tour of computer systems* 
    - We have moved the discussion of Amdahl's Law from Ch5 to Ch1.
- *Ch2: Representing and manipulating Information*
    - A consistent bit of feeback from readers and reviewers is that some of the materials in this chapter can be a bit overwhelming.
        - consistent 一致的
    - So we have tried to make the material more accessible by clarifying the points at which we delve into a more mathematical style of presentation. 
        - delve into 钻研
    - This enable the readers to first skim over mathematical details to get a high-level overview and then return for a more thorough reading.
        - skim over 略过;速读
        - thorough 十分的;彻底的
- *Ch3: Machine-Level Representation of Programs.*
    - We have converted from the earlier presentation of based on a mix of IA86 and x86-64 to one based on entirely x86-64.
    - We have also updated for the style of code generated by more recent version of *gcc*. 
    - The result is a substantial rewriting, including changing the order in which some of the concepts are presented.
        - substantial 实质上 大量的 可观的
    - We also have included, for the first time, a presentation of the machined-level support for programs operating on floating-point data.
    - We have created a Web aside describing IA32 machine code for legacy reasons.
        - legacy 遗赠物 遗产 遗留系统 遗留
- *Ch4: Processor Architecture.*
    - We have revised the earlier processor design, based on a 32-bit architecture, to one that supports 64-bit words and operations.
- *Ch5: Optimizing Program Performance.*
    - We have updated the material to reflect the performance capabilities of recent generations of x86-64 processors. 
        - capability 性能
        - reflect 反射
    - With the introduction of more functional units and more sophisticated control logic, the model of program performance we developed based on a data-flow representation of programs has become more reliable predictor of performance than it was before.
        - sophisticated 复杂的
- *Ch6: The Memory Hierarchy.*
    - We have updated the material to reflect more recent technology.
- *Ch7: Linking.*
    - We have rewritten this chapter for x86-64, expanded the discussion of using the GOT and PLT to create position-independent code, and added a new section on a powerful technique on linking known as *library interpositioning*.
- *Ch8: Exceptional control flow.*
    - We have added a more regorous treatment of signal handlers, including async-signal-safe functions, specific guidelines for writing signal handlers, and using sigsuspend to wait for the handler.
        - async-signal-safe function
        - regorous 严格的
        - sigsuspend 信号暂停？信号缓期？挂起进程等待特定信号？
- *Ch9: Virtual Memory.*
    - This chapter has changed only slightly.
- *Ch10: System-Level I/O.*
    - We have added a new section on files and the file hierarchy, but otherwise, this chapter has changed only slightly.
- *Ch11: Networking Programming.*
    - We have introduced techniques for protol-independent and thread-safe network programming using the modern getaddrinfo and getnameinfo functions, which replace the obsolete and non-reentrant gethostbyname and gethostbyaddr functions.
        - protocol 协议
        - thread 线 线程
        - obsolete 老式的
        - reentrant 凹的 再进去的 可重入的
        - non-reentrant 不可重入
- *Ch12: Concurrent Programming.*
    - We have increased our coverage of using thread-level parallelism to make programs run faster on multi-core machines.
        - concurrent programming 并发编程
        - parallelism 平行
<br>
## Origin of the Book

- stem from 起源于
- stem 根茎
- sophomore 二年级生
- graduate student 研究生（已本科毕业生）
- undergraduate
- prerequisite 前提 先决条件

CMU 
15-213: Introduction to Computer Systems (ICS)
1998 fall

required core course for all undergraduates in the CS and ECE departments at Carnegie Mellon

prerequisite for most upper-level courses in CS and ECE

filter:
we would cover a topic only if it affected the preformance, correctness, or utility of user-level C programs
- performance
- correctness
- utility 效用 实用 利用率
<br>

out topic example:
- hardware adder
- bus design
<br>

in topic example:
- machine language
<br>

instead of focusing on how to write assembly language by hand, we would look at how a C compiler translates C constructs into machine code
- construct 构造n
<br>

- broad 宽
- holistic 整体的 全盘的
- faculty 能力 才能 全体教员 全体从业人员
- variant 变体 
- enlightened 开明的 进步的 有见识的
<br>

## For Instructors: Courses Based on the Book

- characterize 描绘 描述特征
<br>

Five systems courses based on CSAPP book
- **ORG.**: Computer Organization course with traditional topic: logic design, processor architecture, assembly language, and memory systems
- **ORG+.**: with additional emphasis on the impact of hardware on the performance of application programs. More about code optimization and more about improving the memory performance of their C program.
- **ICS.**: designed to produce enlightened programmers who understand the impact of the hardware, operating system, and compilation system on the performance and correctness of their application progarms. Diff from ORG+: low-level processor architecture not covered. Instead, programmers work with a higher-level model of a modern out-of-order processor. fits nicely into a 10-week quarter.
- **ICS+.**: with additional coverage of systems programming topics: system-level I/O, network programming, and concurrent programming. Cover everything except low-level processor architecture.
Semester-long CMU course.
- **SP.**: A systems programming course. Similar to ICS+, but it drops floating point and performance optimization, and it place more emphasis on systems programming, including process control, dynamic linking, system-level I/O, network programming, and concurrent programming. Instructors might want to supplement from other sources for advanced topics such as daemons, terminal control, and Unix IPC.
    - daemons 半人半神的精灵 守护进程 进程保护
    - Unix IPC 进程间通信 interprocess communication
<br>

Figure 2 Five courses
| Chapter | Topic     | ORG | ORG+ | ICS | ICS+ | SP |
| ---- | :---- | ---- | ---- | ---- | ---- | ---- |
| 1 | Tour of systems        | A | A | A | A | A |
| 2 | Data representation    | A | A | A | A | d |
| 3 | Machine language       | A | A | A | A | A | 
| 4 | Processor architecture | A | A |   |   |   |
| 5 | Code optimization      |   | A | A | A |   |
| 6 | Memory hierarchy       | a | A | A | A | a |
| 7 | Linking                |   |   | c | c | A |
| 8 | Exceptional control flow | |   | A | A | A |
| 9 | Virtual memory         | b | A | A | A | A |
| 10 | System-level I/O      |   |   |   | A | A |
| 11 | Network programming   |   |   |   | A | A |
| 12 | Concurrent programming |  |   |   | A | A |
<br>

A) All;  
a) hardware only;  
b) no dynamic storage allocation;  
c) no dynamic linking;  
d) no floating point;  
<br>

## For Instructors: Classroom-Tested Laboratory Exercises

- median scores 中位数
- means of  平均值
- cite 引用 传讯 想起 表彰
- the fun, exciting, and relevant laboratory exercises

The labs are available from CSAPP Web page.

*Data Lab.*
This lab requires students to implement simple logical and arithmetic functions, but using a highly restricted subset of C. For example, they must compute the absolute value of a number using only bit-level operatiions. This lab helps students understand the bit-level representations of C data types and the bit-level behavior of the operations on data.

*Binary Bomb Lab.* 
A binary bomb is a program provided to students as an object-code file. When run, it prompts the user to type in six different strings. If any of these are incorrect, the bomb "explodes", printing an error message and logging the event on a grading server. Students must "defuse" their own unique bombs by disassembling and reverse engineering the programs to determine what the six strings should be. The lab teaches students to understand assembly language and also forces them to learn how to use a debugger.

*Buffer Overfloww Lab.*
Students are required to modify the run-time behavior of a binary executable by exploiting a buffer overflow vulnerability. this lab teaches the students about the stack discipline and about the dangeer of writing code that is vulnerable to buffer overflow attacks.

*Architecture Lab.*
Several of the homework problems of Chapter 4 can be combined into a lab assignment, where students modify the HCL description of a processor to add new instructions, change the vranch prediction policy,o or add or remove bypassing paths and register ports. The resulting processors aan be simulated and run through automated tests that will detect most of the possible bugs. This labs lets students experience the exciting parts of pocessor design without requiring a complete background in logic design and hardware description langages.

*Performance Lab.* Students must optimize the performance of an application kernel function such as convolution or matrix transposition. This lab provides a very clear demonstration of the properties of cache memories and gives students experience with low-level program optimization.

*Cache Lab.*
In this alternative to the performance lab, students write a general-purpose cache simulator, and then optimize a samll matrix transpose kernel to minimize the number of misses on a simulated cache. We use the Valgrind tool to generate real address traces for the matrix transpose kernel.

*Shell Lab.*
Students implement their own Unix shell program with job control, including the Ctrl+C and Ctrl+Z keystrokes and the fg, bg, and jobs commands. This is the student's first introduction to concurrency, and it gives them a clear idea of Unix process control, signals, adn signal handling.

*Malloc Lab.*
Students implement their own versions of mallo, free, and (optionally) realloc. This lab gives students a clear understanding of data layout and organization, and requires them to evaluate different trade-offs between space and time efficiency.

*Proxy Lab.* 
Students implement a concurrent Web proxy that sits between their browsers and the rest of the World Wide Web. This lab exposes the students to such tipics as Web clients and servers, and ties together many of the concepts from the course, such as byte ordering, file I/O, process control, signals, signal handling, memory mapping, sockets, and concurrency. Students like being able to see their programs in action with real Web browsers and Web servers.

The CS:APP instrutro's manual has a detaied discussion of the labs, as well as directions for downloading the support software.

## Acknowledgments for the Third Edition
- acknowlegment 感谢















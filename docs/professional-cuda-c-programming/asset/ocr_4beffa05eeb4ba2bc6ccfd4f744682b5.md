# PARALLEL COMPUTING

During the past several decades, there has been ever-increasing interest in parallel computation. The primary goal of parallel computing is to improve the speed of computation.

From a pure calculation perspective, parallel computing can be defined as a form of computation in which many calculations are carried out simultaneously, operating on the principle that large problems can be divided into smaller ones, and each smaller one is solved concurrently.

From the programmer's perspective, a natural question is how to map the concurrent calculations onto computers. Suppose you have multiple computing resources, use of multiple computing resources (cores or computers) to perform the concurrent calculations. A large problem is broken down into smaller ones, and each smaller one is solved concurrently on different computing resources. The software and hardware aspects of parallel computing are closely intertwined together. In fact, parallel computing usually involves distinct areas of computing technologies:

+   * Computer architecture (hardware aspect)
* Parallel programming (software aspect)

Parallel architecture focuses on supporting parallelism at an architectural level, while parallel programming focuses on solving a problem concurrently by fully using the computational power of the computer architecture. In order to achieve parallel execution in software, the hardware must provide a platform that supports concurrent execution of multiple processes or multiple threads.

Most modern processors implement the Harvard architecture, as shown in Figure 1-1, which is comprised of three main components:

+   * Memory (instruction memory and data memory)
* Central processing unit (control unit and arithmetic logic unit)
* Input/Output interfaces

![](bbox=[0.095, 0.663, 0.536, 0.903])

FIGURE 1-1
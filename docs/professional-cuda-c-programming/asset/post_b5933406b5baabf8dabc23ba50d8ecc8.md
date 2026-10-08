
[content]

# CHAPTER 1 EXERCISES

1. Refer to Figure 1-5 and illustrate the following patterns of data partition:

- Block partition along the x dimension for 2D data
- Cyclic partition along the y dimension for 2D data
- Cyclic partition along the z dimension for 3D data

2. Remove the cudaDeviceReset function from hello.cu, then compile and run it to see what would happen.

3. Replace the function cudaDeviceRest in hello.cu with cudaDeviceSynchronize, then compile and run it to see what happens.

4. Refer to the section "Hello World from GPU." Remove the device architecture flag from the compiler command line and compile it as follows to see what happens.

```
$ nvcc hello.cu -o hello
```

5. Refer to the CUDA online document (http://docs.nvidia.com/cuda/index.html). Based on the section "CUDA Compiler Driver NVCC," what file suffixes does nvcc support compilation?

6. Each thread executes the kernel given a unique thread ID that is accessible within the kernel through the threadIdx.x variable. Modify the kernel function in hello.cu with the thread index to let the output be:

```
$ ./hello
Hello World from CPU!
Hello World from GPU thread !
```

# 2

# CUDA Programming Model

WHAT'S IN THIS CHAPTER?

- Writing a CUDA program
- Executing a kernel function
- Organizing threads with grids and blocks
- Measuring GPU performance

> The wrox.com downloads for this chapter are found at www.wrox.com/go/producad on the Download Code tab. The code is in the Chapter 2 download and individually named according to the names throughout the chapter.

CUDA is a parallel computing platform and programming model with a small set of extensions to the C language. With CUDA, you can implement a parallel algorithm as easily as you write C programs. You can build applications for a myriad of systems with CUDA on NVIDIA GPUs, ranging from embedded devices, tablet devices, laptops, desktops, and workstations for HPC clustered systems. Familiar programming software tools have been extended to help you edit, debug, and analyze your CUDA program during the lifetime of your project. In this chapter, you are going to learn how to write a CUDA program through two simple examples: vector addition and matrix addition.

# INTRODUCING THE CUDA PROGRAMMING MODEL

Programming models present an abstraction of computer architectures that act as a bridge between an application and its implementation on available hardware. Figure 2-1 illustrates the important layers of abstraction that lie between the program and the programming model implementation. The communication abstraction is the boundary between the program and the programming model implementation, which is realized through a compiler or libraries using privileged hardware primitives and the operating system. The program, written for a programming model, dictates how components of the program share information and coordinate their activities. The programming model provides a logical view of specific computing architectures. Typically, it is embodied in a programming language or programming environment.

![](img/506ba3a4c9f4512233692f3f20de1f3a_51_0.png)

FIGURE 2-1

In addition to sharing many abstractions with other parallel programming models, the CUDA programming model provides the following special features to harness the computing power of GPU architectures.

- A way to organize threads on the GPU through a hierarchy structure
- A way to access memory on the GPU through a hierarchy structure

You will focus on the first topic in this and the next chapter, and learn the second topic in Chapters 4 and 5.

From the perspective of a programmer, you can view parallel computation from different levels, such as:

- Domain level
- Logic level
- Hardware level

As you work through your program and algorithm design, your main concern is at the domain level: how to decompose data and functions to solve the problem correctly and efficiently while running in a parallel environment. When you enter the programming phase, your concern turns to how to organize your concurrent threads threads and calculations solve the problem correctly. In C parallel programming, you must manage your threads explicitly using either pthreads or OpenMP techniques. CUDA exposes a thread abstraction to allow you to control thread behavior. As you walk through examples in this book, you will see that this abstraction delivers superior scalability for parallel programming. At the hardware level, being able to understand how threads are mapped to cores may help improve performance.

The CUDA threading model exposes sensitive information to you without forcing too many low-level details. You will learn more about this in Chapter 3.

# CUDA Programming Structure

The CUDA programming model enables you to execute applications on heterogeneous computing systems by annotating code with small extensions to the C programming language. A heterogeneous environment consists of CPUs complemented by GPUs, each with its own memory shared by a PCI-Express bus. Therefore, you should note the following:

- Host: The CPU and its memory (host memory)
- Device: The GPU and its memory (device memory)

To clearly design the different memory spaces, example code in this book uses variable names that start with h_ for host memory, and d_ for device memory. Starting with CUDA 6, NVIDIA introduced a programming model improvement called Unified Memory, which bridges the divide between host and device memory. This improvement allows you to access both the CPU and GPU using a single pointer, while the system automatically migrates data between the host and device. More details about the unified memory will be covered in Chapter 4. For now, it is important that you learn how to allocate the host and device memory, and explicitly copy data that is shared between the CPU and GPU. The programmer-managed control of memory and data gives you the power to optimize your application and maximize hardware utilization.

A key component of the CUDA programming model is the kernel—the code that runs on the GPU. As the developer, you can express a kernel as a sequential function. From the scenes, CUDA schedules scheduling kernels on GPU threads. From the host, you define how your algorithm is mapped to the device based on application data and GPU capability. The intent is to enable you to use the logic of your algorithm in a straightforward fashion (by writing sequential code) and not get bogged down by details of creating and managing thousands of GPU threads.

The host can operate independently of the device for most operations. When a kernel has launched, the control is returned immediately to the host, freeing the GPU to perform additional tasks complemented by parallel code running on the device. The CUDA programming model is primarily asynchronous so that GPU computation performed on the GPU can be overlapped with host-communication. A typical CUDA program consists of serial code complemented by parallel code. As shown in Figure 2-2, the serial code (as well as task parallel code) is executed on the host, while the parallel code is executed on the GPU device. The host code is written in ANSI C, and the device code is written using CUDA. You can put all in a single source file, or use multiple files to build your application or libraries. The NVIDIA Compiler (nvcc) generates the executable code for CUDA host and device.

A typical processing flow of a CUDA program follows this pattern:

1. Copy data from CPU memory to GPU memory.
2. Invoke kernels to operate on the data stored in GPU memory.
3. Copy data back from GPU memory to CPU memory.

You will start learning about memory management and data movement between the host and device. Later, this chapter will cover more details on GPU kernel execution.

# ### CUDA C/++ Application

![](img/506ba3a4c9f4512233692f3f20de1f3a_53_0.png)

FIGURE 2-2

# ### Managing Memory

The CUDA programming model assumes a system composed of a host and a device, each with its own memory. Kernels operate out of device memory. To allow you to have full control and achieve the best performance, the CUDA runtime provides functions to allocate device memory, release device memory, and transfer data between the host memory and device memory. Table 2-1 lists the C functions and their corresponding CUDA functions for memory operations.

#### TABLE 2-1: Host and Device Memory Functions

| STANDARD C FUNCTIONS | CUDA FUNCTIONS |
| --- | --- |
| malloc | cudaMalloc |
| memmove | cudaMemcpy |
| memset | cudaMemset |
| free | cudaFree |

The function used to perform GPU memory allocation is cudaMalloc, and its function signature:
cudaError_t cudaMalloc( void** devPtr, size_t size )

This function allocates a linear range of device memory with the specified size in bytes. The allocated memory is returned through devPtr. You may notice the striking similarity between malloc and the standard C runtime malloc. This is intentional. By keeping the interface close to the standard C runtime libraries as possible, CUDA makes easy application porting.

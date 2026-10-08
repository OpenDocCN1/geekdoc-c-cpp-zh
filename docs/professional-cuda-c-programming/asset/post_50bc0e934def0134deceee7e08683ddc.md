
Shared memory is partitioned among all resident thread blocks; therefore, it is a critical resource and might limit kernel occupancy.

# Optimizing Instruction Execution

There are several ways to optimize kernel execution, including:

- Hiding latency by keeping sufficient active warps
- Hiding latency by assigning more independent work to a thread
- Avoiding divergent paths when it runs within a warp

Even though a CUDA kernel is expressed in scalar fashion as though it runs on a single CUDA core, the code is always executed in a warp unit in SIMT (single-instruction multiple-thread) fashion. When an instruction is issued for a warp, each thread carries out the same operation with its own data.

Threads can be organized by modifying the kernel execution configuration. The thread block size affects the number of active warps on an SM. GPUs hide latency by having asynchronous work in flight (such as global loads and stores) in order to saturate the warp schedule, pipeline, and memory bus. You can adjust the kernel execution configuration for more warps or each thread to do more independent work that can be pipelined and overlapped. GPU devices with different compute capabilities have different hardware limits; therefore, grid/block heuristics play a very important role in optimizing kernel performance on different platforms.

Because all threads in a warp execute the same instruction at each step, if there are different control flow paths within a warp due to data-dependent conditional branches, divergence among them might occur. When threads within a warp diverge, the warp must execute each branch in sequence while disabling threads that did not execute that path. Large portions of time for your application are in divergent code, it will significantly affect kernel performance.

Inter-communication and synchronization are very important features in parallel programming and can create obstacles to achieving good performance. CUDA provides several mechanisms that enable you to manage synchronization at different levels. Typically, you have two ways to explicitly synchronize your kernel. You can:

- Synchronize at the grid level
- Synchronize within a thread block

Synchronizing threads inside potentially divergent code is dangerous and can cause unanticipated errors. You must take care to ensure that all threads converge at explicit barrier point within a thread block. In general, synchronization adds overhead to a kernel and restricts the flexibility of the CUDA scheduler when deciding which warps in a thread block are eligible for execution.

# CUDA Code Compilation

The source code of a CUDA application generally contains two types of source files: conventional C source files and CUDA source files. Within a device code, there are two types:

- Facilitates code reuse and reduces compile time
- Lets you combine object files into static libraries
- Lets you link and call external device code
- Lets you create and use third-party libraries

# Separate Compilation

CUDA compilation embeds device code in host objects. With whole program compilation, executable device code is embedded in the host object. With separate compilation the process is not as simple. Three steps are:

1. The device compiler embeds re-locatable device code in the host file.
2. The device linker combines device objects.
3. The host linker combines device and host objects into a final executable.

Consider a simple example that contains three files: a.cu, b.cu, and c.cpp. Because you reference across two files, you have to use separate compilation to generate the executable. If you are targeting a Fermi device (compute 2.x), you first generate re-locatable objects using the following command:

```
$ nvcc -arch=sm_20 -dc a.cu b.cu
```

The option -dc passed to nvcc instructs the compiler to compile each input file (a.cu and b.cu) into an object file that contains re-locatable device code. Next, you link all device objects together using the following command:

```
$ nvcc -arch=sm_20 -dlink a.o b.o -o link.o
```

The option -dlink passed to nvcc causes all device objects with re-locatable device code (a.o and b.o) to be linked into an object file (link.o) that can be passed to the host linker. Finally, the host linker is used to generate the executable, as follows:

```
$ g++ -c c.cpp -o c.o
$ g++ link.o -o test -L<path> -lcudart
```

Figure 10-3 illustrates the separate compilation process.

# Sample Makefile

Listing 10-1 is a sample Makefile that uses separate compilation. You will need to replace the full path names and update the name of the executable in the sample Makefile to match your working environment. You can extend this sample to a typical project that has:

- Both C and CUDA files
- Device function or device variable references across CUDA C files

![](img/506ba3a4c9f4512233692f3f20de1f3a_462_0.png)

FIGURE 10-3

The file sample-makefile can be downloaded from wrox.com.

# LISTING 10-1: Sample Makefile (Makefile)

```
SRCS := $(wildcard *.c)
OBJS := $(patsubst %.c,%.o,$(SRCS))

CUDA_SRCS := $(wildcard *.cu)
CUDA_OBJS := $(patsubst %.cu,%.o,$(SRCS))

CUDA_PATH := /usr/local/cuda-6.0 specify CUDA root path
NVCC := $(CUDA_PATH)/bin/nvcc
CC := icc
LD := icc -fopenmp

CUDA_LIB := -L$(CUDA_PATH)/lib64 -lcublas -lcufft -lcudart
CUDA_INC += -I$(CUDA_PATH)/include
```

# LISTING 10-1 (continued)

```
CFLAGS      += -std=c39
INCLUDES    += # specify include path for host code

GPU_CARD     := -arch=sm_35 # specify your device compute capability
NVCC_FLAGS   += -O3 -dc # separate compilation
NVCC_FLAGS   += -xcompiler -fopennm
CUDA_LINK_FLAGS := -dlink # device linker option

EXEC         := test # test your executable name
CUDA_LINK_OBJ := cuLink.o

all: $(EXEC)
	$(OBJS) $(CUDA_OBJS)
	$(NVCC) $(GPU_CARD) $(CUDA_LINK_FLAGS) -o $(CUDA_LINK_OBJ) $(CUDA_OBJS)
	$(LD) -o $@ $(OBJS) $(CUDA_OBJS) $(CUDA_LINK_OBJ) $(CUDA_LIB)

%.o: %.c
	$(CC) -o $@ -c $(CFLAGS) $(INCLUDES) <

%.cu: %.cu
	$(NVCC) $(GPU_CARD) $(NVCC_FLAGS) -o $@

clean:
	rm -f $(OBJS) $(CUDA_OBJS) $(CUDA_LINK_OBJ) $(EXEC)

install:


# Integrating CUDA Files into C

CUDA provides two sets of runtime:

- An interface with C++ conventions
- An interface with C conventions

When porting C to CUDA, you might need to prepare device memory and data from functions. For example, to call CUDA runtime you need to include the:

```
#include <cuda_runtime.h>
```

To call kernel launch because host functions in device source files default to C++, you will also need to use the following declaration to resolve mangled:

```cpp
extern "C" void wrapper_launch(...);
```

The keyword extern "C" indicates to the compiler that the host function name should be unmangled so that it can be linked with C. Figure 10-4 illustrates how you can organize a kernel function using:

# Host Files

# Device Files

```
#include <cuda_runtime.h>

extern "C"
void launch_myKernel(...)
{
    myKernel<<<grid,block>>>(...);
}

global void myKernel(...)
{
}
```

![](img/506ba3a4c9f4512233692f3f20de1f3a_464_0.png)

FIGURE 10-4

# CUDA Error Handling

Error handling is arguably the least glamorous but most important part of production application development. Building a program that will be able to stand up to the tortures of misuse without undefined behavior is a necessity before deploying any application in a production environment.

Fortunately, CUDA makes it easy to detect errors. Every CUDA API and library call returns an error code indicating success or details about a failure. These error codes can be useful in recovering from the error, or displaying an informative message to the user. Just as in any systems-level software development project, checking these error on function call is a requirement for stability.

One idiosyncrasy of CUDA error checking is its asynchrony. Error codes returned from a function call may or not be a result of actions performed by that particular call. The function may be returning information on an error caused by any previous asynchronous call which may still be executing. This complicates the process of providing useful error messages to the user or recovering from failure. These problems can be mitigated by avoiding operations run in parallel, and being prepared to handle errors from any function.

CUDA provides three function calls that you can use for error checking. cudaLastError checks the current state of CUDA for reported errors. If no errors have been recorded, it returns cudaSuccess. If one has been recorded, it returns error and clears the internal CUDA state to be cudaSuccess. As a result, multiple calls to cudaLastError return an error, the calling

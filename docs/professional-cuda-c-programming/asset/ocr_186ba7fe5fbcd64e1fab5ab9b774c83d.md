In this example, you have two GPUs installed (your configuration may be different, and may show more or fewer devices). Now you are ready to write your first CUDA C code. To write a CUDA C program, you need to:

+   1. Create a source code file with the special name extension of `.cu`.

+   2. Compile the program using the CUDA `nvcc` compiler.

+   3. Run the executable file from the command line, which contains the kernel code executable on the GPU.

As a starting point, write a C program to print "Hello World" as follows:

```
```c
#include <stdio.h>
int main(void)
{
    printf("Hello World from CPU!\n");
}
```
```

Save the code into `hello.cu` and then compile it with `nvcc`. The CUDA `nvcc` compiler has similar semantics to `gcc` and other compilers.

```
$ nvcc hello.cu -o hello
```

If you run the executable file `hello`, it will print:

Hello World from CPU!

Next, write a kernel function, named `helloFromGPU`, to print the string of "Hello World from GPU!" as follows:

```
```c
global__ void helloFromGPU(void)
{
    printf("Hello World from GPU!\n");
}
```
```

The qualifier `global__` tells that the function will be called from the CPU and executed on the GPU. Launch the kernel with `<<<1,10>>>`.

```
helloFromGPU<<<1,10>>>();
```

Triple angle brackets mark a call from the host to the code on the device side. A kernel is executed by an array of threads and all threads run the same kernel. The parameters within the triple angle brackets are the execution configuration, which specifies how many threads will execute the kernel. In this example, you will run 10 GPU threads. Putting all these things together, you have the program in Listing I-1:

# LISTING 1-1: Hello World from GPU (hello.cu)

```
```c
#include <stdio.h>
global__ void helloFromGPU(void)
{
    printf("Hello World from GPU!\n");
}
```
```
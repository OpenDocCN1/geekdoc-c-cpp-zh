# # Threading on GPUs

So coming back to threads, let's look at a section of code and see what this means from a programming perspective.

```
```c
void some_func(void)
{
    int i;

    for (i=0;i<128;i++)
    {
        a[i] = b[i] * c[i];
    }
}
```
```

This piece of code is very simple. It stores the result of a multiplication of b and c value for a given index in the result variable a for that same index. The for loop iterates 128 times (indexes 0 to 127). In CUDA you could translate this to 128 threads, each of which executes the line

```
```c
a[i] = b[i] * c[i];
```
```

This is possible because there is no dependency between one iteration of the loop and the next. Thus, to transform this into a parallel program is actually quite easy. This is called loop parallelization and is very much the basis for one of the more popular parallel language extensions, OpenMP.

On a quad-core CPU you could also translate this to four blocks, where CPU core 1 handles indexes 0-31, core 2 indexes 32-63, core 3 indexes 64-95, and core 4 indexes 96-127. Some compilers will either automatically translate such blocks or translate them where the programmer marks that this loop can be parallelized. The Intel compiler is particularly good at this. Such compilers can be used to create embedded SSE instructions to vectorize a loop in this way, in addition to spawning multiple threads. This gives two levels of parallelism and is not too different from the GPU model.

In CUDA, you translate this loop by creating a kernel function, which is a function that executes on the GPU only and cannot be executed directly on the CPU. In the CUDA programming model the CPU handles the serial code execution, which is where it excels. When you come to a computationally intense section of code the CPU hands it over to the GPU to make use of the huge computational power it has. Some of you might remember the days when CPUs would use a floating-point coprocessor. Applications that used a large amount of floating-point math ran many times faster on machines fitted with such coprocessors. Exactly the same is true for GPUs. They are used to accelerate computationally intense sections of a program.

The GPU kernel function, conceptually, looks identical to the loop body, but with the loop structure removed. Thus, you have the following:

```
```c
__global__ void some_kernel_func(int * const a, const int * const b, const int * const c)
{
    a[i] = b[i] * c[i];
}
```
```

Notice you have lost the loop and the loop control variable, i. You also have a __global__ prefix added to the C function that tells the compiler to generate GPU code and not CPU
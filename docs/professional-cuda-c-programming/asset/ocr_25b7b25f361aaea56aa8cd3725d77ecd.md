gang-partitioned mode, worker-partitioned mode, etc. In CUDA, the compiler searches the block of code decorated by the kernels for parallel loops that can be executed in CUDA kernels. Any code within a kernels block that is not parallelized is still executed, but not in parallel.

As a simple example, consider the code in simple-kernels.c available from Wix.com. The core logic is included in the following snippet:

```
#pragma acc kernels
{
    for (i = 0; i < N; i++) {
        C[i] = A[i] + B[i];
    }
    for (i = 0; i < N; i++) {
        D[i] = C[i] * A[i];
    }
}
```

This kernels block contains two loops that can be parallelized. If you have a PGI compiler, this example can be compiled with:

```
$ pgcc -acc simple-kernels.c -o simple-kernels
```

Adding the -acc flag enables PGI compiler support for OpenACC, allowing it to recognize any #pragma acc directives in the provided code. It is also strongly recommended that you add the -Minofacc flag to the PGI compiler to gain insight into how auto-parallelization is performed. Using-Minofacc with simple-kernels.c produces the following output:

```
$ pgcc -acc -Minofacc simple-kernels.c -o simple-kernels
main:
34, Generating present_or_copout(C[:1024])
Generating present_or_copyn(A[:1024])
Generating present_or_copyn(B[:1024])
Generating present_or_copout(D[:1024])
Generating Tesla code
36, Loop is parallelizable
    Accelerator kernel generated
36, #pragma acc loop gang, vector(128) /* blockIdx.x threadIdx.x */
39, Loop is parallelizable
    Accelerator kernel generated
39, #pragma acc loop gang, vector(128) /* blockIdx.x threadIdx.x */ *
```

For now, the statements that mention present_or_copout and present_or_copyn will be covered in the next section on "Using OpenACC Data Directives.\ Instead, consider the lines labeled 36 and 39, indicating the source lines where each loop starts. In both cases, OpenACC automatically finds that the loop is parallelizable. It also prints information on the parallelization strategy used for each loop:

```
#pragma acc loop gang, vector(128) /* blockIdx.x threadIdx.x */
```

This information indicates that both loops are fully parallelized across gangs and vectors, with a vector width of 128 elements. In CUDA terms, this will map to a thread block
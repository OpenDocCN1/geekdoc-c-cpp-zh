
# TABLE 8-5: Loop Clauses

| CLAUSE | BEHAVIOR IN A PARALLEL REGION | BEHAVIOR IN A KERNELS REGION |
|---|---|---|
| collapse(int) | Marks a loop directive as applying to multiple nested loops. The number of nested loops is specified with the argument to collapse. | Same as parallel |
| gang(int) | Indicates that a loop should be distributed across parallel gangs. The number of gangs is set by the parallel directive. | Indicates that a loop should be distributed across parallel gangs. gang integer optionally takes a single integer argument: the number of workers to use when executing the loop |
| worker(int) | Indicates that a loop should be distributed in parallel across workers in each gang, transitioning each gang from worker-single to worker-partitioned mode. | Indicates that a loop should be distributed in parallel across workers in each gang. Worker optionally takes a single integer argument: the number of workers to use for each |
| vector(int) | Indicates that a loop should be distributed by vector elements. Causes a worker to transition from single to vector-partitioned mode. | Indicates that a loop should be distributed by vector elements. vector optionally takes a single integer argument: the width to use for each worker |
| seq | Force the loops marked with seq to be executed sequentially by the accelerator. | Same as parallel |
| auto | Indicates that the compiler should select gang, worker, or vector parallelism for the associated loop | Same as parallel |
| tile(int, ...) | Tiles the attached loop(s) by the provided tile size. This converts a loop into two loops: an inner loop of tile_size iterations and an outer loop, which executes sufficient times to match the original code behavior. If attached to multiple tightly nested loops, tile can take multiple tile sizes and automatically place all outer loops outside of all inner loops. | Same as parallel |

# TABLE 8-5 (continued)

| CLAUSE | BEHAVIOR IN A PARALLEL REGION | BEHAVIOR IN A KERNELS REGION |
|---|---|---|
| device_type(type) | Acts as a demarcator between clause lists for different device types. All clauses following a device_type and until the end of the directive or the next device_type clause apply when the loop is being run on the specified device type. | Same as parallel |
| independent | Asserts that the marked loop is parallelizable, overriding compiler analysis. | Same as parallel |
| private(var, ...) | Create grant-private copies of each of the specified variables for the marked loop. | Same as parallel |
| reduction | See the discussion of reduction earlier in this section. | Same as parallel |

You can also combine the **loop directive** with *parallel* or *kernels* in a single **pragma**:

```
#pragma acc parallel loop
for (i = 0; i < N; i++) {
}

#pragma acc kernels loop
for (i = 0; i < N; i++) {
}
```

These are simply shortcut directs that expand to *parallel* and *kernels* directives that are immediately followed by a loop directive:

```
#pragma acc parallel
{
#pragma acc loop
for (i = 0; i < N; i++) {
  
}
}
#pragma acc kernels
{
#pragma acc loop
for (i = 0; i < N; i++) {
  
}
}
```

# OpenACC Compute Directives Summary

This section covered a variety of OpenACC clauses and directives that can be used to parallelize computational regions of code on an accelerator. While the kernels directive is automated and gives the compiler freedom to automatically parallelize a region without burden on you, the parallel directive gives you more control over how code is parallelized. In both cases, the loop directive can be used to tell the compiler to parallelize the attached loop.

While this section provided comprehensive coverage of techniques for mapping computation to the accelerator in OpenACC, you may have noticed that no mention was made of communication between the host application and its accelerator. The parallel and kernels directives automatically performed all transfers for you. The next section will cover how the OpenACC data directive and additional clauses are used to optimize host-accelerator communication in OpenACC.

# Using OpenACC Data Directives

It is possible to write OpenACC programs with absolutely no concern for data movement. However, doing so will drastically reduce performance as OpenACC conservatively performs communication than may be necessary. This section will cover how the #pragma data directive is used to explicitly perform communication between the host and an OpenACC accelerator. You will also learn about related data clauses that may be applied to the parallel and kernels directives.

# Using the data Directive

In OpenACC, #pragma data is used to explicitly transfer data between the host application and accelerator, similar to the variants of cudaMemcpy CUDA. Like the kernels and parallel directives, data is applied to a region of code. It defines the transfers that must be performed on the boundaries of that region. For instance a variable can be marked as copying, meaning it is transferred to the accelerator at the start of the region but not transferred out at the end. Inversely, copyout transfers the content back to the host at the end of a data region, but does not transfer them to the accelerator at the start.

As an example, consider simple-data.c available for download from Wrox.com. simple-data.c is an extension of simple-parallel.c. The core logic is outlined inline below:

```
#pragma acc copyin(A[0:N], B[0:N]) copyout(C[0:N], D[0:N])
#pragma acc parallel
{
  #pragma acc loop
  for (i = 0; i < N; i++) {
    C[i] = A[i] + B[i];
  }

  #pragma acc loop
  for (i = 0; i < N; i++) {
    D[i] = C[i] * A[i];
  }
}
```

The added #pragma acc data directive informs the compiler that A and B should be copied to the device, while C and D should be copied back. This statement also specifies the range of the arrays to transfer, in this entire array. In some cases, the compiler may be able to infer the size of the arrays being copied, which would slightly simplify this:

```
#pragma acc data copyin(A, B) copyout(C, D)
```

As a result of these modifications, the amount of bytes transferred is cut in half relative to the transfers that would be performed without the data directive.

In addition to the data directive, #pragma acc enter data and #pragma acc exit data can also be used to mark arrays for transfer to and from the accelerator at arbitrary points in execution. When an enter data directive is encountered by the compiler, it indicates what should be copied to the device. That data will remain allocated on the device until an exit data directive is encountered that transfers back, or program terminates. The enter data and exit data directives are most useful when the the async and wait clauses, which both support. Note that the data directive does not support async and wait clauses.

When an async clause is used to enter data or exit data it creates an asynchronous transfer of data to or from the accelerator, analogous to a cudaMemAsync. Just as asynchronous copies are useful in CUDA as well to overlap computation and communication, they can be useful in OpenACC as well. When a wait clause is applied to an enter data or exit data directive, it has the same effect as on kernels or parallel directives: The execution of the data directive waits for other asynchronous tasks to finish. Not that communication directives (that is, enter exit data) can use async and wait to interact with asynchronous computational tasks (that is, kernels and parallel) and vice versa. Consider the code snippet:

```
int *A = init_data(N);
int *B = init_more_data(N);

do_some_heavy_work(C);

#pragma acc data copyin(B[0:N]) copyout(A[0:N])
{
    for (int i = 0; i < N; i++) {
        A[i] = do_work(B[i]);
    }
}
do_lots_more_work(D);
```

Here, the data directive is used to transfer B to the device, and A back. However, the data directive uses synchronous transfers this application will have to block and wait for massive arrays to be transferred. If the enter data and exit data directives are used instead of the async, then communication overhead can be hidden by the computation in do_some_heavy_work and do_lots_more_work:

```
int *A = init_data(N);
int *B = init_more_data(N);
```

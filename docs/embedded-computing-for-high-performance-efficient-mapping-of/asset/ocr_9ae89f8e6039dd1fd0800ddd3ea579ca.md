shows that the computation exhibits considerable data reuse, it may not entirely fit the cache. The following code uses loop tiling to partition the iteration space into smaller blocks of size bIk:

```
for (int i0 = 0; i0 < nX; i0 += bIk)
  for (int j0 = 0; j0 < nZ; j0 += bIk)
    for (int k0 = 0; k0 < nY; k0 += bIk)
      for (int i1 = i0; i1 < min(i0 + bIk, nX); i1 += 4)
        for (int j1 = j0; j1 < min(j0 + bIk, nZ); j1 += 4)
          for (int k1 = k0; k1 < min(k0 + bIk, nY); k1 += 4)
            C[i1*nZ+j1] += A[i1*nY+k1] * B[k1*nZ+j1];
```

Although this code executes using the same operations as the unblocked version, the sequence of independent operations is performed differently. In this case, each iteration (i0, j0, k0) performs 3 x bIk^2 memory accesses. We can now choose a bIk value small enough such that 3 x bIk^2 data fit in the target machine cache. Note that optimized libraries are likely to further partition the loop iteration space into more levels to make a more effective use of the cache hierarchy.

# 6.8 LARA STRATEGIES

In this section, we consider three problems based on topics covered in this chapter: controlling code optimizations (Section 6.8.1), leveraging a multicore CPU architecture with OpenMP (Section 6.8.2), and monitoring the execution of MPI applications (Section 6.8.3). We use LARA aspects to capture the strategies that address these problems, allowing them to be applied automatically and systematically to different application codes with the appropriate weaver infrastructure.

# 6.8.1 CAPTURING HEURISTICS TO CONTROL CODE TRANSFORMATIONS

As discussed in Section 6.3.2, compilers have their own internal heuristics for applying a specific set of optimizations. With LARA, developers can describe their own strategies without changing the compiler's internal logic or manually applying them.

In the following aspect definition, we present a simple LARA example that inlines all calls of a function when specific criteria is satisfied. The target function name is specified through the aspect input parameter. In this example, we only wish to inline invoked functions if the target function (the caller) does not contain loops. It is easy to modify this strategy to include other criteria, such as based on function properties and/or to consider all the functions in the input program instead of only targeting a specific function passed as argument to the aspect.
```
for (i=1; j < N; j++){
    for (i=1; i < N; i++){
        C[i] = C[i] + A[i][j];
    }
}
```

```
for ((j=1); j < N; j += tile_size){
    for ((i=1; i < N; i += tile_size){
        for (j=j; j < j+tile_size; j++){
            for (i=i; i < i+tile_size; i++){
                C[i] = C[i] + A[i][j];
            }
        }
    }
}
```

![](bbox=[0.22, 0.25, 0.85, 0.48])

Depending on the data layout of the manipulated arrays, the tiled version of the code in Fig. 4.5B can exhibit a substantial performance advantage over the original version. While in the original loop nest the accesses to the array a have a substantial stride (assuming a row-major organization as in C), in the transformed code these accesses are more localized resulting in better cache reuse.

An even better loop organization would result from using loop interchange on two control loops of the tiled loop nest as depicted in Fig. 4.6. Here, the order in which the tiles are traversed enhance the locality of both the accesses to the c and a arrays.

These examples illustrate the use of precise data dependence analysis in the presence of loop nests that manipulate multidimensional arrays using affine index functions. The formalization of loop transformations as a linear algebra framework allows the compiler to reason about the legality of the transformations and the opportunities to exploit concurrency and data locality.

While in the context of scientific and high-performance computing the use of data dependence analysis frameworks such as the one outlined here has been very
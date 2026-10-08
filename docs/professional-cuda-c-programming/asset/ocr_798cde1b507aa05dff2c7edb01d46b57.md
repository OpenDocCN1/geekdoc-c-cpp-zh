The code above implements addition, any commutative and associative operation could replace addition. For example, the maximum value in the input vector could be calculated by replacing the sum with a max. Other example valid operations are minimum, average, and product.

This general problem of performing a commutative and associative operation across a vector is known as the reduction problem. Parallel reduction is the parallel execution of this operation. Parallel reduction is one of the most common parallel patterns, and a key operation in many parallel algorithms.

In this section, you will implement several different parallel reduction kernels, and examine how the different implementations affect kernel performance.

# Divergence in Parallel Reduction

As a starting point, you will experiment with a kernel implementing the neighboring pair approach illustrated in Figure 3-21. Each thread adds two adjacent elements to produce a partial sum.

![](bbox=[0.095, 0.385, 0.605, 0.702])

FIGURE 3-21

In this kernel, there are two global memory arrays: one large array for storing the entire array to reduce, and one smaller array for holding the partial sums of each thread block. Each thread block operates independently on a portion of the array. One iteration of a loop performs a single reduction step. The reduction is done in-place, which means that the values in global memory are replaced by partial sums at each step. The __syncthreads statement ensures that all partial sums for every thread in the current iteration have saved to global memory before any threads in the thread block enter the next iteration. All threads that enter the next iteration consumes the values
# ## 7.1 Chapter Objectives

Through the course of this chapter, you will accomplish the following:

+   - You will learn about the performance characteristics of texture memory.
+   - You will learn how to use one-dimensional texture memory with CUDA C.
+   - You will learn how to use two-dimensional texture memory with CUDA C.

# ## 7.2 Texture Memory Overview

If you read the introduction to this chapter, the secret is already out: There is yet another type of read-only memory that is available for use in your programs written in CUDA C. Readers familiar with the workings of graphics hardware will not be surprised, but the GPU's sophisticated texture memory may also be used for general-purpose computing. Although NVIDIA designed the texture units for the classical OpenGL and DirectX rendering pipelines, texture memory has some properties that make it extremely useful for computing.

Like constant memory, texture memory is cached on chip, so in some situations it will provide higher effective bandwidth by reducing memory requests to off-chip DRAM. Specifically, texture caches are designed for graphics applications where memory access patterns exhibit a great deal of spatial locality. In a computing application, this roughly implies that a thread is likely to read from an address "near" the address that nearby threads read, as shown in Figure 7.1.

![](bbox=[0.176, 0.673, 0.723, 0.843])

Figure 7.1 A mapping of threads into a two-dimensional region of memory
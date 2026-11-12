# STRATEGY 5: ALGORITHMS

Selecting an efficient algorithm on the GPU can be challenging. The best algorithm in the CPU domain is not necessarily the best for the GPU. The GPU has its own unique challenges. To get the best performance you need to understand the hardware. Thus, when considering algorithms, we need to think about:

+   - How to decompose the problem into blocks or tiles and then how to decompose those blocks into threads.
+   - How the threads will access the data and what sort of memory pattern this will generate.
+   - What data reuse opportunities are present and how these can be realized.
+   - How much work the algorithm will be performing in total and whether there is a significantly difference from a serial implementation.

There is an 800-plus-page book published by Morgan Kaufman entitled GPU Computing Gems that covers in detail implementation of various algorithms for the following areas:

+   - Scientific simulation
+   - Life sciences
+   - Statistical modeling
+   - Data-intensive applications
+   - Electronic design and automation
+   - Ray tracing and rendering
+   - Computer vision
+   - Video and image processing
+   - Medical imaging

The purpose of this section is not to look at algorithms that are specific to certain fields, as they are of limited general interest. Here we look at a few common algorithms that can be implemented, which in turn may form building blocks for more complex algorithms. This book is not about providing sets of examples you can copy and paste, but providing examples where you can learn the concepts of what makes good CUDA programs.

# Sorting

There are many, many sorting algorithms available, some of which can easily and efficiently be implemented on the GPU and many of which are not well suited. We've looked already in previous chapters at merge sort, radix sort, and the more exotic sample sort. We'll look here at one more parallel sort that is useful in terms of looking at how algorithms are implemented in GPUs.

# Odd/even sort

An odd/even sort works by selecting every even array index and comparing it with the higher adjacent odd array index (Figure 9.34). If the number at the even element is larger than the element at the odd index, the elements are swapped. The process is then repeated, starting with the odd indexes and
# Listing 11.15 GOOD f90 (min stride), BAD Python/C (max stride).

```
for j = 1, N; {
for i = 1, N; {
c(i,j) = 0.0
}
for k = 1, N; {
for i = 1, N; {c(i,j) = c(i,j) + a(i,k)*b(k,j) }}
}
```



In Section 10.16, we discussed how the trend toward exascale computing appears to be one using multinode-multicore-GPU computers, as illustrated in Figure 10.14. The GPU component in this figure extends a supercomputer’s architecture beyond that of computers such as IBM Blue Gene. The GPUs in these future supercomputers are electronic devices designed to accelerate the creation of visual images. A GPU's efficiency arises from its ability to create many different parts of an image in parallel, an important ability because there are millions of pixels to display simultaneously. Indeed, these units can process 100s of millions of polygons in a second. Because GPUs are designed to assist the video processing on commodity devices such as personal computers, game machines, and mobile phones, they have become inexpensive, high performance, parallel computers in their own right. Yet because GPUs are designed to assist in video processing, their architecture and their programming are different from that of the general purpose CPUs usually used for scientific applications, and it takes some work to use them for scientific computing.

Programming of GPUs requires specialized tools specific to the GPU architecture being used, and while we do discuss them in Section 11.6.2, their low-level details places the normal level of this book. What is often called “compute unified device architecture (CUDA) programming” refers to programming for the architecture developed by the Nvidia corporation, and is probably the most popular approach to GPU programming at present (Zeller, 2008). However, some of the complications are being reduced via extensions and wrappers developed for popular programming languages such as C, Fortran, Python, Java, and Perl. However, the general principles involved are just an extension of those used already discussed, and after we have you work through some examples of those general principles, in Section 11.6 we give some practical tips for programming multinode-multicore-GPU computers.

In this section, we discuss some practical tips for multicore, GPU Programming. In the next section, we provide some actual examples of GPU programming using Nvidia's CUDA language, with access to it from within Python programs via the use of PyCUDA (Klöckner, 2014). But do not think this is nothing more than adding in another package to Python. That section is marked as optional because using CUDA goes beyond the usual level of this text, and because, in our experience...
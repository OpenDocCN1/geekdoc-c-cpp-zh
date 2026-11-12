
Along with the introduction of CUDA came the Tesla series of cards. These cards are not graphics cards, and in fact they have no DVI or VGA connectors on them. They are dedicated compute cards aimed at scientific computing. Here we see huge speedups in scientific calculations. These cards can either be installed in a regular desktop PC or in dedicated server racks. NVIDIA provides such a system at http://www.nvidia.com/object/preconfigured_clusters.html, which claims to provide up to 30 times the power of a conventional cluster. CUDA and GPUs are reshaping the world of high-performance computing.

## GPU HARDWARE

The NVIDIA G80 series processor and beyond implemented a design that is similar to both the Connection Machine and IBM's Cell processor. Each graphics card consists of a number of SMs. To each SM is attached eight or more SPs (Stream Processors). The original 9800 GTX card has eight SMs, giving a total of 128 SPs. However, unlike the Roadrunner, each GPU board can be purchased for a few hundred USD and it doesn't take 2.35 MW to power it. Power considerations are not to be overlooked, as we'll discuss later when we talk about building GPU servers.

The GPU cards can broadly be considered as accelerator or coprocessor cards. A GPU card, currently, must operate in conjunction with a CPU-based host. In this regard it follows very much the approach of the Cell processor with the regular serial core and N SIMD SPE cores. Each GPU device contains a set of SMs, each of which contain a set of SPs or CUDA cores. The SPs execute work as parallel sets of up to 32 units. They eliminate a lot of the complex circuitry needed on CPUs to achieve high-speed serial execution through instruction-level parallelism. They replace this with a programmer-specified explicit parallelism model, allowing more compute capacity to be squeezed onto the same area of silicon.

The overall throughput of GPUs is largely determined by the number of SPs present, the bandwidth to the global memory, and how well the programmer makes use of the parallel architecture he or she is working with. See Table 1.3 for a listing of current NVIDIA GPU cards.

Which board is correct for a given application is a balance between memory and GPU processing power needed for a given application. Note the 9800 GX2, 295, 590, 690, and K10 cards are actually dual cards, so to make full use of these they need to be programmed as two devices not one. The one caveat GPU here is that the figures quoted are for single-precision (32-bit) floating-point performance, not double-precision (64-bit) precision. Also be careful with the GF100 (Fermi) series, as the Tesla variant has double the number of double-precision units found in the standard desktop units, so achieves significantly better double-precision throughput. The Kepler K20, yet to be released, will also have significant double precision performance over and above its already released K10 cousin.

Note also, although not shown here, as the generations have evolved, the power consumption, clock for clock, per SM has come down. However, the overall power consumption has increased considerably and this is one of the key considerations in any multi-GPU-based solution. Typically, we see dual-GPU-based cards (9800 GX2, 295, 590, 690) having marginally lower power consumption figures than the equivalent two single cards due to the use of shared circuitry and/or reduced clock frequencies.

NVIDIA provides various racks (the M series computing modules) containing two to four Tesla cards connected on a shared PCI-E bus for high-density computing. It's quite possible to build your own GPU cluster or microsupercomputer from standard PC parts, and we show you how to do this later in the book.

| GPU Series | Device | Number of SPs | Max Memory | GFlops (FMAD) | Bandwidth (GB/s) | Power (Watts) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 9800 GT | G92 | 96 | 2GB | 504 | 57 | 125 |
| 9800 GTX | G92 | 128 | 2GB | 648 | 70 | 140 |
| 9800 GX2 | G92 | 256 | 1GB | 1152 | 2 x 64 | 197 |
| 260 | G200 | 216 | 2GB | 804 | 110 | 182 |
| 285 | G200 | 240 | 2GB | 1062 | 159 | 204 |
| 295 | G200 | 480 | 1.8GB | 1788 | 2 x 110 | 289 |
| 470 | GF100 | 448 | 1.2GB | 1088 | 134 | 215 |
| 480 | GF100 | 448 | 1.5GB | 1344 | 177 | 250 |
| 580 | GF110 | 512 | 1.5GB | 1581 | 152 | 244 |
| 590 | GF110 | 1024 | 3GB | 2488 | 2 x 164 | 365 |
| 680 | GK104 | 1536 | 2GB | 3090 | 192 | 195 |
| 690 | GK104 | 3072 | 4GB | 5620 | 2 x 192 | 300 |
| Tesla C870 | G80 | 128 | 1.5GB | 518 | 77 | 171 |
| C1060 | G200 | 240 | 4GB | 933 | 102 | 188 |
| Tesla C2070 | GF100 | 448 | 6GB | 1288 | 144 | 247 |
| Tesla K10 | GK104 | 3072 | 8GB | 5184 | 2 x 160 | 250 |

The great thing about CUDA is that, despite all the variability in hardware, programs written for the original CUDA devices can run on today's CUDA devices. The CUDA compilation model applies the same principle as used in Java—runtime compilation of a virtual instruction set. This allows modern GPUs to execute code from even the oldest generation GPUs. In many cases they benefit significantly from the original programmer reworking the program for the features of the newer GPUs. In fact, there is considerable scope for tuning for the various hardware revisions, which we'll cover toward the end of the book.

## ALTERNATIVES TO CUDA

### OpenCL

So what of the other GPU manufacturers, ATI (now AMD) being the prime example? AMD's product range is as impressive as the NVIDIA range in terms of raw computer power. However, AMD brought its stream computing technology to the marketplace a long time after NVIDIA brought out CUDA. As a consequence, NVIDIA has far more applications available for CUDA than AMD/ATI does for its competing stream technology.

OpenCL and DirectCompute is not something we'll cover in this book, but they deserve a mention in terms of alternatives to CUDA. CUDA is currently only officially executable on NVIDIA hardware. While NVIDIA has a sizeable chunk of the GPU market, its competitors also hold a sizeable chunk. As developers, we want to develop products for as large a market as possible, especially if we're talking about the consumer market. As such, people should be aware there are alternatives to CUDA, which support both NVIDIA's and others' hardware.

OpenCL is an open and royalty-free standard supported by NVIDIA, AMD, and others. The OpenCL trademark is owned by Apple. It sets out an open standard that allows the use of compute devices. A compute device can be a GPU, CPU, or other specialist device for which an OpenCL driver exists. As of 2012, OpenCL supports all major brands of GPU devices, including CPUs with at least SSE3 support.

Anyone who is familiar with CUDA can pick up OpenCL relatively easily, as the fundamental concepts are quite similar. However, OpenCL is somewhat more complex to use than CUDA, in that much of the work the CUDA runtime API does for the programmer needs to be explicitly performed in OpenCL. You can read more about OpenCL at http://www.khronos.org/opencl/. There are also now a number of books written on OpenCL. I'd personally recommend learning CUDA prior to OpenCL as CUDA is somewhat of a higher-level language extension than OpenCL.

### DirectCompute

DirectCompute is Microsoft's alternative to CUDA and OpenCL. It is a proprietary product linked to the Windows operating system, and in particular, the DirectX 11 API. The DirectX API was a huge leap forward for any of those who remember programming video cards before it. It meant the developers had to learn only one library API to program all graphics cards, rather than write or license drivers for each major video card manufacturer.

DirectX 11 is the latest standard and supported under Windows 7. With Microsoft's name behind the standard, you might expect to see some quite rapid adoption among the developer community. This is especially the case with developers already familiar with DirectX APIs. If you are familiar with CUDA and DirectCompute, then it is quite an easy task to port a CUDA application over to DirectCompute. According to Microsoft, this is something you can typically do in an afternoon's work if you are familiar with both systems. However, being Windows centric, we'll exclude DirectCompute from many high-end systems where the various flavors of UNIX dominate.

Microsoft are also set to launch C++ AMP, an additional set of standard template libraries (STLs), which may appeal more to programmers already familiar with C++-style STLs.

### CPU alternatives

The main parallel processing languages extensions are MPI, OpenMP, and pthreads if you are developing for Linux. For Windows there is the Windows threading model and OpenMP. MPI and pthreads are supported as various ports from the Unix world.

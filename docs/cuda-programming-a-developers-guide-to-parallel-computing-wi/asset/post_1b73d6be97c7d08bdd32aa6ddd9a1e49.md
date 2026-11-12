
Often an application will be tailored to a particular architecture. Thus, you might have a code section such as the following:

```
if ( (major == 2) && (minor == 0) ) // Compute 2.0
    num_blocks = (96*4);
else if ( (major == 2) && (minor == 1) ) // Compute 2.1
    num_blocks = (96*2);
else
    num_blocks = 64; // Assume compute 1.x
```

Now what happens if a compute 2.2 or compute 3.0 architecture is released? In the sample program we'll drop through to the compute 1.x path (the G80/G92/G200 series). The users of your program don't want to replace their Fermi-class GPU with a new Kepler card and find your program runs slower or not at all on their brand-new graphics card. When writing such code, assume you may also come across an unknown computer level and cater for it accordingly.

With the move from G200 to Fermi there was a transition period, where authors had to reissue programs because the number of blocks executed per SM remained the same between generations, only the number of threads per block increased. If a kernel was already using the maximum number of blocks per SM, which allowed for the best instruction mix and thus good performance, no additional blocks got scheduled onto the SMs. Thus, the new hardware went unused and the existing software did not run any faster on the new hardware.

The major transition between G200 and Fermi was the need to increase the number of threads per block. The maximum number of threads per block, a property that can be queried, went from a maximum 512 to 1024. At the same time the number of resident warps has increased from 24 (compute 1.0/1.1) to 32 (compute 1.2/1.3) to 48 (compute 2.0/2.1). Thus, it's likely in the future we'll continue to see such a trend, with blocks containing larger and larger thread numbers. Kepler was the first GPU architecture to also increase the block count per SM, doubling it from 8 to 16 blocks. Thus, the optimal number of threads, to schedule the maximum number of blocks, shifts back to 2048 threads + 16 blocks = 128 threads per block.

We can work out the number of warps available from simply querying the number of threads and the warp size. The cudaDeviceProp structure returns warpSize and maxThreadsPerBlock. Thus, we can call cudaGetDeviceProperties(&deviceProps) API and then divide the number of threads per block by the number of warps to work out the maximum number of warps on a given GPU.

This approach would work well for Kepler GK104 and also the upcoming Kepler GK110. However, it does not take account of the changes in the programming model that the GK110 will bring. The dynamic parallelism aspect of the GK110, now that it's public, can clearly be planned for. NVIDIA showed some work at GTC (GPU Technology Conference), where it claimed this feature alone, primarily the elimination of the CPU control overhead, would lead to quite significant speedups on many codes. It also leads to greatly simpler forms of recursion, where the recursive part can increase the amount of parallelism as the number of nodes expands and contracts depending on the data that is encountered.

One important aspect that you can implement into programs today to run on Kepler hardware is the use of the dedicated 48 K read-only texture cache without the need to do texture memory programming. This will require only that you declare read-only pointers with the C99 standard __restrict__ keyword, so for example:

```
void my_func(float * __restrict__ out_ptr, const float * __restrict__ in_ptr)
```

In this example by adding this keyword we're saying that any writes to the parameter out_ptr will have no effect on the memory region pointed to by in_ptr. In effect, we're saying that the two pointers do not alias memory to another. This will cause the reads via in_ptr to be cached in the texture cache, giving an additional 48 K of read-only cache memory. Potentially this could significantly reduce off-chip access to global memory and thus significantly improve memory throughput.

The Hyper-Q logic is also something you should think about in terms of what elements of existing kernels can be performed in parallel. For the first time task-level parallelism will be truly possible on the GPU. To prepare for this, if you currently run a series of kernels, split these into independent streams, one stream for every independent task. This will not adversely affect code performance when running on your current platform, but will prepare those kernels to execute better on Kepler once this feature becomes available.

Finally, the new K10 Tesla product is a dual GPU, based on the currently available GTX690 consumer card. As with CPUs, if you're using only a single core you're wasting 50% plus of the available compute capability. Thus, anyone planning to install the K10 product will need to move their existing code to support multiple GPUs. We covered this in Chapter 8. You'll need to think about where the data resides and if any communication between the GPUs will be necessary. Moving to a multi-GPU solution today will make the transition much easier and provide almost linear scaling for many applications.

## FURTHER RESOURCES

### Introduction

There are many CUDA resources available on the Internet and through a large number of universities worldwide. We run sessions for professionals wishing to learn CUDA on an individual or group basis. As such, I try to attend, in person or online, as many courses about CUDA as possible each year. As CUDA is a great passion of mine, I've read every book published to date on this subject. I'd, therefore, like to provide some information here about the various CUDA resources for anyone wishing to learn more about CUDA. This information is also available from our website www.learncuda.com, a portal for the various CUDA resources available worldwide.

### Online courses

One of the great successes of CUDA is the commitment from NVIDIA to bring CUDA to a wider audience. If we look back in time, there have been many attempts to bring parallel programming to the mainstream and many languages designed to enable the use of parallel constructs. With the exception of perhaps OpenMP, and to a lesser extent MPI, all have failed. This is largely because they never escaped the niche group they were created for, did not have a major backer willing to invest in training, and were often restricted to a small number of machines owned by universities, governments, or corporations.

Thus, we start with one of the best resources for CUDA, NVIDIA's own page on training: http://developer.nvidia.com/cuda-training. Here you can access a number of recorded lectures from various universities, including:

- ECE-498AL, http://courses.engr.illinois.edu/ece498al/ — a course taught by Professor Wen-mei W. Hwu, author of the first major textbook on CUDA. Available from the 2010 course are lecture audio recording and slides.
- Stanford CS193G, http://code.google.com/p/stanford-cs193g-sp2010/ — a course run by Stanford University based on the ECE-498 course. Includes recorded lecture videos available via iTunes. Taught by Jared Hoberock and David Tarjan.
- Wisconsin ME964, http://bsl.wisc.edu/Courses/ME964/ — a course on high-performance computing applications in engineering, with links to lecture videos and a number of interesting guest lectures. Taught by Dan Negrut.
- EE171 Parallel Computer Architecture, http://www.instruction.com/object/cudaad_ucadavis — an excellent course covering data-level parallelism, instruction-level parallelism, and thread-level parallelism from the architecture perspective. Taught by John Owens, University of California—Davis.

The next major source of online information is the recorded GPU conference archives. Usually every year NVIDIA holds a conference in San Jose, California, where they are based, called the GPU Technology Conference. These are actually held worldwide in various locations. About a month after the conference, the various sessions are uploaded to NVIDIA's GPU technology portal at http://www.gputechconf.com/gtcnew/on-demand-gtc.php. There are far too many sessions to attend since, like many conferences, sessions overlap with one another. You can view almost all of the sessions online going back a number of years. Also available are other conferences where NVIDIA has recorded sessions.

The keynotes, especially those by Jen-Hsun Huang, are always very interesting to listen to and give a great insight into the future of GPU technology. The keynote on the DARPA challenge by Sebastian Thrun shows just how wide the range of CUDA applications is, for example, with GPUs being used to autonomously control a car. Various talks by Paulius Micikevicius are available focusing on CUDA optimization, as well as one talk by Vasily Volkov on occupancy, which is also interesting to watch.

The next major source of online information is the archived webinars provided by NVIDIA that can be found at http://developer.nvidia.com/gpu-computing-webinars. The webinar series is aimed at registered CUDA developers. Registration is free and allows you access to the webinars live. Live attendance allows you to ask questions and provide feedback on a particular subject of interest. Sometime after the webinar is over, the archived versions usually become available. The webinar series tends to focus on new innovations in CUDA, the API, and may also have sessions on vendor-specific tools.

There are also many other resources available on CUDA and parallel computing. Visit www.learncuda.com for a complete list.

### Taught courses

Many universities teach CUDA as part of parallel programming courses. Often it is taught alongside OpenMP and MPI, which are the dominant intercore and intranode programming models used today. NVIDIA provides a very useful tool to identify where CUDA is being taught around the world, so you

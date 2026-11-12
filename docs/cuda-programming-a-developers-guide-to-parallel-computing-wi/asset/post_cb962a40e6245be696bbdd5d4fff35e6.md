
```cpp
#pragma omp parallel num_threads(4)
```

Assuming you have a quad-core CPU and four GPU cards attached, then you would specify to OpenACC that you wish the current thread to use a given GPU.

```cpp
#pragma omp parallel num_threads(4)
{
    const int cpu_thread_id = omp_get_thread_num();
    acc_set_device_num( cpu_thread_id, acc_device_nvidia );
}
```

If you have only two GPUs in the system then you might be better off specifying two threads for OpenMP. If you wished to make use of four threads, but only have two for GPU usage, you could do the following:

```cpp
const int num_gpus = acc_get_num_devices( acc_device_nvidia );
#pragma omp parallel num_threads(4)
{
    const int cpu_thread_id = omp_get_thread_num();
    if ( cpu_thread_id < num_gpus )
    {
        // Do CPU and GPU work
        acc_set_device_num( cpu_thread_id, acc_device_nvidia );
    }
    else
    {
        // Do CPU only work
    }
}
```

We can do the same in MPI by using

```cpp
const int num_gpus = acc_get_num_devices( acc_device_nvidia );
// Get my MPI virtual process id (rank)
int my_rank;
MPI_Comm_rank( MPI_COMM_WORLD, &my_rank );
if ( my_rank < num_gpus )
{
    // Do CPU and GPU work e.g. workers
    acc_set_device_num( my_rank, acc_device_nvidia );
}
else
{
    // Do CPU only work, e.g. master
}
```

One issue to be careful of here is that the acc_set_device_num API call is a one-time event only per host thread. This is very much the way the cudaSetDevice call used to work prior to the CUDA 4.x SDK. You cannot select a context from a single host thread and thus control multiple GPUs from that single thread. The only model supported is one where there is a single host thread per GPU context.

Note that a dedicated 1:1 ratio of CPU cores to GPUs is the ideal for heavily used systems. However, oversubscribing GPUs to CPU cores can be useful, as rarely will GPU programs actually saturate the GPU. Thus, there may be points where the GPUs are underutilized, typically at synchronization points and between kernel invocations. In cases where you have a master/worker arrangement, which is typical in MPI, it can be beneficial to dedicate a non-GPU, CPU core to be the master.

One aspect I should touch on here is memory patterns. OpenACC, when implemented on an accelerator that does coalescing of global memory, will be just as badly affected by a poor memory layout as a CUDA program will. There is no automatic transpose. You need to think about your memory layout and create one that is optimal for a GPU (data in columns of 32 elements, rather than sequential rows).

Overall OpenACC represents a very interesting development in GPU programming and potentially opens up the GPU programming arena to many non-GPU programmers. Many of these people will progress to use CUDA, as it's perfectly possible to mix OpenACC and CUDA. Thus, you can start with OpenACC, and if you find specific areas where you need that extra control, switch over to CUDA, while leaving most of the application untouched.

## WRITING YOUR OWN KERNELS

We've presented a number of other options in this chapter that range from specifying the parallelism at a high level and having the compiler do the heavy lifting, to using libraries developed by those far better at exploiting the hardware than you are. You will never, and in fact probably should not try to, be the best at everything. Tools such as compiler directives and libraries allow you to leverage the effort of others to achieve your goals. Your knowledge resides primarily within your own field of interest.

As a professional developer, or even as a student, you should be conscious of the time you take to develop a solution. It may be technically challenging to develop the most efficient parallel quick sort, but probably some bright computer science graduate has already written a paper on it. If you are hiring, then the obvious thing to do is bring this person on board. Writing in kernels, in terms of people or software, is something that can give you a huge head start on whoever your competition may be.

It also makes a lot of sense to select libraries where they cover something that is not your area of expertise. If you are developing an image blur algorithm, for example, loading/saving the images from the disk is not really what you are interested in. There are a number of open-source, or commercial, libraries that may cover this aspect of your development.

One common problem you may encounter using libraries is memory allocation. Most CPU-based solutions, if they allocate memory, do not allocate pinned memory. Thus, an image library that returns a pointer to the loaded image will cause a slowdown in your application when you transfer that image data to the GPU. Therefore, look for libraries that allow the user to control the memory management, or are GPU aware and support pinned memory.

The next issue we hit with the directive and library approach is they are, generally, not multi-GPU aware unless written as such. As you can usually get up to four GPU cards into a workstation, this approach is a bit like using only one of the cores in a standard quad-core CPU. The programming required to support multi-GPU configurations is not trivial, but neither is it rocket science. The libraries we use internally at CudaDeveloper support multiple GPU setups. It complicates the handling of the data and requires a lot more thought, but is certainly doable.

The issue of how much you need to write yourself often is a question of performance. In using directives you trade a certain percentage of performance for quicker program development. Libraries, by comparison, may bring a significant speedup along with a reduction in development effort, but at the potential cost of flexibility and license issues. Many are restricted in terms of commercial usage, which simply reflects that if you intend to avoid your own development costs by using libraries, you should be prepared to pay for that privilege. For academic usage, simply acknowledging the contribution is usually sufficient.

Thus, there are a number of reasons why you might choose to develop your own kernels in CUDA. This text provides good insight to the issues of developing kernels using CUDA. The basic principles (coalesced memory access, fully utilizing the hardware, avoiding contention of resources, understanding the hardware limitations, data locality) apply regardless of whether you write the kernels yourself or abstract them to someone else’s problem.

We’ve covered in this section some of the NVIDIA-provided libraries. If you are working in a field that these cover, why would you not choose to use such libraries? They are developed by the manufacturer to run well on their hardware. They are designed to be used as the basic building blocks of more complex algorithms. NVIDIA’s licensing terms are very generous in that they want people to use the libraries and to build CUDA applications. This is hardly surprising when you consider wider acceptance of CUDA means more GPUs get sold, and of course the more valuable your knowledge of CUDA becomes.

The question is really does this bring you sufficient level of performance? Most people program in a high-level language because it’s much more productive than something like Assembler. The better programmers out there understand both C and Assembler in great detail. They know when they should use C for the productivity gains and know when a small number of functions need to be hand-coded in Assembler. The question of using libraries/directives is largely a similar one. You could write everything yourself, unless you have to, why make your life so hard?

When developing applications for GPUs, a good approach is to first get a prototype working on the CPU side. Consider how you’d like to make a CPU version multicore aware and if it would benefit the application. What will be the CPU/GPU work balance? How will you create threads on the CPU side if you need them? However, at least initially, stick with a single CPU thread and a single GPU, but think at the start about what you want to achieve in the end.

Now think about the host/device transfers. The transfer-compute-transfer model will usually (depending on the ratios) underutilize the GPU. To some extent we can overlap transfer/compute depending on the hardware you have to support.

Next think about the memory hierarchy within the GPU. What locality (registers, shared, cache, constant, texture) are you going to exploit on the GPU? What data layout do you need for these various types of data stores?

Now think about the kernel design. The decomposition into threads and blocks has implications in terms of the amount of interthread/interblock communication and resource usage. What serialization or contention issues are you likely to have?

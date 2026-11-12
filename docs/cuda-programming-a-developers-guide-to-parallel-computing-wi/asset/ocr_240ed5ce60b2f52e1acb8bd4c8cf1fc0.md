![](bbox=[0.13, 0.115, 0.83, 0.435])

opened up the possibility to program GPUs without having to learn complex shader languages, or to think only in terms of graphics primitives.

CUDA is an extension to the C language that allows GPU code to be written in regular C. The code is either targeted for the host processor (the CPU) or targeted at the device processor (the GPU). The host processor spawns multithread tasks (or kernels as they are known in CUDA) onto the GPU device. The GPU has its own internal scheduler that will then allocate the kernels to whatever GPU hardware is present. We’ll cover scheduling in detail later. Provided there is enough parallelism in the task, as the number of SMs in the GPU grows, so should the speed of the program.

However, herein hides a big problem. You have to ask what percentage of the code can be run in parallel. The maximum speedup possible is limited by the amount of serial code. If you have an infinite amount of processing power and could do the parallel tasks in zero time, you would still be left with the time from the serial code part. Therefore, we have to consider at the outset if we can indeed parallelize a significant amount of the workload.

NVIDIA is committed to providing support to CUDA. Considerable information, examples, and tools to help with development are available from its website at http://www.nvidia.com under CudaZone. CUDA, unlike its predecessors, has now actually started to gain momentum and for the first time it looks like there will be a programming language that will emerge as the one of choice for GPU programming. Given that the number of CUDA-enabled GPUs now number in the millions, there is a huge market out there waiting for CUDA-enabled applications.

There are currently many CUDA-enabled applications and the list grows monthly. NVIDIA showcases many of these on its community website at http://www.nvidia.com/object/cuda_apps_flash_new.html.

In areas where programs have to do a lot of computational work—for example, making a DVD from your home movies (video transcoding)—we see most mainstream video packages now supporting CUDA. The average speedup is 5 to 10 times in this domain.
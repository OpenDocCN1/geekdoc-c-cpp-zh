```
printf ( " --- MP Information for device %d ---\n", i ) ;
printf ( "Multiprocessor count: %d\n",
prop.multiProcessorCount ) ;
printf ( "Shared mem per mp: %d\n", prop.sharedMemPerBlock ) ;
printf ( "Registers per mp: %d\n", prop.regsPerBlock ) ;
printf ( "Threads in warp: %d\n", prop.warpSize ) ;
printf ( "Max threads per block: %d\n",
prop.maxThreadsPerBlock ) ;
printf ( "Max thread dimensions: (%d, %d, %d)\n",
prop.maxThreadsDim[0] , prop.maxThreadsDim[1] ,
prop.maxThreadsDim[2] ) ;
printf ( "Max grid dimensions: (%d, %d, %d)\n",
prop.maxGridSize[0] , prop.maxGridSize[1] ,
prop.maxGridSize[2] ) ;
printf ( "\n" ) ;
}
}
```

# 3.4 Using Device Properties

Other than writing an application that handily prints every detail of every CUDA-capable card, why might we be interested in the properties of each device in our system? Since we as software developers want everyone to think our software is fast, we might be interested in choosing the GPU with the most multiprocessors on which to run our code. Or if the kernel needs close interaction with the CPU, we might be interested in running our code on the integrated GPU that shares system memory with the CPU. These are both properties we can query with cudaGetDeviceProperties ().

Suppose that we are writing an application that depends on double-precision floating-point support. After a quick consultation with Appendix A of the NVIDIA CUDA Programming Guide, we know that cards that have compute capability 1.3 or higher support double-precision floating-point math. So to successfully run the double-precision application we've written, we need to find at least one device of compute capability 1.3 or higher.
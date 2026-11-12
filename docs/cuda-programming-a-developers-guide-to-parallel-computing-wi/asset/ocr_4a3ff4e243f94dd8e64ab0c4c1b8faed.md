192, 256, 384, and 512 work well with compute 2.x devices. The 256 value is usually the best for the compute 3.x platform.

However, when considering adding any specifiers here, consider the likely impact of future hardware and how this might limit the use of other accelerator targets. By specifying nothing you are letting the compiler select what it thinks is the best value. When a new GPU comes out with more threads per block and more blocks per SM, once the vendors update the compiler to accommodate it, all will work. If you do specify these parameters, you should be specifying some multiple of the current maximum to allow for your code to run on future devices without running out of blocks.

By default the OpenACC model uses synchronous kernel calls. That is, the host processor will wait for the GPU to complete and then continue execution once the GPU kernel calls returns. This is akin to making a function call in C as opposed to spawning a worker thread and later converging.

You should be aware by now that this approach, although nice to develop the initial application on, should be replaced with an asynchronous model as soon as the application is running well. You probably have a reasonable multicore CPU in the machine and could make good use of it while the GPU is off calculating something. On the top of the list of things to allocate to the CPU should be those operations requiring few compute actions compared to loads and stores to and from memory.

One of the reasons why we see the reduction operation perform better, or at least at the same speed as the GPU, is the amount of work done per memory read/write. To calculate data on the GPU we need to either generate it there or send it over the PCI-E bus. If you are shipping two data items over the bus just to perform a simple operation such as addition, forget it and do it on the CPU instead. The cost the PCI-E transfer greatly outweighs any other consideration in such a scenario. The best candidates for the GPU are those computationally intensive areas, or where the additional memory bandwidth on the GPU can make a difference.

Thus, OpenACC provides the async clause for kernels and data to allow them run asynchronously to the host and perform asynchronous transfers with the host.

```
#pragma acc kernels loop async
for (i=0; i < num_elem; i++)
{
...
}
```

Asynchronous transfers require the use of pinned memory, that is, memory that cannot be swapped to disk. You do not need to explicitly care about this in OpenACC as you do with CUDA. Specifying the async clause will cause the OpenACC compiler to use pinned memory under the hood for transfers. Of course, one thing to remember when using an asynchronous operation is that you cannot change the data that is being transferred or operated on by the kernel until the asynchronous operation has completed.

Once people have mastered asynchronous communication and achieved the best performance they are able to on a single-core/GPU pair, the obvious question is: Can I speed up my application by using multiple GPUs? The answer is of course yes, and very often you’ll see near linear scaling if you can stay within a single node.

The OpenACC standard supports only a “one CPU thread per GPU” view of multiple GPUs on a single node. If you plan on performing some work on the CPU, this makes perfect sense, as it allows you to exploit the full potential of a multicore CPU. Thus, with OpenMP you simply launch a number of threads using the OpenMP directive
```
omp_set_num_threads(num_gpus);
//omp_set_num_threads(2*num_gpus);
#pragma omp parallel
{
}
```

There are two approaches here: to set one thread per GPU or multiple threads per GPU (Figure 10.6). The later approach is more useful where you have many more CPU cores than GPUs. A simpler form of this OpenMP directive that often works more reliably is the one we've used in the sample program:

```
// Spawn one CPU thread for each device
#pragma omp parallel num_threads(num_devices)
{
}
```

With this approach it does not matter how OpenMP may or may not have been configured, what environment variables are set or not, it spawns the specified number of threads. Note that the current thread is one of the threads used to execute work.

```
Identified 4 devices. Spawning 4 threads to calculate 64 MB using (32768x512)
Kernel Time for device GeForce GTX 470 id:0: 427.74ms
CPU count for thread 0: 1239000000
Kernel Time for device GeForce 9800 GT id:1: 3300.55ms
CPU count for thread 1: 1180000000
Kernel Time for device GeForce GTX 285 id:2: 1693.63ms
CPU count for thread 2: 1229000000
Kernel Time for device GeForce GTX 460 id:3: 662.61ms
CPU count for thread 3: 1254000000
```

You can see from the program output that, by using different GPUs, the threads finish at different times. You can see from Figure 10.6 that there are four tops running, including the originating thread. If viewed on screen you would see dark green bars along the top showing the threads are mostly running (~95%) with occasional stalls that would be shown in light green. Below are the four GPU tasks each of which is performing a memsset, a kernel launch, and then a copy back to host. The bottom row of bars shows the CPU utilization for this timeframe. You can see the CPU is busy almost the entire time.

As the four GPUs finish, the CPU threads continue to work until all GPUs in the set have completed. We could of course, and you would in practice, allocate more GPU work to these GPUs if we really had such different performance characteristics with our GPUs. However, most GPU systems will have all of the same GPUs present and thus we'd not have to care about reissuing work until they had all completed. As they are all the same, given a similar job, they would all complete around the same time.

The next issue we should address with using OpenMP is where to put resource allocations and deallocations. Allocation of memory and creation of resources on a given device is a time-consuming process. Often there needs to be a common understanding of the allocation across threads and thus common data structures. To share common data structures across threads requires locking and this in
![](bbox=[0.18, 0.08, 0.85, 0.24])

Figure 7.2 Using multiple process accelerated by GPUs communicating with MPI. (See insert for colour representation of this figure)

The direct diagonalization of the RMM eigenproblem is an example of a computationally inexpensive operation that should be ported to prolong GPU data residency. The expansion set for each band generally has only a few vectors, resulting in very small eigenproblems that have no impact on overall performance. There is one such eigenproblem per band per RMM-DIIS iteration, so copying data from and to the GPU memory space each time would be prohibitively expensive. To prevent these frequent and costly data movements, MAGMA routines should be used, even though they are highly inefficient for such small problem sizes.

# 7.4.2 Parallel Optimization Techniques (Off-Node)

# 7.4.2.1 Multiple Host CPUs and Multiple GPUs

In order to address larger physical systems, one needs to deal with platforms composed of multiple GPUs and multicore CPUs. There are two general parallel setups:

+   1. Each GPU receives kernels from exactly one CPU process
+   2. Each GPU receives kernels from multiple CPU processes

The first setup can be further divided into the case where only one CPU process runs per GPU and the case where many CPU processes run per GPU, but only one is designated for kernel launch. As we will see, recent improvements to the GPU runtime have all but deprecated the latter setup.

There are two advantages to a one-process-per-GPU setup. First, this setup minimizes the number of messages that must be sent between processes, which reduces the overall share of the communication time. These messages can be seen in Figure 7.2. Because GPU-enabled nodes are generally much more arithmetically capable than CPU-only counterparts, GPU implementations are more sensitive to the communication overhead. Using streams to overlap communication and computation can help mitigate this effect. Second, this setup maximizes the potential for blocking and batching by dividing the data as little as possible. GPU can run only a fixed number of kernels concurrently, presently 32. If the problem is decomposed beyond the point at which 32 kernels occupy the device, then further parallelism will reduce occupancy and degrade performance.

There are two advantages to a multiple processes per the GPU setup. The first is that using multiple processes will accelerate the CPU portion of the work. For PW DFT, we have described how to port the majority of the workload, so this is of less of an issue. The second advantage is implicit streaming with the multiprocessor server (MPS). MPS allows kernels from different CPU processes to run concurrently. By default, each CPU process submits kernels to a different stream, so using multiple processes is like streaming over the entire calculation, excepting barriers. This can be a quick and easy way to improve GPU occupancy without writing streams or batches into the code.
pretended in our model application and the mini apps. Achieving high performance may require fundamental changes in the applications.

The main difference between MPI and OpenMP in parallelizing the primary loop over the band is how the data are allocated and initialized. The data locality is enforced in MPI: each task owns its data and there is no conflict in terms of read or write and of cache interference.

In an OpenMP program, many threads are all sharing the same address space and may thus suffer from factors such as false sharing (where two different threads are accessing different parts of the same cache line). NUMAs can also interfere with performance, because data may be allocated in “far” memory. Policies such as first-touch in modern operating systems alleviate this; in particular, it is helpful to initialize data structures in parallel, so that the thread that initializes a piece of data is also the thread that will work on that data. The mini apps, dgemm.cpp and fft3d.cpp, employ this allocation-and-initialization per thread method to maximize the data locality.

Because of these intricate memory policies and because of other overhead (such as starting the OpenMP threads the first time), the experiments ignore the timings for initialization and for the first call to any MKL routine.

Figure 18.6a shows the performance of a batch of 240 DGEMMs on an Intel Xeon Phi coprocessor 7120P for the problem sizes for which using 240 MPI tasks is feasible. These results, which can be also reproduced on any Intel Xeon processors as shown in Figure 18.6b, should assure developers that OpenMP itself does not compromise performance compared to MPI. The performance gain coming from the expanded memory available for the applications is obvious: there is no more need to waste cores by using fewer MPI tasks per node because the memory demand is high. In real simulations, this flexibility of mixing MPI and OpenMP at the same efficiency allows the users to partition a node to meet the memory requirement, to minimize any NUMA impact, and to optimize the on-node and off-node communications.

![](bbox=[0.12, 0.62, 0.88, 0.84])

# FIGURE 18.6

Total GFlop/s of concurrent DGEMMs C=A(N,N)*B(N,N) (a) on Intel® Xeon Phi™ coprocessor 7120P @1.24 GHz and (b) on Intel® Xeon® processor E5-2697 @2.60 GHz, each size N tested with all MPI, all OpenMP, and hybrid of OpenMP/MKL within MPI.
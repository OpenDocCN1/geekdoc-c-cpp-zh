![](bbox=[0.18, 0.11, 0.78, 0.41])

# FIGURE 17.6

Stencil-test run-times as in Figures 17.4 and 17.5, but on the Intel Xeon Phi coprocessor, and using a total of 200 threads in all cases.

all cases. When using the fine-grained OpenMP version, performance improves from 1 thread to 2, but remains insensitive to the MPI/OpenMP “mix” after that. Both of the coarse-grained versions, on the other hand, perform better with more OpenMP and less MPI, and they perform significantly better than the fine-grained OpenMP version. That is really no surprise, at least for the larger thread counts, though it is perhaps more surprising for the single-threaded case. In principle a single thread has no “graininess” at all, neither coarse or fine, but Figure 17.4 suggests that the extra directives invoked in the fine-grained case do incur some overhead, even in the single-threaded case.

Figure 17.5 is similar to Figure 17.4, but for the case where hyper-threading was used, so for all results shown in Figure 17.5 the product of MPI processes and OpenMP threads is 40. Perhaps, the first point to make is that hyper-threading is very effective here: using it reduces run-times by almost a factor of 2. The fastest run-time in Figure 17.4 is 16.6 s (for the partial coarse-grained run with 20 threads), and in Figure 17.5 is 8.6 s (also for the partial coarse-grained run with 20 threads—but of course this time with the benefit of a second MPI process).

Otherwise, the main result of Figure 17.5 is the same as Figure 17.4, namely, that coarse-grained multi-threading performs better than fine-grained—significantly better for most thread counts, but also even for 1 thread, however marginally. For all runs in both Figures 17.4 and 17.5, the performance costs of the extra MPI messages in the full coarse-grained case are negligible—but they may become more noticeable if run over a network between multiple nodes.

Figure 17.6 is similar to Figures 17.4 and 17.5, but shows results from 200 threads of the Intel Xeon Phi coprocessor. Even though 240 threads were available, it was easier to divide the 800 × 800 × 1000 domain in different ways among 200 threads rather than 240. In any case, runs using all 240 threads on
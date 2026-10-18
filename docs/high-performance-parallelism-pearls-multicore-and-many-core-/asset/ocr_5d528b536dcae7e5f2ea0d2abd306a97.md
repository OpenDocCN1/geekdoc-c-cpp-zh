# Halo speedup on eight nodes in symmetric mode

![](bbox=[0.22, 0.17, 0.56, 0.295])

# FIGURE 16.13

Speedup of MPI SHM approach compared to the point-to-point based, measured with eight neighbors and different processes decompositions (1-D and 2-D) measured on 8 nodes with 480 processes in symmetric mode. Each node contains one processor and one coprocessor.

are placed on the same node creating in case of 1-D very compact neighbors assignments while for 2-D decomposition and relatively big number of processes, most of the partners are non-local processes. As we stated in the previous chapter, number of local node partners has direct impact on the overall performance. Figure 16.13 shows speedup obtained on eight Intel Xeon processors and eight Intel Xeon Phi coprocessors in symmetric mode. The program execution is called symmetric when the complete program runs on both the host and the coprocessor as peers (not using explicit offload programming). This mode is only logically symmetric although, the host and coprocessor may have different computational and communication performances. In case of pure MPI applications, developer may choose a different number of processes per node. We ran the test with 480 processes, 28 per processor, and 32 per coprocessor and different process topologies corresponding to Figure 16.8.

These experiments confirm that the overall performance of MPI SHM pattern depends on the number of local neighbors rather than on the total processes count. Therefore, the proposed approach has good scaling potential with the proper partner assignments.

# SUMMARY

An interprocess shared memory extension was added in MPI 3.0. We have described this extension, and how it can be used to perform communication efficiency and memory footprint optimization. We demonstrated how to apply this new feature in a simple 1-D ring “hello world” example and extended it for several node runs. Using a modified MPPTTEST benchmark, we achieved up to 4.9× improvement over a standard point-to-point communication approach on one Intel Xeon Phi coprocessor. Moreover, we showed that the proposed approach may benefit halo exchanges even for multi-node cases, and we obtained up to 1.8× improvement with two Intel Xeon Phi coprocessors. Finally, we showed that the benefits of MPI SHM grow as we increase the number of intranode neighbors for halo exchanges.
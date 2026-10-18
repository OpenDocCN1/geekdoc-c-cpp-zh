
型号为 5110P、SOA 长度为 8 的模型性能为 283.8 GFLOPs，比我们之前测得的数值低 2 到 3 GFLOPS。我们认为这只不过是一个波动，在这个水平上大约处于 1% 的量级。最后我们注意到，与 Intel Xeon Phi 协处理器在 SOA 长度为 8（其向量长度的一半）时表现最佳的方式类似，Xeon 的结果也在 SOA 长度为 4（其向量长度的一半）时达到最佳。

需要声明的是，要在 Intel Xeon Phi 协处理器上获得此级别的性能，必须在启动时启用 icache_snoop_off 功能。如果没有此功能，Xeon Phi 上的性能可能会比我们的数值低。例如，在 Intel Endeavor 集群中的 61 核 Xeon Phi（启用了 icache_snoop_off）上，我们在某个特定基准测试中持续达到了 320 GFLOPS。在 Stampede（类似的 61 核 Xeon Phi 部件）上运行相同规模的问题，由于未启用 icache_snoop_off 功能，性能为 271 GFLOPS。

## 路的尽头？

当然不是！不过，我们已经接近本章的尾声。为了优化 Wilson-Dslash 的单节点性能，我们付出了大量工作，并且收获颇丰。然而，仍有许多途径尚未探索，只因本章篇幅有限。

一个非常重要的方面是将 Wilson-Dslash 扩展到多个节点，无论是 Intel Xeon Phi 协处理器还是 Intel Xeon 处理器。完成此工作的代码已在 QPhiX 中提供，原始代码中也有（尽管该原始代码使用了略有不同的算法）。在当前作为 PCIe 卡的设置中，多节点扩展遇到了一些挑战，值得用单独一章来讲述。有兴趣的读者可参阅本章末尾的“更多信息”部分。

另一个重要考量是，Wilson-Dslash 算子通常是大型复合算子中计算开销最大的部分。通常需要用较大的复合算子来求解线性方程组。最近，求解这些系统的方法取得了进展，不仅包括通常的 Krylov 子空间方法，如共轭梯度法或稳定双共轭梯度法，还包括较新的算法，如广义共轭残差法或 Flexible GMRES，这些算法允许使用区域分解预条件子与紧缩技术，以及代数多重网格方法。特别是，区域分解预条件子具有非常好的性质：小区域可以被阻塞到 Intel Xeon Phi 协处理器的 L2 缓存中，从而将带宽瓶颈从主内存带宽转移到缓存带宽。关于在 Intel Xeon Phi 协处理器上使用区域分解预条件子优化求解器的详细阐述，可参见我们在 Supercomputing 2014 上的论文（见“更多信息”部分）。

当需要求解多个系统时，还可以考虑跨系统进行向量化，这可能比 QPhiX 中所考虑的向量化更简单。这在“HISQ inverter”论文（见“更多信息”部分）中针对 QCD 的不同公式化方式实现过，而 Wilson-Dslash 的相关工作正在进行中，初步结果令人鼓舞。

本章我们想强调的要点是什么呢？或许如下：

- 为了以最高效率利用系统，对性能有一些模型是很有帮助的。它是内存受限还是计算受限？预期性能能否与系统参数关联起来？
- 在我们的案例中，我们对模型进行了多次改进，例如考虑流式存储、缓存重用或压缩。
- 在我们的案例中，必须采用多种优化步骤。仅靠线程化并行并不足以获得最佳性能，还需要向量化、预取、分块以及一些同步操作。
- 要准备好迎接意外。在我们的案例中，意外来自屏障（barrier）带来的改进，以及发现 SOA 长度为向量长度一半时，其性能反而优于 SOA 长度等于向量长度时的表现。
- 特定领域的代码生成器可能很有帮助。它们不一定需要非常复杂，并且可以降低探索某些优化（例如加载、预取等策略）的痛苦。在某些情况下，例如我们这里，它们还有助于在其他架构上获得更好的性能。

## 更多信息

- Babich, R., Brannick, J., Brower, R.C., Clark, M.A., Manteuffel, T.A., et al., 2010. Adaptive multigrid algorithm for the lattice Wilson-Dirac operator. Phys. Rev. Lett. 105, 201602.
- Babich, R., Clark, M.A., Joó, B., Shi, G., Brower, R.C., Gottlieb, S., 2011. Scaling lattice QCD beyond 100 GPUS. In: Proceedings of 2011 International Conference for High Performance Computing, Networking, Storage and Analysis, SC ’11, New York, NY, USA. ACM, pp. 70:1-70:11.
- Boyle, P.A., 2009. The {BAGEL} assembler generation library. Comput. Phys. Commun. 180 (12), 2739-2748. 40 {YEARS} {OF} CPC: a celebratory issue focused on quality software for high performance, grid and novel computing architectures.
- Clark, M.A., Babich, R., Barros, K., Brower, R.C., Rebbi, C., 2010. Solving lattice QCD systems of equations using mixed precision solvers on GPUs. Comput. Phys. Commun. 181, 1517-1528.
- Edwards, R.G., Joó, B., 2005. The Chroma software system for lattice QCD. Nucl. Phys. Proc. Suppl. 140, 832.
- Frommer, A., Kahl, K., Krieg, S., Leder, B., Rottmann, M., 2014. Adaptive aggregation based domain decomposition multigrid for the lattice Wilson-Dirac operator. SIAM J. Sci. Comput. 36, A1581-A1608.
- Frommer, A., Nobile, A., Zingler, P., 2012. Deflation and flexible SAP-preconditioning of GMRES in lattice QCD simulation. ArXiv e-prints, April.
- Heybrock, S., Joó, B., Kalamkar, D.D., Smelyanskiy, M., Vaidyanathan, K., Wettig, T., Dubey, P., 2014. Lattice QCD with domain decomposition on Intel® Xeon Phi™ co-processors. In: Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis, SC ’14, Piscataway, NJ, USA. IEEE Press, pp. 69-80.
- Hestenes, M.R., Stiefel, E., 1952. Methods of conjugate gradients for solving linear systems. J. Res. Natl Bur. Stand. 49 (6), 409-436.
- Jeffers, J., Reinders, J., 2013. Intel® Xeon Phi™ Coprocessor High-Performance Programming, first ed. Morgan-Kauffman, Elsevier, Waltham, MA, USA.
- Jeffers, J., Reinders, J., 2014. High Performance Parallelism Pearls, first ed. Morgan-Kauffman, Elsevier, Waltham, MA, USA.
- Joó, B., Kalamkar, D.D., Vaidyanathan, K., Smelyanskiy, M., Pamnany, K., Lee, V.W., Dubey, P., Watson, W., 2013. Lattice QCD on Intel Xeon Phi coprocessors. In: Kunkel, J.M., Ludwig, T., Meuer, H.W. (Eds.), Supercomputing, volume 7905 of Lecture Notes in Computer Science. Springer, Heidelberg, pp. 40-54.
- O. Kaczmarek, Schmidt, C., Steinbrecher, P., Mukherjee, S., Wagner, M., 2014. HISQ inverter on Intel Xeon Phi and NVIDIA GPUs, CoRR abs/1409.1510, http://arxiv.org/abs/1409.1510.
- Luscher, M., 2007. Local coherence and deflation of the low quark modes in lattice QCD. JHEP 0707, 081.
- McClendon, C., 2001. Optimized Lattice QCD Kernels for a Pentium 4 Cluster. Technical Report JLAB-THY-01-29, Jefferson Lab, September.
- Nguyen, A., Satish, N., Chhugani, J., Kim, C., Dubey, P., 2010. 3.5D blocking optimization for stencil computations on modern CPUs and GPUs. In: Proceedings of the 2010 ACM/IEEE International Conference for High Performance Computing, Networking, Storage and Analysis, SC ’10, Washington, DC, USA. IEEE Computer Society, pp. 1-13.
- Pochinsky, A.V. QA0 Code Generator. http://www.mit.edu/~avp/qa0.
- Jefferson Lab GitHub Projects. CPP Wilson-Dslash. https://github.com/jeffersonlab/cpp_wilson_dslash.git.
- Jefferson Lab GitHub Projects. QPhiX-Codegen Code Generator. https://github.com/jeffersonlab/qphix-codegen.git.
- Jefferson Lab GitHub Projects. QPhiX Library. https://github.com/jeffersonlab/qphix.git.
- Smelyanskiy, M., Vaidyanathan, K., Choi, J., Joo, B., Chhugani, J., Clark, M.A., Dubey, P., 2011. High-performance lattice QCD for multicores based parallel systems using a cache-friendly hybrid threaded-MPI approach. In: 2011 International Conference for High Performance Computing, Networking, Storage and Analysis (SC), November, pp. 1-10.
- van der Vorst, H.A., 1992. Bi-CGSTAB: a fast and smoothly converging variant of bi-CG for the solution of nonsymmetric linear systems. SIAM J. Sci. Stat. Comput. 13 (2), 631-644.
- Vaidyanathan, K., Pamnany, K., Kalamkar, D.D., Heinecke, A., Smelyanskiy, M., Park, J., Kim, D., Shet, G.A., Kaul, B., Joo, B., Dubey, P., 2014. Improving communication performance and scalability of native applications on Intel Xeon Phi coprocessor clusters. In: 2014 IEEE 28th International Parallel and Distributed Processing Symposium, May, pp. 1083-1092.
- 从本章及其他章节下载代码，http://lotosforces.com。

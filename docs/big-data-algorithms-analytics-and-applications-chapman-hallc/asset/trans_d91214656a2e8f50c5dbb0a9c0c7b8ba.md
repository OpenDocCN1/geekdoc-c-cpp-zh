
x轴表示线程数，y轴表示执行时间（秒）。两种亲和性之间的差异可以从三个部分进行对比：

- 1. 当仅需要少量线程时，紧凑亲和性比分散亲和性更有效，如图20.2所示。当线程数少于八个时，紧凑亲和性仅使用少量核心（一到两个核心），因此线程之间的通信开销较小；另一方面，分散亲和性使用的核心数与线程数相同。
- 2. 在16到240个线程之间，分散亲和性比紧凑亲和性更快，如图20.3所示。在这种情况下，即使紧凑亲和性使用更少的核心，每个核心

![](img/1643181e79c76dc765d55a7355afb4a4_436_0.png)
图20.2 分散亲和性和紧凑亲和性在一到两个核心上的差异。

![](img/1643181e79c76dc765d55a7355afb4a4_436_1.png)
图20.3 分散亲和性和紧凑亲和性在多于两个核心上的差异。

![](img/1643181e79c76dc765d55a7355afb4a4_437_0.png)
图20.4 分散亲和性和紧凑亲和性的差异。

都满载了四个线程；它们会竞争硬件资源来执行，从而减慢单个执行速度，我们称之为“线程间干扰”，这超过了它们从节省通信开销中获得的好处。另一方面，在分散亲和性中，核心并未完全满载，这就显示出了好处。

- 3. 当线程数较多（超过240个线程）时，两种亲和性的效果几乎相同，如图20.4所示。在这种情况下，线程数超过了硬件能力（60个核心，每个核心4个线程，总共240个线程），因此无论采用哪种亲和性，所有核心都已满载。

总体而言，当我们在Xeon Phi上运行程序时，必须根据线程数和相应的并行级别来考虑合适的亲和性。

## 20.3.4 最佳线程数

在讨论了亲和性的影响之后，找到执行时的最佳线程数是另一个目标。我们尝试针对紧凑亲和性和分散亲和性分别确定最佳线程数。图20.5的结果表明，使用分散亲和性时，最佳线程数为120，对应于使用Xeon Phi上的全部60个核心，每个核心2个线程；使用紧凑亲和性时，最佳线程数为240，对应于使用Xeon Phi上的全部60个核心，每个核心4个线程。

![](img/1643181e79c76dc765d55a7355afb4a4_438_0.png)
图20.5 最佳线程数。

## 20.3.5 向量化

从图20.1可以看出，函数GetHammingDistance耗时第二，仅次于ReadFile函数。由于Xeon Phi配备了非常强大的向量引擎[19]，我们的目标是利用向量引擎来提高整体性能。因此，我们通过添加并行化和向量化来重写GetHammingDistance函数。由于我们已经讨论了最佳线程数和合适的亲和性，在这种情况下，我们使用分散亲和性运行程序。图20.6显示了在卸载模式下，使用和不使用向量化时，在Xeon Phi上运行虹膜匹配算法的执行时间。请注意，y轴采用对数刻度，因此基本上，2表示100秒，3表示1000秒，依此类推。显然，在所有情况下，向量化都提高了性能。最佳执行时间出现在我们使用最佳线程数120时。

![](img/1643181e79c76dc765d55a7355afb4a4_438_1.png)
图20.6 使用向量化与不使用向量化的多线程之间的差异。

## 20.4 结论

大数据生物特征识别处理提出了巨大的计算需求，同时它本质上也是高度并行的。在本研究中，作为案例研究，我们实现了虹膜匹配算法的OpenMP版本，并在创新的Intel Xeon Phi协处理器平台上评估了其性能。我们对虹膜匹配算法进行了工作负载特征分析，分析了不同的线程到核心亲和性设置对性能的影响，确定了运行工作负载的最佳线程数，最重要的是，对代码进行了向量化，以利用Xeon Phi自带的强大向量引擎来提高性能。根据我们的经验，尽管新兴的众核平台能够提供足够的并行性，但重新设计应用程序以利用硬件平台的特定特性，对于实现大数据处理的最佳性能非常重要。

## 致谢

我们感谢国家计算科学研究所（NICS）为我们提供访问BEACON超级计算机的权限以开展这项研究。我们还要感谢Gildo Torres和Guthrie Cordone的反馈，他们的反馈极大地改进了本实验的结果和本研究的质量。本工作得到美国国家科学基金会资助，资助号为IIP-1332046。本文所表达的任何观点、发现、结论或建议均为作者个人观点，不一定反映美国国家科学基金会的意见。

## 参考文献

- 1. Top 500 Supercomputer Sites, November 2013. Available at http://www.top500.org/.
- 2. A. Sussman, "Biometrics and Cloud Computing," presented at the Biometrics Consortium Conference 2012, September 19, 2012.
- 3. L. Meadows, "Experiments with WRF on Intel Many Integrated Core (Intel MIC) Architecture," in Proceedings of the 8th International Conference on OpenMP in a Heterogeneous World, Ser. IWOMP'12, Springer-Verlag, Berlin, Heidelberg, pp. 130–139, 2012.
- 4. J. Jeffers and J. Reinders, Intel Xeon Phi Coprocessor High Performance Programming, 1st ed., Morgan Kaufmann, Boston, 2013.
- 5. J. Dokulil, E. Bajrovic, S. Benkner, S. Pillana and M. Sandrisser, "Efficient Hybrid Execution of C++ Applications using Intel Xeon PhiTM Coprocessor," Research Group Scientific Computing, University of Vienna, Austria, November 2012.
- 6. K. Krommydas, T. R. W. Scogland and W. C. Feng, "On the Programmability and Performance of Heterogeneous Platforms," in Parallel and Distributed Systems (ICPADS), 2013 International Conference on, pp. 224–231, December 15–18, 2013.
- 7. P. Sutton, Benchmarks: Intel Xeon Phi vs. Sandy Bridge, 2013. Available at http://blog.xcelerit.com/benchmarks-intel-xeon-phi-vs-intel-sandybridge/.
- 8. J. G. Daugman, "High Confidence Visual Recognition of Persons by a Test of Statistical Independence," Pattern Analysis and Machine Intelligence, IEEE Transactions on, vol. 15, no. 11, pp. 1148–1161, 1993.
- 9. G. Torres, J. K.-T. Chang, F. Hua, C. Liu and S. Schuckers, "A Power-Aware Study of Iris Matching Algorithms on Intel's SCC," in 2013 International Workshop on Embedded Multicore Systems (ICPP-EMS 2013), in conjunction with ICPP 2013, Lyon, France, October 1–4, 2013.
- 10. OpenMP. Available at http://openmp.org/wp/.
- 11. E. Saule and U. V. Catalyurek, “An Early Evaluation of the Scalability of Graph Algorithms on the Intel MIC Architecture,” in 26th International Symposium on Parallel and Distributed Processing, Workshops and PhD Forum (IPDPSW), Workshop on Multithreaded Architectures and Applications (MTAAP), 2012.
- 12. G. Gan, “Programming Model and Execution Model for OpenMP on the Cyclops-64 Manycore Processor,” Ph.D. Dissertation, University of Delaware, Newark, DE, 2010.
- 13. Intel® VTune™ Amplifier XE 2013. Available at https://software.intel.com/en-us/intel-vtune-amplifier-xe.
- 14. J. K.-T. Chang, F. Hua, G. Torres, C. Liu and S. Schuckers, “Workload Characteristics for Iris Matching Algorithm: A Case Study,” in 13th Annual IEEE Conference on Technologies for Homeland Security (HST’13), Boston, MA, November 12-14, 2013.
- 15. Beacon. Available at http://www.nics.tennessee.edu/beacon.
- 16. The Green500 List, June 2013. Available at http://www.green500.org/lists/green201306.
- 17. Beacon on Top500. Available at http://www.top500.org/system/177997?U3MMkI4dufR.
- 18. P. A. Johnson, P. Lopez-Meyer, N. Sazonova, F. Hua and S. Schuckers, “Quality in Face and Iris Research Ensemble (Q-FIRE),” in Fourth IEEE International Conference on Biometrics: Theory Applications and Systems (BTAS), pp. 1-6, 2010.
- 19. E. Saule, K. Kaya and U. V. Catalyurek, “Performance Evaluation of Sparse Matrix Multiplication Kernels on Intel Xeon Phi,” arXiv preprint arXiv:1302.1078, 2013.


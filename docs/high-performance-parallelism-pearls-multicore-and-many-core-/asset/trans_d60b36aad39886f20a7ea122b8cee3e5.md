

## FIGURE 11.11

不同数据库规模下 DBThreads 的可扩展性分析。

![](img/16cb41208935c5f22dd1044f03f2e31b_253_0.png)

![](img/16cb41208935c5f22dd1044f03f2e31b_253_1.png)

![](img/16cb41208935c5f22dd1044f03f2e31b_253_2.png)

在 32 个线程之前表现尚可。超出之后，我们看到搜索组件的性能出现下降。尽管如此，与单线程情况相比，使用 120 个线程在 KD-tree 创建上带来了约 18× 的加速。当我们比较更大数据库规模下的扩展结果时，可以观察到相似的扩展模式，在 800 和 1200 张图像数据库中均如此，其中树创建时间在超过 64 个线程后达到谷底，而搜索时间改进在从 32 个线程增加到 64 个线程时跃升至 6×。

我们使用 Intel VTune Amplifier 分析器通过热点分析来研究扩展开销。图 11.13a 显示了使用 120 个线程运行时应用程序的热点分析，其中 libiomp5.so 库占据了 CPU 时间的主导地位。它是一个内部 OpenMP 库，用于在执行时管理 OpenMP 线程。此库中的 kmp_fork_call 是最热的函数。进一步调查问题后得知，创建一次的 OpenMP 线程会在程序生命周期内驻留在线程池中，处于主动自旋状态，准备在代码的下一个并行区域被调度。当将 OpenMP 线程数增加到 64 或 120 时，这种由于空闲自旋导致的影响会被进一步放大。我们还分析了如图 11.13c 所示的锁和等待时间以及调用栈，发现其中很大一部分花费在 libc 的 clone 模块中，该模块是内部用于线程创建的库。这种开销归因于大量线程创建以及等待临界区锁的关联空闲自旋。

## FLANN THREADS SCALING

由于在不同工作负载下 DB 线程的可扩展性在超过 64 个线程后出现谷底，我们接下来尝试在保持 DBthreads 和 KD-trees 不变的情况下改变 FLANN 线程数。可以从图 11.12 中观察到，增加 FLANNthreads 数量会减少树创建时间，但会增加搜索时间。这是因为 FLANN 线程主要利用应用程序中 KD-tree 创建部分的并行性。我们观察到在不同数据库规模下树创建时间减少了 23-58%。需要注意的是，每个 DB 线程并行创建 FLANN 线程。例如，如果将 FLANNthreads 参数设置为 2，在 800 张图像数据库的情况下，总共会创建 1600（800 × 2）个 FLANN 线程。因此，从实际角度来看，此参数不能超过 2 或 4，并且有必要根据 FLANN 线程的数量确定最佳的 KD-tree 参数。

如图所示 11.13b，显示了 FLANN 双线程版本的 VTune 前四个热点，OpenMP 开销主导了计算时间，如同 DB 线程的情况一样。此外，可以从图 11.13d 观察到，FLANN 内核的 CPU 利用率被系统库开销所占据。从图 11.13e 可以看出，CPU 利用率由 kmpc_global_thread_num 主导，并且与单线程版本 FLANN 相比，自旋锁时间增加了 14 倍。

## KD-TREE SCALING WITH DBTHREADS

为了克服收益递减规律，我们尝试增加要搜索的随机化 KD-tree 数量，最佳 DBThread 参数为 16（即 16），并将 FLANNthreads 数量保持在 1。需要强调的是，当我们增加 KD-tree 时，我们有效地增加了线程处理的总工作量，即相当于使用更大的输入。如图 11.14 所示，对于我们的 400 张图像数据库，16 个 KD-tree 的树创建时间和搜索时间分别比单 KD-tree 情况增加了 72× 和 31×。然而，KD-tree 大小为 16 或 32 在实际设置中更为现实，因为它为每个线程提供了更合理的 workload，从而提高了其计算密度。可以观察到，随着 KD-tree 数量的增加，创建时间和搜索时间的工作量都在增加。The

| Number of Images | DB,Flann,KD-trees | Create Time (ms) | Search Time (ms) |
|---|---|---|---|
| 400 | 16,1,1 | 16 | 15 |
|  | 16,2,2 | 13 | 92 |
| 800 | 16,1,1 | 28 | 29 |
|  | 16,2,2 | 19 | 325 |
| 1200 | 16,1,1 | 57 | 47 |
|  | 16,2,2 | 39 | 642 |

FIGURE 11.12

不同数据库规模下 FLANNThread 读取扩展。第二个列下的值对应于 <DB 线程、FLANN 线程和 KD-tree 数量 >。

| Module | CPU Time |
|---|---|
| libiomp5.so | 5.52 |
| vmlinux | 0.45 |
| FLANN::searchLevel | 0.08 |
| FLANN::meanSplit | 0.06 |

(a)

| Module | CPU Time |
|---|---|
| libiomp5.so | 1.03 |
| FLANN::meanSplit | 0.66 |
| FLANN::searchLevel | 0.58 |
| FLANN::selectDivision | 0.93 |

(b)

```
flann::NNIndex<flann::L2<float>>::knnSearch          libiomp5.so
flann_find_nearest_neighbors_index                    libflann.so.1.8.4
flann_find_nearest_neighbors_index<float, float>      libflann.so.1.8.4
flann_find_nearest_neighbors_index                    libflann.so.1.8.4
call_flannC                                           server
call_image_matching_module                            server
clone                                                 libc-2.12.so
```

(c)

![](img/16cb41208935c5f22dd1044f03f2e31b_255_0.png)

(d)

|  |  |  |  |
|---|---|---|---|
| ▶ kmpc_global_thread_num | 27.350s | 24.537s libiomp5.so |  |
| ▶ _kmp_fork_call | 9.109s | 9.109s libiomp5.so |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::search | 1.701s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::mean | 0.300s | 0s libflann.so.1.8.4 |  |
| ▶ std::_adjust_heap<__gnu_cxx::__normal_iter | 0.090s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::select | 0.040s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KNNSimpleResultSet<float>::addPoint | 0.030s | 0s libflann.so.1.8.4 |  |

(e)

## FIGURE 11.13

使用 120 个 DBThreads 和 2 个 FLANN Threads 在 800 张图像数据库中进行 VTune 分析。(a) 120 DBThreads 的热点，(b) 2 FLANN Threads 的热点，(c) DBThreads 的锁和等待时间，(d) 使用 FLANN 线程时的按线程 CPU 利用率，(e) 使用 FLANN 线程时的按模块 CPU 利用率。

![](img/16cb41208935c5f22dd1044f03f2e31b_256_0.png)

## FIGURE 11.14

使用 DBThread 计数配置扩展 KD-tree。X 轴上的值是 <DBThreads, KD-trees>。

使用多个 KD-tree 的内存开销也随构建的 KD-tree 数量线性增加。因此，在下一组实验中，我们将要构建的 KD-tree 数量固定为 32。

我们还研究了使用 32 个 KD-tree（图 11.15）和不同数量的 DBThreads 的可扩展性。我们发现通过构建更多随机化 KD-tree 来增加计算密度有助于提高图像搜索精度。同时，我们可以克服图 11.11 中显示的超过 32 个核心的可扩展性问题。可以看出，通过选择合适的 KD-tree 参数，与图 11.11 的扩展相比，我们在 32 到 120 之间观察到超过 6× 的可扩展性改进。我们还将相同的参数配置与处理器单独进行比较。在图 11.16 中，我们比较了处理器性能与处理器+协处理器组合在不同 KD-tree 数量下的性能。KD-tree 的创建时间在两种配置中都会增加，如果将单线程处理器性能与协处理器相比，我们观察到树创建时间和搜索时间分别提高了 34% 和 18%，后者主要是由于 KD-tree 一旦为数据库创建，就会在协处理器上多次运行时被重用。

我们还分析了协处理器代码中向量化的影响（图 11.17）。最高级别的向量化 O3 仅比没有任何优化的基线好 4%，


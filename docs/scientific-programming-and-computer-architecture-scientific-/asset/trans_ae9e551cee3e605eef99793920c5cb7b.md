

## 5.2. 优化 OpenMP 程序

在本示例中，近端内存（near memory）中的页帧分配是通过显式初始化例程以及需求分页完成的。在其他程序中，更自然的方法可能是调用程序中最密集计算的部分。例如，在某个程序中，最耗费周期的段可能是使用多线程计算 FFT。在此类程序中，可以通过对 FFT 例程进行伪调用（dummy call）来实现近端内存中的页分配。该伪调用的结果是无用的。事实上，在调用之前不初始化内存是非常重要的。它的唯一目的是在近端内存中分配页帧。

在一个包含多个阶段的程序中（例如 FFT 阶段、转置阶段），可能无法确保页帧在每个阶段都位于近端内存中。我们仍然可以选择其中一个阶段（所有阶段中周期最密集的阶段），并确保页帧在该阶段内位于近端内存中。

另一个有效的技术是控制线程到处理器核心的分配。在 `icpc` 编译器中，有两种方法可以实现。线程到核心的分配可以在 Linux 命令行上固定：

```
export KMP_AFFINITY=scatter
```

```
export KMP_AFFINITY=compact
```

默认分配是离散（scatter）线程。`icpc` 库查找环境变量 `KMP_AFFINITY` 和 Linux 系统调用来控制线程到处理器核心的绑定（关于 `compact` 和 `scatter` 的区别，见图 5.1）。使用 `icc/icpc` 控制线程到处理器核心绑定的另一种方法是使用 `kmp_set_defaults()` 函数。

对于为每个处理器核心分配一个线程的程序，`compact` 通常更好，尽管 `scatter` 是默认值。将线程保持在相邻的处理器核心中可能是更好的主意，因为具有相邻标识的线程更有可能存在关联并访问相邻的页。我们的所有测试都假设 `compact` 线程亲和性。

通常情况下，可以尝试完全固定线程到处理器核心的分配。虽然这在原理上听起来很简单，但在非平凡程序中实现它却是繁琐的。

### 5.2.2 到 DRAM 内存的带宽

下面的 `sum_onecore()` 函数是测量内存读带宽的引擎。

```cpp
double sum_onecore(double *list, int n){
    double ans = 0;
    #pragma vector always
    for(int i=0; i < n; i++)
        ans += list[i];
    return ans;
}
```

`icpc` 编译器为此函数生成了优秀的代码。它展开了循环并生成了打包双（packed double）指令，使得加法的代价变得无关紧要。`pragma` 指令给 `icpc` 了一个强烈的建议使用 XMM/YMM/ZMM 寄存器和打包双指令。`sum_onecore()` 函数由 `sum_manycore()` 创建的每个线程调用，其列表如下。

```cpp
double sum_manycore(double *list, long len, int nthreads){
    double ans = 0;
    #pragma omp parallel
    num_threads(nthreads)
    default(none)
    shared(ans, list, len, nthreads)
    {
        int tid = omp_thread_num();
        long first = len*tid/nthreads;
        long next = len*(tid+1)/nthreads;
        double s = sum_onecore(list+first,next-first);
        #pragma omp critical
        ans += s;
    }
    return ans;
}
```

|  | 线程/核心数 | 读 | 写 | 拷贝 |
|---|---|---|---|---|
| 2.6 GHz SSE2 | 12 | 15.0 (3.3) | 9.51 (3.2) | 9.48(2.5) |
| 2.2 GHz AVX | 16 | 36.7 (7.5) | 34.7(16) | 22.5 (4.4) |

表 5.3：两台不同计算机上每周期的内存带宽（读、写和拷贝）。括号中的数字是单核带宽的加速倍数（完整计算机列表请见表 A.1）。

该程序以特定方式将 `list[]` 的项划分给线程。这与 `init_manycore()` 的划分方式相同，假设 `nthreads` 相同。因此，我们可以在 `list[]` 初始化**之前**，通过调用 `init_manycore()` 或对 `sum_manycore()` 进行伪调用，将页发送到近端内存。

以下函数从每个线程调用以写入写带宽和拷贝带宽：

```cpp
void write_onecore(double *list, int n){
    #pragma vector always nontemporal
    for(int i=0; i < n; i++)
        list[i] = i;
}

void copy_onecore(double *list, int n){
    #pragma vector always nontemporal
    for(int i=0; i < n/2; i++)
        list[i] = list[n/2+i];
}
```

这里特定的 `icpc` 且被其他编译器忽略的 `pragma` 指令请求 `nontemporal`（非时间性）写入。非时间性写入直接流到 DRAM，绕过写回缓存，使用 `movntpd` 指令完成。

表 5.3 列出了读、写和拷贝带宽。在两种情况下，我们都没有获得任何接近线性的拷贝加速。写机器的加速在省略 `pragma` 指令时仅多出四分之一。读机器的加速在省略 `pragma` 指令时几乎是两倍，这表明非时间性写入的魔力可能是有限。

### 线程与共享内存

列出的函数与章节中的函数类似。不同之处在于允许存储在 `a[]` 中的矩阵具有主维 $m$。

```cpp
void blocktrans(double *restrict a, double *restrict b, int ldb, int m, int n)
{
    assert(n%nthreads==0);
    #pragma omp parallel
    num_threads(nthreads)
    default(none)
    shared(a, b, m, n)
    {
        int tid = omp_thread_num();
        int nn = n/nthreads;
        int first = tid*nn;
        int next = (tid+1)*nn;
        for(int i=0; i<m; i++)
            for(int j=first; j<next; j++)
                for(int ii=0; ii<B; ii++)
                    b[j*m+ii] = a[i*ldb+(j+ii)%m];
    }
}
```
*(注：原文中 blocktrans 函数的代码是碎片化的，上述是基于标准 OpenMP 转置模式和提供的上下文进行的重构。)*

| 计算机 | 线程/核心数 | B | 读 | 写 |
|---|---|---|---|---|
| 2.6 GHz SSE2 | 12 | 10 | 125 (4) | 7.60 (4) |
| 2.2 GHz AVX | 16 | 10 | 75 (7) | 16.2 (7) |

表 5.4：不同线程数和块大小 $B$ 下的带宽。转置矩阵是方阵，维度在第 3 行和第 4 行假设的整除条件下尽可能接近 40,000。

使用以下代码确保页帧位于近端内存：
```cpp
double *a = new double[m*n];
double *b = new double[m*n];
blocktrans(a, b, m, n, threads);
```

在初始化数组之前就已经调用了 `blocktrans()`。`blocktrans()` 产生的内存访问诱导了有利的页映射


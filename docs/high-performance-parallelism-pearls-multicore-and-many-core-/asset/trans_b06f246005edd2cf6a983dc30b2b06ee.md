

兼容 Intel Xeon Phi 加速器与 Intel 处理器之间的兼容性。我们在 RHEL（Red Hat Enterprise Linux）发行版上使用 3.10.0 Linux 内核，对 Intel Xeon 处理器进行了实验和分析。我们的内核没有用于测量 RAPL（Runtime Average Power Limit）性能事件的适当 PAPI（Performance Application Programming Interface）内核修改，需要进行补丁。

我们测量不同类型的 OpenMP 亲和性的每瓦计算性能，具体为 compact 和 scatter。如上所述，“compact”亲和性按顺序将连续线程打包到同一核心上，然后继续在相邻核心上打包，以最好地允许资源共享（如缓存）。相比之下，“scatter”亲和性将连续线程分散到不同核心上，在线程之间共享或同步很少的环境中有用。

保持粒度为“fine”。有三种粒度类型，“core”、“fine”和“thread”。使用“core”粒度将 OpenMP 线程绑定到特定核心，意味着只有一个特定核心，例如 core25，将执行给定的 OpenMP 线程；尽管该线程可以移动到在该核心上执行的四个不同线程上下文中的任何一个。使用“fine”或“thread”粒度是相同的，导致 OpenMP 线程仅绑定到该核心内的一个线程上下文。默认 OpenMP 粒度为“core”。你可以使用 KMP_AFFINITY 环境变量在运行时设置粒度，

```
export KMP_AFFINITY='scatter,granularity=fine'
```

使用 Class C 问题规模。这样每个数据采集的运行时间在合理时间内完成。每次采集 244 次运行大约需要 45 分钟，需要大约 3 小时才能收集全部四组数据。根据处理器的速度和实验可用时间，你可能希望将问题规模设置为更小（CLASS = B）或更大（CLASS = D）。你通过“make”中的 CLASS 操作数设置问题的规模。

将线程从一个变化到加速器可以同时执行的线程的最大数量，即 244。你可以通过几种不同的方式做到这一点。我们选择使用 OpenMP 运行时环境变量 OMP_NUM_THREADS。由于亲和性会影响线程在核心间的分布，其影响与应用程序线程数相关联。

为减少收集的数据量，每次采样使用的线程数增加四个线程，例如，样本 1 使用一个线程，样本 2 使用五个线程，样本 3 使用九个线程，依此类推。在加速器的情况下，由于每个核心可以同时执行四个线程，因此这是一个自然的数字。请参见图 25.2。只要我们在采样，当每个核心执行的线程数相同时，样本之间的功率相对差异得以保持，我们拥有相似的数据。如果我们相反比较以每个核心三个线程结束的样本与以每个核心一个线程结束的样本，我们将比较不相似的数据，因为三个线程的核心功耗将大于一个线程的核心功耗。虽然这在使用“scattered”亲和性时不重要，但对于 compact，我们希望使用可以执行在核心上的线程数的倍数。对于 Intel® Xeon 处理器，这是每个核心两个线程。对于 Intel® Xeon Phi™ 加速器，这是每个核心四个线程。使用此增量不应影响收集的数据或分析。

对每个线程数和每种亲和性类型重复整个数据采集四次并平均结果。更多采集运行可以实现更具统计严谨性的数据，但就本次采集而言，四次运行足以说明技术。

## DATA COLLECTION

对于每次数据采集，请参见图 25.3，记录 NPB EP 的默认输出，然后转储 /sys/class/micras/power 中包含的功率信息。你可能希望以更常规的形式表达此脚本，如图 25.4 所示，使用带参数的脚本文件。在 Pearls 网站，http://lotsof cores.com，你会找到这些相同的脚本，但采用更传统的多行形式。图 25.5 中的形式很方便，因为它允许在无需每次编辑和验证的情况下进行非常快速的实验和

```
#script to collect the data
export KMP_AFFINITY='scatter,granularity=fine' ; for j in 1 2 3 4 ; do >&2 echo ; >&2 echo EXPT $j; for i in {1..244..4}; do export OMP_NUM_THREADS=$i; echo OMP_NUM_THREADS\($OMP_NUM_THREADS\); >&2 echo -n $OMP_NUM_THREADS; ./ep.C.knc ; echo PWR******; cat /sys/class/micras/power ; done > epC_1_244_4_scatter_$j.log ; done
```

FIGURE 25.3
Script to collect power and performance data from an Intel Xeon Phi coprocessor.

```
#script to collect the data
export KMP_AFFINITY='scatter,granularity=fine' ; \
for j in 1 2 3 4 ; do \
    >&2 echo ; \
    >&2 echo EXPT $j; \
    for i in {1..244..4}; do \
        export OMP_NUM_THREADS=$i; \
        echo OMP_NUM_THREADS\($OMP_NUM_THREADS\); \
        >&2 echo -n $OMP_NUM_THREADS; \
        ./ep.C.knc ; \
        echo PWR******; \
        cat /sys/class/micras/power ; \
    done \
    > epC_1_244_4_scatter_$j.log ; \
done
```

FIGURE 25.4
A more conventional view of the script to collect power and performance data from an Intel Xeon Phi coprocessor.

```
#Script to reduce the data
$ sed -n '/^OMP/ p; /Completed/{N;N;N;N;N; p;}; /Mop/ p; /^PWR/{N;N;p}' epC_1_244_4_scatter_1.log > epC_1_244_4_scatter_reducedA.log
#strip out unused lines
$ sed -n '/Time/{s/[^0-9.]*\/n/; p}; /threads/{s/[^0-9.]*//g; p}; /Mop/{s/[^0-9.]*//g; p}; /^PWR/{N;N;s/^PWR[*]*\n//;p}' epC_1_244_4_scatter_reducedA.log > epC_1_244_4_scatter_reducedB.csv
#strip out unwanted text
$ sed -n '/^$/{N;N;N;N;N;N; s/\n/,/g; p}' epC_1_244_4_scatter_reducedB.csv > epC_1_244_4_scatter_reducedC.csv
#put in csv format using ",".
```

# FIGURE 25.5

Script to extract desired performance power data and delete unneeded data.

定制。图 25.6 和 25.7 是两种输出的示例。对以下两种情况执行此数据采集

```
KMP_AFFINITY = 'scatter,granularity=fine' and
KMP_AFFINITY = 'compact,granularity=fine'.
```

使用另一个脚本，如图 25.7 所示来提取数据。图 25.7 中的 sed（Stream EDitor）脚本提取可用线程数、CPU 时间、Mop/s 总计、Mop/s/线程、win 0 的总功率和 win 1 的总功率。然后将其结果以 CSV 数据格式放置。

（对于加速器，/sys/class/micras/power 的数据输出格式在源代码之外几乎没有文档记录，即使那样也很少定义“win 0”和“win 1”具体是什么，除了它们是某个间隔的功率平均值。请参阅文章，https://software.intel.com/en-us/articles/measuring-power-on-intel-xeon-phi-product-family-devices。尝试使用其中一个与另一个进行比较，看看是否有显著差异。）

使用你喜欢的工具绘制结果。我们使用 Microsoft Excel 导入、减少和绘制数据。

为此数据获取两个图，Performance/Power 和 Power/Thread Number。两者都提供了有关亲和性如何影响应用程序功耗的见解。你的图应与图 25.8 和 25.9 非常相似。图 25.8 显示性能每瓦特（Mops/s/W）作为 OpenMP 线程数函数的。图 25.9 显示功率（瓦特）本身作为线程数的函数。

## ANALYSIS

我们将首先查看 Intel Xeon Phi 加速器的功率和性能，然后查看 Intel Xeon 处理器。我们可以指出图的某些关键特征并推断其来源。你应该将这些图与你自己的进行比较，看看是否能识别出相似的特征。图 25.8 显示性能（Mega operations/sec）每消耗功率或 Mops/s/W。此每瓦性能图或许是最有力的证据，证明 OpenMP 亲和性对应用程序消耗的功率的影响。

散布亲和性结果与紧凑亲和性之间最大的差异是什么？图 25.8 显示在某些点，散布亲和性的每瓦性能比使用紧凑亲和性时高出超过两个 Mop/s。作为健全性检查，验证两个图是否收敛


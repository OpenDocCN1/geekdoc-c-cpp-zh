
计算被卸载到协处理器上，而其余的串行代码继续在处理器上运行。在对称实现中，协处理器通常通过 MPI 协议被独立用作为自足的计算节点。我们仔细检查了源代码，以确定哪种并行模式最适合 eFindSite。我们仔细考虑了几个因素。eFindSite 的框架用 C++ 编写，而蛋白质结构比对用 Fortran77 实现。对于每个单独的模板-目标结构比对，都会从主函数调用子例程 frtmalgn。图5.3显示了由 Doxygen 生成的详细调用图，说明了 frtmalgn 及其子例程的嵌套函数调用。使用 Fortran 特定的 OpenMP 编译指示将结构比对计算转移到协处理器，所需的代码转换最少。此外，一些比对前和比对后的函数（例如用于对模板结合配体进行分组的亲和传播聚类）仅以针对 Linux 主机预编译的外部库形式提供。此外，根据先前执行的代码剖析，eFindSite 的总内存占用会随着目标蛋白质大小和相关模板数量的增加而增长，考虑到协处理器上可用的内存空间，这些值大到令人望而却步。因此，我们排除了原生执行模式，并决定仅将结构比对部分“卸载”到协处理器，而将其余部分

![](img/16cb41208935c5f22dd1044f03f2e31b_109_0.png)

图5.3
蛋白质结构比对子例程的调用图。frtmalgn 作为顶层子例程在 eFindSite 的主函数中被调用。

代码的其余部分（包括比对前和比对后的计算）留在处理器上。在本章中，我们讨论使用卸载模式对 eFindSite 进行并行化，并针对 501 个目标蛋白质进行性能分析。

## 移植 eFindSite 以支持协处理器卸载

eFindSite 并行版本的流程图如图5.4所示。eFindSite 以目标蛋白质结构和配体结合模板库作为输入，来识别配体结合位点。结果，它产生一系列信息丰富的预测，包括推定的配体结合位点和结合残基、目标蛋白质与模板蛋白质之间的结构比对，以及用于虚拟筛选的配体分子指纹。作为结合位点预测核心的工作流程分为三个阶段。在比对前步骤中，eFindSite 从库中提取模板信息，并构建与目标的全局序列比对；这些计算在处理器上顺序执行。接下来，它将每个模板结构比对到目标上；此部分非常适合并行计算，因为各个比对彼此完全独立。代码剖析也指出这部分代码是计算最密集的。因此，我们决定对结构比对循环进行并行化，以便使用

![](img/16cb41208935c5f22dd1044f03f2e31b_110_0.png)

# 图5.4

eFindSite 的工作流程。比对前和比对后的计算使用单个处理器线程执行。结构比对使用处理器和/或协处理器上的多个线程并行执行。

多个处理器和/或协处理器线程。图5.4显示了每个结构比对被分配给一个唯一的硬件线程，因此不同的线程针对目标蛋白质并发地执行不同模板的计算。一旦结构比对完成，结果被发送回处理器，处理器在最终的比对后步骤中对识别出的结合口袋进行聚类和排序，并预测相应的结合残基。

在以下各节中，我们讨论将 eFindSite 移植到协处理器的一些细节。在主函数中，结构比对在一个遍历模板库的主循环内执行。结构比对的并行化是通过使用标准 OpenMP 编译指示并发执行每个比对来实现的，如图5.5所示。当主函数内调用包装函数 frtmalgn 时，结构比对开始执行，该函数调用用 Fortran77 实现的串行子例程 frtmalign 来进行实际的比对计算。我们发现这部分代码大量使用公共块，导致结构比对线程不安全。为了保证线程安全，我们使用 [!$omp threadprivate (/block_name/)] 将所有 Fortran77 公共块标记为线程私有，如图5.6所示。

eFindSite 的这种实现将部分代码卸载到协处理器上，在协处理器上执行结构比对，然后将结果传回处理器以执行最终的比对后计算。由于协处理器具有自己的内存，卸载模式需要在处理器和协处理器之间进行数据传输。eFindSite 使用 C++ 类来存储和操作与模板蛋白质相关的数据，例如原子坐标、氨基酸残基和序列。为了便于数据传输，我们额外做了工作，将原始数据结构转换为扁平的、可按位复制的数据数组，然后将其传输到协处理器，如图5.7所示。我们注意到，包含目标蛋白质和模板库的数组仅被复制到协处理器一次，因此来回移动数据的开销几乎为零。每个结构比对

```
//loop through the library of template proteins to conduct structure alignments
std::multimap< int, Template *, greater<int> >::iterator tpl1;
//parallelize the loop
#pragma omp parallel for schedule(dynamic) private(tpl1)
for (tpl1 = template_set.begin(); tpl1 != template_set.end(); tpl1++) {
    char template_seq[MAXPRO];
    int template_res[MAXPRO];
    double template_xyz[MAXPRO][3];
    //assemble protein residue, sequence and coordinate from the template library
    int template_len = ((*tpl1).second)->getProteinResiduesTotal();
    strcpy(template_seq, (((*tpl1).second)->getProteinSequence()).c_str());
    for ( int t_i =0; t_i < template_len; t_i++) {
        template_res[t_i] = t_i +1;
    }
    ((*tpl1).second)->getProteinCoordsCA(template_xyz);
    int t_score1, t_alig[MAXPRO];
    double t_score2, t_score3, t_score4, t_t[3], t_u[3][3];
    // call structure alignment subroutine
    frtmalign_(&t_score1, &t_score2, &t_score3, &t_score4, &template_len,\
    &target_len, &template_seq, &target_seq, &t_alig, &template_res,\
    &target_res, &template_xyz, &target_xyz, &t_t, &t_u, &align_len);
}
```

# 图5.5

主循环的 OpenMP 并行化，该循环执行目标蛋白质与一组配体结合模板之间的结构比对。

```
subroutine
frtmalign(tm_score1,tm_score2,tm_score3,tm_score4,target_len,template_len,
&           target_seq,template_seq,tm_align,target_res,template_res,
&           target_xyz,template_xyz,tm_tt1,tm_uu1,align_length)

parameter (maxres=1000)          ! no. of residues
parameter (maxlen=2*maxres)      ! for alignment
parameter (npr=2)                ! no. of proteins to align
double precision tm_score2,tm_score3,tm_score4,tm_xyzla(0:2,0:maxres-1),
&           template_xyz(0:2,0:maxres-1), tm_tt1(0:2),tm_uu1(0:2,0:2)
integer tm_score1,target_len,template_len, align_length,
&           tm_align(0:maxres-1),target_res(0:maxres-1),
&           template_res(0:maxres-1)
character*1 target_seq(0:maxres-1), template_seq(0:maxres-1)
character*3 resa(maxres,npr),resn(maxres,0:1)
character*1 seqa(maxres,npr),seqn(maxres,0:1)
dimension invmap0(maxres),ires(maxres,0:1)
dimension xtm1(maxres),ytm1(maxres),ztm1(maxres)
dimension xtm2(maxres),ytm2(maxres),ztm2(maxres)
dimension m1(maxres),m2(maxres)
dimension xyz(3,maxres,npr),length(npr)
common /coord/ xa(3,maxres,0:1)
common /length/ nseq1,nseq2
common /pdbinfo/ ires1(maxres,npr),resa,seqa
common /secstr/ isec(maxres),jsec(maxres)      !secondary structure
common /nln2/ n1(maxres),n2(maxres)
common /dinfo/ d8
common /stru/xt(maxres),yt(maxres),zt(maxres),xb(maxres),yb(maxres),
&               zb(maxres)
// OpenMP pragma to mark thread private
! $omp threadprivate(/coord/)
! $omp threadprivate(/length/)
! $omp threadprivate(/pdbinfo/)
! $omp threadprivate(/secstr/)
! $omp threadprivate(/nln2/)
! $omp threadprivate(/dinfo/)
! $omp threadprivate(/stru/)

cc call other routines...
end
```

# 图5.6

Fortran77 中公共块的线程安全实现。

该比对在协处理器上执行时，会通过偏移机制从传输的数据块中提取给定模板所需的数据。此外，我们使用编译器指令来标记卸载执行，如图5.8所示。具体来说，协处理器上用于结构比对计算的所有 Fortran77 子例程和全局变量分别使用卸载属性 [!dir$ attributes offload:mic:: subroutine_name] 和 [!dir$ attributes offload:mic::variable_name] 进行标记。此外，当在卸载块内调用 OpenMP 时，使用“MIC_”前缀设置协处理器的环境变量，即 [export MIC_OMP_NUM_THREADS=n]。由于 eFindSite 中单个结构比对的内存占用大于默认的 OpenMP 堆栈大小，我们通过使用 [export MIC_OMP_STACKSIZE=64M] 来增大它。

Intel Xeon Phi 协处理器型号 SE10P 具有 61 个内核，支持多达 240 个并行线程，其中第 61 个内核在使用卸载时保留给操作系统、I/O 操作等。线程在硬件内核上的物理分布由线程亲和性设置控制，

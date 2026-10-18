

## FIGURE 10.4

ℓ₁ℓ₂ℓ₃ 迭代空间的结构，显示了有效和无效的迭代。

将线程添加到 ℓ₁ 循环将得到一个 MPI/OpenMP 混合代码，可以扩展到使用 O(1000) 个协处理器，每个协处理器有 2000 个并行任务。虽然这听起来像是一个很棒的想法，但这种设置的问题在于嵌套循环的三角形结构会导致 ℓ₁ 循环中的负载不均衡，这在图 10.5 中针对四个线程进行了可视化。OpenMP 中不平衡的循环通常通过使用动态调度或基于任务的并行性来处理。在我们的实验中，我们发现这些方法由于无法将特定组的并行任务绑定到同一核心而导致缓存行为不佳和数据重用水平低。此外，这种方法只是对问题进行了修补，并没有解决根本的算法问题。

理想的解决方案是将整个 ℓ₁ℓ₂ℓ₃ 循环巢展平为一维迭代空间，并尽可能均匀地在线程之间分配迭代。OpenMP 提供了 collapse pragma 来精确地执行此操作；然而，在存在循环边界之间依赖关系的情况下，如我们这种情况，则无法使用。我们选择手动重构循环，使其可以从指定的起始 ℓ₁ℓ₂ℓ₃ 三元组运行到指定的结束三元组，如图 10.6 所示。这样，分配给协处理器上给定并行任务的工作可以用六个边界整齐地表示：(lower_l1, lower_l2, lower_l3, upper_l1, upper_l2, upper_l3)。

为了确定这些边界，我们首先执行整个循环巢的“试运行”以计算总迭代次数 N。接下来，我们在 P 个并行工作者之间均匀分配迭代次数，将余数分配给前 N mod P 个工作者。最后，循环的另一次遍历会根据分配给每个工作者的迭代次数记录每个工作者的 ℓ₁ℓ₂ℓ₃ 边界。这给出了一个

Valid (ℓ₁, ℓ₂) and ℓ₃

Valid (ℓ₁, ℓ₂) but invalid ℓ₃

## FIGURE 10.5

对循环巢并行化的天真尝试。每个颜色对应一个不同的线程。

```
int start_l1 = lower_l1;
int end_l1 = upper_l1+1;
for (l1=start_l1; l1<end_l1; l1++)
{
    int start_l2 = l1 == lower_l1 ? lower_l2 : l1;
    int end_l2 = l1 == upper_l1 ? upper_l2+1 : lsize;
    for (l2=start_l2; l2<end_l2; l2++)
    {
        int start_l3 = l2+(l1/2);
        int end_l3 = min(l1+l2,lmax)+1;
        if ((l1==lower_l1) && (l2==lower_l2))
        {
            start_l3 = lower_l3;
        }
        if ((l1==upper_l1) && (l2==upper_l2))
        {
            end_l3 = upper_l3;
        }
        for (l3 = start_l3; l3 < end_l3; l3 += 2)
        {
            // loop interior...
        }
    }
}
```

## FIGURE 10.6

图 10.3 中所示循环的展平版本，可以在三角形迭代空间中的任意下限和上限点之间运行。

## FIGURE 10.7

循环巢的优化线程调度（关于迭代次数）。

在假设所有迭代花费相同时间的情况下，实现了最佳负载平衡的循环，如图 10.7 所示。我们已经在经验上观察到这种情况。

现在我们有了可用的卸载实现，我们可以开始迭代优化过程，以缩小处理器和协处理器性能之间的差距。查看协处理器上运行的代码配置文件，我们发现其执行时间的一半以上花费在图 10.3 中所示的函数 plijk 上。这是一个简单的内联函数，用于索引一些数组并计算图 10.2 中第二个方程的第二行，给定 ℓ1ℓ2ℓ3。该函数已经由编译器很好地向量化，因此仅通过微优化很难获得太多收益——然而，仔细查看图 10.3 中的代码，我们可以看到 plijk 对每个 ℓ1ℓ2ℓ3 三元组调用 Nterms² 次。这可以通过改变循环顺序减少到 Nterms 次调用，将 n 循环移入 ℓ 循环内部并将结果存储在数组 x[n] 中。循环巢的重排版本显示在图 10.8 中。

在此重排循环巢之后，很明显原始代码的 MPI 并行化是低效的；对 n 进行并行化会分配 calculate_xint 的工作，但会在所有处理器上冗余计算 plijk。正如线程的情况一样，我们现在必须找到一种方法将三角形循环巢分布到 MPI 秩上。幸运的是，之前为线程描述的方法可以很容易地扩展以在并行层次结构的多个级别之间分配工作：我们首先在 MPI 任务之间分配迭代，然后在 OpenMP 线程之间细分这些迭代。

```
for (l3 = start_l3; l3 < end_l3; l3 += 2)
{
    for (n = 0; n < terms; n++)
    {
        x[n] = calculate_xint(l1,l2,l3,n,xsize,xvec,yvec,thread_data[
            tid].task_spl);
    }
    double s1 = svec[l1]; double s2 = svec[l2]; double s3 = svec[l3];
    double z = permsix(l1,l2,l3)*calculate_geometric(l1,l2,l3)/sqrt(s1*s2*s3);
    for (m = 0; m < terms; m++)
    {
        double y = plijk(m,l1,l2,l3);
        for (n = 0; n < terms; n++)
        {
            mmat[m][n] += x[n] * y * z;
        }
    }
}
```

## FIGURE 10.8

图 10.3 中所示循环体的重新排列版本。

## INTRODUCING NESTED PARALLELISM

尽管新的循环结构减少了算法复杂性，从而减少了所需的工作总量，但考虑其内存使用情况很重要——天真的实现要求每个线程都存储 x 和 plijk 的外积在临时矩阵 mmat 中，该矩阵有 N_terms^2 个元素。对于典型的 N_terms 大小，mmat 每个线程需要 O(10MB) 的内存，远远超过 Intel Xeon Phi 协处理器上 512 kB L2 缓存的容量，并可能导致 Intel Xeon 处理器上更大的 L3 缓存的容量问题。我们希望每个核心运行两个到四个线程这一事实只会使问题更糟（见图 10.9），并且线程之间对容量的竞争甚至可能导致抖动。

理想情况下，我们应该只为每个核心保留一个 mmat 的副本，避免冗余计算，并紧密控制数据放置以最大化缓存重用并避免伪共享。只有通过重新排列循环以适应嵌套并行，才能同时实现所有这些目标，将外部 l 循环拆分到核心上，将内部 n 和 m 循环拆分到每个核心上的线程上。这种简单的线程到工作的重新映射显著减少了内存需求，并且还确保了

![](img/16cb41208935c5f22dd1044f03f2e31b_228_0.png)

## FIGURE 10.9

每个线程的临时数据 mmat 大于协处理器核心上的 L2 缓存。使用每个核心四个线程时，这个问题会四倍恶化。

成本在嵌套区域经常遇到时是禁止的，例如当线程为最内层循环生成时。

然而，Intel® OpenMP 运行时（版本 15 更新 1 或更高版本）中支持一个实验性功能，称为“热团队”，它能够通过在非嵌套并行代码执行期间保持线程池存活（但处于空闲状态）来减少这些开销。热团队的使用由两个环境变量控制：KMP_HOT_TEAMS_MODE 和 KMP_HOT_TEAMS_MAX_LEVEL。为了在团队大小变化时保持未使用的团队成员存活，我们设置 KMP_HOT_TEAMS_MODE=1，并且由于我们有两级并行性，我们设置 KMP_HOT_TEAMS_MAX_LEVEL=2。

还必须注意线程亲和性设置。OpenMP 4.0 提供了新的环境变量来处理线程的物理放置，OMP_PROC_BIND 和 OMP_PLACES，并且这些变量与嵌套并行区域兼容。为了将团队领导者放置在单独的核心上，并将团队成员放置在同一核心上，我们设置 OMP_PROC_BIND=spread,close 和 OMP_PLACES=threads。

## OpenMP 4.0 TEAMS

teams 和 distribute 构造被添加到 OpenMP 4.0 中，作为其对加速器的支持的一部分，并且类似于 OpenACC 提供的“gang”和“worker”模型。图 10.11 显示了对简单循环巢的示例。

使用 teams 需要比简单嵌套更广泛的代码更改，因为对其使用有一些限制。首先，teams 构造必须包含在 target 构造内，因此不能轻易用于主机上的嵌套并行——teams 区域只有在 target 构造的“if”子句计算为 false 时才能在主机上执行！其次，它必须是该 target 构造中出现的第一个语句，因此在串行和并行代码之间切换需要单独的 target 构造（导致卸载代码的不必要的宿主-设备同步）。第三，虽然团队内的线程可以用 OpenMP barrier 同步，但不同团队中的线程不能同步（除非通过 teams 和 target 区域的关闭）。

这些限制使这种方法比简单嵌套的灵活性更差，并且还迫使开发人员为主机和设备维护相同代码的单独版本。将 OpenMP 4.0 teams 逆向移植到我们现有的预先存在的代码中很困难，因为它不是考虑到这些限制而设计的。对于已经分为并行内核的代码（例如 CUDA 或 OpenCL 代码），这种逆向移植过程将需要更少的广泛更改。

```
#pragma omp target device(0)
partition_block(lsize, omp_get_num_teams(), &start_l, &end_l);

#pragma omp target device(0)
#pragma omp teams num_teams(60) thread_limit(4)
for (l = start_l; l < end_l; l++)
{
    #pragma omp parallel for num_threads(4) schedule(static,1)
    for (n = 0; n < terms; n++)
    { ... }
}
```

## FIGURE 10.11

OpenMP teams 区域的示例。teams 构造必须在 target 构造之后立即调用。


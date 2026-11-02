
如果估计量是无偏的，则可以由估计量来估计。注意，\([h_l, h_u]\) 可以关于实际估计值 \(h(x_0, x_1, \ldots, x_{n-1})\) 不对称。当分布 \(F_{H^*}\) 偏斜时，就会发生这种情况。

为简单起见，正如我们在第 8.3.2 节中所见，可以使用方差 \(\operatorname{Var}[H]\) 来描述估计量的统计不确定性。如第 289 页所述，这基本上对应于 \(\alpha=0.32\) 的不确定性。标准误差棒对应的量是 \(\sqrt{\operatorname{Var}[H]}\)。

下面的 C 函数计算 \(\operatorname{Var}[H^*]\)，作为未知 \(\operatorname{Var}[H]\) 的近似。需要传递的参数包括样本点数量 \(n\)、包含样本点的数组、bootstrap 迭代次数 \(K\)，以及指向表示估计量的函数 \(f\) 的指针。\(f\) 必须接受两个参数：样本点数量和包含样本的数组。函数指针的说明见第 59 页。函数 `bootstrap_variance()` 返回 \(\operatorname{Var}[H^*]\)。

**获取源代码**

- 目录：randomness
- 文件：`bootstrap.c`, `bootstrap_test.c`

```c
double bootstrap_variance(int n, double *x, int n_resample,
                          double (*f)(int, double *))
{
    double *xb;      /* bootstrap sample */
    double *h;       /* results from resampling */
    int sample, i;   /* loop counters */
    int k;           /* sample point id */
    double var;      /* result to be returned */

    h = (double *) malloc(n_resample * sizeof(double));
    xb = (double *) malloc(n * sizeof(double));
    for (sample = 0; sample < n_resample; sample++)
    {
        for (i = 0; i < n; i++) /* resample */
        {
            k = (int) floor(drand48() * n); /* select random point */
            xb[i] = x[k];
        }
        h[sample] = f(n, xb); /* calculate estimator */
    }

    var = variance(n_resample, h); /* obtain bootstrap variance */
    free(h);
    free(xb);
    return(var);
}
```

bootstrap 样本 \(\{x_i^*\}\) 存储在数组 `xb` 中，而采样得到的估计值 \(\{h_i^*\}\) 存储在数组 `h` 中。这些数组在第 10-11 行分配。在主循环（第 12-20 行）中计算 bootstrap 样本，每次获得估计量并将结果存储在 `h` 中。最后，计算样本 \(\{h_i^*\}\) 的方差（第 22 行）。这里使用了 `variance()` 函数，其工作方式与 `mean()` 函数类似，参见练习（5）。练习（6）要求你实现一个用于一般置信区间的 bootstrap 函数。

最直接的方式是将估计量均值作为第四个参数调用 `bootstrap_variance()`。对于“表现良好”的分布（即少量随机变量之和类似于高斯分布的分布），只要 `n_resample` 足够大，得到的方差将非常接近标准高斯（\(\alpha=0.32\)）误差棒。

对于计算样本均值的性质，bootstrap 方法效果很好，但在这种情况下，标准高斯置信区间也足以令人满意。对于非标准估计量，bootstrap 方法更有意义。统计物理学领域一个著名的例子是所谓的 Binder 累积量 [Binder (1981)]，其定义如下：

\[
b(x_0, x_1, \ldots, x_{n-1}) = 0.5 \left( 3 - \frac{\overline{x^4}}{[\overline{x^2}]^2} \right) \tag{8.71}
\]

其中上划线同样表示样本均值，例如 \(\overline{x^2} = \frac{1}{n} \sum_{i=0}^{n-1} x_i^2\)。Binder 累积量通常用于通过模拟确定相变，此时只能研究由有限数量粒子组成的系统。例如，考虑一个处于某个温度 \(T\) 的铁磁系统。在低于居里温度 \(T_c\) 的低温下，系统会表现出宏观磁化强度 \(m\)。另一方面，对于高于 \(T_c\) 的温度，随着系统尺寸增大，\(m\) 平均而言会收敛到零。如果系统尺寸较小，这种转变是模糊的。然而，当对不同组样本点 \(\{m(T,L)_i\}\) 评估 Binder 累积量时（这些样本点是在多个温度 \(T\) 和不同系统尺寸 \(L\) 下获得的），不同 \(L\) 对应的 \(b_L(T)\) 曲线都会（几乎）在 \(T_c\) 处交叉 [Landau and Binder (2000)]，从而可以非常精确地确定 \(T_c\)。图 8.21 展示了一个二维（即层状）模型铁磁体的示例结果，该模型包含 \(L \times L\) 个粒子。Binder 累积量还被用于模拟许多其他系统，如无序材料、气体、优化问题、液体以及描述社会系统的图。

**获取源代码**

- 目录：randomness
- 文件：`binder_L8.dat`, `binder_L10.dat`, `binder_L16.dat`, `binder_L30.dat`

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_314_0.png)

图 8.21 二维模型铁磁体的 Binder 累积量随温度 \(T\)（无量纲单位）变化的曲线图。每个系统由 \(L \times L\) 个粒子组成。不同系统尺寸 \(L\) 的曲线在非常接近相变温度 \(T_c = 2.269\)（由该模型的解析计算得知）处交叉。所示的误差棒可以通过 bootstrap 方法获得。

使用标准误差分析来获得 Binder 累积量的置信区间非常困难（甚至不可能）。而使用 bootstrap 则很直接。你只需使用上面展示的 `bootstrap_variance()` 函数，并传入一个对给定数据点集评估 Binder 累积量的函数作为参数即可。

到目前为止，我们假设使用经验分布函数 \(F_X\) 来确定 \(F_H\) 的近似。或者，可以使用某些可能可用的额外知识。或者，可以通过使用由参数向量 \(\Delta\) 参数化的分布函数 \(F_\Delta\) 来做出额外假设。对于指数分布，该向量只由一个参数组成，即期望值；而对于高斯分布，\(\Delta\) 将由期望值和方差组成。原则上，可以存在任意复杂的、具有多个参数的分布。

为了使 \(F_\Delta\) 成为 \(F_X\) 的“良好”近似，必须调整参数，使分布函数“最好地”表示样本 \(\{x_i\}\)，从而得到参数向量 \(\hat{\Delta}\)。执行这种参数拟合的方法和工具将在第 8.6.2 节中介绍。使用 \(F_\Delta\) 可以像上面那样进行：要么基于 \(F_\Delta\) 精确计算 \(F_H\)，但大多数时候过于繁琐。相反，通常执行模拟，通过模拟 \(F_\Delta\) 反复抽取样本 \(\{\tilde{x}_0, \tilde{x}_1, \ldots, \tilde{x}_{n-1}\}\)，并每次计算估计量 \(\hat{h} = h(\tilde{x}_0, \tilde{x}_1, \ldots, \tilde{x}_{n-1})\)。与上面讨论的经验 bootstrap 情况一样，这会产生样本分布函数 \(F_{H^*}\)，并对其做进一步分析。这种使用 \(F_\Delta\) 代替 \(F_X\) 的方法称为参数 bootstrap（parametric bootstrap）。

请注意，bootstrap 方法确实要求样本点彼此统计独立。例如，数据可以通过马尔可夫链蒙特卡洛模拟生成 [Newman and Barkema (1999); Landau and Binder (2000); Robert and Casella (2004); Liu (2008)]，其中每个数据点 \(x_{i+1}\) 通过某个随机过程计算，但也依赖于前一个数据点 \(x_i\)。关于如何量化相关性的更多细节见第 8.5 节。例如，置信区间将取决于“独立”数据点的比例。这很容易理解：假设你把原始样本 \(\{x_i\}\) 中的每个数据点替换为 10 份副本，从而使样本增大 10 倍，但没有添加任何信息。这会影响后续的 bootstrap 计算，因为 bootstrap 样本的波动会减小。例如，假设你的原始样本只有两个独立样本点 \(x_1 \ne x_2\)。因此，bootstrap 样本可能包含两次 \(x_1\) 或两次 \(x_2\)，或者各一次。因此，bootstrap 平均值会强烈波动。另一方面，如果样本中有 10 个数据点 \(x_1\) 和 10 个数据点 \(x_2\)，那么 bootstrap 样本大多数时候会包含大约 10 个 \(x_1\) 和大约 10 个 \(x_2\)，只有在极少数情况下才会只看到（即 20 次）值 \(x_2\)。因此，bootstrap 均值的波动会较小。在这方面，bootstrap 与第 8.3.2 节中解释的经典置信区间计算类似，后者同样假设数据独立，并且独立数据点的数量会进入像式 (8.62) 这样的公式中。因此，为了对此进行修正，可以将获得的 bootstrap 误差棒乘以因子 \(\sqrt{\lambda_c}\)，其中 \(\lambda_c\) 是顺序相关样本点的典型数量。

应该提到的是，bootstrap 只是几种重采样技术之一。另一种著名的方法是 jackknife（刀切法）方法，它不使用 \(F_X\) 或拟合的 \(F_\Delta\) 进行随机采样。相反，

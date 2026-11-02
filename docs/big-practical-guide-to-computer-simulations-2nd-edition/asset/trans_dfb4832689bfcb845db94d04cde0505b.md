

考虑对数似然函数

$l(\hat{\theta}) \equiv \log L(\hat{\theta}).$

(8.94)

这将单个数据点的 pmf 或 pdf 的乘积转化为求和，从而使导数更容易求得。此外，由于对数函数是单调函数，似然函数的最大值点与对数似然函数的最大值点相同。因此，在最大似然方法中，通过以下方程组确定“最适合”的参数：

$$\frac{\partial l(\theta)}{\partial \theta_k} \stackrel{!}{=} 0 \quad (k = 1,\dots,n_p)$$ (8.95)

注意，一阶导数为零这一事实仅保证得到极值点。此外，这些方程通常有多个解。因此，必须明确检查哪些解确实是极大值，以及其中哪个是最大的极大值。注意，最大似然估计量是样本的函数，因此也是随机变量 $\mathrm{ML}_{\theta,n}(X_0,\dots,X_{n-1})$。

作为简单示例，我们考虑指数分布，其 pdf 由式 (8.39) 给出。它有一个参数 $\mu$。在样本 $\{x_0,x_1,\dots,x_{n-1}\}$ 的情况下，对数似然函数为

$$l(\mu) = \log \prod_{i=0}^{n-1} f_\mu(x_i)$$
$$= \sum_{i=0}^{n-1} \log \left\{\frac{1}{\mu} \exp\left(-\frac{x_i}{\mu}\right)\right\}$$
$$= \sum_{i=0}^{n-1} \left(\log\left\{\frac{1}{\mu}\right\} - \frac{x_i}{\mu}\right)$$
$$= n \log\left\{\frac{1}{\mu}\right\} - \frac{n \bar{x}}{\mu}$$

对 $\mu$ 求导，我们得到：
$$0 \stackrel{!}{=} \frac{\partial L(\theta)}{\partial \mu} = n \frac{1}{\mu^2} \mu - \frac{n}{\mu^2} \bar{x} = \frac{-n}{\mu^2}(\mu - \bar{x})$$
这意味着 $\mu = \bar{x}$。容易验证这对应一个极大值。由于指数分布的期望值正是 $\mathrm{E}[X] = \mu$，这与 8.3 节的结果一致，那里证明了样本均值是期望值的无偏估计量。

如果将最大似然原理应用于参数为 $\mu$ 和 $\sigma^2$ 的高斯分布，则得到的最大似然估计量分别为样本均值 $\bar{x}$（对应 $\mu$）和样本方差 $s^2$（对应 $\sigma^2$）（此处不推导，例如参见 [Dekking 等人 (2005)]）。这意味着（见式 (8.58)）$\sigma^2$ 的最大似然估计量是有偏的。幸运的是，我们知道当 $n \to \infty$ 时偏差会渐近消失。事实上，在关于底层分布的相当温和的条件下，可以证明参数 $\theta_k$ 的所有最大似然估计量 $ML_{\theta_k,n}(X_0,...,X_{n-1})$ 都是渐近无偏的，即

$$\lim_{n\to\infty} E[ML_{\theta_k,n}] = \theta_k \tag{8.96}$$

与指数分布和高斯分布的情形不同，在许多应用中，最大似然参数与标准样本估计量之间没有直接关系。此外，$ML_{\theta_k,n}$ 通常甚至无法解析确定。在这种情况下，必须数值优化对数似然函数，例如使用 GNU 科学库（GSL）中的相应方法（见 7.3 节）。

| 项目 |
|------|
| 获取源代码 |
| 目录：randomness |
| 文件：max_likely.c |

作为示例，我们考虑 Fisher-Tippett 分布，见式 (8.43)，将其平移以使最大值出现在 $x_0$ 处而不是 0 处。因此，我们需要调整两个参数 $\lambda$ 和 $x_0$。在使用 GSL 的最小化函数时，待优化函数（目标函数），即这里的对数似然函数，必须采用特殊格式。目标函数的第一个参数包含待调整的 pdf 参数，即目标函数的主参数向量。该参数必须是 `gsl_vector` 类型，这是 GSL 的向量类型。要使用此数据类型，需要包含 `<gsl_vector.h>`。这些向量通过 `gsl_vector_alloc()` 创建，通过 `gsl_vector_set()` 设置元素，通过 `gsl_vector_get()` 访问元素，并通过 `gsl_vector_free()` 释放。这些函数的用法从下面的示例中应当不言自明，但您也可以参阅 GSL 文档 [Galassi 等人 (2006)]。

目标函数的第二个参数包含一个指针，指向计算目标函数所需的全部附加数据，在本例中即样本。因此，样本必须存储在一段连续内存中。为此，我们使用以下结构体类型：

```
typedef struct
{
    int n;      /* number of sample points; */
    double *x;  /* sample */
}
sample_t;
```

由于 GSL 包实际提供的是最小化函数，而我们需要的是最大值，因此实际的对数似然函数返回的是负的对数似然。对数似然函数如下所示：

```
double ll_ft(const gsl_vector *par, void *param)
{
    double lambda, x0;                  /* parameters of pdf */
    sample_t *sample;                   /* sample */
    double sum;     /* sum of log-likelihood contributions */
    int i;          /* loop counter */

    lambda = gsl_vector_get(par, 0);            /* get data */
    x0 = gsl_vector_get(par, 1);
    sample = (sample_t *) param;

    sum = sample->n*log(lambda);        /* calculate log likelihood */
    for(i=0; i<sample->n; i++)
        sum -= lambda*(sample->x[i]-x0) +
               exp(-lambda*(sample->x[i]-x0));

    return(-sum);                       /* return - log likelihood */
}
```

首先，我们将作为参数传入的指针转换为我们认为便于使用的数据格式（第 8-10 行）。接下来，实际的对数似然

$l(\lambda, x_0) = n \log \lambda - \lambda \sum_{i=0}^{n-1} (x_i - x_0) - \sum_{i=0}^{n-1} \exp(-\lambda(x_i - x_0))$

在第 12-15 行中计算，最后以相反的符号返回（第 17 行）。

GSL 内置了多种最小化算法。它们都被归入两种框架之一。一种框架适用于需要目标函数及其一阶导数的算法；另一种框架则只需目标函数即可。这里我们使用单纯形算法，它属于后一种形式。它通过构造一个单纯形，²¹ 在单纯形的顶点处评估目标函数

21 单纯形是由 n+1 个顶点在 n 维空间中生成的凸集。

然后调用 gsl_multimin_fminimizer_set()，同时传入目标函数、起始点 par 和（初始）单纯形大小。²² sample.x[] 数组必须填入实际样本（此处未显示）。

最小化循环如下所示：

```
do
{
    /* perform minimization */
    iter++;
    status = gsl_multimin_fminimizer_iterate(s);  /* one step */
    if(status)  /* error ? */
        break;
    size = gsl_multimin_fminimizer_size(s);   /* converged ? */
    status = gsl_multimin_test_size(size, 1e-4);
}
while( (status == GSL_CONTINUE) && (iter<100) );
```

主要工作由 gsl_multimin_fminimizer_iterate() 完成。然后检查是否发生错误。接下来，计算单纯形的大小，最后检验该大小是否低于某个限值，本例中为 10⁻⁴。

参数的实际估计值可通过 gsl_vector_get(s->x, 0) 和 gsl_vector_get(s->x, 1) 获得。注意，最后应释放所有已分配的内存：

```
gsl_vector_free(par);                 /* free everything */
gsl_vector_free(simplex_size);
gsl_multimin_fminimizer_free(s);
free(sample.x);
```

作为示例，根据参数 λ = 3.0、x₀ = 2.0 的 Fisher-Tippett 分布生成了 n = 10000 个数据点。使用上述起始参数，最小化在 39 次迭代后收敛到 λ̂ = 2.995 和 x̂₀ = 2.003。

## 8.6.2 数据拟合

在上一节中，选择概率分布的参数，使分布能最好地描述数据。这里，我们考虑一个更一般的情形，称为数据建模。如上所述，这里给定一个三元组样本 $\{(x_0, y_0, \sigma_0), (x_1, y_1, \sigma_1), \dots, (x_{n-1}, y_{n-1}, \sigma_{n-1})\}$。通常，$y_i$ 是在模拟中获得的测量值，模拟时将某个控制参数（例如温度）固定在不同的值 $x_i$ 上；$\sigma_i$ 是 $y_i$ 的相应误差棒。这里，我们希望确定参数 $\underline{\theta} = (\theta_1, \dots, \theta_{n_p})$，使得给定的参数化函数 $y_{\underline{\theta}}(x)$ 能“最好”地拟合数据，即所谓将函数拟合到数据。与拟合 pmf 或 pdf 的情况类似，对于“最好”没有通用的原则。

我们假设 $y_i$ 是随机变量，也就是说，比较不同的模拟。因此，测量值围绕其“真实”值 $y_{\underline{\theta}}(x_i)$ 散布。这种散布可以近似地用均值为 $y_{\underline{\theta}}(x_i)$、方差为 $\sigma_i^2$ 的高斯分布来描述：

$$q_{\underline{\theta}}(y_i) \sim \exp\left(-\frac{(y_i - y_{\underline{\theta}}(x_i))^2}{2\sigma_i^2}\right). \tag{8.97}$$

这一假设通常成立，例如当每个样本点 $y_i$ 本身是在控制参数值 $x_i$ 下进行模拟所得的样本均值，且 $\sigma_i$ 是相应的误差棒时。完整数据样本的对数似然函数为

$$l(\underline{\theta}) = \log \prod_{i=0}^{n-1} q_{\underline{\theta}}(y_i)$$
$$
\sim -\sum_{i=0}^{n-1} \frac{1}{2}\left(\frac{y_i - y_{\underline{\theta}}(x_i)}{\sigma_i}\right)^2$$

最大化 $l(\underline{\theta})$ 等价于最小化 $-2l(\underline{\theta})$，因此需要最小化均方差异

$$\chi^2_{\underline{\theta}} = \sum_{i=0}^{n-1} \left(\frac{y_i - y_{\underline{\theta}}(x_i)}{\sigma_i}\right)^2 \tag{8.98}$$

这意味着参数 $\underline{\theta}$ 的确定使得函数 $y_{\underline{\theta}}(x)$ 尽可能近地跟随数据点 $\{(x_0, y_0), \dots, (x_{n-1}, y_{n-1})\}$，其中偏差以误差棒 $\sigma_i$ 来衡量。因此，误差棒较小的数据点具有更大的权重。整个过程称为最小二乘拟合。

最小化后的均方差异是一个随机变量。注意，各项之间并不统计独立，因为它们通过 $n_p$ 个参数 $\underline{\theta}$ 相关联，而这些参数是通过最小化 $\chi^2_{\underline{\theta}}$ 确定的。作为


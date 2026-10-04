
is.sample.wge(data, lambda, offset, phi) 基于 Parzen 窗口根据对偶过程的谱估计计算并绘制瞬时谱。

lambda 是 $G(\lambda; p)$ 模型中 $\lambda$ 的值（默认 lambda = 0，即 M-平稳模型）。

offset 是偏移量参数（参见关于图 13.2 的讨论，默认 = 60）。

示例：使用以下命令，根据从图 13.2c（以及图 13.4a）中的数据获得的图 13.4b 中的对偶数据进行周期图拟合，计算瞬时谱：

```
data(fig13.2)
is.sample.wge(fig13.2c, lambda = -0.4, offset = 63)
```

与图 13.8c 所示基于 AR 的瞬时谱进行比较。

## 13B1 生成图 13.19e 和 f 的滤波步骤

```
data(fig13.18a)
# 我们将使用真实值 (lambda = 0 且 offset = 175)
dual=trans.to.dual.wge(fig13.18a, lambda = 0, offset = 175)
plot=FALSE
y1=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
y2=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
```

## 练习题

13.1 使用 twsg 函数 gen.lambda.wge 从 Euler(4) 模型创建一个长度为 $n = 256$ 的实现：

```
X(h^k)-1.75X(h^{k-1})+1.95X(h^{k-2})-1.70X(h^{k-3})+0.95(h^{k-4})=a(h^k),
```

偏移量为 60。

- a. 对偶数据应该包含哪些系统频率？
- b. 使用函数 est.lambda.wge 并指定 $\lambda = 0$，对生成的数据拟合 Euler 模型。选择 0:200 作为偏移范围，12 作为最大 AR 阶数。
- c. 使用程序打印的输出，显示并讨论以下图表：
    - i. 数据
    - ii. 对偶过程
    ## G-平稳过程
    - iii. 原始数据和对偶数据的谱密度估计。可以使用 Parzen 谱估计器（使用 parzen.wge）或 AR 谱估计器（使用 true.arma.spec.wge）来获得。是否有证据表明预期的系统频率（来自 (a)）存在于对偶数据中？
    - iv. Euler 模型与拟合原始数据的 AR 模型之间的预测性能的对比（使用 fore.glambda.wge）。
    - v. 使用 is.glambda.wge 估计的瞬时谱。
- d. 计算并绘制 Wigner-Ville 谱（使用 vw.wge），并与 (c) 部分 (v) 中的瞬时谱进行比较。

13.2 tswge 数据集 prob1.2 包含一个 M-平稳余弦加噪声过程的长度为 $n = 256$ 的实现：

$X(t) = 5 \cos[2\pi\ln(t+50) + \psi] + a(t),$

其中 $y=1$，且 $\sigma_y^2=1$。

- a. 拟合一个 Euler 模型（即 $\lambda=0$ 的 $G(\lambda)$ 模型）。选择 200 作为偏移范围，12 作为最大 AR 阶数。
- b. 使用程序打印的输出，显示并讨论问题 13.1(c) 中列出的项目。

13.3 重新运行问题 13.1 中的分析，从 $G(4; 2)$ 模型生成长度为 $n=256$ 的实现，其对偶为：

$X_t = -1.75X_{t-1} + 1.95X_{t-2} - 1.70X_{t-3} + 0.95X_{t-4} = a_t$，

偏移量为 60。讨论 Euler($\rho$) 模型和 $G(\rho; 2)$ 模型之间的时变频率（TVF）行为差异。对数据拟合一个 $G(\lambda; \lambda)$。这涉及两个步骤：

- a. 识别一个 $G(\rho; \lambda)$
- b. 使用 (a) 中得到的偏移量和 $\lambda$ 对数据拟合 $G(\rho; \lambda)$。

这两个步骤的完成如下：

- a. 在 est.glambda.wge 中让 $\lambda$ 的范围为 1:3（包含真实值 2），让 offset 范围为 0:100。
- b. 对数据拟合 $G(\rho; \lambda)$（即通过基于 (a) 部分中的 $\lambda$ 和偏移量的时间变换创建的对偶数据拟合 AR 模型）。
- c. 使用程序打印的输出，显示并讨论问题 13.1(c) 中列出的项目。

13.4 使用问题 13.3 中的步骤 (a–c)（使用 $\lambda$ 范围 1:3 和偏移量范围 0:100），对以下 `tswave` 数据集拟合 $G(p; \lambda)$ 模型：

- a. doppler——一个多普勒信号
- b. prob12.6c—一个模拟数据集
- c. noctula——回声定位信号

## 参考文献

Akaike, H. 1969. Fitting autoregressive models for regression, Annals of the Institute of Statistical Mathematics 21, 243–247.

Akaike, H. 1973. Information theory and an extension of the maximum likelihood principle. In 2nd International Symposium on Information Theory, Petrov, B.N. and Csaki, F. (eds.), Akademia Kiado. Budapest. 267–281.

Akaike, H. 1976. Canonical correlations analysis of time series and the use of an information criterion. In Advances and Case Studies in System Identification, Mehra, R. and Lainiotis, D.G. (eds.), Academic Press: London. 365–381.

Alder, A. 1952. On the properties of certain tests, Journal of the Royal Statistical Society 15, 63–71.

Andel, C. 1979. Asymptotic theory of certain “goodness-of-fit” criteria, Biometrika 66, 19–212.

Ansley, C. 1980. A survey of work in time series, Journal of Statistics 7, 55–58.

Bartlett, M. 1946. On the theory of filter coefficients, Journal of the Royal Statistical Society 7, 536–541.

Box, C.F. 1952. A maximum likelihood procedure for regression with correlated errors, The Review of Economics and Statistics, Academic Press: London.

Box, G.E. 1970. Detection of autocorrelations in time series, Journal of American Statistics 140, 211–252.

Box, G.E. and Jenkins, G.M. 1978. Time Series: Analysis and Forecasting, Wiley: New York.

Box, G.E. and Pierce, D.A. 1902. Introduction to Time Series, 3rd edn, Wiley: New York.

Burg, J.P. 1995. Maximum entropy spectral analysis, PhD dissertation, Department of Geophysics, Stanford University.

Butter, S. 1930. On the Yule-Walker equations of an autoregressive moving average process, IEEE Transactions on Information Theory 32, 417–419.

Campbell, M.J. and Walker, A.M. 1977. A survey of work in time series, Journal of the Royal Statistical Society 15, 63–71.

Chung, C.F. 1996a. Estimating a generalized long memory process, Journal of Econometrics 73, 237–259.

Chui, C.K. 1992. An Introduction to Wavelets, Vol. 1, Academic Press: San Diego, CA.

Casella, G. and Berger, R.L. 2001. Statistical Inference, 2nd edn, Dublin Press: Belmont, CA.

Chan, W.S. 1994. On portmante goodness-of-fits in robust time series modeling, Computational Statistics 9, 301–310.

Cheng, Q.C. 1993. Transfer function model and GARMA II, PhD dissertation, Department of Statistical Science, Southern Methodist University: Dallas.

Cheng, Q.S. 1999. On time-reversibility of linear processes, Biometrika 86, 483–488.

Cho, I. 1986. An algorithm for solving the Yule-Walker equations of an autoregressive moving average time series, IEEE Transactions on Information Theory 32, 417–419.

Cho, E., Woodward, W.A., and Gray, H.L. 2006. Euler (p,q) processes and their application to noncommutative time series with time-varying frequencies, Communications in Statistics 35, 2245–2262.



g. is.sample.wge(data,lambda,offset,phi) 计算并绘制基于对偶的谱估计使用 Parzen 窗口的瞬时谱。

lambda 是 G(λ; p) 模型中 λ 的值（默认 lambda = 0，即 M-平稳模型）

offset 是偏移参数（参见例如关于图 13.2 的讨论，默认 = 60）

示例：要基于对偶数据在图 13.4b 中对图 13.2c 中的数据（以及图 13.4a）进行周期拟合计算瞬时谱，使用以下命令：

```
data(fig13.2)
is.sample.wge(fig13.2c, lambda = -0.4, offset = 63)
```

与图 13.8c 中所示的基于 AR 的瞬时谱进行比较。

## 13B1 产生图 13.19e 和 f 的滤波步骤

```
data(fig13.18a)
#we will use true values (lambda = 0 and offset = 175)
dual=trans.to.dual.wge(fig13.18a, lambda = 0, offset = 175)
plot=FALSE
l1=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
l2=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
```

## EXERCISES

13.1 使用 twsg 函数 gen.lambda.wge 从 Euler(4) 模型生成长度 n = 256 的实现

```
X(h^k)-1.75X(h^{k-1})+1.95X(h^{k-2})-1.70X(h^{k-3})+0.95(h^{k-4})=a(h^k),
```

偏移为 60。

- a. 对偶数据应包含哪些系统频率？
- b. 通过使用函数 est.lambda.wge 并指定 λ = 0 来拟合生成数据的 Euler 模型。选择 0:200 作为偏移范围和 12 作为最大 AR 阶数。
- c. 使用程序打印的输出，显示并讨论以下图的
- i. 数据
- ii. 对偶
- iii. 原始数据和对偶数据的谱密度估计。可以使用 Parzen 谱估计器（使用 parzen.wge）或 AR 谱估计器（使用 true.arma.spec.wge）获得。是否有证据表明预期系统频率（来自 (a)）存在于对偶数据中？
- iv. Euler 模型与拟合到原始数据的 AR 模型的预测性能（使用 fore.glambda.wge）。
- v. 使用 is.glambda.wge 估计的瞬时谱

d. 计算并绘制 Wigner-Ville 谱（使用 vw.wge）并将其与 (c) 部分 (v) 中的瞬时谱进行比较

13.2 tswge 数据集 prob1.2 包含长度 n = 256 的 M-平稳余弦加噪声过程的实现

> $X(t) = 5 \cos[2\pi\ln(t+50) + \psi] + a(t),$

其中 $y=1$，并且 $\sigma_y^2=1$。

- a. 拟合 Euler 模型（即 λ=0 的 $G(\lambda)$ 模型）。选择 200 作为偏移范围和 12 作为最大 AR 阶数。
b. 使用程序打印的输出，显示并讨论问题 13.1(c) 中列出的图的项目。

13.3 通过从 $G(4; 2)$ 模型生成长度 $n=256$ 的实现，重新运行问题 13.1 中的分析，其对偶为

> $X_t = -1.75X_{t-1} + 1.95X_{t-2} - 1.70X_{t-3} + 0.95X_{t-4} = a_t$,

偏移为 60。讨论 Euler($\rho$) 模型与 $G(\rho; 2)$ 模型的 TVF 行为之间的差异。
拟合 $G(\lambda; \lambda)$ 到数据。这涉及两个步骤：

- a. 识别 $G(\rho; \lambda)$
b. 使用在 (a) 中获得的偏移和 λ 拟合 $G(\rho; \lambda)$ 到数据。

这两个步骤如下完成：

- a. 在 est.glambda.wge 中让 λ 从 1:3 变化（以包含真实值 2）并且让 offset 变化 0:100。
b. 拟合 $G(\rho; \lambda)$ 到数据（即通过对基于 λ 和 offset 在部分 (a) 中创建的对偶数据进行时间变换拟合 AR 模型）。

- c. 使用程序打印的输出，显示并讨论问题 13.1(c) 中列出的图的项目。

## G-Stationary Processes

13.4 使用问题 13.3 中的步骤 (a–c)（使用 λ 范围 1:3 和 offset 范围 0:100）拟合以下 `tswave` 数据集的 $G(p; \lambda)$ 模型：

- a. doppler——多普勒信号
- b. prob12.6c——模拟数据集
- c. noctula——回声定位信号

## References

Akaike, H. 1969. Fitting autoregressive models for regression, Annals of the Institute of Statistical Mathematics 21, 243–247.

Akaike, H. 1973. Information theory and an extension of the maximum likelihood principle. In 2nd International Symposium on Information Theory, Petrov, B.N. and Csaki, F. (eds.), Akademia Kiado. Budapest, 267–281.

Akaike, H. 1976. Canonical correlations analysis of time series and the use of an information criterion. In Advances and Case Studies in System Identification, Mehra, R. and Lainiotis, D.G. (eds), Academic Press: New York 27–96.

Alder, A.C., Fry, T.B., Woodward, W.A., Haley, R.W., Sarosi, G., and Livingston, E.H. 2010. Association of viral infection and appendicitis, Archives of Surgery 145, 63–71.

Andel, J. Anderson, T. and Darling, D.A. 1952. Asymptotic theory of certain “goodness-of-fit” criteria based on stochastic processes, Annals of Mathematical Statistics 23, 193–212.

Ansley, C.F. 1979. An algorithm for the exact likelihood of a mixed autoregressivemoving average process, Biometrika 66, 59–65.

Bao, W. 2014. Analysis of time series with time-frequency behavior and long memory, PhD Dissertation, Department of Statistical Science, Southern Methodist University: Dallas, TX.

Bartlett, M.S. 1946. On the theoretical expectations and sampling properties of correlated time series, Journal of the Royal Statistical Society B8, 24–41.

Beach, C.M. and Mackinnon, J.G. 1978. A maximum likelihood procedure for regression with correlated errors, Econometrica 46, 51–58.

Beguin, J.M., Gourieux, C., and Montfort, A. 1980. Identification of a mixed-autoregressive-moving average process: The method. In Time Series, Anderson, O.D. (ed.), North-Holland: Amsterdam, the Netherlands, 423–436.

Bera, A.K. and Higgins, M.L. 1993. ARCH models: Properties, estimation and testing, Journal of Economic Statistics 7, 307–366.

Beran, J. 1994. For Long-Memory Processes, Chapman & Hall: New York.

Bansali, R.Y. 1979. A mixed spectrum analysis of the lynx data, Journal of the Royal Society A142, 199–209.

Billingsley, P. 1995. Probability and Measure, 3rd edn., Wiley & Sons: New York.

Bloomfield, P. and Nychka, D.W. 1992. Climate spectra and detecting climate change, Climate Change 21, 275–287.

Boashash, B. 1992a. Estimating and interpreting the instantaneous frequency—Part 1: Fundamentals, Proceedings of the IEEE 80, 520–538.

Boashash, B. 1992b. Estimating and interpreting the instantaneous frequency–Part 2: Algorithms and applications, Proceedings of the IEEE 80, 540–568.

Boashash, B. 2003. Time Frequency Analysis, Elsevier: Oxford, UK.

Bollerslev, T. 1986. Generalized autoregressive conditional heteroskedasticity, Journal of Econometrics 31, 307–327.

## 596

## References

Box, G.E.P. and Cox, D. 1964. An analysis of transformations, Journal of the Royal Statistical Society, B 26, 211–252.

Box, G.E.P., Jenkins, G.M., and Reinsel, C.G. 2008. Time Series Analysis: Forecasting and Control, Wiley: Hoboken, NJ.

Box, G.E.P. and Pierce, D.A. 1970. Distribution of the autocorrelations in autoregressive moving average time series models, Journal of American Statistical Association 65, 1509–1526.

Bremaker, M., Brammer, M., Bullmore, E., Das, P., and Williams, L. 2004. Spatio-temporal wavelet resampling for functional neuroimaging data, Human Brain Mapping 23, 1–25.

Brillinger, D.R. 1989. Consistent detection of a monotonic trend superposed on a stationary time series, Biometrika 76, 23–30.

Brockwell, P.J. and Davis, R.A. 1991. Time Series: Theory and Methods, 2nd edn., Springer-Verlag: New York.

Brockwell, P.J. and Davis, R.A. 2002. Introduction to Time Series and Forecasting, 2nd edn., Springer-Verlag: New York.

Bruce, A. and Gao, H. 1996. Applied Wavelet Analysis with S+, Springer-Verlag: New York.

Bullmore, E., Long, C., Suckling, J., Fadili, J., Calvert, G., Zelaya, F., Carpenter, T., and Bammer. 2001. Colored noise and computational inference in physiological time series analysis: Resampling methods in time and wavelet domains, Human Brain Mapping 12, 61–78.

Burg, J.P. 1995. Maximum entropy spectral analysis, PhD dissertation, Department of Geophysics, Stanford University: Stanford, CA.

Butterworth, S. 1930. On the theory of filter coefficients, Experimental Wireless and the Wireless Engineer 7, 536–541.

Campbell, M.J. and Walker, A.M. 1977. A survey of statistical work in the Mackenzie river systems. II Annual Canadian lynx foray for the years 1821–1924 and a new analysis. Journal of the Royal Statistical Society A140, 411–443.

Caner, E. and Watson, M.W. 1997. Estimating deterministic trends in the presence of correlated errors, The Review of Economics and Statistics 79, 184–200.

Carmona, R., Huang, W., and Torrésani, B. 1998. Practical Time-Frequency Analysis, Academic Press: San Diego, CA.

Casella, G. and Berger, R.L. 2001. Statistical Inference, 2nd edn, Duxbury Press: Belmont, CA.

Chan, W.S. 1994. On portmanteau goodness-of-fits in robust time series modeling, Computational Statistics 9, 301–310.

Cheng, Q.C. 1993. Transfer function model and GARMA II model, PhD dissertation, Department of Statistical Science, Southern Methodist University: Dallas, TX.

Cheng, Q.S. 1999. On time-reversibility of linear processes, Biometrika 86, 483–488.

Cho, I. 1986. An algorithm for solving the Yule-Walker equations of an autoregressive moving average time series, IEEE Transactions on Information Theory 32, 417–419.

Cho, E., Woodward, W.A., and Gray, H.L. 2006. Euler (p,q) processes and their application to noncommutative time series with time-varying frequencies, Communications in Statistics A 35, 2245–2262.

Chui, C.K. 1992. An Introduction to Wavelets, Vol. 1, Academic Press: San Diego, CA.

Chung, C.F. 1996a. Estimating a generalized long memory process, Journal of Econometrics 73, 237–259.


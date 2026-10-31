

ld = butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .075)
lo = trans.to.original.wge(ld$x.filt, offset = 175, h = dual$h, lambda = 0)

（注意：ld 是图13.19d中所示的低通滤波后的对偶数据，lo 是图13.19e中所示原始时间尺度下的TVF滤波数据。另请注意，dual$h 是调用 trans.to.dual 时输出的结果。）

- **fore.glambda.wge (x, lambda, offset, n.ahead, lastn, plot)**

  该函数使用第13.3.3节讨论并在例13.7中进一步说明的3步方法预测未来 n.ahead 步。您可以选择计算并绘制序列末尾之后 n.ahead 步的预测，也可以预测序列中最后 n.ahead 个数据值。为便于比较，还会绘制AR预测图。

  - x：实现（realization）
  - lambda：G(λ; p) 模型中 λ 的值（默认为 lambda = 0，即 M-平稳模型）
  - offset：偏移参数（参见例如图13.2的讨论）（默认 = 60）
  - phi：拟合对偶数据的AR模型的AR参数向量（默认为 phi = 0）
  - n.ahead：想要预测的前向步数（默认 = 2）
  - lastn：逻辑变量。如果 lastn = FALSE（默认），则预测为 x(n + 1), x(n + 2), ..., x(n + n.ahead)，其中 n 是实现（realization）的长度。如果 lastn = TRUE，则程序预测实现中的最后 n.ahead 个值。（默认 = FALSE）。同时绘制AR预测以供比较。
  - plot：逻辑变量。如果 plot = TRUE（默认），则预测将与实现一起绘制。如果 plot = FALSE，则不输出图。（默认 = TRUE）

  示例：要计算并绘制图13.8b中所示的预测，请使用以下命令：

  ```
  data(fig13.2c)
  dual.data = trans.to.dual.wge(fig13.2c, lambda = -.4, offset = 63)
  aic5.wge(dual.data, p = 0:12, type = 'bic')
  # BIC 选择 p = 5
  ardual = est.ar.wge(dual.data, p = 5)
  example = fore.glambda.wge(fig13.2c, lambda = -.1, offset = 38, phi = ardual$phi, n.ahead = 60, lastn = TRUE)
  ```

  注意：对偶数据是通过使用例13.7中找到的 λ 和 offset 进行变换得到的。另请参见上面 est.glambda.wge 的示例。

- **is.glambda.wge (n, lambda, offset, phi)** 基于拟合对偶数据的AR模型以及用于创建对偶数据集的 lambda 和 offset，计算并绘制瞬时频谱。

  - n：原始数据集的长度
  - lambda：G(λ; p) 模型中 λ 的值（默认为 lambda = 0，即 M-平稳模型）
  - offset：偏移参数（参见例如图13.2的讨论）（默认 = 60）
  - phi：拟合对偶数据的AR模型的AR参数向量（默认为 phi = 0）

  示例：要计算图13.8c中所示的瞬时频谱，请使用以下命令：

  ```
  is.glambda.wge(n = 200, lambda = -0.4, offset = 63, phi = c(.93, -.32, -.15, -.15, -.17))
  ```

  注意：phi 系数是通过对偶数据集拟合AR(5)模型获得的ML估计。请参见上文 (c) 中的示例。

- **is.sample.wge (data, lambda, offset, phi)** 基于使用 Parzen 窗对对偶数据进行频谱估计，计算并绘制瞬时频谱。

  - lambda：G(λ; p) 模型中 λ 的值（默认为 lambda = 0，即 M-平稳模型）
  - offset：偏移参数（参见例如图13.2的讨论）（默认 = 60）

  示例：要基于图13.4b中对偶数据的周期图拟合（该数据源自图13.2c（以及图13.4a）中的数据）计算瞬时频谱，请使用以下命令：

  ```
  data(fig13.2c)
  is.sample.wge(fig13.2c, lambda = -0.4, offset = 63)
  ```

  将其与图13.8c中基于AR的瞬时频谱进行比较。

### 13B.1 生成图13.19e和图13.19f的滤波步骤

```
data(fig13.18a)
# 我们将使用真实值（lambda = 0 和 offset = 175）
dual = trans.to.dual.wge(fig13.18a, lambda = 0, offset = 175, plot = FALSE)
l1 = butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
l2 = butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
```

## 习题

- **13.1** 使用 tswge 函数 gen.glambda.wge 从 Euler(4) 模型生成一个长度为 n = 256 的实现（realization）：

  X(t^k) - 1.75X(t^{k-1}) + 1.95X(t^{k-2}) - 1.70X(t^{k-3}) + 0.95X(t^{k-4}) = a(t^k)，

  偏移量为 60。

  - a. 对偶数据应包含哪些系统频率？
  - b. 使用函数 est.glambda.wge 并指定 λ = 0，将 Euler 模型拟合到生成的数据集。选择 0:200 作为偏移范围，12 作为最大AR阶数。
  - c. 使用程序打印的输出，展示并讨论以下图：
    - i. 数据
    - ii. 对偶数据
    - iii. 原始数据和对偶数据的频谱密度估计。这些可以使用 Parzen 频谱估计器（使用 parzen.wge）或 AR 频谱估计器（使用 true.arma.spec.wge）获得。是否有证据表明 (a) 中预期的系统频率存在于对偶数据中？
    - iv. Euler 模型与拟合原始数据的AR模型的预测性能比较（使用 fore.glambda.wge）
    - v. 使用 is.glambda.wge 估计的瞬时频谱
  - d. 计算并绘制 Wigner–Ville 频谱（使用 vw.wge），并将其与 (c) 第 (v) 部分的瞬时频谱进行比较

- **13.2** tswge 数据集 prob13.2 包含一个长度为 n = 256 的 M-平稳余弦加噪声过程的实现：

  X(t) = 5 cos[2π5 ln(t + 50) + ψ] + a(t)，

  其中 ψ = 1.2，σ_a² = 1。

  - a. 拟合一个 Euler 模型（即 λ = 0 的 G(λ) 模型）。选择 0:200 作为偏移范围，12 作为最大AR阶数。
  - b. 使用程序打印的输出，展示并讨论问题13.1(c)中列出各项的图。

- **13.3** 重新运行问题13.1中的分析，从 G(4; 2) 模型生成一个长度为 n = 256 的实现，其对偶模型为：

  X_t - 1.75X_{t-1} + 1.95X_{t-2} - 1.70X_{t-3} + 0.95X_{t-4} = a_t，

  偏移量为 60。讨论 Euler(p) 模型与 G(p; 2) 模型在 TVF 行为上的差异。

  将 G(p; λ) 模型拟合到数据。这包括两个步骤：
  - a. 确定 offset 和 λ。
  - b. 使用 (a) 中获得的 offset 和 λ，将 G(p; λ) 模型拟合到数据。

  这两个步骤的实现方式如下：
  - a. 在 est.glambda.wge 中，让 λ 在 1:3 范围内变化（以包含真实值 2），偏移范围设为 0:100。
  - b. 将 G(p; λ) 模型拟合到数据（即通过对基于 (a) 中获得的 λ 和 offset 进行时间变换创建的对偶数据拟合AR模型）。
  - c. 使用程序打印的输出，展示并讨论问题13.1(c)中列出各项的图。

- **13.4** 使用问题13.3中的步骤 (a–c)（λ 范围 1:3，偏移范围 0:100）将 G(p; λ) 模型拟合到以下 tswge 数据集：
  - a. doppler——多普勒信号
  - b. prob12.6c——一个模拟数据集
  - c. noctula——回声定位信号

## 参考文献

- Akaike, H. 1969. Fitting autoregressive models for regression, Annals of the Institute of Statistical Mathematics 21, 243–247.
- Akaike, H. 1973. Information theory and an extension of the maximum likelihood principle. In 2nd International Symposium on Information Theory, Petrov, B.N. and Csaki, F. (eds.), Akademiai Kiado: Budapest, 267–281.
- Akaike, H. 1976. Canonical correlations analysis of time series and the use of an information criterion. In Advances and Case Studies in System Identification, Mehra, R. and Lainiotis, D.G. (eds.), Academic Press: New York, 27–96.
- Alder, A.C., Fomby, T.B., Woodward, W.A., Haley, R.W., Sarosi, G., and Livingston, E.H. 2010. Association of viral infection and appendicitis, Archives of Surgery 145, 63–71.
- Andel, J. 1986. Long memory time series models, Kybernetika 22, 105–123.
- Anderson, T.W. and Darling, D.A. 1952. Asymptotic theory of certain “goodness-of-fit” criteria based on stochastic processes, Annals of Mathematical Statistics 23, 193–212.
- Ansley, C.F. 1979. An algorithm for the exact likelihood of a mixed autoregressive-moving average process, Biometrika 66, 59–65.
- Bao, W. 2014. Analysis of time series with time-varying frequency behavior and long memory, PhD Dissertation, Department of Statistical Science, Southern Methodist University: Dallas, TX.
- Bartlett, M.S. 1946. On the theoretical specification and sampling properties of autocorrelated time series, Journal of the Royal Statistical Society B8, 27–41.
- Beach, C.M. and MacKinnon, J.G. 1978. A maximum likelihood procedure for regression with autocorrelated errors, Econometrica 46, 51–58.
- Beguin, J.M., Gouriéroux, C., and Montfort, A. 1980. Identification of a mixed auto-regressive-moving average process: The corner method. In Time Series, Anderson, O.D. (ed.), North-Holland: Amsterdam, the Netherlands, 423–436.
- Bera, A.K. and Higgins, M.L. 1993. ARCH models: Properties, estimation and testing, Journal of Economic Surveys 7, 307–366.
- Beran, J. 1994. Statistics for Long-Memory Processes, Chapman & Hall: New York.
- Bhansali, R.J. 1979. A mixed spectrum analysis of the lynx data, Journal of the Royal Statistical Society A142, 199–209.
- Billingsley, P. 1995. Probability and Measure, 3rd edn., John Wiley & Sons: New York.
- Bloomfield, P. and Nychka, D.W. 1992. Climate spectra and detecting climate change, Climatic Change 21, 275–287.
- Boashash, B. 1992a. Estimating and interpreting the instantaneous frequency—Part 1: Fundamentals, Proceedings of the IEEE 80, 520–538.
- Boashash, B. 1992b. Estimating and interpreting the instantaneous frequency—Part 2: Algorithms and applications, Proceedings of the IEEE 80, 540–568.
- Boashash, B. 2003. Time Frequency Analysis, Elsevier: Oxford, U.K.
- Bollerslev, T. 1986. Generalized autoregressive conditional heteroskedasticity, Journal of Econometrics 31, 307–327.
- Box, G.E.P. and Cox, D.R. 1964. An analysis of transformations, Journal of the Royal Statistical Society, Series B 26, 211–252.
- Box, G.E.P., Jenkins, G.M., and Reinsel, G.C. 2008. Time Series Analysis: Forecasting and Control, Wiley: Hoboken, NJ.



$X_t = -1.75X_{t-1} + 1.95X_{t-2} - 1.70X_{t-3} + 0.95X_{t-4} = a_t$,

偏移为 60。讨论 Euler($\rho$) 模型与 $G(\rho; 2)$ 模型的 TVF 行为之间的差异。

拟合 $G(\lambda; \lambda)$ 到数据。这涉及两个步骤：

- a. 识别 $G(\rho; \lambda)$
- b. 使用在 (a) 中获得的偏移和 λ 拟合 $G(\rho; \lambda)$ 到数据。

这两个步骤如下完成：

- a. 在 `est.glambda.wge` 中让 λ 从 1:3 变化（以包含真实值 2）并且让 offset 变化 0:100。
- b. 拟合 $G(\rho; \lambda)$ 到数据（即通过对基于 λ 和 offset 在部分 (a) 中创建的对偶数据进行时间变换拟合 AR 模型）。
- c. 使用程序打印的输出，显示并讨论问题 13.1(c) 中列出的图的项目。

## G-Stationary Processes

13.4 使用问题 13.3 中的步骤 (a–c)（使用 λ 范围 1:3 和 offset 范围 0:100）拟合以下 `tswave` 数据集的 $G(p; \lambda)$ 模型：

- a. `doppler`——多普勒信号
- b. `prob12.6c`——模拟数据集
- c. `noctula`——回声定位信号

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

596

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

## 参考文献

Chung, C.F. 1996b. A generalized fractionally integrated autoregressive moving-process, Journal of Time Series Analysis 17, 111–140.

Chung, C.L. 2001. A Course in Probability Theory, Academic Press: San Diego, CA.

Cochrane, D. and Orcutt, G.H. 1949. Application of least squares to relationships with autocorrelated error terms, Journal of the American Statistical Association 44, 32–61.

Coifman, R. and Wickerhouse, V. 1992. Entropy-based algorithms for best basis selection, IEEE Transactions on Information Control 38, 713–718.

Cryer, J.D. and Chan, K.S. 2008. Time Series Analysis with Applications in R, 2nd ed., Springer-Verlag: New York.

Daubechies, I. 1988. Orthonormal bases of compactly supported wavelets, Communications in Pure and Applied Mathematics 41, 909–996.

Daubechies, I. 1992. Ten Lectures on Wavelets, Society for Industrial and Applied Mathematics, SIAM: Philadelphia, PA.

Havis, H.T. and Jones, R.H. 1968. Estimation of the innovation variance of a stationary series, Journal of the American Statistical Association 63, 141–149.

Dickey, D.A. 1976. Estimation and hypothesis testing in nonstationary time series, PhD Dissertation, Iowa State University: Ames, IA.

Dickey, D.A. and Fuller, W.A. 1979. Distribution of the estimators for autoregressive series with a unit root, Journal of the American Statistical Association 74, 427–431.



a, b, rho: -1.8787828,-5.8789232, 0.3055131
*Genz West                     : 1.003499500688108e-09
*Genz QuantLib 1.8             : 1.003499502515318e-09

*Drezner 1978 Quantlib 1.8  : 9.854280102848721e-10
*FDM approx                    : 1.001043599137774e-09
FDM approx extrap              : 1.00349809494e-09

a, b, rho: -0.32177054,-2.9262971, -0.46594091
*Genz West                     : 3.560500239620657e-05
*Genz QuantLib 1.8             : 3.560500239620712e-05

*Drezner 1978 Quantlib 1.8  : 3.555883404780285e-05
*FDM approx                    : 3.511401126791778e-05
FDM approx extrap              : 3.56043363362e-05

a, b, rho: 4.7155323,7.8416032, -0.69093606
*Genz West                     : 0.9999987946014995
*Genz QuantLib 1.8             : 0.9999987946014997

*Drezner 1978 Quantlib 1.8  : 0.9999987946014997
*FDM approx                    : 0.9999988671747321
FDM approx extrap              : 0.999998795263

a, b, rho: -1.946981,3.1876528, 0.054292586
*Genz West                     : 0.02575683532947779
*Genz QuantLib 1.8             : 0.02575683532947772

*Drezner 1978 Quantlib 1.8  : 0.0257568435454463
*FDM approx                    : 0.02568591162309218
FDM approx extrap              : 0.025756830355

a, b, rho: -4.7346574,3.0501621, 0.948175
*Genz West                     : 1.097127038323874e-06
*Genz QuantLib 1.8             : 1.097127038329759e-06

*Drezner 1978 Quantlib 1.8  : 1.097127038329759e-06
*FDM approx                    : 1.092586880408237e-06
FDM approx extrap              : 1.09712429482e-06

a, b, rho: 7.2957037,-7.3891475, -0.80360421
*Genz West                     : 7.245942013444848e-14
*Genz QuantLib 1.8             : 7.245942070366185e-14

*Drezner 1978 Quantlib 1.8  : 7.260858581048524e-14
*FDM approx                    : 7.194843962877875e-14
FDM approx extrap              : 7.19003890218e-14

a, b, rho: -2.726639,4.9965896, 0.17220467
*Genz West                     : 0.003199150045498287
*Genz QuantLib 1.8             : 0.003199150045498298

*Drezner 1978 Quantlib 1.8     : 0.003199150046013107
*FDM approx                   : 0.003186916800067802
FDM approx extrap             : 0.00319914563772

Max error West/QL: 1.11022302463e-16
Max error Fdm/West: 0.00055286738894
Max error Fdm Extrap/West: 3.32514473067e-07

我们注意到当 NX = NY = 50 时，有限差分法仍能给出四到六位数字的精度。

基于我们的实验，我们可以得出以下结论：

- West 和 Quantlib 对 Genz 算法的实现在机器精度范围内给出相同的精度。我们使用有限差分法来检验它们，以确保它们不会对参数的某些值给出相同的错误输出。
- 有限差分方法的附加价值在于它可以根据我们的精度要求进行调整。该方案是二阶精度的，我们可以使用 Richardson 外推法达到四阶精度。此外，这些方案输出一个矩阵，这可以节省某些应用类别的重新计算。
- 有限差分方法可以应用于广泛的双变量和三变量分布，例如双变量 t 分布和三变量正态分布。
- Drezner（1978）算法的精度低于其他方案，并且在 ρ = ±1 时会退化。

为完整起见，我们现在讨论另外两种计算 (16.1) 的算法。

## 16.5 ABRAMOWITZ AND STEGUN 近似

Abramowitz 和 Stegun（1965）给出了若干计算 (16.1) 的方法。我们重点关注由嵌套积分定义的特定情况（‘AS 26.3.3’）：

```
M(a, b; ρ) = ∫_{-∞}^{a} Z(x)dx ∫_{-∞}^{w(x)} Z(t)dt    (16.7)
```

其中：

```
Z(x) = 1/√(2π) e^{-x²/2}
```

并且

```
w(x) = (b - ρx)/√(1 - ρ²).
```

我们推测这种公式化可能比其他方法更容易计算。为此，我们将 (16.7) 写成形式：

```
M(a, b; ρ) = ∫_{-∞}^{a} Z(x) N(w(x)) dx    (16.8)
```

其中一般情况下：

$$N(t) = \int_{-\infty}^{t} Z(s) ds.$$

假设我们有一种计算单变量累积函数 $N(t)$ 的方法（我们有），我们可以应用一些数值求积方案来近似 (16.8) 中的积分。在本例中我们使用二阶 *midpoint rule* 并应用重复的 Richardson 外推法以达到更高阶精度。首先，我们定义以下函数：

```
// Normal variates etc.
double Pdf(double x)
{
    const double A = 1.0 / std::sqrt(2.0 * 3.141592653589793238462);
    return A * std::exp(-x*x*0.5);
}

// C++11 supports the error function
auto cndN = [](double x)
    { return 0.5 * (1.0 - std::erf(-x / std::sqrt(2.0))); };

double Cdf(double x)
{ // The approximation to the cumulative normal distribution
    return cndN(x);
}
```

将 midpoint rule 应用于 (16.8) 的代码为：

```
double BivariateNormal(double a, double b, double rho,
                    double ALower, double BLower, long NX)
{ // 26.3.3 Abramowitz and Stegun
    double res = 0.0;
    double hx = (a - ALower) / NX;
    const double fac = 1.0 / std::sqrt(1 - rho*rho);
    double s = ALower + (0.5*hx);
    double hx2 = hx / 2;
    double x = s;
    double w;
    for (long n = 0; n < NX; n += 1)
    {
        w = fac*(b - rho*(x));
        res += hx*Pdf(x)*Cdf(w);
        x += hx;
    }
}
```

而重复 Richardson 外推法的代码为：

```
double BivariateNormalExtrapolate(double a, double b, double rho,
    double ALower, double BLower, long NX)
{ // 26.3.3 Abramowitz and Stegun

    // Repeated Richardson extrapolation
    double uh = BivariateNormal(a, b, rho, ALower, BLower, NX);
    double uh2 = BivariateNormal(a, b, rho, ALower, BLower, 2 * NX);
    auto vh = (4 * uh2 - uh) / 3.0;

    double uh4 = BivariateNormal(a, b, rho, ALower, BLower, 4 * NX);
    auto vh2 = (4 * uh4 - uh2) / 3.0;

    return (16 * vh2 - vh) / 15;

    return vh;
}
```

最后，我们创建一个测试程序来展示如何在第 16.4 节中的一些示例上使用该算法：

```
int main()
{
    // Range of values to test with
    //double a = 0.88323078; double b = 1.0534402; double rho =
    //-0.35704502;
    //double a = -3.6033799; double b = 5.1965627; double rho = 0.69074304;
    //double a = -6.3771756; double b = 0.2349262; double rho =
    //-0.19490095;
    double a = -1.946981; double b = 3.1876528; double rho = 0.054292586;
    //double a = 6.088323078; double b = 6.0534402; double rho =
    //0.999935704502;

    long N = 20; // Number of subdivisions
    double AL = -8.0; double BL = -8.0;

    std::cout << "*A&S 26.3.3   : " << std::setprecision(16)
              << BivariateNormal(a, b, rho, AL, BL, N) << '\n';

    std::cout << "*A&S 26.3.3 Extrapolated  : " << std::setprecision(16)
              << BivariateNormalExtrapolate(a, b, rho, AL, BL, N) << '\n';

    return 0;
}
```

我们主要为完整性引入了 26.3.3 示例。

在‘AS 26.3.3’（方程 (16.8)）的情况下，我们得到求积方案：

M(a, b, ρ) ≅ ∫_{AL}^{a} Z(x) N(w(x)) dx ≅ ((a - AL)/2) ∑_{j=1}^{n} w_j Z(\tilde{x}_j) N(w(\tilde{x}_j))    (16.11)

其中 \tilde{x}_j = (a-AL)/2 x_j + (a+AL)/2 , j = 1, ..., n 且 AL = 截断点。

我们已通过以下自由函数实现了方程 (16.11)（注意我们使用循环展开来提高性能）：

```
double BivariateNormalGaussLegendre(double a, double b, double rho,
 double ALower)
{ // 26.3.3 Abramowitz and Stegun

 // 20-point Gauss Legendre rule
 // Nodes
 const std::vector<double> x = { -0.0765265211334973,
 0.0765265211334973, -0.2277858511416451,
 0.2277858511416451, -0.3737060887154195,
 0.3737060887154195, -0.5108670019508271,
 0.5108670019508271, -0.6360536807265150,
 0.6360536807265150, -0.7463319064601508,
 0.7463319064601508, -0.8391169718222188,
 0.8391169718222188, -0.912234428513259,
 0.912234428513259, -0.963971927779138,
 0.963971927779138, -0.9931285991850949,
 0.9931285991850949 };

 // Weights
 const std::vector<double> w = { 0.1527533871307258,
 0.1527533871307258, 0.1491729864726037,
 0.1491729864726037, 0.1420961093183820,
 0.1420961093183820, 0.1316886384491766,
 0.1316886384491766, 0.1181945319615184,
 0.1181945319615184, 0.1019301198172404,
 0.1019301198172404, 0.0832767415767048,
 0.0832767415767048, 0.0626720483341091,
 0.0626720483341091, 0.0406014298003869,
 0.0406014298003869, 0.0176140071391521,
 0.0176140071391521 };

 // Using Gauss Legendre 20-point method
 long N = 20;

 double res = 0.0;
 double alpha = (a - ALower) / 2.0;
 double beta = (a + ALower) / 2.0;

 const double fac = 1.0 / std::sqrt(1 - rho*rho);
 double xl, wl;
```


# 340 MATLAB 和 C# 中的 Heston 模型及其扩展

$\ell = \ln(Ke^{-rt}/S_t)$。在被积函数 (11.31) 中，$R_2 = \text{Re}[\varphi_2(u)]$ 和 $I_2 = \text{Im}[\varphi_2(u)]$ 分别表示 Attari (2004) 特征函数 $\varphi_2(u)$ 的实部和虚部，该函数给出：

```
$\varphi_2(u) = \exp(C_2(\tau,u) + D_2(\tau,u)v_0 - iurt). \quad (11.32)$
```

在 (11.32) 中，$C_2(\tau,u)$ 和 $D_2(\tau,u)$ 是 Heston (1993) 特征函数 $f_2(u)$ 中的项，$v_0$ 是波动方差参数 $S_v$。我们在第 3 章看到 $\varphi_2(u)$ 独立于通过参数 $\ell$ 出现的现价 $S_t$。因此，导出看涨权的 delta 表达式是简单的：

```
$\Delta_C = 1 - \frac{Ke^{-rt}}{\pi} \int_0^\infty \frac{\partial A(u)}{\partial S} du. \quad (11.33)$
```

应用链式法则，我们得到 (11.33) 中的被积函数为：

```
$\frac{\partial A(u)}{\partial S} = \frac{-F(u)\sin(u) + G(u)\cos(u)}{1+u^2} \times \left(-\frac{u}{S}\right). \quad (11.34)$
```

因为 $\partial(\ell u)/\partial S = -u/S$。gamma 给出：

```
$\Gamma = \frac{Ke^{-rt}}{\pi} \int_0^\infty \frac{\partial^2 A(u)}{\partial S^2} du. \quad (11.35)$
```

被积函数为：

```
$\frac{\partial^2 A(u)}{\partial S^2} = \frac{-F(u)(\cos(\ell u)+\sin(\ell u)) + G(u)(-\sin(\ell u)+\cos(\ell u))}{1+u^2} \times \left(\frac{u}{S^2}\right). \quad (11.36)$
```

在 Attari (2004) 的看涨权公式中，delta 和 gamma 可以很容易地得到闭式形式，且不于现价 $S_t$。通过这种方法获取其他希腊字母是不实际的，因为希腊字母的参数出现在 $\varphi_2(u)$ 中。事实上，为了获得 $A(u)$ 的导数，我们需要像方程 (11.31) 所示分离 $\varphi_2(u)$ 的实部和虚部，并分别获得这些部分的导数。我们仍然可以使用有限差分获取模型中的希腊字母。

Matlab 函数 `AttariProbreeks.m` 计算方程 (11.34) 和 (11.36) 中 delta 和 gamma 所需被积函数。它与第 3 章介绍的 `AttariProb` 非常相似，因此不再完整给出：

```
function A = AttariProbreeks(u,...,Greek)

% Attari 和 L 函数的特征函数

f = exp(C + D*v0 - i*u*tau);

l = log(exp(-r*tau)*K/S0);
```

### 系数
F = (real(f) + imag(f)/u);
G = (imag(f) - real(f)/u);
% 返回所选希腊字母的被积函数
if strcmp(Greek, 'Delta'):
    A = (F*sin(L) - G*cos(L)) * u/S0/(1+u^2)
elseif strcmp(Greek, 'Gamma'):
    A = (-F*cos(L) + G*sin(L)) * u/S0/(1+u^2)
```

在 Attari (2004) 看涨权公式中，delta 和 gamma 可以很容易地得到不依赖于现价 $S_t$ 的闭式形式。通过这种方法获取其他希腊字母是不实际的，因为希腊字母的参数出现在 $\varphi_2(u)$ 中。事实上，为了获得 $A(u)$ 的导数，我们需要像方程 (11.31) 所示分离 $\varphi_2(u)$ 的实部和虚部，并分别获得这些部分的导数。我们仍然可以使用有限差分获取模型中的希腊字母。

`AttariProbreeks.m` 函数计算方程 (11.34) 和 (11.36) 中 delta 和 gamma 所需的被积函数。它与第 3 章介绍的 `AttariProb` 函数非常相似，因此在这里不再完整给出：

```matlab
function A = AttariProbreeks(u,...,Greek)
% Attari 和 L 函数的特征函数
f = exp(C + D*v0 - i*u*tau);
l = log(exp(-r*tau)*K/S0);
```

### 系数

F = (real(f) + imag(f)/u);

G = (imag(f) - real(f)/u);

% 返回所选希腊字母的被积函数

if strcmp(Greek, 'Delta'):

    A = (F*sin(L) - G*cos(L)) * u/S0/(1+u^2)

elseif strcmp(Greek, 'Gamma'):

    A = (-F*cos(L) + G*sin(L)) * u/S0/(1+u^2)

```

*(注：由于提供的文本中存在大量重复和断层，上述译文已根据逻辑进行了整理，以确保翻译的连贯性)*

## Heston 希腊字母

# 339

![](img/bc3df3b6c26c2272307f56b6cf75ef87_345_0.png)

**图 11.2** Heston 模型的 Theta

## 在 ATTARI 和 CARR-MADAN 公式下的希腊字母

在之前的章节中，我们根据原始的 Heston (1993) 看涨权价格公式推导并实现了希腊字母。我们也可以在其他公式（例如之前章节中遇到的公式）下推导出希腊字母的解析表达式。使用 Zhu (2010) 推导的 Attari (2004) 看涨权公式来获取 delta 和 gamma 是直接的。回想第 3 章，该模型中的看涨权公式给出：

```
$C(K) = S_t - \frac{1}{2}Ke^{-rt} - \frac{Ke^{-rt}}{\pi} \int_{0}^{\infty} A(u)du.$
```

被积函数为：

```
$A(u) = \frac{R_2 + \frac{I_2}{u}}\cos(\ell u) + \left(I_2 - \frac{R_2}{u}\right)\sin(\ell u)}{1+u^2} \frac{F(u)\cos(\ell u) + G(u)\sin(\ell u)}{1+u^2} \quad (11.31)$
```

# 340 MATLAB 和 C# 中的 Heston 模型及其扩展

$\ell = \ln(Ke^{-rt}/S_t)$。在被积函数 (11.31) 中，$R_2 = \text{Re}[\varphi_2(u)]$ 和 $I_2 = \text{Im}[\varphi_2(u)]$ 分别表示 Attari (2004) 特征函数 $\varphi_2(u)$ 的实部和虚部，该函数给出：

```
$\varphi_2(u) = \exp(C_2(\tau,u) + D_2(\tau,u)v_0 - iurt). \quad (11.32)$
```

在 (11.32) 中，$C_2(\tau,u)$ 和 $D_2(\tau,u)$ 是 Heston (1993) 特征函数 $f_2(u)$ 中的项，$v_0$ 是波动方差参数 $S_v$。我们在第 3 章看到 $\varphi_2(u)$ 独立于通过参数 $\ell$ 出现的现价 $S_t$。因此，导出看涨权的 delta 表达式是简单的：

```
$\Delta_C = 1 - \frac{Ke^{-rt}}{\pi} \int_0^\infty \frac{\partial A(u)}{\partial S} du. \quad (11.33)$
```

应用链式法则，我们得到 (11.33) 中的被积函数为：

```
$\frac{\partial A(u)}{\partial S} = \frac{-F(u)\sin(u) + G(u)\cos(u)}{1+u^2} \times \left(-\frac{u}{S}\right). \quad (11.34)$
```

因为 $\partial(\ell u)/\partial S = -u/S$。gamma 给出：

```
$\Gamma = \frac{Ke^{-rt}}{\pi} \int_0^\infty \frac{\partial^2 A(u)}{\partial S^2} du. \quad (11.35)$
```

被积函数为：

```
$\frac{\partial^2 A(u)}{\partial S^2} = \frac{-F(u)(\cos(\ell u)+\sin(\ell u)) + G(u)(-\sin(\ell u)+\cos(\ell u))}{1+u^2} \times \left(\frac{u}{S^2}\right). \quad (11.36)$
```

在 Attari (2004) 的看涨权公式中，delta 和 gamma 可以很容易地得到闭式形式，且不依赖于现价 $S_t$。通过这种方法获取其他希腊字母是不实际的，因为希腊字母的参数出现在 $\varphi_2(u)$ 中。事实上，为了获得 $A(u)$ 的导数，我们需要像方程 (11.31) 所示分离 $\varphi_2(u)$ 的实部和虚部，并分别获得这些部分的导数。我们仍然可以使用有限差分获取模型中的希腊字母。

`AttariProbreeks.m` 函数计算方程 (11.34) 和 (11.36) 中 delta 和 gamma 所需被积函数。它与第 3 章介绍的 `AttariProb` 函数非常相似，因此在这里不再完整给出：

```
function A = AttariProbreeks(u,...,Greek)

% Attari 和 L 函数的特征函数

f = exp(C + D*v0 - i*u*tau);

l = log(exp(-r*tau)*K/S0);
```

### 系数
F = (real(f) + imag(f)/u);
G = (imag(f) - real(f)/u);
% 返回所选希腊字母的被积函数
if strcmp(Greek, 'Delta'):
    A = (F*sin(L) - G*cos(L)) * u/S0/(1+u^2)
elseif strcmp(Greek, 'Gamma'):
    A = (-F*cos(L) + G*sin(L)) * u/S0/(1+u^2)
```

# 344

# MATLAB 和 C# 中的 Heston 模型及其扩展

```matlab
function y = LewisIntegrandGreek(k,...,Greek)
% 基础变换，H(k,S,t)
H = exp(C + D*0)
% 返回积分函数的实部
if strstrcmp(Greek, 'Price')
y = real(-X-i*k-r*tau)/(k^2-i*k*H)
elif strcmp(Greek, 'Delta')
y = real(-X-i*k-r*tau)/(k^2-i*k)*H*(-i/S)
elif strcmp(Greek, 'Gamma')
y = real(-exp(-X-i*k-r*tau)*H/S^2)
elif strcmp(Greek, 'Rho')
y = real(-exp(-i*k-r*tau)/(k^2-i*k)*H*D)*sqrt(v0)
elif strcmp(Greek, 'Theta')
y = real(exp(-i*k-r*tau)*(k^2-i*k)*H)
DC = kappa*theta(kappa/2) + g*exp(d) ...
DD = (kappa/2)*exp(d*t)*(g-1)/(1-g*exp(d)) ...
y = real((-1-i*r-q)/(C+D*v0))*exp(-X-i ...
elif strcmp(Greek, 'Volga')
y = exp(-i*k)/(k^2-i*k)*H*D*sqrt(v0)
elif strcmp(Greek, 'Vanna')
y = real(I)*4*sqrt(v0)
elif strcmp(Greek, 'Vanna')
y = real(exp(-i*k-r*tau)/(k^2-i*k)*H*D*(-i/S)*sqrt(v0))
end
```

该函数被传递给 Matlab 函数 `LewisGreekPrice.m`。C# 代码类似，此处未给出。

Lewis (2001) 推导出的期权价格 $C(S)$ 也使用了第 4 章涵盖的 Parseval 等等式。使用 $k=1/2$ 的公式是 Lewis (2001) 中的方程 (3.11)。

> $C(S_i) = S_i e^{-qt} - \int_{0}^{\infty} \frac{\sqrt{S_i e^{-qt}+r\tau/2}}}{\pi} \text{Re} \left[ e^{ix\mu} \left( u - \frac{1}{2i} \right) \right] \frac{1}{u^2+4} du \n= S_i e^{-qt} \int_{0}^{\infty} \text{Re} \left[ K^{iu-e^{-r\tau f_2}} \left( u - \frac{1}{2i} \right) \right] \frac{1}{u^2+4} du$

其中 $X$ 定义在 (11.40) 之后我们使用了第 4 章中的结论 $\varphi(u)=f_2(u)e^{-uy}$，其中 $Y = In_t + (r-q)\tau$ 且 $f_2$ 是 Heston (1993) 特征函数。同样通过对这种 Lewis 2001 价格形式的希腊字母进行直接求导得到。Matlab 函数 `LewisGreeks311.m` 和 C# 函数 `LewisGreeks311` 用于实现来自 Lewis (2001) 方程 (3.11) 的看涨价格 $C(S)$ 的希腊字母。这些函数与之前章节介绍的相似，此处不再给出。

表 11.3 展示了使用本章采用闭式形式的希腊字母。我们使用以下设置：$S=100, \theta=0.25, \tau=0.05, q=0$，以及参数值 $\kappa=2, v_0=0.05,\sigma=0.1,$ 和 $\rho=-0.9$。

## Heston 希腊字母

## 表 11.3 各种形式下的闭式希腊字母

| | Heston (1993) | Attari (2004) | Carr and Madan (1999) | Lewis (2000) | Lewis (2001) |

|---|---|---|---|---|---|

| 价格 Delta (Price Delta) | 0.5836 | 0.5836 | 0.5083 | 0.5666 | 0.5837 |

| Gamma | 0.0347 | 0.0347 | 0.0347 | 0.0353 | 0.0347 |

| Theta | -11.3995 | | -11.4094 | -11.3464 | -11.4009 |

| Rho | 13.3128 | | 13.3127 | 12.8696 | 13.3133 |

| Vega 1 | 15.3911 | | 15.3909 | 15.4812 | 15.3915 |

| Vanna | -0.1257 | | -0.1257 | 0.0516 | -0.1257 |

| Volga | 15.5081 | | 15.4273 | 15.7285 | 15.4054 |

### 使用 FFT 和 FRFT 的希腊字母

我们在第 5 章中看到，快速傅里叶变换 (FFT) 和分数傅里叶变换 (FRFT) 都能非常快速地产生价格并适用于广泛的执行权样本。将这些方法以相同的方式产生希腊字母是简单的。回顾第 5 章实现看涨价格的方法，我们构建了积分网格 $\{v_j\}_{j=1}^N$ 和对数执行权 $\{k_j\}_{j=1}^N$，并计算点 $x_j = \exp[(b - \ln S_0)\psi(v_j)]$ 对于 $j = 1, \dots, N$。我们通过和得到 $\hat{x}_u = C(k_u)$，即在对数执行权点 $k_u$ 处评估的看涨价格：

```
$\hat{x}_u = \frac{e^{-u a k_u}}{\pi} \sum_{j=1}^N \left[ e^{-\frac{i}{2}(j-1)(u-1)} X_j \right] \text{ for } u = 1, \dots, N. \quad (42)$
```

为了在 $x$ 中通过 FFT 获得一组希腊字母，我们只需将

```
$\psi(v_j) = \frac{e^{-v_j^2} f_2(v_j) - (\alpha + i)}{\alpha^2 + v_j^2} \quad (43)$
```

替换为使用 $f_2$ 导数的修改版本，例如方程 (38) 中的 theta。使用 FFT 实现希腊字母需要对第 5 章提出的代码进行轻微修改。Matlab 函数 `HestonCallFFreek.m` 与该章节的 `HestonCallFFT` 几乎相同，不同在于它使用了 `HestonGreeks.m` 函数。它通过额外参数返回特征函数或其导数：

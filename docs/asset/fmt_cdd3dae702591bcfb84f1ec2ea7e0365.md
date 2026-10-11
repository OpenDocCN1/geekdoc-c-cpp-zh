
```sas
c = probb = 0;
do it = 0 to m[j];
ratio = it/m[j];
if (ratio > lowerb[s]) && (ratio <= upper[s]) then do
aux = lgamma(mj+1) + lgamma(c) + lgamma(it+c*pi) + lgamma(m[j]-it+c-pi)
probbb = lgamma(m[j]-it+1) - lgamma(m[j]+c)
probbb = lgamma(c*pi) + exp(aux);
end;
```

```sas
end;
end;
expect[s] = expect[s] + probb;
probbb = 0;
```

```sas
end;
expect[k] = n-sum(expect[1:k-1]);
```

```sas
call collapse ~parms_b,lower,upper,expected;

parms = ~parms_b,lower;
call gof(r,t,n,m,lower,upper,expected,nparms,obs_sum,exp_sum,goStat);

* 打印 Beta-二项分布下的结果:

print "Goodness-of-fit Test under Beta-binomial Distribution";
print "lower upper expected";
print "Total Counts";
print n obs exp_sum;
print "Null Hypothesis: Data are distributed according to a Beta-binomial Distribution";
print GOStat;

* 输出结果（观测值与期望值）到数据集 Resid_BB，后续用于 QQ 图:

Distribution = j(nrow(obs,1),'Beta-Binomial');
Resid = obs - expected;
create Resid_BB var(Distribution Resid);
append;

****************************************************************
* 2 开始在随机聚类二项分布下的 GOF 检验;
*************************************************

use pi_rcb var (Pred);
read all into pi;
use rho_cb var (Pred);
read all into rho;

* 计算随机聚类二项分布的期望频率:
k = max(j) + 1;

* 初始化:
lowerb = j(k,1,-0.00000001);
upper = j(k,1,1.00000001);

expect = j(k,1,0);

* 定义区间的上界和下界:
do s = 2 to k;
lowerb(s) = (s-1)/k;
upper(s-1) = (s)/k;
end;

do s = 1 to k-1;
expect[s] = 0;
do j = 1 to n;
pi = pi[j];
rho = rho[j];
pic = 1-rho;
p2 = 1-rho*rhopt;
p1 = p2*rho;
end;
end;

probrcb = 0;
xl = (0:m[j]);
m2 = m[j];
pr1 = PROBNML(p1,m[j],xl);
pr2 = PROBNML(p2,m[j],xl);
pr1[2:m2] = pr1[2:m2]*pr1[1:m2-1];
pr2[2:m2] = pr2[2:m2]*pr2[1:m2-1];
```

SAS 中提供了用于处理这些模型的程序。其中包括 `SAS/STAT` 中的 `GENMOD`、`GLIMMIX` 和 `NLMIXED` 过程，以及 `SAS/ETS` 软件中提供的 `COUNTREG` 过程。读者可能记得，二项数据的过离散模型可以被看作二项分布的推广。同样地，对于过离散的计数数据，它们相对于泊松分布是分层的模型。下面的图展示了第 4 章涵盖的分布，以及本章将涵盖的分布（完整描绘请参阅第 1 章附录 1.1）。

## 1) 二项分布

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_172_0.png)

## 2) 泊松分布

# 6.2 负二项分布

用于解释计数响应中过离散的基准模型是负二项（NB）分布。这种分布可以通过几种不同的方式推导出来，并在过去的几个世纪里经过了广泛的研究（Johnson, Kotz, and Kemp 1992, 第 3 节，第 5 章）。负二项分布最为人知的解释是：在系列伯努利试验中，在出现预定次数的成功之前失败次数的数分布。然而，在过离散的背景下，它处理具有计数响应的聚类数据缺乏等离散性（条件均值和方差相等）的能力是我们关注的重点。我们现在给出负二项分布的推导过程，该推导与过离散的关系更为直接。我们首先假设对于给定的簇，计数数量（关于速率参数）的条件分布是泊松分布。进一步地从分层角度，速率根据 Gamma 分布变化。那么，计数的无条件分布就是 Nb。为此，令 $Y_j, j=1,2,...,n$ 为独立分布的随机变量，使得 $Y_j \sim \text{Poisson}(u_j)$。$Y_j$ 的概率函数为：

$$\Pr(Y_j|u_j) = \frac{e^{-u_j} u_j^{Y_j}}{\Gamma(Y_j+1)} \quad (6.1)$$

其中 $\Gamma(\cdot)$ 是 Gamma 函数，对于整数参数 $y+1$ 变为 $y!$。假设速率参数 $u_j, j=1,2,...,n$ 是独立同分布的，服从 Gamma($\alpha$,$\beta$）。也就是说，每个 $u_j$ 的密度函数为：

$$f(u) = \frac{u^{\alpha-1}}{\Gamma(\alpha)\beta^\alpha} e^{-\frac{u}{\beta}}, u > 0 \quad (6.2)$$

其中 $\alpha$ 是形状参数，$\beta$ 是尺度参数。

在上述参数化下，Gamma 分布的均值和方差为：

$$E(U) = \alpha\beta$$

和

$$\text{Var}(U) = \alpha\beta^2.$$

可以证明（Johnson, Kotz, and Kemp 1992, p. 204），$Y_j$ 的无条件分布为：

$$\Pr(Y_j=y) = \frac{\Gamma(y+\alpha)}{\Gamma(\alpha)\Gamma(y+1)} \left(\frac{1}{1+\beta}\right)^\alpha \left(\frac{\beta}{1+\beta}\right)^y, y=0,1,... \quad (6.3)$$

这可以很容易识别为成功概率为 $\frac{\beta}{1+\beta}$ 的负二项分布($\alpha$，$\beta$)。

由此得出，$Y_j$ 的无条件均值和方差为：

$$E(Y_j) = \alpha\beta \quad (6.4)$$

和

$$\text{Var}(Y_j) = \alpha\beta(1+\beta) \quad (6.5)$$

负二项分布对应于泊松-Gamma 混合模型，其中混合分布是 Gamma 分布（泊松分布的共轭先验）。该模型与 Beta-二项分布之间存在相似性，这种性在于后者通过相似的机制产生，即当成功概率根据 Beta 分布变化时，获得二项分布的无条件分布。在参数化 $\mu = \alpha$ 和 $\kappa = \frac{1}{\alpha}$ 下，$Y_j$ 的无条件概率函数为：

$$\Pr(Y_j = y) = \frac{\Gamma(y+\frac{1}{\kappa})}{\Gamma(\frac{1}{\kappa})\Gamma(y+1)} \left(\frac{\kappa\mu}{1+\kappa\mu}\right)^y, y=0,1,... \quad (6.6)$$

这种参数化产生了一阶矩的如下表示：

$$E(Y_j) = \mu \quad (6.7)$$

和

$$\text{Var}(Y_j) = \mu + \kappa\mu^2 = \mu(1+\kappa\mu) \quad (6.8)$$

Cameron and Triv (1986) 考虑了一类具有均值 $\mu$ 和方差函数 $\mu+\mu^p$ 的通用 NB 模型，其中 $-\infty < p < \infty$。$p=2$ 的情况提供了 NB 模型的标准公式，并对应于第 1.3 节描述的相对于泊松方差函数的过离散的常见描述。$p=1$ 的情况提供了 Dean (1992) 所考虑的类泊松计数的过离散方差函数。`GENMOD`、`GLIMMIX` 和 `CONTREG` 在 $p=2$ 的情况下提供了 $\mu$ 和 $\kappa$ 的极大似然估计。`CONTREG` 还提供了具有线性方差函数 $\mu(1+\kappa\mu)$ 的负二项模型。参数 $\kappa$ 被称为“离散参数”。程序 6 提供了生成相同均值 $\mu$ 的泊松和 NB 分布概率函数的程序语句，相应的方差分别为 $\mu$ 和 $\mu(1+\kappa\mu)$。在示例中，$\mu$ 的值为 10，$\kappa$ 的值为 0.2。因此，两者的均值均为 10，负二项分布的方差为 30，是泊松分布方差的三倍。图 6.1 展示了这两个分布。Joe 和 Zhou (2005) 提出的广义泊松分布作为 NB 模型的替代方案。广义泊松分布有一个尺度参数，当该参数为零时退化为泊松分布。它比 NB 分布具有更肥的尾部。关于广义泊松分布的细节，请参考 `GLIMMIX` 过程。

## 程序6：生成相同均值 $\mu$ 的泊松和 NB 分布概率函数的程序

```sas
/*
绘制泊松和负二项分布的概率函数的图
*/
@macro plots_p_nb(mu, kappa);
data p_nb;
format Distribution $17.;
label Prob = "Probability";
mu = &mu;
kappa = &kappa;
alpha = 1/&kappa;
p = 1/(1+&kappa);
pc = 1-&p;

do Y=0 to 30;
Prob = PDF('POISSON',y,mu);
Distribution = 'Poisson';
output;
Prob = PDF('NEGEB',y,p,alpha);
Distribution = 'Negative-binomial';
output;
end;

keep y Prob Distribution;
title "泊松和负二项分布概率函数";
title2 "Mu=&mu, Kappa=\&kappa";
proc sgscatter data=p_nb;
compare y=Prob x=y / group=Distribution
markerattrs=(size=10);
end;
%mend plots_p_nb;
ods html;
ods graphics on;
%plots_p_nb(10, 0.2);
ods graphics off;
ods html close;
```

输出 6.1：均值为 10 的泊松分布和均值为 10、方差为 30 的负二项分布的概率函数图

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_176_0.png)

# 6.3 零膨胀泊松和零膨胀负二项分布

如第 4.3 节所述，Cohen (1966) 提出了一类具有形式概率函数的混合分布：

$$g(y; \omega, \alpha_1, \alpha_2, \dots, \alpha_k) = \begin{cases} \omega+(1-\omega)f(0), & \text{if } y=0 \\ (1-\omega)f(y; \alpha_1, \alpha_2, \dots, \alpha_k), & \text{if } y \ge 1 \end{cases} \quad (6.9)$$

# 第6章 过度离散计数响应的似然模型 165

$0 \le \omega \le 1$且$f(y;alpha_1, \alpha_2, \dots, \alpha_s)$可以是定义在域 $y=0, 1, \dots,$ 上的任何离散分布，参数为 $(\alpha_1, \alpha_2, \dots, \alpha_s)$。将此处的演示与 Cohen 的原始工作比较时，需要注意符号的一个重要变化。请注意，根据方程 (6.9)，$y=0$的概率为 $\omega(1-\omega)f(0)$,而在 Cohen 的符号中，相同的概率由 $(1-\omega)+\omega f(0)$给出。我们遵循 Johnson 等人 (1992) 第8章第2.2节节的参数化方法，这与 `GENMOD` 和 `COUNTREG` 中使用的符号一致。在 Cohen 的论文中，$\omega$ 代表“人口中感染或易感人群的比例”，这与概率函数 $f(\cdot)$ 相关。我们的参数化方法允许我们将 $\omega$ 解释为**零膨胀概率**测量值。这一族分布允许对零的过度进行建模，并很容易适用于泊松分布和负二项分布。$\omega$ 可以取负值，前提是：

$$\omega \ge \frac{-f(0)}{1-f(0)} \quad (6.10)$$

在这种情况下，与 $f(y;alpha_1, \alpha_2, \dots, \alpha_s)$ 相关的零比例会减少。

如果 $f(y;\mu)$ 对应于参数为 $\mu$ 的泊松分布的概率函数，根据 (6.9) 可 $Y$ 是参数为 $(\mu, \omega)$ 的零膨胀泊松分布 (ZIP)，其概率函数为

$$Pr(Y=y) = \omega I(y=0)+(1-\omega)\frac{e^{-\mu y}}{\Gamma(y+1)}, y=0,1,\dots \quad (6.11)$$

$I(\cdot)$ 是指示函数。读者应该注意 (6.10) 中有两个零的来源：一个来自概率为 $\omega$ 的零退化分布，另一个来自概率为 $(1-\omega)$ 的 Poisson($\mu$)。请注意，$Pr(Y=0)=\omega+(1-\omega)e^{-\mu}$，对于 $\omega>0$，该值始终大于或等于 $e^{-\mu}$。同样，对于如 (6.10) 中的 $\mu<0$，在 ZIP 模型下观测到零的概率将小于泊松分布下零的概率。ZIP 分布的均值和方差可以证明为

$$E(Y) = (1-\omega)(\mu+\mu^2) \quad (6.12)$$

和

$$Var(Y) = (1-\omega)(\mu+\mu^2) \quad (6.13)$$

回计数数据的标准差是泊松分布，当泊松类型变量的方差大于该值时，存在过度离散。从 $Var(Y)=(1-\omega)(\mu+\mu^2) > (1-\omega)E(Y)$ 可以看出，泊松中零的过度意味着过度离散。

## 166 SAS 中的过度离散模型

注意，ZIP 的方差可能不会超过普通泊松分布的方差。因此，重要的是，在此背景下，过度离散的含义严格通过比较分布本身的均值和方差来定义，而不是相对于泊松方差进行比较。回想 NB 被认为相对于泊松具有过度离散。

同样，概率函数 (6.9) 也可以扩展到负二项分布。如果 $f(\mu,\kappa)$ 对应于参数为 $(\mu,\kappa)$ 的 NB 分布的概率函数，那么参数为 $(\mu,\kappa)$ 的零膨胀负二项分布 (ZINB) 的概率函数给出

$$Pr(Y=y)=\omega I(y=0)+(1-\omega)\frac{\Gamma(y+\frac{1}{\kappa})}{\Gamma(\frac{1}{\kappa})}\left(\frac{\mu}{1+\kappa}\right)^y,y=0,1,\dots \quad (14)$$

在 ZIP 分布的情况下，ZINB 分布中的零来自不同的来源：概率为 $\omega$ 的零退化分布，以及概率为 $(1-\omega)$ 的负二项($\mu,\kappa$)。观察分布 (5) 和 (6) 都是混合分布。显示 ZINB 分布的均值和方差为

$$E(Y)=(1-\omega)\mu \quad (15)$$

和

$$Var(Y)=(1-\omega)(\mu(1+\kappa)+\omega^2) \quad (16)$$

在 ZIP 分布的情况下，$Var(Y)=(1-\omega)(\mu+\omega^2)$ 的事实表明 NB 分布中零的过度意味着过度离散。再次，过度离散是指比较均值与方差。与泊松一样，ZINB 和 NB 在保持相同零比例的情况下表现出更大的变异。这类似于 NB 相对于泊松具有过度离散的事实。

# 第6章 过度离散计数响应的似然模型 167

# 6.4 吸虫卵数量示例

吸虫是一类扁虫，包括具有厚外皮以及用于附着组织的吸盘或钩的动物寄生虫。它们也被称为蛭。吸虫引起称为血吸虫病（也称为血虫病）的疾病在亚洲、非洲和南美最常见，特别是在淡水域可能携带寄生虫的地方。Cohen (1966) 对从一个埃及村庄 926 名居民那里收集的单片吸虫卵数量计数样本进行了分析。人口由感染组和非感染组混合组成。

表 6.1：吸虫卵计数

| 卵 ($O_i$) | $E_i$ |

| :--- | :--- |

| 0 | 603 |

| 1 | 112 |

| 2 | 93 |

| 3 | 53 |

| 4 | 19 |

| 5 | 21 |

| 6 | 7 |

| 7 | 6 |

| 8 | 5 |

| 9 | 2 |

| 10 | 1 |

| 11 | 2 |

| 14 | 2 |


![](img/5c3cdcd9b21d4d4e9da6d42180679a02_23_0.png)

**图11** 两相微流示意图。相I和相II的黏度分别为 \(\mu^I\) 和 \(\mu^{II}\)，宽度分别为 \(a\) 和 \(b\)。

为了获得相I和相II的应力，对式(4)进行积分，表示为

$$
\tau_{zx}^I = \frac{\Delta P}{L} x + C_1^I \\
\tau_{zx}^{II} = \frac{\Delta P}{L} x + C_1^{II}
\tag{6}
$$

其中 \(C_1\) 为常数，上标 I 和 II 分别表示相 I 和相 II。这里，假设剪切应力连续性作为边界条件。即，

$$
\tau_{zx}^I = \tau_{zx}^{II} \text{ at } x = 0
\tag{7}
$$

将式(6)代入式(7)，得到如下关系。

$$
C_1^I = C_1^{II} = C_1
\tag{8}
$$

这里使用牛顿黏性定律，

$$
\tau_{zx} = \mu \frac{dv_z}{dx}
\tag{9}
$$

其中 \(v_z\) 为 z 方向流速。利用式(6)–(9)，相I和相II的速度 \(v^I\) 和 \(v^{II}\) 表示为

$$
\begin{aligned}
v_z^I &= \frac{\Delta P}{2\mu^I L}x^2 + \frac{C_1}{\mu^I}x + C_2^I \\
v_z^{II} &= \frac{\Delta P}{2\mu^{II} L}x^2 + \frac{C_1}{\mu^{II}}x + C_2^{II}
\end{aligned}
\tag{10}
$$

水/丁醇（3.0 cP）、水/乙酸丁酯（0.73 cP）和水/乙酸乙酯（0.43 cP）。

多相微流受压力支配（Aota et al., 2007a, 2009a）。描述多相微流所需的一个重要参数是驱动流体的压力。由于流体黏度，压力在流动下游部分降低。当相互接触的两种流体具有不同黏度时，两相之间的压力差（\(\Delta P_{\mathrm{flow}}\)）是接触长度和流速的函数。另一个重要参数是由两相之间界面张力引起的拉普拉斯压力（\(\Delta P_{\mathrm{Laplace}}\)）。通过 \(\Delta P_{\mathrm{Laplace}}\) 与 \(\Delta P_{\mathrm{flow}}\) 之间建立的平衡，界面位置固定在微通道中的某一点处。

图13a展示了两相微流液-液界面处的压力平衡。由于玻璃的亲水性，玻璃表面上的液-液界面朝有机相弯曲。\(\Delta P_{\mathrm{Laplace}}\) 在弯曲的液-液界面处产生。

![](img/5c3cdcd9b21d4d4e9da6d42180679a02_26_0.png)

**图13**  (a) 液-液界面处的压力平衡。两相分离时，压力差与拉普拉斯压力平衡。(b) 当两相之间的压力差大于最大拉普拉斯压力时，有机相向水相移动。(c) 当压力差小于最小拉普拉斯压力时，水相向有机相移动。缩写：Aq.，水相；Org.，有机相（Aota et al., 2009a）。

基于杨–拉普拉斯方程，\(\Delta P_{\mathrm{Laplace}}\) 估算如下：

$$
\Delta P_{\mathrm{Laplace}}=\gamma\left(\frac{1}{R_1}+\frac{1}{R_2}\right) \tag{22}
$$

其中 \(R_1\) 和 \(R_2\) 分别是液-液界面在垂直于和平行于液流方向上的曲率半径。对于平行多相微流，该方程简化如下。

$$
\Delta P_{\mathrm{Laplace}}=\gamma\left(\frac{1}{R_1}\right)=\frac{2\gamma\sin(\theta-90^\circ)}{d} \tag{23}
$$

其中 \(\theta\) 和 \(d\) 分别为接触角和微通道深度。接触角限制在水相前进接触角 \(\theta_{\mathrm{aq}}\) 与有机相前进接触角 \(\theta_{\mathrm{org}}\) 之间。因此，\(\Delta P_{\mathrm{Laplace}}\) 限制如下：

$$
\frac{2\gamma\sin(\theta_{\mathrm{aq}}-90^\circ)}{d}<\Delta P_{\mathrm{Laplace}}<\frac{2\gamma\sin(\theta_{\mathrm{org}}-90^\circ)}{d} \tag{24}
$$

当 \(\Delta P_{\mathrm{flow}}\) 超过最大 \(\Delta P_{\mathrm{Laplace}}\) 时，有机相向水相流动（图13b）。当 \(\Delta P_{\mathrm{flow}}\) 低于最小 \(\Delta P_{\mathrm{Laplace}}\) 时，水相向有机相流动（图13c）。当改变流速比时，通过改变液-液界面位置来维持压力平衡。该模型表明，微流控的重要参数是界面张力、动态接触角和微通道深度。该模型也可应用于气液微流。

考虑界面压力模型，流速应处于上限和下限之间。可通过考虑微通道中的压力损失来评估 \(\Delta P_{\mathrm{flow}}\)。假设开放出口处的压力为大气压 \(P_{\mathrm{atm}}\)，则由压力损失 \(\Delta P\) 得到的各相压力 \(P\) 表示如下：

$$
P=P_{\mathrm{atm}}+\Delta P_{\mathrm{tube}}+\Delta P_{\mathrm{channel}}
$$
$$
=P_{\mathrm{atm}}+\frac{2f\rho v_{\mathrm{tube}}^2L_{\mathrm{tube}}}{d_{h,\mathrm{tube}}}+\frac{2f\rho v_{\mathrm{channel}}^2L_{\mathrm{channel}}}{d_{h,\mathrm{channel}}} \tag{25}
$$

其中 \(f\)、\(\rho\)、\(v\) 和 \(L\) 分别为摩擦因子、密度、流体平均速度，以及分别对应出口管和微通道部分的管长与通道长度。当气液和液液微流被视为层流时，\(f\) 表示如下：

$$
f=\frac{16}{\mathrm{Re}}=\frac{16\mu}{\rho v d_h} \tag{26}
$$

因此，\(\Delta P_{\mathrm{flow}}\) 可表示如下：

$$
\Delta P_{\mathrm{flow}} = P_{\mathrm{org}} - P_{\mathrm{aq}}
= \frac{32\mu_{\mathrm{org}}V_{\mathrm{channel,org}}L_{\mathrm{channel,org}}}{d_{h,\mathrm{channel,org}}^{2}} + \frac{32\mu_{\mathrm{org}}V_{\mathrm{tube,org}}L_{\mathrm{tube,org}}}{d_{h,\mathrm{tube,org}}^{2}}
- \frac{32\mu_{\mathrm{aq}}V_{\mathrm{channel,aq}}L_{\mathrm{channel,aq}}}{d_{h,\mathrm{channel,aq}}^{2}} - \frac{32\mu_{\mathrm{aq}}V_{\mathrm{tube,aq}}L_{\mathrm{tube,aq}}}{d_{h,\mathrm{tube,aq}}^{2}} \tag{27}
$$

其中下标 org 和 aq 分别对应有机相和水相。利用式(27)评估了 \(\Delta P_{\mathrm{flow}}\) 的上限和下限。表2汇总了各种溶剂黏度的文献值。可利用式(23)评估 \(\Delta P_{\mathrm{Laplace}}\)。表3汇总了各种溶剂的界面张力。水在玻璃上的前进接触角和后退接触角

**表2** 20 °C 时溶剂黏度汇总

| 溶剂 | 黏度（cP） |
| --- | --- |
| 丙酮 | 0.315 |
| 苯胺 | 4.40 |
| 1-丁醇 | 2.948 |
| 乙酸丁酯 | 0.732 |
| 四氯化碳 | 0.969 |
| 氯仿 | 0.58 |
| 环己烷（17 °C 时） | 1.02 |
| 1-癸醇 | 12.96 |
| 二氯甲烷 | 0.445 |
| 乙醚（25 °C 时） | 0.224 |
| 1,4-二氧六环（25 °C 时） | 1.177 |
| 十二烷（25 °C 时） | 1.383 |
| 乙醇 | 1.20 |
| 乙酸乙酯 | 0.455 |
| 己烷 | 0.326 |
| 甲醇 | 0.597 |
| 硝基苯 | 2.03 |
| 1-辛醇（25 °C 时） | 7.288 |
| 戊烷 | 0.240 |
| 1-丙醇 | 2.256 |
| 甲苯 | 0.590 |
| 水 | 1.002 |
| 间二甲苯 | 0.620 |

![](img/5c3cdcd9b21d4d4e9da6d42180679a02_31_0.png)

**图15** 气液微流的相分离条件。溶剂：1，1-癸醇；2，1-辛醇；3，1-丙醇；4，硝基苯；5，十二烷；6，1,4-二氧六环；7，乙醇；8，水；9，四氯化碳；10，间二甲苯；11，己烷；12，甲苯；13，氯仿；14，乙酸乙酯；15，二氯甲烷；16，环己烷；17，丙酮；18，戊烷；19，乙醚。空心圆表示理论上限，空心三角形表示理论下限，实心圆表示上限实验结果，实心三角形表示下限实验结果（Aota et al., 2009a）。

### 3.2 多相微流的稳定化方法

泵流速的扰动可能使多相微流失稳。然而，利用微通道结构和表面能的控制方法可有效维持对微流控的稳健控制。研究人员提出，可通过改变微通道结构或向微通道添加特征来稳定多相微流，具体而言，沿微通道设置导流结构（Fokeshi et al., 2002）或柱状结构（Maruyama et al., 2004），这些结构使流体界面可具有比平坦表面更宽的接触角范围。研究人员可利用液-液微流设计各种微流控化学过程。

其他研究团队提出采用选择性化学表面修饰来稳定多相微流（Aota et al., 2007a, 2007b; Hibara et al., 2002, 2003, 2005, 2008; van der Linden et al., 2006; Zhao et al., 2001, 2002a, 2002b, 2003）。图16展示了具有化学图案化表面的微通道中液-液界面的形状。水在疏水表面上的接触角可大于90°。因此，与具有导流结构或柱状结构的微通道相比，具有图案化表面的微通道中的多相微流可在更宽的条件范围内形成。

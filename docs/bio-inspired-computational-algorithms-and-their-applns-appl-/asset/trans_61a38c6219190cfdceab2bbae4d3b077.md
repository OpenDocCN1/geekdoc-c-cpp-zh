
- Green, J. (2005). 育种遗传算法背后的思想，*开普敦大学电气工程系*。

- Folly, K. A. (2006). 电力系统稳定器的设计：遗传算法与基于种群的增量学习之间的比较，*2006 IEEE 电力工程学会大会*，ISSN: 1932-5517。

- Hemmati, R., Mojtaba, S., Boroujeni, S. & Abdollahi, M. (2010). 鲁棒型与智能型电力系统稳定器的比较。*国际物理科学杂志*，第5卷，第17期，第2564-2573页。

- Holland, J. H. (1975). *自然与人工系统中的适应*，密歇根大学出版社，安娜堡。

- Hongesombut, K., Dechanupaprittha, S., Mitani, Y. & Ngamroo, I. (2005). 基于分层与并行微遗传算法多目标设计的鲁棒电力系统稳定器整定。*第15届电力系统计算会议论文集*，列日。

- Ibraham & Ismail, Z. (2009). 一种用于随机需求车辆路径问题的育种遗传算法。*应用研究杂志*，第5卷，第11期，第1998-2005页。

- Kundur, P. (1994). *电力系统稳定性与控制*，McGraw Hill，1994。

- Michalewicz, Z. (1996). *遗传算法 + 数据结构 = 进化程序*。第3版。Springer-Verlag。

- Mitchell, M. (1996). *遗传算法导论*，麻省理工学院出版社。

- Muhlenbein, H. (1994). 育种遗传算法——一种可证明的最优搜索算法及其应用，可从 http://www.ieee.org 获取。

- Shetekela, S. & Folly, K. A. (2010). 用于电力系统稳定器设计的育种遗传算法。*2010 IEEE 进化计算大会（CEC）*，西班牙巴塞罗那。

- Shetekela (2010). *使用进化算法设计电力系统稳定器*，硕士论文，开普敦大学电气工程系。

- Shaghoolian, G. & Faiz, J. (2010). 电力系统稳定器对单机无穷大母线小信号稳定性的影响。*国际电气与电力工程杂志*，第14卷，第2期，第45-53页。

- Sundareswara, K. & Begum, S. R. (2004). 电力系统稳定器的遗传整定。*欧洲电气汇刊*，第14卷，第151-160页。

- Tiako, R. & Folly, K. A. (2009). 使用多潮流条件研究电力系统稳定器参数优化。*澳大利亚电气与电子工程杂志*，第5卷，第3期，第237-244页。

- Yoshimura, K. & Uchida, N. (2000). 多机电力系统中增强稳定性与鲁棒性的 P + ω 参数优化。*日本电气工程*，第131卷，第1期，第19-31页（译自 Denki Gakkai Ronbunshi，第11卷，1998年11月，第1312-1320页）。

- Wang, Z., Chung, C. Y., & Wong, C. T. (2008). 使用差分进化在多运行条件下设计鲁棒电力系统稳定器。*IET 发电、输电与配电*，第2卷，第5期，第690-700页。

## 关于高功率等级下同步电机中感应电机最优 PWM 的应用

Arash Sayyah<sup>1</sup> 和 Alireza Rezazadeh<sup>2</sup>  
<sup>1</sup>波士顿大学电子与计算机工程系，马萨诸塞州波士顿  
<sup>2</sup>德黑兰沙希德·贝赫什提大学电子与计算机工程系  
<sup>1</sup>美国  
<sup>2</sup>伊朗

### 1. 引言

同步电机的显著特征，如恒定运行转速、通过提供无功功率以抵消感性负载造成的滞后功率因数而实现显著节能、低浪涌电流，以及可设计转矩特性以满足被驱动负载要求的能力，使其成为众多行业的最优选择。这些电机的经济利用以及效率提升是应受到高度重视的问题。

在高功率额定运行中，驱动电路的高开关效率至关重要，因此最优脉宽调制（PWM）是合理的供电方案（Holtz, 1992）。采用最优PWM可减少电机过热，从而降低转矩脉动。由内部损耗引起的过热是电机额定选型的一个主要因素。此外，设置合适的冷却方法是一个尤其重要的问题，且其复杂性随电机尺寸增大而增加。在实现最优PWM的各种方法中，谐波消除法占主导地位（Mohan et al., 1995），（Enjeti et al., 1990），（Sun et al., 1996），（Chiasson et al., 2004），（Czarkowski et al., 2002），（Sayyah et al., 2006c）。由于铜耗从根本上由电流谐波决定，因此定义一个与谐波不良影响相关的性能指标至关重要，而不是仅关注特定谐波（Bose, 2002）。在此，总谐波电流畸变（THCD）是用于最小化电机损耗的目标函数。

同步电机在直轴（d）和交轴（q）上具有不对称结构，这使其建模与感应电机有很大不同。特别地，将说明高功率同步电机中的THCD取决于电机的一些内部参数；尤其是 $l_d$ 和 $l_q$，分别为d轴和q轴电感。基于在特定运行点采集的输入和输出数据，这些参数通过在线辨识方法确定（Ljung & Söderstrom, 1983）。根据辨识出的参数，该问题被重新表述为优化任务，并通过遗传算法（GA）寻找最优脉冲模式。确实，所提目标函数的复杂性和非线性增加了陷入……的概率

其中 $\theta$ 是转子角。忽略(14)中的欧姆项，可得：

$$
\mathbf{u}_{\alpha\beta}
= \frac{d}{d\tau}\left(L_S(\theta)i_{\alpha\beta}
+ l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right).
\tag{15}
$$

其中：

$$
L_S(\theta)=\frac{l_d+l_q}{2}I_2
+\frac{l_d-l_q}{2}\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}.
\tag{16}
$$

$I_2$ 是 $2\times2$ 单位矩阵。因此：

$$
\begin{aligned}
i_{\alpha\beta}
&=L_S^{-1}(\theta)\cdot\left(\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right)\\
&=\begin{pmatrix}
\frac{l_d+l_q}{2l_d l_q} - \frac{l_d-l_q}{2l_d l_q}\cos2\theta &
-\frac{l_d-l_q}{2l_d l_q}\sin2\theta\\
-\frac{l_d-l_q}{2l_d l_q}\sin2\theta &
\frac{l_d+l_q}{2l_d l_q} + \frac{l_d-l_q}{2l_d l_q}\cos2\theta
\end{pmatrix}
\cdot\left\{\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right\}\\
&=\left(\frac{l_d+l_q}{2l_d l_q}I_2
- \frac{l_d-l_q}{2l_d l_q}\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}\right)
\cdot\left(\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right).
\end{aligned}
\tag{17}
$$

进一步简化后，可得 $i_{\alpha\beta}$ 为：

$$
i_{\alpha\beta}
= \frac{l_d+l_q}{2l_d l_q}\int u_{\alpha\beta}\,d\tau
+ l_1 - \frac{l_d-l_q}{2l_d l_q}l_2.
\tag{18}
$$

其中：

$$
l_1
= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}
\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}
\cdot\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F.
\tag{19}
$$

以及

$$
l_2
= \begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}
\cdot\int u_{\alpha\beta}\,d\tau.
\tag{20}
$$

利用三角恒等式 $\cos(\theta_1 - \theta_2) = \cos\theta_1\cos\theta_2 + \sin\theta_1\sin\theta_2$ 和 $\sin(\theta_1 - \theta_2) = \sin\theta_1\cos\theta_2 - \cos\theta_1\sin\theta_2$，式18中的 $l_1$ 项可简化为：

$$
\begin{aligned}
l_1
&= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}
\begin{pmatrix}\cos2\theta\cos\theta+\sin2\theta\sin\theta\\
\sin2\theta\cos\theta-\cos2\theta\sin\theta\end{pmatrix}i_F\\
&= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\\
&= -\frac{l_{md}}{l_d}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F.
\end{aligned}
\tag{21}
$$

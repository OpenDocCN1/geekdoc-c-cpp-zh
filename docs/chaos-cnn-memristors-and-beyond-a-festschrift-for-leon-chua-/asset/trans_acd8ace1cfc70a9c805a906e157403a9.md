

是状态的无记忆、非线性函数。如果所有的 $A_{kl}$ 均为零，则得到线性 CNN。

仅使用最近邻连接，两层线性 CNN 可以实现与 $\phi=0$ 的 Gabor 滤波器相似的滤波器，只是调制函数不是高斯，而是按拉普拉斯分布衰减。在一维情况下，滤波器核由下式给出

$$g(x)=\frac{\lambda}{2\alpha}\exp\left(-\frac{\lambda}{\alpha}|x|\right)\exp(j\Omega_xx)$$ (15)

虽然高斯函数在理论上具有吸引力，因为它们最小化不确定性关系，但多项研究表明，在实际应用中调制函数的确切形状并不关键。通过使用更大的模板半径，可以获得更接近高斯包络的近似。

两层架构的一个显著优势是，它使我们能够用纯最近邻连接的递归架构建立空间振荡的 RF 轮廓。用单层架构也可以获得类似的 RF 轮廓，但需要第二最近邻连接，并且只能表示该对中的一个成员 [18]。

图 3 显示了实现一维图像 Gabor 型滤波的双层线性 CNN 一个像素的电路。电容器 $v_e(n)$ 和 $v_o(n)$ 上的电压表示像素 $n$ 处两层的状态变量。一种

![](img/039e7d3c23390584a66737067db8b75_207_0.png)

Fig. 3. The circuit architecture for one pixel in a one dimensional array. Resistors are labeled by their conductances. Trapezoidal blocks denote transconductance amplifiers labeled by their gains. Unit capacitance between each node and ground is assumed for modelling purposes.

定义此网络 CNN 克隆模板的方法是按 $v(n)=v_e(n)+jv_o(n)$ 在每个像素处定义一个复值状态。我们得到一个具有复值克隆模板的单层 CNN。非零克隆模板由下式给出

$$B=[0\ 1\ 0]$$ (16)

$$C=[(G_{1x}+jG_{2x})\quad(-G_0-2G_{1x})\\(G_{1x}+jG_{2x})]$$ (17)

其中 $G_0$、$G_{1x}$ 和 $G_{2x}$ 为实值。或者，我们可以通过以下方式定义两层实值层之间的内部和层间模板

$$B_{ee}=B_{oo}=[0\ 1\ 0]$$ (18)

$$C_{ee}=C_{oo}=[G_{1x}\ (-G_0-2G_{1x})\ G_{1x}]$$ (19)

$$C_{eo}=C_{oe}=[-G_{2x}\ 0\ G_{2x}]$$ (20)

对于实值输入图像，我们可以将 $B_{oo}$ 设为零。滤波器参数与模板系数之间的关系为

$$\alpha^2=\sqrt{G_{1x}^2+G_{2x}^2}$$ (21)

$$\lambda^2=G_0+2G_{1x}-2\alpha^2$$ (22)

$$\Omega_x=\arctan(G_{2x}/G_{1x})$$ (23)

更近期的网络设计执行相同的滤波操作，但包含四层，其中成对的层表示正负半波整流滤波器输出，我们将其称为 ON 和 OFF 分量 [6]。尽管四层网络所需的硬件是双层网络的两倍，但这种 ON-OFF 表示在我们的设计中具有与生物学中相同的优势。在生物学中，ON-OFF 表示是节能的，因为静息信号对应于 ON 和 OFF 神经元上的小尖峰率。在我们的模拟电路中，静息信号对应于 ON 和 OFF 电路中的小电流。因此，该架构会自动将功率分配给活跃神经元，而活动较少的神经元耗散的功率很少。另一个优点是 ON-OFF 信号表示包括简单细胞模型的一部分的半波整流操作。

图 4 显示了四层网络中细胞之间的相互作用。我们用 $e+$、$e-$、$o+$ 和 $o-$ 来标记层，其中字母表示层实现的滤波器的对称性（偶或奇），+ 或 − 符号表示极性（ON 或 OFF）。非零克隆

![](img/039e7d3c23390584a66737067db8b75_208_0.png)

Fig. 4. Cell interconnections in a 1D version of the four layer network for Gabor-type filtering. The representation of the “e” and “o” layers of the two layer network is split across two layers representing the ON (+) and OFF (−) components. Interconnections terminating with filled circles are inhibitory. Interconnections terminating with open triangles are excitatory. Interconnections by resistors are implemented using the state feedback template. The mutually inhibitory interconnections between positive and negative layers of the same type are introduced by the output nonlinearity.

模板由下式给出

```
A_{e+o-} = A_{e-o+} = A_{o+e+}
= A_{o-e-} = [G_{2x} 0 0]  (24)
A_{e+o+} = A_{e-o-} = A_{o+e-}
= A_{o-e+} = [0 0 G_{2x}]  (25)
B_{e+e+} = B_{e-e-} = B_{o+o+}
= B_{o-o-} = [0 1 0]  (26)
C_{e+e+} = C_{e-e-} = C_{o+o+} = C_{o-o-}
= [G_{1x} (-G_0 - 2G_{1x}) G_{1x}]  (27)
```

这里我们假设输入图像为复值，其中输入的实部和虚部使用 ON-OFF 表示编码，每种表示都与相应的 CNN 层相关联。双层网络中负模板系数通过 ON 和 OFF 层之间的兴奋性连接实现。ON 和 OFF 层的输出等于其状态的正负半波整流之差

```
y_{e+} = |v_{e+} - v_{e-}|^+  (28)
y_{e-} = |v_{e+} - v_{e-}|^-  (29)
```

```
y_{o+} = |v_{o+} - v_{o-}|^+  (30)
y_{o-} = |v_{o+} - v_{o-}|^-  (31)
```

其中 |x|^+ = max{x, 0} 且 |x|^- = min{x, 0}。该输出非线性通过去除其状态中的共模分量来耦合 ON 和 OFF 层。这对于确保阵列的稳定性很重要，因为所有层间连接都是兴奋性的。

单眼神经元视网膜定位阵列的硬件实现已报道，这些神经元调谐到不同的方向，如图 2 的左侧和右侧列所示。通过将硅视网膜的输出扇出到不同的芯片，可以获得调谐到不同方向的神经元的视网膜定位阵列。每个芯片都相同，包含一个四层网络，阵列中有 32 × 64 个神经元，采用 0.25 um CMOS 工艺 [6]。它们通过对每个芯片施加不同的外部偏置电压来调谐到不同的方向。该网络的模拟处理组件使用工作在弱反转的晶体管实现，以实现最大能量效率。

在此实现中，芯片内的神经元活动使用硅积分和放电神经元阵列进行尖峰编码，并在芯片之间使用地址事件表示协议 AER 进行通信，AER 是一种异步数字协议，通过将尖峰神经元的地址放在数字总线上来在芯片的神经元阵列中发出尖峰 [14]。地址出现在总线上的时间直接编码尖峰时间。同步尖峰由仲裁器处理，授予总线的顺序访问。虽然这会引入一些尖峰时间的抖动，但由于现代电子电路的速度很高，这种抖动的幅度约为几十纳秒，因此与生物神经元的时间常数相比可以忽略不计。在输入侧，数字总线上出现的地址会导致向阵列中相应神经元的输入提供尖峰（电流脉冲）。当我们使用这种基于尖峰的通信方案时，ON-OFF 信号表示是有利的，因为神经元的静息尖峰率很低，这减少了数字总线上的流量。从硅视网膜到不同芯片的尖峰扇出使用包含在每个 Gabor 型滤波芯片上的路由电路实现 [16]。

图 5 显示了用于单眼方向选择性滤波的 CNN 架构的多芯片实现，以及系统的测量数据。输入由 [25,26] 中描述的硅视网膜芯片提供。该实现包含 35,648 个模型神经元，分布在五个芯片上。不同芯片上的神经元在连续时间内相互作用，并通过 AER 传输的尖峰进行通信。在每个芯片内，神经元在连续时间内相互作用，但通过作为电流编码的等级活动进行。

由于 CNN 阵列的连续时间操作和异步通信协议，我们已经能够实现为同一视网膜位置服务的神经元之间的反馈相互作用，但具有不同的方向调谐，即使这些神经元位于不同的芯片上 [7]。这些反馈相互作用增强了神经元的方向选择性。

图 2 所示的单眼处理链的下一阶段是对时间进行滤波，以建立对时间频率和运动方向的选择性。如前一节所述，由于我们同时计算空间滤波器的两个相位正交输出，因此所需的时空滤波器在空间和时间上是可分离的。这意味着所需的 CNN 阵列由解耦的单元组成，其中每个单元构造为


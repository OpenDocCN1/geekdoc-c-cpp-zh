

![](img/039e7d3c23390584a66737067db8b75b_551_0.png)

图 14. Volterra 结果（虚线）与数值计算曲线之间的比较。对于所有量，Volterra 方法都能给出良好的近似值。如预期，Volterra 结果无法再现电路的瞬态行为。

对于每种特定的参数设置。未来计划将当前方法扩展到具有任意数量忆阻器的电路。

## 参考文献

- [1] Boyd, S., Tang, Y. and Chua, L. (1983). 测量 Volterra 核，*IEEE Transactions on Circuits and Systems* **30**, 8, pp. 571–577。
- [2] Cai, W., Ellinger, F., Tetzlaff, R. and Schmidt, T. (2011a). 基于非线性离子漂移模型的二氧化钛忆阻器的 Abel 动力学，提交至 *IEEE Transactions on Circuits and Systems*，arXiv:1105.2668。
- [3] Cai, W., Schmidt, T., Joerges, U. and Ellinger, F. (2011b). 一种反馈自旋阀忆阻系统，提交至 *IEEE Transactions on Circuits and Systems*，arXiv:1104.5518。
- [4] Chua, L. O. (1971). 忆阻器——缺失的电路元件，*IEEE Trans. Circuit Theory* **18**, 5, pp. 507–519, URL http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=1083337。
- [5] Chua, L. O. and Kang, S. M. (1976). 忆阻器件与系统，*Proc. IEEE* **64**, 2, pp. 209–223, http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=1454361。
- [6] Corinto, F., Ascoli, A. and Gilli, M. (2011). 忆阻器振荡器的非线性动力学，*IEEE Trans. Circuits Syst.* **58**, 6。
- [7] Drakakis, E. M., Yaliraki, S. N. and Barahona, M. (2010). 忆阻器与 Bernoulli 动力学，载于 *2010 12th International Workshop on Cellular Nanoscale Networks and their Applications (CNNA)*，http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5430324。
- [8] Erokhin, V. (2010). 有机忆阻器：基本原理，载于 *Proceedings of 2010 IEEE International Symposium on Circuits and Systems (ISCAS)*，pp. 5–8，http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5537145。
- [9] Joglekar, Y. N. and Wolf, S. J. (2009). 难以捉摸的忆阻器：基本电电路的特性，*European Journal of Physics* **30**, 4, pp. 661–675，http://iopscience.iop.org/0143-0807/30/4/001。
- [10] Schetzen, M. (1985). 非线性网络的多线性理论，*Journal of the Franklin Institute* **320**, 5, pp. 221–247，http://linkinghub.elsevier.com/retrieve/pii/0016003285900237。
- [11] Schmidt, T., Feldmann, U., Neudeck, W. and Tetzlaff, R. (2011). 单忆阻器电路的解析方法，载于 *Proc. of the European Conference on Circuit Theory and Design (ECCTD2011)*，pp. 93–96。
- [12] Strukov, D., Borghetti, J. and Williams, R. (2009). 薄膜半导体忆阻行为的耦合离子与电子传输模型，*Small* **5**, 9, pp. 1058–1063。
- [13] Strukov, D. B., Snider, G. S., Stewart, D. R. and Williams, R. S. (2008). 发现缺失的忆阻器，*Nature* **453**, 7191, pp. 80–83，http://www.nature.com/nature/journal/v453/n7191/full/nature06932.html。
- [14] Ventra, M. D., Pershin, Y. V. and Chua, L. O. (2009). 具有记忆的电路元件：忆阻器、忆容和忆感，*Proc. IEEE* **97**, 10, pp. 1717–1724，http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5247127。
- [15] Wang, X., Chen, Y., Xi, H., Li, H. and Dimitrov, D. (2009). 通过自旋扭矩诱导的磁化运动的自旋电子忆阻器，*IEEE Electron Device Lett.* **30**, 3, pp. 294–297，http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=4781542。
- [16] Williams, S. (2010). 第二届忆阻器与忆阻系统研讨会演讲，伯克利。

## 第 44 章

## 硬件忆阻器仿真器

Andrew L. Fitch 和 Herbert H. C. Iu

电气、电子与计算机工程学院，
西澳大利亚大学

Chi K. Tse

电子与信息工程系，
香港理工大学

本章回顾了若干近期使用模拟和微处理器电路建模忆阻系统的最新方法。由于忆阻器尚未以任何形式进入市场，这些仿真电路为研究人员开发忆阻系统的应用提供了有效的平台。

- 1. 引言 ................................................. 540
- 2. 忆阻器建模电路 ....................................... 541
  - 2.1. 基于 JFET 的磁控 MMC ...................................... 541
  - 2.2. 脉冲控制微处理器基于 MMC ....................... 541
  - 2.3. 即插即用 MMC .................................................. 542
  - 2.4. 用于混沌电路的忆阻系统 ........................... 542
  - 2.5. 基于光敏电阻的实用应用 MMC .. 543
- 3. 结论 ........................................................... 546
- 参考文献 .............................................................. 546

## 1. 引言

本章考察了若干近期使用模拟和微处理器电路建模忆阻系统的最新方法。自从惠普公司于 2008 年宣布成功制造忆阻器 [1] 以来，研究人员开发了若干电路来观察忆阻行为，无论是作为独立现象还是作为组件在实际应用中。

开发功能性忆阻器模型对于探索该新元件的特性和开发其应用而言至关重要，如果不是必不可少的话。目前，忆阻器尚未以任何形式进入市场。希望，尽管没有迹象表明会发生，未来某个时候忆阻器将作为通孔或表面贴装的双端器件提供。这将极大地促进应用开发和原型制作。很少有人愿意等待这种情况发生，而现在，所有关于开发忆阻系统应用和了解忆阻器的研究都必须使用基于电路和数学的模型进行。

## 2. 忆阻器建模电路

在本节中，将考察若干提出的忆阻器建模电路（MMC）。

### 2.1. 基于 JFET 的磁控 MMC

Valsa *et al.* [2] 于 2010 年开发了一种磁控 MMC。该电路旨在通过观察忆阻器对不同输入信号的响应来获得关于忆阻器特性的理论概念的证明。电路使用 JFET 提供电压控制电导（$G_M$）和基于运算放大器的积分器来获得表示磁通的电压（$v_\phi$），该电压用于控制 $G_M$。响应于适当频率和幅度的输入正弦信号，电路能够观察到通过零的特征滞后环。

由于使用积分器子电路来获得对应于磁通的电压，电路在频率方面的运行区域限制为低于 5 Hz 的信号。该区域可以通过改变电阻 $R$ 或电容 $C$ 的值来调整，以改变如图 1 所示积分器的 $RC$ 关系，从而适用于更高频率的输入信号，但运行区域的宽度仍将保持相似。

该电路不能用于在功能电路中仿真忆阻器；它旨在在一个实验环境中观察忆阻行为，而非实际应用。

### 2.2. 脉冲控制微处理器基于 MMC

Pershin 和 Ventra [3] 于 2010 年开发了一种可编程模拟电路。该电路从完全不同的方向接近合适的忆阻器仿真器的设计。

![](img/039e7d3c23390584a66737067db8b75b_553_0.png)

该方法基于以下概念。薄膜 TiO₂ 忆阻器并不表现得像理想忆阻器；其行为并不理想且相当复杂 [3, 4]。Pershin 和 Ventra 选择使用脉冲串来设置忆阻器的状态，然后使用低电压模拟信号进行实际信号处理。这利用了忆阻器中观察到的阈值行为，其中较大的信号会改变器件的电导，而更小的信号可以通过且无或可忽略的影响 [4, 5]。

![](img/039e7d3c23390584a66737067db8b75b_553_1.png)

图 2 所示的框图显示电路包含微处理器、模数转换器（ADC）和数字电位器。电路工作时 ADC 将模拟信号转换为其二进制等价物并提供给微处理器。微处理器随后将数字电位器设置为所需电阻值。根据 Pershin 和 Ventra [3]，微处理器被编码为根据以下公式处理信号

$$
I(t) = R_M^{-1}(x, V_M, t) V_M(t),
\tag{1}
$$

$$
\dot{x} = f(x, V_M, t),
\tag{2}
$$

其中 $x$ 是表示 $n$ 个内部状态变量的向量，$R_M$ 是记忆电阻，$R_M^{-1}$ 是其倒数，即记忆电导 [3]。在 Valsa *et al.* [2] 中，已指出使用数字系统仿真模拟元件的缺点是等效数字信号的分辨率有限以及数字电位器的物理特性。考虑到所使用的数字电位器是 256 位 10 kΩ 类型 [3]，这将导致 39 Ω 的步进，该评论是可以证明的。电路还受限于 ADC 采样频率 1 kHz，这意味着施加到电路上的工作信号应最多为 50 Hz，理想情况下小于 10 Hz [3]。


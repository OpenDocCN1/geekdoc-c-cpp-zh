

其时域动态执行了所需的时域滤波操作。

四层 CNN 单元可用于实现由式 (11) 给出且 α = 1 的复值时域滤波器 [22]。为了便于集成到多芯片网络中，该单元电路接收并产生四个脉冲编码信号，表示输入和输出的实部和虚部的 ON 和 OFF 分量。每个像素处空间滤波芯片的四个输出可以直接连接到 CNN 时域滤波单元阵列的对应输入，以实现具有式 (6) 给出的时空感受野的时空滤波器。

图 4 显示了四层时域滤波单元的输入、状态和输出之间的关系。该单元中输入与输出之间的关系与四层方向选择性滤波阵列中单元所使用的关系相同，如式 (28)-(31) 所示。时域滤波阵列的非零克隆模板由下式给出

```
A_{o+e+} = A_{e-o+} = A_{o-e-} = A_{e+o-} = [β]  (32)
B_{e+e+} = B_{e-e-} = B_{o+o+} = B_{o-o-} = [1]  (33)
C_{e+e+} = C_{e-e-} = C_{o+o+}
      = C_{o-o-} = [-1]  (34)
```

输出反馈克隆模板中的 β 值与式 (5) 中的滤波器中心频率 Ω_t 之间的关系为 Ω_t = β/τ。

该单元电路已按 [22] 中所述在 1.5μm CMOS 工艺中实现。时间常数 τ 和空间频率调谐 Ω_t 可通过外部施加的偏置电压进行调节。内部，脉冲序列被积分以产生连续变化的电流，这些电流使用由工作在弱反型区的 CMOS 晶体管构成的对数域滤波电路进行滤波，其中低电流水平使我们能够获得数量级为数十赫兹的调谐和时间常数，与真实皮层细胞的时域频率调谐一致。

图 2 所示 CNN 架构的最后一步是组合单眼响应以创建对双眼视差选择性的神经元。根据 (12)，这可以在每个空间位置单独完成。因此，实现视差选择性细胞的 CNN 阵列由四个层单元阵列组成，这些单元在空间上和层间都是解耦的。CNN 动态简化为每个层和空间位置的泄漏积分。

![](img/039e7d3c23390584a66737067db8b75b_210_0.png)

图 6. 实现用于成像皮层神经元运动选择性的时域滤波器的四层 CNN 单元的输入、状态和输出之间的关系。内部，所有信号均由电流表示。外部，信号编码为电压脉冲序列（用三个脉冲表示）。尖峰神经元模块（SN）将电流转换为电压脉冲。脉冲发生器模块（PG）将电压脉冲转换为电流脉冲。标记为 1/(τs+1) 的模块为泄漏积分器。

这些细胞的视差选择性并非通过改变 CNN 阵列的动态来调节，而是通过改变组合来自两只眼睛的输出来调节。根据 (13)，视差调谐可以通过在两个单眼感受野之间引入位置偏移或相位偏移来改变。由于来自不同位置和不同相位的神经元输出都编码在单个 AER 总线上，我们可以使用地址重映射电路来选择不同的单眼输出组合，从而改变视差调谐。位置偏移可以通过向来自左眼或右眼方向选择性滤波芯片的脉冲的地址添加水平偏移来实现。相位偏移可以通过改变左眼和右眼方向选择性芯片在每个像素处的四个滤波输出的组合方式来实现。为了实现零相位偏移，左眼和右眼在每一层对应的输出被组合，即左眼 e+ 输出与右眼 e+ 输出组合，依此类推。为了实现 -90° 相位偏移，左眼 e+（e−）输出与右眼 o+（o−）输出组合

![](img/039e7d3c23390584a66737067db8b75b_211_0.png)

(a)

![](img/039e7d3c23390584a66737067db8b75b_211_1.png)

(b)

图 7. (a) 视差调谐神经元的多芯片实现的照片。两个 AER 视网膜提供了系统对左眼和右眼输入的模拟。插入板将硅视网膜使用的 AER 地址格式转换为 Gabor 型芯片使用的格式。然后左眼和右眼输入由调谐到垂直方向的方向选择性神经元处理。然后将左眼和右眼方向调谐神经元的输出组合以产生调谐到双眼视差的神经元。(b) 测量的双眼调谐曲线显示为图像，其中像素的灰度编码了复细胞对聚焦到左眼和右眼芯片上的成对空间条刺激的响应。每个位置表示在左眼和右眼特定位置呈现的输入的放电率。较暗的灰度表示较高的放电率。(A, D) 通过相位和位置编码调谐到负视差的神经元的调谐曲线。(B) 对应于不同视差的地图区域。(C, F) 通过相位和位置编码调谐到正视差的神经元的 RF 地图。(E) 调谐到零视差的神经元的时序曲线，该曲线对位置和相位编码相同。

和左眼 o+（o−）输出与右眼 e−（o+）输出组合。

在 [23] 中，我们描述了此类脉冲重映射电路的构建，并给出了通过位置和相位偏移调谐到不同视差的神经元的测量结果。图 7 显示了系统的照片，以及系统通过将两个显示器的输出聚焦到代表左眼和右眼的硅视网膜上呈现图像时测量的视差调谐曲线。

## 4. 总结

我们描述了一种统一的 CNN 架构，可用于构建硅神经元，以模拟视觉皮层神经元在六个刺激维度上的多维选择性。该 CNN 架构的可行性已通过使用全定制混合模拟数字电路构建的工作硬件原型得到验证。为了支持神经元之间完全连续时间交互并允许实时反馈的可能性，该架构可以通过将计算分布到多个芯片上来实现，每个芯片包含多层 CNN 阵列并通过类似于神经动作电位（脉冲）的电压脉冲进行通信。

## 参考文献

- [1] Adelson and Bergen (1985). Spatiotemporal energy models for the perception of motion, Journal Optical Society of America A, Vol. 2, pp. 284–299.
- [2] A. Anzai, I. Ohzawa, and R. D. Freeman (1999a). Neural mechanisms for processing binocular information I. Simple cells, Journal of Neurophysiology, Vol. 82, pp. 891–908.
- [3] A. Anzai, I. Ohzawa, and R. D. Freeman (1999b). Neural mechanisms for processing binocular information II. Complex cells, Journal of Neurophysiology, Vol. 82, pp. 909–24.
- [4] A. Anzai, I. Ohzawa, and R. D. Freeman (1999c). Neural mechanisms for encoding binocular disparity: receptive field position versus phase, Journal of Neurophysiology, Vol. 82, pp. 874–90.
- [5] Y. Chen, Y. Wang, and N. Qian (2001). Modeling V1 disparity tuning to time-varying stimuli, Journal of Neurophysiology, Vol. 86, pp. 143–55.
- [6] T. Y. W. Choi, B. E. Shi, and K. Boahen (2004). An ON-OFF Orientation Selective Address Event Representation Image Transceiver Chip, IEEE Transactions on Circuits and Systems-I: Fundamental Theory and Applications, Vol. 51, no. 2, Feb.
- [7] T. Y. W. Choi, P. Merolla, J. Arthur, K. Boahen, and B. E. Shi (2005). Neuromorphic implementation of orientation hypercolumns. IEEE Transactions on Circuits and Systems-I: Regular Papers, Vol. 52, no. 6, pp. 1049–1060, Jun.
- [8] L. O. Chua and L. Yang (1988). Cellular neural networks: Theory, IEEE Transactions on Circuits and Systems, Vol. 35, pp. 1257–1272, Oct.
- [9] J. G. Daugman (1980), Two-dimensional spectral analysis of cortical receptive field profiles, Vision Research, Vol. 20, pp. 847–856.
- [10] R. Van Ee and B. L. Anderson (2001). Motion direction, speed and orientation in binocular matching, Nature, Vol. 410, pp. 690–694.
- [11] W. S. Geisler and D. G. Albrecht (1997). Visual cortex neurons in monkeys and cats: Detection, discrimination, and identification, Visual Neuroscience, Vol. 14, pp. 897–919.
- [12] D. H. Hubel and T. N. Wiesel (2001). Receptive fields, binocular interaction and functional architecture in the cats visual cortex, Journal of Physiology, Vol. 160, pp. 106–154.
- [13] J. P. Jones and L. A. Palmer (1987). An evaluation of the two-dimensional Gabor filter model of simple receptive fields in cat striate cortex, Journal of Neuroscience, Vol. 58, pp. 1233–1258.
- [14] M. Mahowald (1994). An Analog VLSI System for Stereoscopic Vision. Kluwer Academic Publishers.
- [15] S. Marceljia (1980). Mathematical description of the responses of simple cortical cells, Journal Opt. Soc. Am., Vol. 70, pp. 1297–1300.
- [16] P. Merolla, J. Arthur, B. Shi and K. Boahen (2007). Expandable networks for neuromorphic chips, IEEE Transactions on Circuits and Systems-I: Regular Papers, Vol. 54, no. 2, pp. 301–311, Feb.
- [17] I. Ohzawa, G. C. DeAngelis, and R. D. Freeman (1990). Stereoscopic depth discrimination in the visual cortex: Neurons ideally suited as disparity detectors, Science, Vol. 249, pp. 1037–1041.
- [18] L. Raffo (1995). Resistive network implementing maps of Gabor functions of any phase, Electronics Letters, Vol. 31, no. 22, pp. 1913–1914, Oct.
- [19] T. Roska and L. O. Chua (1993). “The CNN Universal Machine: An analogic array computer,” IEEE Transactions on Circuits and Systems-II, Vol. 40, no. 3, pp. 163–173.
- [20] B. E. Shi (1998). Gabor-type filtering in space and time with cellular neural networks, IEEE Trans. Circuits and Systems-I: Fundamental Theory and Applications, Vol. 45, no. 2, pp. 121–132, Feb.
- [21] B. E. Shi (2000). A low power orientation selective vision sensor, IEEE Transactions on Circuits and Systems-II: Analog and Digital Signal Processing, Vol. 47, pp. 435–440.
- [22] B. E. Shi, E. K. C. Tsang and P. S. P. Au (2006). An ON-OFF temporal filter circuit for motion energy computations, IEEE Transactions on Circuits and Systems-II: Express Briefs, Vol. 53, no. 9, pp. 951–955, Sep.
- [23] E. K. C. Tsang and B. E. Shi (2004). A preference for phase-based disparity in a neuromorphic implementation of the binocular energy model, Neural Computation, Vol. 16, no. 8, pp. 1579–1600, Aug.


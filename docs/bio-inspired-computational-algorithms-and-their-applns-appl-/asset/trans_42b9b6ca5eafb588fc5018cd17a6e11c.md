
## 7. 结论

本文提出了一种有效的高功率同步电机谐波损耗最小化的替代方法。这些电机中提出的电流谐波模型取决于 d 轴和 q 轴的电感，即直轴和交轴电感。由于高功率应用是关注重点，找到在每个特定工作点具有最小损耗的全局最优解具有重要意义。对于具有指定特性的已识别典型电机，该问题被重新表述为优化任务，并通过遗传算法（GA）寻求最优脉冲模式以最小化总谐波电流畸变（THCD）。最优脉宽调制（PWM）波形可实现多达 12 次开关（每个 PWM 波形四分之一周期），其中对于超过此数量的开关角度，空间矢量 PWM（SVPWM）方法优于最优 PWM 方法。选择 GA 作为优化方法似乎完全可取，考虑到其主要特征能够克服确定性优化方法的不足，特别是在决策变量增加时，更有可能找到全局最优解，以及所提出目标函数的非线性和复杂性。

前述电感明显受工作点修改、老化和温度升高影响。因此，进行中的开关模式不再是全局最优模式，因此执行优化过程以从先前的识别程序结果中确定新的最优脉冲模式是必不可少的。开关模式的替换会引发不利的瞬态条件。电流谐波模型与其参数无关的感应电机的最优脉冲模式被应用于具有不同 i_q/i_d 值的同步电机的谐波模型。所提出方法的有效性值得注意，特别是在 i_q/i_d 值较大和高调制指数的情况下。

## 8. 致谢

作者感谢伍珀塔尔大学的 Joachim Holtz 教授对本研究中开发方法提出的恰当建议。

## 9. 参考文献

- Bäck, T.; Hammel, U. & Schwefel, H.-P. (1997). 进化计算：历史与现状评述. IEEE Transactions on Evolutionary Computation, Vol. 1, No. 1, April 1997, 3-17.
- Boldea, I. & Nasar, S. A. (1992). AC 驱动器的矢量控制, CRC Press, Boca Raton, FL.
- Bose, B. K. (2002). 现代电力电子技术与交流驱动, Prentice Hall, Upper Saddle River, NJ.
- Chiasson, J.; Tolbert, L. M.; McKenzie, K. & Du, Z. (2004). 谐波消除问题的完整解. IEEE Transactions on Power Electronics, Vol. 19, No. 2, March 2004, 491-499.
- Czarkowski, D.; Chudnovsky, D. V.; Chudnovsky, G. V. & Selesnick, I. W. (2002). 单相逆变器最优PWM问题的求解. IEEE Transactions on Circuits and Systems-I, Vol. 49, No. 4, April 2002, 465-475.
- Davis, L. (1991). 遗传算法手册, Van Nostrand Reinhold, New York.
- Eiben, Á. E.; Hinterding, R. & Michalewicz, Z. (1999). 进化算法中的参数控制. IEEE Transactions on Evolutionary Computation, Vol. 3, No. 2, July 1999, 124-141.
- Enjeti, P. N.; Ziogas, P. D. & Lindsay, J. F. (1990). 用于消除谐波的编程PWM技术：批判性评估. IEEE Transactions on Industry Applications, Vol. 26, No. 2, Mar./Apr. 1990, 302-316.
- Goldberg, D. E. (1989). 搜索、优化和机器学习中的遗传算法, Addison-Wesley, Reading, MA.
- Holtz, J. (1992). 脉宽调制综述. IEEE Transactions on Industrial Electronics, Vol. 39, No. 5, December 1992, 410-419.
- Holtz, J. (1995). 用复信号流图表示交流电机的动态特性. IEEE Transactions on Industrial Electronics, Vol. 42, No. 3, June 1995, 263-271.
- Leonhard, W. (2001). 电驱动控制, 3rd ed., Springer-Verlag, New York.
- Ljung, L. & Söderström, T. (1983). 递归辨识理论与实践, MIT Press, Cambridge, MA.
- Michalewicz, Z. (1996). 遗传算法 + 数据结构 = 进化程序, Springer-Verlag, New York.
- Mohan, N.; Undeland, T. M. & Robbins, W. P. (1995). 电力电子学：变换器、应用与设计, Wiley, New York.
- Rezazadeh, A. R.; Sayyah, A. & Aflaki, M. (2006). 用于离线最优PWM供电大功率同步电机的调制误差观测与调节, Proceedings of 1st IEEE conference on industrial electronics and applications, pp. 1300-1307, May 2006, Singapore.
- Sayyah, A.; Aflaki, M. & Rezazadeh, A. R. (2006). 基于GA的感应电机总谐波电流畸变优化及选定谐波抑制, Proceedings of international symposium on power electronics, electrical drives, automation and motion, pp. 1361-1366, Italy, May 2006, Taormina (Sicily).
- Sayyah, A.; Aflaki, M. & Rezazadeh, A. R. (2006). 使用遗传算法最小化大功率感应电机总谐波电流畸变的最佳PWM, Proceedings of SICE-ICASE international joint conference, Korea, pp. 5494-5499, October 2006, Busan.
- Sayyah, A.; Aflaki, M. & Rezazadeh, A. R. (2006). 使用遗传算法优化PWM逆变器的THD并抑制特定阶次谐波, Proceedings of IEEE international symposium on intelligent control, pp. 874-879, Germany, October 2006, Munich.
- Sun, J. (1995). 大功率电压源逆变器的最优脉宽调制技术, Thesis, University of Paderborn, Germany.
- Sun, J.; Beineke, S. & Grotstollen, H. (1996). 基于谐波消除方程实时求解的最优PWM. IEEE Transactions on Power Electronics, Vol. 11, No. 4, July 1996, 612-621.

## 第 3 部分

## 人工免疫系统与群体智能

## 人工免疫系统、动态适应度景观与变化检测问题

Hendrik Richter  
HTWK Leipzig University of Applied Sciences  
Germany

### 1. 引言

让生物过程、行为和结构启发问题求解算法和设备的设计，在过去几十年里一直是工程和应用科学中一个突出且持久的主题。在此背景下，仿生计算发挥了开创性的作用。诸如进化计算 (1; 8; 25)、人工免疫系统 (4; 6; 43)、膜计算 (29) 或群体系统 (9; 22) 等领域已走出襁褓阶段，并在理论基础和重要应用方面取得了进展。这些领域发展成当前形态的事实及其方式归因于三大主要发展：(i) 以数字计算机形式出现的廉价、快速且可靠的计算能力，(ii) 计算能力与算法方法实现相结合可创造出强大的问题求解器的认识，以及 (iii) 生物系统可以被富有成效地理解为信息处理单元，因而可经常用于计算和/或算法目的的见解。这一趋势当然不应与计算生物学混淆，但与之高度相关，并且如果没有生物学中向算法化和数学化的根本进展，可能是不可想象的，参见例如 (5; 16; 21; 38) 的最新讨论。在上述仿生计算领域中，进化算法和人工免疫系统发挥着独特作用，因为它们的历史特别悠久，且已达到的成熟度显著较高。在本文中，我们将使用这两种方案相结合来解决动态优化中最大跟踪与变化检测相互交织的问题。

为了通过进化计算成功解决动态优化问题，需要对标准算法结构进行补充，即通过维持和增强种群多样性的算子。这里的动态优化是指相关适应度景观的拓扑结构随时间变化。相当数量的这些用于多样性管理的算子（例如记忆方案、随机移民或超突变 (24; 26; 30; 33; 35; 39; 45)）只有在已知适应度景观变化发生的时间点时才能被触发并正常工作。因此，变化检测问题在解决动态优化问题中具有很高的实际相关性 (3; 19; 27)。

原则上，变化检测基于利用从适应度景观中提取的关于搜索空间中点适应度值的信息。这种信息的提取可以以两种方式进行。其中一种是使用进化算法的

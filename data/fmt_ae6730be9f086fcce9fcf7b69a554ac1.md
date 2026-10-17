
## C.3 信状态动力学

虽然我们不得不从有限状态空间 `$X$` 移动到单纯形 `$S$` 是遗憾的，但幸运的是价值函数具有简单的结构：通过归纳法可以证明，`$V_n$` 作为 `$b \in S$` 的函数是凹的且分段线性的 [201, 326]。我们可以正确地得出结论，`$H^*$` 同样作为 `$b$` 的函数是凹。这为近似动态规划或强化学习的简单近似架构打开了大门。

下一节包含命题 C.1 的证明。

## C.3 信状态动力学

这些笔记的完整详细介绍可以在 Hajek 的书 [154] 或 Van Handel 的《隐马尔可夫模型讲义》[362] 中找到。然而给出信状态转移律的命题 C.1 较难找到（这通常被认为是理所当然的）。记得 `$(X, Y)$` 被视为具有 (C.5) 中给出转移律的 MDP 模型的状态过程。这种表示法对我们的目的来说太复杂。我们感兴趣的是构造一个递归算法来生成信状态——这是一个关于 `$x$` 的函数，因此我们抑制了观测的作用。对于每个 `$n$`，观测到的量 `$y_n = Y_n$` 和 `$u_{n-1} = U_{n-1}$`，用 (C.5) 的符号表示：

$$\rho_n(x_n | x_{n-1}) = p(x_n | x_{n-1}, u_{n-1})q(y_n | x_n),$$

其中理解 `$x_{n-1}$` 和 `$x_n$` 是变量。相比之下，(C.12) 中出现的 `$y_n$` 和 `$u_{n-1}$` 不是变量。它们是观测值。

我们首先考虑一个（看似更复杂的问题：给定序列 `$x^n \in X^{n+1}$`，我们想要找到 `$X_0^n \triangleq (X_0, \dots, X_n) = x_0^n$` 的条件概率，记为

$$\beta_n(x_0^n) = P\{X_0^n = x_0^n | Y_n\}$$

这被称为平滑问题，因为我们希望在给定当前观测值的情况下估计过去的状态。输出和输入序列 `$u_0^{n-1}, y_0^{n-1}$` 使用贝叶斯规则得到：

$$\beta_n(x_0^n) = P\{X_0^n = x_0^n | Y_n = y_0^n, U_{n-1} = u_0^{n-1}\} = \frac{P\{X_0^n = x_0^n, Y_n = y_0^n, U_{n-1} = u_0^{n-1}\}}{P\{Y_n = y_0^n, U_{n-1} = u_0^{n-1}\}}$$

分母可以视为归一常数（它不依赖于 `$x_0^n$`）。令 `$\beta_n^*$` 表示分子得到：

$$\beta_n^*(x_0^n) = P\{X_0^n = x_0^n \text{ and } Y_n = y_0^n, U_{n-1} = u_0^{n-1}\} = \rho_n(x_n | x_{n-1}) \times \dots \times \rho_1(x_1 | x_0) \times \mu(x_0),$$

其中 `$\mu$` 定义了 `$X_0$` 的分布。

这对任何 `$n$` 都成立，因此我们得到了一个递归关系。

$$\beta_n^*(x_0^n) = \rho_n(x_n, x_{n-1})\beta_{n-1}^*(x_0^{n-1}).$$

## 414 部分观测与信状态

我们通过归一化得到 `$\beta_n$`，因为我们知道它是概率质量函数（pmf）：

$$\beta_n(x_0^n) = \kappa_n \beta_n^*(x_0^n), \quad \kappa_n^{-1} = \sum_{x_0, \dots, x_n} \beta_n^*(x_0, \dots, x_n).$$

原始问题呢？我们再次使用贝叶斯规则：

$$b_n(x_n) = P\{X_n = x_n | Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}\} = \frac{P\{X_n = x_n, Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}\}}{b_n^*(u_n^1)}.$$

分子记作 `$b_n^*(x_n)$`，从 `$\beta_n^*$` 得到：

$$b_n^*(x_n) = P\{X_n = x_n | Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}\}.$$

应用 (C.13) 得到未归一化信状态的递归公式：

$$\beta_n^*(x_n) = \sum_{x_0, \dots, x_{n-1}} \rho_n(x_n | x_{n-1}) \beta_{n-1}^*(x_0, \dots, x_{n-1}) = \sum_{x_0, \dots, x_{n-1}} \rho_n(x_n | x_{n-1}) \left[ \sum_{x_0, \dots, x_{n-2}} \rho_{n-1}(x_{n-1} | x_{n-2}) \beta_{n-2}^*(x_0, \dots, x_{n-2}) \right].$$

由此，我们得到线性动力学：

$$b_n^*(x') = \sum_{x} \rho_n(x' | x) b_{n-1}^*(x), \quad n \geq 1, x' \in X.$$

根据命题 C.3，得到命题 C.1 中给出的信状态转移矩阵。

## 命题 C.3 (非线性) 信状态动力学是非线性的：

$$beta_n(x') = \kappa_0 \mu(x')q(Y_0 | x').$$

$$\beta_n(x') = M(b_{n-1}, Y_n, U_{n-1}) = \kappa_n \sum_{x} \rho_n(x' | x) b_{n-1}(x), \quad x' \in X, n \geq 1.$$

其中 `$\rho_n$` 在 (C.12) 中定义，`$\kappa_n$` 由约束 `$\sum_{x} b_n(x) = 1$` 确定。

## 参考文献

[1] A. Agarwal and O. Dekel. 多点反馈在线优化最优算法。Proc. COLT, 28–40, 2010.
[2] A. Agarwal, S. M. Kakade, J. D. Lee, and M. Mahajan. 马尔可夫决策中的策略梯度最优性和近似。Proc. COLT, 64–66, 2020.
[3] R. Agrawal. 多臂老虎机的样本均值策略 $O(\log n)$。Advances in Applied Probability, 1054–1078.
[4] V. M. Alekseev. 常微分解扰动的估计（俄文）。Vestnik Moskov. Ser., 28–36, 1961.
[5] F. Alvarez, H. Attouch, J. Bolte, and P. Redont. 带 Hessian 阻尼的二阶梯度耗散系统：用于优化和力学。Journal de mathématiques appliquées, 18(4):771–779, 2002.
[6] S. I. Amari and S. C. Douglas. 为什么自然梯度？ICASP 98, volume 2, 1213–1216. IEEE, 1998.
[7] B. D. Anderson and J. Moore. 最优控制：线性二次方法。Prentice Hall, Englewood Cliffs, NJ, 1990.
[8] L. L. Andrew, M. Lin, and A. Wiedman. 扩展中的最优性、公平性和鲁棒性。SIGMETRICS Conference, Ev. Rev., 38(1):37–48, 2021.
[9] O. Ansche, N. Baer, and N. Shukin. 平均 DQN：深度强化学习的简化与稳定。Proc. ICML, 176–185. JMLR.org, 2017.
[10] A. Apostolacos, V. Bouskar, E. Fernandez-Gauchart, M. Ghosh, and S. I. Marcus. 平均成本的离散控制马尔可夫过程。SIAM Journal Control Opt., 31:282–344, 1993.
[11] K. B. Ayrium and M. Kris. 极值控制实时估计。John Wiley & Sons, Inc., New York, NY, 2003.
[12] S. Asussen and P. W. Glyn. 随机仿真：算法与分析。Stochastic Modeling and Applied Probability, 57. Springer-Verlag, New York, NY, 2007.
[13] K. J. Åström. 完整信息马尔可夫过程的最优控制。J of Mathematical Analysis and Applications, 10:174–205, 1965.
[14] K. J. Åström and K. Furita. 能量控制摆摆。Automica, 36(2):287–295, 2000.
[15] K. J. Åström and R. M. Murray. 反馈系统：科学家与工程师导论。Princeton University Press, Princeton, NJ, 2nd ed., 2010.
[16] H. Attouch, X. Goud. 重球摩擦法，第一部分：连续系统：通过耗散系统的渐近分析对实值函数局部极值的全局探索。Communications in Contemporary Mechanics, 2(01):1–34, 2000.
[17] P. Auer, N. Cesa Bianchi, and P. Fischer. 多臂老虎机的有限时间分析。Machine Learning, 47(2-3):235–256, 2002.
[18] M. G. Azar, R. Munos, M. Ghavamzadeh, and H. Kappen. 速度学习。Proc. Advances in Neural Information Processing Systems, 2411–2411.
[19] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[20] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[21] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[22] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[23] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[24] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[25] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[26] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[27] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[28] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[29] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.
[30] F. Batch, S. Meyer, and N. Shukin. Speed-learning. JMLR.org, 2017.

# 参考文献

[44] D. Bertsekas 和 J. N. Tsitsiklis 神经动态规划（Neuro-Dynamic Programming）。Athena Scientific, Cambridge, MA, 1996.
[45] D. P. Bertsekas 编程与最优控制，第二卷。Athena Scientific, Belmont, MA, 第 4 版, 2012.
[46] D. Bertsekas 动态规划与最优控制，第一卷。Athena Scientific, Belmont, MA, 第 4 版, 2017.
[47] D. Bertsekas 强化学习与最优控制。Athena Scientific, Belmont, MA, 2019.
[48] J. Bhandari 和 D. Russo, 策略梯度方法的全局最优性。arXiv 预印本：1906.01786, 2019.
[49] J. Bhandari, D. Russo 和 R. Singal. 线性函数近似下时间差学习的有限时间分析。Proc. COIT, 1691–1692, 2018.
[50] S. Bhatnagar 同步扰动与有限差分法。Wiley 运筹学与管理百科，https://openlibrary.wiley.com/doi/10.1002/9780740005351.ecorm0784, 2010.
[51] S. Bhatnagar 和 V. S. Borkar. 用于仿真优化的多尺度混沌 SPSA 和平滑函数算法。79(6):588–580, 2003.
[52] S. Bhatnagar, M. C. Fu 和 I-J. Wang. 使用确定扰动序列的双时间同步随机优化。ACM 建模与计算机系统事务 (TACS), 13(2):180–209, 2003.
[53] S. Bhatnagar, M. Ghavandzadeh, M. Lee 和 R. S. Sutton. 自然演员-评论算法。Proc. 神经信息处理系统进展（NeurIPS），页 105–112, 2008.
[54] S. Bhatnagar, H. Prasad 和 L. Prashanth. 优化的递归算法扰动方法：控制与信息科学讲义。Springer, London, 2013.
[55] S. Bhatnagar, D. Precup, J. R. Sutton, H. R. Mai 和 C. Szepesvari. 带平滑随机近似的收敛时间差学习。Advances 神经信息处理系统进展（NeurIPS），页 1204–1211, 2009.
[56] S. Bhatnagar, R. S. Sutton, M. Ghavandzadeh 和 M. Lee. 自然演员-评论算法。Automata, 45(11):2471–2482, 2009.
[57] C. M. Bishop. 模式识别与机器学习。Springer, 2006.
[58] J. R. Blum, 多维随机近似法。数学统计学杂志，25(4):733–744, 1954.
[59] V. Borkar 和 S. P. Mey 用于图聚类的 Oja 算法、马尔可夫谱分解和风险敏感控制。Automata, 48(10):2521–2519, 2012.
[60] V. Borkar 和 P. Paravaya. 马尔可夫链的自适应控制；i：有限参数集。IEEE 自动控制事务，24(6):953–957, 1979.
[61] V. Borkar 和 P. Paravaya. 马尔可夫链的识别与自适应控制。SIAM 控制与优化期刊，20(4):470–489, 1982.
[62] V. Borkar. 马尔可夫链的识别与自适应控制。博士论文，加利福尼亚大学伯克利分校，1989.
[63] V. Borkar. 决策过程中的凸分析。《马尔可夫决策过程手册》，国际运筹学与管理科学第 00 卷，页 347–375。Kluer 出出版社，Boston, MA, 2002.
[64] V. Borkar. 强化学习——数值方法与马尔可夫链蒙特卡洛之间的桥梁。由 N. S. S. Batry, B. Raejev, M. Deladeep 和 T. S. R. K. Rao 编，《数学科学视角》，页 71–91。World Scientific, Singapore, 2009.
[65] V. Borkar. 随机近似：动力系统视角。Hindustan Book Agency 和剑桥大学出版社（联合出版），印度德里，及英国剑桥，2008.
[66] V. Borkar. 随机近似：动力系统视角（第 2 版，即将出版）。Hindustan Book Agency, 印度德里，及英国剑桥，2020.
[67] V. Borkar 和 G. Gaurat. 长期平均最优控制问题的线性规划。优化理论与应用期刊，181(1):101–125, 2019.
[68] V. S. Borkar, V. Gaitsgory 和 I. Shvartmans. 离散时间长期最优控制问题的 LP 公式化：遍历性学情况。SIAM 控制与优化期刊，57(3):1877–1818, 2019.
[69] V. S. Borkar 和 S. P. Mey. 随机近似收敛的 ODE。SIAM 控制与优化期刊，38(2):447–469, 2000.
[70] J. A. Boyan. 技术更新：最小二差时间差学习。Machine Learning，49(2-3):233–246, 2002.
[71] S. Boyd, L. Ghaoui, E. Perez 和 V. Balakrishnan. 控制理论中的线性不等式。SIAM, 1994.
[72] S. Boyd, N. Parikh 和 E. Chu 通过乘子交替法进行分布式优化。Multipliers Publishers, Norfolk, MA, 2011.
[73] S. Boyd 和 L. Vandenberg. 凸优化，第 1 版，剑桥大学出版社，纽约，2004.
[74] S. Bradley, Y. Dystkie 和 A. Bart. 使用策略迭代的自适应二次控制。美国会议，第 3 卷，页 3475–3479, 1994.
[75] S. J. Bradley 和 A. G. Bart. 时间差学习的最小二差算法。Machine Learning，22(1-3):33–57, 1996.
[76] W. L. Rogan. 现代控制理论。Pearson, 第 3 版,1990.
[77] J. Abu, Mesbari, M. Fazel. 通过一阶方法的 LQR：离散时间情况。arXiv 预印本，arXiv:1907.08291, 2019.
[78] S. Subek 和 N. Cesa-Bianchi. 随机与多臂老虎机的稳健性分析。Machine Learning，5(1):1–22, 2002.
[79] J. C. Sutton. 常微分方程的数值方法。Wiley & Sons, 纽约，2016.
[80] P. E. Gaines. 均场博。J. Baillie 和 T. Samuel 编，《系统与控制百科》，页 706–712。Springer, 2015.
[81] E. E. Chatterjee, A. Patra 和 H. K. Joker. 受限轨道长度下小摆系统的摆起与稳定。Systems & Control，47(4):355–364, 2002.
[82] H. Chen 和 L. Guo. 识别与随机控制。Birkhauser, Boston, MA, 1991.
[83] R. T. Chen, A. Bernstein, A. Devraj 和 D. Duvenov. 神经微分方程。Proc. 神经信息处理系统进展（NeurIPS），第 32 卷，页 6572–6583, 2018.
[84] S. Chen, A. Bernstein, A. Devraj 和 S. Meyn. 准随机近似的稳定性与收敛性。arXiv:2009.14431, 2020.
[85] S. Chen, A. Bernstein, A. Devraj 和 S. Meyn. 使用准随机近似加速收敛与强化学习。美国控制会议（ACC），页 1965–1972, 2021年5月.
[86] S. Chen, A. Devraj 和 S. Meyn. 重新审视用于准随机近似快速收敛的 ODE。系统控制期刊，郭磊教授 60 周岁生日纪念控制基础问题特别刊，34(5):1681–1702, 2021.
[87] S. Chen, A. Devraj, V. Borkar 和 I. Koyannis. 随机近似的 ODE 方法。已投稿，2021.
[88] S. Chen, A. Devraj, A. Bucic 和 S. Meyn. 蒙特卡洛与线性随机近似的显式均方界。S. Chiappia 和 R. Calandra 编，AISTATS 会议，第 108 卷，页 4173–4183, 2020.
[89] S. Chen, A. Devraj 和 F. Lu. 非线性函数近似下的 Q 学习。M. Ranzato, R. Hadjell 和 H. Lin 编，神经信息处理系统进展（NeurIPS），arXiv:1910.05405，第 33 卷，页 1687–1690.
[90] T. Chen, Y. Hua 和 W. Yan. 主成分提取的全局收敛性。IEEE 神经网络事务，9(1):58–67, 1998.
[91] W. Chen, D. Huang, A. Kulkarni 等。使用流模型和扩散近似的近似规划。第 48 届中国会议（中国），页 3575–3580, 2009.
[92] Y. Chen, A. Bernstein, A. Devraj 和 S. Meyn 通过乘子交替法进行分布式优化。美国会议（ACC），页 3140–3147, 2019.
[93] S. Boyd 和 L. Vandenberg. 凸优化，第 1 版，剑桥大学出版社，纽约，2004.
[94] S. Bradley, Y. Dystkie 和 A. Bart. 使用策略迭代的自适应二次控制。美国会议，第 3 卷，页 3475–3479, 1994.

420

# 参考文献

[114] A. M. Devraj 和 S. P. Meyn. 具有一致界方差的Q-learning：大折扣不是学习的障碍。arXiv e-prints, arXiv:2002.10301 (将发表于 IEEE Trans Auto (Control), 2020年2月)。
[115] P. Diaconis. 马尔可夫链蒙特卡洛革命。Bull. Amer. Math. Soc. (N.S), 46(2): 179–205, 2009。
[116] D. Ding 和 M. R. Jovanovic. 近端增广拉格朗日上原对梯度流动力学的全局指数稳定性。Proc. of the Annual Control Conf., pages 3414–3419. IEEE, 2019.
[117] R. East, E. Moulines 和 P. Prieur. 非线性时间序列：方法、应用及示例。Springer ICM, 2018。
[118] R. East, E. Moulines 和 D. Stoffler. 非线性马尔可夫链。Chapman-CRC Press, 2014。
[119] K. Duffy 和 S. P. Meyn. 劣策略的大偏差渐近性。Stochastic, 4(1): 300–319, 2014。
[120] K. R. Duffy. 估计反射随机游走的均值时容易出错。Performance Evaluation, 67(12):12290–13003, 2003。
[121] K. Dupee, P. M. Patre, M. Johnson 和 W. E. Dixon. 非线性欧拉-拉格日系统的逆最优控制，第一部分：全反馈控制。Proc. of the Conference on Decision and Control, 与中国会议召开, pages 321–326, 2009。
[122] R. Durrett. 随机空间模型。SIAM Review, 41(4):677–718, 1999。
[123] E. B. Dynkin 和 A. A. Yushevich. 受控马尔可夫过程，Grundlehren des Mathematischen [Fundamental of Mathematical Sciences] 第235卷。Springer-Verlag, 柏林，1979。由 J. M. Danskin 和 C. Holland 从俄语原文翻译。
[124] E. El-Dar 和 Y. Meyn. Q-learning的学习率。J of Machine Learning Research, 4:25–50, 2003。
[125] V. Fabian 等. 关于随机近似中的渐近正态性。The Annals of Mathematical Statistics, 39(4):1327–1332, 1998。
[126] A-M. Farah 和 M. Ghamzadeh. PID加速值迭代算法。在 M. Meila 和 T. Zhang 编著。ICML, volume 139, pages 3143–3153, 18–24 2021。
[127] M. Fayzlab, A. Ribeiro, M. Morari 和 V. Preciado. 通过二次约束分析优化算法：非凸凸问题。SIAM Journal on Optimization, 23(3):2654–2689。
[128] E. Feinberg 和 A. Swieartz, 编。马尔可夫决策过程：模型、方法、方向与优化。Kluwer Acad. Publ.,2001。
[129] E. A. Feinberg 和 A. Swieartz, 编。马尔可夫决策过程手册。Int. Series in Operations Research & Management Science, 60.Klu Publishers, 波士顿，马萨诸塞州，2002。方法与应用。
[130] A. Feintik 和 B. Francis. 求解贝尔曼方程的有限核损失。Automata, 48(5):901–908, 2012。
[131] Y. Feng, L. Li 和 Q. Liu. 求解贝尔曼方程的核损失。在 Advances in Neural Information Processing Systems, pages 15456–15467, 2019。
[132] L. Finlay, V. Gaitsgory 和 I. Lebedev. 与确定性长期平均最优控制相关的线性规划问题的衰减。SIAM Journal on Control and Optimization, 46(5):1667–1700, 2008。
[133] J. M. Feng 和 G. L. Jones. 马尔可夫链蒙特卡洛中的批量均值和方差估计器。Annals of Statistics, 38(2):1034–1070, 2010年4月。
[134] G. Foster, E. Moulines, S. M. Meyn. 马尔可夫链的ODE方法及其在MCMC中的应用。在 Valuetools '06:第一次性能评估方法与技术国际会议论文集,page 42, ACM Press, 纽约，马萨诸塞州，2006。
[135] F. G. Foster. 关于具有可数状态的马尔可夫链。Proc. Cambridge Phil. Soc., 47(188):591–592, 1995。
[136] A. Fradkov 和 B. T. Polyak. 俄罗斯的自适应与鲁棒控制。IFAC–Papers,53(2):1373–1378, 2020。第21届IFAC世界会议。
[137] K. Furuta, M. Yamashita 和 S. Kobayashi. 倒立摆的切换控制。在工业电子、控制与仪器国际会议,pages2193–2198。
[138] P. A. Gagni. 马尔可夫链：从理论到实现。John Wiley & Sons，纽约，2017。
[139] V. Gaitsgory, Parkinson 和 I. Shvartman. 离散时间确定性无限最优控制问题的线性规划表述。Discrete and Continuous Dynamical Systems – Series B,22(10):3821–3838, 2017。
[140] V. Gaitsgory 和 M. Quincampo. 确定性控制生成的八面体测度集。Nonlinear Analysis: Theory, Methods,88,2013。
[141] J. George, P. W. Harrison 和 S. Meyn. 队列的动态控制。Operations Res.,49(5):720–731, 2001。
[142] P. W. Glynn. 无限视界的随机近似。Nonlinear Analysis: Theory, Methods,5:27–41, 2013。
[143] P. W. Glynn. 似然比估计：概述。在 Winter Conference,355–366, 1987。
[144] P. W. Glynn. 相对值估计。Ann. Prob.,24(2):916–931, 1996。
[145] G. Goodman, P. M. Patre 和 S. Mey. 决策控制的自适应过滤。Discrete Event Systems,13(1–2):149–189, 2003。
[146] J. Jordan, M. Meila 和 T. Zhang. 强化学习。pages261–268, 1995。
[147] J. Jordan, M. Meila 和 T. Zhang. 稳定函数近似。在第13届国际控制方法会议,pages5079–5084, 2015。
[148] J. Jordan, M. Meila 和 T. Zhang. 离散事件系统。Springer, 柏林，2015。
[149] R. Graham, D. Knuth 和 O. Patashnik. 具体的数学。Addison-Wesley, Inc., 波士顿，马萨诸塞州，第二版，1994。
[150] L. Green, R. Robertson 和 S. Mey. AlphaGo超越了对手。Scientific American, https://www.scientificamerican.com/ai-self-vanishes-predecessor/,2017。
[151] E. Fabian, R. Bartlett 和 J. Baxter. 梯度估计的方差削减。Journal of Machine Learning Research,5:1471–1530, 2004。
[152] A. Gupta, R. Jain 和 P. W. Glynn. MDP的在线学习。IEEE Transactions on Automatic Control,59(6):1423–1438, 2014年6月。
[153] A. Gupta, R. Jain 和 P. W. Glynn. 用于平均成本的经验算法。在 Dec. Control,pages5079–5084, 2015。
[154] B. Hajek. 工程师的随机过程。Cambridge University Press, 剑桥，英国，2015。
[155] P. Hartman. 关于作为复合组合的表示。Pacific Journal of Mathematics,9(3):707–713, 1959。
[156] T. Hastie, R. Tibirani 和 J. Friedman. 统计分析要素。Springer Series in Statistics, Springer, 纽约，马萨诸塞州，第二版，2001。第三次印刷，2003。
[157] S. Henderson. 通过近似马尔可夫过程进行方差削减。博士论文，斯坦福大学，1997。
[158] S. Henderson 和 P. W. Glynn. 离散事件系统的再生稳态仿真。ACM Transactions on Modeling and Simulation,31:11–345, 2005。
[159] S. Henderson, P. Mey 和 V. Baadić. 类网络中的性能评估与策略选择。Discrete Dynamic Event Systems: Theory and Applications,13(1–2):149–189, 2003。学习、优化和决策的特刊（受邀）。
[160] D. Hernández-Hernandez. 确定性最优控制问题的线性规划法。Mathematical Control,24(1):17–33, 1996。
[161] O. Hernández-Hernandez 和 J. B. Lasserre. 线性规划法。在马尔可夫决策过程手册，Internat. Ser Oper Res. Management Sci. 第40卷,pages377–407.Kluwer Acad Publ., 波士顿，马萨诸塞州，2003。
[162] O. Hernández-Hernandez 和 J. B. Lasserre. 离散时间马尔可夫控制过程：基本最优准则，第30卷。Springer Science & Business Media, 纽约，马萨诸塞州，2012。

# 参考文献

[163] B. Hu and L. Lessard. Nesterov 加速方法的耗散性理论。见 Proc. ICML，pages 1549–1557, 2017.
[164] B. Hu, S. Wright, and L. Lessard. 加速随机方差缩小的耗散性理论：基于半正规划的 SVRG 和 Katyusa 统一分析。见 Proc. ICML，pages 2038–2047, 2018.
[165] D. Huang, W. Chen, P. Mehta, M. Meyn, and A. Surana. 神经动态规划的特征选择。由 F. Lewis 编，反馈控制的强化学习与动态规划。Wiley, Hoboken, 2011.
[166] M. Huang, P. E. Caines, and R. P. Mallame. 非智能体的大群成本耦合 LQ 问题：个体行为与去中心化纳什均衡。IEEE Trans. Automat. Control, 52(9):1560–1571, 2007.
[167] M. Huang, R. P. Mallame, and P. E. Caines. 大群随机博弈：闭环 Mean-Vlasov 系统与纳什均衡原理。Communications in Information and Systems, 6(3):221–251, 2004.
[168] A. Isers. 微分方程数值分析入门教程，第 44 卷。Cambridge University Press, 2009.
[169] T. Jaakola, M. Jordan, and S. Singh. 随机迭代算法的收敛性。Neural Computation, 6:1185–1201, 1994.
[170] K. G. Jameson, R. Nowak, and B. Recht. 无导优化的复杂度。见 Proc. Advances in Neural Information Processing Systems，pages 2672–2680, 2012.
[171] C. Jin, J. Allen-Zhu, and M. J. Jordan. Q-learning 足够高效吗？见 Neural Information Processing Systems,31:4863–4873, 2018.
[172] S. Kakade and J. Lang. 近似最优强化学习。见 Proc. ICML：pages 267–274, 2002.
[173] S. Kakade. 自然策略梯度。见 Proc. Advances in Neural Information Processing Systems，pages 1531–1538, 2002.
[175] R. E. Kalman. 对最优控制理论的贡献。Bol. Soc. Mat. Mexico, 5:102–119, 1960.
[176] R. Kalman. 什么是是线性控制系统？Journal of Basic Engineering, 86:51, 1964.
[177] A. Kanoushti, T. Sutter, and M. Mohajerin Esifani, and J. Lygeros. 关于有限线性规划以及接近无限时折现控制问题的方法。IEEE Control Systems Letters, 1(1):134–139, 2017年7月.
[178] A. Kara and S. Yuksel. POMDP 的有限记忆学习收敛性以及策略过滤下策略的近优性。arXiv preprint:2103.12158, 2021.
[179] H. Karimi, J. Nuti, and M. Schmidt. Polyak-Lojasiewicz 条件下梯度和近端梯度法的线性收敛。见 Online Conference on Machine Learning and Knowledge Discovery in Databases, volume 9851, pages 795–811. Springer-Verlag, Berlin, Helsinki, 2016.
[180] P. Kanamaram. 带有控制马尔可夫噪声和离策略差分学习的双尺度随机近似。Math. Opt. Res., 43(1):130–150, 2018.
[181] H. K. Khalil. 非线性系统。Prentice Hall, Saddle River, NJ, 第3版，2002.
[182] J. Kiefer and J. Wolfowitz. 回归函数最大值的随机估计。Ann. Math. Statist., 23(3):462–466, 1952年9月.
[183] Y. H. Kim and F. L. Lewis. 基于神经网络的高级反馈控制，第 21 卷。World Scientific Harmonic, Jackson, NJ, 1998.
[184] B. Kiumari, K. Gammammoudis, H. Modares, and F. L. Lewis. 最优与自主控制强化学习：综述。Transactions on Neural Networks and Learning Systems, 29(6):2042–2062, 2017.
[185] G. Ohs. AlphaGo。RKCo Films, 2017.
[186] P. Kovovich, H. K. Khalil, and J. O'Reilly. 控制中的奇异扰动方法：分析与设计。Society for Industrial and Applied Mathematics, Philadelphia, PA, 1999.
[187] D. Koller and R. Parr. 分解 MDP 的策略迭代。见第16次不智能性会议论文集，pages 326–334, 2000.
[188] V. Korda. Actor-Critic。博士论文，Massachusetts Institute of Technology, 2002.
[189] V. Korda and V. S. Borkar. 马尔可夫过程的学习。硕士论文，印度科学学院计算机科学与自动化系, 1997.
[190] V. Korda and V. S. Borkar. 马尔可夫过程的 Actor-critic 类型算法。SIAM Journal on Control and Optimization, 38(1):94–123, 1999.
[191] V. Korda and J. Titslis. Actor-critic 算法。见 Neural Information Processing Systems, pages 1008–1014, 2020.
[192] V. Korda and J. Titslis. Actor-critic 算法。SIAM J. Control.,42(4):1143–1166 (电子版), 2003.
[193] V. Korda and J. Titslis. 双尺度随机近似的收敛率。Ann. Appl. Probab.,44(2):796–819, 2004.
[194] I. Kontoyamis, A. Lrastras-Monot, and S. P. Meyn. 马尔可夫链的相对熵和指数衰减界。见 IEEE 信息理论会议，pages 1563–1567, 2005.
[195] I. Kontoyamis, A. Lrastras-Monot, and S. P. Meyn. 马尔可夫链的渐近界与停止规则。见第一次机器学习方法与工具会议论文集，pages 1563–1567, Association for Computing Machinery, New York, NY, 2006.
[196] I. Kontoyamis and S. P. Meyn. 几何遍历性马尔可夫过程的偏差理论与极限定理。Ann. Appl. Probab.,13:304–362, 2003.
[197] I. Kontoyamis and S. P. Meyn. 乘法马尔可夫链的大偏差理论。Electron. J. Probab.,10(3):61–123 (电子版), 2005.
[198] N. B. Kovacchi and A. M. Startuat. 随机方法的连续时间分析。J. Machine Learning Research,22(17):1–40, 2021.
[199] A. Krener. 反馈强化。见 J. Basilwell and C. Williams，Mathematical Control，pages 66–98, 1999.
[200] W. Krichene and P. L. Bartlett. 随机动态过程的平均与聚合。Neural Information Systems,30:6796–6806, 2017.
[201] V. Krishnamurthy. 部分观测过程的结构性结果。ArXiv-prints, arXiv:1512.03875, 2015.
[202] M. Sotine, P. W. Kokannidis and Tsakopoulos. 非线性与自适应控制设计。Wiley & Sons, New York, NY, 1995.
[203] P. R. Kumar and T. I. Seidman. 机器系统分布式调度中的动态不稳定性和稳定方法。IEEE Trans. Autom. Control,35(3):289–298, 1990年3月.
[204] H. J. Kushner and G. Y. Meyn. 随机近似与应用，数学（New York）第 35 卷。Springer-Verlag, New York, 1997.
[205] K. Haweaker and R. Sivan. 线性最优系统。Wiley-Interscience, New York, NY, 1972.
[206] M. G. Lagoudakis and R. Parr. 无模型二乘策略迭代。见 Neural Information Processing Systems, pages 1547–1554, 2002.
[207] T. L. 时不变系统渐近有效控制中的信息界、确定性等价与学习。由 L. Gerencser and P. E. Paine 编，随机系统主题：建模、估计与自适应控制，pages 335–368. Springer Verlag, Heidelberg, Germany, 1991.
[208] T. L. Lai and H. Robbins. 渐近有效适应分配规则。见 Appl. Math.,6(1):4–22, 1985.
[209] C. Lakshminarayayan and S. Szepesvari. 线性随机近似：用于尺度近似。Automatica,79:108–114, 2017.
[210] C. Lakshminarayayan and S. Szepesvari. 线性随机近似：恒定步长和平均能走多远？见人工智能与统计国际会议，pages 1347–1355, 2018.
[211] S. Lange, T. Gabel, and M. Riedmiller. 批量强化学习。见 强化学习，pages 45–73, 2012.
[212] J. Kiefer and J. Wolfowitz. 随机近似。。。..,,,22222222222222.................,6(2):218–272, 1990.
[214] D. Lasry and J. Guy. 大群纳什均衡。Communications in Information and Systems,6(3):221–251, 2004.
[215] V. Korda. 马尔可夫过程。World Scientific, Jackson, NJ, 1998.
[216] I. Kontoyamis and S. P. Meyn. 偏差理论。Cambridge University Press, Cambridge, 2020.
[217] M. Lee. 线性线性系统？Journal of Basic Engineering, 86:51, 1964.
[218] D. Lee and S...  离策略策略策略学习。arXiv-prints:2103.12158, 2021.
[219] D. Lee and S. Sutton. 简单随机搜索。ArXiv-prints, arXiv:1912.0270, 2019.
[220] H. Mania, A. Guy, and B. Right. 简单随机搜索提供了一种竞争性的强化学习方法。见 Neural Information Processing Systems, pages 1800–1809, 2018.

## 参考文献

[237] A. S. Manne. Linear programming and sequential decisions. Management Sci., 6(3):259–267, 1960.
[238] P. Marbach and J. N. Tsitsikis. Simulation-based optimization of Markov reward processes: implementation issues. In Proc. of the Dec. and Control, volume 2, pages 1769–1774. IEEE, 1999.
[239] P. Marbach and J. N. Tsitsikis. Simulation-based optimization of Markov reward processes. IEEE Trans. Autom. Control, 46(2):191–209, 2001.
[240] I. M. Marels, B. D. Anderson, R. R. Bitmead, M. Bodson, and S. S. Savistry. Revisiting the MIT role for adaptive control. K. Astrom and B. Bittitten, Editors Systems in Control and Signal Processing 1986, pages 161–166. Elsevier, Netherlands, 1987.
[241] N. Natmin, A. Proutiere, A. Santos, and S. Tu. From self-tuning regulators to reinforcement learning and back again. In Proc. of the Dec. and Control, pages 3724–3740, 2019.
[242] D. Mayne, J. Rawlings, C. Rao, and P. Skojart. Constrained model predictive control: stability and optimality. Automatica, 36(5):789–814, 2000.
[243] D. Mayne. Model predictive control: developments and future promise. Automatica, 50(12):2967–2986, 2014.
[244] E. Mazumdar, A. Pachiano, Y.-a. Ma, P. L. Bartlett, and M. I. Jordan. Thompson sampling with Langevin algorithms. arXiv eprints, arXiv–2002.0220.
[245] P. G. Mehta and S. P. Meyn. Q-learning and Pontryagin’s minimum. In Proc. of the Conf. on Dec. and Control, pages 3598–3605, 2009.
[246] P. G. Mehta and S. P. Meyn. Q-learning, I: deterministic optimal control. ArXiv eprints:2008.03352.
[247] P. G. Mehta, S. P. Meyn, G. Neu, and F. Lu. Q-learning. In Proc of the American Control Conf., pages 4740–4756, 2021.
[248] J. M. Cao, X. Ciao, C. Szepesvari. On the global convergence rates of stochastic policy gradient methods.
[249] F. S. Melo, S. P. Meyn, and M. I. Ribeiro. Analysis of reinforcement learning with function approximation. In Proc. ICML, 664–671, ACM, New York, NY, 2008.
[250] M. Metivier and P. Pierrot. The methods of degree presente pour une sure classe d’stochastic algorithms as a depros. Theory Related Fields, 74:403–428, 1997.
[251] C. D. Meyn, Jr. The role of the generalized inverse in the theory of finite Markov chains. SIAM Review, 17(3):443–464, 1975.
[252] S. M. Meyn. Workloads for stochastic networks: value functions and performance evaluation. IEEE Trans. Autom. Control, 50(8):1106–1122, August 2005.
[253] S. P. Meyn. Large deviation and control variates for large functions. Ann. Prob., 16(1):310–339.
[254] S. P. Meyn. Control Techniques for Complex Networks. Cambridge University Press, 2007.
[255] S. P. Meyn and R. L. Tweedie. Bellman-based Markov models for detection and optimization. In Proc. of the Dec. and Control, pages 5558–5564, 2008.
[256] S. P. Meyn and R. L. Tweedie. Computable bounds for convergence rates of Markov chains. Ann. Prob., 22(4):1911, 1994.
[257] S. M. Meyn and R. L. Tweedie. Markov Chains and Stability. Cambridge University Press, Cambridge, UK, 2002.
[258] D. Michie and R. A. Boxes. Boxes: in an adaptive experiment. Machine Intelligence, 2(2):137–152, 1968.
[259] V. Meyn, A. P. Badia, M. Mirza, A. Graves, T. P. Lillicarc, T. Harley, D. Silver, and K. Kavukoglu. Stochastic methods for deep reinforcement learning. arXiv:abs/1602.01783.
[260] V. Meyn, K. Kavukoglu, D. Silver, A. Graves, I. Antonoglou, D. Wierstra, and M. A. Riedmier. Playing Atari with deep reinforcement learning. arXiv:abs/1312.5602.
[261] V. Meyn, K. Kavukoglu, D. Silver, et al. Human-level control through deep reinforcement learning. 51:529–533, 2015.
[262] M. Mohri, A. Rostamizadeh, and A. Talwalkar. Foundations of Machine Learning. MIT Press, Cambridge, MA, 2018.
[263] D. K. Molzah, F. Dörfler, S. Low, R. Chakrabarti, and J. Lavaei. A survey of distributed optimization and control for electric power systems. Trans on Smart Grid, 8(6):2941–2962, 2017.
[264] A. W. Moore. Efficient Memory-Based Learning for Robot Control. PhD thesis, University of Cambridge, Computer Laboratory.
[265] W. Mou, C. Jin, J. M. Wainwright, and P. I. Jordan. On fine-grained Polyak-Ruppert and non-asymptotic convergence. arXiv-prints, arXiv:2004.04719, 2020.
[266] E. Moulines and F. R. Bach. Non-asymptotic analysis of stochastic algorithms for machine learning. Advances in Neural Processing Systems, 24, 451–459, 2011.
[267] K. P. Murphy. Machine Learning: A Probabilistic Perspective. MIT Press, Cambridge, MA, 2012.
[268] R. Murray. Feedback control theory: techniques and real-time decision making. Tutorial series at the Simons Institute on Real-Time Decision Making. https://sims.berkeley.edu/murray
[269] O. Nachum and B. Dai. Reinforcement learning via Fenchel-Rockafellar duality. arXiv preprint arXiv:2001.01866, 2020.
[270] O. Nachum, M. Orunci, K. Xu, and D. Schuurmans. Building the gap between value and reinforcement learning. Advances Neural Processing Systems, 30, 8, 2017.
[271] A. Nedic and D. Bertsek. Least squares policy evaluation with linear function approximation. Discrete Dynamic Systems: Theory and Applications, 13(1-2):79–110, 2003.
[272] A. Nemirovki, A. Juditsky, G. Lan, and A. Shapiro. Robust stochastic approximation approach to convergence. SIAM Journal on Optimization, 19(4):1574–1609, 2009.
[273] Y. Nesterov. Lectures on Optimization. Springer Optimization and Its Applications 137. Springer Publ., New York, NY, 2018.
[274] Y. Nesterov and V. Polyak. Random gradient minimization of convergence functions. Foundations of Computational Mathematics, 17(2):527–566, 2017.
[275] J. Norris. Markov Chains in Statistical and Probabilistic Mathematics. Cambridge University Press, Cambridge, UK, 1997.
[276] M. A. Nowak. General Evolutionary Dynamics: Exploring the Equations of Life. Harvard University Press, Cambridge, MA, 2006.
[277] E. Oja. A simplified neural for principal component analysis. J. Math. Biol., 15(3):263–278, 1983.
[278] D. Ormondeit and P. Glyn. Kernel-based reinforcement learning in average-cost problems. Trans. on Automatic Control, 47(10):1624–1636, October 2002.
[280] J. S. Orr and C. J. Denny. Analysis of the XL-15 flight 36-95 divergent lift-cycle optimization. Journal of Aircraft, 54(1):115–1148, 2017.
[281] I. Osman, B. Van Roy, and Z. Wen. Reinforcement learning and exploration via randomized value functions. Proc. of ICML, 2377–2386, 2012.
[282] N. Parikh and S. Boyd. Proximal Algorithms. Foundations and Optimization. New Publishers, Sherwood, MA, 2013.
[283] J. B. Park and J. Y. Lee. Nonlinear adaptive control by Lyapunov analysis: overview and survey. Journal of Control Research, and Systems, 20(3):261–269, 2003.
[284] S. P. Meyn and R. L. Tweedie. Bellman-based Markov models for detection and optimization. In Proc of the Dec. Control., pages 5558–5564, 2008.
[285] S. P. Meyn and R. L. Tweedie. Computable bounds for convergence rates of Markov chains. Ann. Prob., 22(4):1911, 1994.
[286] S. P. Meyn and R. L. Tweedie. Bellman-based Markov models for detection and optimization. In Proc of the Dec. Control., pages 5558–5564, 2008.

## 428 参考文献

[315] E. Seneta. 《非负矩阵与马尔可夫链》。Springer, 纽约, 纽约州, 第2版, 1981.
[316] C. Shannon. 《通信的数学理论》。Bell System Tech. J., 27:379–423, 625–656, 1948.
[317] H. Sharma, R. Jain, and A. Gupta. 一种连续空间非参数方法的经验相对学习算法. 欧洲控制会议，pages 1368–1373. IEEE, 2019.
[318] B. Shi, S. S, D. Wu, and M. J. Jordan. 通过高分辨率微分方程的辛离散化实现加速. 在 H. Wallach, L. Lachehelle, A. Beygelmer, F. d'Alché-Duc, E. Fox, and R. Garnett，《神经信息处理系统进展》，pages 5774–5752, 2019.
[319] S. Shridkar and S. Meyn. 拟随机近似. 美国会议论文集，pages 2429–2445, 2021.
[320] S. Shivam, I. Buckley, Y. Ward, C. Seatu, and M. Eggert. 基于牛顿-拉夫逊流的跟踪：车辆适应.arXiv:abs/1811.08033, 2018.
[321] R. Skora and W. Skarbek. Alpha算法的稳定性. 在 L. Polkowski 和 A. Skowron编选，《计算机科学讲义中的行计数与趋势》，计算机科学讲义第1224卷，pages 354–360. Springer Verlag, 2019.
[322] D. Silver, T. Hubbert, J. Schwinger, 等. 一种通过自对弈精象棋、将棋和围棋的通用强化学习算法。《科学》，362(6419):1140–1144, 2018.
[323] D. Silver, G. Wang, N. Heess, D. Driester, and M. Mieder. 确定性策略梯度算法. 国际机器学习会议(ICML)，pages 387–395, 2014.
[324] S. P. Singh, T. Jaakkola, and M. Jordan. 软状态聚合的强化学习。《神经信息处理系统论文集》，7:361, 1995.
[325] S. Smale. 局部与全局牛顿法的收敛过程。《数学经济学杂志》，12(2):107–120, 1976.
[326] R. D. Small and E. Sondik. 有限时域内部分观测马尔可夫过程的最优收敛。《开放研究(Open Res.)》，21(5):1071–1088, 2013.
[327] J. C. Stall. 带有同步扰动梯度估计的多变量随机近似。《IEEE自动控制汇刊》，37(3):331–342, 1992.
[328] J. C. Stall. 用于获得极大似然估计的随机近似技术. 美国会议论文集，pages 1161–1167. IEEE, 1987.
[329] J. C. Stall. 同步扰动随机近似的非方程测量。《自动机》，30(1):109–112, 1987.
[330] M. W. Spong and B. Hu. 摆系统：一种用于控制研究和教育的机电系统。控制会议论文集，pages 555–556. IEEE, 1995.
[331] M. W. Spong and L. Prality. 使用切换和饱和的无向机械系统控制. 在 A. Morse编选，《逻辑切换控制》，pages 162–172. Springer, 柏林, 海德堡 1997.
[332] M. W. Spong and M. Vidyasagar. 《机器人动力学与控制》。Wiley & Sons, 芝加哥, 英国, 2008.
[333] R. Srikant and Y. Ying. 线性随机近似和一维学习的有限时间误差界. 计算学习理论会议集(COLT)，pages 2803–2830, 2019.
[334] R. L. Stratonovich. 条件马尔可夫过程。《SIAM概率理论应用杂志(SIAM J. Theory Prob. Appl.)》，5:1576–1780, 1963.
[335] W. Su, B. Boyd, and E. Candelas. 为牛顿加速梯度法的微分方程：理论与见解. 神经信息处理系统进展论文集，pages 2510–2518, 2014.
[336] J. Subramanian and A. Mahajan. 部分观测系统的近似信息状态。控制会议论文集，pages 1629–1636. IEEE, 2019.
[337] J. Subramanian, A. Sinha, R. Seaj, and A. Mahajan. 部分观测强化学习的近似信息状态.arXiv:2010.08843, 2020.
[338] R. Sutton and A. Barto. 《强化学习：导论》。MIT Press, 马萨诸塞州剑桥, 第2版, 2018. 在线获取：www.uboston.edu/~book/html
[339] R. S. Sutton. 时间信用分配。马萨诸塞大学博士论文，阿姆斯特斯特，1984.
[340] R. S. Sutton. 通过时间差分方法学习。《机器学习》，3(1):9–44, 1988.
[341] R. S. Sutton. 强化学习中的泛化：编码示例。神经信息处理系统论文集，1038–1070, 1995.
[342] R. S. Sutton and A. G. Barto. 迈向网络理论：期望与预测。《心理评论(Psychological Review)》，88(2):115–138, 1981.
[343] R. S. Sutton, A. G. Barto. 强化学习是直接控制。《控制系统》，121(2):19–22, 1992.
[344] R. S. Sutton, D. A. McAllister, S. P. Singh, and Y. Mansour. 连续领域强化学习的策略梯度方法。《神经信息处理系统进展》，pages 5774–5752, 2019.
[345] R. S. Sutton, C. Szesvari, and H. 线性函数近似的离策略时间差收敛算法。神经信息处理系统论文集，pages 1609–1616, 2008.
[346] C. Szesvari. Q-学习的渐近收敛率。神经信息处理系统论文集，pages 1064–1070, 1997.
[347] C. Szesvari. 强化学习算法。《人工智能与机器学习教程》。Morgan & Clay Publishers, 圣拉斐尔, CA, 2010.
[348] T. Yan, H. Moise, C. Mancise, D. Necic, and I. Marels. 从1922到2010年的极值寻求。第29次中国会议，pages 14–26. IEEE, 2010.
[349] A. Zaks and J. Lin. 未知系统的分析：线性规划方法.arXiv/2003.00779, 2020.
[350] G. Tesauro, TD Mann. 自教算法，大师级比赛。《神经通信》，6(2):215–219, 1994.
[351] G. Thopp and V. Borkar. 基于 Alekseev 公式的随机近似浓度。《统计系统(Statistical Systems)》，9(1):1–26, 2010.
[352] J. Titsiskis. 异步随机近似与Q-学习。《机器学习》，16:185–202, 1994.
[353] J. Titsiskis and B. Vay. 马尔可夫过程的最优映射：希尔伯特空间理论、近似算法以及在高维金融衍生品中的应用。《IEEE自动控制汇刊》，44(10):1840–1851, 1999.
[354] J. Titsiskis and B. Vay. 差分学习分析。《自动控制(Automatica)》，35(11):1799–1808, 1998.
[355] J. N. Titsiskis and B. Vay. 大规模动态规划基于特征的方法。《机器学习》，22(3):59–94, 1996.
[356] J. N. Titsiskis and B. Vay. 强化控制中时间差分学习分析。《IEEE自动控制汇刊》，42(5):674–690, 1997.
[357] Y. Z. Zynik and Z. J. Nikodik. 扩散生成模型采样与推理的理论保证。Academic Press, 纽约, 纽约州, 1971.
[358] B. Zen and M. Raginsky. 扩散生成模型采样与推理的理论保证。在 A. Beygelmer 和 D. Hsu 编，《COLT》，第99卷，pages 3084–3114, 2019.
[359] K. G. Vavoudakis, F. L. Lewis, and D. Vrobe. 用于自主控制和博弈论的强化学习。在 P. Angelov编，《计算机学习与智能手册》。World Scientific, Hackacksack, NJ, 第2版, 2021.
[360] K. G. Vavoudakis, Y. Wan, F. L., and D. Canverse,编。《强化学习与控制手册》。系统、决策与控制研究(SSDC).

# 符号与缩写词表

`$I_A$` : 指示函数, 395
`$\Phi$` : (平稳)策略, 9, 247
`$\pi$` : `$X$` 的不变概率质量函数, 205, 319
`$\varrho$` : 169
`$X, U$` 的不变概率质量函数, 319
占用概率质量函数, 194
`$\lambda$` : 探索信号, 31
`$\psi_{(n)}$` : `$\psi(\phi(n))$`, 178, 319
`$c_n$` : `$\frac{d}{dt}\phi(n)$`, 107
`$\zeta_n$` : 适能值 (Eligibility value), 163
`$\Gamma$` : 损失函数, 31, 90
`$\mathcal{H}$` : 最小或评估, 319
`$A^*$` : 随机策略得分函数, 377
`$\lambda$` : TD(lambda) 中的折扣, 178
`$\lambda$` 或 `$\eta$` : 特征值, 22, 356
`$\Theta$` : ODE QA 的状态, 98
`$\tilde{t}$` : 时间缩放 ODE, 107
`$\theta$` : ODE 似近的状态, 85
`$\tau$` = ODE 变量替换, 107

`$F_k$` : 过滤, 247, 397
`$\mathcal{J}$` : QSA/SA 向量场, 98, 280

`$\mathcal{H}$` : 函数类, 160
IDP : 逆动态规划, 63
inf : 下确界 (Infimum), 396

`$k$` : 核, 165

liminf, 396
limsup, 396
LQR, 52
LSTD, 173, 371
LTI, 12

ACOE : 平均成本优化质量, 245
ARE : 代数 Ric卡提方程, 66, 77

MDP : 马尔可夫决策过程, 245
MSBE : 均方贝尔曼误差, 325
MSE : 均方误差, 281

+ `$B$` : 贝尔曼误差, 63
+ `$C^1$` : 连续可微, 23
CLT : 中心极限定理, 222

PIA, 404
PJR : Markov-Juditsky-Ruppert, 108
pmf : 概率质量函数, 206
`$P_n, P_s$` : 398
`$P_t$` : 受控转移矩阵, 245

`$D$` : 序分差 (Temporal difference), 162, 325
DCOE : 折扣成本优化质量, 59, 318
DP : 动态规划, 53
DLP : 动态规划线性, 65, 407
Dual, 对偶, 193

`$Q$` : Q 函数, 53, 216
固定策略, 103, 320

qSGD : Quaoistic 梯度下降, 114

ERM : 经验风险最小化, 196, 296
ESC : 极值寻求控制, 114
`$E_u$` : 207, 398
`$E_\mu$` : 398

RKHS, 166
`$S^0$` : 马尔夫族得分函数, 231
`$S_v(r)$` : 下水平集, 17
SGD : 随机梯度下降, 141, 231
294

SNR : 随机牛顿-拉夫逊法, 302
SPP, 60, 402

SPSA : 同步扰动随机近似, 157

sup : 上确界 (Supremum), 396

U : 输入空间, 12

(V3) : 雅普诺夫漂移条件, 234

(V4) : 雅普诺夫漂移条件, 235

VIA : 54, 403

X : 状态空间, 12

`$x^e$` : 平衡状态,
`$Z_t$` : 缩放 QSA 误差, 107
`$Z_{ri}$` : 缩放 SA 误差, 282

# 索引

+ 动作空间, 12
Actor-critic 方法
- 兼容特征, 380
- 费雪信息矩阵, 384
- 得分函数, 377
- 可接受输入, 246
- 优势函数, 322, 382
- 对于最优策略, 337
- ARMA 模型, 12
- 渐近协方差, 281
- 渐近稳定性, 18
- 指数级 19
- 全局, 18
- 平均成本最优控制, 402
- 平均成本最优方程, 245, 403

+ Basis, 68
- 线性独立, 177, 325
- 表格, 163, 358
- 贝叶状态, 410
- 贝尔曼方程, 53
- 固定策略, 56
- 贝尔曼误差, 63
- 中心极限定理 (CLT), 222
- 批量均值法, 223
- 强制性, 20
- 紧紧, 395
- 比较定理, 21
- 兼容特征, 380
- 条件数, 396
- 条件期望, 237, 323
- 连续可微, 23
- 控制变变量, 230
- 受控转移矩阵, 245
- 凸, 91
- 严格的, 92
- 强力的, 92
- 未来代价 (Cost to go), 52
- 连续时间, 69

+ 干扰抑制, 13
- 漂移条件, 23
- 漂移不等式, 19
- 动态规划, 54
- 动态规划 (DP) 方程, 53
- 适能向量, 163, 178, 327
- 经验
- 分布, 162
- 均值, 162
- Pnf, 162
- 经验风险, 161
- 平衡, 17
- 吸引区域, 199
- 遍历性的, 209, 213
- 几何, 235
- 欧拉近似, 87
- 示例
- Acrobot, 30
- 多老虎机 (Bandits), 266
- CartPole, 38
- 无摩擦摆钟, 28
- 线性状态模型, 208
- M/M/1 队列, 211
- M/M/1 , 252, 322
- MagBall, 36
- 山地车, 34, 70, 118
- 排队游戏, 261
- 排队网络, 73
- 部分信息 Rover, 264
- 速度缩放, 253
- 练习
- CartPole, 38
- 稳定性标准, 239
- 条件期望简介, 237
- l模型, 275
- 摆钟, 47, 153
- 佩朗-弗罗贝尼斯理论, 241
- 全观测 Rover, 271
- 仿真理论与实践, 239

+ 折扣因子, 59
- 折扣成本, 402

索引 (续)
- 速度缩放, 272
- 表格基, 358
- 零, 35
- 外生, 11
- 期望
- 条件, 237, 323
- 经验缓冲区, 162
- 探索, 4, 31, 266
- 极值寻求控制, 114
- 反馈律, 9
- 反馈控制, 99
- 固定点方程, 53
- 流体模型, 248
- 基础矩阵, 58, 241
- 伽尔金, 163, 178
- 梯度下降
- 加速, 155
- 随机, 114
- 梯度流, 90
- 矩阵增益, 60, 401
- Grönwall 不等式, 86
- 哈密顿-雅可比-贝尔曼方程, 69
- 历史状态, 123
- HJB 方程, 69
- 亥维茨, 273
- 指示函数, 395
- 紧紧的, 220
- 下确界, 396
- 信息状态, 410
- 输入, 12
- 可接受, 246
- 输入空间 U, 12
- 内部控制, 14
- 原则, 14
- 逆动态规划 (IDP), 63
- 不可约的, 233
- Kac 定理, 234
- L-smooth
- 大数定律 (LLN), 222
- 线性独立性, 177, 325
- 线性二次调节器, 52, 77
- 线性状态模型, 15, 208
- 线性化, 29
- Lipschitz 连续的, 85
- 负载, 211
- LSTD 学习, 329
- LTI 系统, 126
- 增益矩阵, 15
- 雅普诺夫方程, 26
- 雅普诺夫函数, 19
- 控制, 63, 81
- 马尔可夫链
- $\psi$-不可约, 233, 234
- $\rho$-不可约, 234
- 非周期性的, 333
- 通信图, 214
- 遍历, 205
- 无记忆性, 205
- 移位算子, 398
- 谱隙, 214
- 转移核, 206
- 转移矩阵, 206
- Ui-链, 233
- 马尔可夫决策过程, 245
- 马尔可夫性质, 399
- 强力的, 406
- 鞅差分, 307
- 均场动力学, 248
- 模型预测控制, 62
- 蒙特卡洛, 222
- 控制变, 230
- 邻域, 395
- 牛顿-拉夫逊算法, 284
- 牛顿-拉夫逊流, 88
- 正则化的, 89, 301
- 非线性空间模型, 122
- 连续时间, 16
- 观测
- 占用 $\phi$, 194
- ODE 方法, 84, 281
- Oja 算法, 151
- 最优控制
- 哈密顿, 70
- 最小原理, 70
- 风险敏感, 276
- 优性
- 平均成本, 245, 403
- 优化, 90
- 驻点, 47
- 普通微分方程 (ODE), 84
- ODE 方法, 84, 281
- 向量场, 23
- 泊松方程, 216
- 泊松不等式, 20, 218
- 连续时间, 24
- 策略, 9
- H-贪婪的, 321
- 线性最优, 66
- 马尔可夫, 13, 247
- 平稳马尔可夫, 247

+ 策略改进
- 近似, 104
- 平均成本, 404
- 折扣成本, 320
- Polyak-Juditsky–Ruppert, 108, 282
- 正定的, 396
- 最优性原理, 53
- 连续时间, 69
- 概率质量函数 (pmf), 206
- 探测信号, 98

+ 状态空间 X, 12
- 状态模型, 12
- 随机近似
- 算法, 280
- 平均化, 282
- 投影, 286
- 重启, 286
- SNR, 302
- Zap, 301
- 随机梯度下降, 231, 294
- 拟的, 114
- 随机牛顿-拉夫逊, 302
- 下水平集, 19
- 逐次近似, 54
- Picard 迭代, 85
- 充分统计量, 12, 205
- 上确界, 396

+ Q 函数
- 平均成本, 246
- 固定策略, 320
- 总成本, 554
- Q-learning
- 异步的, 339
- Q(S), 183, 349
- Q(O), 338
- 相对的, 344
- 同步的, 339
- Watkins, 351

+ 表格基, 163, 358
- TD 学习, 172, 332
- 优势, 337
- LSTD, 329
- 离策略的, 117, 332
- 在策略的, 172, 332
- 再生的, 374
- 相对值函数, 216, 403
- 复现希尔伯特空间, 166
- Ric卡方程, 66, 77
- 风险敏感最优控制, 276

+ 调节, 15
- 转移矩阵, 206
- 受控, 245

+ 样本复杂度, 290

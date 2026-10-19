
这实际上非常有用。在散射理论中，它被称为*波矩阵*，因为它用于波函数的展开：

$$u(r)=N_0\sum_{i=1}^{N}\frac{\sin(k_i r)}{k_i r}F(k_i,k_0)^{-1}.$$  (26.42)

这里$N_0$是归一化常数，$R$振幅适用于驻波边界条件。因此，一旦我们知道了$F$，也就知道了波函数。

+   1. 绘制$u(r)$并将其与自由波进行比较。

# 代码、小程序和动画

表A.1 Python代码，第1–26章。

| 名称 | 列表编号 | 描述 | 名称 | 列表编号 | 描述 |
|---|---|---|---|---|---|
| EasyVisual | 1.1 | 可视化简易绘图 | 3GraphVisual | 1.2 | 可视化多图 |
| 3Dshapes | 1.3 | 可视化3D形状 | EasyMatPlot | 1.4 | Matplot 2D |
| GradesMatPlot | 1.5 | Matplot多图 | MatPlot2figs | 1.6 | Matplot多图 |
| PondMatPlot | 1.7 | Matplot散点图 | Simple3Dplot | 1.8 | Matplot曲面 |
| Scatter3dPlot | 1.9 | Matplot 3D散点图 | EqHeatAnimate | 1.10 | Matplot动画 |
| MayaLines | 1.12 | Mayavi流线 | MayaYlm | 1.10 | Mayavi曲面 |
| Area | 2.1 | 简单屏幕输入/输出 | AreaFormatted | 2.2 | 格式化输入/输出 |
| Directives | 2.3 | 输入/输出指令、转义 | Limits | 2.4 | 机器精度 |
| Bessel | 3.1 | 向下递推 | Walk | 4.1 | 随机游走 |
| Walk3D | 4.1 | 3D随机游走 | DecaySound | 4.2 | 自发衰变 |
| TrapMethods | 5.1 | 梯形法则 | IntegGauss | 5.2 | 高斯求积 |
| vonNeuman | 5.3 | 冯·诺依曼舍选法 | Eigen | 6.34 | 矩阵特征值 |
| Matrix | 6.5 | 矩阵数组乘法 | NewtonNDanimate | 6.1 | N维牛顿–拉弗森法 |
| Bisection | 7.1 | 二分算法 | NewtonCD | 7.2 | 牛顿–拉弗森搜索 |
| Lagrange | 7.5 | 拉格朗日插值 | Spline | 7.3 | 样条拟合 |
| SplineInteract | 7.3 | 交互式样条 | Fit | 7.4 | 最小二乘拟合 |
| rk4 | 8.1 | rk4常微分方程求解器 | rk45 | 8.2 | 自适应步长rk4 |
| ABM | 8.3 | ABM常微分方程求解器 | QuantumNumerov | 9.1 | 薛定谔方程 |
| QuantumEigen | 9.2 | 量子本征rk4 | ProjectileAir | 9.3 | 考虑阻力的抛体运动 |
| TuneNumPy | 11.5 | NumPy向量 | Tune.f90 | 11.6 | Fortran调优 |
| Tune | 11.7 | Python调优 | Tune4 | 11.8 | Python循环展开 |
| tune4.f95 | 11.9 | Fortran循环展开 | SumArraysCuda | 11.16 | CUDA GPU程序 |
| SumArraysCuda2 | 11.17 | GPU块 | DFTcomplex | 12.1 | 复数离散傅里叶变换 |
| DFTreal | 12.2 | 实数离散傅里叶变换 | FourierMatplot | 12.2 | 交互式离散傅里叶变换 |
| NoiseSincFilter | 12.4 | 傅里叶滤波 | FFT.py | 12.3 | 快速傅里叶变换 |
| FFTappl | 12.3 | 快速傅里叶变换+图形 | CWT | 13.1 | 连续小波 |
| DWT | 13.2 | 离散小波 | Bugs | 14.1 | 逻辑斯蒂分岔 |

# 表A.1（续）.

| 名称 | 列表编号 | 描述 | 名称 | 列表编号 | 描述 |
|------|-------------|-------------|------|-------------|-------------|
| LyapLog | 14.2 | 李雅普诺夫系数 | Entropy | 14.3 | 香农熵 |
| PredatorPrey | 14.4 | 种群动力学 | Fern3D | 16.1 | 3D蕨叶 |
| Column | 16.2 | 柱状生长 | Gameoflife | 16.3 | 生命游戏 |
| Islands.pov | 16.4 | 光线追踪 | Film | online | 薄膜沉积 |
| Coastline | online | 盒计数 | DLA | 16.7 | 凝聚 |
| Fern | 16.1 | 1D蕨叶 | Sierpin | 16.2 | 谢尔宾斯基垫片 |
| IsingViz | 17.1 | 伊辛模型 | WangLandau | 17.2 | 王–兰道蒙特卡洛 |
| QMC | 17.3 | 量子蒙特卡洛 | QMCbouncer | 17.4 | 量子蒙特卡洛弹跳粒子 |
| MD | 18.1 | 1D分子动力学 | MD2D | 18.1 | 2D分子动力学 |
| LaplaceLine | 19.1 | 拉普拉斯方程 | EqHeat | 20.1 | 热方程解 |
| EqHeat | 20.1 | 热方程 | HeatCNTridiag | 20.2 | 改进的热方程求解 |
| EqStringAnimate | 21.1 | 波动方程 | EqStringMatPlot.py | online | 使用Matplot的波动 |
| Waves2D | 21.2 | 2D波动方程 | Waves2Danal | online | 解析薄膜 |
| HarmosAnimate | 22.1 | 量子波包 | FDTD | 22.2 | 时域有限差分 |
| CircPolarztn | 22.3 | 时域有限差分圆偏振 | LaplaceFEM_1D | 23.1 | 一维有限元 |
| LaplaceFEM_1D | 23.1 | 一维有限元 | LaplaceFEM_2D | 23.2 | 二维有限元 |
| AdvecLax | 24.1 | 平流方程 | Soliton | 24.2 | KdV孤子 |
| SolitonAnimate | online | 孤子动画 | Beam | 25.1 | 纳维–斯托克斯方程 |
| BeamContour | 25.4 | 流场等值线 | Bound | 26.1 | 积分方程本征 |
| Scatt | 26.2 | 积分方程散射 |

# 表A.2 动画（mpeg和avi格式需要VLC或QuickTime等播放器，gif格式需要Web浏览器）。

| 目录 | 章节 | 目录 | 章节 |
|----------|---------|----------|---------|
| DoublePendulum（另见小程序） | 15 | Fractals（另见小程序） | 16 |
| MapleWaveMovie（需要Maple） | 21 | Laplace（DX动画） | 19 |
| MD | 18 | TwoSlits | 22 |
| 2D solitons | 21,25 | Utilities（脚本、颜色映射） |  |
| Waves（动画gif需要浏览器） | 21 |  |  |

# 参考文献

Abarbanel, H.D.I., Rabinovich, M.I., and Sushchik, M.M. (1993) 《物理学家非线性动力学导论》, World Scientific, Singapore.
Abramowitz, M. and Stegun, I.A. (1972) 《数学函数手册》, 第10版, US Govt. Printing Office, Washington.
Addison, P.S. (2002) 《图解小波变换手册》, Institute of Physics Publishing, Bristol and Philadelphia.
Allan, M.P. and Tildesley, J.P. (1987) 《液体计算机模拟》, Oxford Science Publications, Oxford.
Amdahl, G. (1967) 《单处理器方法实现大规模计算能力的有效性》, Proc. AFIPS, 第483页.
Ancona, M.G. (2002) 《应用科学与工程计算方法》, Rinton Press, Princeton.
Anderson, E., Bai, Z., Bischof, C., Demmel, J., Dongarra, J., Du Croz, J., Greenbaum, A., Hammarling, S., McKenney, A., Ostrouchov, S., and Sorensen, D. (2013) 《LAPACK用户指南》, 第3版, SIAM, Philadelphia, www.netlib.org (访问日期：2015年3月22日).
Anderson, J.A., Lorenz, C.D., and Traveset, A. (2008) HOOMD-blue, 通用分子动力学模拟. J. Comput. Phys., 227 (10), 5342, codeblue.umich.edu/hoomd-blue (访问日期：2015年3月22日).
Arfken, G.B. and Weber, H.J. (2001) 《物理学家数学方法》, Harcourt/Academic Press, San Diego.
Argyris, J., Haase, M., and Heinrich, J.C. (1991) Comput. Methods Appl. Mech. Eng., 86, 1.
Armin, B. and Shlomo, H. (eds) (1991) 《分形与无序系统》, Springer, Berlin.
Askar, A. and Cakmak, A.S. (1977) J. Chem. Phys., 68, 2794.
Banacloche, J.G. (1999) 《量子弹跳球》. Am. J. Phys., 67, 776.
Barnsley, M.F. and Hurd, L.P. (1992) 《分形图像压缩》, A.K. Peters, Wellesley.
Beazley, D.M. (2009) 《Python必备参考》, 第4版, Addison-Wesley, Reading, MA, USA.
Becker, R.A. (1954) 《理论力学导论》, McGraw-Hill, New York.
Bevington, P.R. and Robinson, D.K. (2002) 《物理科学数据简化和误差分析》, 第3版, McGraw-Hill, New York.
Bleher, S., Grebogi, C., and Ott, E. (1990) 《混沌散射中的分岔》. Physica D, 46, 87.
Briggs, W.L. and Henson, V.E. (1995) 《离散傅里叶变换：用户手册》, SIAM, Philadelphia.
Bunde, A. and Havlin, S. (eds) (1991) 《分形与无序系统》, Springer, Berlin.
Burgers, J.M. (1974) 《非线性扩散方程；渐近解与统计问题》, Reidel, Boston.
Car, R. and Parrinello, M. (1985) Phys. Rev. Lett., 55, 2471.
Cencini, M., Cecconi, F. and Vulpiani, A. (2010) 《从简单模型到复杂系统的混沌》, World Scientific, Singapore.
Christiansen, P.L. and Lomdahl, P.S. (1981) Physica D, 2, 482.
Christiansen, P.L. and Olsen, O.H. (1978) Phys. Lett. A, 68, 185; Christiansen, P.L. and Olsen, O.H. (1979) Phys. Scr., 20, 531.

Goodings, D.A. and Szeredi, T. (1992) 《用路径积分法的量子弹跳器》. Am. J. Phys., 59, 924.
Goswani, J.C. and Chan, A.K. (1999) 《小波基础》, John Wiley & Sons, New York.
Gottfried, K. (1966) 《量子力学》, Benjamin, New York.
Gould, H., Tobochnik, J., and Christian, W. (2006) 《计算机模拟方法导论》, 第3版, Addison-Wesley, Reading, USA.
Graps, A. (1995) 《小波导论》. Comput. Sci. Eng., 2, 50.
Gurney, W.S.C. and Nisbet, R.M. (1998) 《生态动力学》, Oxford University Press, Oxford.
Haftel, M.I. and Tabakin, F. (1970) Nucl. Phys., 158, 1.
Hardwich, J. (1996) 《优化规则》, www.cs.cmu.edu/~jch/java (访问日期：2015年3月22日).
Hartmann, W.M. (1998) 《信号、声音与感觉》, AIP Press, Springer, New York.
Higgins, R.J. (1976) 《快速傅里叶变换：介绍及一些小型计算机实验》. Am. J. Phys., 44, 766.
Hildebrand, F.B. (1956) 《数值分析导论》, McGraw-Hill, New York.
Hinsen, K. (2013) 《可重复研究的软件开发》. Comput. Sci. Eng, 4 (15), 60–63, www.computer.org/portal/web/cise/home (访问日期：2015年3月22日).
History of Python (2009) 《Python历史》 python-history.blogspot.com/2009/01/brief-timeline-of-python.html (访问日期：2015年3月22日).
Hockney, R.W. and J.W. Eastwood (1988) 《粒子计算机模拟》, Adam Hilger, Bristol.
Hubble, E. (1929) 《河外星云距离与径向速度之间的关系》. Proc. Natl. Acad. Sci. USA, 15 (3), 168.
Hunag, K. (1987) 《统计力学》, John Wiley & Sons, New York.
Jackson, J.D. (1988) 《经典电动力学》, 第3版, John Wiley & Sons, New York.
Jackson, J.E. (1988) 《主成分用户指南》, John Wiley & Sons, New York.
Jolliffe, I.Y. (2001) 《主成分分析》, 第2版, Springer, New York.
José, J.V. and Salatan, E.J. (1988) 《经典动力学》, Cambridge University Press, Cambridge.
Kennedy, R. (2006) 《波洛克分形案例聚焦物理学》, New York Times, 2, 5 December 2006.
Kirk, D. and Wen-Mei, W.H. (2013) 《大规模并行处理器编程》, 第2版, Morgan Kauffman, Waltham.
Kittel, C. (2005) 《固体物理学导论》, 第8版, John Wiley & Sons, Inc., Hoboken.
Klöckner, A. (2014) PyCUDA, mathematician.de/software/pycuda (访问日期：2015年3月22日).
Koonin, S.E. (1986) 《计算物理学》, Benjamin, Menlo Park, CA.
Korteweg, D.J. and deVries, G. (1895) Philos. Mag., 39, 4.
Kreyszig, E. (1998) 《高等工程数学》, 第8版, John Wiley & Sons, New York.
Lamb, H. (1993) 《流体动力学》, 第6版, Cambridge University Press, Cambridge.
Landau, D.P. and Wang, F. (2001) 《确定经典统计模型的态密度：产生平坦直方图的随机游走算法》. Phys. Rev. E, 64, 056101; Landau, D.P., Tsai, S.-H., and Exler, M. (2004) 《统计物理中蒙特卡洛模拟的新方法：王–兰道采样》. Am. J. Phys., 72, 1294.
Landau, L.D. and Lifshitz, E.M. (1987) 《流体力学》, 第2版, Butterworth-Heinemann, Oxford.
Landau, L.D. and Lifshitz, E.M. (1976) 《量子力学》, Pergamon, Oxford.
Landau, L.D. and Lifshitz, E.M. (1976) 《力学》, 第3版, Butterworth-Heinemann, Oxford.
Landau, R.H. (2008) 《资源信函CP-2：计算物理学》. Am. J. Phys., 76, 296.
Landau, R.H. (2005) 《科学计算入门教程》, Princeton University Press, Princeton.
Landau, R.H. (1996) 《量子力学II：量子理论第二教程》, 第2版, John Wiley & Sons, New York.




C/C++ 代码) 或与已执行指令的二进制文件和/或痕迹 [41]。近年来，针对动态硬件/软件分区的方法受到更多关注（参见，例如，[7,42]）。其他方法考虑硬件/软件组件的静态准备，但将在硬件或软件中执行计算的决策委托给运行时。例如，Beisel 等人 [28] 提出了一种在运行时决定库函数级别硬件/软件分区的系统。该系统拦截库调用，并对每个调用决定将调用卸载到硬件加速器。决策基于存储每个受支持函数和不同数据大小执行时间信息的表格。其他决策还可以考虑其他信息，例如每个循环在每个执行点将执行的迭代次数（在运行时计算），以决定将计算卸载到硬件加速器。Vaz 等人 [29] 提议将应用程序中的决策点移动，以可能隐藏一些开销，例如协处理器执行的准备。

当前的异构多核架构支持 GPU 和/或可重构硬件（例如，由 FPGA 提供），并有可能提供不同的执行模型和架构，从而增加了将计算映射到目标组件的复杂性。系统可能不仅需要考虑可能适合特定目标的代码转换，还需要决定在哪里执行计算，这并非易事。例如，当考虑由 CPU + GPU 组成的目标架构时，系统可能需要决定在多核 CPU 上还是在 GPU 上执行 OpenCL 内核 [30]。问题的复杂性以及做出决策所涉及的可变参数正在通过复杂的解决方案来解决，例如使用机器学习技术基于静态和动态代码特征来估计执行时间 [31]。其他作者在针对 GPU 加速时解决数据迁移问题 [32]。由于这些是热门研究主题，预计将提出进一步的解决方案，特别是考虑代码转换、工作负载、运行时适应性和目标架构特定性之间的相互作用。

## REFERENCES

- [1] Mathworks 公司，MATLAB——技术计算语言。http://www.mathworks.com/products/matlab [2016 年 5 月访问]。
- [2] Simulink——仿真和基于模型的设计——MathWorks，© 1994–2016 The MathWorks, Inc.，www.mathworks.com/products/simulink/ [2016 年 5 月访问]。
- [3] Corre Y, Hoang V-T, Diguet J-P, Heller D, Lagadec H, 基于 LHS 的 ad hoc 硬件加速器快速设计空间探索：FPGA 上 MPSoC 综合的关键工具。载于：信号和图像处理设计与架构国际会议 (DASIP’2012)，2012 年 10 月 23–25 日，8 页。
- [4] Kernighan BW. C 程序设计语言。第 2 版。Piscataway, NJ: Prentice Hall; 1988。
- [5] Octave 主页。http://www.gnu.org/software/octave/ [2016 年 5 月访问]。
- [6] Scilab：主页，© Scilab Enterprises S.A.S 2013。http://www.scilab.org/ [2016 年 1 月访问]。
- [7] UT DSP 基准套件。http://www.eecg.toronto.edu/~corinna/DSP/Infrastructure/UTDSP.html [2016 年 3 月访问]。
- [8] Fowler M. 领域特定语言。第 1 版。Boston, USA: Addison-Wesley Professional; 2010。
- [9] 欢迎访问 UML 网站！Copyright © 1997–2016 Object Management Group®, Inc. http://www.uml.org/ [2016 年 5 月访问]。
- [10] Ptolemy 项目主页。Copyright © 1999–2016 UC Regents. ptolemy.eecs.berkeley.edu/ [2016 年 5 月访问]。
- [11] 什么是硬件在环仿真？© 1994–2016 The MathWorks, Inc. http://www.mathworks.com/help/physmod/simscape/ug/what-is-hardware-in-the-loop-simulation.html [2016 年 5 月访问]。
- [12] Kirchhoff U., J. Mendhekar A. Maeda C, Lopes CV, Jean-Marc L, 等。面向切面编程。载于：第 11 届面向对象编程欧洲会议 (ECOOP’97)，芬兰 Jyväskylä，1997 年 6 月 9–13 日，计算机科学讲义 (LNCS)，第 1241 卷。Heidelberg: Springer-Verlag; 1997. 第 220–42 页。
- [13] Elrad T, Filman RE, Bader A. 面向切面编程：简介。Commun ACM 2001;44(10):29–32。
- [14] 角点检测。https://en.wikipedia.org/wiki/Corner_detection [2016 年 5 月访问]。
- [15] Fingeroff M. 高层次综合蓝皮书。Bloomington, IN: Xlibris Corporation; 2010。
- [16] Vivado 高层次综合。http://www.xilinx.com/products/designtools/vivado/integration/esl-design.html [2016 年 1 月访问]。
- [17] Arató P, Mann ZA, Orbán A. 硬件/软件分区的算法方面。ACM Trans Des Autom Electron Syst (TODAES) 2005;10(1):136–56。
- [18] Duran A, Ayguadé E, Badia RM, Labarta J, Martinell L, Martorell X, 等。OmpSs：异构多核架构编程提案。Parallel Process Lett 2011;21(02):173–93。
- [19] Wessing JR, Stiti G. 弹性计算：面向多核异构计算的透明、可移植和自适应框架。载于：ACM SIGPLAN/SIGBED 嵌入式系统语言、编译器和工具会议论文集；2010. 第 115–24 页。
- [20] Cardoso JMP, Carvalho T, Coutinho JGF, Nobre R, Nane R, Diniz PC, 等。使用 LARA 切面控制综合工具链中的设计复杂性。Microprocess Microsyst 2013;37(8):1078–89。
- [21] Cardoso JMP, Coutinho JGF, Carvalho T, Diniz PC, Petrov Z, Luk W, 等。使用 LARA 面向切面编程方法的性能驱动插装和映射策略。载于：Software: practice and experience (SPE)。New York, NY, USA: John Wiley & Sons Ltd; 2014. 12 月。
- [22] Fabry J, Dinkelaker T, Noyé J, Tanter É. 领域特定切面语言分类法。ACM Comput Surv 2015;47(3): 文章 40，44 页。
- [23] Cardoso JMP, Diniz P, Coutinho JG, Petrov Z，编。嵌入式可重构系统的编译与综合：面向切面方法。第 1 版。New York, Dordrecht, Heidelberg, London: Springer; 2013. 5 月。
- [24] Bertels K, Sima VM, Yankova Y, Kuzmanov G, Luk W, Coutinho JGF, 等。HArtes：异构多核平台的硬件/软件协同设计。IEEE Micro 2010;30(5):88–97。
- [25] López-Vallejo M, López JC. 关于硬件/软件分区问题：系统建模和分区技术。ACM Trans Des Autom Electron Syst 2003; 8(3):269–97。
- [26] Ernst R, Henkel J, Benne T. 微控制器的硬件/软件协同综合。IEEE Des Test 1993;10(4):64–75。
- [27] Stitt G, Lysecky R, Vahid F. 动态硬件/软件分区：一种初步方法。载于：第 40 届设计自动化年会 (DAC’03) 论文集。New York, NY, USA: ACM; 2003. 第 250–5 页。
- [28] Beisel T, Nickamp M, Plessl C. 使用共享库拦截在具有异构硬件加速器的系统中实现透明加速。载于：面向特定应用的系统、架构和处理器国际会议 (ASAP’10) 论文集。IEEE Computer Society，7 月：2010. 第 65–72 页。
- [29] Vaz G, Riebler H, Kenter T, Plessl C. 将动态卸载决策嵌入应用程序代码的潜力和方法。Comput Electr Eng 2016;55(9):1–11。
- [30] Wang Z, Grove D, O’Boyle MIF. 面向基于 GPU 的异构系统的数据并行程序到 OpenCL 的自动可移植映射。ACM Trans Archit Code Optim 2014;11(1):26。
- [31] Wen Y, Wang Z, O’Boyle M. CPU/GPU 异构平台上 OpenCL 程序的智能多任务调度。载于：第 21 届 IEEE 高性能计算国际会议 (HiPC’14) 论文集，印度果阿，IEEE。2014 年 12 月 17–20 日。10 页。
- [32] Wang B, Wu B, Li D, Shen X, Yu W, Jiao Y, 等。通过软件/硬件协同设计探索混合内存以提高 GPU 能效。载于：第 22 届并行架构和编译技术国际会议 (PACT’13) 论文集，IEEE Press，Piscataway, NJ，2013. 第 93–102 页。
- [33] Hickey PC, Pike L, Elliott T, Bielamann J, Launchbury J. 使用嵌入式 DSL 构建嵌入式系统。载于：第 19 届 ACM SIGPLAN 函数式编程国际会议 (ICFP ’14) 论文集。New York, NY, USA: ACM; 2014. 第 3–9 页。
- [34] Graepel T, Candela JQ, Borchert T, Herbrich R. 面向 Microsoft Bing 搜索引擎赞助搜索广告的 Web 规模贝叶斯点击率预测。载于：第 27 届机器学习国际会议 (ICML-10) 论文集；2010. 第 13–20 页。
- [35] Augonnet C, Thibault S, Namyst R, Wacrenier P-A. StarPU：异构多核架构任务调度的统一平台。Concur Comput Pract Eng 2011;23(2):187–98。
- [36] Linderman MD, Collins JD, Wang H, Meng TH. Merge：异构多核系统的编程模型。ACM SIGOPS Oper Syst Rev 2008;42(2)。
- [37] O’Neill E, McGloin J, Coutinho JGF, Doole A, Ragusa C, Pell O, Sanders P. 异构处理器间数据库功能的跨资源优化。载于：带应用的并行和分布式处理 (ISPA)，26–28 Aug.；2014. 第 150–7 页。
- [38] Cardoso JMP, Carvalho T, de F. Coutinho JG, Luk W, Nobre R, Diniz PC, 等。LARA：嵌入式系统的面向切面编程语言。载于：面向切面软件开发国际会议 (AOSD’12) 论文集，德国波茨坦，3 月 25–30 日。ACM; 2012. 第 179–90 页。
- [39] Kiczales G, Lamping J, Mendhekar A, Maeda C, Videira Lopes C, Loingtier J-M, Irwin J. 面向切面编程。载于：第 11 届面向对象编程欧洲会议 (ECOOP’97)，芬兰 Jyväskylä。1997 年 6 月 9–13 日，计算机科学讲义 (LNCS)，第 1241 卷。Springer; 1997. 第 220–42 页。
- [40] Gupta RK, De Micheli G. 数字系统的硬件/软件协同综合。IEEE Des Test Comput 1993;10(3):29–41。
- [41] Bispo J, Paulino N, Cardoso JMP, Ferreira JC. 面向可重构 HW/SW 系统的基于痕迹的透明二进制加速。IEEE Trans Ind Inform 2013;9(3):1625–34。
- [42] Lysecky R, Vahid F. 基于 MicroBlaze 的 warp 处理器的设计与实现。ACM Trans Embed Comput Syst 2009;8(3):21–22。


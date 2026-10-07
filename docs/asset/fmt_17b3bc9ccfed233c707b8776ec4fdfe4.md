
在过去的 5 年中，GUI 模型的自动化提取已成为热门研究课题。软件行业显然对自动化 GUI 测试的有效方法感兴趣，但另一个使其人气日益增加的重要原因是 GUI 框架提供了易于观察和交互 GUI 的便捷访问方法，例如 Jemmy [14]、Microsoft Automation [13] 和 Robotium [138]。这些 GUI 框架解决了模型提取中的许多技术问题，但随着研究的进行，挑战依然存在，新问题也随之出现。此外，还有实际问题阻碍了工具和方法在大规模工业中的应用，例如工具的可用性和扩展性。

## 6.1. 趋势

基于这项用于测试的 GUI 模型自动化提取的前沿研究，我们观察到以下趋势：(1) 使用混合方法进行模型提取的情况日益增加；(2) 已发布了首批具有良好前景的长期工业实践报告；(3) 使用提取的 GUI 模型进行测试的新方法；(4) 使用虚拟机进行模型提取的情况将增加。

在他们最新的工作中，该领域的许多研究人员结合了静态和动态分析，以提取更好、更详细的模型 [136]，或从提取的模型中生成更好的测试 [92]。动态分析一直是 GUI 模型提取的主流方法，但随着提取技术的演进和对更详细分析的需求，静态方法已被重新审视并与动态方法相结合。

尽管工业界对使用提取的模型进行自动化 GUI 测试的采用仍欠缺，但首批针对大型商业应用的长期工业评估已经发布，且结果令人鼓舞 [227]。随着方法和工具的演进以及可用性和扩展性的改进，大规模的工业采用将随之而来。本研究中提到的许多工具已作为开源软件发布，希望其使用的增加将加速开发。

大多数方法使用提取的 GUI 模型，基于 GUI 应用早期版本的行为生成带有断言（test oracles）的测试用例。通过这种方式可以检测行为的变化。最近的一研究 [227] 使用模型比较而非测试用例进行回归测试。其基本思想是提取每个新版本的模型，另一种利用提取的 GUI 模型的新方法是提供自动化工具支持以加速手动 GUI 测试活动 [227]。

虚拟机可用于减少模型提取和 GUI 测试期间的非确定行为，例如测试环境中的外部变化和事件，如操作系统通知用户有新的软件更新 [227]。在模型提取期间 GUI 重启时，恢复虚拟机的干净快照（如 [227] 所示），还可以消除无意的上下文信息，例如事件历史或影响 GUI 状态的长事件序列不会被捕获到模型中。我们预计使用虚拟机进行模型提取和 GUI 测试将增加。

## 6.2. 未来

随着计算机变得更快更好，保持模型提取快速和提取模型规模较小将不再是问题。在此之前，我们必须不断寻找平衡：既不覆盖 GUI 的所有可能交互以保持提取速度，又能提取具有足够 GUI 覆盖率的模型；并抽象不必要的细节以保持模型足够小到计算上可行，但又能捕捉足够的信息以明确确定 GUI 的状态。尽管某些方法旨在实现全自动 GUI 测试，但在实践中始终需要手动投入。问题在于手动投入的最佳位置是提供有意义的输入、验证提取模型的正确性，还是其他地方。这些步骤中的大部分可以在自动化步骤之前或之后通过手动投入更新。

## REFERENCES

[1] X. Yang. GUI interface modelling and test automation, PhD thesis, School of Engineering, Victoria University, Melbourne, 2011.

[2] J. Silva, J.S. Sarava, J.C. Campos, A generic library for GUI reasoning and testing, in: Proc. 2nd Ind. Workshop on Formal Methods for Interactive Systems (FMIS 2007), 4 September, Lancaster, UK, 2007, pp. 77–93.

[3] A.M. Memon, A. Nagarajan, Q. Xie, Automating regression testing for evolving GUI software, Softw. Mant. Res. Pract. 18 (2) (2008), article no. 4., ACM New York, NY, pp. 1–36.

[4] J. Canny, The future of human-computer interaction, ACM Queue 6 (6) (2006) 24–32, ACM, New York, NY.

[5] B.A. Myers, UIMS, toolkits, builders, ACM Comput. Hum. Interact. 2 (1) (1995), Human Interaction Institute, Carnegie Mellon University, May 24, 1996. A revised version of “User Interface Software Tools”.

[6] A.M. Memon, Using reuse for automated usability evaluation of GUI-based applications, in: A. Sefifah, J. Vanderdonckt, M.C. Desimaris, Human-Centered Software Engineering: Engineering Models, Patterns and Architectures for HCI, Springer, London, 2009, pp. 335–355.

[7] J. Silva, J.S. Sarava, J.C. Campos, A generic library for GUI reasoning and testing, in: Proc. 2009 ACM Symposium on Applied Computing (SAC'09), 8–12 Mar 2009, Honolulu, HI, USA, 2009, pp. 121–128.

[8] A.M. Memon, GUI testing pitfalls and process, Computer 35 (8) (2002) 87–88, IEEE Computer Society.

[9] ... （此处原文截断，未翻译参考文献）

# 模型的 GUI 自动化工程

[10] B.A. Myers, S.E. Hudson, R. Pausch, 用户界面软件工具的现在与未来, ACM Trans. Comput. Hum. Interact. 7 (1) (2000) 3–28.

[11] B.A. Myers, S.Y. Park, Y. Nakano, G. Mueller, A. Ko, 设计师如何设计以及设计行为；in: Proc. 2008 IEEE Symposium on Visual Languages and Human-Centric Computing (VL/HC), 15–19 Sep 2008, Hersberg, Germany, 2008, pp. 177–184.

[12] A.M.P. Brito, A.C.R. Pavia, J.P. Faria, 用于测试的 GUI 模型逆向工程，in: Proc. 2010 5th Iberian Conf. Information Systems and Technologies (CISTI), 16–19 June 2010, Santiago de Compostela, 2010, pp. 177–184.

[13] Microsoft UI Automation。`http://msdn.microsoft.com/en-us/library/ms74327(vs=11.0)`

[14] Jenny, 用于 GUI 自动化的开源 Java 库。`http://jenny.java.net`.

[15] K. Li

[16] P. A, N. Mensch, T. Raty, 用于测试的 GUI 模型逆向工程，in: Proc. 2013 Int. Conf. Control and Information Technologies (CoDIT13), 6–9 March 2013, , pp. 441–447.

[17] M. Utting, B. Regan, 基于模型的测试：一种方法, Morgan Publishers Inc., San Francisco, CA, 2006.

[18] T. Kanstrën, A, 基于观测的测试框架, VTT Publications 727, Espoo, Finland, 2010.

[19] K. Gull, 自动 GUI：现状，in: Proc. 2012 IEEE 23rd Symposium on Reliability Engineering (ISSREW), 27–30 November 2012, Dallas, TX, 2012, pp. 207–212.

[20] T. Systac, Java 静态与动态逆向工程, Electa 35, Tamparen, 2000.

[21] R. Kollmann, P. Selonen, E. Stroulia, T. Austi, A. Zindorf, 工具支持的 UML 逆向工程研究，in: 9th Winter Conf. on Reverse Engineering (WCRE’02), 29 Oct 2002, Richmond, VA, USA, 2002, pp. 22–32.

[22] A.M. Menon, B.N. Nguyen, GUI 前端自动化模型测试进展，博士论文, Adv. Comput. 80 (2010) 121–162, Elsevier Inc.

[23] B. Nguyen, 未定义参数的 GUI 测试，Department of Computer Science, University of Maryland, College Park, 2013.

[24] P. Ao, N. Mensch, T. Raty, 有效数据增强 GUI 生成，in: Proc. 2011 IEEE Conf. on Systems (ICOS 2011), 25–28 Sep 2011, Langawi, Malaysia, 2011, pp. 310–315.

[25] A.M. Menon, GUI 应用的事件驱动流模型，Softw. Test. Verif. Rel. 17 (3)(2007) 137–157, John Wiley and Sons Ltd, Chichester, UK.

[26] J. Bancerij, B. Nguyen, V. Garousis, A.M. Menon, 图形用户界面 (GUI) 测试：系统映射与存储，Inform. Softw. Technol. 55 (10) (2013) 1699–1694, Elsevier.

[27] X. Yuan, A.M. Menon, 使用 GUI 运行时后端生成序列测试用例，IEEE Trans. Soft. Eng. 36 (1) (2016) 81–95, IEEE Computer Society.

[28] R.J.K. Jacob, A. Girouard, L.M. Hirshield, M.S. Horn, O. Shaer, E.T. Solovy, J. Ziegelbaum, 基于现实的交互：一种后-WIMP 接口框架，in: Proc. SIGCHI on Human Factors in Computing Systems (CHI ’08), 5–10 Apr 2008, Florence, Italy, 2008, pp. 201–210.

[29] A. Dam, 后-WIMP 用户界面，ACM Commun. 40 (2) (1997) 63–67, ACM, New York, NY.

100

Pekka Aho 等人。

[30] IEEE Computer Society Professionals Committee, 软件工程知识体系：2004 版本，IEEE Computer Society, 2004.

[31] IEEE 软件工程标准，ANSI/IEEE Std 610.12-1990, IEEE Standards Association, New York, NY.

[32] F. Belli, M. Linch, 服务的事件驱动建模和测试，in: Proc. 32nd Annual IEEE Int. Conf on Software Systems and Applications (COMPACS'08), 28 Jul 2008, Turku, Finland, 2008, pp. 116–173.

[33] X. Yuan, M. Cohen, GUI 工程：结合事件，IEEE Trans. Softw. Eng. 37 (4) (2011) 559–574, IEEE Computer Society.

[34] Q. Xie, 一项利用试点研究驱动自动化测试 GUI 模型的逆向工程事件，ACM Softw. Method. 18 (2) (2008), 文章编号. 7. ACM, New York, NY.

[35] D. Iglesias, L. Castro, 图形用户界面属性测试，J. Comput. Inform. Technol. 1 (3) (2011) 60–71, Academy.

[36] P. Brooks, A. Robinson, 工业系统的初始表征，in: IEEE Int. Conf. on Software Verification and Validation (ICST 2009), 4 Apr 2009, Denver, CO, 2009, pp. 11–20.

[37] J. Bowen, S. Reijmers, UI 驱动的基于测试，Innov. Softw. Eng. 19 (3) (2009) 21–35.

[38] J.C. Campos, C. Silva, 用户界面软件逆向工程框架，in: Reverse Engineering—进展与应用, March 2012, InTech, 2012, pp. 31–54.

[39] P. Santos, R. Resende, C. Padua, 信息系统测试，in: Proc. 2007 ACM Symposium on Applied Computing (SAC), 11–15 Mar 2007, Seoul, Korea, 2007, pp. 1409–415.

[40] A. Bertolino, P. Invernardi, H. Muccini, 通向自动化测试，in: Proc. Int. Conf. on Dependable Systems and Networks (DSN2004), 28 Jun 2004, Florence, Italy, 2004, pp. 124–125.

[41] G.Z. Holzmann, M. Smith, 基于模型提取的分布式系统自动化验证方法，IEEE Trans. Softw. 28 (4) (2002) 364–367, IEEE Computer Society.

[42] M. Charmank, Q. Xie, C. Fu, 维护和执行 GUI 驱动的测试脚本，in: Proc. 2009 31st Int. Conf. on Software Engineering (ICSE 2009), 16–24 May 2009, Vancouver, Canada, 2009, pp. 408–418.

[43] jUnit, 用于 Swing 应用的 JUnit 框架扩展。`http://junit.sourceforge.org`.

[44] J. Andersson, G. Bache, 视频商店复兴：GUI 验收，in: Proc. 5th Int. Conf. on Extreme Programming and Agile in Software Engineering (XP’2004), 6–10 Jun 2004, Garnisch-Partirchen, Germany, 2004, pp. 1–10.

[45] Abstract, GUI 组件和程序的自动化测试框架。`http://abstract.sourceforge.org`.

[46] Squish, 用于 GUI 回归测试的 GUI 测试自动化工具。`http://www.froglogic.com/squish-ui-testing`.

[47] JITE, GUI 测试自动化框架。`http://marathontesting.com`.

[48] T. Y, T. Chang, R.C. Miller, Sikuli：使用 GUI 截图进行搜索和自动化，in: Proc. 22nd Annual ACM Symposium on User Interface Software and Technology, 4–7 Oct 2009, Victoria, Canada, 2009, pp. 183–192.

[49] Sikuli, 使用截图进行自动化测试和 GUI 测试的工具。`http://docs.sikuli.org`.

[50] SeleniumHQ, Web 应用自动化测试工具。`http://docs.seleniumhq.org`.

[51] Appium, 用于原生和混合移动应用的开源测试框架。`http://appium.io`.

[52] A. Kivinen, M. Maunmaa, M. Katara, 使用三层架构控制测试，in: Proc. 2nd Workshop on Model Based Testing (MBT 2006), 25–26 Mar 2006, Vienna, Austria, 2006, pp. 53–66.

[53] Enterprise Architect, 概念建模。`http://www.sparx`.

[54] Conformiq Designer, 概念测试。`http://www.conformiq.com/designer/`.



## 参考文献

- Ting N. (2006). 引言与药物开发过程。In Ting N, ed. *药物开发中的剂量发现*. New York: Springer.

- Ting N. (2011). 治疗慢性疾病的第2期临床开发。*Drug Information Journal* 45: 431–442。

- 国际协调会议. (1997). E8: 临床试验的一般考虑因素。访问：[http://www.ich.org/fileadmin/Public_Web_Site/ICH_Products/Guide]

- 国际协调会议. (1994). E4: 支持药物注册的剂量-响应关系。访问：[http://www.ich.org/fileadmin/Public_Web_Site/ICH_Products/Guide]

- Grieve AP. (2011). 适应性试验设计：寻找答案。*International Clinical Trials*, Issue 22, 16-20.

- Trevor AJ, Katzung BG, Masters SB. (2010). *Katzung and Trevor’s药理学考试与委员会评审*, 第九版. New York: McGraw Hill, 15.

- Ting N. (2008). 确认与探索：临床试验设计的步进式方法。*Drug Information Journal* 42: 545-554.

- Thomas N & Ting N. (2009). 最小有效剂量。In D’Agostino RB, Sullivan L, Massaro J, eds. *临床试验百科全*. Hoboken, NJ: Wiley-Blackwell.

- Fillon TG. (1995). 通过回归模型和百分位数估计估计化合物的最小治疗有效剂量。*Statistics in Medicine* 14: 925-932.

- Pinheiro JC, Bornkamp B & Bretz F. (2006). 结合多次比较和建模程序的剂量药研究的设计与分析。*Journal of Biopharmaceutical Statistics* 16: 639–656.

11. Hochberg Y & Tamhane A. (1987). 多重比较程序。New York: Wiley.

12. Wang X & Ting N. (2012). 结合剂量范围探索的概念性临床试验设计。Pharmaceutical Statistics 11: 403-409.

13. Pinheiro J, Bretz F & Branson. (2006). 剂量-响应研究分析-建模方法。In Ting N, ed. 药物开发中的剂量发现. New York: Springer.

14. Ting N, ed. (2006). 药物开发中的剂量发现. New York: Springer.

15. Hamlet A, Ting N, Hanumara C & Finman JS. (2002). 早期反应临床试验设计中的剂量间隔。Drug Information Journal 36: 855-864.

16. Ting N. (2009). II期骨关节炎临床试验设计的实际与统计考量：案例研究。Communications in Statistics – Theory and Methods 38: 3282-3296.

17. Penel N & Kramar A. (2012). 修改的斐波那契剂量递增广泛对应什么？BMC Medical Research Methodology 12: 103.

18. Quinian JA & Krams M. (2006). 执行适应性设计：逻辑与运营考量。Drug Information Journal 40: 437-444.

19. Krams M, Lees KR, Hacke W, Orgogozo JM & Ford GA 为 ASTIN 研究小组。(2003)。ASTIN: 针对急性缺血性卒中 UK-279,276 的适应性剂量-响应研究。Stroke 34: 2543-254.

20. Yuan G & Ting N. (2014). 首剂量范围临床试验设计：更多剂量？还是更宽的范围？In Young WR & Chen DG, eds. 临床试验生物统计学与生物医药应用。Boca Raton, FL: Chapman and Hall/CRC.

- 21. Chow SC, Shao J & Wang H. (2007). 临床研究中的样本量计算，第二版。Boca Raton, FL: Chapman & Hall/CRC.

- 22. Bellamy N, Campbell J, Stevens J, Pilcher L, Stewart C & Mahmood Z. (1997). 西安大略和麦克马斯特大学 VA3.0 骨关节炎指数计算机化版本的验证研究。Journal of Rheumatology 24: 2413-2415.

- 23. Fedorov VV & Leonov SL. (2014). 非线性响应模型的优化设计。Boca Raton, Florida: Chapman and Hall/CRC.

- 24. MacDougall J. (2006). 剂量-响应研究分析 – Emax 模型。In Ting N, ed. 药物开发中的剂量发现. New York: Springer.

## 作者

Naitee Ting，高级首席生物统计学家，勃林格殷恩格翰制药有限公司，美国康涅狄格州里奇菲尔德。

袁郭君，全球生物统计总监，EMD Serono, Inc（默克 KgaA 子公司），美国马萨诸塞州比勒卡。

François Beckers，全球生物统计学负责人，Merck Serono, Inc（默克 KgaA 子公司），德国达姆施塔特。

## 第7章：用于剂量-响应测试的 MCP-Mod

### 7.1 引言
### 7.2 方法论
### 7.3 设计阶段 MCP-Mod 的考量
### 7.4 使用 SAS 的示例
### 7.5 结论
### 7.6 参考文献
### 7.7 附录

#### 7.1 引言
药物行业中一个众为人知的问题是为III期选择合适的剂量。历史上，剂量发现研究是基于多次比较进行设计和分析的。然而，在II期，精确的剂量-响应关系通常是未知的。

MCP-Mod 方法最近被认为是处理II期设计和分析中模型不确定性的有效方法。在设计阶段，识别一组合适的模型；在分析阶段，使用趋势检验对这些模型进行剂量响应测试。一旦建立了剂量-响应信号，将使用集合中的最佳模型进行目标估计。

然而，其结论的有效性很大程度上取决于对模型的适当选择。在本章的剩余部分，我们将详细介绍 MCP-Mod 的核心方法论，包括对通用模型的扩展，通过示例进行说明，并提供底层 SAS 代码。

#### 7.2 方法论

##### 7.2.1 原始 MCP-Mod 方法
在本节中，我们首先为单正态分布终点提供原始 MCP-Mod 方法 [2] 的简短技术描述。随后，我们描述了一种最近开发的 MCP-Mod 变体，该变体将方法论扩展到通用参数模型的剂量发现研究（例如二分类、计数或事件终点，并包括某些纵向方法），[4]。

MCP-Mod 程序通过五个步骤实施；参见图 7.1 原始 MCP-Mod 程序的分层概述：

- 在设计阶段，识别若干候选剂量响应形状，这些形状可能代表真实的剂量响应关系。
- 推导出优化对比系数，使得检测与相应候选模型的特定剂量响应形状的边际功效最大化。
- 在分析阶段，基于之前的优化系数通过多次对比检验评估单个形状的显著性，以评估是否可以建立剂量响应信号。这形成了 MCP-Mod 的 MCP 部分。
- 使用模型选择准则（如 AIC 或 BIC）选择候选模型或使用模型平均法。
- 使用选定的模型通过基于的方法对适当剂量进行推断。这形成了 MCP-Mod 的 Mod 部分。


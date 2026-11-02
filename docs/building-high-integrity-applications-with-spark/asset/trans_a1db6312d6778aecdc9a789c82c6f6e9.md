
- 6. McCormick 等人（2011）对在 Ada 中与硬件交互进行了完整讨论。
- 7. 感谢 Altran UK 的 Angela Wallenburg 和 AdaCore 的 Yannick Moy 提供此示例。
- 8. 抽象状态方面的完整语法见《SPARK 2014 参考手册》（SPARK Team，2014a）第 7.1.4 节。
- 9. 此示例的全部源代码可在 http://www.cambridge.org/us/academic/subjects/computer-science/programming-languages-and-applied-logic/building-high-integrity-applications-spark?format=PB 获取。

## 8 使用 SPARK 的软件工程

- 1. 当函数 Empty 被编写为普通函数时，其后置条件未能得到证明。SPARK 工具不会为子程序生成后置条件。当把后置条件添加到该普通函数的主体后，证明成功了。由于表达式函数的结果被视为该函数的后置条件，因此只要有可能，就值得使用表达式函数而不是普通函数。
- 2. 感谢 Rod Chapman 建议使用“验证驱动开发”这一名称。
- 3. 该方法的名称大致源自这样一种概念：将信息流作为设计构成系统的对象或实体的核心工具。INFORMED 是 INformation Flow ORiented MEthod of Design（面向信息流的设计方法）的首字母缩写。
- 4. 例如，定义记录类型会隐式定义相等性和字段选择操作。我们可能会添加诸如“小于或等于”之类的附加操作。
- 5. 流行的 OpenSSL 库中的 Heartbleed 漏洞，部分原因是在同一缓冲区对象中混合了敏感数据与非敏感数据。
- 6. 经典的口语化定义：验证——我们是否正确地构建产品？确认——我们是否构建了正确的产品？
- 7. Bob 还必须相信所使用的各种密码算法是安全的。

## 9 高级技术

- 1. 当断言策略设置为 Check 时，Ada 断言是可执行的。因此，当断言策略设置为 Check 时，幽灵函数可能会被执行。
- 2. SPARK 的未来版本可能允许在 Assume 编译指示中使用 'Old。
- 3. 感谢 Johannes Kanig。
- 4. 兼容证明器的完整列表见 http://why3.lri.fr/#provers。
- 5. 另请注意子类型谓词，尽管在撰写本文时，SPARK 尚不支持 Dynamic_Predicate。
- 6. 此后该限制已被部分解除，并且仍在继续改进 SPARK 工具在这一领域的工作。
- 7. 实际实现需要根据 X 的值选择正平方根或负平方根。

## 参考文献

- Ada 一致性评估机构。2012。《Ada 参考手册，ISO/IEC 8652:2012 (E)》。第 3 版。
- Adams, C.、Cain, P.、Pinkas, D. 和 Zuccherato, R. 2001（8 月）。RFC-3161：互联网 X.509 公钥基础设施时间戳协议（TSP）。加利福尼亚州弗里蒙特：互联网工程任务组。
- Aho, Alfred V.、Lam, Monica S.、Sethi, Ravi 和 Ullman, Jeffrey D. 2007。《编译器：原理、技术与工具》。第 2 版。马萨诸塞州波士顿：Addison Wesley。
- Amey, Peter. 2002。构造即正确：更好也可以更便宜。《CrossTalk，国防软件工程杂志》，15(3)，24–28。
- Ammann, Paul 和 Offutt, Jeff. 2008。《软件测试导论》。剑桥：剑桥大学出版社。
- Barnes, John. 2012。《SPARK：经过验证的高完整性软件方法》。http://www.altran.co.uk，英国：Altran Praxis。
- Barnes, John. 2014。《Ada 2012 程序设计》。剑桥：剑桥大学出版社。
- Beizer, Boris. 1990。《软件测试技术》。纽约：Van Nostrand Reinhold。
- Ben-Ari, Mordechai. 2009。《面向软件工程师的 Ada》。第 2 版。伦敦：Springer-Verlag。
- Bjørner, Nikolaj. 2012。使用 Z3 将可满足性提升到新水平。第 1–8 页，载于：Gramlich, Bernhard、Miller, Dale 和 Sattler, Uli（编），《自动推理》。计算机科学讲义，第 7364 卷。柏林：Springer。
- Black, Rex. 2007。《实用软件测试：成为有效且高效的测试专业人员》。印第安纳波利斯：Wiley。
- Blair, Michael、Obenski, Sally 和 Bridickas, Paula. 1992。《爱国者导弹防御：软件问题导致沙特阿拉伯达兰的系统故障》。技术报告 GAO/IMTEC-92-26。华盛顿特区：美国总审计局。
- Bobot, François、Fillâtre, Jean-Christophe、Marché, Claude 和 Paskevich, Andrei. 2011。Why3：看管你的证明器群。载于：中间验证语言研讨会（第 53–64 页）。波兰弗罗茨瓦夫。
- Chapin, Peter. 2014。Thumper。https://github.com/pchapin/thumper。
- Chapman, Roderick、Botcazou, Eric 和 Wallenburg, Angela. 2011。SPARKSkein：Skein 的形式化快速参考实现。第 16–27 页，载于：第 14 届巴西形式化方法会议：基础与应用论文集。SBMF'11。柏林：Springer-Verlag。
- Chapman, Roderick 和 Schanda, Florian. 2014。我们到了吗？使用 SPARK 进行工业定理证明的 20 年。第 17–26 页，载于：Klein, Gerwin 和 Gamboa, Ruben（编），《交互式定理证明》。计算机科学讲义，第 8558 卷。瑞士：Springer International Publishing。
- Comar, Cyrille、Kanig, Johannes 和 Moy, Yannick. 2012。《将形式化程序验证与测试集成》。技术报告。AdaCore。http://www.adacore.com/uploads_gems/Hi-Lite_ERTS-2012.pdf。
- Croxford, Martin 和 Chapman, Roderick. 2005。构造即正确：高完整性软件宣言。《CrossTalk，国防软件工程杂志》，18(12)，5–8。
- Dale, Nell 和 McCormick, John. 2007。《Ada 与数据结构：面向对象方法》，第 2 版。马萨诸塞州萨德伯里：Jones and Bartlett。
- Dale, Nell、Weems, Chip 和 McCormick, John. 2000。《使用 Ada 95 进行程序设计与问题求解》。第 2 版。马萨诸塞州萨德伯里：Jones and Bartlett。
- Davis, Noopur 和 Mullaney, Julia. 2003。《实践中的团队软件过程（TSP）：近期成果摘要》。技术报告 CMU/SEI-2003-TR-014 ESC-TR-2003-014。宾夕法尼亚州匹兹堡：卡内基梅隆大学软件工程研究所。
- DeRemer, Frank 和 Kron, Hans. 1975。大规模编程与小规模编程。第 114–121 页，载于：可靠软件国际会议论文集。纽约：美国计算机协会。
- Dross, Claire、Efstathopoulos, Pavlos、Lesens, David、Mentré, David 和 Moy, Yannick. 2014。《铁路、太空、安全：SPARK 2014 的三个案例研究》。http://www.spark-2014.org/uploads/erts_2014.pdf。
- Dutertre, Bruno. 2014。Yices 2.2。第 737–744 页，载于：Biere, Armin 和 Bloem, Roderick（编），《计算机辅助验证（CAV'2014）》。计算机科学讲义，第 8559 卷。德国海德堡：Springer。
- Eisenstadt, Marc. 1997。我最棘手的缺陷战争故事。《ACM 通讯》，40(4)，30–37。
- English, John. 2001。《Ada 95：面向对象编程的技艺》。http://www.adaic.org/resources/add_content/docs/craft/html/contents.htm。
- Epp, Susanna S. 2010。《离散数学及其应用》。第 4 版。加利福尼亚州太平洋格罗夫：Brooks/Cole Publishing。
- Gersting, Judith. 2014。《计算机科学中的数学结构》。第 7 版。纽约：W.H. Freeman。
- GNAT，2015a。《GNAT 参考手册》，http://docs.adacore.com/gnat_rm-docs/html/gnat_rm/gnat_rm.html。
- GNAT，2015b。《GNAT 用户指南》，http://docs.adacore.com/gnat_ugn-docs/html/gnat_ugn/gnat_ugn.html。
- Hall, Anthony 和 Chapman, Roderick. 2002。构造即正确：开发商业安全系统。《IEEE 软件》，19(1)，18–25。
- Humphrey, Watts. 2000。《团队软件过程导论》。SEI 软件工程丛书。马萨诸塞州波士顿：Addison Wesley。
- Humphrey, Watts. 2004。《安全改变一切》。在 ACM SIGAda 年度国际会议上发表的主题演讲，11 月 14–18 日，佐治亚州亚特兰大。
- Humphrey, Watts. 2006a（1 月）。有缺陷的软件也能工作。《SEI 新闻》。http://www.sei.cmu.edu/library/abstracts/news-at-sei/wattsnew20041.cfm。
- Humphrey, Watts. 2006b（2 月）。安全改变一切。《SEI 新闻》。http://www.sei.cmu.edu/library/abstracts/news-at-sei/wattsnew20042.cfm。
- 国际电信联盟。2002（7 月）。《信息技术——ASN.1 编码规则：基本编码规则（BER）、规范编码规则（CER）、可辨别编码规则（DER）规范》。瑞士日内瓦。
- Jones, Capers. 2000。《软件评估、基准与最佳实践》。Addison-Wesley 信息技术丛书。波士顿：Addison Wesley。
- Jones, Capers. 2012（9 月）。《2012 年的软件质量：现状调查》。新英格兰软件质量小组。http://sqgne.org/presentations/2012-13/Jones-Sep-2012.pdf。
- Jones, Capers. 2013。《软件缺陷来源与移除方法》。技术报告。罗德岛州纳拉甘西特：Namcook Analytics LLC。
- Jorgensen, Paul. 2008。《软件测试：工匠方法》。第 3 版。佛罗里达州博卡拉顿：Auerbach Publications。
- Kaner, Cem、Falk, Jack 和 Nguyen, Hung Quoc. 1999。《计算机软件测试》。第 2 版。印第安纳州印第安纳波利斯：Wiley。
- Knight, John、DeLong, Colleen、Gibbs, Matthew 和 Nakano, Luis. 1997（9 月）。为什么形式化方法没有被更广泛地使用？载于：Holloway, Michael 和 Hayhurst, Kelly（编），《第四届 NASA 兰利形式化方法研讨会论文集》，第 1–12 页。弗吉尼亚州汉普顿：NASA。
- Knuth, Donald. 1998。《计算机程序设计艺术：半数值算法》。第 2 卷。马萨诸塞州波士顿：Addison-Wesley。
- Mao, Wenbo. 2004。《现代密码学：理论与实践》。新泽西州上萨德尔河：Pearson。
- Marsh, William 和 O’Neill, Ian. 1994。《SPARK 的形式化语义》。技术报告。英格兰巴斯：Program Validation（可从 Altran Praxis 获取）。
- McCormick, John. 1997。论坛来信。《ACM 通讯》，40(8)，30。
- McCormick, John W.、Singhoff, Frank 和 Hugues, Jérôme. 2011。《使用 Ada 构建并行、嵌入式和实时应用》。英格兰剑桥：剑桥大学出版社。
- Mills, Harlan、Dyer, Michael 和 Linger, Richard. 1987。净室软件工程。《IEEE 软件》，4(5)，19–25。
- Moy, Yannick、Ledinot, Emmanuel、Delseny, Hervé、Wiels, Virginie 和 Monate, Benjamin. 2013。测试还是形式化验证：DO-178C 的替代方案与工业经验。《IEEE 软件》，30(3)，50–57。
- NASA。2011（1 月）。《国家公路交通安全管理局丰田意外加速调查》。技术评估报告 TI-10-00618。华盛顿特区：NASA 工程与安全中心。
- 纽约大学。2014。CVC4：SMT 求解器。http://cvc4.cs.nyu.edu/web/。
- 美国国家标准与技术研究院。2002（5 月）。《软件测试基础设施不足的经济影响》。规划报告 02-3。华盛顿特区：NIST。



# 基于知识的系统与法律应用

A.P.I.C. 系列 ·36·

![](img/fd9daa466aa6610f0ebd57e2ccc632c5_0_0.png)

编辑：TREVOR BENCH-CAPON

# 基于知识的系统与法律应用

这是 A.P.I.C. 系列的第 36 
总编辑：M.J.R. Shave 和 I.C. Wands
本系列的完整书目见本书末尾

# A.P.I.C. 系列
第 36 号

# 基于知识的系统与法律应用

编辑：

# T.J.M. BENCH-CAPON
英国利物浦大学
计算机科学系

![](img/fd9daa466aa6610f0ebd57e2ccc632c5_6_0.png)

学术出版社 (ACADEMIC PRESS)

Harcourt Brace Jovanovich 出版社
伦敦 圣地亚哥 纽约 波士顿
悉尼  东京 多伦多

学术出版社有限公司 (ACADEMIC PRESS LIMITED)
24/28 Oval Road,
伦敦 NW1 7DX

美国版由
ACADEMIC PRESS INC. 出版
圣地亚哥，CA 92101

版权所有 © 1991
ACADEMIC PRESS LIMITED

本书采用无酸纸印刷

版权保留所有权利

未经出版社书面许可，不得以影印、微缩或任何其他形式复制本书的任何部分

# 英国图书馆出版数据目录

现可用

ISBN 0-12-086441-X

于大不列印刷并装订
TJ Press Ltd., Padstow, Cornwall

# 目录

- 前言 vii
- 传记信息 xi
- 第一部分 - 背景 1
- 1 计算机程序中的法律表示 3
  Marek Sergot
- 2 DHSS 演示项目的机遇 69
  Trevor Bench-Capon
- 第二部分：任务 75
- 3 为司法裁决者提供的支持环境 77
  Andrew Taylor
- 4 为立法制定提供的支持 95
  Andrew Taylor 和 Trevor Bench-Capon
- 5 为公众提供的支持 115
  Nigel Gilbert
- 6 在多个应用中使用公共知识库 129
  Trevor Bench-Capon
- 第三部分：原型 137
- 7 本地办公室系统 139
  Justin Forder 和 Andrew Taylor
- 8 政策系统 165
  Graham Storrs
- 9 申诉人建议系统 183
  Nigel Gilbert
- 10 管理大型协作项目 199
  Charlie Portman
- 第四部分：问题 209
- 11 用于基于知识的系统的文本分析 213
  Elizabeth Cordingley
- 12 法律应用的知识表示 245
  Trevor Bench-Capon 和 Justin Forder
- 13 混合主导交互 265
  David Frohlich 和 Paul Luff
- 14 组决策 295
  Graham Storrs
- 15 组织与社会影响 309
  Andrew Taylor
- 16 结论 329
  Trevor Bench-Capon
- 参考文献 343
- 索引 365

# 前言

## 引言
人工智能本质上是一门实验性科学，应用于法律领域的基于知识系统的子领域也不例外这一通用原则。该领域受到许多显著实验的刺激，如 [McCarty 1977] 中描述的 McCarty TAXMAN、Rissland 的 HYPO [Rissland and Ashley 1977] 以及帝国理工学院的英国国籍法实验 [Sergot 1976]。通过实施方案，我们取得了进展，这些方案有助于澄清底层理念的优缺点，并通过对在工作系统中实现这些理念构想的经验进行反思，我们也获得了进步。当然，有价值的不仅是这些对实验的反思，还有整个社区的反思。本书旨在提供从 Alvey-DHSS 演示项目中在基于知识系统与法律领域进行的一系列相关实验中获得的经验以及一些教训。该项目运行于 1984 年至 1989 年，为开展持续性实验提供了一个难得的机遇。书中的章节代表了许多参与项目人员对项目的反思：他们的结论可能有所不同，但都基于共同的经验。

Alvey-DHSS 演示项目是一个大型演示项目，由英国贸易和工业部的 Alvey 指导部以及英国科学与工程研究委员会支持。项目合作者包括 ICL、Logica、帝国理工学院以及兰卡斯特大学、利物浦大学和萨里大学。此外，卫生和社会保障部（DHSS）指派了若干名员工全职参与该项目。

本书分为四个部分。第一部分包含了理解书中其余内容所需的背景材料。第二部分集中于目标组织内部的任务，该项目研究了支持这些任务的方法。识别出三个可以被基于知识系统（KBS）支持的独特领域，并为这三个领域构建了原型系统。从演示项目中获得的一个重要教训是：所支持任务的性质对支持该任务的系统性质具有全影响：构建一个系统并希望它能支持整个范围的用户是不恰当的。详细理各项任务的独特需求是演示项目的主要成就之一。第三部分详细介绍了构建的系统本身，这些章节也为书中其他章节的观察和一般评论提供了实验依据。最后一部分根据在法律领域构建 KBS 时出现的若干问题进行组织。因此，书中有关于知识分析、知识表示、与此类系统的交互性质、协作工作以及此类系统的社会和组织影响的章节。最后是一个结论性章节，我尝试整合各章节的一些线索，为讨论应用于法律领域的 KBS 产生一个框架。

感谢所有在项目漫长运行期间参与并以各种方式做出贡献的人。。这包括 Alison Adams, Jo Bird, Steve Blackburn, Tim Bond, Simon Booker, Julie Bourwe, Sarah Buckland, Christopher Burton, Alan Bustany, Tony Chandler, Marcus Clarke, Carolyn Lee, Cody Cox, Leo Crossfield, Ann Curry, Jo Dartnell, Sarah Hardy, Sandra Hill, Heather Hopkins, Steve Hopwood, Paul Portman, Howlin Wilson, Paul J.O. Marks, Lil Masterman, Rosemary Mathews, George Matieson, Tony McEnery, Linette Middleton, Alison Mill-Ingen, Hilary Milner, Steve Owianka, Mika Pappas, Chris Penn, Martin Perret, Nicky Perry, Sarah Pett, Ian Pickup, Charlie Portman, Mark Reader, Green Robinson, Peter Robinson, Tom Routen, Marek Sergot, Murray Shanahan, Graham Storrs, Andrew Taylor, Walton Tesdale, Chris Thomas, Steve Timms, Peter Turner, Richard Turner, Julie Weaver, Kelvin Hall van der Werve, Mary Whittaker, David Wolstenholme 和 Graham Young。我还要感谢利物浦大学帮助准备本书的同事们，特别是 Paul Dunne 和 Ken Chan。

# 传记信息

在牛津大学约翰学院学习哲学，并在那里获得了哲学博士学位（D. Phil.）。他在卫生和社会保障部的政策和计算机部门工作了六年，在那里他协助建立了 Alvey DHSS 演示项目。随后他前往伦敦帝国理工学院参与演示项目，并研究应用于立法的逻辑编程。自1987以来，一直是利物浦大学的计算机科学讲。

ELIZABETH S. CORDINGLE 在美国获得物理学学，随后在萨里大学获得社会研究硕士学位。她的研究经验包括对地方当局社会服务部门计算机的研究，并在1984 年 7 月至项目完成期间一直致力于 Alvey DHSS 演示项目。Elizabeth 目前在 BT 研究实验室担任执行工程师。

JUSTIN FORDER 是 Logica Cambridge Ltd 的首席顾问。在 Alvey DHSS 演示项目中，他参与了政策和本地办公室应用，以及工具包的定义和设计。他继续在决策支持中使用从项目中学到的教训。


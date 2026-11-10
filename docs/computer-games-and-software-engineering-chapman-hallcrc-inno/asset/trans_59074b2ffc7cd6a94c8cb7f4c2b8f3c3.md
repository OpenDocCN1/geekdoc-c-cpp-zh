

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_89_0.png)

图3.7 示例测试游戏的定制化表格用例规格说明。

## 3.3.3 形式化模型

### 3.3.3.1 XML

XML 是一种形式化的、基于文本的文档标记语言，最初设计用于在万维网上轻松分发信息（W3C 2006）。本工作选择使用 XML 的原因如下：

- *XML 是形式化且简洁的。* XML 规范包含使用扩展巴科斯-瑙尔范式表示的正式文法规范。该文法为 XML 提供了全面的语法，并为所有 XML 文档提供了一种检查其格式是否良好的方法。格式良好的 XML 文档允许符合 XML 文法规范的解析器无误地解析和处理文档中的数据。

- **XML 文档具有人类可读性。** 由于 XML 文档中的标记文本可以自定义，因此 XML 文档可以使用描述性名称编写，使人们能够轻松理解所存储数据的类型。注释也可用于在文档内提供进一步描述，而不会影响文档的语法。这一特性很重要，因为 XML 文档还可以作为转换记录，用于验证模型转换是否成功。

- **编写程序处理 XML 文档是直接了当的。** XML 文档是基于文本的文档，可以根据需要解析以提取数据和进行操作。许多编程语言都提供了用于在 XML 文档中进行数据操作的标准库。

- **XML 支持多种多样的应用程序。** XML 是一种广泛使用的语言，目前正被多个行业的多种应用程序所使用。

### 3.3.3.2 SimSYS XML 游戏脚本

表格化的半形式化符号会被转换为一个单一的 XML 文件，该文件可加载到 SimSYS 游戏引擎中。表3.1展示了该 XML 文件的一部分；其中定义了游戏的 XML 模式。转换是一次一部分地进行的，并使用标签来组织内容。例如，Challenge 中的一个问题与表格规格说明中描述的、软件工程设计中的特定主题和可迁移技能相关（Challenge 中包含哪些类型的知识？）；这些

**表3.1 测试游戏挑战的 XML 部分表示**

```xml
1.1 ...
<!-- Act 1, Scene 1, Screen 1, Challenge 1 -->
<challengeStructure>
    <gameElement xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" xsi:type = "prop">
    <gameElement xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" xsi:type = "IDENTIFIER">
        <id> challenge1 </id>
    <challengeItemList>
    <item>
<!-- What kind of knowledge is in the challenge? -->
<domainKnowledgeList>
    <domainKnowledge>software engineering</domainKnowledge>
    <area>Software Design</area>
    <topic_list>
        <topic>General_Design_Concepts</topic>
        <topic>Context_of_Software_Design</topic>
        <topic>Software_Design_Process</topic>
        <topic>Software_Design_Re-use</topic>
    </topic_list>
</domainKnowledgeList>
<transferableKnowledgeList>
    <transferableKnowledge>analysis
    </transferableKnowledge>
    <transferableKnowledge>critical_thinking
    </transferableKnowledge>
    <transferableKnowledge>problem_solving
    </transferableKnowledge>
</transferableKnowledgeList>
<!-- How is the knowledge being assessed? -->
    <expression>dialog</expression>
    <learningTaxonomyList>
        <learningTaxonomy>knowledge</learningTaxonomy>
        <learningTaxonomy>application
        </learningTaxonomy>
    </learningTaxonomyList>
<!-- Challenge item-->
<!-- The challenge item has a stem, with zero or one
text (description or vignette), zero or more images,
and a question. -->
<!-- stem description-->
<stemDescription>
    <type>
        <typeName>InformationBox</typeName>
        <event>
            <eventName>NONE</eventName>
            <animation>FADEIN</animation>
            <time>QUICK</time>
        </event>
        <color>YELLOW</color>
        <location>UR</location>
    </type>
<!-- -->
<name> Option1 </name>
<location> UUL </location>
<color> Yellow </color>
<text> Strategy Pattern </text>
<!-- Hint -->
<type>
    <typeName> InformationBox</typeName>
    <name> Hint1 </name>
    <eventName> HOVER</eventName>
    <location> UUL </location>
    <color> Yellow </color>
    <text>The Strategy pattern defines a family
          of algorithms, encapsulates each one, and
          makes them interchangeable; algorithms are
          selected at runtime. It is a behavioral
          pattern. </text>
</type>
<!-- Evaluation -->
<evaluation> Incorrect </evaluation>
<!--Reward -->
<reward>NONE</reward>
<type>
    <!-- Feedback -->
    <typeName> MessageBox </typeName>
    <location> UC </location>
    <color> Yellow </color>
    <text>: Sorry - the correct answer is the
          bridge pattern</text>
</type>
</stemOption>
...
</stemOptionList>
</item>
...
</ChallengeItemList>
...
```

这些内容以 XML 表示，使用了两种标签来定义主题列表（`<domainKnowledgeList>`、`<transferableKnowledgeList>`）。接下来的标签定义了问题的评估方法，即“如何评估知识？”具有四个答案选项的问题——评估、提示、奖励和反馈——在 XML 文件中随后出现。尽管文件相当长，但易于阅读；从半形式化表格模型到 XML 的手动映射非常耗时，但并非太难。

## 3.4 结论与未来工作

SimSYS 方法用于工程化严肃教育游戏（SEGs）是一个迭代式的三步方法，它基于模型，并从一开始就将学习目标整合到游戏开发中。该方法从一个非正式叙事（如故事板）开始，随后将其转换为定制化的半形式化 UML 用例模型（包括可视化和表格化规格说明），最后转换为形式化模型。我们的第一个形式化模型使用 XML；该 XML 就是可以在 SimSYS 游戏引擎中加载和测试的游戏规格说明。在将三步方法应用于工程化一组测试游戏时，我们发现它虽然直接，但劳动强度大。特别是，创建形式化 XML 模型需要大量时间；手动测试游戏也非常耗时。

目前正在研究一个智能自动化游戏生成模块，以减轻填充非正式叙事和半形式化模型（模板实例化）的工作量，并自动生成 XML 模型。我们还计划探索将半形式化模型转换为状态图表示，该表示可以利用现有的商业工具支持（例如 IBM 2012）进行加载、动画演示或模拟，从而提供一种补充的验证方法。

我们认识到，该方法的验证目前仅限于我们的初步原型工作（符号测试游戏、软件工程测试游戏）。还需要进行额外的验证，既需要我们继续推进自己的项目，也需要外部教育游戏研究人员和教育工作者参与，以探索诸如该方法扩展到更大游戏和相关游戏集合时的可扩展性等问题。

## 参考文献

- Abran, A.、Moore, J.W. 和 Bourque, P. (2004). *软件工程知识体系指南（SWEBOK）：2004年版.* IEEE 计算机学会，洛斯阿拉米托斯，加利福尼亚州。附录 D.

- Adams, E. (2010). *游戏设计基础.* 第2版. New Riders Publishing，伯克利，加利福尼亚州。

- Anderson, Jr., E.G. 和 Morrice, D.J. (2000). 用于教学服务导向供应链管理的仿真游戏：信息共享是否能帮助管理者做出服务能力决策？*生产与运营管理* 9: 40–55.

- Anderson, L. W.、Krathwohl, D. R. 等（编）(2001). *学习、教学和评估的分类学：布卢姆教育目标分类学的修订版.* Allyn & Bacon（培生教育集团）。波士顿，马萨诸塞州。

- Braithwaite, B. 和 Schreiber, I. (2008). *游戏设计师的挑战.* Charles River Media，波士顿，马萨诸塞州。

- Chen, F. 和 Samoengraja, R. (2000). 静态啤酒游戏. *生产与运营管理* 9: 19–30.

- Cooper, K. 和 Longstreet, C.L. (2012a). 面向严肃教育游戏的模型驱动游戏工程：游戏需求的定制化用例. *IEEE 第17届国际计算机游戏会议论文集*，路易斯维尔，肯塔基州，7月30日至8月1日，第208–212页。

- Cooper, K. 和 Longstreet, C.L. (2012b). 面向 SimSYS 中模型驱动游戏工程：敏捷软件开发过程游戏的需求. 技术报告，联合发布 UTDCS-06-12. 德克萨斯大学达拉斯分校，理查森，德克萨斯州；MU-CII-01-12 马凯特大学，密尔沃基，威斯康星州。3月。

- Cooper, K.、Nass, E. 和 Longstreet, C.L. (2014). 面向严肃教育游戏的模型驱动需求工程：非正式、半正式和形式化模型. *第20届国际需求工程工作会议论文集：软件质量基础*，德国埃森，4月7–10日，第17–22页。

- Crookall, D. 和 Saunders, D.（编）(1989). 走向传播与仿真的整合. 载于 *传播与仿真：从两个领域到一个领域.* Multilingual Matters，克利夫登。

- Dantas, A.R.、Barros, M.O. 和 Werner, C. (2005). 模拟模型在软件项目经理基于游戏培训中的应用. *过程仿真与建模研讨会*，圣路易斯，密苏里州，5月14–15日，第110–116页。

- Dempsey, V.J.、Haynes, L.L.、Lucassen, B.A. 和 Casey, M.S. (2002). 四十个简单的电脑游戏及其对教育工作者的意义. *仿真与游戏* 33(2):157–168.

- Deterding, S.、Dixon, D.、Khaled, R. 和 Nacke, L. (2011). 从游戏设计元素到游戏感：定义“游戏化”. *第15届国际学术 Mindtrek 会议论文集*，芬兰坦佩雷，9月28–30日，第9–15页。

- Gee, J.P. (2003). *电子游戏能教给我们关于学习和读写能力的什么？* Macmillan，纽约。


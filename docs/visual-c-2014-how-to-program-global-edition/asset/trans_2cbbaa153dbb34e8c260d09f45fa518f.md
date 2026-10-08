

# 全球版

# Visual C#

# 程序设计

第六版

Paul Deitel • Harvey Deitel

![](img/57baed2319be0bb1b5f98674846f2711_0_0.png)

![](img/57baed2319be0bb1b5f98674846f2711_0_1.png)

# Visual C#

# 程序设计

![](img/57baed2319be0bb1b5f98674846f2711_1_0.png)

本页特意留白

# Visual C#

# 程序设计

第六版

全球版

# Paul Deitel 
Harvey Deitel

Deitel & Associates, Inc.

![](img/57baed2319be0bb1b5f98674846f2711_3_0.png)

波士顿 哥伦布斯 霍霍肯 印第安波利斯 纽约 旧金山
阿姆斯特丹 开普敦敦 迪拜 伦敦 马德里 米兰 慕尼黑 巴黎 蒙特利尔
多伦多 德里 墨西哥城 圣保罗 悉尼 香港 首尔 台北 东京

副总裁、编辑监：Marcia Horton
策划编辑：Tracy Johnson
编辑助理：Krizty Alura
全球版策划编辑：Sourabh Maheshwari
营销副总裁：Christy Lesko
现场营销经理：Demeterius Hall
营销助理：Joe Bryan
产品管理总：Erik Gregg
程序与项目管理组长：Scott Diansco
程序经理：Carolle Snyder
项目经理：Robert Engelhardt
全球版项目编辑：K.K. Neelakantan
制造：Higher Ed | RR Donnelly: Maura Calidars-Garcia
全球版高级制造控制员：Trudy Kimber
全球版媒体制作：Vikram Kumar
封面设计：Lumina Datamatics
研发经理：Ben Ferrini
库存经理：Ann Lam

书中借自其他来源的致谢和感谢内容出现在本书中第 6 页。
本书的作者和出版商在准备本书方面付出了最大努力。这些努力包括对理论和程序的开发、研究和测试，以确定其有效性。作者和出版商对这些程序或书中包含的文档不提供任何形式的明示或暗示保证。作者和出版商对于提供、执行或使用这些程序而引起的任何附带或间接损害不承担责任。

Pearson Education Limited
Edinburgh Gate
Harlow
nex CM20 2JE

全球范围内 Pearson 及其关联公司网站为：
www.pearonglobaleditions.com
© Pearson Education Limited 2018

Paul Deital 和 Harvey Deitel 已根据 1988 年《版权、设计与专利法案》主张了他们作为本书作者的权利。
内容改编自美国版 *visual C# How to Program*, 第 6 版，ISBN-978-360154-0，Paul Deital 和 Harvey Deitel 编写，Pearson Education 出版 © 2017。

保留所有权利。未经出版商事先书面许可或根据英国版权许可机构有限公司（地址：Sutton House, 60 Girby Street, London EC1 8HT）的限制性复制许可，不得以任何形式或通过任何电子、机械、复印、录音或其他方式复制本出版物的任何部分、存储在检索系统中或传输。
此处使用的商标为其各自所有者的财产。本文中使用任何商标均不授予作者或出版商对此类商标的任何所有权，使用此类商标也不意味着此类所有者对本书的任何关联或认可。

英国图书馆编书目录：可从英国图书馆获取本书的目录
 1 9 8 7 6 5 4 3 2 1
ISBN-10: 1-292-15346-6
ISBN-13: 978-1-292-15346-9
GEX Publishing Services 字体设计
在马来西亚打印并装订

纪念 MIT 电子工程与计算机科学荣誉教授 William Siebert：

你在《信号与系统》讲座中使用可视化技术，启迪了几代工程师、计算机科学家、教育者和作者展示其工作的方式。

Harvey 和 Paul Deitel

# 商标

DEITEL® 和双大指向上虫标志是 Deitel and Associates, Inc. 的注册商标。
Microsoft® Windows® 和 Microsoft Visual C#® 是美国及其他国家 Microsoft 公司的注册商标。本书未获得 Microsoft 公司的赞助、认可或与其存在关联。

UNIX 是 The Open Group 的注册商标。

> 在本书中，使用了许多商标。我们并没有在每个商标名称的出现处都放置商标符号，而是说明我们仅以编辑方式使用这些名称，并为了商标所有者的利益，无侵犯商标的意图。

# 目录

# 前言 23

# 在开始之前 37

# I 计算机、互联网与 Visual C# 简介 41

- 1.1 节：引言 (Introduction) 42
- 1.2 工业与研究中的计算机与互联网 42
- 1.3 硬件与软件 45
- 1.3.1 摩尔定律 45
- 1.3.2 计算机体系 46
- 1.4 数据层次结构 47
- 1.5 机器语言、汇编语言和高级语言 50
- 1.6 对象技术 51
- 1.7 互联网和万维网 53
- 1.8 C# 55
- 1.8.1 面向对象编程 56
- 1.8.2 事件驱动型编程 56
- 1.8.3 可视化编程 56
- 1.8.4 泛型与函数编程 56
- 1.8.5 国际标准 57
- 1.8.6 非 Windows 平台上的 C# 57
- 1.8.7 互联网与 Web 编程 57
- 1.8.8 使用 async 和 await 进行异步编程 57
- 1.8.9 其他关键编程语言 58
- 1.9 .NET 60
- 1.9.1 .NET Framework 60
- 1.9.2 通用语言运行时 (CLR) 60
- 1.9.3 平台独立性 61
- 1.9.4 语言互操作性 61
- 1.10 微软 Windows® 操作系统 61
- 1.11 集成开发环境 (IDE) 61
- 1.12 可视化编程 63

![](img/57baed2319be0bb1b5f98674846f2711_7_0.png)

# 可视化编程

- 2.1 引言 63
- 2.2 Visual Studio 概述 63
- 2.2.1 集成开发环境 63
- 2.2.2 特性 63
- 2.3 帮助 63
- 2.4 解决方案管理器 63
- 2.4.1 工具栏 63
- 2.4.2 属性 63
- 2.5 控件 63
- 2.6 窗口 63
- 2.7 本节总结 63

- 3.1 引言 123
- 3.7 内存概念 25
- 3.8 算术 26
- 3.8.1 直接行形式的算术 27
- 3.8.2 用于分组表达式的括号 27
- 3.8.3 运算符优先级 27
- 3.8.4 C# 算术表达式 28
- 3.8.5 冗余括号 29
- 3.9 决策：等等与关系运算符 29
- 3.10 本节总结 34

# 4 类、对象与字符串 146

- 4.1 引言 147
- 4.2 测试驱动类 148
- 4.2.1 实例化对象——关键字 new 148
- 4.2.2 调用 类的 GetName 方法 149
- 4.2.3 从用户处输入名称 149
- 4.2.4 调用 类的 SetName 方法 150
- 4.3 带有实例变量和 Get 方法的类 150
- 4.3.1 Account 类声明 150
- 4.3.2 关键字 class 与类体 151
- 4.3.3 字符串类型的实例变量 name 151
- 4.3.4 SetName 方法 152
- 4.3.5 GetName 方法 154
- 4.3.6 访问修饰符 private 和 public 154
- 4.3.7 Account UML 类图 155
- 4.4 创建、编译和运行两个类的 Visual 项目 156
- 4.5 使用 Set 和 Get 方法的软件工程 157
- 4.6 具有适当 Set 和 Get 方法的 Account 158
- 4.6.1 使用 Account 属性的 Account 类 158
- 4.6.2 带有实例变量和属性的 Account 类 160
- 4.6.3 带有属性的 Account UML 类图 162
- 4.7 属性 162
- 4.8 Account 类：使用构造函数初始化 163
- 4.8.1 用于自定义对象初始化的 Account 构造函数 163
- 4.8.2 AccountTest 类：在创建时初始化 Account 对象 164


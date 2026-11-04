
- 第 21 章，使用 async 和 await 进行异步编程

说明如何通过编写能够异步处理任务的应用程序来利用多核架构，对于具有长时间运行或计算密集型任务的应用，这可以提高应用性能和 GUI 响应能力。async 修饰符和 await 运算符极大地简化了异步编程，减少了错误，并使您的应用能够利用当今多核计算机、智能手机和平板电脑的处理能力。在本版中，我们添加了一个案例研究，在 GUI 应用中使用任务并行库 (TPL)、async 和 await——我们让 GUI 线程中的进度条持续移动，同时另一个线程中执行冗长且计算密集型的计算。

## 在线附加内容

图 2 展示了随本书出版提供的在线附加内容。

| 在线主题 |
|---|
| XML 与 LINQ to XML |
| Windows Presentation Foundation (WPF) GUI 与 XAML |
| Windows Presentation Foundation (WPF) 图形与多媒体 |
| ATM 案例研究，第 1 部分：使用 UML 进行面向对象设计 |
| ATM 案例研究，第 2 部分：在 C# 中实现面向对象设计 |
| 附录：使用 Visual Studio 调试器 |

图 2 | 《C# 6 for Programmers, 6/e》配套网站上的在线主题。

## 访问附加内容

要访问这些材料——以及在下载、更新和更正内容可用时获取它们——请在 informit.com 注册您的《C# 6 for Programmers, 6/e》副本。注册方法：

- 1. 转到 http://informit.com/register
- 2. 登录或创建账户。
- 3. 输入产品 ISBN——9780134596327——并单击“提交”。

注册图书后，您将在“已注册产品”下找到任何可用的附加内容。以下是对初始在线内容的快速浏览。

## XML 与 LINQ to XML

可扩展标记语言（XML）在第 21 章中作了简要介绍，它广泛存在于软件开发行业、电子商务以及整个 .NET 平台中。要理解 XAML——一种 Microsoft XML 词汇表，用于描述 Windows Presentation Foundation (WPF) 应用、通用 Windows 平台 (UWP) 应用和 Windows 10 Mobile 的图形用户界面、图形与多媒体——需要先了解 XML

## 适用于桌面和移动应用的通用 Windows 平台 (UWP)

通用 Windows 平台 (UWP) 旨在为所有 Windows 设备提供共同的平台和用户体验，包括个人计算机、智能手机、平板电脑、Xbox，甚至 Microsoft 新的 HoloLens 虚拟现实和增强现实全息头戴式设备——所有这些设备都使用几乎相同的代码。²

## REST Web 服务

Web 服务使您能够以将 Web 转变为可重用服务库的方式打包应用功能。我们在第 21 章中使用了一个基于 Flickr REST 的 Web 服务。

## Microsoft Azure™ 云计算

Microsoft Azure 的 Web 服务使您能够在“云”中开发、管理和分发应用。

## 关于表述方式的说明

《C# 6 for Programmers, 6/e》包含丰富的示例集。我们专注于构建精心设计、高性能的软件，并强调程序的清晰性。

*语法着色。* 为了提高可读性，我们对代码进行语法着色，类似于 Visual Studio 为代码着色的方式。我们的语法着色约定如下：

```text
comments appear like this
keywords appear like this
constants and literal values appear like this
all other code appears in black
```

*代码突出显示。* 我们通过将关键代码段置于灰色矩形中来强调它们。

*使用字体强调。* 我们将关键术语以及索引中每次定义出现处的页码引用放在**粗体**文本中，以便于参考。我们以**粗体 Helvetica** 字体显示屏幕组件（例如，文件菜单），并以 Lucida 字体显示 Visual C# 程序文本（例如，int count = 5;）。我们使用*斜体*表示强调。

*目标。* 章目标预览本章涵盖的主题。

*编程提示。* 我们包含专注于程序开发重要方面的编程提示。这些提示和实践代表了我们从总计九十年的编程、专业培训和大学教学经验中汲取的精华。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_28_0.png)

## 良好的编程实践

> 良好的编程实践提醒您注意有助于编写更清晰、更易理解且更易维护的程序的技巧。

2. 截至 2016 年夏季，Windows Forms、WPF 和 UWP 应用均可通过 Windows 商店发布分发，无论免费还是收费。有关更多信息，请参见 http://bit.ly/DesktopToUWP。

- **常见编程错误**
  *指出这些常见编程错误可降低您犯这些错误的可能性。*
- **错误预防提示**
  *这些提示包含有关暴露和消除程序中缺陷的建议；许多提示描述了 Visual C# 中防止缺陷进入程序的方面。*
- **性能提示**
  *这些提示强调使程序运行更快或最大限度减少程序占用内存量的机会。*
- **软件工程观察**
  *软件工程观察强调影响软件系统构造（尤其是大型系统）的体系结构和设计问题。*
- **外观与感觉观察**
  *这些观察帮助您设计符合行业规范、有吸引力且用户友好的图形用户界面。*

*索引。* 我们包含了一个详尽的索引供参考。索引中关键术语的定义出现处以粗体页码突出显示。

### 获取《C# 6 for Programmers, 6/e》中使用的软件

我们在《C# 6 for Programmers, 6/e》中使用 Microsoft 免费的 Visual Studio 2015 Community 版编写了本书的代码示例。有关下载和安装说明，请参见本前言之后的“开始之前”部分。

### Microsoft DreamSpark™

Microsoft 通过一项名为 DreamSpark (http://www.dreamspark.com) 的计划，向学生免费提供许多专业开发人员工具。如果您是在大学课程中使用本书的学生，请查看网站，了解验证您身份的详细信息，以便利用该计划。

### 致谢

我们要感谢 Deitel & Associates, Inc. 的 Barbara Deitel。她悉心研究了 Visual C#、Visual Studio、.NET 和其他关键组件的最新版本。我们还要感谢哈丁大学计算机科学副教授 Frank McCown 博士，他建议在第 21 章中包含一个使用 ProgressBar 以及 async 和 await 的示例——因此我们将我们另一本书 *Java for Programmers, 3/e* 中的一个类似示例移植到了 C#。

我们很幸运能与 Pearson 敬业的出版专业团队合作。我们感谢我们的朋友和职业同事、Pearson IT Professional Group 主编 Mark L. Taub 的非凡努力和指导。

Kristy Alaura 在招募本书审阅者和管理审阅流程方面做了出色的工作。Julie Nahil 在使本书得以出版方面做得非常出色，Chuti Prasertsith 在封面设计上施展了他的魔法。

### 审阅者

本书由行业 C# 专家和教授 C# 课程的学者仔细审阅。他们为改进表述提供了无数建议。书中任何遗留的缺陷均由我们自己负责。

*第六版审阅者：* Lucian Wischik（Microsoft Visual C# 团队）、Octavio Hernandez（Microsoft 认证解决方案开发人员，Advanced Bancios 首席软件工程师）、José Antonio González Seco（西班牙安达卢西亚议会）、Bradley Sward（杜佩奇学院）和 Qian Chen（萨凡纳州立大学工程技术系：计算机科学技术项目）。

*其他近期版本审阅者：* Douglas B. Bock（MCSD.NET，南伊利诺伊大学爱德华兹维尔分校）、Dan Crevier（Microsoft）、Shay Friedman（Microsoft Visual C# MVP）、Amit K. Ghosh（得克萨斯大学埃尔帕索分校）、Marcelo Guerra Hahn（Microsoft）、Kim Hamilton（Microsoft 软件设计工程师，*Learning UML 2.0* 合著者）、Huanhui Hu（Microsoft Corporation）、Stephen Hustedde（South Mountain College）、James Edward Keysor（佛罗里达理工学院）、Narges Kasiri（俄克拉何马州立大学）、Helena Kotas（Microsoft）、Charles Liu（得克萨斯大学圣安东尼奥分校）、Chris Lovett（Microsoft 软件架构师）、Bashar Lulu（NIETA 阿拉伯湾地区负责人）、John McIlhinney（Spatial Intelligence；Microsoft MVP Visual Developer，Visual Basic）、Ged Mead（Microsoft Visual Basic MVP，DevCity.net）、Anand Mukundan（Polaris Software Lab Ltd. 架构师）、Hamid R. Nemati 博士（北卡罗来纳大学格林斯伯勒分校）、Timothy Ng（Microsoft）、Akira Onishi（Microsoft）、Jeffrey P. Scott（黑鹰技术学院）、Joe Stagner（Microsoft 开发人员工具与平台高级项目经理）、Erick Thompson（Microsoft）、Jesús Ubaldo Quevedo-Torrero（威斯康星大学帕克赛德分校计算机科学系）、Shawn Weisfeld（Microsoft MVP，UserGroup.tv 总裁兼创始人）以及 Zijiang Yang（西密歇根大学）。

在阅读本书时，我们真诚地感谢您的评论、批评、更正和改进建议。请将所有通信寄至：

deitel@deitel.com

我们将及时回复。撰写 *C# 6 for Programmers, 6/e* 很有趣——希望您喜欢阅读！

Paul Deitel  
Harvey Deitel

## 关于作者

Paul Deitel 是 Deitel & Associates, Inc. 的首席执行官兼首席技术官，在计算领域拥有超过 35 年的经验。他毕业于麻省理工学院 (MIT)，在那里学习信息技术。通过 Deitel & Associates, Inc.，他在全球范围内为客户提供了数百门企业编程培训课程，客户包括 Cisco、IBM、Boeing、Siemens、Sun Microsystems（现为 Oracle）、Dell、Fidelity、位于肯尼迪航天中心（Kennedy Space Cen-）的 NASA



Dr. Harvey M. Deitel，Deitel & Associates, Inc. 的董事长兼首席战略官，在计算机领域拥有 47 年的学术和行业经验。Deitel 博士在麻省理工学院获得理学学士和理学硕士学位，并在波士顿大学获得博士学位。他拥有 20 年的大学教学经验，包括获得终身教职并担任波士顿学院计算机科学系主任，随后与他的儿子 Paul J. Deitel 一起创立了 Deitel & Associates, Inc.。他和 Paul 是数十本图书和多媒体产品的合著者，并且还在撰写更多作品。Deitel 的教材获得了国际认可，已翻译成日语、德语、俄语、西班牙语、繁体中文、简体中文、韩语、法语、波兰语、意大利语、葡萄牙语、希腊语、乌尔都语和土耳其语出版。Deitel 博士为众多大型企业、学术机构、政府组织和军队举办了数百场专业研讨会。

## 关于 Deitel & Associates, Inc.

Deitel & Associates, Inc. 是一家国际公认的企业培训和内容创作机构，专注于计算机编程语言、互联网和网络软件技术、面向对象技术教育以及通过其互联网业务倡议进行的互联网业务开发。该公司提供针对主要编程语言和平台的讲师主导的专业课程，如 C++、Java、C、C#、Visual C++、Visual Basic、XML、Perl、Python、面向对象技术以及互联网和网络编程。Deitel & Associates, Inc. 的创始人是 Paul J. Deitel 和 Harvey M. Deitel 博士。该公司的客户包括世界上许多最大的公司、政府机构、军队分支机构和学术机构。通过与 Prentice Hall 长达 32 年的出版合作，Deitel & Associates, Inc. 出版领先的编程专业书籍、教科书、LiveLessons 视频课程、交互式多媒体 Cyber Classrooms、基于网络的培训课程以及适用于流行课程管理系统的电子内容。Deitel & Associates, Inc. 和作者可通过电子邮件联系：

```
deitel@deitel.com
```

要了解更多关于 Deitel & Associates, Inc.、其出版物以及其 Dive-Into® 系列企业培训课程的信息，该课程在全球客户现场提供，请访问：

```
www.deitel.com
```

并在以下地址订阅免费的 Deitel® Buzz Online 电子邮件通讯：

```
www.deitel.com/newsletter/subscribe.html
```

请查看不断增长的在线 Deitel 资源中心列表：

```
www.deitel.com/resourcecenters.html
```

希望购买 Deitel 出版物的个人可以通过以下方式进行：

```
www.deitel.com/books/index.html
```

企业、政府、军队和学术机构的大批量订单应直接向 Prentice Hall 下单。欲了解更多信息，请访问

```
www.prenhall.com/mischtm/support.html#order
```

## 开始之前

请遵循本节中的说明，在开始使用本书之前下载本书的示例。

## 下载 C++ for Programmers 示例代码

*C++ for Programmers* 的示例可以作为 ZIP 归档文件从 www.deitel.com/books/cppfp/ 下载。注册并登录后，点击“Download Code Examples and Other Premium Content for Registered Users”下的示例链接。将 ZIP 文件保存到您能记住的位置。使用 ZIP 文件提取程序（如 WinZip，www.winzip.com）将示例文件提取到您的硬盘上。

## 安装/选择编译器

如果您的计算机运行的是 Windows XP 或 Windows Vista，您可以安装 Visual C++ Express（www.microsoft.com/express/vc/）来编辑、编译、执行、调试和修改您的程序。按照屏幕上的说明安装 Visual C++ Express。我们建议您使用默认安装选项并选择同时安装文档。

如果您的计算机使用 Linux 或 Mac OS X，则您可能已经安装了 GNU C++ 命令行编译器。还有许多其他 C++ 编译器和 IDE。我们在 C++ 资源中心提供了指向适用于 Windows、Linux 和 Mac OS X 平台的各种免费 C++ 开发工具的链接，网址为

www.deitel.com/cplusplus/

该资源中心还链接到在线教程，可帮助您开始使用各种 C++ 开发工具。

您现在准备好开始使用 *C++ for Programmers* 了。我们希望您喜欢这本书！如果您有任何问题，请随时发送电子邮件至 deitel@deitel.com。我们会及时回复。

## 引言

> 语言的主要优点是清晰。
> —Galen

> 我们的人生被琐事消磨殆尽。……简化，简化。
> —Henry David Thoreau

> 他有一种美妙的天赋，能够紧凑地打包思想，使其便携。
> —Thomas B. Macaulay

> 人仍然是最神奇的计算机。
> —John F. Kennedy

## OBJECTIVES

在本章中你将学习：

- 面向对象技术概念，如类、对象、属性、行为、封装和继承。
- 典型的 C++ 程序开发环境。
- 行业标准面向对象系统建模语言 UML 的历史。
- 互联网和万维网的历史，以及 Web 2.0 现象。
- 在两个流行的 C++ 环境中测试驱动 C++ 应用程序——在 Linux 上运行的 GNU C++ 和在 Windows® 上运行的 Microsoft 的 Visual C++®。
- 什么是开源，以及两个流行的 C++ 开源库——用于图形和游戏编程的 Ogre，以及用于广泛增强 C++ 标准库功能的 Boost。

## 1.1 引言

### 大纲

1.1 引言  
1.2 C 和 C++ 的历史  
1.3 C++ 标准库  
1.4 关键软件趋势：面向对象技术  
1.5 典型的 C++ 开发环境  
1.6 关于 C++ 和 C++ *for Programmers* 的说明  
1.7 测试驱动 C++ 应用程序  
1.8 软件技术  
1.9 C++ 的未来：开源 Boost 库、TR1 和 C++0x  
1.10 软件工程案例研究：面向对象技术和 UML 简介  
1.11 总结  
1.12 网络资源

欢迎来到 C++！我们付出了艰苦努力，创造了我们希望您会觉得信息丰富、有趣且具有挑战性的学习体验。C++ 是一种功能强大的计算机编程语言，适合有经验的程序员用于构建实质性的信息系统。*C++ for Programmers* 是这些受众的有效学习工具。

本书强调通过经过验证的面向对象编程技术实现程序清晰度。这是一本“早期类和对象”书籍。我们在完整的工作 C++ 程序的上下文中教授 C++ 特性，并展示在计算机上运行这些程序时产生的输出——我们称之为 *live-code approach*。您可以从 www.deitel.com/books/cppfp/ 下载示例程序。

早期章节介绍了 C++ 的基础知识，为后续章节中对 C++ 的深入处理奠定了坚实的基础。有经验的程序员往往快速阅读早期章节，然后发现本书其余部分对 C++ 的处理严谨且富有挑战性。

C++ 是当今最流行的软件开发语言之一。本书讨论的是在美国通过 *American National Standards Institute (ANSI)* 和在全球通过 *International Organization for Standardization (ISO)* 标准化版本的 C++。

要及时了解 Deitel & Associates 的 C++ 发展动态，请注册我们的免费电子邮件通讯 *Deitel® Buzz Online*，网址为

```
www.deitel.com/newsletter/subscribe.html
```

请查看我们不断增长的 C++ 及相关资源中心列表，网址为

```
www.deitel.com/ResourceCenters.html
```

在阅读本书时对您有价值的资源中心包括 C++、C++ 游戏编程、C++ Boost 库、代码搜索引擎和代码站点、计算机游戏编程、编程项目、Eclipse、Linux、开源和


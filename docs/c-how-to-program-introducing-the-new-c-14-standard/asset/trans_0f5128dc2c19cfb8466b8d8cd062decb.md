
戴特尔父子的出版物赢得了国际认可，已被翻译成日语、德语、俄语、西班牙语、法语、波兰语、意大利语、简体中文、繁体中文、韩语、葡萄牙语、希腊语、乌尔都语和土耳其语出版。戴特尔博士已为学术机构、企业、政府和军方客户讲授了数百门编程课程。

## 关于 Deitel & Associates, Inc.

Deitel & Associates, Inc. 由 Paul Deitel 和 Harvey Deitel 创立，是一家国际公认的写作和企业培训机构，专长于计算机编程语言、对象技术、互联网与 Web 软件技术，以及 Android 和 iOS 应用开发。该公司的客户包括学术机构、许多全球最大的公司、政府机构和军方分支。公司提供由讲师主导的培训课程，在全世界客户现场讲授主要编程语言和平台，包括 C++、C、Java™、Android 应用开发、iOS 应用开发、Swift™、Visual C#®、Visual Basic®、互联网与 Web 编程，以及不断增加的额外编程和软件开发课程。

通过与 Prentice Hall/Pearson 长达 40 年的出版合作关系，Deitel & Associates, Inc. 出版前沿的编程大学教材、专业书籍和 *LiveLessons* 视频课程。可通过以下方式联系 Deitel & Associates, Inc. 和作者：

deitel@deitel.com

如需了解 Deitel 企业培训课程的更多信息，请访问：

http://www.deitel.com/training

如需申请在贵组织进行全球现场、讲师主导培训的方案，请发送电子邮件至 deitel@deitel.com。

希望购买 Deitel 图书的个人可通过以下方式购买：

http://bit.ly/DeitelOnAmazon

希望购买 Deitel *LiveLessons* 视频培训的个人可访问：

http://bit.ly/DeitelOnInformIT

所有 Deitel 图书和 *LiveLessons* 视频也以电子形式提供给 Safari Books Online 订阅者，网址为：

http://SafariBooksOnline.com

您可以在以下网址获得免费的 10 天 Safari Books Online 试用：

https://www.safaribooksonline.com/register/

公司、政府、军方和学术机构的大宗订单应直接向 Pearson 下订。更多信息请访问：

http://www.informit.com/store/sales.aspx

## 开始之前

本节包含在使用本书之前应查看的信息，以及确保您的计算机已正确设置以编译示例程序的说明。

## 字体和命名约定

我们使用字体来区分各种功能，例如菜单名称、菜单项，以及 IDE（集成开发环境）中出现的其他元素，例如 Microsoft 的 Visual Studio。我们的约定是：用无衬线粗体 **Helvetica** 字体强调 IDE 功能（例如 **文件** 菜单），并用无衬线 `Lucida` 字体强调程序文本（例如 `bool x = true;`）。

## 获取 C++ *程序设计教程（第 10 版）* 中使用的软件

在阅读本书之前，您应下载并安装 C++ 编译器。我们使用以下免费 C++ 开发工具编写了 C++ *程序设计教程（第 10 版）* 的代码示例：

- 微软免费的 Visual Studio Community 2015 版，其中包括 Visual C++ 编译器和其它微软开发工具。它运行于 Windows，可从以下地址下载：

  https://www.visualstudio.com/products/visual-studio-community-vs

- GNU 免费的 GNU C++ 5.2.1 编译器。GNU C++ 已安装在大多数 Linux 系统上，也可安装在 Mac OS X 和 Windows 系统上。Linux 有许多版本，称为 Linux 发行版，它们使用不同技术执行软件升级。请查阅您所用发行版的在线文档，了解如何将 GNU C++ 升级到最新版本。GNU C++ 可从以下地址获取：

  http://gcc.gnu.org/install/binaries.html

- 苹果免费的 Xcode，OS X 用户可从 Mac App Store 下载——单击 Mac 屏幕底部 Dock 中的应用图标，然后在应用商店中搜索 Xcode。

我们还提供每种 C++ 工具入门视频的链接，地址为：

## 获取代码示例

*C++ 程序设计教程（第 10 版）* 的示例可从以下地址下载：

http://www.deitel.com/books/cpphtp10

单击 **下载代码示例** 链接，将 ZIP 归档文件下载到您的计算机。请记下保存文件的位置——大多数浏览器会将文件保存到您用户账户的 `Downloads` 文件夹中。

在本书中，要求您在计算机上访问示例代码的步骤假定您已从 ZIP 文件中提取示例，并将它们放在 Windows 上的 `C:\examples` 中，或其他平台上的用户账户 `Documents` 目录中。您可以将它们解压到任何喜欢的位置，但如果选择其他位置，则需要相应更新我们的步骤。

## 创建项目

在 **1.10 节** 中，我们演示如何使用以下工具编译和运行程序：

- Windows 上的 Microsoft Visual Studio Community 2015 版（**1.10.1 节**）
- Linux 上的 GNU C++ 5.2.1（**1.10.2 节**）
- OS X 上的 Apple Xcode（**1.10.3 节**）

对于 GNU C++ 和 Xcode，必须使用 C++14 编译程序。在 GNU C++ 中，编译代码时请包含选项 `-std=c++14`，如下所示：

```bash
g++ -std=c++14 YourFileName.cpp
```

对于 Xcode，在按照 **1.10.3 节** 的步骤创建项目后：

- 选择 Xcode **项目** 导航器顶部的根节点。
- 单击 **编辑器** 区域中的 **构建设置** 选项卡。
- 向下滚动到 **Apple LLVM 7.0 - 语言 - C++** 部分。
- 对于 **C++ 语言方言** 选项，选择 **C++14 [-std=c++14]**。

## 解答您的 C++ 问题

在阅读本书时，如果您有疑问，可以很容易地通过以下方式联系我们：

deitel@deitel.com

我们会及时回复。

此外，网络上充满编程信息。对于非程序员和程序员来说，一个非常宝贵的资源是以下网站：

http://stackoverflow.com

在该网站上，您可以：

- 搜索大多数常见编程问题的答案。
- 搜索错误消息，了解其原因。
- 提出编程问题，获得全世界程序员的解答。
- 获得关于编程总体上的宝贵见解。

## 在线 C++ 文档

有关 C++ 标准库的文档，请访问：

http://cppreference.com

并务必查看以下网址的 C++ 常见问题解答：

https://isocpp.org/faq

## 1 计算机与 C++ 简介

## 目标

在本章中，您将学习：

- 计算机领域令人兴奋的最新发展。
- 计算机硬件、软件和网络基础。
- 数据层次结构。
- 不同类型的编程语言。
- 基本的对象技术概念。
- 互联网和万维网的一些基础知识。
- 典型的 C++ 程序开发环境。
- 试运行一个 C++ 应用程序。
- 一些关键的最新软件技术。
- 计算机如何帮助您有所作为。

## 大纲

- 1. **1.1 简介**
- 2. **1.2 工业与研究中的计算机和互联网**
- 3. **1.3 硬件与软件**
  - A. **1.3.1 摩尔定律**
  - B. **1.3.2 计算机组成**
- 4. **1.4 数据层次结构**
- 5. **1.5 机器语言、汇编语言和高级语言**
- 6. **1.6 C 与 C++**
- 7. **1.7 编程语言**
- 8. **1.8 对象技术简介**
- 9. **1.9 典型的 C++ 开发环境**
- 10. **1.10 试运行一个 C++ 应用程序**
  - A. **1.10.1 在 Windows 的 Visual Studio 2015 中编译和运行应用程序**
  - B. **1.10.2 在 Linux 上使用 GNU C++ 编译和运行**
  - C. **1.10.3 在 Mac OS X 上使用 Xcode 编译和运行**
- 11. **1.11 操作系统**
  - A. **1.11.1 Windows——专有操作系统**
  - B. **1.11.2 Linux——开源操作系统**

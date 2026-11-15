# EMBOSS 开发者指南：生物信息学编程











Peter M. Rice 是欧洲生物信息学研究所（EMBL-EBI，英国 Hinxton）的小组负责人，该中心是生物信息学研究与服务机构，也是欧洲分子生物学实验室（EMBL）的一部分。Peter 于 1996 年在桑格中心（英国 Hinxton）任职期间发起了 EMBOSS 项目，与 Alan Bleasby（SEQNET，Daresbury）合作，并与 Thure Etzold（EMBL-EBI）协作。

Alan J. Bleasby 是 EMBL-EBI 的高级科学官员。他在达尔斯伯里实验室（英国 Warrington）开发了早期的 EMBOSS 编程库（AJAX），并负责 SEQNET 英国国家生物信息学服务。他目前全职从事 EMBOSS 工作。

Jon C. Ison 自 2000 年起一直是 EMBOSS 的开发者。他也位于 EMBL-EBI，并与 Peter 和 Alan 一起协调 EMBOSS 工作。他目前正在从事本体学、数据集成和应用程序开发方面的工作。

EMBOSS 团队感谢以下机构对本项目的慷慨支持，包括 Wellcome Trust、医学研究委员会、生物技术与生物科学研究委员会（BBSRC）和 EMBL-EBI。

由 Internet Archive 数字化
于 2023 年
由 Kahle/Austin Foundation 提供资助


## 致谢

### EMBOSS 致谢

EMBOSS 开发者谨感谢为本项目提供资助的资助机构以及众多做出贡献的人员。如果您未出现在下列名单中，请接受我们的歉意并告知我们。特别感谢多年来提出宝贵建议、批评和赞扬的所有用户。

### 资助机构

- 生物技术与生物科学研究委员会 (BBSRC)
- 欧洲分子生物学实验室 – 欧洲生物信息学研究所 (EMBL-EBI)
- 医学研究委员会 (MRC)
- 威康信托基金

### 贡献者

彼得·赖斯和艾伦·布莱兹比是该项目的发起人。彼得最初是项目协调员，在为 Lion Bioscience 和桑格中心工作后，转到 EMBL-EBI。他领导的 EBI 赖斯小组承担了 EMBOSS 项目。

艾伦·布莱兹比在达尔斯伯里实验室期间编写了最初的 AJAX 库，现与彼得·赖斯共同协调该项目。在 MRC 人类基因组计划资源中心工作后，艾伦于 2005 年转到 EBI 全职从事 EMBOSS 工作。

乔恩·伊森自 2000 年以来为项目的所有领域做出了贡献，现全职与彼得和艾伦合作协调项目。

彼得、乔恩和艾伦谨感谢：

- 迈克尔·舒斯特，感谢其为与 ENSEMBL 数据库接口贡献代码。
- 马赫穆特·乌卢达格，感谢其各项贡献。
- 加里·威廉姆斯，感谢其编写应用程序和文档、提供用户支持以及许多其他贡献。
- 蒂姆·卡弗，感谢其众多贡献，包括 Jemboss 的设计、实现和支持。
- 丽莎·穆兰，感谢其在 EMBOSS 会议上的诸多贡献。她编写了培训材料，组织了培训课程并进行了演讲。
- 伊安·朗登，感谢其在获得威康信托基金资助全职工作期间，对 EMBOSS 各个方面所做的工作，特别是图形的集成。
- 大卫·马丁，感谢其开发新应用程序、进行错误测试和编写文档。
- 盖伊·博图，感谢其编写 wEMBOSS 文档以及许多有价值的错误报告和建议。
- 尼古拉·若尔夫，感谢其许多错误报告和建议。
- 达米安·康塞尔，感谢其在 EMBOSS 会议上的贡献以及文档工作。
- 休·摩根，感谢其在图形库方面的工作。
- 克劳德·比兹利，感谢其在 CORBA 集成方面的工作。
- 兰吉瓦·拉纳辛赫、瓦卡斯·阿万和迈克尔·赫利，感谢其在蛋白质结构应用方面的工作。
- 比贾亚·贾萨尔，感谢其在 EMBOSS 会议上的贡献以及 SRS 接口支持。
- 瓦尔·柯温，感谢其贡献应用程序、文档并开发培训材料。
- 理查德·布拉斯克维奇，感谢其在 GFF 和窗口方面的工作。
- 凯瑟琳·勒通达尔，感谢其与 PISE 的集成。
- 凯瑟琳·比尔，感谢其与 SPIN 的集成。
- 托马斯·洛朗，感谢其在 SRS 接口方面的工作。
- 罗德里戈·洛佩兹，感谢其在 CpG 岛应用方面的工作以及一般性鼓励。
- 西妮阿德·奥利里，感谢其贡献应用程序。
- 东·德·博尔，感谢其编写 ACD 文档
- 马克·法勒，感谢其在 EMMA 和其他项目方面的工作。
- 安德烈·布拉维耶，感谢其最初的 Windows 移植工作。
- 马丁·萨拉丘，已不幸去世，和马克·科莱，感谢其为 wEMBOSS 做出的贡献。
- 卢克·麦卡锡，感谢其开发 EMBOSS Explorer。
- 彼得·科克，感谢其对 FASTQ 和其他序列格式进行验证。
- 大卫·鲍尔、图雷·埃茨尔德、马丁·森格、汤姆·奥因、唐·吉尔伯特、威尔·吉尔伯特、罗杰·斯塔登、比尔·皮尔森、西蒙·凯利、伊万·伯尼、苏珊·简·约翰斯 以及我们可能遗漏的任何人，感谢他们的贡献。
- 珍妮特·桑顿、格雷厄姆·卡梅伦、迈克尔·阿什伯恩、马丁·毕肖普和理查德·杜宾，感谢他们的支持。

### EMBOSS 开发者指南致谢

作者谨感谢以下个人为 EMBOSS 文档或 EMBOSS 开发者指南的制作做出的贡献：

- 剑桥大学出版社的卡特里娜·哈利迪，感谢其鼓励和建议。
- 东·德·博尔，感谢其过去对 ACD 文档的贡献。

## 前言

## EMBOSS 简介

欧洲分子生物学开放软件套件 (EMBOSS) 是一套高质量、文档齐全的开源软件工具包，用于分子生物学。它包含 200 多个用于分子序列分析及其他生物信息学常见任务的应用程序。它在一致且功能强大的命令行界面下，将核心应用程序与一系列流行的第三方软件包集成在一起。该软件具有许多有用功能；例如，它可以自动处理各种格式的数据，并允许从网络透明地检索序列数据。

EMBOSS 包含广泛的 C 编程库，具有简洁且一致的 API。它具有许多有用的内置功能，例如命令行处理和常见文件格式，使其成为开发和发布生物信息学程序的强大且便捷的平台。秉持开源精神，EMBOSS 对所有人免费，代码根据 GNU 通用公共许可证 (GPL 和 LGPL) 授权供所有人使用。没有任何个人或机构“拥有”该代码，今后也不会。根据许可证条款，它可以通过互联网下载、复制、定制和传递，只要这些相同的自由为他人保留。我们强烈鼓励贡献！

EMBOSS 已广泛应用。它在要求苛刻的生产环境中使用，反映了代码库的成熟度。每年发布一个主要的新稳定版本。对于需要最新代码的用户，当前源代码树可以通过 CVS 下载。已有数千次下载，包括全球管理员进行的全站安装，服务于数百甚至数千名用户。EMBOSS 有许多可用的接口，包括易于使用的 Web 界面和强大的工作流软件，使应用程序可以组合成分析流水线。

## 开发 EMBOSS

在 EMBOSS 下进行软件开发和维护变得简单。EMBOSS 具有强大的内置功能，任何应用程序都可以几乎无需额外编码即可使用。这包括对许多简单和复杂（生物）数据类型、常见文件格式和简单数据库配置的支持。已建立通用机制，用于序列和序列特征规范以及控制程序行为的限定符。根据您的特定要求，这可能会为您节省大量精力。此外，例如，当新的输入和输出数据格式添加到 EMBOSS 时，您的应用程序将自动能够使用它们；无需更改应用程序代码。针对质量保证测试、安装、维护和支持等关键方面，已建立明确定义的流程。一般方面由 EMBOSS 开发者处理，留给您支持特定于您自己软件的部分。

您的应用程序将使用 EMBOSS 命令行，该命令行在各应用程序中保持一致。AJAX 命令定义 (ACD) 文件定义了命令行界面以及所有应用程序参数的数据类型和允许值。命令行和用户输入的处理与验证在启动时自动处理，在 before the


应用程序正式启动。例如，生成合理的提示并针对超出范围的值重新提示。代码的用户界面处理方面与核心功能有清晰的分离：使用单个函数调用来处理命令行和 ACD 文件。ACD 语法还使得在 EMBOSS 下封装第三方应用程序变得简单。

EMBOSS 包含广泛的 C 编程库（AJAX 和 NUCLEUS），分别用于低级和高级任务。这些库提供了一个强大的工具包，用于开发新的生物信息学应用程序和工作流，并扩展核心库功能。应用程序员接口（API）全面且一致。开发人员无需了解内部实现即可使用这些库：如何调用函数、所需的输入数据和输出都有明确的文档。所有代码均为 ANSI 标准 C，并且有定义的编码和文档标准。

EMBOSS 下的内存管理大大简化。ACD 文件中定义的所有数据的内存都会自动分配。字符串、序列和数组等编程对象的动态内存管理也会自动处理，为应用程序员节省了大量精力。

EMBOSS 源代码文档完善，并作为 SRS 数据库编入索引，以便轻松搜索和导航。文档从代码中的结构化注释自动生成，这些注释经过验证以确保正确性和一致性，例如，函数和函数参数具有标准化名称。EMBOSS 开发者指南包含大多数库文件的编程指南和示例代码，说明其用途。用于讨论开发和报告错误的邮件列表响应时间良好。

## AJAX

AJAX 是所有 EMBOSS 应用程序使用的核心低级库，提供了一套全面的基本对象和函数。它包括字符串、序列、特征、结构、文件句柄、表、列表、树、动态数组等的标准数据结构。包含用于字符串处理、模式匹配、排序、迭代和非常快速的数据库索引的算法，以及更多内容。AJAX 根据 GNU LGPL 许可。

## NUCLEUS

NUCLEUS 包含高级代码和算法，主要用于常见的分子序列分析任务。包含用于序列比较、翻译、密码子用法和注释的函数。与 AJAX 库和 EMBOSS 应用程序相比，NUCLEUS 的某些部分开发或文档不够完善。在未来的代码重构中，库将被整合，文档将得到改进。NUCLEUS 与 AJAX 一样，根据 GNU LGPL 许可。

## 关于作者

### Peter Rice

Peter Rice 是欧洲生物信息学研究所（EMBL-EBI，英国欣克斯顿）的小组负责人，该中心是生物信息学研究和服务中心，也是欧洲分子生物学实验室（EMBL）的一部分。他的小组通过应用程序开发和参与标准制定，调查并就 EMBL-EBI 的 e-Science 和网格技术需求提供建议。他的小组还托管 EMBOSS 项目。Peter 于 1996 年在桑格中心（英国欣克斯顿）任职期间发起了 EMBOSS，与 Alan Bleasby（SEQNET，达尔斯伯里）合作，并与 Thure Etzold（EMBL-EBI）协作。他于 2000 年离开桑格中心去 LION Bioscience 工作，并于 2003 年加入 EMBL-EBI。

### Alan Bleasby

Alan Bleasby 是 EMBL-EBI 的高级科学官员。Alan 在达尔斯伯里实验室（英国沃灵顿）开发了早期的 EMBOSS 编程库（AJAX），在那里他负责 SEQNET 英国国家生物信息学服务。当 SEQNET 和 HGMP-RC 服务于 1999 年初合并时，他转至英国医学研究委员会人类基因组计划资源中心（UK HGMP-RC），在那里他是蛋白质组学应用小组的小组负责人并协调 EMBOSS。当 HGMP-RC 于 2005 年关闭时，他转至 EBI 全职从事 EMBOSS 工作。

### Jon Ison

Jon Ison 是 EMBL-EBI 的高级科学官员。他于 1999 年从利兹大学转至英国 HGMP-RC，从事生物序列和结构分析协作计算项目（CCP11）的工作，随后于 2000 年担任蛋白质组学应用小组的软件专家。自那时起，他一直是 EMBOSS 的主要贡献者和开发人员，并于 2005 年与 Alan 一起转至 EMBL-EBI，在那里他与 Peter 和 Alan 一起协调该项目。

## 如何引用 EMBOSS

在适当的地方请引用 EMBOSS。

- Rice P., Bleasby A. 和 Ison J. *EMBOSS 用户指南*. 剑桥大学出版社。
- Ison J., Rice P. 和 Bleasby A. *EMBOSS 开发者指南*. 剑桥大学出版社。
- Bleasby A., Ison J. 和 Rice P. *EMBOSS 管理员指南*. 剑桥大学出版社。
- Rice P., Longden I. 和 Bleasby A. EMBOSS：欧洲分子生物学开放软件套件。*遗传学趋势* 2000 **16**(6):276–277。
- EMBOSS 网站。http://emboss.open-bio.org/

## 约定

### EMBOSS 指南约定

#### 命令行会话和命令

命令行会话或任何其他屏幕输出的示例如下所示：

```
% secret
Reads and writes (returns) sequences
Input (gapped) sequence(s) : embl:x65923
output sequence(s) [x65923.fasta] : stdout
>X65923 X65923.1 H.sapiens fau mRNA
ttccttttctcgactccatcttcgcggtagctgggaccgccgttcagtcgccaatatgc
agtctttgtccgcgcccaggagctacacaccttcgaggtgaccggccaggaaacggtcg
cccagatcagggctcatgtagcctcactggaggcattggccccggaagatcaagtcgtgc
tcctggcaggcgcgccctggaggatgaggccactctgggccagtgcggggtggaggccc
tgactaccctggaagtgcaggccgcatgcttggaggtaaagttcatggttccctggccc
gtgctggaaaagtgagaggtcagactctaaggtggccaaacaggagaagagagaagaga
agacaggtcgggctaagcggcggatgcagtacacacggcgctttgtcaacgttgtgccca
cctttggcaagaagaagggccccaaatgcaactcttaagtctttgtaattctggcttc
tctaataaaaagccacttagttcagtcaaaaaaaaa
```

在上面的示例中，在命令行上输入的命令采用此格式。

偶尔，您会看到值（通常用于命令）以 *此格式* 给出，表示必须替换的值。例如，*应用程序名称* 将被替换为应用程序的名称。在下面的命令行中，*5* 和 *25* 将被替换

- * secret -sbegin 5 -send 25

#### 程序清单和代码

程序清单将如下所示：

```
#include "emboss.h"
/* @prog helloworld
******************************************************************/
**
** Prints "Hello, World!" to the screen.
**
*******************************************************************/
int main(int argc, char **argv)
{
    embInit("helloworld", argc, argv);
    ajFmtPrint ("Hello, World!\n");
    embExit();
    return 0;
}
```

偶尔，文本中会引用代码，并以此格式给出。例如：

- 上面的 main() 函数包含函数 ajFmtPrint。

## 其他约定

提到的软件包、应用程序和接口采用此格式。例如：

- HMMER 是一个 EMBASSY 包，用于封装第三方应用程序。

- seqret 是 EMBOSS 程序的示例。

- Jemboss 是 EMBOSS 接口的示例。

程序选项采用此格式：

- -help

数据库名称或数据库的部分采用此格式。例如：

- EMBL 是序列数据库的示例

特定的 EMBOSS 系统文件或目录、环境变量以及所有其他系统特定项目采用此格式。例如：

- .embossrc 和 emboss.default 是 EMBOSS 系统文件。

- EMBOSS_ACDROOT 是 EMBOSS 环境变量。

- 目录是系统项目的示例，例如：/home/auser/emboss/emboss/ajax/

## 特殊文本块

一些特殊注释与正文分开。

### 注意

提醒某些操作可能会产生不良或意外后果的说明。

### 重要

具有特殊意义的注释或说明。

### 备注

与正文相关但属于边缘信息的重要信息。

### 提示

有用的提示、快捷方式等。





## 欢迎使用 EMBOSS 开发者指南

### 摘要

本手册是面向 EMBOSS 新手编写的。您至少需要具备分子生物学的基本了解，并熟悉 UNIX 和 C 编程语言。您应当知道如何使用文本编辑器打开、使用、保存和关闭文件。如果您使用过 EMBOSS 程序并熟悉命令行，也会有所帮助（参见 *EMBOSS 用户指南*）。

EMBOSS 指南中的所有材料均可在 EMBOSS 网站上获取：

http://emboss.open-bio.org

# 第 1 章. 入门

在开始编程之前您应该了解的事项，包括软件许可证详情、CVS（开发者）版本的安装说明、开发者文档摘要以及如何浏览库文档的说明，还有邮件列表详情及如何贡献软件。

# 第 2 章. 您的第一个 EMBOSS 应用程序

编写第一个 EMBOSS 应用程序的逐步指南。这是应用程序开发的温和入门，说明了必要的常见步骤。

# 第 3 章. EMBOSS 下的软件开发

本章概述了任何原生应用程序可以在无需或只需少量额外编码的情况下使用的内置功能。解释了开发的基本步骤：项目管理和规划、ACD 文件和 C 源代码开发、集成和编译、调试、质量保证测试、文档、分发、维护、支持和培训。包含了 C 编码、代码文档和应用程序文档的标准和指南。

# 第 4 章. ACD 文件开发

每个 EMBOSS 和 EMBASSY 程序都有一个 ACD（AJAX 命令定义）文件，用于描述应用程序、其选项（参数）和命令行界面。ACD 文件控制应用程序在命令行中的行为，特别是所有用户输入操作。本章描述了 ACD 文件开发的所有方面。它展示了如何编写应用程序和数据定义，如何在 ACD 文件中执行操作并控制用户提示。最后，描述了用于调试和测试 ACD 文件的实用程序。

# 第 5 章. C 编程

深入探讨 EMBOSS 对象（C 数据结构）的编程和内存管理，这是掌握和扩展库所必需的。内容包括基本 C 数据类型、EMBOSS 对象（C 数据结构）、C 指针编程和内存管理入门。

# 第 6 章. 使用 AJAX 进行编程

使用 AJAX 进行编程的指南，补充在线库文档。它们包括 ACD 文件处理、数组、比对、密码子使用表、异常消息、特征、文件输入和输出、图形、列表、数学、矩阵、菜单、序列模式、系统发育数据、应用程序报告、序列、翻译、‘简单’ ACD 数据类型、字符串、系统代码和表格。

# 第 7 章. 质量保证

对 EMBOSS 代码和文档执行各种质量保证测试，以维护软件包的质量和完整性。您将学习如何为自己的应用程序编写和运行质量保证测试。

# 第 8 章. 应用程序文档标准

没有文档的软件通常价值不大，而良好的文档可以极大地增强软件的实用性。您将学习如何为新应用程序编写符合 EMBOSS 风格的全面文档。

# 第 9 章. 完整的应用程序：secret

详细介绍开发完整应用程序（secret）所需的所有步骤。ACD 文件和 C 源代码的开发说明了任何 EMBOSS 程序可以在无需或只需少量额外编码的情况下使用的强大内置功能。

# 第 10 章. 合并第三方应用程序

将第三方应用程序合并到 EMBOSS 中有充分理由。本章概述了包装和移植第三方代码的好处。给出了应用程序包装器开发和代码移植的指南。以 HMMERNEW EMBASSY 包为例进行说明，该包包装了 Scan Eddy 的 hmmer 应用程序，用于隐马尔可夫模型。概述了应用程序移植的方法。

# 附录 A. ACD 语法参考

AJAX 命令定义（ACD）语言是为编写 EMBOSS 应用程序的 ACD 文件而设计的。此处以简洁形式描述了完整语法。

# 附录 B. C 编程库

AJAX 和 NUCLEUS 编程库的参考信息。

# 附录 C. C 编码标准

为确保 EMBOSS 代码的一致性，所有 C 代码都应符合基本样式。这些标准（大多涉及代码布局）已详细描述。

# 附录 D. 代码文档标准

EMBOSS 代码文档标准描述了如何全面记录您的代码。为一般注释和用于记录应用程序和库源文件、函数及数据类型的结构化注释提供了建议。

# 附录 E. 资源

EMBOSS 的编程接口列表。

# 入门

### 1.1 许可证信息

EMBOSS 根据 GNU 软件许可证，供所有人使用。AJAX 和 NUCLEUS 库根据 GNU 宽通用公共许可证（LGPL）发布。应用程序根据 GNU 通用公共许可证（GPL）发布。如果您计划使用这些库开发专有软件，应阅读完整的许可条件：

```
GPL (http://www.gnu.org/copyleft/gpl.html)
LGPL (http://www.gnu.org/copyleft/lgpl.html)
```

选择这些许可证是为了提供最大灵活性并鼓励开发。只要您为他人保留这些自由，它们就为您在软件开发中提供了自由。

### 1.1.1 通用公共许可证（GPL）

GPL 允许您自由修改、复制和分发应用程序源代码，只要派生作品的源代码根据 GPL 许可并提供。这意味着您可以自由扩展和改进 EMBOSS 应用程序。

区分“派生作品”与完全新代码很重要。通常，派生作品要么是对原始源代码的直接修改，要么是（静态或动态）链接到原始代码。例如，使用 GPL 许可共享库的软件将是“派生作品”，这就是为什么 EMBOSS 库使用 LGPL 以避免此限制。解析 ACD 文件 *不* 构成“派生作品”，本身不受许可约束。许多开发者都这样做过，例如，在编写 EMBOSS 接口时。

> **重要**
> 
> GPL 许可证的规则仅在分发代码时生效。这意味着您可以为内部使用而使用和修改代码，无需获得许可或通知任何人。

### 1.1.2 宽通用公共许可证（LGPL）

LGPL 要求对库的所有更改必须公开发布（源代码必须可用）。但是，可以开发使用库的全新应用程序，而无需发布源代码。库可以与专有软件链接，而如果根据 GPL 许可，库只能与自由程序一起使用。

### 1.1.3 EMBASSY 下的许可

不使用 GPL 或 LGPL 许可证的开发者仍然可以贡献。EMBASSY 集合可以包含使用 AJAX 或 NUCLEUS 但根据其自身许可条件的包。它们将受 AJAX 和 NUCLEUS 库的 LGPL 约束，但不一定受完整 GPL 约束。

### 1.2 安装 CVS（开发者）版本

此处仅包含 EMBOSS 安装的非常基本信息。有关完整说明，请参见 *EMBOSS 管理员指南*。基本安装步骤如下：

- 1. 下载 EMBOSS 源代码。
- 2. 配置 EMBOSS。稳定版本包含用于此目的的‘configure’脚本，而开发者（CVS）版本包含创建此脚本所需的文件。
- 3. 编译 EMBOSS。这将从应用程序源代码生成可执行文件。
- 4. 为可执行文件设置 `PATH`。
- 5. 测试安装。
- 6. 设置您的数据库。

#### 注意

要配置和编译 EMBOSS，系统上必须安装以下 GNU 配置工具：

- - autoconf
- - automake
- - libtool

您的操作系统通常会提供这些软件包；如果没有，则可以下载（从 ftp://ftp.gnu.org/gnu/）源代码并安装（按上述顺序，并确保每个新安装的软件包被优先查找，而不是任何旧版本，然后再安装下一个）。

如果您例如正在开发图形软件，可能会遇到其他软件依赖项；有关更多信息，请参见 *EMBOSS 管理员指南*。





## 1.2.1 通过 CVS 下载

To download via CVS you must have cvs installed on your system. It is there if an application is listed after typing:

```
which cvs
```

You must also use the secure shell SSH for the file transfer. Depending on your shell, type one of the following:

```
setenv CVS_RSH ssh
declare -x CVS_RSH=ssh
export CVS_RSH=ssh
```

To checkout the EMBOSS source code tree, go to the directory where you want the top-level EMBOSS directory created. For example to create EMBOSS in /home/auser/src/ you'd type:

```
cd /home/auser/src
```

To checkout EMBOSS you must first log on to the open-bio.org CVS server by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
```

You will be prompted for a password which is cvs. You are now logged on to the CVS server. Checkout (download) EMBOSS by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss checkout
emboss
```

This will take some time as it's downloading several megabytes of source code and data from the USA. Once the download is complete, terminate your CVS session with:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss logout
```

Here is a typical CVS session:

```
% declare -x CVS_RSH=ssh
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
Logging in to :pserver:cvs@cvs.open-bio.org:2401/home/repository/emboss
CVS password:
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss checkout emboss
cvs checkout: Updating emboss
cvs checkout: Updating emboss/emboss
U emboss/emboss/AUTHORS
U emboss/emboss/COMPAT
U emboss/emboss/COPYING
U emboss/emboss/ChangeLog
.
... screen output truncated
.
%
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss logout
Logging out of :pserver:cvs@cvs.open-bio.org:2401/home/repository/emboss
%
% ls
emboss
```

## 1.2.2 使用 CVS 保持更新

Once you’ve downloaded the CVS version of EMBOSS, you should keep up to date with the latest changes. To do this, move to the directory which you wish to update (or the root emboss directory to update everything) and type:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss update
```

Bear in mind that if you have edited any files then those edits will be merged with the version downloaded via CVS. If you wish to conserve your edits in their original form, you should copy the edited files to a safe place first.

## 1.2.3 配置

You must first build the script and other files used to configure the package. From the second-level EMBOSS directory (e.g. /home/auser/emboss/emboss) type:

```
aclocal -I m4
autoconf
automake -a
```

aclocal is part of the automake package. These commands build the “configure” script (./configure) from the file configure.in (in the EMBOSS distribution) and various other files needed for installation. Specifically:

- aclocal creates aclocal.m4 containing m4 macros used by the auto* tools.
- autoconf reads configure.in and creates the “configure” script.
- automake reads Makefile.am and creates Makefile.in

**Tip**

If you experience any errors at that stage it is possible that your GNU configuration tools are out of date, if so then update them. It is also possible that your version of libtool is more recent than that used in the current EMBOSS CVS; you can check that by looking at the version number in the ltmain.sh file at the top source level of the checked-out tree. If your installed version of libtool is newer then you may have to type autoreconf -fi and then retype the previous GNU configuration tool commands. autoreconf is part of the autoconf package.

Running the resulting ./configure will

- Check whether your system has the necessary functionality and libraries to compile EMBOSS.
- Read Makefile.in and generate platform-specific Makefiles (used later).
- Configure your system. For example, the installation path and various system variables are set and files are flagged to compile (or not).

**Note**

./configure is controlled by command line arguments and by environment variables. Command line arguments are generally used to switch on features autoconf was unable to detect. Environment variables are generally used to set build information such as compiler options.

If you intend to compile using make install (see below) you must specify an installation area for the executables and supporting files. It is good practice to specify these even if you intend to compile with a plain make. To do this, type:

```
./configure --prefix=/home/auser/emboss
```

Further, if you are using the gcc compiler it's a good idea to turn warnings on. You can do this while setting the installation areas:

```
./configure --prefix=/home/auser/emboss --enable-warnings
```

You can also turn on more strict developer warnings by typing:

```
./configure --prefix=/home/auser/emboss --enable-warnings --enable-devwarnings
```

### Important

Note that the warnings switches, such as `--enable-warnings`, are for `gcc` compilers only. There is a further configuration switch, `--enable-devextrawarnings`, which turns on some rather pedantic warnings which are nonetheless useful in some rare circumstances. As that switch can produce compilation noise it is not recommended to specify it in general use.

### Caution

To support the Portable Network Graphics (PNG) format, EMBOSS requires the `libgd`, `libpng` and `libz` libraries. On many Linux systems, most support libraries are installed under the directories `/usr/` and `/lib`. For example, `/lib`, `/usr/lib`, `/usr/X11R6/lib`, etc. Whereas Linux distributions include RPMs for these libraries, other operating systems do not.

If you are installing these libraries and include files in somewhere other than `/usr` then you must specify their location when configuring. Assuming you have installed them under `/usr/local` (e.g. `/usr/local/lib` and `/usr/local/include`) you would add the following switch to the configuration command line:

```
--with-pngdriver=/usr/local
```

For more information on the configurability of the build type:

```
./configure --help
```

## 1.2.4 编译

To compile EMBOSS, type:

```
make
```

This will, by using the Makefiles, compile all the source files into executable binaries within your chosen checked-out location e.g.:

```
/home/auser/emboss/emboss/emboss
```

Alternatively, compiling with:

```
make install
```

will install the binaries and supporting files into bin, lib and share subdirectories of the directory you specified using --prefix on the configure line. In the example above, this is the top-level EMBOSS directory level from the CVS checkout, e.g.:

```
/home/auser/emboss
```

Had you not specified --prefix=/home/auser/emboss they'd be installed to /usr/local by default (that isn't recommended).

> **Tip**
> If you want EMBOSS installed in somewhere other than /usr/local then use the --prefix option of GNU configure to specify the EMBOSS installation directory. This is the recommended method of installation as EMBOSS has hundreds of files which might otherwise obscure other software, particularly under /usr/local/bin.

To compile and reinstall EMBOSS on subsequent occasions, use the following commands:

```
make clean
./configure
make
make install
```

Though extremely rare, there are circumstances where you may have to type rm config.cache (on very old installations) or rm -rf autom4te.cache before doing the above. Those occasions generally happen when trying to update a rather old existing version of EMBOSS.

### 1.2.4.1 Static and dynamic compilation

> **Note**
> A static library (statically linked library) is a library called by an application in which links to external functions and variables are resolved at compile-time by a linker. Static libraries are either compiled into object files and merged with the application during building/linking into a single executable, or are loaded at run-time and are accessible to the executable.
> 
> A dynamic library (dynamically linked library) in contrast implements dynamic linking, where libraries remain in separate files on disk and are not copied into the executable or library at compile-time. Instead a loader is used to access the library at load or run-time.
> 
> Executables created using static libraries are larger than executables linked to dynamic libraries, because static libraries include the code for the library function(s) within the executable. Static libraries, however, can be useful for debugging purposes and sometimes result in faster executables than when using dynamic libraries.





上述命令将创建动态链接的 EMBOSS。若要创建静态链接的 EMBOSS，请使用：

```
./configure --disable-shared
```

### 1.2.4.1.1 通过脚本进行静态编译

有一个可用于编译 EMBOSS 的脚本。如果您需要静态链接的 EMBOSS，只需键入：

```
source make-static-developers
```

或

```
./make-static-developers
```

具体取决于您的 shell。
这将调用以下命令：

```
aclocal -I m4
autoconf
automake -a
./configure --enable-warnings --disable-shared --enable-debug
make
```

## 1.2.5 设置您的 PATH

**注意**

您的 PATH 是一个环境变量，它定义了一组目录列表，操作系统会在响应 Unix 命令时搜索这些目录以查找可执行应用程序。例如，当您键入 `cd` 或 `ls` 等命令时，被调用的应用程序通常是 /bin/cd 或 /bin/ls。大多数 Unix 安装会自动将目录 /bin 放入您的 PATH 中。对于 EMBOSS，您可能需要手动设置 PATH 以指向可执行文件。

您必须设置可执行应用程序的路径。假设 EMBOSS 已安装在您的主目录中，并且您使用的是 csh 风格的 shell，则键入以下命令（根据需要替换路径）：

```
set path= (/home/auser/emboss/emboss/emboss $path)
rehash
```

或者，如果您使用的是 sh 风格的 shell，则键入以下命令：

```
export PATH=/home/auser/emboss/emboss/emboss:$PATH
```

但是，如果您使用的是 make install 而不是仅 make，则命令会有所不同（您必须将 PATH 设置为安装可执行文件的位置）。对于 csh 风格的 shell：

```
set path= (/home/auser/emboss/bin $path)
rehash
```

对于 sh 风格的 shell：

```
export PATH=/home/auser/emboss/bin:$PATH
```

## 1.2.6 测试一切是否正常

要测试您的安装是否正常，可以运行：

```
embossversion
```

并检查是否报告了 EMBOSS 版本号。

您也可以尝试使用 seqret 应用程序从随 EMBOSS 发行版一起提供的测试数据库中检索一些序列。但是，在这样做之前，您需要为 EMBOSS 设置数据库。

## 1.2.7 数据库设置

> **注意**
> 数据库设置在 *EMBOSS 管理员指南* 中有介绍；下面仅介绍最基本的内容。

EMBOSS 发行版中包含一些测试数据库。例如，它们位于：

```
/home/auser/emboss/emboss/test
```

您想要使用的任何数据库都必须定义在以下文件之一中：

- .embossrc（在您的主目录中）
- emboss.default（在顶级 emboss 目录中）

这些文件用于配置 EMBOSS。.embossrc 用于个人配置，而 emboss.default 用于站点范围配置。CVS 发行版中包含一个模板文件（.../emboss/emboss/emboss.default.template）。现在，在您的主目录中创建一个名为 .embossrc 的文件，内容如下（您需要更改测试目录的路径）：

```
DB embl
[
type: N
method: direct
format: embl
dir: /home/auser/workspace/emboss/emboss/test/embl/
file: *.dat
comment: "EMBL sequences"
]

DB swissprot
[
type: P
method: direct
format: swiss
dir: /home/auser/workspace/emboss/emboss/test/swiss/
file: seq.dat
comment: "Swissprot sequences"
]
```

设置好数据库后，执行以下命令（在提示符处接受默认值）：

```
seqret embl:x65923
more x65923.fasta
seqret swissprot:UBR5_RAT
more UBR5_RAT
```

如果您得到类似于以下的输出，则可以放心，安装已成功。

```
% seqret embl:x65923
Reads and writes (returns) sequences
Output sequence [x65923.fasta]:
% more x65923.fasta
>X65923 X65923.1 H.sapiens fau mRNA
ttcctctttctcgactccatctttcgcggtagctgggaccgccgtttcagtcgccaatatgc
agctctttgtccgcgcccaggagctacacaccttcgaggtgaccggccagg aaacggtcg
ccagatcacaggctcatgtagcctcactggagggcattgccccggaagatcaagtcgtgc
tcctggcagggcgccccctggaggatgaggccactctggccacgtgcggggtggaggccc
tgactacctggaagtagcaggccgcatgcttggaggttaaagttcatggttccctggccc
gtgctggaaaggtgagaggttcagactcctaaggtggccaaacacggagagaagaagaaga
agacaggtcgggctaaggcgggatgcagtacaaccggcgctttgtcaacgttgtgccca
cctttggcaagagaagggccccaatgccaactcttaagcttttgtaattctggctttc
ctaataaaaaaggcacttagttcagtcaaaaaaaaa
%
% seqret swissprot:UBR5_RAT
Reads and writes (returns) sequences
Output sequence [ubr5_rat.fasta]:
% more ubr5_rat.fasta
>UBR5_RAT Q62671 Q62671 E3 ubiquitin-protein ligase UBR5 (6.3.2.-)
MSARGDFLNYALSLMRSHNDEHSDVLPVLDVCSLKHVAYVFQALIYWIKAMNQQTTLDT
PQLERKRTRELLELGIDNDESEHENDDTSQSATLNDKDDESLPAETGQNHFPFRRSDSM
TFLGCIPPNPFEVPLAEAIPLADQPHLLQPNARKEDLFGRPSQGLYSSSAGSGKCLVEVT
MDRNCEVLPTKMSYAANLKNVMNQNRQKKAGEDQSMLAEEDASSKKPSAHVDVAAQLK
SSLAAIGLTESGEGPPLTSFRPCQSFMGMVISHDMILLGRWRLSLELFGRVFMEGAEPG
SILTELGGFEVKESKFREMEKLRNQGSRDLSLEVDRDRDLLIQQTMRQLNNHFGRRCAT
TPMAVHRVKVTFKDEPGEGSGVARSFYTAIAQAFLSNEKLPLNLDCIQNANKGTHTSLMQR
LRNRGERDREREREREMRRSSGLRAGSRRDRDRDFRRQLSIDTRPFRPASEGNPSDDPPDP
LPAHRQALGERLYPRVQAMQPAFASKITGMLELISPAQLLLLLLASEDSLRARVEEAMELI
VAHGRENGADSILDLGLLDSSEKVQENRKRHGSSRSVVDMDLDDTDDGDDNAPLFYQPGK
RGFYTPRPGKNTEARLNCFRNIGRILGCLLQNELCPITLNRHVIKVLLGRKVNWHDFAF
FDPVMYESLRQLILASQSSDADAVFSAMDLFAFVDLCKEEGGGQVELIPNGVNIPIVTPQN
VYEYVRKYAEHRMLVVAEQPLHAMRKGLLDVLPKNSLEDLTAEDFRLLVNGCGEVNVQML
ISFTSFNDESGENAEKLLQFKRWFWSIVERMSMTERQDLVYFWTSSPSPLPASEEGQFPMP
SITIRPPDDQHLPTANTCISRLYVPLYSSKQILKQKLLLLAIKTKNFGFV
```

## 1.2.8 EMBASSY 包

以下示例用于安装 EMBASSY 包的 CVS（开发者）版本。

- 1. 进入包目录：

```
cd embassy/PackageName
```

- 2. 创建配置文件：

```
aclocal -I m4
autoconf
automake -a
```

- 3. 配置并编译包。配置应使用与主包相同的选项。因此，如果您使用了：

```
./configure -with-pngdriver=/opt/lib -prefix=/home/auser/emboss
```

用于主包，那么对 EMBASSY 包也使用相同的命令。然后：

```
make
make install
```

## 1.3 开发者文档

EMBOSS 文档非常丰富。根据您的经验和要求，您可以采用不同的方式来学习它：

- 应用程序文档
- 库文档
- 源代码
- 使用 SRS 浏览源代码
- 演示应用程序（每个库文件）
- 关键主题的编程指南
- AJAX 命令定义（ACD）文档
- C 编码标准和指南
- 质量保证指南
- 代码和应用程序文档标准
- EMBOSS 软件开发课程。

## 1.3.1 应用程序文档

每个 EMBOSS 应用程序都有详细文档：

| CVS（开发者）版本文档 | http://emboss.open-bio.org/rel/dev/apps |
|---|---|
| 稳定版 6 文档 | http://emboss.open-bio.org/rel/rel6/apps |

## 1.3.2 库文档

AJAX 和 NUCLEUS 包含数百个库调用，初次使用可能令人望而生畏。CVS（开发者）版本和稳定版的主要版本均可在线查阅文档。文档源自源代码本身中的结构化注释（参见附录 D，代码文档标准）。

### 1.3.2.1 AJAX 库文档

AJAX 是所有 EMBOSS 应用程序使用的核心库。它涵盖标准数据结构和算法：

| CVS（开发者）版本文档 | http://emboss.open-bio.org/rel/dev/libs |
|---|---|
| 稳定版 6 文档 | http://emboss.open-bio.org/rel/rel6/libs |

### 1.3.2.2 NUCLEUS 库文档

NUCLEUS 提供特定于分子序列分析的高级功能：

| CVS（开发者）版本文档 | http://emboss.open-bio.org/rel/dev/libs/ |
|---|---|
| 稳定版 6 文档 | http://emboss.open-bio.org/rel/rel6/libs |

## 1.3.3 浏览库

浏览库文档非常简单

- 从 EMBOSS 主页（http://emboss.open-bio.org/），点击“AJAX”或“NUCLEUS”。

这将显示 AJAX 或 NUCLEUS 库的表格。

AJAX 或 NUCLEUS 库表格中的行对应于单个库文件，例如用于比对、数组处理、断言函数等。表格中有以下列：

| 库文档 | 链接到库文件文档（见下文），后者引用了所有可用对象（C 数据结构）和函数。 |
|---|---|
| 简短描述 | 库文件的简短描述。 |
| 编程指南 | 链接到库文件的详细编程指南和使用说明（如果可用）（参见第 6.2 节，“编程指南”）。 |
| 示例应用程序（C 源代码） | 链接到示例应用程序的 C 源代码，用于说明库的使用（如果可用）（参见第 6.1 节，“演示应用程序”）。 |
| 示例应用程序（ACD 代码） | 链接到示例应用程序的 ACD 代码（参见第 6.1 节，“演示应用程序”）。 |

### 1.3.3.1 库文件文档

- 在表格中找到“字符串操作”，并按照“库文档”下的链接操作。

这将显示可用于字符串处理（`ajstr.c/h` 库文件）的文档。





库文件文档包括以下部分：

| 摘要 | 库文件的简短描述。 |
| 描述 | 库文件的较长描述。 |
| 数据结构 | 每个对象（C 数据结构）的名称、简短描述和进一步信息的链接。 |
| 函数类别描述 | 按对象类型组织的每个函数类别的正式描述。 |
| 函数（按对象和类别组织） | 按对象类型和函数类别组织的每个函数的名称、简短描述和正式描述链接。 |
| 函数（字母顺序列表） | 按字母顺序组织的库中每个函数的名称、简短描述和正式描述链接。 |

### 1.3.3.2 函数文档

函数文档包含所有关键信息。文件中的各部分如下：

| 函数概要 | 函数名称、简短描述及首次提供时的 EMBOSS 版本号。 |
| 函数原型 | 标准 C 形式的函数原型。 |
| 函数参数表 | 函数参数标记如下：<br>* `INPUT` 参数由函数读取。<br>* `OUTPUT` 参数由其写入。<br>* `UPDATE` 参数可能被读取和写入。 |
| 返回值 | 返回值的描述。 |
| 描述 | 函数的完整描述。 |
| 源代码 | 函数的 C 源代码。 |
| 使用示例 | 函数的典型用法，自动生成。 |
| 注释 | 诸如使用说明等外围文档。 |
| 警告 | 谨慎的使用建议、已知错误等。 |
| 异常 | 函数可能生成的异常和其他消息。 |
| 依赖项 | 函数依赖的外部实体，例如环境变量和文件。 |
| 另请参见 | 链接到同一类别中的函数。 |

### 1.3.3.3 对象（C 数据结构）文档

对象已全面描述。

| 结构概要 | C 数据结构名称、简短描述及首次提供时的 EMBOSS 版本号。 |
| 概要 | 对象概要（数据类型和变量名）。 |
| 数据定义 | 对象的数据类型定义。 |
| 描述 | 对象的完整描述。 |
| 元素 | 数据结构中元素的描述。 |
| 函数 | 操作该对象的函数。 |
| 源代码 | 数据结构的 C 源代码。 |
| 使用示例 | 典型用法示例，自动生成。 |
| 注释 | 诸如使用说明等外围文档。 |
| 警告 | 谨慎的使用建议、已知错误等。 |
| 另请参见 | 链接到同一库文件中的结构。 |

## 1.3.4 源代码

源代码是重要参考。搜索库或应用程序代码的简单方法是使用 UNIX 命令 grep 在 C 源文件中搜索关键字。这是一种快速查找对象或函数的便捷直接方式。

如果您不确定如何执行特定任务，例如读取数据文件，那么您应该能够快速找到执行类似操作的程序。请记住，解决问题有多种方法，您找到的示例不一定是最佳方法。

每个应用程序有两个文件需要查看（C 源代码和 ACD 文件）。它们位于以下目录中：

```
/home/auser/emboss/emboss/emboss/c
/home/auser/emboss/emboss/emboss/acd/
```

### 1.3.4.1 使用 SRS 导航源代码

可以直接检查源代码并使用 SRS 进行导航。库源代码在 EBI SRS 服务器的 SRS 中编入索引：

```
http://srs.ebi.ac.uk/
```

对象（C 数据结构）和函数有单独的 SRS 数据库：

| EFUNC：CVS（开发者）版本中的函数 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EFUNC |
| EDATA：CVS（开发者）版本中的对象 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EDATA |
| EFUNCREL：稳定版 6.0.0 中的函数 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EFUNCREL |
| EDATAREL：稳定版 6.0.0 中的对象 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EDATAREL |

### 1.3.4.1.1 搜索 EDATA

从 http://www.ebi.ac.uk/srs/：

- 1. 单击“库页面”选项卡。
- 2. 单击“其他数据库”左侧的 + 以展开“其他数据库”部分。

您将看到列出的 EDATA、EDATAREL、EFUNC 和 EFUNCREL。

- 3. 选中 EMBOSS 数据结构（CVS）旁边的复选框，然后单击“查询表单”选项卡。
- 4. 将其中一个 AllText 选项更改为 ID，并在其关联框中输入 * 字符，然后单击搜索。

您将看到每个可用对象的列表。以下是更具体的搜索：

- 1. 返回查询表单，将 * 替换为 ajpstr（AJAX 字符串对象）。
- 2. 单击搜索。

您将看到返回两个条目，AjPStr 和 AjPStrTok。单击 AjPStr 的链接。此处的文档分为几个部分。前三部分给出了对象的名称、描述和“别名”：

- AjSStr 是字符串对象的名称。
- AjPStr 是对象指针的数据类型。
- AjPPStr 是指向对象指针的指针的数据类型。
- AjOStr 是对象本身的数据类型。

注意 AjSStr、AjOStr、AjPStr 的含义 AjSStr 是字符串对象的正式名称，AjOStr 是对象的数据类型名称，而 AjPStr 是对象指针的数据类型名称。在实践中，AjOStr（以及所有其他 AJO* 数据类型）在 EMBOSS 中从不使用。相反，内存中对象实例的内存会动态分配给指针 AjPStr（参见第 5.5 节，“使用对象的编程”）。因此，在 SRS 中，AjPStr 在“名称”之后给出，为了简洁起见，“对象”常被用来指代 AjPStr（例如），而实际上指的是“对象指针”。对象和指针的使用在其他地方有深入介绍（第 5.5 节，“使用对象的编程”）。

EDATA 和 EDATAREL 包含使用每个对象的函数链接，如果您想知道可以对对象做什么，这很方便。EFUNC 和 EFUNCREL 中的函数按相关功能类别组织，这些类别对应 C 源文件中的部分（参见附录 D，代码文档标准及以下内容）。

在“别名”部分之后，您将看到类别中几个函数块。您看到的类别将取决于库文件，但可能包括：

- 迭代器 – 迭代，例如遍历字符串中的单个字符。
- 构造函数 – 创建对象的新实例（分配内存）。
- 析构函数 – 销毁对象的实例（释放内存）。
- 赋值 – 初始化对象，必要时替换内容。
- 修改器 – 更改或替换对象的内容。
- 运算符 – 使用但不更改对象的内容。
- 输出 – 将对象的内容写入外部文件。
- 强制转换 – 将对象转换为另一种类型的对象或数据。

在页面底部，您将看到以下部分：

- 属性列出 C 数据结构的元素。
- 主体给出对象定义的 C 代码。

### 1.3.4.1.2 搜索 EFUNC

可以直接搜索 EFUNC 数据库。如果您知道想要的函数类型但不知道名称，这很有用。函数名称和函数参数的名称及顺序已标准化（参见第 D.1 节，“代码文档标准”），以便直观且一致。

假设您想搜索一个将一个字符串追加到另一个字符串的函数：

- 1. 返回 SRS 数据库页面，取消选中 EDATA 数据库，并选中 EFUNC 数据库的复选框。
- 2. 选择查询表单。
- 3. 通常最好将搜索限制在描述字段，以检索更具体的匹配项。因此：将 AllText 更改为 Description。
- 4. 在关联框中键入 append & string，然后单击搜索。

将出现函数列表。您只能使用以 aj 或 emb 开头的函数，分别是 AJAX 和 NUCLEUS 库中的公共函数。其他函数是隐藏函数，由 EMBOSS 的内部访问，不供一般使用。





你需要的函数是 ajStrAppend* 家族中的函数。你会发现，有些函数接受其他字符串对象、字符串或仅单个字符。

当然，这种搜索方法受函数描述中使用的词汇限制。例如，使用的是术语“append”，而不是“catenate”。你可以通过重复上述搜索并使用 catenate & string 来亲自验证。

为了展示限制搜索的优势：

- 将 Description 字段改回 AllText，并重复 string & append 查询。

你会发现结果列表中包含大量噪声。

当然，如果你知道函数名称并需要查看源代码，可以使用 SRS。

- 1. 返回 EFUNC 页面并将 AllText 改为 ID。
- 2. 现在使用 ajstrappend 作为搜索词。执行搜索，然后单击 EFUNC: ajStrAppends。

屏幕上应显示 ajStrAppendS 的源代码。同样，输出分为几个部分。函数名称指示其所在的源库文件；ajStrAppendS 中的 str 指示 ajstr 库。description 字段给出了使用 Description 搜索时搜索的文本。

对库用户来说，最有用的信息是 Input、Returns 和 Prototype 字段。

Input 字段显示，该函数将字符串对象指针的地址作为其第一个参数，将字符串对象指针作为其第二个参数。Returns 字段显示函数的返回值（AjBool，一个布尔值）。Prototype 字段中一目了然地给出了函数的所有这些信息。

原型下方是函数体。这显然包含函数的源代码。C 语言保留字以红色突出显示。源代码中标记了对其他 EMBOSS 函数的任何调用。未突出显示的函数调用是标准 C 库调用。例如，你可以单击 ajFatal 来查看该函数的代码。

单击原型行上的红色箭头将显示使用此特定函数的所有 EMBOSS 函数。单击蓝色箭头将显示由此特定函数调用的所有 EMBOSS 函数。

## 1.3.5 演示应用程序

EMBOSS 为某些 AJAX 和 NUCLEUS 库文件包含一个应用程序，用于说明常用函数的正确用法。目前，这些“演示应用程序”保存在 myembossdemo 包中，并带有前缀“demo”。例如，以下文件说明了字符串库的用法：

```
/home/auser/emboss/emboss/embassy/myembossdemo/emboss src/demostring.c
/home/auser/emboss/emboss/embassy/myembossdemo/emboss_acd/demostring.acd
```

有关编译和使用这些应用程序的信息，请参见第 3.1 节“EMBOSS 编程”。

## 1.3.6 编程指南

大多数 AJAX 子库均提供编程指南（第 6.2 节“编程指南”）。这些指南总结了可用的 C 数据结构和函数，并给出了使用示例。如果你想了解 EMBOSS 编程中特定领域的所有内容，它们非常有用。

## 1.3.7 AJAX 命令定义 (ACD) 开发者指南和语法

每个 EMBOSS 应用程序都有一个 AJAX 命令定义 (ACD) 文件，其中包含命令行界面的完整定义，并定义了应用程序运行所需的所有信息。

ACD 文件采用 ACD 语法编写（附录 A，_ACD 语法参考_），该语法定义了一组可供应用程序使用的数据类型、用于限定数据类型的属性以及更多内容。要开发新应用程序，你需要掌握 ACD 编程（参见第 5 章，_C 编程_）。

## 1.3.8 C 编码标准和指南

为确保一致性，所有代码都应符合基本样式和标准。你应该熟悉这些 C 编码标准（附录 C，_C 编码标准_），其中大部分涉及代码布局。

## 1.3.9 质量保证指南

为保持软件包的质量和完整性，对代码和文档执行各种质量保证测试。这包括应用程序测试运行、编译和内存泄漏测试以及用于对象和函数的结构化文档的验证。

所有代码都应经过彻底测试，新库代码应按照 EMBOSS 标准（见下文）进行文档记录，以便可以执行检查。如果你开发新应用程序，还应为其提供测试数据（参见第 7.2 节“应用程序质量保证”）。

## 1.3.10 代码和应用程序文档标准

没有文档的软件通常价值不大，而良好的文档可以极大地提高软件的实用性。所有贡献的代码都应有充分的文档。任何新应用程序还需要最终用户文档。为确保一致性，文档应符合为代码（附录 D，_代码文档标准_）和应用程序（第 8 章，_应用程序文档标准_）定义的基本样式和标准。

## 1.3.11 EMBOSS 软件开发课程

“使用 EMBOSS 进行生物信息学软件开发”的实践课程为 EMBOSS 编程提供了良好的入门介绍，包括使用 EMBOSS 编程库编写基本生物信息学应用程序的所有步骤。如果你想参加或主持课程，请联系 EMBOSS 开发者（emboss-bug@emboss.open-bio.org）。

## 1.4 项目邮件列表

有三个 EMBOSS 邮件列表可供你加入。这些列表为关于 EMBOSS 及其未来发展的讨论提供了论坛，是宝贵的帮助来源。

### 1.4.1 用户邮件列表

```
emboss@emboss.open-bio.org
```

这是一个公开列表（任何人都可以加入），供最终用户进行一般性公告和讨论。要订阅此列表，请访问：

```
http://emboss.open-bio.org/mailman/listinfo/emboss
```

### 1.4.2 开发者邮件列表

```
emboss-dev@emboss.open-bio.org
```

这是一个封闭列表，供使用 EMBOSS 的开发者进行讨论。要订阅此列表，请访问：

```
http://emboss.open-bio.org/mailman/listinfo/emboss-dev
```

如果你希望为 EMBOSS 做出贡献，请将代码和文档发送到：

```
emboss-submit@emboss.open-bio.org
```

### 1.4.3 公告邮件列表

```
emboss-announce@emboss.open-bio.org
```

这是一个用于重大公告的列表，主要涉及新版本和更新。它的发帖量远少于其他群组，适合希望保持软件更新但对其他讨论兴趣不大的系统管理员。要订阅此列表，请访问：

```
http://emboss.open-bio.org/mailman/listinfo/emboss-announce
```

### 1.4.4 邮件归档

可查阅讨论邮件列表之前发帖的归档。

### 1.4.4.1 用户邮件列表归档

```
http://emboss.open-bio.org/pipermail/emboss/
```

这是 emboss@emboss.open-bio.org 的归档。

### 1.4.4.2 开发者邮件列表归档

```
http://emboss.open-bio.org/pipermail/emboss-dev/
```

这是 emboss-dev@emboss.open-bio.org 的归档。

## 1.5 向 EMBOSS 贡献软件

### 1.5.1 请提交你的代码！

你在 EMBOSS 上的内部开发很可能对其他人有价值。请提交你的代码。你可以与 EMBOSS 开发者讨论你所做的工作：

```
emboss-bug@emboss.open-bio.org.
```

否则，如果你有准备提交的软件，请将代码和文档发送到：

```
emboss-submit@emboss.open-bio.org
```

如果你的添加具有通用实用性，它们将被添加到软件包中。EMBOSS 开发者将协助你对代码进行任何必要的更改，或为你执行这些更改。

### 1.5.2 代码提交类型

EMBOSS 的长期成功依赖于外部开发者的代码提交。提交可能包括：

- 对现有 AJAX 或 NUCLEUS 库的扩展
- 对现有 EMBOSS 或 EMBASSY 应用程序的扩展
- 新库或应用程序的代码
- 响应 EMBOSS 功能请求的代码
- 响应 EMBOSS 错误报告的代码修复
- 调用 EMBOSS 应用程序的脚本和其他软件
- 其他内容。

### 1.5.3 已知所需的开发工作

有许多已知需要进行软件开发的领域。

```
http://emboss.open-bio.org/wiki/New_Applications
```

该列表包括 EMBOSS 用户提交的新应用程序建议、新功能请求和其他开发工作。在这些领域的工作肯定会很有价值，因此如果任何已知需求引起你的兴趣，请志愿参与该工作。

如果你有一个不是已知需求的编码项目，你的代码仍然非常受欢迎。请将你的想法发送到邮件列表。

### 1.5.3.1 EMBOSS 功能请求和错误报告

一种非常有价值的贡献方式是编写代码来响应 EMBOSS 用户发布的功能请求和错误报告。这些请求记录在 SourceForge 上：

```
https://sourceforge.net/projects/emboss/support
```





# 你的第一个 EMBOSS 应用程序

大多数编程书籍都以在屏幕上输出简单短语的程序开始，而这个短语总是“Hello World!”。本节将引导你在 EMBOSS 下编写 helloworld 的过程。你将了解每个 EMBOSS 程序共有的基本元素，并了解创建应用程序的步骤。

下面的一些示例使用 myemboss（第 3.2 节，“集成与编译”），因此你必须先安装并配置此软件包。myemboss 是一个特殊的 EMBASSY 软件包，位于常规 EMBASSY 应用程序目录中，例如：

```
/home/auser/emboss/emboss/embassy/myemboss
```

## 2.1 C 语言中的 helloworld

以下是一个在屏幕上打印“Hello World!”的 C 程序的源代码：

```
#include <stdio.h>
int main(void)
{
  printf("Hello World!\n");
  return 0;
}
```

第一行是预处理器指令，告诉编译器包含头文件 stdio.h。要包含的文件名周围的尖括号告诉预处理器在默认位置查找 stdio.h。在 Linux 系统上，此默认位置通常是目录 /usr/include。

该程序由一个单一函数（main）组成，该函数没有参数且返回整数类型，在此情况下，它在向屏幕打印“Hello World!”后向操作系统返回 0。

如果将源代码保存到名为 helloworld.c 的文件，则要获得程序的可执行（可运行）版本，必须通过键入以下命令之一来编译源代码。

使用 gcc（ANSI C 编译器）：

```
gcc helloworld.c -o helloworld
```

使用 cc（默认 C 编译器）：

```
cc helloworld.c -o helloworld
```

如果没有编译错误，你将得到一个名为 helloworld 的可执行文件。如果你省略了 -o helloworld，可执行文件将被称为 a.out。要运行你的程序，只需在 UNIX 提示符下键入 helloworld：

```
% helloworld
Hello World!
%
```

运行 csh shell 的人可能需要先键入 rehash。

## 2.2 EMBOSS 中的 helloworld

你可能按照标准模式编写程序：编写源代码文件，编译源代码，然后调试生成的可执行程序。最后运行你调试过的二进制文件。

编写 EMBOSS 程序时有一些额外的步骤。关键区别在于，除了编写源代码外，你还必须为新应用程序编写一个 ACD 文件。ACD 文件包含命令行接口的描述。它指定了确切需要哪些输入值、如何验证它们以及输出什么。它控制应用程序在命令行上的行为，特别是用户输入操作。

所有必需的参数都在应用程序正式开始之前提示输入。输入值被读取并保存在内存中，按需打开文件等等，以便在应用程序正式启动时所有参数都可用。EMBOSS 应用程序在处理数小时后不能再向用户询问更多信息！

在编写源代码之前先编写 ACD 文件是一种良好的做法，因为这迫使你仔细考虑应用程序的输入和输出以及用户确切需要提供什么。然后你应该使用名为 acdc 的 EMBOSS 应用程序来测试 ACD 文件（见下文）。此外，你必须将应用程序集成到 EMBOSS 或 EMBASSY 中。

因此，编写你的第一个 EMBOSS 应用程序的基本步骤是：

- 1. 编写 ACD 文件
- 2. 测试 ACD 文件
- 3. 编写源代码
- 4. 将应用程序集成到 EMBOSS 或 EMBASSY 中（例如 myemboss）
- 5. 编译。

此外，任何软件项目还有几个其他注意事项：

- - 规划与设计 – 考虑问题并设计软件
- - 调试 – 使其在不崩溃或出现明显问题的情况下运行
- - 测试 – 确保其在所有条件下都能正确工作
- - 文档 – 描述其工作原理
- - 安装与分发
- - 维护、支持和培训。

### 2.2.1 规划与设计

你应该仔细考虑手头的任务，并在编码之前规划或设计你的软件。考虑输入和输出以及源代码中的主要逻辑步骤。**helloworld** 是一个非常简单的程序，必须：

- 1. 读取并处理 ACD 文件
- 2. 向屏幕打印“Hello World!”
- 3. 干净退出

软件规划在第 3.1 节“EMBOSS 编程”中介绍。

### 2.2.2 编写 ACD 文件

**helloworld** 的输入和输出非常简单。该程序只需向屏幕打印“Hello World!”，因此不需要用户提供任何内容。因此 ACD 文件相当精简也不足为奇。不过，作为最低要求，所有 ACD 文件都必须包含一个带有单个 _documentation:_ 属性的 _应用程序定义_：

```
application: helloworld
[
    documentation: "Prints 'Hello World!' to the screen."
]
```

此定义必须放在文件的第一位。定义由 `application:` 标记组成，后跟应用程序名称和一组方括号括起来的属性块。每个属性都是一个 `name: value` 键值对。上述定义包含一个 `documentation:` 属性。文本应是对程序的简洁描述，并在运行程序时打印到屏幕上。如果缺少 `documentation:` 属性，运行程序时将发出警告。

通常你会在一个名为 **myemboss** 的特殊 EMBASSY 软件包中开发新代码，该软件包专门用于尚未准备好合并到主 EMBOSS 或 EMBASSY 软件包中的应用程序（参见第 3.1 节“EMBOSS 编程”）。将你的 ACD 文件保存在 **myemboss** ACD 目录中：

```
../myemboss/emboss_acd
```

如果要将程序添加到 EMBOSS 本身，则目录将是：

```
../emboss/acd
```

ACD 文件的文件名形式为 ApplicationName.acd，其中 ApplicationName 是应用程序的名称。文件扩展名 .acd 是强制性的。文件名（不带 .acd 扩展名）与 C 源代码文件名相同是合理的（但不是强制性的）。

有关更多信息，请参阅 ACD 语法的详细信息（附录 A，ACD 语法参考）和 ACD 文件开发（第 4.1 节，“ACD 文件开发简介”）。

### 2.2.3 测试 ACD 文件

提供了特殊实用程序（第 4.6 节，“ACD 实用程序”）来帮助你测试和验证 ACD 文件。你需要的主要工具称为 acdc（ACD 编译器），当在命令行上将 ACD 文件名作为第一个参数给出时，它将解析文件、验证文件、解析命令行并“运行”应用程序命令行接口，就像应用程序本身正在运行一样。

因此，测试 ACD 文件很容易。你只需运行 acdc，并将你的应用程序名称作为参数：

```
acdc ApplicationName
```

其中 ApplicationName 是应用程序的名称。因此，对于 helloworld：

```
% acdc helloworld
Prints 'Hello World!' to the screen.
%
```

acdc 读取 helloworld.acd 并读取任何所需数据，就像应用程序本身正在运行一样。它还将测试命令行上的任何内容，并以与真实应用程序完全相同的方式报告错误。在此情况下，没有所需数据，命令行上也没有其他内容。由于 acdc 在上面的示例中没有报告错误，我们可以假设一切正常。

### 2.2.4 编写源代码

在知道你有一个可用的 ACD 文件后，你可以转向 C 源代码本身，它应该类似于这样：

```
/* @source helloworld Prints "Hello World!" to the screen.
 *
 * @author: Copyright (C) Arthur Geek (ageek@ebi.ac.uk)
 *
 * @#
 *
 * This program is free software; you can redistribute it and/or
 * modify it under the terms of the GNU General Public License
 * as published by the Free Software Foundation; either version 2
 * of the License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
 ************************************************************************/

#include "emboss.h"

/* @prog helloworld *********************************************************
 *
 * Prints "Hello World!" to the screen.
 *
 *****************************************************************************/

int main(int argc, char **argv)
{
    embInit("helloworld", argc, argv);
    ajFmtPrint("Hello World!\n");
    embExit();
    return 0;
}
```

helloworld.c 文件以及事实上所有 EMBOSS 程序都有三个主要部分：

- 标准 EMBOSS 应用程序文档标头
- #include 语句
- 应用程序代码本身

在 C 语言中（EMBOSS 代码也不例外），每个程序都必须有一个 main() 函数。对于 helloworld.c，程序本身仅由 main() 函数组成，但大多数程序除了 main() 之外还有其他函数。

源代码以标准 EMBOSS 标头开始。此注释块包括程序名称及其简短描述、版权声明、许可信息、免责声明、作者姓名和联系信息。例如 @source 之类的标签允许 EMBOSS 从代码自动生成文档。EMBOSS 应用程序根据 GNU 通用公共许可证授权，因此这些注释必须包含在源代码中。

接下来是预处理器指令 #include "emboss.h"。与 #include <stdio.h> 相反，这导入了整个 EMBOSS 接口，即使所有 EMBOSS 库调用可供你使用。这必须包含在每个 EMBOSS 程序的开头。





在 EMBOSS 版本的 helloworld 中，文件名 emboss.h 用引号括起来，这意味着预处理器将在当前目录以及配置文件 emboss/Makefile.am 中定义的任何其他目录中查找。

emboss.h 是主包含文件。它包含 AJAX 和 NUCLEUS C 编程语言库的所有其他头文件。如果你查看头文件内部，你会发现最终 stdio.h 本身也被包含：

```
% more nucleus/emboss.h
#ifndef emboss_h
#define emboss_h
#include "ajax.h"
#include "ajgraph.h"
#include "embaln.h"
#include "embcom.h"
#include "embcons.h"
#include "embdbi.h"
.
.
% more ajax/core/ajax.h
#ifdef __cplusplus
extern "C"
{
#endif
#ifndef ajax_h
#define ajax_h
#include "ajarch.h"
#include <stdarg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "ajassert.h"
#include "ajdefine.h"
#include "ajstr.h"
#include "ajtime.h"
#include "ajfile.h"
.
.
```

### 注意

#include "emboss.h" 语句是 C 预处理器的指令。任何以 # 字符开头的行都会在源代码编译之前由 C 预处理器处理。例如，行 #include "emboss.h" 告诉预处理器在编译之前用文件 emboss.h 的完整文本替换该行。

在预处理器指令之后是 main() 函数的文档。每个函数，包括 main()，都必须有文档。未记录的代码通常价值不大，例外是自解释的代码。即便如此，尤其是在较大的程序中，记录至少程序逻辑的主要步骤通常也是有帮助的。

> **注意**
>
> EMBOSS 为函数文档使用标准格式（参见附录 D，*代码文档标准*）。目前，你只需要知道 @prog 标记用于记录 `main()` 函数。你已经在头文件文档中看到了 @source 和 @author。这些标记由一个程序读取，该程序解析源代码并自动生成发布到网络和 SRS 中的文档。

实际的源代码以 `main()` 函数开始。`int` 表示 `main()` 函数的类型为 `int`。换句话说，当调用 `helloworld` 时，它将向操作系统返回一个整数值。C 语言中的 `main()` 函数通常为 `int` 类型。

命令行必须可用，因此 `main` 必须包含它。这是在参数列表中使用 `int argc` 和 `char **argv` 来完成的。这是 C 语言中表达程序应将命令行上的任何输入读取为字符串数组的标准方式。`argc` 是参数的数量（命令行上由空白分隔的单词），而 `argv` 是字符串数组本身。

> **注意**
>
> 让我们假装 `helloworld` 接受一个参数（实际上不接受），并且是这样调用的：
>
> `helloworld "Print this message"`
>
> 那么 `argv[0]` 将具有值 "helloworld"，`argv[1]` 将具有值 "Print this message"，而 `argc` 的值为 "2"。

对 EMBOSS 库进行了三次调用：`embInit`、`ajFmtPrint` 和 `embExit`。EMBOSS 编程的一大优势是，你不需要编写自己的代码来处理命令行（`argv` 数组）；此功能已内置于函数 `embInit` 中。所有 EMBOSS 应用程序都必须调用此函数，它处理所有用户输入处理，并且必须在应用程序开始时立即执行。`embInit` 执行以下操作：

- 读取本地数据库定义
- 找到要使用的正确 ACD 文件（应用程序名称为 "helloworld"，因此它在 ACD 目录中查找 `helloworld.acd`）
- 读取 ACD 文件
- 处理命令行（它使用来自 `main` 的 `argc` 和 `argv`）

`embInit` 处理对用户的所有提示，以输入未在命令行中输入的值，包括对超出范围的值重新提示用户。如果我们的 ACD 文件更复杂，例如需要将序列作为输入和文件作为输出，那么在调用返回时，它将已读取序列并将其放在内存中的某个位置，并且还打开了输出文件。

ajFmtPrint 用于将文本打印到屏幕。ajFmtPrint 是 C stdio（标准输入/输出）库中 printf() C 函数的 EMBOSS 版本。embExit 调用一些内部清理和统计例程。
有关 C 编程的更多信息，请参见第 6.2 节“编程指南”。

## 2.2.5 集成（将应用程序添加到 EMBOSS）

在拥有 C 源代码和 ACD 文件后，必须在编译之前将应用程序添加到 myemboss（或 EMBOSS 本身）。myemboss 包含两个文件，都称为 Makefile.am，它们共同包含关于包中每个 C 源文件和 ACD 文件的信息。因此，要将 helloworld 添加到 myemboss，必须编辑这些文件。假设你已将 EMBOSS 的 CVS 版本检出到 /home/auser/emboss，你将拥有以下目录：
用于 C 源文件和可执行文件的“可执行文件目录”：

```
/home/auser/emboss/emboss/embassy/myemboss/src
```

用于 ACD 文件的“ACD 目录”：

```
/home/auser/emboss/emboss/embassy/myemboss/emboss_acd
```

你需要编辑的文件是：

```
/home/auser/emboss/emboss/embassy/myemboss/src/Makefile.am
/home/auser/emboss/emboss/embassy/myemboss/emboss_acd/Makefile.am
```

如果你要将应用程序添加到主 EMBOSS 包中，文件将是：

```
/home/auser/emboss/emboss/emboss/Makefile.am
/home/auser/emboss/emboss/emboss/acd/Makefile.am
```

可执行文件目录中的 Makefile.am 包含每个 C 源文件的信息。首先，必须将程序名称添加到 bin_PROGRAMS 列表中。这通常按字母顺序进行。以下为 EMBOSS 显示了编辑前后的阶段，但 myemboss 的编辑相同。

### 编辑前

```
bin_PROGRAMS = aaindexextract abiview acdc antigenic \
...
garnier geecee getorf helixturnhelix hmoment \
...
```

### 编辑后

```
bin_PROGRAMS = aaindexextract abiview acdc antigenic \
...
garnier geecee getorf helixturnhelix helloworld hmoment \
...
```

### 重要

编辑 Makefile.am 时，必须显式添加行延续字符 ('\\') 以将条目分成多行。

其次，必须将应用程序源文件添加到 SOURCES 部分。要添加的行具有以下一般语法：

```
ApplicationName_SOURCES = ApplicationName.c
```

其中 ApplicationName 是应用程序的名称。此行应按字母顺序添加。因此，文件的外观将如下所示。

### 编辑前

```
...
geecee_SOURCES = geecee.c
getorf_SOURCES = getorf.c
helixturnhelix_SOURCES = helixturnhelix.c
hmoment_SOURCES = hmoment.c
iep_SOURCES = iep.c
infoalign_SOURCES = infoalign.c
...
```

### 编辑后

```
...
geecee_SOURCES = geecee.c
getorf_SOURCES = getorf.c
helixturnhelix_SOURCES = helixturnhelix.c
helloworld_SOURCES = helloworld.c
hmoment_SOURCES = hmoment.c
iep_SOURCES = iep.c
infoalign_SOURCES = infoalign.c
...
```

ACD 目录中的 Makefile.am 包含每个 ACD 文件的信息。对此文件只需添加新 ACD 文件的名称。同样，通常按字母顺序进行。以下是主 EMBOSS 包中该文件的外观：

### 编辑前

```
pkgdata_DATA = codes.english \
    aaindexextract.acd abiview.acd ajbad.acd ajfeatest.acd ajtest.acd \
...
    garnier.acd geecee.acd getorf.acd helixturnhelix.acd hmoment.acd \
    histogrammtest.acd iep.acd infoalign.acd infoseq.acd isochore.acd \
    lindna.acd listor.acd \
    marscan.acd maskfeat.acd maskseq.acd \
    matcher.acd
```

### 编辑后

```
pkgdata_DATA = codes.english \
    aaindexextract.acd abiview.acd ajbad.acd ajfeatest.acd ajtest.acd \
...
    garnier.acd geecee.acd getorf.acd helixturnhelix.acd helloworld.acd \
    hmoment.acd histogrammtest.acd iep.acd infoalign.acd infoseq.acd \
    isochore.acd lindna.acd listor.acd \
    marscan.acd maskfeat.acd maskseq.acd \
    matcher.acd
```

同样，必须显式添加行延续字符 ('\\')。

## 2.2.6 编译

你可以从可执行文件目录 (.../myemboss/source) 输入以下命令之一来编译应用程序：

```
make helloworld
make
```

后一种选项可能较慢，因为在进行库更改时，有时需要编译所有内容。

GNU 工具将识别 Makefile.am 文件是否已编辑，并在发出 make 命令时重建 Makefile 文件。直接编辑 Makefile 文件本身是不良实践。

以下是在主 EMBOSS 包中编译 helloworld 的示例：

```
% pwd
/home/auser/emboss/emboss/emboss/
% make helloworld
/bin/sh ../libtool --tag=CC --mode=link gcc -O2 -Wall -fno-strict-aliasing -o
helloworld helloworld.o
../nucleus/libnucleus.la ../ajax/libajaxg.la ../ajax/libajax.la ../plplot/
libplplot.la -
L/usr/X11R6/lib
-lX11 -lm -lgd -lpng -lz -lm
gcc -O2 -Wall -fno-strict-aliasing -o .libs/helloworld helloworld.o
../nucleus/.libs/libnucleus.so
../ajax/.libs/libajaxg.so ../ajax/.libs/libajax.so ../plplot/.libs/libplplot.so-
L/usr/X11R6/lib -lX11
```





-lgd -lpng -lz -lm -Wl,--rpath-
Wl,/home/auser/emboss_test_installation_for_course/emboss/lib
creating helloworld
```

Finally, to run the program:

```
% helloworld
Prints 'Hello World!' to the screen.
Hello World!
%
```

### 2.2.7 调试

在此情况下不应需要调试，但较大的程序必然包含需要修复的错误，然后应用程序才能运行完成，甚至根本无法运行。调试在其他地方有更详细的介绍（第 3.3 节，“调试”）。

### 2.2.8 测试

彻底的测试是软件开发的重要组成部分。对于 EMBOSS，这包括由 EMBOSS 开发人员定期运行的正式质量保证测试，以确保应用程序按预期工作。如果你想贡献你的应用程序，你需要编写这些测试（参见第 7 章，质量保证）。

### 2.2.9 文档

你应确保 main() 函数有适当的文档，并且 C 源文件包含标准文档块。helloworld 非常简单，不需要除从源代码和 ACD 文件自动生成的基本内容之外的最终用户文档。

更复杂的程序应有完整的文档。这包括代码中的文档（参见附录 D，代码文档标准），例如用于数据类型和函数，以及最终用户文档（参见第 8 章，应用程序文档标准）用于整个应用程序。

## 2.3 修改 helloworld

EMBOSS 允许通过 ACD 语言对应用程序的命令行界面进行非常灵活的描述。在本节中，我们将更深入地了解编写 ACD 文件以及处理它们所需的代码。你将了解新的 ACD 数据类型和属性。

考虑这个简单的任务：

- 修改 helloworld 以在屏幕上打印用户定义的字符串，打印次数由用户定义。

### 2.3.1 修改 ACD 文件

要将硬编码字符串“Hello World!”替换为用户定义的字符串，你必须：

- 向 ACD 文件添加新的数据定义。你需要的 ACD 数据类型，不出所料，是字符串。还有许多其他类型可用（第 4.3 节，“数据定义”）。
- 为你的数据定义提供适当的标签。
- 为字符串提供默认值。你需要向字符串定义添加 default 属性，并设置合理的默认值 "Hello World!"（或其他内容）。

你的 ACD 文件现在应该类似于这样：

```
application: helloworld
[
    documentation: "Prints 'Hello World!' to the screen."
]
string: printme
[
    default: "Hello World!"
]
```

### 2.3.2 修改 C 源代码

要修改 C 源代码以支持用户定义的字符串，你需要：

- 定义适当的 AJAX 对象，即用于保存 ACD 字符串数据类型。
- 添加适当的 ajAcdGet* 函数（在此例中为 ajAcdGetString）以检索新 ACD 数据项的值。ajAcdGetString 的参数必须与 ACD 文件中的数据标签相同。
- 调用函数将字符串打印到屏幕。
- 注释掉（或删除）现有的硬编码 ajFmtPrint 语句。
- 干净地退出；记得释放字符串对象（通过调用 ajStrDel），该对象已由 ajAcdGetString（间接地）分配。

你的源代码现在将类似于：

```
#include <stdio.h>
int main(void)
{
    AjPStr printme=NULL;
    printme = ajAcdGetString("printme");
    ajFmtPrint("%S\n", printme);
    ajStrDel(&printme);
    embExit();
    return 0;
}
```

你可以看到，ajFmtPrint 与转换说明符（%S）一起用于打印 EMBOSS 字符串。

**注意**

ajFmtPrint 和 C 等效函数（printf()）都使用 _转换说明符_，它们控制函数的参数在打印时如何被解释。转换说明符由百分号（%）后跟一个字符组成。例如，有符号十进制整数变量使用转换 %d 进行打印转换，字符串使用转换 %s 正确格式化。ajFmtPrint 支持其他 AJAX 数据类型，包括布尔值（%B）、日期（%D）和 AJAX 字符串（%S）等。（参见第 5.1 节，“基本数据类型”）

### 2.3.3 运行程序

运行程序时，你应该得到类似这样的输出：

```
% helloworld
My first EMBOSS program
Hello World!
```

显然，它正在使用默认值。但是，字符串可以是 _用户定义的_，你只需在调用程序时在命令行上指定适当的 _限定符_（数据项的标签，本例中为 printme）和关联的字符串值即可：

```
% helloworld -printme "Hello Sailor!"
My first EMBOSS program
Hello Sailor!
```

作为最后的修饰，向应用程序定义添加 groups: 属性，以将你的应用程序分配到功能组。查看有效组名称列表（第 4.2.4.1 节，“应用程序组名称文件 (groups.standard)”）。这将使用户更容易找到它。

另外，添加一行注释（以 # 开头），给出 ACD 文件最后编辑的日期。application: 定义现在应该类似于这样：

```
application: helloworld
[
    documentation: "Prints 'Hello World!' to the screen."
    groups: "Test"
###   Last edited 2007.
]
```

### 2.3.4 限定符和参数

不得不使用 -printme 选项有点麻烦，如果你能在不知道标签名称的情况下指定要打印的文本，那将很好。为此，你使用 parameter: 属性。如果数据项使用 parameter: 定义，则在命令行上使用标志不是强制性的，也就是说，你可以直接输入：

```
helloworld "Hello Sailor!"
```

要将字符串定义为参数，请向 ACD 字符串定义添加以下内容：

```
parameter: "Y"
```

如果需要，你仍然可以使用限定符名称，但这不是强制性的。

### 2.3.5 添加整数

下一个任务是向 ACD 文件添加整数数据项，以控制用户定义的字符串在屏幕上打印的次数。要添加整数，你需要重复添加字符串时经历的步骤。

你的 ACD 文件将包含以下数据定义：

```
integer:n
[
    default: "1"
]
```

C 代码需要修改为类似这样的内容：

```
#include "emboss.h"
int main(void)
{
    AjPStr printme = NULL;
    ajint n = 0;
    printme = ajAcdGetString("printme");
    n = ajAcdGetInt("n");
    while(n)
    {
        ajFmtPrint("%S\n", printme);
        n--;
    }
    ajStrDel(&printme);
    embExit();
    return 0;
}
```

你会注意到，新整数没有调用析构函数。这是因为 ajint 是基本 AJAX 数据类型，而不是对象（C 数据结构），因此不需要显式内存管理。有关编程基本类型（第 5.1 节，“基本数据类型”）和对象（第 5.3 节，“对象（C 数据结构）”）的更多信息，请参见其他部分。

### 2.3.6 重新探讨参数和限定符

暂时不要将整数设为参数——尝试使用不同的命令行调用 **helloworld**。你应该注意，参数是否在新整数的限定符之前或之后并不重要。换句话说，你可以这样调用应用程序：

```
helloworld -n 10 "Hello Sailor!"
```

或者这样：

```
helloworld "Hello Sailor!" -n 10
```

现在，在 ACD 文件中将整数设为参数。再次尝试调用 **helloworld**。你会发现参数的顺序很重要——它们必须与 ACD 文件中使用的顺序一致！

例如，如果你的 ACD 文件如下所示：

```
application: helloworld
[
    documentation: "Prints a user-defined string to the screen."
]
string: printme
[
    parameter: "Y"
    default: "Hello World!"
]
integer: n
[
    parameter: "Y"
    default: "1"
]
```

你可以这样调用程序：

```
helloworld "Hello Sailor!" 10
```

但不能这样：

```
helloworld 10 "Hello Sailor!"
```

参数必须按照它们在 ACD 文件中定义的顺序出现在命令行上。





## 2.4 修改 matcher

The EMBOSS application **matcher** generates pairwise local alignments given either DNA or protein sequences. It has different options depending on the type of input. When wrapping such programs, for instance for incorporation into a graphical user interface, it is often convenient to split them into separate nucleotide and protein applications with the same application code underneath. SRS is a good example of a system which wraps EMBOSS applications in this way.

EMBOSS 应用程序 **matcher** 可根据 DNA 或蛋白质序列生成成对局部比对。它根据输入类型提供不同的选项。在封装此类程序时，例如将其集成到图形用户界面中，通常将其拆分为独立的核苷酸和蛋白质应用程序（底层使用相同的应用程序代码）会很方便。SRS 是以这种方式封装 EMBOSS 应用程序的系统的一个良好示例。

To deepen your knowledge, use **matcher** as a template to produce new, separate applications for protein (**matcherpro**) and nucleotide (**matchernuc**) sequences.

为加深您的了解，请使用 **matcher** 作为模板，为蛋白质（**matcherpro**）和核苷酸（**matchernuc**）序列生成新的独立应用程序。

### 2.4.1 Planning

You need to change how the **matcher** functionality is presented to the user, therefore you'll need two new ACD files and a copy of the **matcher** source code for each. Both new applications will effectively use the _same_ source code with only trivial differences.

您需要更改向用户展示 **matcher** 功能的方式，因此需要为每个应用程序创建两个新的 ACD 文件和 **matcher** 源代码的副本。这两个新应用程序将实际使用 _相同_ 的源代码，只有微小的差异。

The steps to create these applications are as follows:

创建这些应用程序的步骤如下：

- 1. Create the application source code (`matcherpro.c` and `matchernuc.c` files) in:

```
../embassy/myemboss/src
```

Copy the source code for **matcher** from `../emboss/matcher.c`.

- 1. 在以下位置创建应用程序源代码（`matcherpro.c` 和 `matchernuc.c` 文件）：

```
../embassy/myemboss/src
```

从 `../emboss/matcher.c` 复制 **matcher** 的源代码。

- 2. Create the application ACD files (`matcherpro.acd` and `matchernuc.acd`) in:

```
../embassy/myemboss/emboss_acd
```

Use `../emboss/matcher.acd` as a template.

- 2. 在以下位置创建应用程序 ACD 文件（`matcherpro.acd` 和 `matchernuc.acd`）：

```
../embassy/myemboss/emboss_acd
```

使用 `../emboss/matcher.acd` 作为模板。

- 3. Add the applications to the **myemboss** package by updating the two `Makefile.am` files:

```
../embassy/myemboss/src/Makefile.am
../embassy/myemboss/emboss_acd/Makefile.am
```

- 3. 通过更新两个 `Makefile.am` 文件将应用程序添加到 **myemboss** 包中：

```
../embassy/myemboss/src/Makefile.am
../embassy/myemboss/emboss_acd/Makefile.am
```

- 4. Compile and test the applications.

- 4. 编译并测试应用程序。

### 2.4.2 Editing the ACD files

The original `matcher.acd` is shown below (help: attributes are not shown):

```
application: matcher [
 documentation: "Waterman-Eggert local alignment of two sequences"
 groups: "Alignment:Local"
]

section: input [
    information: "Input section"
    type: "page"
]

sequence: asequence [
    parameter: "Y"
    type: "any"
]

sequence: bsequence [
    parameter: "Y"
    type: "@($(acdprotein) ? stopprotein : nucleotide)"
]

matrix: datafile [
    additional: "Y"
    information: "Matrix file"
    protein: "$(acdprotein)"
]

endsection: input

section: additional [
    information: "Additional section"
    type: "page"
]

integer: alternatives [
    additional: "Y"
    information: "Number of alternative matches"
    default: "1"
    minimum: "1"
]

integer: gapopen [
    additional: "Y"
    information: "Gap penalty"
    default: "@($(acdprotein)? 14 : 16)"
    minimum: "0"
    valid: "Positive integer"
    expected: "14 for protein, 16 for nucleic"
]

integer: gapextend [
    additional: "Y"
    information: "Gap length penalty"
    default: "@($(acdprotein)? 4 : 4)"
    minimum: "0"
    valid: "Positive integer"
    expected: "4 for any sequence"
]

endsection: additional

section: output [
	information: "Output section"
	type: "page"
]

align: outfile [
	parameter: "Y"
	aformat: "markx0"
	minseqs: "2"
	maxseqs: "2"
]

endsection: output
```

The ACD file introduces several new concepts:

ACD 文件引入了几个新概念：

- The groups: attribute in the application definition assigns the application to a group (see Section 4.2, ‘Application definition’).

- 应用程序定义中的 groups: 属性将应用程序分配到一个组（参见第 4.2 节“应用程序定义”）。

- The sequence ACD datatype is used to define two input sequences; asequence and bsequence.

- sequence ACD 数据类型用于定义两个输入序列；asequence 和 bsequence。

- The sequence type of asequence is set by the type: attribute, in this case to “any”, i.e. any type of sequence is acceptable.

- asequence 的序列类型由 type: 属性设置，在此情况下设置为“any”，即可接受任何类型的序列。

- For bsequence, the sequence type is calculated from the ACD variable acdprotein; if acdprotein is true then type: is set to stopprotein, otherwise it’s set to nucleotide.

- 对于 bsequence，序列类型是根据 ACD 变量 acdprotein 计算的；如果 acdprotein 为 true，则 type: 设置为 stopprotein，否则设置为 nucleotide。

- acdprotein is an ‘automatic ACD variable’ with a boolean type whose value is set automatically when the first sequence is read in. So, if the first sequence is a protein, then acdprotein will be true. Automatic ACD variables are described in detail elsewhere (Section 4.4, ‘Operations’).

- acdprotein 是一个带有布尔类型的“自动 ACD 变量”，其值在读取第一个序列时自动设置。因此，如果第一个序列是蛋白质，则 acdprotein 将为 true。自动 ACD 变量在其他地方详细描述（第 4.4 节“操作”）。

- The matrix datatype is used to define a substitution matrix (called matrixfile). EMBOSS will search for this data file in the EMBOSS data directory (see the EMBOSS User’s Guide).

- matrix 数据类型用于定义替换矩阵（称为 matrixfile）。EMBOSS 将在 EMBOSS 数据目录中搜索此数据文件（参见 EMBOSS 用户指南）。

- information: is used to set a user-prompt for some of the data items. It is not needed for the sequence inputs (EMBOSS will automatically generate a suitable prompt) but can be given for the other types used (see Section 4.3, ‘Data definition’).

- information: 用于为某些数据项设置用户提示。对于序列输入不需要此项（EMBOSS 会自动生成合适的提示），但可以为其他使用的类型提供（参见第 4.3 节“数据定义”）。

- Qualifiers and parameters in the ACD file are organised into sections (input, additional and output). These help to tidy the ACD file and are exploited by user interfaces (see Section 4.3, ‘Data definition’).

- ACD 文件中的限定符和参数被组织成各个部分（input、additional 和 output）。这些部分有助于整理 ACD 文件，并被用户界面利用（参见第 4.3 节“数据定义”）。

- Options in the additional section are defined to be ‘additional qualifiers’ by the attribute additional: "Y". Values for additional qualifiers are not prompted for (the default value will be used instead) unless -options is given on the command line, which will turn prompting on for these qualifiers (see Section 4.1, ‘Introduction to ACD file development’).

- additional 部分中的选项通过属性 additional: "Y" 被定义为“附加限定符”。除非在命令行中给出 -options（这将为这些限定符打开提示），否则不会提示输入附加限定符的值（将改用默认值）（参见第 4.1 节“ACD 文件开发简介”）。

- Two gap penalties (gapopen and gapextend) are defined as integer ACD types. The minimum:, valid: and expected: attributes are used to set minimum and expected values and a corresponding message to the user.

- 两个间隙罚分（gapopen 和 gapextend）被定义为整数 ACD 类型。minimum:、valid: 和 expected: 属性用于设置最小值和预期值以及向用户显示的相应消息。

## 2.4 修改 matcher

There is a single output, a sequence alignment (outfile) which is defined by the type align. The format (markx0) and minimum and maximum number of sequences (2 in both cases, i.e. a pairwise alignment) are set using the attributes aformat:, minseqs: and maxseqs respectively.

只有一个输出，即序列比对（outfile），由 align 类型定义。格式（markx0）以及最小和最大序列数（两者均为 2，即成对比对）分别使用 aformat:、minseqs: 和 maxseqs 属性设置。

The changes necessary for matcherpro.acd are:

matcherpro.acd 所需的更改如下：

- The application name should be changed to matcherpro.

- 应用程序名称应更改为 matcherpro。

- The documentation: attribute should state that the application works on protein sequences only.

- documentation: 属性应说明该应用程序仅适用于蛋白质序列。

- The type: attribute of the first input sequence should be changed from any to protein.

- 第一个输入序列的 type: 属性应从 any 更改为 protein。

- The type of the second input sequence should be stopprotein.

- 第二个输入序列的类型应为 stopprotein。

- The residue substitution matrix should be of type protein. Currently this is given as protein: "$(acdprotein)" which means that the protein: attribute will be set to true if the first sequence is a protein. $(acdprotein) should be replaced with y.

- 残基替换矩阵应为 protein 类型。目前此项设置为 protein: "$(acdprotein)"，这意味着如果第一个序列是蛋白质，则 protein: 属性将设置为 true。应将 $(acdprotein) 替换为 y。

- All other occurrences of lines containing acdprotein should be replaced as appropriate (see below).

- 包含 acdprotein 的所有其他行出现应根据需要替换（见下文）。

The parts of matcherpro.acd which have been modified and differ from matcher.acd are shown below:

matcherpro.acd 中已修改且与 matcher.acd 不同的部分如下所示：

```
application: matcherpro [
documentation: "Waterman-Eggert local alignment of two sequences"
groups: "Alignment:Local"
]
... lines omitted

sequence: asequence [
parameter: "Y"
type: "protein"
]

sequence: bsequence [
parameter: "Y"
type: "stopprotein"
]

... lines omitted

matrix: datafile [
additional: "Y"
information: "Matrix file"
protein: "Y"
]

... lines omitted

integer: gapopen [
additional: "Y"
information: "Gap penalty"
default: "14"
minimum: "0"
valid: "Positive integer"
expected: "14"
]

integer: gapextend [
additional: "Y"
information: "Gap length penalty"
default: "4"
minimum: "0"
valid: "Positive integer"
expected: "4 for any sequence"

]
... lines omitted
```

### 2.4.3 Editing the C source file

The main() function for matcher is shown below. The application includes several functions and macros that are not shown:

```
#include "emboss.h"
/* @prog matcher **********************************************************
**
** Finds the best local alignments between two sequences
**
***********************************************************************/

int main(int argc, char **argv)
{
    AjPStr aa0str = 0;
    AjPStr aalstr = 0;
    const char *s1;
    const char *s2;
    ajint gdelval;
    ajint ggapval;
    ajint i;
    ajint K;

    AjPAlign align = NULL;

    embInit("matcher", argc, argv);

    seq = ajAcdGetSeq("asequence");
    ajSeqTrim(seq);
    seq2 = ajAcdGetSeq("bsequence");
    ajSeqTrim(seq2);
    matrix = ajAcdGetMatrix("datafile");
    K = ajAcdGetInt("alternatives");
    gdelval = ajAcdGetInt("gapopen");
    ggapval = ajAcdGetInt("gapextend");
    align = ajAcdGetAlign("outfile");

    /*
    create sequence indices. i.e. A->0, B->1 ... Z->25 etc.
    This is done so that ajBasecodeToInt has only to be done once for
    each residue in the sequence
```



```c
ajSeqFmtUpper(seq);
ajSeqFmtUpper(seq2);

s1 = ajStrGetPtr(ajSeqGetSeqS(seq));
s2 = ajStrGetPtr(ajSeqGetSeqS(seq2));

sub = ajMatrixGetMatrix(matrix);
cvt = ajMatrixGetCvt(matrix);

aa0str = ajStrNewRes(2+ajSeqGetLen(seq)); /* length + blank + trailing null */
aa1str = ajStrNewRes(2+ajSeqGetLen(seq2));
ajStrAppendK(&aa0str, '');
ajStrAppendK(&aa1str, '');

for(i=0;i<ajSeqGetLen(seq);i++)
	ajStrAppendK(&aa0str,(char)ajSeqcvtGetCodeK(cvt, *s1++));

for(i=0;i<ajSeqGetLen(seq2);i++)
	ajStrAppendK(&aa1str,ajSeqcvtGetCodeK(cvt, *s2++));

matcher_Sim(align, ajStrGetPtr(aa0str),ajStrGetPtr(aa1str),
	seq,seq2,
	K,(gdelval-ggapval),ggapval,
	ajSeqGetOffset(seq), ajSeqGetOffset(seq2), 2);

ajStrDel(&aa0str);
ajStrDel(&aa1str);

ajSeqDel(&seq);
ajSeqDel(&seq2);

embExit();

return 0;
}
```

matcher.c introduces many new concepts:

- Two AJAX strings (aa0str and aa1str) are defined using AjPStr.
- An alignment object (align) is created using AjPAlign.
- The values from the ACD file are picked up by calls beginning with ajAcdGet. The functions are named to make the types returned obvious: ajAcdGetSeq returns sequences, ajAcdGetMatrix returns a matrix and so on.
- The next block of code creates the sequences indices. You needn't concern yourself with the details. Functions for this include ajMatrixGetMatrix, ajMatrixGetCvt and ajSeqcvtGetCodeK. The function matcher_Sim (not shown) is also called and is a function local to matcher.
- Strings and sequences that were allocated are freed by calling ajStrDel and ajSeqDel.
- The application then exits cleanly by calling embExit.

One small edit is needed in the `src/matcherpro.c` file:

- Change the `embInit` call to `embInitP` (which is used for EMBASSY packages) and add `"myemboss"` as the last argument so EMBOSS knows you are in the **myemboss** package
- Change the program name in the `embInitP` call to `"matcherpro"` so that it uses the new ACD file.
- Change the program name in the main function comment call to `"matcherpro"` to match the program name.

The parts of `matcherpro.c` which have been modified and differ from `matcher.c` are shown below:

```c
/* @prog matcher ************************************************************************************************
embInitP("matcherpro", argc, argv, "myemboss");
```

## 2.4.4 Compilation

To compile and install the application from the **myemboss** directory, type:

```
make
```

Or, if you are using **myemboss** as part of a fully installed EMBOSS system then type:

```
make install
```

## 2.4.5 Testing all is well

**matcherpro** has just been added to your system, therefore you may need to make it visible in your path, for example, by running the UNIX command `rehash`, if you use a `csh` shell. To check all is well, you can run:

```
acdvalid matcherpro
```

and check that no errors or warnings are reported. As `matcher.acd` has already been validated it should be fine.

You should now have a new application **matcherpro** which should produce the same results as **matcher** with protein input, but will refuse to run with DNA sequences. This is shown below:

```
% matcherpro
Finds the best local alignments between two protein sequences
Input protein sequence: embl:L07770
Error: Sequence is not a protein

Error: Unable to read sequence 'embl:L07770'
Input protein sequence:
...
```

Here it is being used correctly:

```
% matcherpro
Finds the best local alignments between two protein sequences
Input protein sequence: swissprot:UBR5_RAT
Second protein sequence:
...
```

## 2.4.6 Further developments

From the above it should be obvious what's required to implement matchernuc.acd and matchernuc.c, so generating two distinct applications, one for nucleotide and one for protein sequences.

If you are familiar with EMBOSS, you might notice that the output format of matcherpro is not the same as water, another popular alignment program. This could be confusing to users, so as a final modification you can make matcherpro consistent with water. To do this, set the aformat : attribute of the outfile data definition, which currently has the value "markx0" to the value ("srspair") defined in the water.acd file.

A similar effect could be achieved by running matcherpro with -aformat srspair on the command line. If for some reason the old format was required, matcherpro could be run with -aformat markx0 on the command line.

## 2.5 String handling

EMBOSS has a wide range of string handling functions. All of them start with the prefix ajStr and are defined in the ajstr.c source file. You'll practice using a few of them here by writing a new application that prompts the user for one or more strings, processes them, and writes the results to a plain text output file. This builds upon the string handling code used when modifying helloworld.

### 2.5.1 stringplay.acd

To begin, create an ACD file for a new application. We'll call the latter stringplay. The steps are as follows:

- Create the ACD file myemboss/emboss_acd/stringplay.acd
- Add an application: definition with documentation: and group: attributes
- Add one or more string: definitions with appropriate default:, information: and help: attributes
- An output file is needed, so add an outfile ACD data definition
- Test the file by running `acdc stringplay`
- Fix any warning or error messages generated by `acdc`
- Run `make` to compile the application and `make install` (depending on your installation) in the emboss_acd directory (or above) to install this file.

The ACD file might look something like this:

```
application: stringplay
[
    documentation: "An application for experimenting with basic string handling."
    groups: "Test"
]

string: astring
[
    parameter: "Y"
    default: "ParameterString"
    information: "First input string (parameter)"
    help: "This string is a parameter meaning you needn't specify the label (-astring) on the command line when specifying a value for it."
]

string: bstring
[
    standard: "Y"
    default: "StandardString"
    information: "Second input string (standard qualifier)"
    help: "This string is a standard qualifier meaning it will be prompted for if not specified on the command line."
]

string: cstring
[
    additional: "Y"
    default: "AdditionalString"
    information: "Third input string (additional qualifier)"
    help: "This string is a additional qualifier meaning it will only be prompted for if -options is given on the command line."
]

string: dstring
[
    default: "AdvancedString"
    information: "Fourth input string (advanced qualifier)"
    help: "This string is an advanced qualifier meaning it will never be prompted for."
]

outfile: outfile
[
    parameter: "Y"
]
```

You can use `acd stringplay` to test the ACD file. `acdc` will 'run' it exactly as if the application source code existed. It will prompt for any string inputs, assuming you defined them with `parameter:` or `standard:` attributes in the ACD file.

If you defined any strings with the additional : attribute then they will be prompted for only if you specify -options on the command line when you run stringplay. If you didn't specify parameter:, standard: or additional: then they will default to being an advanced qualifier and will never be prompted for.

Regardless of how you define the string inputs, they can be set on the command line by using e.g.:

```
-astring StringValue
```

where -astring is the label of the data definition and StringValue is the value of the string to set.

If you define the strings with parameter: then the flag (-astring) is optional, although values for parameters must be given in the order they appear in the ACD file.

It is also usually sensible to define a default value with the default: attribute. For additional and advanced qualifiers a default value is essential.

You should experiment by running acdc stringplay using the above ACD file, specifying values on the command line with and without any data labels.

### 2.5.2 stringplay.c

The C source code (myemboss/src/stringplay.c) must declare variables to hold all the strings and the output file from the ACD file. It must also pick up the values from the ACD file. At a minimum, the application should write the strings to the output file. It should then close the output file and exit cleanly.

If you are using the stringplay.acd shown above then the C source code should look something like this:

```c
#include "emboss.h"
int main (int argc, char* argv[])
{
    AjPStr astring = NULL;
    AjPStr bstring = NULL;
    AjPStr cstring = NULL;
    AjPStr dstring = NULL;

    AjPFile outf = NULL;
    embInitP("stringplay", argc, argv, "myemboss");
    astring = ajAcdGetString("astring");
    bstring = ajAcdGetString("bstring");
    cstring = ajAcdGetString("cstring");
    dstring = ajAcdGetString("dstring");
    outf = ajAcdGetOutfile("outfile");

    /* functional part of code would go here */
    ajFmtPrintF(outf, "astring: %S\nbstring: %S\ncstring: %S\ndstring: %S\n",
                astring, bstring, cstring, dstring);

    ajFileClose(&outf);
    ajStrDel(&astring);
    ajStrDel(&bstring);
```



ajStrDel(&cstring);
ajStrDel(&dstring);

embExit();
return 0;
}

## 2.5.3 编译与测试

要编译您的程序，请从 myemboss 目录下执行以下命令：

```
make
```

如果您将 myemboss 用作已完整安装的 EMBOSS 系统的一部分，请使用以下命令安装：

```
make install
```

## 2.5.4 添加功能

EMBOSS 字符串处理库非常庞大。您可以查看 ajstr.h 和 ajstr.c 来了解可用内容。为方便起见，函数被组织成若干部分，包括赋值、组合、剪切、替换、查询、元素检索、格式化、比较等。下面仅展示了这些类别中的少数几个函数：

```
/** A string "assignment" function to copy a string to a string. */
AjBool ajStrAssignS(AjPStr* Pstr, const AjPStr str);

/** A string "combination" function which appends a strings */
AjBool ajStrAppendS(AjPStr* Pstr, const AjPStr str);

/** A string "combination" function which inserts a text string into a
string at a specified position. */
AjBool ajStrInsertS (AjPStr* pthis, ajint pos, const AjPStr str);

/** A string "cut" function which removes a substring from a string. */
AjBool ajStrCutRange(AjPStr* Pstr, ajint pos1, ajint pos2);

/** A string "cut" function which removes the end from a string
reducing it to a defined length. */
AjBool ajStrTruncateLen(AjPStr* Pstr, size_t len);

/** A string "substitution" function which reverses the order of characters
in a string. */
AjBool ajStrReverse(AjPStr* Pstr);
```

/* A string "query" function which counts occurrences of a character in a string. */
ajint ajStrCalcCountK(const AjPStr str, char chr);

/* A string "element retrieval" function which returns a single
character at a given position from a string. */
char ajStrGetCharPos(const AjPStr str, ajint pos);

/* A string "formatting" function which converts a string to upper case. */
AjBool ajStrFmtUpper(AjPStr* Pstr);
/* A string "comparison" function which is a simple test for matching
two strings. */
AjBool ajStrMatchS (const AjPStr this, const AjPStr str);

/* A string "comparison" to test for matching the start of a string against a
given prefix string. */
AjBool ajStrPrefixS(const AjPStr str, const AjPStr str2);

/* A string "comparison" function to find the first occurrence in a string of a
second string. */
ajint ajStrFindS (const AjPStr str, const AjPStr str2);

许多函数返回 AjBool。这可能指示函数是否重新分配了内存、是否成功、测试是否为真等等。确切含义请参阅 ajstr.c 中的文档。

AjPStr* Pstr 表示由函数修改（或可能修改）的字符串参数。参数前的 const 表示具有常量值的变量。因此，此处 const AjPStr str 表示由函数使用但不修改的字符串参数；该指针不能由函数重新分配。

下面举几个例子来说明如何调用某些字符串函数。首先，ajStrAssignS 用于将现有字符串赋值给新字符串。该函数应在构造 newstr 之后调用。newstr 会被修改，因此需要 newstr 的地址：

```
ajStrAssignS(&newstr, astr);
```

这里 ajStrFmtUpper 用于将字符串转换为大写。同样，需要字符串的地址：

```
ajStrFmtUpper(&astring);
```

这里比较两个字符串，如果相同则执行某些操作：

```
if(ajStrMatchS(astr, bstring))
{ /* Do something */ }
```

## 2.5.4.1 字符串内存管理

最佳实践是在使用每个字符串之前显式构造它（分配内存），并在用完后销毁它（释放内存）。默认构造函数

# 2 您的第一个 EMBOSS 应用程序

函数（ajStrNew）和析构函数（ajStrDel）为此目的提供。

用法如下所示：

```c
/* newstr is NULL, no memory is allocated */
AjPStr newstr=NULL;

/* newstr now points to a string object in memory and is ready for use by
our program */
newstr = ajStrNew();

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&newstr);
```

对于 ACD 变量，您无需调用构造函数，因为 embInitP 调用已为这些变量分配内存。如果您这样做，存在内存错误的风险。在下面这段相当牵强且存在错误的代码中，ajAcdGetString 的调用将覆盖由（不必要的）ajStrNewC 调用分配并返回的内存指针：

```c
/* This code is bugged */
AjPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* newstr now points to a string object in memory */
astring = ajStrNewC("Hello");

/* this call will break the handle to the memory allocated by ajStrNewC */
astring = ajAcdGetString("astring");
```

正确的代码是：

```c
AjPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* Get a string value from ACD */
astring = ajAcdGetString("astring");

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&astring);
```

embInitP 创建了一个字符串对象，在用完后必须释放它。这就是 ajStrDel(&astring); 调用的用途。

# EMBOSS 下的软件开发

### 3.1 EMBOSS 编程

#### 3.1.1 简介

EMBOSS 下的软件开发和维护变得简单。EMBOSS 具有强大的内置功能，任何本地应用程序都可以无需或只需少量额外编码即可使用，从而为您节省大量精力。它包含用于扩展核心功能和开发新应用程序的广泛 C 编程库。针对质量保证测试、安装、维护和支持等关键方面，已建立明确的流程。一般方面由 EMBOSS 开发人员处理，留给您支持特定于您自身软件的部分。

#### 3.1.2 内置功能

主要内置功能领域包括：

- 生物数据类型支持
- 常见文件格式支持
- 简单数据库配置
- 命令行处理
- 命令行限定符
- 序列和序列特征规范。

#### 3.1.2.1 生物数据类型支持

EMBOSS 支持多种标准和生物数据类型（第 4.3 节“数据定义”）。应用程序输入和输出的数据类型在 AJAX 命令定义（ACD）文件中定义。数据类型属性允许以更详细的方式指定输入或输出，例如通过设置默认值或定义输入序列的允许类型。计算属性（例如输入序列的长度）在读取数据后、在应用程序正式启动之前可用，从而允许在 ACD 文件中进行进一步的精细控制。

#### 3.1.2.2 常见文件格式支持

EMBOSS 支持用于输入和输出的多种文件格式。生物序列可以使用所有常见格式进行读取和写入。EMBOSS 会自动检测输入序列的格式，但也可以为提高效率而指定格式。序列特征、比对、数据文件等许多其他格式也会自动处理。您编写的任何应用程序也将自动支持这些格式。此外，当向 EMBOSS 添加新的输入和输出数据格式时，您的应用程序将自动能够使用它们；无需更改应用程序代码。有关支持的文件格式的信息，请参阅 _EMBOSS 用户指南_。

#### 3.1.2.3 简单数据库配置

数据库配置简单灵活。支持多种数据库（可以包括远程数据服务器）和多种访问方法。新数据库和访问方法可以轻松添加。有关更多信息，请参阅 _EMBOSS 管理员指南_。

#### 3.1.2.4 命令行处理

您的应用程序将使用 EMBOSS 命令行，该命令行在各应用程序中保持一致。ACD 文件定义了所有应用程序选项的数据类型和允许值。ACD 文件和命令行上的所有输入在启动时（在应用程序正式启动之前）都会进行验证。命令行行为（例如生成合理的提示并针对超出范围的值重新提示）会自动处理。

#### 3.1.2.5 命令行限定符

EMBOSS 包含各种命令行限定符，这些限定符通常不在 ACD 文件中设置。这些包括 _全局限定符_ 和各种 _数据类型特定限定符_。全局限定符可供所有应用程序使用并控制一般应用程序行为。数据类型特定限定符用于更详细地指定特定输入和输出，例如序列。

#### 3.1.2.6 序列和序列特征规范

序列在命令行中通过其统一序列地址（USA）引用，这是定义序列数据位置和格式的一种强大且灵活的规范。同样，序列特征使用统一特征对象（UFO）定义。您编写的任何应用程序都将自动支持 USA 和 UFO。有关更多信息，请参阅 _EMBOSS 用户指南_。

#### 3.1.3 开发基本步骤

软件不仅仅是编码，尤其是为广泛分发并部署在生产环境中的 EMBOSS 开发时。所有要集成到包中的代码都必须在其整个生命周期内进行测试、文档化和管理。无论您打算开发库还是新应用程序，许多步骤都是相同的：



- 1. 项目管理
- 2. 规划
- 3. ACD 文件开发（仅限应用程序）
- 4. C 源代码开发
- 5. 集成与编译
- 6. 调试
- 7. 质量保证测试
- 8. 文档编写
- 9. 分发
- 10. 维护、支持与培训。

在开始项目之前，值得熟悉以下所述步骤。这应能帮助你有效规划软件、高效开发并按时交付项目。

## 3.1.4 项目管理

所有软件始于一个想法，最终以软件退役告终。了解所涉及的步骤将帮助开发者避免一路上的陷阱和问题，或至少做好准备，从而节省大量时间和精力。然而，许多项目在缺乏这种前瞻性的情况下就启动了，尤其是那些急于开始编码的程序员。

### 3.1.4.1 发布软件的模型

EMBOSS 每年在圣斯威辛节（7 月 15 日）发布一个主要版本。版本号通常，但不总是，每年增加 1。其他版本在中间期间根据需要发布。EMBASSY 包没有固定的发布日期或正式的版本编号方案。为避免混淆，包装第三方软件的 EMBASSY 包的版本号设置为与被包装软件的版本号相同。单个 EMBOSS 或 EMBASSY 应用程序没有自己的版本阶段或编号。新程序会在 EMBOSS 邮件列表上公布，以征求用户反馈。

你应该为软件的开发和发布确定一个通用模型。没有一种模型被普遍采用；然而，所有项目都从编码开始前的预开发阶段开始，随后是一个或多个反映代码成熟度的软件版本。以下阶段是典型的：

- 1. 预开发
- 2. 预 Alpha
- 3. Alpha
- 4. Beta
- 5. 发布候选版
- 6. 发布。

在实践中，通常并非每个阶段都有对应的正式软件发布。例如，用户可能只看到测试版和最终发布版。尽管如此，牢记这些阶段仍然有帮助，因为这有助于管理用户的期望。不言而喻，例如，广泛分发未在测试版中充分测试的代码是愚蠢的。在实践中，早期版本通常包含许多错误，因此人们通常会对软件保持警惕，直到它经过数月甚至数年的成熟。

### 预开发

预开发阶段发生在编码开始之前。会指定需求，并规划软件整个生命周期内的预期工作。

### 预 Alpha

预 Alpha 软件仍处于活跃的设计和开发中。通常它是可能最终发布的版本的原型。从用户角度来看，预 Alpha 版本有助于了解即将推出的内容；从开发者角度来看，它提供了一种获取早期用户反馈的手段，以指导设计和开发。

### Alpha

Alpha 软件通常已相当完善，但尚未准备好进行公开发布。部署将非常有限，甚至没有部署。此类部署通常仅限于主要用户组或其他已知能提供良好反馈的特定用户组。通常，大多数主要功能将被实现，大多数主要错误将被修复，但仍会有许多缺失的次要功能、错误和其他问题。Alpha 版本可能是完全重写，也可能是预 Alpha 版本的演进。

### Beta

Beta 软件是第一个重要版本。其主要目的是让尽可能大的用户群对软件进行测试并征求反馈。Beta 软件可能并不完美。它可能在所有情况下都无法正常工作，但应该相对无错误。通常，已知的大多数（如果不是全部）主要错误都应修复。

### 发布候选版

发布候选版是 Beta 版本的改进版，其中所有已知错误都已修复。如果在 Beta 测试期间被大量请求，它可能包含几个新功能，但这些功能不应偏离其基本功能太远。此类重大请求理应（最好）更早被捕获。主要功能现在已“冻结”，从这一点开始，只实现错误修复或次要新功能。发布候选版可以被视为测试版本与部署版本之间的中间状态。发布候选版应由开发者进行大量测试，并在实际用例场景中进行测试。

### 发布

发布版软件已完全开发和测试，应准备好供用户正式使用。它是源自发布候选版测试和改进的软件最终版本。发布版通常会有一个版本号，例如，Version 1.0。

### 3.1.4.2 软件生命周期模型

EMBOSS 开发者使用“代码与修复”和“同步与稳定”模型的组合（见下文）。这已被证明是让用户满意的最务实方式，尤其是在平衡新功能需求与整个包的稳定性和一致性需求方面。

一般做法是在报告错误后尽快修复，并根据需要提供错误修复文件（参见 _EMBOSS 用户指南_）。新功能或应用程序在与用户紧密合作下开发，通常按需求进行，并按计划开发和发布。这会尽可能及时地完成，以便修复所有错误并解决重大问题。所有无法立即实现的错误修复和功能请求都会记录在 SourceForge 网站上（参见第 1.5 节，“向 EMBOSS 贡献软件”）。这样，即使无法立即采取行动，有价值的贡献也不会丢失。

已出现许多软件生命周期模型，所有模型都倾向于关注开发过程本身。它们如下总结。由你决定采用哪一种模型（或其他模型），以最符合你的需求和情况。

### 代码与修复模型

最简单的模型是循环进行编码和错误修复，直到软件适合用途：

- 1. 编写源代码
- 2. 编译并运行程序
- 3. 测试并发现错误
- 4. 修复错误。

### 瀑布模型

开发按一系列明确的管理或开发步骤线性进行。步骤后可能跟随测试，必须通过测试才能进入下一步。通常，只有在当前步骤中发现新问题时，才允许返回上一步。因此，开发以增量和逻辑的方式进行。然而，缺点是此类模型对需求变化相当不灵活。

### 螺旋模型

螺旋模型通过迭代开发周期试图解决瀑布模型的不灵活性。这引入了更多用户参与的机会，但缺点是该模型相当繁琐，因此在实践中难以坚持。每个周期有四个阶段：

- 1. 规格说明：识别用户需求、约束和可能的方法。
- 2. 评估：评估替代方法，通常通过开发原型软件。
- 3. 开发：详细设计代码，实现并测试。
- 4. 规划：根据用户反馈评估软件和下一周期的计划。

### 原型模型

原型模型通过在开发过程中引入明确的评估点，试图确保软件满足用户需求。在这些点上，用户通过演示或实际测试审查软件，通常是原型版本。被审查的软件可能是更大系统的一小部分。随着开发的进展，开发者倾向于自然地关注设计和实现问题，而用户则继续关注其需求。原型模型试图通过定期评估避免任何观点分歧。

### 快速应用开发

这是一种通用的软件开发方法，旨在摆脱不灵活的正式模型。通常，一系列原型由用户和开发者审查，以确保满足用户需求，并在持续开发中进行微调。每个阶段的分析、设计和实现通常限定在一定时间内。这种方法的缺点是，在缺乏前期正式设计说明的情况下，可能难以就项目何时完成达成一致，且软件可能以不可取或不可控的方式演变。

### 同步与稳定模型

该模型协调并行工作的多个开发者，试图快速生产出满足大部分需求的软件，并在后续版本中对其进行改进。它依赖于频繁的代码提交，这些提交会被同步以确保兼容性。测试在所有阶段进行，并与开发同步，所有报告的错误都会立即修复。功能倾向于以增量方式实现，从用户优先级最高的功能开始。软件在其生命周期的关键阶段通过广泛的用户测试和错误修复来稳定。

### 迭代和增量模型

此类模型依赖于一组特定的用例和详细的软件架构。每个用例描述个人或一组用户希望从系统中获得什么，共同描述完整的功能。软件架构描述软件的所有重要组件及其运行环境。用例驱动开发，而测试确保用例正确实现。编码通常划分为覆盖相关用例组，这些组以迭代方式处理。每次迭代都会产生软件的一个增量，即涵盖更多用例的版本。在此模型中，设计可能会根据需要演变，尤其是在早期阶段，后续迭代倾向于在已有工作基础上增加，而不是修改。

### 3.1.4.3 用户需求

EMBOSS 邮件列表（第 1.4 节，“项目邮件列表”）允许用户社区与开发者之间进行讨论。任何新软件都应在邮件列表上讨论。





在实施前列出清单，尤其是为了确定它是否真的需要或已经存在。

软件必须满足预期用户和用例的要求。因此，在软件整个生命周期中让用户参与软件开发是有价值的，甚至是必不可少的，尤其是这四个阶段：

- 1. 开发前
- 2. 开发
- 3. 测试和验证
- 4. 演进。

> **重要**
>
> 还有超出本手册范围的其他要求（例如软件测试和用户需求调查）和策略（例如如何最好地实现不断变化的需求），但核心信息很简单：*始终与您的用户保持联系，即使您是唯一的用户，在软件生命周期的所有阶段*。

### *开发前*

在编码开始之前，在开发前阶段尽可能完整地了解用户或用例要求是至关重要的。试图让用户明确具体的要求。魔鬼藏在细节中，因为任何误解都可能导致开发浪费。要求必须与开发者的限制相平衡，有些功能可能计划在第一个版本中实现，而其他功能则留待以后，但在设计阶段会被考虑。通常，为新功能修改现有代码远比从一开始就编写（或至少考虑）它们要困难得多，因此在此阶段的任何努力都将得到丰厚回报。

### *开发*

在开发的所有阶段向预期用户演示您的软件，尤其是在早期。这样可以确认功能是否按计划发展。随着实施的推进并固定于特定方法，开发者和用户对软件的概念可能会出现偏差。如果保持良好的沟通，可以缓解这种情况。不可避免地，在实施过程中会出现问题，想法也会演变。通过保持联系，您可以避免不必要的开发，并根据持续的进展微调用户需求。

### *测试和验证*

用户最宝贵的贡献在于测试软件。他们会发现使用（和滥用）软件的方式，而这是您未曾预料到的。至关重要的是，这应该验证软件在实际场景中按要求工作并满足用户的需求。通常，测试会产生新的错误和需求，在测试版软件被完善时必须修复或实现。测试应产生一个发布候选版本，其中主要功能被冻结。从那时起，只有次要错误修复和功能才应为正式发布实施。要有条理，以便在适当的时间采纳建议：在发布日期前一天提出重大新功能的建议是不受欢迎的！

试图保持对用户需求的清晰了解，并相应地规划您的工作。

### 演进

即使按照最佳设计实现的软件也只能满足当时已知的需求。在实践中，您的软件必须发展以跟上用户的步伐，用户的需求往往也在变化。在某些情况下，当为不断变化的需求调整软件时，有必要将软件移回测试版，甚至在需要完全重新设计时从头开始。在这种情况下，了解软件的当前阶段有助于管理期望。

### 3.1.5 规划

在开始编码之前，您应该深入思考代码究竟应该实现什么。至少在两个不同的场合这样做，以确保您已考虑到一切。一旦开始编码，要纳入新想法就会困难得多。规划越详细越好！

除了简单情况外，按照某种设计进行编码是有帮助的。这可能是一个“一次性”的代码初始版本，仅用于测试想法，在正式编码开始时被丢弃。否则，使用正式和非正式的方法，例如流程图、散文中的逻辑步骤等。任何有助于形成对代码目的和行为的清晰明确想法的东西都足够。特别注意输入和输出、主要逻辑步骤以及任何棘手的步骤。该过程应产生适合用于编码的设计。

### 3.1.5.1 应用程序开发

EMBOSS 包含许多应用程序，很可能有一个应用程序与您需要的功能类似。因此，在开始编码之前，您应该查看应用程序文档：

- EMBOSS (http://emboss.open-bio.org/rel/dev/apps/)
- EMBASSY (http://emboss.open-bio.org/rel/dev/apps/)

应用程序开发有三种基本类型：

- 修改现有应用程序
- 开发新应用程序
- 为现有第三方软件开发包装器应用程序。

如果似乎只需要对现有应用程序进行简单修改，这可能通过修改 ACD 文件轻松实现，根本不需要新的 C 编码。请参阅 ACD 文件开发（第 5 章，C 编程）和 ACD 语法（附录 A，ACD 语法参考）。

在其他情况下，需要一个完全新的应用程序。AJAX 和 NUCLEUS 库（参见第 B.1 节，‘C 编程库’）为开发

## 3.1 EMBOSS 编程

应用程序从头开始。现有应用程序的 ACD 文件和 C 源代码可能提供有价值的起点，或提供如何继续的线索。

还有些情况，您已经拥有想要纳入 EMBOSS 的应用程序源代码，或者您希望为现有应用程序提供 EMBOSS 风格的命令行界面。EMBOSS 下的应用程序包装和移植将在后面描述（第 10.2 节，‘包装器和端口’）。

在考虑新应用程序时，有两条基本规则（有少数例外）：

- EMBOSS 应用程序应执行单个明确定义的操作。
- 只有当新应用程序与现有程序相比有超过一个额外主要参数的差异时，才应编写新应用程序。

规划中有三个领域值得特别关注：

- 初步文档
- 输入和输出
- 对象和函数。

### *初步文档*

在编码 *之前* 为应用程序及其代码编写一些初步文档。这可能包括，但绝不限于：

- 应用程序功能的单行描述
- 应用程序功能的更详细描述
- 输入和输出文件列表
- 其他应用程序参数列表
- 每个参数的单行描述
- 每个参数的默认值以及是否需要用户提供值
- 程序所有主要逻辑步骤的带编号注释（写入 C 源代码文件）
- 程序棘手步骤的注释
- 为每个主要步骤提供伪代码或其他结构化注释，以捕获程序逻辑、循环结构等。

### *输入和输出*

特别注意应用程序参数；所有输入、输出和任何其他选项。您应该为 ACD 文件中需要的数据定义（第 4.3 节，‘数据定义’）制定一个确定列表。

### *对象和函数*

在开始编码 *之前*，您应该知道需要哪些对象（C 数据结构）和函数，以便您需要的一切都可用。这就像在开始 DIY 项目之前收集所有工具一样。如果您不得不反复中断去查找函数，而本应专注于程序逻辑，进度将会缓慢。如果需要任何新对象和函数，请参阅库开发指南（第 5.5 节，‘使用对象进行编程’）。

### 3.1.5.2 库开发

AJAX 和 NUCLEUS 库易于扩展，但可能已经包含您需要的功能。因此，首先要做的是查看 AJAX 和 NUCLEUS 的文档（参见附录 B，C 编程库）。

库开发包括：

- 扩展现有代码的功能
- 开发新对象和函数
- 开发全新的库文件。

在开发库代码时，要小心避免与现有代码冗余。如果可能，您应该修改现有对象或函数，或者至少将 C 源代码作为起点或获取如何继续的想法。

当代码是专用的（仅由一个应用程序使用）时，它应留在应用程序 C 源代码文件中，直到被更广泛地使用。只有可能具有通用用途的代码才应进入 AJAX 或 NUCLEUS。

当新代码位于现有 AJAX 或 NUCLEUS 库文件的领域时，应将其添加到该文件中。当需要新的功能类别时，应为其创建一个新库文件。

### 3.1.6 在开始编码之前

在开始编码之前，请与 EMBOSS 开发者讨论您的想法：

```
emboss-bug@emboss.open-bio.org.
```

也让其他 EMBOSS 用户知道。许多人可能希望与您合作或建议更简单的做事方式：

```
emboss@emboss.open-bio.org.
```

| 应用程序 ACD 文件 | 任何新应用程序都需要一个 ACD 文件。一旦您熟悉了常规布局、语法（附录 A，ACD 语法参考）和编程方法（第 5 章，C 编程），编写它们就很容易。 |
|---|---|
| 链接到 EMBOSS 库 | 应用程序代码必须链接到 EMBOSS 库。最低要求是处理应用程序 ACD 文件的代码（参见第 6.3 节， |



## Choice of programming language

'Handling ACD files'). 在某些情况下，您可能希望保持原始源代码不变，而是为其开发一个 EMBOSS 包装器应用程序（第 10.2 节，‘包装器和端口’）。理想情况下，代码应使用 ANSI C 或 C++ 编写；但是，也会考虑并欢迎其他语言的贡献。

## Coding standards

代码应遵循基本约定和标准（附录 C，C 编码标准）。这并非严格要求，但受到鼓励。当然，不要因为认为代码不够好而不提交。如果有必要，以后可以改进。

## Licensing

理想情况下，代码将在 GPL 许可证下授权；但是，带有非 GPL 许可证的代码可以纳入 EMBASSY（参见第 1.1 节，‘许可证信息’）。

## Testing

所有提交的代码都应经过充分测试且无错误。如果您开发了新应用程序，则理想情况下应为其提供正式的质量保证测试。有关更多信息，请参见第 7 章，质量保证。

## Documentation

所有应用程序及其底层代码都应有完善的文档。最低要求是其他人能够跟随您所做的工作并使用该软件。理想情况下，文档将符合为代码（附录 D，代码文档标准）和应用程序（第 8 章，应用程序文档标准）定义的基本标准。如果您认为代码不够好，请不要气馁。EMBOSS 开发人员将就如何改进向您提供建议。

## 3.1.7 ACD file development

ACD 文件详细描述了单个 EMBOSS 应用程序的参数和命令行界面。它指定了所需或允许的确切输入值，以及如何提示用户输入，以确保应用程序能够正确运行。它还定义了从 ACD 文件派生的其他界面（例如图形用户界面 (GUI)）的基本功能。

ACD 文件必须包含一个应用程序定义（第 4.2 节，‘应用程序定义’），然后为每个参数包含一个数据定义（第 4.3 节，‘数据定义’）。定义由一个或多个属性组成，这些属性是名称:值对，详细描述应用程序或参数。先给出应用程序定义，然后是数据定义，数据定义组织为“输入”、“输出”等部分。

建议在 C 源代码之前编写 ACD 文件，因为它定义了程序的大部分功能。如果您已经从设计中拥有所有应用程序参数的详细列表，那么编写 ACD 文件应该很容易。ACD 文件使用 ACD 语法编写（附录 A，ACD 语法参考）；请参见编程指南（第 5 章，C 编程）。

提供了各种实用程序（第 4.6 节，‘ACD 实用程序’）用于验证、调试和处理 ACD 文件。您应该使用这些工具来确保 ACD 文件有效且格式正确。例如，您可以使用 acdc 实用程序测试 ACD 文件的功能。一旦有了功能版本，就可以使用 acdpretty 实用程序生成带有标准格式的文件。

## 3.1.8 C source code development

### 3.1.8.1 Coding standards

为确保 EMBOSS 代码的一致性，您编写的所有 C 代码都应符合基本样式。在编码之前，您应熟悉这些标准（附录 C，C 编码标准）。

编码标准主要涉及代码布局，但也包括 EMBOSS 中 C 编程的一些一般指南，特别是数据类型和函数的编程。

### 3.1.8.2 Application development

您需要在适当的目录中创建（如有必要）新的应用程序 C 源代码（ApplicationName.c）文件。文件应具有简短且有意义的名称，如果可能，最好与功能相似的应用程序有一定相似之处。通常，单独开发使用 EMBASSY myemboss 包。或者，可以使用另一个 EMBASSY 包或 EMBOSS 本身中的应用程序目录：

```
/home/auser/emboss/emboss/embassy/myemboss/src
/home/auser/emboss/emboss/embassy/PackageName/src/
/home/auser/emboss/emboss/emboss/
```

编写应用程序 C 源代码时，建议遵循以下几个基本步骤：

- 1. 考虑代码的正确布局（参见附录 C，C 编码标准），包括结构化注释。复制现有应用程序的布局，或者（更好的是）使用 myemboss 中提供的模板（../myemboss/src/template.c）文件。
- 2. 添加一个空的 main() 函数。
- 3. 为任何新函数添加原型。如果需要，以后可以将其移动到 AJAX 或 NUCLEUS。
- 4. 为任何新数据类型添加定义（参见第 5.5 节，‘使用对象进行编程’）。同样，以后可以将其移动到库中。
- 5. 添加初步设计中的任何注释、伪代码等。
- 6. 声明变量并实现读取任何 ACD 数据项的 C 代码（参见第 6.3 节，‘处理 ACD 文件’）。
- 7. 在 main() 末尾添加用于清理 ACD 数据项内存的代码。
- 8. 为 main() 函数编写其余的 C 源代码。
- 9. 为任何函数编写 C 源代码。
- 10. 确保代码（尤其是函数和数据类型）有充分的文档（参见附录 D，代码文档标准）。

### 3.1.8.3 Library development

根据需要，可以在核心 AJAX 或 NUCLEUS 目录中创建新的 C 源代码 (*.c) 和/或头文件 (*.h)：

```
/home/auser/emboss/emboss/ajax/core
```

```
/home/auser/emboss/emboss/nucleus
```

文件应具有简短且有意义的名称。AJAX 文件必须以前缀 aj 开头，例如 ajstr.h 和 ajstr.c 用于字符串处理库。NUCLEUS 文件必须具有前缀 emb；例如 embaln.h 和 embaln.c 用于排列算法代码。

要集成大量代码（例如第三方库），通常会在主 AJAX 目录下创建一个新目录：

```
/home/auser/emboss/emboss/ajax/
```

例如，zlib 库中的文件位于：

```
/home/auser/emboss/emboss/ajax/zlib
```

编写库代码时，有一些基本步骤：

- 1. 考虑代码的正确布局（参见附录 C，C 编码标准），包括结构化注释。复制现有库文件的布局是一种好的策略。
- 2. 添加函数原型。
- 3. 添加数据类型定义（参见第 5.5 节，‘使用对象进行编程’）。这包括私有数据类型（在源文件中）和公共数据类型（在头文件中）。
- 4. 为函数编写 C 源代码。这包括私有（静态）和公共（外部）函数，两者都放在源文件中。
- 5. 确保代码（尤其是函数和数据类型）有充分的文档（参见附录 D，代码文档标准）。

## 3.1.9 Integration and compilation

无论新应用程序是用于 EMBOSS 还是 EMBASSY 包，通常都会先在 myemboss（第 3.2 节，‘集成和编译’）中开发。这是一个几乎为空的 EMBASSY 包，提供了一种将本地应用程序开发与 EMBOSS 的其余部分隔离开来的方法。应用程序是使用从 Makefile.am 文件生成的 Makefile 文件构建的，该文件必须进行编辑以提及新应用程序。在 myemboss 中开发和测试的应用程序可以使用基本相同的过程添加到主包或 EMBASSY 包中。
要添加全新的 EMBASSY 包，必须创建目录结构和所需文件（包括应用程序 ACD 文件、C 源代码文件和文档），并编辑 configure.in 文件和多个 Makefile.am 文件。
AJAX 和 NUCLEUS 的新函数和数据类型必须具有结构化注释，以便与库的其余部分正确集成。全新的库文件通过编辑 AJAX 或 NUCLEUS 目录中的 Makefile.am 文件（视情况而定）来集成。还必须将任何新头文件添加到 ajax.h 和/或 emboss.h 中。
有关更多信息，请参见第 3.2 节，‘集成和编译’。

## 3.1.10 Debugging

任何贡献的代码都应尽可能无错误。EMBOSS 包含用于调试应用程序的内置功能。此外，还提供了用于修复特定代码模块的调试函数。有关更多信息，请参见第 3.3 节，‘调试’。

## 3.1.11 Quality assurance testing

为保持质量，对 EMBOSS 代码和文档执行了各种质量保证测试。所有应用程序都在测试数据上运行，以确保它们按宣传的方式工作。对整个包进行定期编译和内存泄漏测试，以确保代码的完整性，例如，应用程序不会因库的最近更改而损坏。对对象和函数的结构化文档进行验证。这确保，例如，函数和参数具有有意义且一致的名称，并且函数列在文件的正确部分中。

质量保证测试由 EMBOSS 开发人员处理，但有办法提供帮助。您自己的代码应在实际用例场景中进行彻底测试。特别是，在提交之前，应对其进行内存泄漏测试（参见第 3.3 节，‘调试’）：如果您不清楚如何操作，请在 EMBOSS 邮件列表（第 1.4 节，‘项目邮件列表’）上提问。任何要提交的库代码，或者至少是新的公共数据类型和函数，都应使用结构化注释进行文档记录（参见附录 D，代码文档标准），以便可以执行验证检查。任何新应用程序理想情况下都应有测试用例和测试数据（参见第 7 章，质量保证）。

## 3.1.12 Documentation

没有文档的软件通常价值不大，而良好的文档可以极大地增强软件的实用性。所有提交的 EMBOSS 应用程序和库代码都应有充分的文档。任何新应用程序还需要最终用户文档。

生成应用程序最终用户文档的过程（分为不同部分）涉及将手动编写的组件与自动生成的部分（例如，从解析 ACD 文件）相结合。该过程在很大程度上是自动化的。如果您开发新的 EMBASSY 包，则它将需要超出单个应用程序范围的文档。





所有库代码都必须使用结构化注释进行充分文档化，这些注释会被解析以生成在线库文档（第 1.3 节，“开发者文档”）。应用程序代码开头的注释大多包含许可和书目信息。但是，所有公共函数和数据类型也必须进行文档化。函数按功能部分组织在库文件中，这些部分定义了其中函数及其参数的命名规则。库文件开头的注释通常包含详尽的文档。如果你开发新的库文件，则需要提供同等水平的文档。

有关更多信息，请参阅代码文档（附录 D，代码文档标准）和应用程序最终用户文档（第 8 章，应用程序文档标准）的说明。

### 3.1.13 分发

任何贡献的代码都将被广泛分发并安装在许多不同的平台上。已知 EMBOSS 可在几乎每个 UNIX 系统、Microsoft Windows 和 MacOSX 上运行。这里无需做任何事情，因为这由 EMBOSS 开发人员管理，但如果你按上述总结集成、测试并正确记录任何新软件，将大有帮助。

### 3.1.14 维护、支持和培训

任何贡献的代码都需要维护和支持。这在一定程度上由 EMBOSS 开发人员覆盖，他们还运行 EMBOSS 培训课程。但是，如果你维护自己的源代码并通过 EMBOSS 邮件列表（第 1.4 节，“项目邮件列表”）提供支持，将大有帮助。

## 3.2 集成和编译

### 3.2.1 使用 myemboss 进行应用程序开发

myemboss 包是一个几乎为空的 EMBASSY 包，开发人员可以在其中安全地构建自己的 EMBOSS 应用程序。它提供了一种方法，将本地应用程序开发与 EMBOSS 的其余部分隔离开来，从而保持包的完整性。新应用程序，无论其是否最终用于另一个 EMBASSY 包或 EMBOSS 本身，通常都会在 myemboss 中开始其生命周期。

myemboss 需要安装 GNU 工具 autoconf、automake 和 libtool（参见第 1.2 节，“安装 CVS（开发者）版本”）。使用 GNU 工具，你可以非常轻松地添加新应用程序。myemboss 提供了用于集成新应用程序的目录结构和 Makefile 桩。应用程序 ACD 文件放在 myemboss/emboss_acd 目录中，源代码放在 myemboss/src 目录中。

应用程序使用 Makefile 文件构建，但你不需要直接编辑此文件。相反，你编辑一个 Makefile.am 文件，automake 将其转换为 Makefile.in 文件，configure 将其转换为 Makefile 文件。

下面显示了 Makefile.am 文件，并已对其进行编辑以包含两个应用程序：

```
#
SUBDIRS = source emboss_acd emboss_doc
EXTRA_DIST = depcomp ltmain.sh install-sh config.sub config.guess
### tar to pick up the other directories
### then remove any CVS subdirectories
dist-hook:
	tar cBf - emboss_acd | ( cd $(distdir); tar xBf - ; cd emboss_acd; rm -rf CVS)
	tar cBf - emboss_doc | ( cd $(distdir); tar xBf - ; cd emboss_doc; rm -rf CVS; rm -rf master)
```

要在 myemboss 中编译应用程序，如果尚未配置包，则必须先配置它（参见第 1.2 节，“安装 CVS（开发者）版本”），然后从 myemboss 应用程序目录（myemboss/src）键入以下内容：

```
make
```

make 将重新生成 Makefile 文件并构建你的新应用程序，将其链接到 EMBOSS 库（AJAX 和 NUCLEUS）。

这假设你已安装并配置了 EMBOSS 和 myemboss 包。如果你使用 make install 进行了完整的 EMBOSS 安装，则还必须键入：

```
make install
```

以完成在 myemboss 下开发的应用程序的安装。

有关安装的更多信息，请参见第 1.2 节，“安装 CVS（开发者）版本”和《EMBOSS 管理员指南》。

### 3.2.2 添加新的 EMBOSS 应用程序

在 myemboss 中开发和测试过的应用程序可以添加到主包中。将新应用程序添加到 EMBOSS 与 myemboss 基本相同。EMBOSS 有自己的 Makefile.am，与 myemboss 不同，它将应用程序组织为两个部分：

- 标准 EMBOSS 应用程序（“make”应用程序）列在 bin_PROGRAMS 行之后
- 尚未完全集成的应用程序（“make check”应用程序）列在 check_PROGRAMS 行之后。

不完全完整的应用程序应放入 emboss/Makefile.am 文件的“make check”区域。例如，那些可以编译并正确运行，但尚未提供完整文档和质量保证测试的应用程序，应放在这里。只有完全正常工作、经过测试并有文档的应用程序才应放入“make”区域。

Makefile.am 文件的摘录如下，包含一些“make check”应用程序和标准“make”应用程序：

```
SUBDIRS = acd data

EXTRA_DIST = emboss.default.template

if ISSHARED
if ISAXIA64
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L../ajax/.libs -lajax
else
AM_CFLAGS =
endif
endif

check_PROGRAMS = acdlog acdxsd ajtest \
complex corbatest \
entrails entrailsbook entrailshtml entrailswiki giep histogramtest intconv \
origsplitter origunion \
newcoils \
... <lines omitted for brevity>

bin_PROGRAMS = aaindexextract abiview \
acdc acdpretty acdtable acdtrace acdvalid \
aligncopy aligncopypair antigenic \
backtranambig backtranseq banana biosed btwisted \
... <lines omitted for brevity>

water whichdb wobble \
wordcount wordfinder wordmatch wossname \
yank

INCLUDES = -I$(top_srcdir)/nucleus -I$(top_srcdir)/ajax -I$(top_srcdir)/plplot

aaindexextract_SOURCES = aaindexextract.c
abiview_SOURCES = abiview.c
acdc_SOURCES = acdc.c
acdpretty_SOURCES = acdpretty.c
acdtable_SOURCES = acdtable.c

... <lines omitted for brevity>

seqretsingle_SOURCES = seqretsingle.c
seqrettype_SOURCES = seqrettype.c
testplot_SOURCES = testplot.c
treetypedisplay_SOURCES = treetypedisplay.c

### Uncomment to use dual libraries
if ISCYGWIN
LDADD = ../nucleus/libnucleus.la ../ajax/libajax.la ../ajax/libajaxg.la ../plplot/libeplplot.la $(XLIB)
else
LDADD = ../nucleus/libnucleus.la ../ajax/libajaxg.la ../ajax/libajax.la ../plplot/libeplplot.la $(XLIB)
endif

pkgdata_DATA = emboss.default.template
pkgdatadir=$(prefix)/share/$(PACKAGE)

#ifdef PURIFY
### LINK = purify $(LIBTOOL) -mode=link $(CC) $(CFLAGS) $(LDFLAGS) -o $@
#else
#
#endif
```

编译与 **myemboss** 相同。如果尚未配置 EMBOSS 包，则必须先配置它（参见第 1.2 节，“安装 CVS（开发者）版本”），然后从应用程序目录（例如 /home/auser/emboss/emboss/emboss/）键入：

```
make
```

这将重新生成 `Makefile` 文件，构建你的新应用程序并将其链接到库。如果你使用 `make install` 安装了 EMBOSS，则还必须键入：

```
make install
```

以完成新应用程序的安装。
有关安装的更多信息，请参见第 1.2 节，“安装 CVS（开发者）版本”和 _EMBOSS 管理员指南_。

### 3.2.3 添加新的 EMBASSY 应用程序

应用程序添加到 EMBASSY 包的方式与 **myemboss** 完全相同（见上文）。

### 3.2.4 添加新的 EMBASSY 包

要添加全新的 EMBASSY 包，你必须：

- 1. 在主 EMBASSY 目录（../emboss/emboss/embassy/）下为包创建目录结构和所需文件。
- 2. 编写应用程序 ACD 和 C 源代码文件，并填充相应目录。
- 3. 编辑 `Makefile.am` 文件。
- 4. 编辑 `configure.in` 文件。
- 5. 创建应用程序文档并填充相应目录。

### 3.2.4.1 目录结构

无论包如何，目录结构和文件名大多相同。例如，**hmmernnew** EMBASSY 包如下所示：

```
% cd emboss/emboss/embassy/hmmernnew/
% ls
AUTHORS COPYING emboss_acd ltmain.sh NEWS Userguide.pdf
ChangeLog CVS emboss_doc m4 README
configure.in DOCS INSTALL Makefile.am src
```





必需的目录如下：

- src
  “应用程序目录”，存放应用程序 C 源代码。该目录应包含一个 Makefile.am 文件。

- emboss_acd
  “ACD 目录”，存放应用程序 ACD 文件。该目录应包含一个 Makefile.am 文件（见下文）。

- emboss_doc
  “文档目录”。它包含以下子目录：html：HTML 格式的文档；text：纯文本格式的文档；master：带有包含文件的最终格式文档。此目录及其 html 和 text 子目录中均有 Makefile.am 文件，在创建新包时都需要对其进行编辑。使用半自动化流程（附录 8，应用程序文档标准）来创建这些目录中的文档文件。

- DOCS
  此目录原本用于存放外围文档，但当前未使用。

- m4
  此目录包含 automake 过程中使用的宏文件。这些文件可以从另一个 EMBASSY 包中复制。

此外，某些包可能包含以下目录：

- include
  特定于该包的头文件。

- data
  特定于该包的数据文件。

仅当包已提交到 CVS 服务器时，CVS 目录才会出现。

必需的文件如下。如果遗漏其中任何文件，则在将 EMBASSY 包打包为分发文件时，GNU 软件会报错；GNU 软件通常会随后添加一个默认文件：

- README
  这是包的用户指南，通常包含关于整个包的一般性注释，例如安装说明、使用笔记等。它通常不应包含关于单个应用程序的文档。README 并非严格要求，但强烈推荐使用，尤其是当包包含对第三方应用程序的封装（参见第 10.2 节，“封装和端口”）且原始应用程序与封装之间存在差异时。

- COPYING
  版权或其他使用限制信息。这可能只是对包含此类信息的 README 文件的引用，或包含 GPL 许可证或其他内容。

- INSTALL
  EMBASSY 包的标准安装说明。此文件可以从另一个 EMBASSY 包中复制。

- NEWS
  包版本信息。它用于创建捆绑分发文件（通过 make dist）。

- AUTHORS
  作者联系信息。如果 EMBASSY 包包含封装应用程序，则应同时提及原始软件的作者和 EMBASSY 包的作者。

| 文件 | 描述 |
|---|---|
| ChangeLog | 包更改日志文件。提供一个很有帮助，但并非严格必要。 |
| configure.in | 使用 autoconf 处理以生成 configure 脚本的配置文件（参见第 1.2 节，“安装 CVS（开发者）版本”）。应从另一个 EMBASSY 包中复制，但在使用前需要进行一些简单的自定义（参见第 3.2.4.3 节，“编辑 configure.in 文件”）。 |
| ltmain.sh | libtool 包前端脚本。可以从另一个 EMBASSY 包中复制。 |

还可以提供其他文件。例如，HMMERNEW 包含原始 HMmer 应用程序的文档。

## 3.2.4.2 编辑 Makefile.am 文件

EMBASSY 中使用的 Makefile.am 文件与主 EMBOSS 包中使用的不同。在创建新 EMBASSY 包时，必须在以下每个目录中编辑六个 Makefile.am 文件：

- /packagename/
- /packagename/src
- /packagename/emboss_acd
- /packagename/emboss_doc
- /packagename/emboss_doc/html
- /packagename/emboss_doc/text

所需的编辑内容应通过检查下面的文件（针对 myemboss 包）来明显看出。

### /myemboss/Makefile.am

文件如下所示：

```
#
SUBDIRS = source emboss_acd emboss_doc

EXTRA_DIST = depcomp ltmain.sh install-sh config.sub config.guess

### tar to pick up the other directories
### then remove any CVS subdirectories

dist-hook:
	tar cBf - emboss_acd | ( cd $(distdir); tar xBf - ; cd emboss_acd; rm -rf CVS)
	tar cBf - emboss_doc | ( cd $(distdir); tar xBf - ; cd emboss_doc; rm -rf CVS; rm -rf master)
```

SUBDIRS 行必须引用包中所有具有 Makefile.am 文件的顶级子目录。

dist-hook 条目必须相应地进行编辑。

### /myemboss/src/Makefile.am

文件如下所示：

```
## Process this file with automake to produce Makefile.in

EXTRA_DIST = Makefile.am

bin_PROGRAMS = myseq mytest

if LOCALLINK
INCLUDES = -I../include -I../../../nucleus -I../../../ajax -I../../../plplot
else
INCLUDES = -I../include -I${embprefix}/include -I${embprefix}/include/eplplot
endif

if ISSHARED
if ISAXIA64
if LOCALLINK
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L../../../plplot/.libs -L../../../ajax/.libs -L../../../nucleus/.libs -lnucleus -lajax -leplplot
else
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L${embprefix}/lib -lnucleus -lajax -leplplot
endif
else
AM_CFLAGS =
endif
endif

myseq_SOURCES = myseq.c
mytest_SOURCES = mytest.c

if LOCALLINK
LDADD = ../../../nucleus/libnucleus.la ../../../ajax/libajaxg.la ../../../ajax/libajax.la ../../../plplot/libeplplot.la $(XLIB)
else
LDADD = -L${embprefix}/lib -lnucleus -lajaxg -lajax -leplplot $(XLIB)
endif
```

必须在 bin_PROGRAMS 条目中列出所有应用程序的名称，如果这些名称由反斜杠字符分隔，则可能跨越多行。每个应用程序的 C 源代码文件引用位于文件底部附近，例如
myseq_SOURCES = myseq.c。

### /myemboss/emboss_acd/Makefile.am

```
EXTRA_DIST = Makefile.am

pkgdata_DATA = myseq.acd mytest.acd

pkgdatadir=${prefix}/share/EMBOSS/acd
```

必须在 pkgdata_DATA 条目后列出所有应用程序 ACD 文件的名称，这可能跨越多行。

### /myemboss/emboss_doc/Makefile.am

```
SUBDIRS = html text
```

此文件通常不需要编辑。

### /myemboss/emboss_doc/html/Makefile.am

```
pkgdata_DATA = index.html \
myseq.html

pkgdatadir=${prefix}/share/EMBOSS/doc/html/embassy/myseq
```

HTML 格式的所有应用程序文档文件（第 8 章，应用程序文档标准）都必须列在 pkgdata_DATA 条目中，这可能跨越多行。任何其他自动生成的文档文件也列在此处。以 pkgdatadir= 开头的行必须更改，以便给出正确的包名。

### /myemboss/emboss_doc/text/Makefile.am

文件如下所示：

```
pkgdata_DATA = myseq.txt

pkgdatadir=${prefix}/share/EMBOSS/doc/programs/text
```

这基本上与 /myemboss/emboss_doc/html/Makefile.am 相同，但引用纯文本格式的文档。

## 3.2.4.3 编辑 configure.in 文件

此处只需编辑两行：

- 必须更改 AC_INIT 行，以便它引用包中的一个（任意）应用程序 C 源代码文件。
- AM_INIT_AUTOMAKE 行应给出包名和版本号。

一旦应用程序 ACD 文件和 C 源代码编写并集成完毕，编译过程与任何其他 EMBASSY 包相同（参见第 3.2.1 节，“使用 myemboss 进行应用程序开发”）。

## 3.2.5 添加新函数和数据类型

添加到 AJAX 或 NUCLEUS 的任何新函数和数据类型，如果要纳入 EMBOSS 分发版，都应得到适当的文档记录（附录 D.1，“代码文档标准”）。要编译新代码，请键入：

```
make
```

从 AJAX 或 NUCLEUS 目录（视情况而定）执行。当然，您需要重新编译任何静态链接的应用程序才能使用这些更改。或者，通过从二级 EMBOSS 目录键入 make 来重新编译整个包，例如：

```
/home/auser/emboss/emboss/
```

## 3.2.6 添加新库文件

如果您添加了全新的库文件，则必须通过编辑 AJAX 或 NUCLEUS 目录中的 Makefile.am（视情况而定）将其集成到 AJAX 或 NUCLEUS 中。

AJAX Makefile.am 文件的摘录：

```
## Process this file with automake to produce Makefile.in

if ISCYGWIN
lib_LTLIBRARIES = libajax.la
else
lib_LTLIBRARIES = libajax.la libajaxg.la
endif

if ISSHARED
if ISAIA64
if NEEDAJAX
AM_CFLAGS = -Wl,-G -L../plplot/.libs -L.libs -lajax -leplplot -lm
else
AM_CFLAGS = -Wl,-G -L../plplot/.libs -L.libs -leplplot -lm
endif
else
AM_CFLAGS =
endif
endif

if ISCYGWIN
AM_LDFLAGS = -no-undefined -Wl,--add-stdcall-alias -Wl,--export-all-symbols -Wl,--enable-auto-import -L../plplot -leplplot
endif

## PCRE stuff (version 4.3)

POSIX_MALLOC_THRESHOLD = @POSIX_MALLOC_THRESHOLD@
PCRELIBVERSION = @PCRE_LIB_VERSION@
PCREPOSIXLIBVERSION = @PCRE_POSIXLIB_VERSION@

INCLUDES = -DAJAX_FIXED_ROOT=$(AJAX_FIXED_ROOT) -DPREFIX=\"$(prefix)\" -I$(top_srcdir)/plplot $(POSIX_MALLOC_THRESHOLD)
#LDFLAGS = -no-undefined
LIBS =

AJAXSRC = ajacd.c ajalign.c ajarr.c ajassert.c \
ajbase.c \
ajcall.c ajcod.c \
ajdan.c ajdmx.c ajdom.c ajdomain.c ajexcept.c \
ajfeat.c ajfile.c ajfmt.c ajgraphxml.c ajindex.c ajjava.c ajlist.c \
ajmath.c ajmatrices.c ajmem.c ajmess.c ajnam.c ajnexus.c \
ajpat.c ajpdb.c ajpdbio.c ajphylo.c \
ajrange.c ajreg.c ajreport.c \
ajseq.c ajseqabi.c ajseqdb.c ajseqread.c ajseqtype.c ajseqwrite.c \
ajsort.c ajstr.c ajsys.c \
ajtable.c ajtime.c ajtranslate.c ajtree.c ajutil.c ajvector.c \
pcre.c pcre_study.c pcreposix.c

AJAXGSRC = ajgraph.c ajhist.c

include_HEADERS = ajax.h ajarch.h ajdefine.h \
ajacd.h ajalign.h ajarr.h ajassert.h \
```





```
ajbase.h ajcall.h ajcod.h \
ajdan.h ajdmx.h ajdom.h ajdomain.h ajexcept.h \
ajfeat.h ajfeatdata.h ajfile.h ajfmt.h \
ajgraph.h ajgraphxml.h ajgraphstruct.h ajhist.h ajindex.h ajjava.h ajlist.h \
ajmath.h ajmatrices.h ajmem.h ajmess.h ajnam.h ajnexus.h \
ajpat.h ajpdb.h ajpdbio.h ajphylo.h \
ajrange.h ajreg.h ajreport.h \
ajseq.h ajseqabi.h ajseqdata.h ajseqdb.h ajseqread.h ajseqtype.h ajseqwrite.h \
ajsort.h ajstr.h ajsys.h \
ajtable.h ajtime.h ajtranslate.h ajtree.h ajutil.h ajvector.h \
pcre.h pcre_chartables.c pcre_config.h pcre_get.c pcre_printint.c \
pcre_internal.h pcreposix.h
```

```
if ISCYGWIN
libajax_la_SOURCES = $(AJAXSRC) $(AJAXGSRC)
libajax_la_LDFLAGS = -version-info 5:0:0
else
libajax_la_SOURCES = $(AJAXSRC)
libajax_la_LDFLAGS = -version-info 5:0:0
libajaxg_la_SOURCES = $(AJAXGSRC)
libajaxg_la_LDFLAGS = -version-info 5:0:0
endif
```

## NUCLEUS Makefile.am 文件：

```
## Process this file with automake to produce Makefile.in
lib_LTLIBRARIES = libnucleus.la
if ISSHARED
if ISAIXIA64
AM_CFLAGS = -Wl,-G -lm -L../ajax/.libs -lajax
else
AM_CFLAGS =
endif
endif
if ISCYGWIN
AM_LDFLAGS = -no-undefined -Wl,--add-stdcall-alias -Wl,
--export-all-symbols -Wl,--enable-auto-import -L../plplot -L../ajax -leplplot -
lajax
endif
INCLUDES = -I$(top_srcdir)/plplot $(X_CFLAGS) -I$(srcdir)/ -I$(top_srcdir)/ajax
LIBS =
NUCLSRC = embaln.c embcom.c embcons.c \
embdata.c embdbi.c embdmx.c embdomain.c \
embest.c embexit.c embgroup.c \
embiep.c embindex.c embinit.c \
embmat.c embmisc.c embmol.c \
embnmer.c embpat.c embpatlist.c embprop.c embpdb.c \
embread.c embsig.c \
embshow.c embword.c
libnucleus_la_SOURCES = $(NUCLSRC)
```

## 3.2 集成和编译

```
libnucleus_la_LDFLAGS = -version-info 5:0:0

include_HEADERS = emboss.h \
  embaln.h embcom.h embcons.h \
  embdata.h embdbi.h embdmx.h embdomain.h \
  embest.h embexit.h embgroup.h \
  embiep.h embindex.h embinit.h \
  embmat.h embmisc.h embmol.h \
  embnmer.h embpat.h embpatlist.h embprop.h embpdb.h \
  embread.h embsig.h \
  embshow.h embword.h
```

还必须将任何新的头文件添加到 ajax.h 和/或 emboss.h 中。ajax.h 的内容如下：

```
#ifdef __cplusplus
extern "C"
{
#endif

/*
**
** AJAX master include file
**
*/

#ifndef ajax_h
#define ajax_h

#include <stdio.h>

#include "ajarch.h"

#include <stdarg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
/*#include <malloc.h>*/

#include "ajassert.h"
#include "ajdefine.h"
#include "ajstr.h"
#include "ajtime.h"
#include "ajfile.h"
#include "ajlist.h"

#include "ajtable.h"
#include "ajnexus.h"
#include "ajfeat.h"
#include "ajseq.h"
#include "ajseqdata.h"
#include "ajseqtype.h"
#include "ajarr.h"
#include "ajseqread.h"
#include "ajseqwrite.h"
#include "ajindex.h"
#include "ajseqdb.h"
#include "ajseqabi.h"
#include "ajreport.h"
#include "ajfmt.h"
#include "ajmatrices.h"
#include "ajalign.h"

#include "ajrange.h"
#include "ajcod.h"
#include "ajmath.h"

...
... Entries omitted for brevity
...

#endif

#ifdef __cplusplus
}
#endif
```

emboss.h 的内容如下：

```
#ifndef emboss_h
#define emboss_h

#include "ajax.h"
#include "ajgraph.h"
#include "embaln.h"
#include "embcom.h"
#include "embcons.h"
#include "embdbi.h"

...
... Entries omitted for brevity
...

#ifdef WIN32
#define VERSION "5.0.0"
#endif

#endif
```

## 3.3 调试

Bug 是导致代码崩溃或以意外方式运行的代码问题。它们源于语法使用错误（编译器并不总能捕获）和代码逻辑错误。本节提供了一些调试 EMBOSS 代码的实用提示。

### 3.3.1 直接调试

大致而言，调试分为四个阶段，其中修复的 Bug 包括：

- 1. 阻止程序编译
- 2. 导致程序崩溃
- 3. 导致程序运行不正确
- 4. 在广泛测试条件下显现

凭借经验，大多数 Bug 通过目视检查代码就能发现。强烈建议，在编译代码 *之前*，反复阅读代码，直到你确信它应该按预期工作。编写代码本身时要一丝不苟。避免编写过快的诱惑；在一开始就花额外时间避免错误，以后会得到非常丰厚的回报。

> **提示**
>
> 一种简单而强大的调试方法是使用 `ajFmtPrint` 和 `fflush(stdout)` 语句在执行的不同阶段报告关键变量的值，从而追踪和识别问题。`ajFmtPrint` 用于打印变量，`fflush` 会在随后立即调用以刷新输出缓冲区。这一点很重要，因为在崩溃点输出缓冲区可能包含内容，只有通过调用 `fflush(stdout)` 才会将其打印到屏幕上。使用此方法可以轻松解决大多数 Bug。

编写代码时，会有许多阶段，你事先知道变量应该（或不应该）具有什么值，尤其是在检查函数的参数或返回值时。例如，函数使用的指针在大多数情况下不应为 `NULL`。在所有此类位置，至少在代码的早期版本中，应添加代码来捕获错误并引发适当的警告，以便在 Bug 显现之前提醒你注意潜在的 Bug。

`ajmess.h` 中的 AJAX 函数提供了多种级别的错误处理。以下每个函数都会格式化并输出异常消息（作为字符串提供）：

| 函数 | 描述 |
|------|------|
| ajUser | 报告一条信息性消息 |
| ajWarn | 报告一条警告消息 |
| ajErr | 报告一条错误消息 |
| ajExit | 报告一条消息然后退出 |
| ajDie | 报告一条消息然后崩溃（终止）应用程序 |
| ajDebug | 如果命令行中给出了 `-debug` 开关，则将一般调试消息报告到文件 `programname.dbg` |

消息会发送到 `stdout` 或 `stderr`（两种情况通常都是屏幕），或者在 `ajDebug` 的情况下，发送到文件 `programname.dbg`。

> **重要**
>
> EMBOSS 代码大量使用 `ajDebug`，以便可以轻松追踪用户报告的 Bug。因此，调试应用程序的典型方法是使用 `-debug` 生成调试跟踪。

在实践中，为了速度，在代码经过广泛测试完成后，大部分错误捕获代码可以被注释掉或删除。这对于库函数代码尤其正确，因为速度至关重要。

对于绝大多数应用程序，ajDebug 和上述其他函数就足够了。然而，在特殊情况下，你可能需要编写自己的异常处理函数。为此提供了一个 AJAX 库文件 ajmess（参见第 6.23 节，“处理异常消息”）。

### 3.3.2 AJAX 调试函数

大多数 AJAX 库文件都包含用于调试该库文件中代码的函数。这些函数通常会调用 ajDebug。通常会提供函数来报告该库文件中定义的数据结构的内部状态。在某些情况下，会提供特殊的调试文件。例如，调试序列输出时使用“debug”输出序列格式，调试报告格式时使用“trace feature table”。

有关更多信息，请参阅 AJAX 和 NUCLEUS 的库文档。另请参阅各个库文件的编程指南（第 3.1 节，“EMBOSS 编程”）。

### 3.3.3 控制调试行为

EMBOSS 的默认行为是不报告由 ajDebug 调用生成的调试信息。全局命令行限定符 -debug 可用于为任何 EMBOSS 应用程序启用调试。例如，如果你在发出以下命令时认为发现了一个 Bug：

```
secret sequence.seq
```

则可以按以下方式启用调试：

```
secret sequence.seq -debug
```

这将创建一个名为 secret.dbg 的调试文件。可以通过在限定符前加上 no 来显式关闭调试：

```
secret sequence.seq -nodebug
```

但通常无需这样做，因为默认值为 false（无调试）。然而，如果在 EMBOSS 配置文件或环境变量中默认启用了调试，这可能很有用。可以使用 EMBOSS 环境变量全局开启调试：

```
EMBOSS_DEBUG
```



如果此项设置为 TRUE，所有程序都会表现得好像命令行上设置了 -debug。它们会创建一个名为 programme.dbg 的文件，其中包含调试信息。

可以使用以下内容开启 EMBOSS 配置文件 emboss.default 和 .embossrc 处理过程的日志记录：

```
EMBOSS_NAMDEBUG
```

此处理在处理 -debug 命令行开关之前进行。被调用的函数在 ajnam.c 中有描述。调试信息包括以下报告：

- 所有已定义的数据库、变量和环境变量。
- 数据库定义的属性。
- 资源定义的属性。

### 3.3.4 调试器

有些错误可能通过目视检查不明显，或难以使用 ajFmtPrint 和 fflush(stdout) 轻松追踪。对于这类情况，值得使用专门的调试软件。调试器会执行有错误的程序并追踪其内部状态，以便代码问题能够被快速识别和修复。可用的功能取决于所使用的调试器。大多数调试器对程序提供控制，允许以逐步方式执行、为变量赋值等等，相比于在脑海中进行，这提供了一种更快速、更可靠的方式来逐步执行代码逻辑。大多数调试器至少应提供以下信息：

- 程序崩溃时的代码行和语句。
- 如果错误发生在函数内部，则为调用该函数的行及其参数。
- 程序执行过程中特定点处的变量值（函数局部变量或全局变量）。
- 程序中特定表达式的结果。

最流行的 UNIX 调试器是 GDB，即 GNU 调试器（参见 http://sourceware.org/gdb/）。它包含用于追踪和修改程序执行的强大功能，但你只需使用其最基本的功能，它就能变得非常有用。

如果你打算使用 GDB 调试 EMBOSS 代码，则需要使用以下内容配置软件包：

```
--enable-debug
```

在构建软件包之前（参见第 1.2 节，“CVS（开发者版）的安装”）。

> **注意**
> 调试器的输出并不总是完全可信。
> 在极少数情况下，为调试编译的可执行文件的行为可能与标准可执行文件有细微差别。出于这个原因，ajFmtPrint 和 fflush 语句（对可执行文件而言侵入性较小）仍然是最后的手段。

### 3.3.5 追踪内存问题

有些错误无法通过直接手段或调试器识别。此类错误通常由严重的编程错误引起，包括指针的无效使用、内存损坏、内存泄漏或无效内存访问，例如越界数组。这些错误可能极难追踪，但在 C 编程中很容易出现，尤其是在大量使用 C 指针的情况下。幸运的是，有几种优秀的程序可用于捕获和识别此类问题。即使你的代码看起来运行正常，使用内存检查器来验证内存未被侵犯也是非常值得的。使用这些工具可以避免日后数小时的沮丧，并有助于确保你的代码在不同用例中保持稳定。流行的程序包括：

- **Valgrind** (http://valgrind.org/) 一套用于调试和分析 Linux 程序的工具。它能检测许多内存管理和线程错误。它还执行性能分析，帮助你找到加快程序运行并减少内存使用的方法。
- **PurifyPlus** 用于内存损坏检测、内存泄漏检测、应用程序性能分析和代码覆盖率分析的商业软件。
- **Insure++** 功能强大的商业软件，用于检查内存使用的完整性，并检测内存使用中的潜在缺陷和低效问题。

## ACD 文件开发

## 4.1 ACD 文件开发简介

### 4.1.1 ACD 文件简介

每个 EMBOSS 和 EMBASSY 程序都有一个 ACD（AJAX 命令定义）文件，用于描述应用程序、其选项（参数）和命令行界面。ACD 文件控制应用程序在命令行上的行为，特别是所有用户输入操作。它包括：

- 应用程序定义，用于描述应用程序本身，例如其名称、文档文本和功能分组。
- 属性，用于定义在不同条件下确切允许或要求哪些选项，如何在命令行上指定选项值，以及如何提示用户输入值。
- 每个应用程序选项的数据定义。这些描述了程序参数，即程序可以接受或运行所需的数据。这包括输入和输出文件以及所有其他参数。
- 每个应用程序选项的数据类型，以及详细描述允许类型或值的属性，例如默认值以及数据是否必须在限制范围内。这些用于用户输入验证，以确保应用程序参数设置正确。
- 应用程序选项之间的依赖关系，例如仅在指定另一个值时才需要某个值，或者允许的值类型取决于另一个值的值或存在。例如，如果排列程序的输入序列是 DNA，则不应接受蛋白质比较矩阵。

运行应用程序时，ACD 文件会被读取，命令行会由 EMBOSS 内部的 ACD 文件解析器和命令行处理器自动处理。二者共同确保启动时所需信息可用。在应用程序启动前，所有必需的选项值都会根据需要提示输入。不正确或超出范围的输入值会自动重新提示。输入值会被读取并保存在内存中，文件会根据需要打开，等等，以便在应用程序实际运行时所有所需数据均可用。EMBOSS 应用程序在处理数小时后不能再向用户请求更多信息！

ACD 文件使用专为 EMBOSS 设计的 AJAX 命令定义（ACD）语言编写。ACD 语法允许对应用程序的选项及其命令行界面进行非常灵活的描述。它指定了可以出现在命令行或其他界面（例如网页）中的所有内容。提供了专门用于 Web、GUI 和其他类型界面的元数据。例如，单选按钮等图形元素是否适合用于设置选项值。这些元数据以及总体语法使界面开发人员能够轻松创建友好且直观的界面。有多种不同的界面可用（参见 EMBOSS 用户指南）。

应用程序选项和界面的描述通常涉及计算、条件语句以及变量和菜单的使用。ACD 语法支持所有这些操作，还允许你探测序列等输入数据类型的属性。ACD 文件支持各种生物学数据类型和多种不同的文件格式，为应用程序开发人员节省了大量工作。例如，生物序列可以从多种不同的格式读取，并使用多种不同的访问方法。对这些功能的使用对应用程序是透明的，并且无需在 ACD 文件中指定。

### 4.1.2 ACD 一般语法

ACD（附录 A，ACD 语法参考）是一种宽容的语言，除非严格必要，否则不会过度限制可用语法或布局。你不需要了解完整的语法就可以开始编写 ACD 文件；你需要的所有主要功能均已在下方总结。

提供了各种实用程序应用（第 4.6 节，“ACD 实用程序”）用于验证、调试和处理 ACD 文件。编写 ACD 文件后，可以使用这些工具对其进行验证并整齐地重新格式化。

### 4.1.2.1 ACD 文件名

ACD 文件是纯 ASCII 文本文件。它们必须具有 .acd 扩展名，并且通常与应用程序同名：

```
ApplicationName.acd
```

ApplicationName 是传递给函数 embInit 的名称，该函数从应用程序 C 源代码中调用 ACD 文件解析（参见第 4.2 节，“应用程序定义”）。

### 4.1.2.2 空白字符

在 ACD 文件解析期间，整个文件内容实际上被视为单个字符串，并被解析为由空格字符分隔的标记。各个标记之间只需要一个空格，额外的空白字符会被忽略。所有标记在最终解析为相应的数据类型之前都被视为字符串。解析时只进行一次遍历，因此任何元素（例如数据类型定义）必须在被引用之前声明。





### 4.1.2.3 注释

注释行可以添加，以“#”开头并持续到行尾：

```
# This is a valid comment line and will be ignored during ACD parsing.
```

### 4.1.3 ACD 定义

ACD 文件包含应用程序及其所有选项的定义。ACD 文件必须包含一个应用程序定义，然后为每个选项包含一个数据定义。定义包含一个或多个属性，每个属性都是一个 AttributeName: AttributeValue 对。应用程序定义必须首先给出，随后是组织成节（第 4.1.5 节，“ACD 文件节”）的数据定义。

应用程序定义（第 4.2 节，“应用程序定义”）的一般格式为：

```
application: ApplicationName
[
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
]
```

数据定义（第 4.2 节，“应用程序定义”）的一般格式为：

```
Datatype: OptionName
[
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
]
```

属性值通常用双引号括起来，尽管这仅对包含空格的值（通常是字符串）是强制性的。例如，这是一个有效的属性定义：

```
string: "A String Value"
```

这是一个无效的示例：

```
string: A String Value
```

application: 标记和表示数据类型的标记可以缩写，只要它们保持无歧义。例如：

```
appl:
```

有时会代替：

```
application:
```

同样，序列数据类型：

```
sequence:
seqset:
seqall:
```

原则上可以缩写为：

```
sequ
seqs
seqa.
```

属性也可以缩写。例如，用于为数据定义设置默认值的属性：

```
default:
```

可以缩写为：

```
def:
d:
```

不过，此类缩写*不*推荐，因为它们往往会使 ACD 文件更难以阅读。

### 4.1.4 参数和限定符

每个应用程序选项，即 ACD 文件中的每个数据定义，都可以通过相应的 ACD 属性定义为以下之一：

- 参数
- 标准限定符
- 附加限定符

默认值为：

- 高级限定符

使用的属性如下：

```
parameter:  "Y"
standard:   "Y"
additional: "Y"
```

parameter: "Y" 表示该数据定义是一个 _参数_。standard: "Y" 和 additional: "Y" 表示该数据定义是一个 _标准限定符_ 或 _附加限定符_。如果未指定 parameter: "Y"、standard: "Y" 或 additional: "Y" 中的任何一个，则该数据定义默认为 _高级限定符_。参数通常用于输入和输出文件以及其他主要输入和输出数据，而不同类型的限定符用于其他应用程序选项。

> **注意**
>
> 在数据定义中，parameter: "Y"、standard: "Y" 或 additional: "Y" 只能给出其中一个。如果使用了多个，ACD 处理过程中将生成错误消息。

> **注意**
>
> 不应显式指定 parameter: "N"、standard: "N" 或 additional: "N"。如果这样做，ACD 处理过程中将生成错误。实际上，计算出的“N”值确实受支持，并且可以在特殊情况下用于覆盖这些属性的默认行为（参见第 4.5 节，“控制提示”）。

> **注意**
>
> 在早期版本的 EMBOSS 中，使用了 required: 和 optional:。
>
> standard: 现在替代了 required:，additional: 替代了 optional:。

参数和限定符之间的区别在于，在命令行上指定参数值时不需要使用标志。值的指定方式如下：

```
_ApplicationName Option Value._
```

相比之下，指定限定符值时必须使用标志（选项名称）。标准、附加和高级限定符的值的指定方式如下：

```
ApplicationName -OptionName OptionValue.
```

标志（选项名称）也可以放在参数值之前，但不是必需的。但是，如果不为参数使用标志，则需要按照数据定义在 ACD 文件中出现的相同顺序给出值。

这简化了如何为应用程序参数分配值的视图。这里未描述更多可能性，特别是针对处理同一类型的多个选项。有关更多信息，请参阅 EMBOSS 用户指南。

### 4.1.4.1 提示行为和默认值

如果未在命令行上指定，则始终会提示输入参数和标准限定符的值。如果在 ACD 文件中指定了默认值，用户可以按 <回车> 键接受该值。

除非在命令行上给出 -options（这将为这些限定符打开提示），否则不会提示输入附加限定符的值（将改用默认值）。应始终通过指定 default: 属性在 ACD 文件中为附加限定符提供默认值。

即使使用 -options，也绝不会提示输入高级限定符，因此应在 ACD 文件中提供默认值。

### 4.1.4.2 帮助信息

当使用内置限定符 -help 运行程序时，会生成帮助信息。参数和标准限定符的帮助信息出现在帮助显示的“必需”部分中。附加和高级限定符的信息出现在“高级”部分中。

### 4.1.4.3 示例

以下 ACD 文件定义了一个带有序列参数（sequence）和标准限定符（thresh）的应用程序，用于设置评分阈值：

```
application: seqdemo
[
    documentation: "Demo application"
]
sequence: asequence
[
    parameter: "Y"
]
float: thresh
[
    standard: "Y"
```

## 4.1 ACD 文件开发简介

```
default: "2.5"
minimum: "0.0"
maximum: "100.0"
information: "Score threshold"
]
```

asequence 参数可以在不使用限定符名称（标志）的情况下设置，但 thresh 需要一个。该应用程序可以按以下方式调用：

```
seqdemo filename.seq -thresh 5
seqdemo filename.seq
```

在第一种情况下，直接设置 thresh。在第二种情况下，未设置它，用户将被提示输入一个值。
如果，相比之下，thresh 被定义为附加限定符：

```
float: thresh [
    additional: "Y"
    default: "2.5"
    minimum: "0.0"
    maximum: "100.0"
    information: "Score threshold"
]
```

只有在设置 -options 时，用户才会被提示输入一个值：

```
seqdemo filename.seq -options
```

以下 ACD 定义将定义一个高级限定符（abool）：

```
boolean: abool
[
    default: "Yes"
]
```

用户绝不会被提示输入 abool 的值，因此如果未在命令行上设置它，应用程序将使用默认值（“Yes”）继续。abool 可以按以下方式打开或关闭：

```
acdemo -asequence filename.seq -abool
acdemo -asequence filename.seq -noabool
```

### 4.1.5 ACD 文件节

### 4.1.5.1 ACD 文件中的节

EMBOSS 按 ACD 文件中出现的顺序处理 ACD 定义。然而，此顺序不足以让界面开发人员为用户界面构建整洁的选项分组。为了帮助界面开发人员，所有 ACD 数据定义都分组为五个主要节，必须按以下顺序出现：

- 1. 输入
- 2. 必需
- 3. 附加
- 4. 高级
- 5. 输出

节的形式如下：

```
section: input
[
    information: "Input section"
    type: "page"
]
#
# Input data definitions go here
#
endsection: input
```

ACD 文件中的所有数据定义 *必须* 包含在相应的节中，并且节必须按指示顺序给出。否则，ACD 处理过程中将生成错误（参见第 A.1.6 节，“ACD 文件节”）。

每个主要节可以在其中嵌套一个或多个子节，子节还可以根据需要包含进一步嵌套的子节，尽管这很少必要。与主要节不同，子节具有任意名称，可以按任何顺序给出。

有关这些节及其内容的详细描述，请参见第 A.1.6 节，“ACD 文件节”。

### 4.1.5.2 输入节

与输入相关的输入数据类型和其他数据定义。参见第 A.2.2 节，“输入 ACD 数据类型描述”。

### 4.1.5.3 必需节

始终需要用户提供值但不在输入或输出节中的选项。这包括所有定义为 *参数* 的数据定义以及所有定义为 *标准限定符* 的数据定义。





### 4.1.5.4 其他部分

用户偶尔设置的其他限定符。

### 4.1.5.5 高级部分

可以设置值但从不提示输入的高级限定符。它们由以下属性的缺失定义：

```
parameter: "Y"
standard: "Y"
additional: "Y"
```

### 4.1.5.6 输出部分

与输出相关的输出数据类型和其他参数。参见第 A.2.3 节，“输出 ACD 数据类型的描述”。

### 4.1.5.7 示例

wossname 应用程序的搜索输入字符串包含在输入部分中。输出部分包含与输出相关的所有参数和限定符，还包含一个名为 htmlsection 的子部分：

```
section: input
[
  information: "Input section"
  type: "page"
]

string: search
[
  parameter: "Y"
  default: ""
  information: "Text to search for, or blank to list all
  programs"

  help:"Enter a word or words here and a case-independent search
  for it will be made in the one-line documentation, group names and
  keywords of all of the EMBOSS programs. If no keyword is
  specified, all programs will be listed."
  knowntype: "emboss keyword"
]

endsection: input
.
.
section: output
[
  information: "Output section"
  type: "page"
]

outfile: outfile
[
additional: "Y"
default: "stdout"
knowntype: "wossname output"
]
section: htmlsection
[
information: "Html section"
type: "frame"
]
toggle: html
[
additional: "Y"
default: "N"
information: "Format the output for HTML"
help: "If you are sending the output to a file, this will format
it for displaying as a table in a WWW document."
outputmodifier: "Y"
]
boolean: groups
[
additional: "Y"
default: "N"
information: "Output only the group names"
help: "If you use this option, then only the group names will
output to the file"
outputmodifier: "Y"
]
boolean: alphabetic
[
additional: "Y"
default: "N"
information: "Output an alphabetic list of programs"
help: "If you use this option, then you will get a single list of
the program names and descriptions instead of the programs being
listed in their functional groups."
outputmodifier: "Y"
]
endsection: output
```

### 4.1.5.8 标准文件部分（sections.standard 文件）

所有部分和子部分都定义在 sections.standard 文件中，该文件存储在 EMBOSS 应用程序 ACD 文件目录中，例如：

```
../emboss/emboss/emboss/acd/sections.standard
```

此文件的摘录如下所示：

```
#
# ACD sections
#
# top level (page) sections
# =========================
additional page Additional section
advanced page Advanced section
input page Input section
output page Output section
required page Required section
#
#
# sub level (frame) sections
# ==========================
afeaturesection input First feature options
bfeaturesection input Second feature options
consensussection additional Consensus section
datasection output Data output section
fastalignsection additional Fast align options
```

该文件定义了顶级（页面）部分（‘输入’、‘必需’、‘其他’等）的允许顺序。该文件还定义了允许的子部分（在“# 子级（框架）部分”下给出），这些子部分已根据需要为各个应用程序定义和使用。行上的第一个标记是子部分名称。第二个标记是子部分所属的顶级部分：子部分不能出现在列出的任何其他部分中。行上的其余文本是对该部分的描述。

# 4 ACD 文件开发

## 4.2 应用程序定义

## 4.2.1 应用程序定义格式

ACD 文件中的第一个定义必须是应用程序定义。它由 application: 标记、与此 ACD 文件关联的应用程序名称以及方括号中的应用程序属性块组成。每个属性都是一个 name: value 对：

```
application: ApplicationName
[
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
]
```

例如，wossname 应用程序定义具有两个属性（documentation: 和 groups:）：

```
application: wossname
[
    documentation: "Finds programs by keywords"
    groups: "Display"
]
```

应用程序名称（ApplicationName）是任意的，但通常与 ACD 文件名相同。在程序初始化期间（参见第 6.3 节，“处理 ACD 文件”），将调用 embInit 函数以将 C 源代码与 ACD 文件关联并调用 ACD 文件处理。embInit 会传递要解析的 ACD 文件名，例如：

```
embInit("ApplicationName", argc, argv)
```

这使得可以为单个应用程序 C 源代码文件开发多个 ACD 文件（因此也可以开发多个命令行界面）。

> **注意**
> 
> embInit *不* 将 ApplicationName 与应用程序定义中 application: 标记后给出的字符串进行比较。

## 4.2.2 应用程序属性

应用程序属性用于描述应用程序本身的元数据。它们允许你设置诸如文档文本和应用程序所属组等内容。参见第 A.3 节，“应用程序属性”。

> **注意**
> 
> documentation:、keywords: 和 groups: 属性值得特别提及。wossname 程序会搜索它们的字符串值，给定一个关键字，将返回在 groups:、keywords: 或 documentation: 文本中包含该关键字的所有应用程序。
> groups: 字符串也由 seealso 应用程序使用，该应用程序获取 EMBOSS 程序的名称并返回与其共享某些功能的程序列表。

## 4.2.3 应用程序文档

documentation: 属性文本是对应用程序功能的简要描述，在运行程序或显示帮助时（当程序使用 -help 限定符运行时）打印到屏幕上。以下是 seqret 的应用程序定义：

```
application: seqret
[
    documentation: "Reads and writes (returns) a sequence"
    groups: "Edit"
]
```

上述 ACD 文件将在命令行中产生以下行为：

```
% seqret
Reads and writes (returns) a sequence
Input sequence :
```

如果缺少 documentation: 属性，则运行程序时会发出警告。字符串值必须符合某些约定（第 A.3 节，“应用程序属性”）。

### 4.2.3.1 应用程序关键字文件（keywords.standard）

keywords: 属性用于将关键字附加到属性。可给出的允许关键字定义在 keywords.standard 文件中，该文件安装在与 ACD 文件相同的目录中，例如：

```
../emboss/emboss/emboss/acd/Keywords.standard
```

文件如下所示：

```
#
# Application keywords
#
# Keywords are additional search terms to locate applications
# Valid group and subgroup names are not allowed. Keyword searches are
# expected to include the groups . Keywords defined here and in the
# application keywords: attribute are a few terms to be used where the
# short documentation string is not sufficient to identify an
# application by function.
```

你会发现当前未定义任何关键字。如果添加任何关键字，请在注释块之后每行给出一个关键字。

## 4.2.4 应用程序组

groups: 属性根据其功能将应用程序放入组或子组中。同一子组中的程序通常执行类似的操作或在同一常规区域内运行。groups: 属性的字符串值必须遵守某些约定（第 A.3 节，“应用程序属性”）。

一般格式如下：

```
application: ApplicationName
[
   groups: "GroupName1, GroupName2, ... : SubgroupName1, SubgroupName2, ... "
]
```

例如：

```
application: syco
[
   documentation: "Synonymous codon usage Gribsov statistic
   plot"
   groups: "Nucleic:Codon usage, Nucleic:Gene finding"
]
```

通常只指定一个组和子组。例如，以下 ACD 文件指示应用程序 pscan 属于 Protein 组和 Motifs 子组：

```
application: pscan
[
   documentation: "Scans proteins using PRINTS"
   groups: "Protein:Motifs"
]
```

通常只指定一个组也足够了，例如：

```
application: trimest
[
   documentation: "Trim poly-A tails off EST sequences"
   groups: "Edit"
]
```

### 4.2.4.1 应用程序组名称文件（groups.standard）

应用程序组已在其他地方广泛使用，因此 EMBOSS 现在使用一组标准组名称，ACD 文件中的所有组名称都将根据该组名称进行验证。该标准定义在 groups.standard 文件中，该文件安装在与 ACD 文件相同的目录中，例如：

```
.../emboss/emboss/emboss/acd/groups.standard
```

groups.standard 文件为每个有效的 group : 属性值包含一行。组和子组（如果指定）用 ':'（冒号）字符分隔，组或子组名称中的空格将替换为下划线字符 ('_')。还有一个简短的描述，说明可能会放置在组中的内容。文件摘录如下所示：


#
# 应用程序组
#
Acd ACD 文件实用程序
Alignment:Consensus 合并序列以生成共识序列
Alignment:Differences 查找序列之间的差异
Alignment:Dot_plots 点图序列比较
Alignment:Global 全局序列比对
Alignment:Local 局部序列比对
Alignment:Multiple 多序列比对
Display 出版质量的显示
Edit 序列编辑
Enzyme_Kinetics 酶动力学计算
Feature_tables 序列注释的操作和显示
.
.
.

如果指定了组和子组，例如：

```
Alignment : Consensus
```

则组名和子组名不得单独出现在 groups: 属性之后。例如，以下是有效的：

```
groups: "Alignment : Consensus"
```

但以下无效：

```
groups: "Alignment"
```

如果组字符串只有一级，即顶级组，例如：

```
Display
```

那么请不要为其添加子组。例如，以下无效：

```
Display : Features
```

强烈建议使用 groups.standard 中定义的组结构。但是，在编写完全新的程序类别时，请在开发者邮件列表 (emboss-dev(at emboss.open-bio.org)) 上讨论新组名的创建。

注意
groups.standard 中的组名由 EMBOSS 程序 wossname 和 sealso 报告。

## 4.3 数据定义

### 4.3.1 数据定义格式

每个应用程序选项都必须在 ACD 文件中定义。这些选项（或“数据定义”）的定义在文件中紧随应用程序定义之后。所有数据定义 *必须* 包含在适当的 ACD 文件节中（参见第 4.1.5 节，“ACD 文件节”）。否则，在 ACD 处理期间将生成错误。

数据定义的一般格式如下。第一个标记是 ACD 数据类型，第二个标记是选项名，随后是方括号内的数据属性。每个属性是一个名：值对：

```
Datatype: OptionName
[
  DataAttribute1Name: "DataAttribute1Value"
  DataAttribute2Name: "DataAttribute2Value"
]
```

Datatype 必须是有效的 ACD 数据类型（第 A.2 节，“数据类型”）。这些是预定义的，包括 integer 和 float 等简单类型，以及 sequence 等生物类型。还有其他类型可用于定义菜单（例如 list）之类的内容，并控制是否提示输入其他数据定义的值（例如 toggle）。

OptionName 是选项的名称，与 *限定符名*、*参数名* 或 *命令行标志* 同义。它用于从命令行引用数据定义。如果在选项之前指定了标志，则可以在命令行上设置任何选项的值：

```
`-OptionName OptionValue`
```

程序员必须在 C 源代码中对每个应用程序选项有一个句柄，标志也为此目的使用（参见第 6.3 节，“处理 ACD 文件”）。选项名可以是你喜欢的任何字符串，只要合理，但需符合某些约定（第 4.3.2 节，“参数命名约定”）。

属性（第 4.3.4 节，“数据属性类型”）让你控制应用程序参数。它们允许你指定诸如“帮助”文档、默认值以及正确值的要求，例如可设置允许的值范围（最大值和最小值）。它们还允许应用程序程序员控制如何提示用户输入值（如果有的话）（第 4.5 节，“控制提示”）。

属性值是用双引号括起来的字符串，在 ACD 文件处理期间可能会根据其出现的数据定义解析为其他类型。例如，这定义了一个默认值：

```
default: "5.0"
```

如果上述内容出现在浮点数（float:）的定义中，则它在内部将作为浮点数保存。

### 示例

wossname 有一个字符串输入参数（search），字符串定义有五个属性（parameter:, default:, information:, help: 和 knowntype:）：

```
string: search
[
    parameter: "Y"
    default: ""
    information: "Text to search for, or blank to list all
    programs"
    help: "Enter a word or words here and a case-independent search
    for it will be made in the one-line documentation, group names and
    keywords of all of the EMBOSS programs. If no keyword is
    specified, all programs will be listed."
    knowntype: "emboss keyword"
]
```

### 4.3.2 参数命名约定

ACD 数据定义的限定符或参数名（命令行标志）必须是不含空白字符的小写字母数字字符串。理论上它可以是任意长度。在实践中，存在约定（第 A.1 节，“ACD 语法简介”），强烈建议你遵循这些约定。在某些情况下，如果不遵循，在 ACD 处理期间（即解析 ACD 文件时，通常在应用程序运行后）将生成警告或错误消息。

例如，序列数据类型（输入序列）的常规名称是 sequence 或 *序列，而 seqout（输出序列）的常规名称是 outseq 或 *输出序列。换句话说，如果在 ACD 文件中指定了多个同一数据类型的实例，则可以将字符 a、b 等预加到标志上。例如，在指定多个序列时，请使用 asequence、bsequence 等；在指定多个序列输出流时，请使用 aoutseq、boutseq 等。你可以在 matcher 应用程序中看到这一点，它接受两个输入序列：

```
sequence: asequence
[
    parameter: "Y"
    type: "protein"
]
```

```
sequence: bsequence
[
   parameter: "Y"
   type: "stopprotein"
]
```

### 4.3.3 ACD 数据类型

#### 4.3.3.1 ACD 数据类型的分组

为方便起见，可用的 ACD 数据类型按反映相似属性或使用模式的五个分组组织如下：

- 简单数据类型
- 输入数据类型
- 选择数据类型
- 输出数据类型
- 图形数据类型。

下面描述了这些分组。有关数据类型（包括其数据值、默认值和关键属性）的完整描述，请参见第 A.2 节，“数据类型”。

#### 4.3.3.2 简单 ACD 数据类型

简单数据类型（第 A.2.1 节，“简单 ACD 数据类型描述”）包括原始类型和一些派生类型：

| boolean | 简单布尔值 |
| float | 简单浮点数 |
| integer | 简单整数 |
| string | 简单字符串 |
| toggle | 用于控制其他参数的简单布尔开关 |
| array | 整数或浮点数列表 |
| range | 序列位置范围 |
| regexp | 正则表达式模式 |
| pattern | 序列模式 |

#### 4.3.3.3 输入 ACD 数据类型

输入数据类型（第 A.2.2 节，“输入 ACD 数据类型描述”）用于输入序列、序列特征、文件和目录、特定于 **phylipnew** EMBASSY 包的输入、数据文件和其他生物数据文件。

##### 4.3.3.3.1 序列输入

对于生物序列输入，请使用：

- `sequence`: 用于读取的单个序列
- `seqall`: 一组单个序列，逐个寻址
- `seqset`: 一组可以同时使用的单个序列
- `seqsetall`: 一个或多个可以同时使用的单个序列集

在所有情况下，数据值都是输入序列流的统一序列地址 (USA)。USA 规范在 _EMBOSS 用户指南_ 中有描述。

##### 4.3.3.3.2 特征输入

对于生物序列特征输入，请使用：

- `features`: 任何支持的特征格式中的序列特征注释

在所有情况下，数据值都是输入序列特征流的统一特征对象 (UFO)。UFO 规范在 _EMBOSS 用户指南_ 中有描述。

##### 4.3.3.3.3 文件和目录

对于常规输入文件和目录，请使用：

- `directory`: 可用于输入或输出的目录
- `dirlist`: 从目录读取的文件名列表
- `filelist`: 输入文件列表
- `infile`: 与序列无关的输入文件

在所有情况下，数据值都是任何有效的文件或目录名。

##### 4.3.3.3.4 数据文件

对于输入数据文件，请使用：

- `datafile`: 从标准 EMBOSS 数据搜索路径读取的格式化数据文件
- `matrix`: 比较矩阵文件（整数值）
- `matrixf`: 比较矩阵文件（浮点值）

在所有情况下，数据值都是 EMBOSS 数据搜索路径中的文件名（参见 _EMBOSS 用户指南_）。

通常，在指定比较矩阵时，还需要间隙罚分。这些必须在一个或多个其他数据定义中单独指定。




## 4.3.3.3.5 phylipnew EMBASSY 包

以下是特定于 **phylipnew** EMBASSY 包的输入数据类型。它们允许进行详细的类型检查，以及检测和验证 **phylip** 支持的各种替代格式，而无需复杂的额外命令行选项。

- `discretestates`: 离散状态文件
- `distances`: 距离矩阵
- `frequencies`: 频率值
- `properties`: 属性值
- `tree`: 系统进化树

在所有情况下，数据值均为任意有效文件名。

## 4.3.3.3.6 其他生物学输入

其他生物学输入数据类型包括：

- `codon`: 密码子使用表文件
- `cpdb`: 蛋白质坐标数据
- `scop`: SCOP 和 CATH 域分类信息

在所有情况下，数据值均为任意有效文件名。

## 4.3.3.4 输出 ACD 数据类型

输出数据类型（第 A.2.3 节，“输出 ACD 数据类型描述”）用于输出序列、序列特征、比对、文件和目录、特定于 **phylipnew** EMBASSY 包的输出、数据文件、其他生物数据文件以及格式化的应用程序输出文件（报告）。

### 4.3.3.4.1 序列输出

对于生物序列输出，请使用：

- `seqout`: 单个序列的输出文件
- `seqoutall`: 多个序列的输出文件
- `seqoutset`: 存储在内存中的单个序列集合，将写入文件

这些数据类型的行为相同，但它们是为了与输入序列数据类型保持一致而提供的（见上文）。在所有情况下，数据值均为输出序列流的统一序列地址（USA）（参见 *EMBOSS 用户指南*）。

输出序列默认使用 FASTA 格式。格式通常在命令行中设置，但默认值可以通过 `osformat:` 硬编码（参见第 4.3.6.2.2 节，“特征输出”）。

### 4.3.3.4.2 特征

对于生物序列特征输出，请使用：

- `featout`: 序列特征注释的输出文件

数据值为输出序列特征流的统一特征对象（UFO）（参见 EMBOSS 用户指南）。

### 4.3.3.4.3 比对

对于比对输出，请使用：

- `align`: 序列比对的输出文件

数据值为任意有效文件名。

### 4.3.3.4.4 输出文件和目录

对于常规输出文件和目录，请使用：

- `outdir`: 用于写入多个输出文件的输出目录
- `outfile`: 常规输出文件
- `outfileall`: 多个常规输出文件

outfile 和 outfileall 用于其他输出 ACD 数据类型未涵盖的数据。例如，输出文件通常不包含序列数据。它们适用于纯文本的常规应用程序输出。

数据值为任意有效文件名。

### 4.3.3.4.5 输出数据文件

对于输出数据文件，请使用：

- `outdata`: 格式整齐的表格或列表数据的输出文件
- `outmatrix`: 整数比较矩阵数据的输出文件
- `outmatrixf`: 浮点比较矩阵数据的输出文件

在所有情况下，数据值均为任意有效文件名。

### 4.3.3.4.6 phylipnew EMBASSY 包

特定于 phylipnew EMBASSY 包的输出数据类型允许 EMBOSS 提供详细的类型检查，并自动检测和验证 phylip 支持的各种替代格式，而无需复杂的额外命令行选项。

| 数据类型 | 描述 |
| --- | --- |
| outdiscrete | 系统进化离散特征数据的输出文件 |
| outdistance | 系统进化距离矩阵数据的输出文件 |
| outfreq | 系统进化字符频率数据的输出文件 |
| outproperties | 系统进化属性数据的输出文件 |
| outtree | 系统进化树数据的输出文件 |

在所有情况下，数据值均为任意有效文件名。

### 4.3.3.4.7 其他生物学输出

其他生物学输出数据类型包括：

| 数据类型 | 描述 |
| --- | --- |
| outcodon | 密码子使用数据的输出文件 |
| outcpdb | 蛋白质坐标数据的输出文件 |
| outscop | SCOP 和 CATH 域分类信息的输出文件 |

数据值为任意有效文件名。

### 4.3.3.4.8 报告输出

对于格式化的应用程序输出，请使用：

| 数据类型 | 描述 |
| --- | --- |
| report | 序列注释的输出文件 |

数据值为任意有效文件名。

## 4.3.3.5 选择 ACD 数据类型

选择数据类型用于菜单（第 A.2.4.2 节，“选择”）。

用户会看到一个可供选择的有限选项列表。选项由标签和描述文本组成。可以选择一个或多个选项。选择数据类型包括：

| 数据类型 | 描述 |
| --- | --- |
| list | 带有文本标签的选项列表（通常为简洁的文本描述） |
| selection | 带有自动生成数字标签的选项列表（通常为详细的文本描述） |

数据值为一个（或多个）有效选项。选项通过标签（无论是文本还是数字）或标签后给出的描述文本本身的非歧义部分来指定。如果允许多选，则用户必须提供逗号分隔的选项列表。

## 4.3.3.6 图形 ACD 数据类型

图形数据类型用于图形输出（第 A.2.5 节，“图形 ACD 数据类型描述”）。

- `graph`: 任意类型的图形输出
- `xygraph`: 作为简单二维（2D）XY 图的图形输出，序列沿 x 轴排列

数据值为受支持的图形设备（第 A.2.5 节，“图形 ACD 数据类型描述”）。

## 4.3.4 数据属性类型

数据定义可定义三种基本类型的属性：

- 全局属性（第 A.4 节，“全局属性”）
- 数据类型特定属性（第 A.5 节，“数据类型特定属性”）
- 计算属性（第 A.6 节，“计算属性”）
- 作为属性定义的数据类型关联限定符（第 A.2 节，“数据类型”）

全局属性适用于所有数据类型，可以在任何 ACD 数据定义中定义。相比之下，数据类型特定属性仅适用于某些数据类型。每个 ACD 数据类型都有自己的一组特定属性。全局属性和数据类型特定属性的值在 ACD 文件中显式设置。

计算属性是一种数据类型特定属性，在数据定义处理（读取和验证）后赋值，例如，在从文件读取序列后。这允许数据定义引用那些值在事先未知但取决于输入数据的属性，并在 ACD 文件处理过程中自动计算。

数据类型关联限定符（或简称关联限定符）是某些 ACD 数据类型内置的命令行限定符。然而，它们也可以“硬编码”，即在相应的数据定义中定义为属性。

## 4.3.5 全局属性

全局属性适用于所有数据类型。它们可以在任何 ACD 数据定义中定义，其值在 ACD 文件中显式设置（第 A.4 节，“全局属性”）。全局属性如下：

```
GlobalAttributeName: "Value"
```

大多数全局属性具有字符串或布尔值。布尔值具有硬编码的默认值，可以通过 "Y"、"Yes"、"N" 或 "No" 覆盖（字符串不区分大小写）。因此，以下所有属性均有效：

```
parameter: "YES"
parameter: "Yes"
parameter: "Y"
parameter: "NO"
parameter: "No"
parameter: "N"
```

全局属性摘要如下。为方便起见，它们按功能分组如下：

- 参数和限定符
- 用户提示
- 数据类型定义
- 帮助信息和文档
- GUI 提示
- 供 SOAPLAB 使用。

### 4.3.5.1 参数和限定符

每个应用程序参数，即 ACD 文件中的每个数据定义，可以通过相应的全局属性定义为“参数”、“标准限定符”或“附加限定符”之一，默认值为“高级限定符”。

```
parameter:       "Boolean"
standard:        "Boolean"
additional:      "Boolean"
```

默认值为 "N"；但是，这在 ACD 文件中从不显式指定。

### 4.3.5.1.1 何时使用参数

### 报告

报告数据类型（如果使用）通常是应用程序的主要输出，因此应使用 parameter: 属性将其定义为参数。第一个报告文件必须定义为 parameter:（否则在 ACD 处理期间会生成错误）。建议后续报告定义（第二个、第三个等）也定义为参数（如果不这样做，在 ACD 处理期间会生成警告）。例外情况是如果设置了 default: 或 nullok: 属性，在这种情况下不会生成警告或错误消息，因为应用程序可以使用默认值运行，或者可以没有该定义的任何值。

### 序列

序列输入（sequence、seqall、seqsetall 或 seqset ACD 数据类型）和输出（seqout、seqoutall 和 seqoutset ACD 数据类型）通常是 EMBOSS 应用程序的主要输入或输出，因此应与上面的报告数据类型一样定义为参数。

### 特征

序列特征（如果使用）通常是主要输入（feature ACD 数据类型）或输出（featout），因此应与报告数据类型一样定义为参数。





## 比对

align 数据类型，在使用时，通常是主要输出，应定义为参数。第一个及后续的比对输出应定义为参数类型，如果未定义，在 ACD 处理期间将生成警告。例外情况是如果设置了 default: 或 nullok: 属性，在这种情况下，由于应用程序可以使用默认值运行或可以没有该定义的任何值运行，因此不会生成警告或错误消息。

## 文件

文件数据类型，在使用时，通常是主要输入（infile、filelist、directory 或 dirlist ACD 数据类型）或输出（outdir ACD 数据类型），应以与上述报告数据类型相同的方式定义为参数。

### 4.3.5.2 用户提示

属性用于提供将在屏幕上用于提示用户输入值的文本。提示是否出现取决于选项是定义为参数还是限定符类型之一（见上文），以及取决于用于调用应用程序的命令（即指定了哪些选项）。在某些情况下，提示是否出现可能取决于其他输入的值。有关更多信息，请参见第 4.5 节“控制提示”。使用的属性如下：

```
information: "String"
code: "String"
prompt: "String"
```

code:、prompt: 或 information 中只能定义一个。推荐使用 information:（带有标准名称，见下文）。在实践中，prompt: 仅在极少数情况下才需要，即 information: 字符串可能具有误导性的情况。

大多数常见数据类型都为 information: 字符串定义了默认值（参见第 4.3.5.2.1 节“标准提示文件 (codes.english)”），并应使用该值。如果在 ACD 处理期间 information: 属性缺失，或使用的值不是标准值（在有标准值可用的情况下），将生成警告。

如果使用非标准提示，则 information: 属性后给出的文本应符合某些约定（第 A.4.4.1 节‘information: "String" ("")’）。

在以下示例中，为 asequence 定义了非标准提示。如果尝试运行此示例，将生成警告：

```
sequence: asequence
[
    standard: "Y"
    information: "Enter filename"
]
```

在下一个示例中，未指定 information: 字符串，因此将改用来自 codes.english 的标准提示“Read sequence from”：

```
sequence: asequence
[
  standard: "Y"
]
```

### 4.3.5.2.1 标准提示文件 (codes.english)

为提供标准提示，大多数常见数据类型都为 information: 字符串定义了默认值。默认值位于 EMBOSS 系统文件 codes.english 中，路径为应用程序 ACD 文件目录，例如：

```
../emboss/emboss/emboss/acd/codes.english
```

提示出现在以 DEF DatatypeName 开头的行中，其中 DatatypeName 是 ACD 数据类型的名称。该文件还包含针对单个数据类型特定实例的一些其他标准提示，由代码（不以 DEF 开头）标识。这些提示可以与 code: 属性一起使用，例如 code: "GAP"。

文件摘录如下：

```
#
# This is the EMBOSS coded prompts file. Any messages found here will
# override those in the .acd file, and can be translated into other
# languages. The file extension (default "english") is set by the
# variable "emboss_language"
#
# Messages are referred to by .acd files as code: NAME
#
# DEFXXXX codes are automatically searched for ACD type XXXX if there
# is no information (or prompt) defined in the ACD file of as a
# standard prompt for the ACD type.
#
# HELPXXXX codes are automatically searched for ACD type XXXX if there
# is no help text in the ACD file.
#
# Default prompts: these are used where no prompt for a data type
# has been provided.
DEFALIGN	"Write output alignment to"
DEFREPORT	"Write output report to"
DEFINTEGER	"Enter a number"
DEFFLOAT	"Enter a number"
DEFBOOL	"Yes or No"
.
.
.
# Gap penalties
GAP	"What gap penalty"
GAPEXT	"What gap extension penalty"
```

### 4.3.5.3 数据类型定义

五个全局属性涉及数据：

```
knowntype: "String"
default: "Value"
relations: "String"
outputmodifier: "Boolean"
missing: "Boolean"
```

knowntype: 描述数据类型，应在类型本身不明显时定义。它通常为 string:、infile:、outfile: 和 outfileall 数据类型定义，但例如不为 sequence: 定义。

有效的已知类型字符串列在文件 knowntypes.standard 中（其他属性用于设置默认值 (default:)、描述与其他数据定义的关系 (relations:)、控制写入哪些字段 (outputmodifier:) 以及是否可以指定 NULL 值 (missing:)。还接受少数其他值，例如 outfile 数据类型的“ApplicationName output”。这些与数据类型一起记录（第 A.2 节“数据类型”）。

### 注意

如果给出的值不是标准已知类型或其他可接受值，则在 ACD 处理期间将生成警告消息。acdvalid 实用程序将检查 ACD 文件中的所有 knowntype 值，并报告需要已知类型的数据定义中缺失的任何值。

### 4.3.5.3.1 应用数据已知类型文件 (knowntypes.standard)

标准值（已知类型）从 EMBOSS 系统文件 knowntypes.standard 读取，该文件位于应用程序 ACD 文件目录中：

```
../emboss/emboss/emboss/acd
```

| # 已知类型 | | |
| --- | --- | --- |
| # 已知类型字符串 | 类型 | 注释 |
| aaindex_data | file | AAINDEX 条目 |
| aaindex_database | file | AAINDEX 数据库 |
| abi_trace | file | ABI 测序痕迹 |
| ajint_ajlong_data | file | 关于 ajint 和 ajlong 的标准格式信息 |
| alistat_input | file | HMMER alistat 程序输入 |
| alistat_output | file | HMMER alistat 程序输出 |
| amino_acid_classification | file | 氨基酸化学类别数据 |
| . | | |
| . | | |
| . | | |

### 4.3.5.4 帮助信息和文档

每个 EMBOSS 应用程序都接受全局限定符 `-help` 和 `-verbose`，后者与前者结合使用（如果使用的话）。当应用程序使用 `-help` 运行时，将向屏幕打印有用信息，包括所有程序参数和限定符，旁边有解释性文本。

以下属性定义了使用的文本：

```
help: "String"
valid: "String"
expected: "String"
```

help: 通常仅在需要更深入解释应用程序参数时定义。如果未定义 `help:`，则将改用 `information:` 属性的值（如果可用）或默认帮助字符串（见下文）。`help:` 字符串必须符合某些约定（第 A.4.6.1 节‘help: "String" ("")’）。`valid:` 和 `expected:` 用于描述在线文档中允许和预期的值。通常不需要它们，因为在大多数情况下，合理的值从其他属性中很明显。

`help:` 有用的示例：

```
integer: window
[
    standard: "N"
    default: 10
    minimum: 5
    maximum: 100
    information: "Window size"
    help: "Number of residues used to calculate the value for each point"
]
```

### 4.3.5.4.1 标准帮助字符串文件 (codes.english)

默认帮助字符串在 EMBOSS 系统文件 `codes.english` 中为每个数据类型给出（参见第 4.3.5.2.1 节“标准提示文件 (`codes.english`)”）。它们的一般形式为：

```
HELPDatatypeName
```

其中 `DatatypeName` 是 ACD 数据类型的名称。

例如：

```
HELPSEQUENCE "Sequence USA"
HELPDIRECTORY "Directory name"
```

### 4.3.5.5 GUI 提示

needed: 全局属性指示参数是否预期包含在 GUI 表单中。它用于帮助 GUI 开发者。某些数据类型特定属性，例如可为选择列表定义的 button:，也用于提供此类提示。参见第 A.5 节“数据类型特定属性”。

属性定义如下：

```
needed: "Boolean" ("Y")
```

### 4.3.5.6 供 SOAPLAB 使用

以下属性为 SOAPLAB 项目提供元数据。它们不直接由 EMBOSS 使用，不应出现在标准 EMBOSS 应用程序 ACD 文件中。
属性定义如下：

```
qualifier: "String"
template: "String"
comment: "String"
```

### 4.3.6 数据类型特定属性

ACD 数据定义中给出的数据类型特定属性定义应用程序选项的特性。它们控制以下事项：

- 输入和输出文件的名称和位置
- 对输入的详细类型检查，以确保数据符合应用程序要求
- 输出生成的确切数据
- 命令行用户界面的外观和行为
- 用户输入验证，例如确保用户输入在允许范围内
- 应用程序输出验证，例如确保输出符合预期
- 图形界面建议

数据类型特定属性为单个数据类型或相关数据类型组定义。下表总结了每个数据类型的关键属性。有关所有可用属性的描述，请参见第 A.5 节“数据类型特定属性”。

### 4.3.6.1 简单 ACD 数据类型的属性

这些用于验证用户输入。





## 4.3.6.1.1 用户输入验证

minimum: 和 maximum: 可定义于多种数据类型，用于限制值在给定范围内。可用于控制正则表达式或序列模式长度（minlength: 和 maxlength）及大小写（upper: "Y" 或 lower: "Y”）的属性，适用于 regexp 和 pattern 数据类型。

如有需要，可使用正则表达式来验证字符串。

## 4.3.6.2 输入 ACD 数据类型的属性

这些属性用于指定输入数据并验证用户输入。

### 4.3.6.2.1 序列输入

sask: 适用于所有序列输入，并设置 -sask 限定符的默认值。如果设置为 "Y"，则指定将提示输入序列的起始和结束位置，以及核苷酸序列的反转。

序列输入数据类型（sequence、seqall、seqset 和 seqsetall）共享一组用于定义和验证序列输入的通用属性。可通过 type: 限制序列类型，例如程序仅接受 DNA 序列。类型必须是标准序列类型，例如 dna、pureprotein、gaprna 等。参见第 A.7 节 "序列类型"。

### 4.3.6.2.2 特征输入

对于所有序列输入（sequence、seqall、seqset 和 seqsetall 数据类型），如果设置了 features: 属性，则可以读取序列特征（第 6.9 节 "特征处理"）。

可通过设置 type: 来限制特征类型。例如，可以使程序仅接受 DNA 特征。特征类型必须是 protein 或 nucleotide 之一。基于输入序列的类型（如适用）存在默认值，但应指定一个值。如果未为输入特征指定类型，且没有可用于获取默认类型的序列输入，则在 ACD 处理期间将生成错误。

### 4.3.6.2.3 phylip EMBASSY 包

phylip 包数据类型的属性提供详细的类型检查，并可以自动检测和验证 phylip 支持的各种替代格式，而无需复杂的额外命令行选项。参见第 A.5 节 "数据类型特定属性"。

length: 指定每组的属性值数量（properties 数据类型）或每组的频率位点/值数量（frequencies 数据类型）。

size: 指定离散状态集的数量（discretestates 数据类型）、频率集的数量（frequencies 数据类型）或树的数量（tree 数据类型）。

### 4.3.6.2.4 输入文件命名

name:、extension: 和 directory: 或 fullpath: 属性定义于多种数据类型，用于定义输入文件和目录数据类型的名称和位置。在某些情况下，可用默认命名方案或硬编码默认值，但可以通过使用这些属性来覆盖。还可以通过定义 default: 全局属性来设置输入文件名的默认值。例如，数据文件通常具有硬编码文件名，您可以使用 name: 或 default: 自由定义。

在可用默认文件命名方案，但 ACD 文件中也指定了默认值的情况下，如果命令行上给出的参数为空值（""），则可以覆盖 ACD 文件中的默认值并使用命名方案。对于此类数据定义，有必要设置全局属性 missing:。

### 4.3.6.2.5 缺失的输入文件

nullok: 适用于大多数输入数据类型。它是一个布尔属性，用于指定是否接受缺失的输入文件。如果应用程序可以接受此定义的空值，并且可以在没有相应输入文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或者，如果指定了默认值，则可以在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）以指定输入文件不可用。

### 4.3.6.2.6 输入文件数据类型标识

参见第 4.3.5.3 节 "数据类型定义"。

## 4.3.6.3 输出 ACD 数据类型的属性

这些属性用于指定输出文件，在某些情况下还用于指定生成的数据及其验证方式。

### 4.3.6.3.1 序列和序列特征输出

对于序列和特征输出数据类型（featout、seqout、seqoutset 和 seqoutall），如果 ACD 文件中未定义 name: 属性，则将默认为读取的第一个序列的名称（如果可用）。

可通过设置 type: 来限制序列类型。应用程序将验证输出是否为指定类型。类型必须是标准序列类型（参见第 A.7 节 "序列类型"）。

如果未为输出序列指定类型，且没有可用于获取默认类型的序列输入，则在 ACD 处理期间将生成错误。

### 4.3.6.3.2 特征输出

如果设置了 features: 属性，则可以将序列特征与输出序列一起写入（seqout、seqoutall 和 seqoutset 数据类型）。对于所有这些数据类型，可使用 osformat: 指定默认数据格式，该格式可由 -osformat 关联限定符覆盖。

可通过设置 type: 来限制特征类型。基于输入序列的类型（如适用）存在默认值，但应为验证目的指定类型。特征类型必须是 protein 或 nucleotide 之一。如果未为输出特征指定类型，且没有可用于获取默认类型的序列输入，则在 ACD 处理期间将生成错误。

### 4.3.6.3.3 比对输出

任何 seqset 或 seqsetall 数据类型都必须设置 aligned: 属性，否则在 ACD 处理期间将生成错误。

可使用 aformat: 属性设置比对格式。

对于 align 数据定义，minseqs: 和 maxseqs: 设置预期的最小和最大序列数量。如果输出可以包含来自同一输入的多个比对，则应将 multiple: 布尔属性设置为 "Y"。

### 4.3.6.3.4 报告输出

report 数据类型的属性包括：

- **rformat:** 指定要使用的报告格式，必须是受支持的报告格式之一（参见 *EMBOSS 用户指南*）
- **type:** 定义为 "protein" 或 "nucleotide" 之一，前提是报告格式是标准特征表格式之一（参见 *EMBOSS 用户指南*）
- **taglist:** 定义要在输出中报告的内部特征表中的标签/值对。

### 4.3.6.3.5 输出文件命名

输出文件名由 name: 和 extension: 值构成，格式为：

```
name.extension
```

名称和扩展名可能具有默认值。例如，对于 outcodon 数据类型，name: 默认为 outfile，extension: 默认为格式名称，且 cut 定义为默认输出格式。

在可用默认文件命名方案，但 ACD 文件中也指定了默认值的情况下，如果命令行上给出的参数为空值（""），则可以覆盖默认值并使用命名方案。对于此类数据定义，有必要设置全局属性 missing:。

数据类型特定的命令行限定符（参见 *EMBOSS 用户指南*）也可用于命名输出文件，可以通过在命令行上指定限定符，或在 ACD 文件中将其作为属性硬编码。例如，如果指定了限定符 -aname 和 -aextension，则构建格式为 aname.aextension 的比对文件名。值可以使用相应的 aname: 和 aextension: 属性进行硬编码。

还可以通过定义 default: 全局属性来设置输出文件名的默认值。

### 4.3.6.3.6 缺失的输出文件

nullok: 和 nulldefault: 适用于所有输出数据类型。如果应用程序可以接受数据定义的空值，并且可以在不生成相应输出文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或使用 -noFlag（其中 Flag 是数据定义标志）运行应用程序，以指定不生成输出文件。

nulldefault: 覆盖默认名称生成，并将空字符串（无输出文件）用作仅偶尔需要比对文件的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。

### 4.3.6.3.7 输出数据类型标识

使用 knowntype: 识别数据类型。参见第 4.3.5.3 节 "数据类型定义"。

### 4.3.6.3.8 输出数据规范

可使用属性来精确控制生成的数据并验证该数据。例如，比对输出文件的定义方式与普通输出文件（outfile 数据类型）相同，但具有额外属性，以允许选择比对格式，并为验证目的指定预期的比对序列数量。同样，报告输出文件的定义方式与普通输出文件（outfile）相同，但具有额外限定符，以允许选择报告格式。

codon、cpdb 和 scop 数据类型的默认数据格式可以使用 oformat: 指定，该格式可由 -oformat 关联限定符覆盖。

## 4.3.6.4 选择 ACD 数据类型的属性

这些属性控制向用户呈现的菜单（选项列表）的各个方面。例如，菜单上方显示的文本、用户输入的验证方式、选择的最小和最大数量以及选项是否区分大小写。

例如，请考虑此 ACD 列表定义：

```
list: matrix
[
    default: "blosum"        # default value
    minimum: 1 maximum: 1    # must select exactly 1
    header: "Comparison matrices" # printed before list
    values: "B:blosum, P:pam, I:id" # 3 valid values
    delim: ","               # delimiter default ";"
    codedelim: ":"           # label delimiter default ":"
    prompt: "Select one"     # prompt after list
    button: Y                # use radio buttons rather than checkboxes in HTML,
                             # ignored by ACD.
]
```

屏幕上显示的内容如下：

```
Comparison matrices
    B : blosum
    P : pam
    I : id
Select one [blosum] : PAM
```

使用此 ACD 列表定义：


select: matrix
[
    default: "blosum"    # 默认值
    minimum: "1" maximum: "1"    # 必须恰好选择 1 个
    header: "Comparison matrices"    # 列表前打印
    values: "blosum, pam, id"    # 有效值
    delimiter: ","    # 分隔符，默认 ";"
    information: "Select one"    # 列表后提示
    button: "Y"    # 在 HTML 中使用单选按钮而非复选框，
    ignored by ACD
]

你会得到：

比较矩阵
1 : blosum
2 : pam
3 : id
选择一个 [blosum] : PAM

## 4.3.6.5 图形 ACD 数据类型的属性

这些属性指定要输出的图形数据。

gtitle: 指定图形或 graphxy 数据类型的图形标题。可以设置许多其他图形元素。

multiple: 指定单个图形或 graphxy 数据类型输出中多个图形的数量。

## 4.3.7 数据类型关联限定符的属性

某些 ACD 数据类型内置了各种命令行限定符。这些数据类型关联限定符通常仅在命令行上指定。但是，它们也可以作为属性‘hard-coded’在相应的数据定义中，有时这样做是可取的。下面显示了设置文件格式的一些示例：

| 输入序列 | -sformat |
|---|---|
| | sformat: |
| 输出序列 | -osformat |
| | osformat: |
| 输出比对 | -aformat |
| | aformat: |
| 报告输出文件 | -rformat |
| | rformat: |
| 序列特征输入 | -fformat |
| | fformat: |
| 序列特征输出 | -oformat |
| | oformat: |

这些限定符在《EMBOSS 用户指南》中有更详细的描述。

## 4.3.8 计算属性简介

计算属性是数据类型特定的属性，在 ACD 文件处理期间读取输入文件 _after_ 被赋值。这些值是从 ACD 数据定义所引用的实际数据中计算或提取的。

大多数计算属性用于序列输入（`sequence`、`seqall`、`seqset` 和 `seqsetall`）以及序列特征输入（`features`）的数据类型。例如，对于序列数据类型，一旦读取了序列文件或其中的条目，序列的长度和类型即可用。

有关可用计算属性的完整描述，请参见第 A.6 节，“计算属性”。

### 4.3.8.1 检索计算属性的值

计算属性的值通过操作（第 4.4 节，“操作”）从 ACD 文件内部检索。该操作使用前面带有美元符号（`$`）并用括号括起来的 `ParameterName.AttributeName` 术语：

```
$(ParameterName.AttributeName)
```

`$` 语法表示“获取值，即括号内括起来的术语。

这通常是在依赖于其他数据定义的计算属性值的数据定义内部完成的。例如，以下 ACD 文件摘录定义了一个序列参数和一个整数窗口：

```
sequence: sequence
[
    parameter: "Y"
    type: pureprotein
]

integer: window
[
    standard: "Y"
    default: "10"
    maximum: "$(sequence.length)"
]
```

通过使用 `maximum: "$(sequence.length)"`，正在将最大窗口大小（`window` 数据类型的 `maximum` 属性）设置为序列的长度。

### 4.3.8.2 序列计算属性

所有序列输入数据类型：
- sequence
- seqall
- seqset
- seqsetall

都有六个计算属性，这些属性是输入序列的属性，可以在 ACD 中查询：

| 属性 | 描述 |
|---|---|
| begin | 起始残基（-sbegin 值） |
| end | 结束残基（-send 值） |
| length | 长度 |
| protein | 布尔值，如果序列是蛋白质则为 True |
| nucleic | 布尔值，如果序列是核酸则为 True |
| name | 名称 |

假设我们定义了一个名为 asequence 的序列输入，并且有一个看起来如下的 ACD 文件：

```
sequence: asequence
[
   parameter: "y"
   type: protein
]
```

这些属性将按以下方式引用：

- asequence.begin
- asequence.end
- asequence.length
- asequence.protein
- asequence.nucleic
- asequence.name

> **注意**
>
> **begin** 和 **end** 属性的值可以通过在命令行上指定 -sbegin 或 -send 来设置，它们是序列类型的内置限定符。

seqset 和 seqsetall 数据类型具有以下计算属性：

| 属性 | 描述 |
|---|---|
| totweight | 序列集的总序列权重 |
| count | 集中的序列数量 |

seqsetall 还具有：

| 属性 | 描述 |
|---|---|
| multicount | 序列集的数量 |

要检索上面所示的 asequence 定义中的计算属性值，可以使用：

```
$(asequence.begin)
$(asequence.end)
$(asequence.length)
```

### 示例

在编写将一个序列插入到另一个序列的程序时，确保插入位置不大于第一个序列长度的一种方法是使用如下代码：

```
if (position > ajSeqGetLen(seq))
    ajFatal("Insertion position out of bounds");
```

问题是，在用户费尽周折配置应用程序（输入所有输入）后，程序可能会过早终止。更好的做法是界面强制正确输入，并且可以通过在 ACD 文件本身中使用计算属性来实现这一点。

现在，不再对序列插入位置进行硬编码检查，只需在插入位置的整数定义中添加：

```
maximum: $(asequence.end)
```

带有两个输入序列和一个整数插入位置的 ACD 文件可能看起来如下：

```
sequence: targetsequence
[
   parameter: "Y"
   type: "protein"
]

sequence: insertsequence
[
   parameter: "Y"
   type: "protein"
]

integer: position
[
   parameter: "Y"
   maximum: $(targetsequence.end)
]
```

当然，也可以从两个序列中检索计算属性的值。在以下示例中，定义了一个序列窗口，其长度不能超过两个序列长度之和。使用了计算，因此必须用括号括起来，并以“at”符号（“@”）开头：

```
integer: window
[
    parameter: "Y"
    maximum: @($(targetsequence.length) + $(insertsequence.length))
]
```

这些计算属性也用于条件语句。在以下示例中，序列输入为 any 类型。正在使用三元条件运算符（参见第 4.4 节，“操作”）来根据自动确定的序列类型设置默认替换矩阵：

```
sequence: sequence
[
  parameter: "Y"
  type: "anY"
]

integer: penalty
[
  parameter: "Y"
  default: "@($(sequence.protein) ? EBLOSUM62 : EDNAFULL)"
  etc
]
```

### 4.3.8.3 特征计算属性

序列特征输入数据类型：

```
features
```

具有七个计算属性：

| 属性 | 描述 |
|---|---|
| fbegin | 要使用的特征的起始位置（-fbegin 值） |
| fend | 要使用的特征的结束位置（-fend 值） |
| flength | 序列的总长度 |
| fprotein | 布尔值，如果特征表是蛋白质则为 True |
| fnucleic | 布尔值，如果特征表是核苷酸则为 True |
| fname | 特征表的名称 |
| fsize | 特征数量 |

这些是输入特征的属性，可以在 ACD 中查询。

> **注意**
>
> fbegin 和 fend 属性的值可以通过在命令行上指定 -fbegin 或 -fend 来设置，它们是 features 数据类型的内置限定符。

假设你定义了一个名为 afeatures 的特征输入，并且有一个看起来如下的 ACD 文件：

```
features: afeatures
[
  parameter: "Y"
]
```

这些属性将按以下方式引用：

- afeatures.fbegin
- afeatures.fend

等等。

要从上面的 afeatures 定义中检索计算属性值，可以使用：

```
$(afeatures.fbegin)
$(afeatures.fend)
$(afeatures.flength)
```

### 示例

在编写比较两个序列特征的程序时，这些序列可能是蛋白质或核苷酸序列，需要确保两个序列类型相同。从应用程序代码实现这一点的一种方法是调用 AJAX 函数来返回两者的类型，如果不相同则退出：

```
if((ajFeattableIsProt(features1)&& ajFeattableIsNuc(features2)) ||
   (ajFeattableIsNuc(features1) && ajFeattableIsProt(features2)))
   ajFatal("Input feature tables are not of the same type");
```

这段代码的问题是，如果特征表类型不同，应用程序在运行时会终止。更好的做法是在应用程序正式启动之前，让界面强制正确输入，这可以通过使用计算属性来实现。

假设应用程序将两个特征表参数作为输入，因此 ACD 文件看起来如下：

```
features: afeatures
[
  parameter: "Y"
]

features: bfeatures
[
  parameter: "Y"
]
```



与其对特征类型进行硬编码检查，不如在读取的第二个特征上强制执行：第一个特征表可以是任何类型，但第二个必须与第一个匹配。这是通过为特征表声明 type : 属性来实现的。第二个特征表的 type : 通过在三元条件中检索第一个特征表的 fprotein 计算属性来设置为与第一个相同（参见第 4.4 节“操作”）：

```
features: afeatures
[
    parameter: "Y"
    type: "any"
]

features: bfeatures
[
    parameter: "Y"
    type: "@($(afeatures.fprotein) ? protein : nucleotide)"
]
]
```

## 4.4 Operations

### 4.4.1 Types of operation

Operations are used within ACD files to achieve flexible and precise control over the command line interface. Currently the following types of operation are supported:

- To retrieve the value of a data definition
- To retrieve the values of attributes and calculated attributes of a data definition
- To retrieve the values of variables
- Arithmetic operations
- Tests for equality
- Boolean logical operations
- Calculations that use the above operations
- Unary and ternary conditional statements using the above operations.

### 4.4.2 General operation syntax

An operation must be enclosed in a pair of parentheses and preceded by the ‘at’ symbol (‘@’):

```
@(operation)
```

If the operation contains whitespaces, the whole token should be enclosed by double quotes (" "):

```
"@(operation with white space)"
```

Operations can be nested, in which case each operation must be enclosed in parentheses:

"@(operation @(nested operation)) "

An operation typically contains a reference to the value or attribute of a data definition or variable. They may also contain arithmetic, logical and conditional operators.

### 4.4.2.1 Arithmetic operators

- @(a+b) [Addition]
- @(a-b) [Subtraction]
- @(a*b) [Multiplication]
- @(a/b) [Division]

### 4.4.2.2 Logical operators

- @(!a) [Not boolean]
- @(a|b) [Or]
- @(a&b) [And]

### 4.4.2.3 Equality operators

- @(token1==token2) [Equality]
- @(token1!=token2) [Non-equality]
- @(token1<token2) [Less-than]
- @(token1>token2) [Greater-than]

### 4.4.2.4 Conditional operators

- @(boolval ? iftrue : iffalse) [If]
- @(testval = A : 1 B : 2 else : 0) [Case]

### 4.4.3 Retrieving data values in ACD files

The attribute values for a given data definition can depend on the values from other data definitions. It is possible to retrieve the value of:

- A data definition (application parameter)
- An attribute of a data definition
- A calculated attribute of a data definition
- An ACD variable definition.

Such values are retrieved using the ACD “get the value of” syntax which consists of a term ParameterName.AttributeName term surrounded by parentheses with a dollar sign ($) at the front:

```
$(ParameterName.AttributeName)
```

If only the value of the data definition is to be retrieved then the AttributeName component is omitted:

```
$(ParameterName)
```

Of course a variable name may also be given. Variables do not have attributes therefore the syntax is:

```
$(VariableName)
```

For example, in the following ACD file excerpt two integer inputs are defined:

```
integer: gapopenalty
[
  standard: "Y"
  default: "10"
]

integer: gapextpenalty
[
  standard: "Y"
  default: "$(gapopenalty)"
]
```

The default for the standard qualifier gapextpenalty is set to the value of qualifier gapopenalty.

As another example assume a sequence input and a window over that sequence which should not be longer than the sequence itself. There is also a sub-window which (by default) is one residue shorter than the main window, and an array of numbers that is the same size as the sub-window. The following ACD code would suffice:

```
sequence: sequence
[
  parameter: "Y"
]

integer: window
[
  standard: "Y"
  default: "10"
  maximum: "$(sequence.length)"
]

integer: subwindow [
  standard: "Y"
  default: "@($(window)-1)"
  maximum: "@($(window.maximum)-1)"
]
array: values
[
  standard: "Y"
  size: "$(subwindow)"
]
```

sequence.length is a calculated attribute and is the length of the sequence. The $(sequence.length) value is calculated during ACD processing once the input sequence has been read in. In contrast window.maximum simply refers to the maximum: attribute of the window data definition.

Of course you need to be careful that the type of retrieved value matches that of the attribute which is being calculated. For instance, if you have defined a toggle datatype:

```
toggle: dovalues
[
  standard: "Y"
]
```

then the following definition is perfectly valid because the standard: global attribute has a boolean value, which is the same type as the toggle datatype.

```
array: values
[
  standard: "$(toggle)"
  size: "$(subwindow)"
]
```

The following definition is *not* valid and an error will be generated during ACD processing:

```
array: values
[
  standard: "Y"
  size: "$(toggle)"    /* This is not valid ! */
]
```

It is invalid because the size: attribute of the array datatype has an integer value, whereas the toggle datatype has a boolean value.

### 4.4.4 Calculations and tests

Calculations can be performed in ACD using the @ syntax. A rather silly, but legal, calculation would be:

```
@(5 + 9)
```

which equates to the value 14. Calculations can be used to add, subtract, multiply or divide, or test for equality, inequality, “greater than” or “less than”. The test values can be integers, floats and strings. You can use calculations with most attributes of datatypes where they make sense. In the following example a start condition is set to have a maximum value of the sequence length minus a window size value plus 1:

```
sequence: sequence
[
   parameter: "Y"
   type: pureprotein
]

integer: window
[
   standard: "Y"
]

integer: start
[
   standard: "Y"
   maximum: "@(@($(sequence.length) - $(window)) + 1)"
]
```

Note that there are two separate calculations here so each needs to be surrounded by the @() syntax. Long calculations can get messy. If you need to use them then you possibly need to rethink your ACD logic. If they can't be avoided then they can be tidied up with the use of variables (see below).

### 4.4.4.1 Arithmetic operations

The supported arithmetic operations are addition, subtraction, multiplication and division. The standard characters for the arithmetic operations are used: +, -, * and /.

```
@(a+b)   (Addition)
@(a-b)   (Subtraction)
@(a*b)   (Multiplication)
@(a/b)   (Division)
```

The operands a and b must resolve to a numeric value (integer or floating point); the result is undefined otherwise but will most probably result in an error during ACD processing.

Only a single arithmetic operation is allowed per set of parentheses, for instance, the code below is not valid:

```
integer: a []
integer: b []
integer: c []
integer: n

[
   default: "@(a + b + c)"   /* This is not valid ! */
]
```

It could however be rewritten using nested operations. The following is perfectly valid:

```
integer: n
[
default: "@(@(a + b)+c)"
]
```

Note that two sets of parentheses are required: The first around the addition of a and b which gives @(a + b). The second around the addition of @(a + b) to c, which gives @(@(a + b)+c). Where more than one arithmetic operation is required, however, one would typically use an internal ACD variable to hold the intermediate results.

### 4.4.4.2 Tests for equality

The supported equality tests (symbols in parenthesis) are “equality” (==), “non-equality” (!=), “less than” (<) and “greater than” (>):

```
@(token1 == token2)   (Equality)
@(token1 != token2)   (Non-equality)
@(token1 < token2)    (Less-than)
@(token1 > token2)    (Greater-than)
```

The above equality tests can be used on strings in which case the lexicographical sorting order of the string is used.

### 4.4.4.3 Boolean tests

The supported boolean operations are logical AND, logical OR and logical NOT. Again, the standard characters are used: &, | and !:

```
@(!a)   (NOT)
@(a|b)  (OR)
@(a&b)  (AND)
```

In the following ACD code snippet:

```
integer: fubar
[
    standard: "Y"
    default: 5
    etc
]

integer: rtfm
[
    standard: "@(@($(fubar)==3) | @($(fubar)==7)) "
    etc
]
```

The integer rtfm will only be prompted for if the value of fubar is either 3 or 7. Each of the equality tests is a calculation and the boolean test is another calculation. There are therefore three instances of @().





## 4.4.5 Conditional statements

ACD中有三种条件语句：一元、三元和案例型。

### 4.4.5.1 Unary conditional statements

一元条件的典型用途是开启或关闭提示。假设只有当序列被确定为蛋白质时才应提示输入窗口大小。实现此功能的ACD如下所示：

```
sequence: sequence
[
  parameter: "Y"
  type: gapany
]

integer: window
[
  standard: "$(sequence.protein)"
  etc
]
```

如果序列是蛋白质，则所需语句等效于：

```
standard: "Y"
```

并开启提示。如果序列是核酸，则语句等效于：

```
standard: "N"
```

这将有效地禁用提示。控制提示在其他地方有详细描述（第4.5节，“控制提示”）。

### 4.4.5.2 Ternary conditional statements

三元条件语句的一般形式为：

```
@(conditional ? value-if-true : value-if-false)
```

当为应用程序设置两种不同的使用模式时，它们很有用，例如在排列程序中为蛋白质和核酸设置不同的间隙罚分值。下面的示例将蛋白质的罚分设置为14，核酸的罚分设置为16：

```
integer: penalty
[
  standard: "N"
  default: "@($(sequence.protein) ? 14 : 16)"
  etc
]
```

### 4.4.5.3 Case conditional

在案例型操作中，测试值与一系列可能值进行比较。如果找到匹配项，则操作将解析为与该可能值关联的结果。测试值作为字符串解析，后跟等号（=），等号后跟一个或多个由冒号（:）分隔的可能值和关联值对。如果没有可能值匹配，则操作将解析为与关键字else关联的默认结果。

else : 默认值对不是强制性的，如果在没有默认值的操作中没有可能值匹配，则操作将解析为NULL。

其形式化如下：

```
@(testval = poss_valA : ass_valA
poss_valB : ass_valB
else : default_val)
```

例如：

```
string: matrix
[
    default: "@($(sequence.type) =
    protein : BLOSUM62
    dna : dnamat
    rna : rnat
    else : unknown)"
]
```

$(sequence.type)变量是一个字符串值，保存名为sequence的ACD数据项的序列类型。如果类型是protein，则操作解析为BLOSUM62；如果类型是dna，则解析为DNAMAT。如果类型不在此列表中，则操作解析为unknown。

如果测试值无法明确分配给单个关联值，则操作将解析为与其可能值匹配的最后一个关联值。

### 4.4.6 Use of variables

变量用于保存部分计算或值，很有用。其一般语法为：

```
VariableName : Variable value
```

请注意，由于变量只有一个值且没有属性，因此不使用方括号。

例如，以下是确定序列窗口最大大小的计算：

```
integer: start
[
    standard: "Y"
    maximum: "@(@($(sequence.length) - $(window)) + 1)"
]
```

可以通过将其中一个计算存储为部分结果来整理，如下所示：

```
variable: lminusw "@($(sequence.length) - $(window))"
integer: start
[
    standard: "Y"
    maximum: "@($(lminusw) + 1)"
]
```

在以下ACD代码中，内部ACD变量protlen用于存储中间结果。变量$(protlen)的值从输入序列（sequence数据类型）的长度计算得出，并用于定义窗口参数的最大大小：

```
variable: protlen "@( $(sequence.length) / 3 )"
integer: window
[
    maximum: "@($(protlen)-50)"
    default: 50
]
```

使用嵌套操作如下所示也可以实现相同的结果：

```
integer: window
[
    maximum: "@( @( $(sequence.length) / 3) - 50)"
    default: 50
]
```

窗口参数直接从sequence.length变量（计算属性）计算得出，方法是将除法算术操作嵌套在单独的减法操作中。

变量可用于简化ACD文件，使其更易于读取和解析。ACD文件可以使用变量定义仅定义一次结果，然后在所有后续ACD数据类型定义中按名称引用该变量。

### Caution

使用变量可能表明ACD定义中存在一定的复杂性。当使用变量，或当条件操作引用另一个ACD值时，应用程序在逻辑上可能被视为由解析的条件分叉的两个或多个独立应用程序。

### 4.4.6.1 Automatic variables

目前只有一个这样的变量（acdprotein），它根据读取的第一个序列的类型设置为true或false。

## 4.5 控制提示

### 4.5.1 Introduction

可靠地提示用户输入值是任何应用程序界面的关键部分。EMBOSS允许您精确控制应用程序参数的提示方式，从而为您节省大量开发时间。这是通过使用ACD数据属性实现的：

- parameter: "Y"表示该数据项是一个参数，即您不必在命令行上使用数据标签来为其指定值，例如myprog 10。
- standard: "Y"和additional : "Y"表示该数据项是一个限定符，即您必须在命令行上使用数据标签来为其指定值，例如myprog -somevalue 10。如果数据定义未定义为参数，或标准或附加限定符，则它将默认为高级限定符。

如果未在命令行上指定，参数和标准限定符的值始终会提示（带有其默认值）。除非在命令行上给出-options，否则不会提示附加限定符的值（将使用默认值）。ACD文件中应始终给出附加限定符的默认值。高级限定符的值永远不会提示。

### 4.5.2 Parameters

请考虑以下ACD文件，用于名为helloworld的应用程序，它定义了两个参数，即字符串输入（string数据类型）和输出文件（outfile数据类型）：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]

string: message
[
    parameter: "Y"
]

outfile: outfile
[
    parameter: "Y"
]
```

参数的值必须在命令行上按照它们在ACD文件中出现的顺序指定。因此，要为helloworld指定两个参数，您需要输入类似：

```
helloworld "Hello World!" message.dat
```

这将导致Hello World!被打印到输出文件message.dat。或者，使用以下任一命令也是完全可以接受的：

```
helloworld -message "Hello World!" -outfile message.dat
helloworld -outfile message.dat -message "Hello World!"
helloworld -message "Hello World!" message.dat
```

对于参数，您不必使用名称标志，而对于限定符则必须使用。如果省略参数的标志，则它们的值*必须*在命令行上按照它们在ACD文件中出现的顺序出现。

但是，您可能不想强制用户指定消息，而是依赖ACD文件中定义的默认消息（“Hello World!”）在未给出其他内容时打印。因此，通过输入：

```
helloworld message.dat
```

您希望“Hello World!”（默认消息）被打印到文件message.dat。

上述ACD文件不会这样做。所有数据定义都是参数（parameter：），因此如果未在命令行上给出，则会提示输入。输入上述命令会导致message.dat被当作要打印的字符串，然后您将被提示输入输出文件名。简而言之，不是所需的行为。这时就需要限定符了。

### 4.5.3 Qualifiers

限定符（无论是“标准”、“附加”还是“高级”）的值可以出现在命令行上的任何位置，但您必须始终通过其标志引用它们。因此，如果您的消息定义为限定符而非参数，则对它的引用必须如下所示：

```
-message "Hello World!"
```

要将数据定义指定为限定符，您使用standard:或additional:，而不是当前指定的parameter:属性。或者，如果您未指定这些属性中的任何一个，它将默认为高级限定符。例如：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
    standard: "Y"
]
outfile: outfile
[
    parameter: "Y"
]
```





## 4.5 控制提示

由于您现在只有一个参数，以下两个命令行都是有效的：

```
helloworld -message "Hello World!" message.dat
helloworld message.dat -message "Hello World!"
```

现在如果您在命令行中未指定消息文本，即您只输入：

```
helloworld message.dat
```

那么 message.dat 将被视为一个参数，并被当作输出文件名。程序随后会提示您输入要打印的字符串。这接近我们想要的，但仍不完全是期望的行为。我们希望它能直接使用默认字符串运行。

### 4.5.4 默认值

您可以使用 default: 属性为大多数数据定义关联默认值。ACD 可以修改如下：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
    standard: "Y"
    default: "Hello World!"
]
outfile: outfile
[
    parameter: "Y"
]
```

现在如果您输入：

```
helloworld message.dat
```

那么，尽管您指定了默认值，它仍在提示输入值。请记住，标准数据定义的所有值始终会被提示输入，无论是否指定了默认值。您需要将 message 指定为“附加”或“高级”限定符，这些通常不会被提示输入。

ACD 文件将如下所示：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
  additional: "Y"
  default: "Hello World!"
]
outfile: outfile
[
  parameter: "Y"
]
```

这个 ACD 终于实现了所需功能。输入：

```
helloworld message.dat
```

将把 Hello World! 打印到文件 message.dat 中，即期望的行为。
当然，您也可以通过在命令行中指定消息来覆盖默认消息：

```
helloworld -message "Goodbye World!" message.dat
```

这将向输出文件打印一条相当令人不快的消息。对于附加和高级 ACD 数据定义，您通常应提供默认值，因为如果您未在命令行中指定值，EMBOSS 不会提示您输入。如果您尝试在 C 源代码中访问未指定数据项的值，EMBOSS 会生成错误。相比之下，标准和参数数据定义的值如果未在命令行中指定，始终会被提示输入，因此默认值有用但非必需。

### 注意

请注意，某些数据类型（如 boolean）具有内置默认值。

### 4.5.5 最大值和最小值

为 ACD 数据类型定义设置最大值和/或最小值限制通常很有用，甚至至关重要。这是通过使用 minimum 和 maximum 属性以直观的方式完成的：

```
integer: window
[
  standard: "Y"
  default: "10"
  minimum: "5"
  maximum: "100"
]
```

### 4.5.6 设置提示

EMBOSS 始终会提供默认提示文本。请考虑以下 ACD 文件：

```
integer: window
[
 standard: "Y"
 default: "10"
 minimum: "5"
 maximum: "100"
]
```

用户将按以下方式被提示：

```
-window : Enter a number [10] :
```

虽然足够，但这并不十分友好。您可以使用 information: 属性为数据类型定义设置提示。ACD 文件将如下所示：

```
integer: window
[
 standard: "Y"
 default: "10"
 minimum: "5"
 maximum: "100"
 information: "Window size"
]
```

这将给出以下提示。

```
Window size [10]:
```

这要有意义得多。

### 4.5.7 否定

迄今为止，您只在参数或限定符定义后描述了值 "Y"。然而，否定（间接指定值 "N"）在 ACD 文件中常有用处。举个简单的例子：

```
sequence: sequence
[
 parameter: "Y"
]
```

```
integer: n
[
    standard: "@($(sequence.length) > 100)"
]
```

如果序列长度大于 100，standard: 属性将被设置为 "Y"，否则设置为 "N"。虽然值 "N" 不应在 parameter:、standard: 或 additional: 后显式指定，但计算结果为 "N" 的计算值实际上对限定符（而非参数）是支持的。在这种情况下，"N" 会覆盖属性的默认行为，使得提示输入值被关闭。这在某些情况下很有用。在此示例中，计算仅在序列长度大于 100 时才会打开提示。

现在假设您的应用程序可以生成图形和文本输出。进一步假设，您只有在用户未选择图形输出时才希望获得文本输出。首先，您将按如下方式设置一个切换 ACD 数据类型定义：

```
toggle: plot
[
    standard: "Y"
    default: "N"
    information: "Plot a graph"
]
```

如果用户在命令行中添加 -plot，$(plot) 的值将为 "Y"。如果用户未在命令行中添加任何内容，或者用户添加了 -noplot，则值为 N。

输出文件现在可以定义为：

```
outfile: outfile
[
    standard: "@(!$plot)"
]
```

仅当 plot 为假时，这才等同于 standard: "Y"。否定运算符 (!) 是一个计算，因此该项必须用 @() 包围。

这唯一令人遗憾的是，它按原样写无法工作，但这与逻辑无关。原因是 EMBOSS 处理文件输入/输出操作的方式与其他数据类型不同。如果它看到文件（例如 outfile）或序列（例如 seqout）定义，它将始终尝试打开它。

如果该项等同于 standard: "N"，且命令行或默认值中未指定文件名（您通常不会为输出文件指定默认名称），则 ACD 解析将尝试打开一个无名文件。这将导致错误。

绕过此问题的方法是使用 nullok: 属性。因此，一个可行的 outfile 定义是：

```
outfile: outfile
[
  standard: "@(!$plot)"
  nullok: "Y"
]
```

上面的 nullok: 属性表示，如果未给出文件名，则可以继续（不生成错误）。

> **注意**
> 
> 如果您运行一个 ACD 文件（例如，使用 acdc（第 4.6.4.1 节，‘acdc’）进行测试，并为 standard: 使用计算值），您将看到一条警告消息。以这种方式使用计算是受支持的，但仅在绝对必要时才推荐。这是因为这可能会使 ACD 文件的理解变得混乱，例如，第三方界面可能会感到困惑。

> **警告**
> 
> 计算 *不应* 用于设置参数的值：如果这样做，在 ACD 处理期间将生成错误。参数被视为应用程序的必要输入。相比之下，计算可以用于控制限定符（无论是标准、附加还是高级）的提示输入。

### 4.5.8 布尔数据类型

ACD 语法提供了两种具有布尔值的数据类型（boolean 和 toggle）。boolean 是标准布尔数据类型，而 toggle 是一种特殊的布尔数据类型，专门用于控制其他属性的提示输入。

以下 ACD 文件展示了一个带有两个参数和一个高级限定符（abool，布尔数据类型）的应用程序。abool 可能会被用来设置输出文件中的详细或简洁文本，尽管它会被赋予一个更直观的名称。

```
application: seqdemo
[
  documentation: "Demo application."
]

sequence: asequence
[
  parameter: "Y"
]

boolean: abool
[
  default: "Y"
]

outfile: outfile
[
  parameter: "Y"
]
```

应用程序可以以以下任一方式调用：

```
seqdemo filename.seq filename.out -abool
seqdemo filename.seq filename.out -noabool
```

在第一个示例中，布尔限定符 abool 被设置为 True。实际上，该值无需显式设置，因为默认值为 True。在第二个命令行中，abool 通过前缀 no 被设置为 False。

### 4.5.8.1 提示布尔值

为布尔数据类型定义 information: 和 help: 全局属性时应小心。这些属性用于提示用户（交互式或通过 GUI）并提供帮助文本。每种情况下提供的文本都应反映布尔选项的预期默认值，这可能与名称所暗示的相反。例如，如果默认设置为 “Y”，则命令行选项通常为 -noFlag，其中 Flag 是限定符。如果默认设置为 “N”，则默认操作可能与信息或帮助文本所暗示的相反。如果值是计算得出的，用户可能需要一些额外指导。

## 4.6 ACD 实用程序

### 4.6.1 简介

EMBOSS 包含六个实用程序，用于运行、测试和记录 ACD 文件，而无需为程序本身编写 C 源代码：

- **acdc** 读取并处理 ACD 文件，按必要提示用户，方式与应用程序运行时完全相同。如果遇到错误，它将终止。这允许在不同条件下测试命令行界面的行为，即使应用程序本身尚未编写。它是使用最广泛的实用程序，也是测试 ACD 文件是否正确工作的基本工具。

- **acdtrace** 的工作方式与 **acdc** 相同，但会报告 ACD 文件中行的处理情况。它还会打印评估任何变量和操作的结果（参见第 4.4 节，‘Operations’）。

- **acdvalid** 处理 ACD 文件并报告由不正确、弃用或过时的语法引起的任何错误或警告。测试超出了 **acdc** 和 **acdtrace** 的范围。它强制执行参数和限定符命名的建议，并突出显示可能对第三方解析软件造成问题的 ACD 语法。

- **acdlog** 处理 ACD 文件和用户输入，同时记录内部数据结构的内容。目前其使用已弃用，应改用 **entrails** 应用程序（见下文）。

- **acdpretty** 从可解析但部分或格式不正确的 ACD 文件生成格式正确的 ACD 文件。

- **acdtable** 创建参数、允许值和默认值的表，用于应用程序文档和提供用户帮助。





## 4.6.2 使用实用程序

实用程序本身没有选项。它们的调用方式相同，即指定要测试的应用程序名称，并在实用程序应用程序名称之后指定任何命令行选项：

```
UtilityName ApplicationName Options
```

例如，这将测试名为 helloworld 的应用程序的 ACD 文件：

```
acdc helloworld
```

acdc、acdtrace 和 acdlog 将通过读取其 ACD 文件，并以与真正运行程序时完全相同的方式处理命令行和用户响应，来运行任何 EMBOSS 程序的命令行界面。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

可以指定任何命令行选项。在以下示例中，seqret 被调用以从序列（sequence.in）中检索区域 50 – 100，并将片段写入输出文件（sequence.out）：

```
acdc seqret sequence.in sequence.out -sbegin 50 -send 100
```

> 注意
> 所有 EMBOSS 应用程序都会调用 NUCLEUS 函数 embInit（对于 EMBASSY 应用程序则为 embInitP），该函数会进一步调用 ACD 文件处理函数。实用程序应用程序将任何参数（即要测试的应用程序的命令行）传递给 embInit 或 embInitP，因此运行方式与原生应用程序完全相同。可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

## 4.6.3 全局限定符

实用程序可以使用所有全局限定符（参见 EMBOSS 用户指南）：

- -auto 关闭任何用户提示。使用 -auto 选项测试应用程序总是很有用，因为这模拟了应用程序由脚本或其他不涉及交互式用户输入的方式调用的情况。
- -debug 打开调试。这将输出与调用 AJAX 函数 ajDebug 相关的参数。
- -filter 从 stdin 读取并写入 stdout，并隐含 -auto。
- -stdout 默认写入 stdout，但仍会提示用户。
- -help 将提供实用程序的用法信息。
- -verbose 与 -help 连用时，还会提供相关限定符和全局限定符。
- -warning 如果需要，程序将生成警告消息。
- -error 如果需要，程序将生成错误消息。
- -fatal 如果需要，程序将生成致命错误（终止）消息。

实用程序本身都不会生成调试、警告、错误或致命消息。但是，由于可以读取输入文件，输入函数所做的任何调试调用或消息 *将* 被报告。

## 4.6.4 实用程序说明

### 4.6.4.1 acdc

acdc 读取并处理 ACD 文件，在必要时提示用户，方式与应用程序运行时完全相同。如果遇到错误，它将终止。这允许在不同条件下测试命令行界面的行为，即使应用程序本身尚未编写。它是使用最广泛的实用程序，是测试 ACD 文件是否正确工作的基本工具。

acdc 没有自己的选项，但接受一个参数，即正在测试的 EMBOSS 应用程序的名称。它通过指定要测试的应用程序名称，并在实用程序应用程序名称之后指定任何命令行选项来调用：

```
acdc ApplicationName Options
```

可以为应用程序指定任何命令行选项。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

acdc 将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 *EMBOSS 用户指南*）。

可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

以下是 **acdc** 的示例会话：

```
% acdc antigenic
Finds antigenic sites in proteins
Input protein sequence(s) : tsw:act1_fgru
Minimum length of antigenic region [6]:
Output report [act1_fgru.antigenic]:
```

### 4.6.4.2 acdtrace

acdtrace 的工作方式与 acdc 相同，但会报告 ACD 文件中行的处理情况。它还会打印评估 ACD 文件中任何变量和操作的结果（参见第 4.4 节，“操作”）。

调用方式如下：

```
acdtrace ApplicationName Options
```

acdtrace 将通过读取其 ACD 文件，并以与真正运行程序时完全相同的方式处理命令行和用户响应，来运行任何 EMBOSS 程序的命令行界面。可以为被调用的应用程序指定任何命令行选项。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

可以以任何可用格式指定输出文件，但它们将为空（不会调用应用程序代码，因此不会有输出）。

acdtrace 将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 EMBOSS 用户指南）。

以下是 acdtrace 的示例会话：

```
% acdtrace antigenic
Finds antigenic sites in proteins
Input protein sequence(s) : tsw:act1_fgru
Minimum length of antigenic region [6]:
Output report [act1_fgru.antigenic]:
```

屏幕上的输出（未显示）可能看起来有点令人困惑，但这是查看变量和操作在 ACD 文件中如何工作的最佳方式。

### 4.6.4.3 acdvalid

acdvalid 处理 ACD 文件，并报告由不正确、已弃用或已过时的语法引起的任何错误或警告。测试内容超出了 acdc 和 acdtrace 的范围。它会突出显示可能导致包装 EMBOSS 应用程序的第三方解析软件出现问题的 ACD 语法。

acdvalid 验证 ACD 文件，测试许多功能，这些功能不会阻止应用程序运行，但可能会为任何用户界面（无论是命令行还是通过包装器）创建问题。acdvalid 的大多数消息都是警告，不会阻止程序运行。

调用方式如下：

```
acdvalid ApplicationName Options
```

acdvalid 将像 acdtrace 一样，以与真正运行程序时完全相同的方式运行命令行界面。

它将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 EMBOSS 用户指南）。

可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

以下是 acdvalid 的示例会话：

```
% acdvalid antigenic
```

acdvalid 会生成错误和警告消息。如果消息是“错误”，则 ACD 文件将无法工作并需要修复。如果消息是“警告”，则 ACD 文件将能工作，但值得尝试修复问题。

> **注意**
> 警告消息仅供参考，但主发布版本中的任何应用程序都会尽可能修复尽多的警告。
>
> 值得在每个新版本的 EMBOSS 中对所有本地 ACD 文件运行 acdvalid。因为每个新版本都会添加额外的验证测试。

### 4.6.4.3.1 acdvalid 测试的功能

这些包括：

- 各部分的顺序正确，为“input”、“required”、“additional”、“advanced”和“output”。
- 部分和子部分名称（第 4.1.5 节，“ACD 文件部分”）在 EMBOSS 系统文件 sections.standard 中定义。
  - 这确保了在使用部分对应用程序参数进行分组时，界面包装器将具有一致的描述。
- 所有数据定义都包含在一个部分或子部分中。
- 限制在一个部分中的参数位于正确的部分。
  - 所有输入 ACD 数据类型（第 A.2.2 节，“输入 ACD 数据类型描述”）必须位于“input”部分，所有输出 ACD 数据类型（第 A.2.3 节，“输出 ACD 数据类型描述”）位于“output”部分。
- 其他参数在其出现的部分中是有效的。





例如，“高级”部分不能包含可能会被提示输入的参数，这排除了设置了 *参数：*、*标准：* 或 *附加：* 属性的数据定义（参数，以及标准和附加限定符）。“附加”部分只能包含设置了 *附加：* 属性的限定符，或控制它们的 *切换* 对象。

- 计算 *不* 用于设置 *参数：* 属性的值。

参数被视为应用程序的基本输入。相比之下，计算可用于控制对 *限定符*（无论是标准、附加还是高级）的提示。

- 如果在 ACD 文件的应用程序定义中使用了 *组：* 属性的值，则该值必须在文件 *groups.standard* 中定义。

- 计算值不用于 *标准：*。

如果 ACD 文件为 *标准：* 设置了计算值，则会报告一条警告消息。以这种方式使用计算是受支持的，但仅在绝对必要时才推荐，因为这可能会使第三方接口等对应用程序输入的理解产生混淆。

- *标准：* 和 *附加：* 属性的计算值（参见第 4.5 节“控制提示”）使用 *切换* 数据类型值，但不使用 *布尔*。

- 这允许接口包装器使用 *切换* 值将应用程序拆分为两个或多个更简单的定义。

- *参数：*、*标准：* 和 *附加：* 属性值未显式设置为 "N"（默认值）。

这会使解析器混淆。您绝不应显式指定 Parameter: "N"、Standard: "N" 或 Additional: "N"。在实践中，"N" 的计算值实际上是受支持的，并且可以在特殊情况下用于覆盖这些属性的默认行为（参见第 4.5 节“控制提示”）。

- 通常作为 EMBOSS 应用程序主要输入或输出的数据类型是通过使用 *参数：* 属性定义为参数的。这些数据类型包括：

- 对齐输出（*比对：* 数据类型）

- 用于输入的序列特征（*特征* 数据类型）和输出（*特征输出* 数据类型）

- 用于输入的文件数据类型（*输入文件*、*文件列表*、*目录* 或 *目录列表* 数据类型）和输出（*输出目录*）

- 应用程序报告输出（*报告：* 数据类型）

- 序列输入（*序列*、*序列集*、*序列集合全部* 或 *序列集合* 数据类型）

- 上述任何数据类型的第一个数据定义 *必须* 定义为参数。建议该数据类型的后续定义（第二个、第三个等等）也定义为参数。例外情况是如果设置了 *默认：* 或 *允许空：* 属性，在这种情况下不会生成警告或错误消息，因为应用程序可以使用默认值或没有该定义的任何值运行。

- 参数和限定符名称（数据定义标志）与公认标准匹配（第 4.1 节“ACD 文件开发简介”）。

例如，所有序列输入都应以“sequence”结尾，以便在命令行上使用短形式（例如 -aseq、-bseq 等）。如果出错，警告消息将说明标准的要求。

- 对齐输出、特征输入和输出、文件输入和输出、报告输出以及序列输入和输出的 ACD 定义（`seqout`、`seqoutall`、`seqoutset` 数据类型）具有标准名称（第 4.1.4 节“参数和限定符”）。

- 当指定 `knowntype:` 属性时，其值应与 EMBOSS 系统文件 `knowntypes.standard` 中为相应数据类型定义的标准名称匹配，或与该数据类型的公认标准格式匹配。

  - 少数不在 `knowntypes.standard` 中的值也是可接受的，例如 `outfile:` 数据类型的“ApplicationName output”。这些值与数据类型一起记录在第 A.5 节“数据类型特定属性”中。

- 要求为 `knowntype:` 属性提供值的数据定义都已定义一个值。这些包括任何输出文件（`outfile` 数据类型）或目录（`outdir`），以及 `string` 数据类型。

- EMBOSS 必须能够识别特征输入和输出的类型。如果未为 `feature` 或 `featout` 定义指定类型（使用 `type:` 属性），且没有可用于获取默认类型的序列输入，则会生成错误。

- EMBOSS 还必须能够识别序列输出的类型。如果未为输出序列（`seqout`、`seqoutset` 或 `seqoutall` 定义）指定类型（使用 `type:` 属性），且没有可用于获取默认类型的序列输入，则会生成错误。

- 具有标准提示的数据类型不应具有 `information:` 或 `prompt:` 属性（参见第 A.4 节“全局属性”）。

  - 为了提供标准提示，大多数常见数据类型都为 `information:` 字符串定义了默认值。这些默认值位于 EMBOSS 系统文件 `codes.english` 中。

- `help:`、`information:` 和 `prompt:` 属性后的文本应符合以下约定：

  - 字符串应以大写字母开头，且不应以句号结尾

- Any `seqset` or `seqsetall` datatype `must` have the `aligned:` attribute set.

## 4.6.4.4 acdlog

acdlog 处理 ACD 文件和用户输入，同时记录内部数据结构的内容。目前其使用已弃用，应改用 entrails 应用程序（第 4.6.5 节“使用 entrails”）。
调用方式如下：

```
acdlog ApplicationName Options
```

与 **acdtrace** 类似，**acdlog** 将以与真实程序运行时完全相同的方式运行命令行界面。

输出文件可以指定为任何可用格式；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

##### 4.6.4.5 acdpretty

**acdpretty** 将从可解析但部分或格式不正确的 ACD 文件生成格式正确的 ACD 文件。

**acdpretty** 读取 ACD 文件并以清晰的格式将其重写到文件：

```
(ProgramName).acdpretty
```

该文件可用于覆盖原始 ACD 文件。所有部分和属性都将缩进。所有值都将加引号。行将在合理的宽度处换行。输出文件旨在作为 GUI 和其他接口包装器使用的解析器的标准格式，而不是直接使用原始 ACD 文件。

调用方式如下：

```
acdpretty ApplicationName Options
```

通常可能为应用程序指定的任何命令行参数基本上都会被忽略，因为一旦打印重新格式化的 ACD 文件，处理就会停止。少数全局限定符可能会与 **acdpretty** 的功能冲突。

##### 4.6.4.6 acdtable

**acdtable** 用于创建应用程序文档中使用的参数、允许值和默认值的表格，并提供用户帮助。

调用方式如下：

```
acdtable ApplicationName Options
```

大多数 ACD 数据类型的可接受预期值和默认值可以自动生成。在其他情况下，允许值通过 valid: 全局属性定义，默认值通过 expected: 全局属性定义（参见第 A.4 节“全局属性”）。

#### 4.6.5 使用 entrails

**entrails** 将报告用于解析 ACD 文件的数据结构的内部情况。它报告：

- 所有已知 ACD 数据类型的详细信息
- 所有已知 ACD 属性的详细信息
- 所有计算属性的详细信息
- 序列访问方法的内部数据结构
- 序列读取和写入的内部数据结构
- 特征处理的内部数据结构
- 比对的内部数据结构
- 应用程序报告的内部数据结构
- 密码子使用表的内部数据结构
- 可用数据库属性的报告
- 可用资源属性的报告。

## 注意

entrails 未在标准 EMBOSS 安装中编译，因为它位于 Makefile.am 文件的“make check”部分中。

要编译 "check_PROGRAMS" 应用程序，请键入：

```
make check
```

在应用程序目录中。如果出于某种原因失败（毕竟该部分保留给正在积极开发的应用程序），请相应地编辑 Makefile.am 文件，使 entrails.c 被视为普通应用程序，并按常规方式编译它。有关更多信息，请参见第 1.2 节“安装 CVS（开发者）版本”。





## 5.1 基本数据类型

### 5.1.1 基本 C 数据类型

C 编程语言支持的基本数据类型包括两种基本算术类型。*整数*类型表示字符或整数，而*浮点*类型表示浮点数，并具有符号位、尾数和指数。

类型前可以加上修饰符，以指定类型是否带符号（仅限整数类型）、大小（`char` 除外，通常始终为 8 位）和精度（仅限浮点类型）。在大多数操作系统上（例如 IRIX 是个例外），整数类型除非另有说明，否则均为带符号：无符号整数可以容纳更大范围的正值。可用的具体类型及其大小取决于编译器。常见类型及其标称大小如下表所示。

| 类型 | 描述 | 大小（字节） |
|---|---|---|
| char | 字符 | 1 |
| short int | 短整数 | 2 |
| int | 整数 | 4 |
| long int | 长整数 | 8 |
| unsigned char | 无符号字符 | 1 |
| unsigned short int | 无符号短整数 | 2 |
| unsigned int | 无符号整数 | 4 |
| unsigned long int | 无符号长整数 | 8 |
| float | 浮点数 | 4 |
| double | 双精度浮点数 | 8 |
| long double | 扩展精度浮点数 | 12 |

此外可能还有其他类型，例如 `long long` 整数类型。标准 C 头文件 `limits.h` 定义了 `char` 的大小（例如 8 位）以及任何实现中允许的其他整数类型的最大值和最小值，以确保每种类型都有最小大小且不大于下一种类型。例如，int 永远不会比 long int 长。同样，头文件 float.h（或等效文件）定义常量，使得浮点类型的精度始终至少等于前一种类型。例如，double 的精度始终至少等于 float。

除了上述基本类型外，C 还定义了 void 类型，用于指定空值，例如用作不返回值的函数的返回类型。

还有枚举，这是一种与一组命名常量整数值关联的唯一类型。

### 5.1.2 基本 AJAX 数据类型

### 5.1.2.1 整数类型

基本 C 数据类型（char 除外）的确切大小和精度取决于实现。为避免这些系统相关限制可能带来的任何潜在问题，AJAX 在 AJAX 文件 ajarch.h 中定义了一组新的基本数据类型，如下所示：

| 类型 | 描述 |
|---|---|
| ajshort | 短整数 |
| ajint | 标准整数 |
| ajlong | 长整数 |
| ajushort | 无符号短整数 |
| ajuint | 无符号标准整数 |
| ajulong | 无符号长整数 |

ajarch.h 中列出的系统之间存在一些差异，但典型定义如下：

```
typedef short ajshort;
typedef int ajint;
typedef long long ajlong;
typedef unsigned int ajuint;
typedef unsigned short ajushort;
typedef unsigned long long ajulong;
```

ajint 通常为 32 位，ajlong 通常为 64 位。如果 32 位足够，请使用 ajint 而不是 int。请使用 ajlong 而不是 long 或 long long。话虽如此，在某些情况下，标准 C int 和 long 应该被使用，例如作为 C 系统库函数的参数。

您应根据需求选择数据类型。例如，如果您使用的是 Alpha 机器，那么 int 和 long 变量都将是 64 位。在这种情况下，不要出于懒惰而只使用 ajlong，因为您的代码在其他平台上可能运行得更慢。

### 5.1.2.2 其他 AJAX 类型

为方便起见，ajdefine.h 还定义了下表中列出的几种数据类型：

| 类型 | 描述 |
| :--- | :--- |
| AjBool | 布尔值 |
| AjStatus | 状态码 |
| AjIntArray | 整数数组（int*） |
| AjFloatArray | 浮点数组（float*） |

**AjBool** 用于存储 true（ajTrue, AJTRUE）和 false（ajFalse, AJFALSE）值。在输出时，转换代码 %b 写入 Y 或 N，而转换代码 %B 写入 Yes 或 No。
还有一个用于测试布尔值的宏：

```c
#define AJBOOL(b) (b ? "TRUE" : "FALSE")
```

**AjStatus** 旨在作为函数的通用返回代码，但目前未使用，因为 AjBool 已足够。它具有常量值，用于指示成功（ajStatusOK）、消息（ajStatusInfo）、警告（ajStatusWarn）、错误（ajStatusError）和致命错误（ajStatusFatal）。

**AjIntArray** 一个简单的 C 类型整数数组：

```c
typedef int* AjIntArray;
```

**AjFloatArray** 一个简单的 C 类型浮点数组：

```c
typedef float* AjFloatArray;
```

要使用这些 AJAX 数据类型，必须在代码中包含文件 ajdefine.h 和 ajarch.h。所有应用程序都必须在代码开头包含预处理器指令 #include "emboss.h"（参见第 2 章，您的第一个 EMBOSS 应用程序）。
emboss.h 是主包含文件，导入整个 EMBOSS 接口：它包含 AJAX 和 NUCLEUS C 编程库中的所有头文件，使所有代码可供您使用。如果您检查该文件，会看到包含了 ajax.h：

```c
% more nucleus/emboss.h

#ifndef emboss_h
#define emboss_h

#include "ajax.h"
#include "ajgraph.h"
.
.
```

它本身包含 ajdefine.h，而 ajdefine.h 包含 ajarch.h：

```c
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajdefine_h
#define ajdefine_h

#include "ajarch.h"
.
.
```

如果您开发使用基本类型的库代码，必须显式包含 ajdefine.h。例如，来自 ajstr.h：

```c
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajstr_h
#define ajstr_h

#include "ajdefine.h"
#include "ajtable.h"
.
.
```

### 5.1.3 派生类型

可能从基本 C 数据类型派生出无限多的其他类型，如下所示：

- 单一类型对象的数组
- 返回单一类型对象的函数
- 指向给定类型对象的指针
- 各种类型对象的结构
- 能够容纳多个不同数据类型对象之一的联合

这里的“对象”可能指具有原始数据类型的变量、函数、数据结构等。通常，这些方法可以以复合方式应用。例如，可以有一个包含函数数组的数据结构，这些函数都返回指向浮点变量数组的指针。指针提供对特定类型对象的句柄，并在管理对象内存时使用。

在 EMBOSS 下编程时，出于大多数目的，事情被简化了：

- 定义新数据结构及其指针有标准方法。数据结构类型和指针类型分别称为“对象”和“对象指针”。
- 非 void 函数通常返回原始数据类型或对象指针。
- 结构通过引用（对象指针）传递给函数：结构本身从不传递。
- 构造函数和析构函数处理对象内存管理。
- 提供了用于通用内存管理的宏。
- AJAX 实现了常见基本数据类型的动态数组，其内存管理自动处理。其他一些数据类型（例如字符串）的内存管理也自动处理。

### 5.1.4 存储类和链接

C 中有两种存储类：自动和静态。每当进入声明自动对象的代码块时（跳入代码的情况除外），都会按声明顺序对其进行初始化。相比之下，静态对象仅在程序正式启动前初始化一次。对象的存储类取决于其声明的上下文和使用的关键字。

自动对象是块局部的，并在退出块时被丢弃。块中的声明默认是自动的，尽管可以使用 auto 关键字显式声明。使用 register 声明的对象是自动的，并且在可能的情况下，会在最快可用的内存寄存器中处理。

静态对象可能是块局部的，也可能是与函数定义处于同一级别的所有块之外。无论哪种情况，在退出并重新进入块时，它们都会保留其值。它们使用关键字 static 声明。

对所有块外部的对象始终是静态的。在这种情况下，static 关键字赋予它们内部链接，这意味着它们仅在本地文件中可见。否则，它们具有外部链接，这意味着它们对整个程序或其他编译单元是全局的。

在为 EMBOSS 编程时，这里有几个含义。任何私有于库文件或应用程序的联合和 C 数据结构（对象）都应在库或应用程序 C 源代码文件中声明为 static。任何公共（外部）联合和结构都在相应的库头文件中给出，不应包含 static 关键字。同样，库中的所有应用程序函数和私有函数都应声明为 static。库中的公共函数不应包含此关键字。

避免将名称导出到单个 C 源文件之外；也就是说，尽可能将每个函数声明为 static（在库头文件或应用程序代码中）。如果代码仅特定于某个应用程序，则应保留在应用程序 C 源代码文件中，直到它更具通用性之前，不要将其移动到库中。

所有数据类型都应按 EMBOSS 风格定义，并且函数必须使用完整的 ANSI C 样式进行原型声明（参见附录 C，C 编码标准）。





## 5.2 C 指针入门

### 5.2.1 指针基础

指针可能是 C 编程中一个难以掌握的方面，其误用带来的问题比语言的其他任何部分都多。然而，只要正确理解其原理，事情就会容易得多。要想精通 EMBOSS 编程，你必须至少掌握指针的基础知识。

除了寄存器变量之外，你在程序中声明的每个变量都位于内存的某个位置，这个“某个位置”就是变量的内存地址。指针仅仅是一个值为该内存地址的变量。在大多数 C 实现中，硬件支持的最长无符号整数用于指针，例如 unsigned long int。这个整数的值是另一个对象（如另一个变量、C 数据结构等）的内存地址。

所以，当程序中的这一行被执行时：

```
ajint x=0;
```

将为程序保留足够的内存来容纳一个整数（通常为 4 字节）。这些字节的值被设置为零。

要声明一个指针变量，你在声明中使用指针运算符 (*)。所以当这一行被调用时：

```
ajint *ptr=NULL;
```

将为指针变量保留内存，并将变量的值设置为 NULL。

要返回变量的内存地址，你使用 &（地址）运算符：

```
ajint x=10;
ajint *ptr=NULL;
ptr = &x;
```

要访问特定内存地址处保存的值，你使用 *（指针）运算符；这称为解引用指针或通过间接方式获取值：

```
ajint x=10;
ajint y=0;
ajint *ptr=NULL;
ptr = &x;
y = *ptr; /* y is set to 10 */
```

从上面的代码可以清楚地看出，x 和 y 保存整数值，或者更简单地说，“x 和 y 是整数”。同样，ptr 保存一个内存地址，或者更简单地说，“ptr 是一个指针”。在上面的代码中，指针被指向 x。

如果你不使“指针是一个值为内存地址的变量”这一基本概念变得复杂，那么你就拥有了在 EMBOSS 中理解和使用指针的基础。

### 示例

考虑以下代码：

```
int main()
{
        ajint x=0;
/* 1. */      printf("Value of x : %d\n", x);
/* 2. */      printf("Memory address of x : %p\n", &x);
/* 3. */      printf("Value of x by indirection : %d\n", *(&x) );
}
/* Output will look like:
Value of x : 0
Memory address of x : #1
Value of x by indirection : 0
(In reality, a hexadecimal number would be printed instead of '#1',
but '#1' is easier to follow).
*/
```

变量名 x 是我们对保留内存的句柄。它指向位于内存地址 #1 的一个整数值。在代码中，执行了以下操作：

- 1. 首先打印 x 的值。
- 2. 然后使用 & 获取变量 x 的内存地址并打印它。
- 3. 然后使用 * 运算符解引用该地址并打印存储在那里的值。

### 5.2.1.1 声明指针

在实践中，指针保存特定对象（如整数、C 数据结构甚至另一个指针）的内存地址。声明指针时必须指定所指向的数据类型。这并不是因为 int 的内存地址与 float 的内存地址有任何不同，而是为了让编译器知道指针在源代码中如何使用。例如，编译器必须知道所指向的数据类型，才能访问所指向的内存，以便例如正确打印一个值。这就是为什么在 C 中指针按所示方式声明：

```
ajint *ptr=NULL;
```

声明中的 * 表示 ptr 是一个内存地址，而 ajint 告诉我们它是整数的地址，即 ptr 是指向整数的指针。

当该行程序被执行时，将为程序保留足够的内存来容纳一个内存地址。这与整数一样，在 32 位机器上通常为 4 字节。这 4 字节的值被设置为 NULL。

# 5 C 编程

重要的是要认识到 * 运算符的含义取决于上下文。只有在变量声明的上下文中，它才将变量声明为指针，例如：

```
ajint *ptr=NULL;
```

表示“ptr 是一个指针变量，将其值设置为 NULL”。

如果 * 出现在变量声明之外，它将表示像上面提到的那样对变量进行解引用，例如：

```
ajint *ptr=NULL;
*ptr = 0;
```

在这里，第二个 *ptr = 0; 表示“解引用 ptr 并将存储在那里的值设置为 0”，或者换句话说，“将内存地址 ptr 处保存的值设置为 0”。请注意，按原样编写的代码会崩溃——但这只是为了说明。

最后要提到的是，我们在声明中将 NULL 值赋给了指针，并在代码中将该内存地址存储的整数设置为 0。它们不能互换使用，因为它们不是同一类型：你应该只对指针使用 NULL。

你可以在下面的代码中看到这一点：

```
int main()
{
/* 1. */ ajint x=0;
/* 1. */ ajint *ptr=NULL;
/* 2. */ printf("Value of x : %d\n", x);
/* 3. */ ptr = &x;
/* 4. */ *ptr=5;
/* 2. */ printf("Value of x : %d\n", x);
}
/* Output will look like this:
Value of x : 0
Value of x : 5
*/
```

在代码中：

- 1. 声明一个整数和一个指向整数的指针。
- 2. 打印 x 的值。
- 3. 将 x 的地址赋给 ptr。
- 4. 通过间接方式将 x 的值设置为 5。

在上面的示例中，你通常会说“ptr 保存 x 的地址”，或者简单地说“ptr 指向 x”。

## 5.2.2 指向指针的指针

上面提到过，指针可以保存另一个指针的内存地址。当你意识到指针（像任何变量一样）位于内存的某个位置时，这很明显。所以，如果保存整数内存地址的指针是“指向整数的指针”，那么保存另一个指针内存地址的指针当然就是“指向指针的指针”。

这段代码展示了如何声明指向指向整数的指针的指针：

```
ajint *ptrto=NULL;
```

为了更好地理解，让我们将声明写成如下形式：

```
(ajint *) *ptrto=NULL;
```

第二个 * 表示 ptrto 是一个内存地址。ajint * 告诉我们它是指向整数的指针的地址。当代码执行时，将为我们保留足够的内存来容纳一个地址，并且字节的值被设置为 NULL。

当然，&（地址）和 *（指针）运算符仍然适用于指向指针的指针。当你有多级指针时，可以使用多个 *（指针）运算符进行解引用。*ptrto 将解引用一次并检索一个地址（指向整数的指针）。**ptrto 将解引用两次并检索一个整数。

你可以在下面的代码中看到这一点：

```
main()
{
/* 1. */ ajint x=0;       /* an integer */
/* 1. */ ajint *ptr=NULL;   /* a pointer to an integer */
/* 1. */ ajint **ptrto=NULL; /* a pointer to a pointer-to-an-integer */

/* 2. */ printf("Address of x : %p\n", &x);
/* 2. */ printf("Address of ptr : %p\n", &ptr);
/* 2. */ printf("Address of ptrto : %p\n", &ptrto);

/* 3. */ ptr = &x;
/* 3. */ ptrto = &ptr;

/* 4. */ printf("Value of x : %d\n", x);
/* 4. */ printf("Value of ptr : %p\n", ptr);
/* 4. */ printf("Value of ptrto : %p\n", ptrto);

/* 5. */ printf("Value of x by dereferencing ptr : %d\n", *ptr);
/* 5. */ printf("Value of x by dereferencing ptrto : %d\n", **ptrto);
/* Output will look like this:
Address of x : #1
Address of ptr : #2
Address of ptrto : #3

Value of x : 0
Value of ptr : #1   /* i.e. the address of x*/
Value of ptrto : #2 /* i.e. the address of ptr*/
Value of x by dereferencing ptr : 0
Value of x by dereferencing ptrto : 0
*/
```

上面的代码中没有新概念，它只是对你已经了解的指针知识的扩展：

- 1. 声明三个名为 x、ptr 和 ptrto 的变量。x 是整数，ptr 是指向整数的指针，ptrto 是指向指向整数的指针的指针。
- 2. 打印每个变量的地址；x 位于 #1，ptr 位于 #2，ptrto 位于 #3。
- 3. 将 x 的地址赋给 ptr。ptr 的地址赋给 ptrto。
- 4. 打印每个变量的值。x 的值为 0，ptr 的值为 x 的地址，即 #1，ptrto 的值为 ptr 的地址，即 #2。
- 5. 通过间接方式打印 x。

你已经知道 *ptr 的含义。接下来，ptrto 被解引用两次，如果你想从中获取整数，就必须这样做。第一次解引用 ptrto 时，你得到 ptr；第二次，你实际上是在解引用 ptr，这会带你到 x。

这一点，实际上所有指针操作，如果你在纸上草图说明正在发生的事情，都非常容易理解：如果你不确定指针发生了什么，请画一个图。

## 5.3 对象（C 数据结构）

要有效地使用 AJAX 和 NUCLEUS 库进行编程，你需要了解 EMBOSS 派生数据类型（对象）是如何定义和使用的。这些包括简单对象，如动态 AJAX 字符串和数组，以及更复杂的生物数据类型，如序列和比对。要使用新数据类型和函数扩展库的功能，你需要更深入地了解 C 指针和内存管理，以及它们在 EMBOSS 中的特定实现。

EMBOSS 从 C++ 借用了对象的概念。对象可以被视为一个“黑盒”，具有明确定义的输入和输出，但内部可能更加不透明，开发者无需关心。对象存储其自身的（成员）数据，并知道如何通过成员函数执行某些操作。从开发者的角度来看，只要接口（即输入和输出）保持不变，内部发生什么并不重要。使用对象允许程序员更紧密地根据问题建模代码，将其分解为小而易于管理的部分。

在 EMBOSS 中，对象是 C 数据结构定义。结构中的元素是成员数据。没有成员函数；但是，所有使用对象的函数都与数据元素一起，在 C 源文件的结构化文档中进行了记录。代码部分及其文档的一致结构强制执行了每个数据类型各部分中所有函数的命名和分类。此文档（参见附录 D，代码文档标准）在线使用，并可通过 SRS 访问（参见第 1.3 节，“开发者文档”）。EMBOSS 维护此



## 5.3 对象（C 数据结构）

link between datatypes and the functions that act upon them so that it’s easy to find the objects and functions you need.

### 5.3.1 对象定义

Objects in EMBOSS are defined (Appendix C, C coding standards) and documented (Appendix D, Code documentation standards) in a standard way.

A typical definition, for the public AJAX string object, is shown below and includes the standard documentation:

```
/* @data AjPStr *********************************************************************************************
**
** Ajax string object.
**
** Holds a null terminated character string with additional data.
** The length is known and held internally.
** The reserved memory size is known and held internally.
** The reference count is known and held internally.
** New pointers can refer to the same string without needing
** to duplicate the character data.
**
** If a string has multiple references it cannot be changed. Any
** instance to be changed is first copied to a new string. This
** means that any function which can change the character data must
** pass a pointer to the string so that the string can be moved.
**
** A default null string is provided. New strings are by default
** implemented as pointers to this with increased reference counters.
**
** AjPStr is implemented as a pointer to a C data structure.
**
** @alias AjPPStr
** @alias AjSStr
** @alias AjOStr
** @iterator AjIStr
**
** @attr Res [ajuint] Reserved bytes (usable for expanding in place)
** @attr Len [ajuint] Length of current string, excluding NULL at end
** @attr Ptr [char*] The string, as a NULL-terminated C string.
** @attr Use [ajuint] Use count: 1 for single reference, more if several
**     pointers share the same string.
**     Must drop to 0 before deleting. Modifying means making
**     a new string if not 1.
** @attr Padding [ajuint] Padding to alignment boundary
** @
*********************************************************************************************/

typedef struct AjSStr
{
    ajuint    Res;
    ajuint    Len;
    char    *Ptr;
    ajuint    Use;
    ajint    Padding;
}   AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

The declaration defines:

- The object name (AjSStr)
- A datatype for the string object proper (AjOStr)
- A datatype for the string object pointer (AjPStr)
- A datatype for a pointer to the string object pointer (AjPPStr).

> **注意**
>
> 对象指针 (AjPStr) 是你通常会使用的数据类型，因此 AjPStr 通常被称为“字符串对象”，而不是更繁琐的“字符串对象指针”。当然，AjPStr 指向内存中的字符串对象。

The datatype naming conventions are supposed to make the names intuitive:

- Aj indicates that the object belongs to the AJAX library
- P indicates that the datatype is a pointer
- Str gives a clue to the name of the AJAX library file in which the object is defined, i.e. the string-handling library ajstr.h.

Many other basic datatypes are available. For example the basic file object AjPFile is defined in the AJAX file ajfile.h whereas the input (AjPSeq) and output (AjPSeqout) sequence objects are in ajseqdata.h and ajseqwrite.h respectively. Different naming conventions apply for public NUCLEUS objects and for private objects including those listed in the application code (see Appendix C, C coding standards).

### 5.3.2 对象函数

You should never access the elements of an object directly, that is what the library functions are for. Objects should always be accessed by calling the appropriate functions. These are fully described by structured comments in a similar way to the objects themselves (see Appendix D, Code documentation standards). Functions are organised by the datatype they act upon and, for easier navigation, into sections of related functionality.

The function sections are supposed to help you to quickly find the functions you need. Functions in the same section tend to have similar names and return types, and similar number, order and type of parameters. As functions in the same section are all used in a similar way then programming with the libraries is reasonably intuitive.

Most of the sections are unique to a given library file however there are some common sections. For example, many of the library files have an ‘element retrieval’ section for functions which return a data element of an object and an ‘element set’ section for functions that set the value of a data element directly. Most of the complex biological datatypes have ‘input’ and ‘output’ sections for reading or writing the data to file in a formatted way. This includes input (AjPSeq) and output (AjPSeqout) sequence objects, application reports (AjPReport) and sequence alignments (AjPAlign).

The common sections are described in more detail in Appendix D, Code documentation standards.

The main thing to be aware of when using objects with functions is that object pointers (for example an AjPStr) are always used: a data structure proper is never passed to or returned from a function for reasons of efficiency. Furthermore, for consistency, all functions in EMBOSS should obey the following rules:

- If a function changes the pointer (so that it points to a new object) or changes the data pointed to in any way then the address of the object pointer is passed.
- If the function merely reads the data pointed to and does not change the pointer itself then the plain object pointer is passed.

Consider, for example, two functions in the AJAX string library ajstr.c: ajStrMatchS and ajStrAssignS. ajStrMatchS compares two strings and returns ajTrue if they are the same whereas ajStrAssignS copies one string value into another.

You can deduce that ajStrMatchS merely reads two string values and therefore object pointers will be passed. In contrast, ajStrAssignS must change the value of the destination string, possibly allocating a new string (as a failsafe in case a NULL pointer is passed to it) or reallocating a new bigger string in cases where a destination string is passed but is too small to hold the new value. In either case the string value will be changed and possibly the pointer too, therefore the address of the object pointer for the destination string is required.

The prototypes show that this is indeed the case:

```
AjBool ajStrMatchS(const AjPStr str, const AjPStr str2);
AjBool ajStrAssignS(AjPStr* Pstr, const AjPStr str);
```

The two strings (str and str2) passed to ajStrMatchS are only read from, therefore the parameters are object pointers (AjPStr). The source string (str) of ajStrAssignS is also read-only, whereas the destination string (Pstr) is modified and therefore the address must be passed (AjPStr* Pstr).

> **提示**
>
> 使用现有库函数时，你无需担心函数内部实现。文档说明是需要对象指针还是其地址。只要你向函数传递原型中显示的内容即可。此外，EMBOSS 应用程序代码是函数在实践中使用方式的丰富示例来源。

## 5.4 EMBOSS 中的内存管理

### 5.4.1 内存管理简介

Memory management in C can be a difficult area to master, especially if you are used to scripting or object-oriented languages where this aspect might be automatically taken care of. It requires a sound knowledge of pointers and discipline in coding but is one of the most powerful aspects of the language, allowing very memory-intensive code to be written in an efficient way that might not be feasible in other languages. Curiously many C programming books omit a detailed coverage of pointers and memory management, yet these areas account for most of the time spent debugging C programs. For this reason great effort has been made to make handling memory in EMBOSS as simple as possible.

Memory management when using the libraries is greatly simplified, at least when programming with the existing datatypes. As far as possible the developer is shielded from low-level C calls to allocate and free memory. This is achieved in the following ways:

- General memory management macros
- Object memory management macros
- Object constructor and destructor functions
- Failsafe object construction
- Dynamic objects
- EMBOSS is free of arbitrary limits.

### 5.4.1.1 通用内存管理宏

General memory management macros (Section 5.4.2.1, ‘General macros’) are provided to wrap the C malloc, calloc and free functions. malloc allocates memory with uninitialised content, calloc allocates memory and initialises it to zero, and free frees allocated memory. When programming using the libraries you should use the objects provided (or create new ones) and therefore will seldom need to call these C functions. In some cases, however, it is necessary or desirable to do so and you should use these associated macros.

### 5.4.1.2 对象内存管理宏

Macros (Section 5.4.2.2, ‘Object macros’) are provided to simplify the memory allocation for single objects and arrays of objects of any type, and for freeing that memory. Bear in mind these macros only allocate memory for a basic object (or an array of them) as defined by a single object definition. Where the object itself includes pointers for nested data structures then memory for these nested objects is not allocated. That is what the constructor functions are for (see below).

### 5.4.1.3 对象构造函数和析构函数

A constructor function (memory allocation) (Section 5.4.3.2, ‘Object construction’) and destructor function (freeing memory (Section 5.4.3.3, ‘Object destruction’)) are provided for every type of object. Their function goes beyond that of the object macros, which merely allocate or free a single block of memory referenced by a single pointer. Constructors will allocate the object and all nested objects and initialise the memory, possibly with values passed in by argument. Similarly, destructors ensure that all pointers nested within the structure are freed correctly and that the main object pointer passed is reset to NULL so that it’s ready for reuse in the calling code.





### 5.4.1.4 防故障对象构建

许多（但目前并非全部）修改通过参数传递的对象的函数，如果传递了未分配（NULL）指针，会为其分配内存。这是作为防止编程不严谨的安全措施提供的。你不应依赖它。建议在适当的情况下，在代码中使用所有对象指针之前显式分配内存，并在使用完后当然释放它们。

### 5.4.1.5 动态对象

大多数对象的内存由库函数根据需要动态重新分配（并释放）。这意味着例如你可以向字符串对象追加文本，而无需担心是否有足够的空间，或者向数组元素写入数据而无需先检查数组是否足够大（必要时会创建新元素）。同样，当内存不再需要时会自动释放。最常用的动态对象是提到的字符串和数组，但大多数对象函数都表现出这种行为。

### 5.4.1.6 EMBOSS 没有任意限制

代码中没有任意的硬编码限制。例如，序列长度或序列比对中的序列数量没有硬编码的最大值，你可以创建的矩阵大小也没有上限。唯一的限制来自你正在使用的硬件。

## 5.4.2 一般内存管理

### 5.4.2.1 一般宏

不要直接调用 malloc、calloc 或 free，而应使用提供的宏：

| 宏 | 说明 |
|---|---|
| AJALLOC(nbytes) | 分配 nbytes 字节的未初始化内存。这等同于使用 malloc。 |
| AJALLOC0(nbytes) | 分配 nbytes 字节的内存并将内存初始化为零。等同于使用 calloc。 |
| AJCALLOC(count, nbytes) | 分配一个包含 count 个 nbytes 字节元素的数组。数组元素未初始化。等同于使用 malloc。 |
| AJCALLOC0(count, nbytes) | 分配一个包含 count 个 nbytes 字节元素的数组并将内存初始化为零。等同于使用 calloc。 |
| AJRESIZE(ptr, nbytes) | 将先前分配的内存（由 ptr 引用）调整为 nbytes 的新大小。将新的额外保留内存（如果有）初始化为零。无论块是否移动，原始内存内容都会保留。如果传递了 NULL 指针，则会自动分配新的内存块。等同于使用 realloc。 |
| AJFREE(ptr) | 使用 free 释放内存并将指针设置为 NULL。忽略 NULL 指针。 |

这些宏中的大多数会分配（或重新分配）一些内存并返回指向它的指针。在失败的情况下，会返回 NULL 指针并引发异常。异常消息会打印到标准错误流，并且代码退出。异常消息包括源文件名和源行号。

对于大多数应用程序，你会使用 AJALLOC0 或 AJCALLOC0，因为默认将内存初始化为零更安全。如果你确定分配后内存会被覆盖，则应改用 AJALLOC 或 AJCALLOC 以提高效率。

### 5.4.2.2 对象宏

下面的宏用于创建任何类型的单个对象或对象数组，并释放该内存。它们为由单个对象定义定义的基本对象（或对象数组）分配内存。如果对象本身包含用于嵌套数据结构的指针，则这些嵌套对象的内存*不会*由这些宏分配（或释放）。它们通常从对象构造函数和析构函数中调用。

| 宏 | 说明 |
|---|---|
| AJNEW(ptr) | 为正确类型的单个对象分配内存到对象指针（p）。内存未初始化。这等同于使用 malloc。 |
| AJNEW0(ptr) | 为正确类型的单个对象分配内存到对象指针（p）。内存初始化为零。这等同于使用 calloc。 |
| AJCNEW(ptr, count) | 为正确类型的 c 个对象的数组分配内存到对象指针（p）。内存未初始化。这等同于使用 malloc。 |
| AJCNEW0(ptr, count) | 为正确类型的 c 个对象的数组分配内存到对象指针（p）。内存初始化为零。这等同于使用 calloc。 |
| AJCRESIZE0(ptr, count) | 将先前分配的对象数组（由 p 引用）调整大小，使其成为正确类型的 c 个对象的数组。将新的额外保留内存（如果有）初始化为零并保留原始内存内容。 |
| AJFREE(ptr) | 释放先前分配的对象或数组（由 ptr 引用）。测试内存指针是否具有非 NULL 值，以防止两次释放或释放未分配的内存。 |

### 5.4.2.3 基本 C 类型数据类型的数组

ajdefine.h 中定义了两种数据类型，用于处理 C 类型整数（int）和浮点数（float）的数组：

```
/* @datatype AjIntArray *************************************************************
***
*** Array of integers
***
*** @attr typedef [ajint*] Value
*** @@@
************************************************************************************/

typedef ajint* AjIntArray;

/* @datatype AjFloatArray ************************************************************
***
**
** Array of floats
**
** @attr typedef [float*] Value
** @@
**********************************************************************************/

typedef float* AjFloatArray;
```

它们可以与上面的宏一起用于为这些数组分配内存。典型用法如下所示：

```
AjIntArray integers = NULL;
AjFloatArray floats = NULL;
ajint dim = 10;

AJCNEW0(integers, dim);
AJCNEW0(floats, dim);

/* Do something with arrays */

AJFREE(integers);
AJFREE(floats);
```

### 5.4.2.4 内存泄漏

当你在源代码中丢失对已分配内存块的引用时，就会发生内存泄漏。这通常发生在不小心让指针指向其他地方，而没有先释放内存或复制指针并稍后释放它时。它们是 C 编程中最常见的错误来源之一，占用了大量调试代码的时间。如果你对指针（特别是 EMBOSS 中的指针实现）有深入理解，并在编码时采取有纪律的方法，则可以轻松避免泄漏。

至关重要的是，你要跟踪内存中到底有哪些对象，以及你持有哪些指向该内存的引用（指针）。如果在使用对象之前显式分配内存，并在使用完对象后稍后释放该内存，则可以避免大多数内存泄漏。要小心将析构函数调用与构造函数调用匹配。如果你依赖函数的防故障内存分配机制，则分配对你是隐藏的，代码中不再明显内存已被分配并需要释放。

考虑以下代码。

```
int main(int argc, char **argv)
{
    AjPStr mystring=NULL;

    embInit("noleaks", argc, argv);

    mystring = ajAcdGetString("astring")
    ajStrDel(&mystring);
    embExit();

    return 0;
}
```

声明了一个 AJAX 字符串对象（AjPStr）并调用 embInit 以调用 ACD 文件处理。读取 ACD 文件并提示用户输入值。对 embInit 的调用还为所有 ACD 数据项分配内存并初始化对象（参见第 6.3 节，“处理 ACD 文件”）。

例如，在使用 ajAcdGetString 调用检索字符串（AjPStr）数据项时，该函数将返回指向由 embInit 创建的字符串的指针。这意味着你不需要先为字符串分配内存，这就是上述代码没有显式调用字符串构造函数的原因。

尽管如此，embInit 创建了一个字符串对象，并且在使用完它后必须释放它。这就是 ajStrDel(&mystring); 调用的目的。如果你省略了这一步，那么你将依赖操作系统在应用程序退出时释放进程内存。这严格来说不是内存泄漏，但属于不良实践。

在以下代码中，字符串构造函数 ajStrNewC 被不必要地调用：

```
```c
int main(int argc, char **argv)
{
    AjPStr mystring=NULL;

    embInit("leaks", argc, argv);

    mystring = ajStrNewC("Hello");
    mystring = ajAcdGetString("astring")        /* Memory leak */
    ajStrDel(&mystring);

    embExit();

    return 0;
}
```
```

字符串对象指针（mystring）与之前一样被定义，并被指向由 ajStrNewC() 分配的新对象。然后，通过调用 ajAcdGetString，同一个指针被指向由 embInit 分配的字符串。你丢失了对 ajStrNewC 分配的内存的控制。换句话说，你创建了一个内存泄漏。

**注意**

这里描述的不是创建内存泄漏的唯一方法。关于如何避免泄漏的详细信息在编程指南中针对各个数据类型进行了描述（参见第 6.2 节，“编程指南”）。提交到 EMBOSS 的所有代码都应经过适当的测试和调试，以确保其不会泄漏内存（参见第 3.3 节，“调试”）。

## 5.4.3 对象内存管理

### 5.4.3.1 简介

在 C++ 中，对象是该对象实例的定义或模板。实例是可以操作的实际事物。如果你想做任何事情，必须在内存中创建一个实例，即实例化对象。在使用 EMBOSS 对象进行编程时，它的



重要的是要区分对象指针和驻留在内存中的对象本身（或实例）。对象指针仅仅是一个保存特定类型对象内存地址的变量。对象本身是驻留在内存中的对象的特定实例。

原则上，可以通过以下方式实例化（为对象分配内存）：

```
#include "emboss.h"
int main(void)
{
    AjOStr my_structure;
    /* Do something with my_structure */
    AJFREE(my_structure);
}
```

my_structure 的声明将在内存中创建一个单个字符串对象，之后通过调用 AJFREE 释放。但是，EMBOSS 不采用这种方法，因为如前所述，出于效率和便利性的原因，始终使用对象指针。上述定义不给予程序员管理对象内存的自由。即使你只需要一个结构，也绝不应该使用（例如）AjOStr，因为这与 EMBOSS 的其余部分不一致。无论如何，上述代码几乎肯定会失败，因为库处理字符串对象的方式。AJFREE 也不会释放 my_structure 中任何所需的内部内存分配。

### 注意

实例化对象的标准方法是向对象指针动态分配内存。出于这个原因和简洁性，例如，AjPStr 可能被称为“对象”，尽管“对象指针”更准确。术语并不重要，只要你明白你正在处理的是指针还是内存中的结构。

所有对象都应该动态分配，并在使用完毕后释放。这很容易，因为每种类型的对象都提供了构造函数（用于内存分配）和析构函数（用于释放内存）。

例如，考虑以下代码：

```
#include "emboss.h"
int main(int argc, char **argv)
{
    AjPStr my_string=NULL;
    embInit("helloworld", argc, argv);
    my_string = ajStrNew();
    ajStrAssignC(&my_string, "Hello, World!\n");
    ajFmtPrint("%S", my_string);
    ajStrDel(&my_string);
    embExit();
    return 0;
}
```

AjPStr my_string=NULL; 声明对象指针并将其初始化为 NULL。声明指针时应始终将其设置为 NULL，因为 EMBOSS 函数假设非 NULL 指针已分配了内存。如果不将指针设置为 NULL，则程序运行时它可能会接收到一些垃圾值，任何使用它的函数都可能错误地假设已为其分配了内存。这可能导致段错误或总线错误！

ajStrNew() 是构造函数。它概念上为对象分配一块内存并返回分配块的内存地址。内存地址保存在变量 my_string 中。暂时忽略对 ajStrAssignC 和 ajFmtPrint 的调用。

ajStrDel() 是析构函数。它不仅必须释放内存，还必须将指针重新设置为 NULL，以便其准备好重复使用。你看，my_string 的地址被传递。你可能会想，my_string 本身就是一个指针，为什么需要传递它的地址？如果你记住在 C 中函数参数是“按值”传递的，答案很简单。每个参数的临时副本会被创建并传递给函数，而不是原始参数。虽然指针的副本足以释放其指向的内存，但如果你想将原始指针设置为 NULL，则需要对原始指针（即其地址）有一个句柄。因此需要传递 my_string 的地址（&my_string）。

## 5.4.3.2 对象构造

构造函数（构造函数）返回内存中新对象的指针。需要考虑四种基本类型的构造函数：

- ACD 数据构造函数
- 默认构造函数
- 替代构造函数
- 主要目的不是对象构造但会在必要时作为故障安全措施构造对象的函数，例如，如果为函数的输出参数传递了 NULL 指针。

在管理对象内存时，需要了解任何被调用函数的行为。需要区分三种情况：

- 函数需要一个预先存在的对象
- 函数可以使用但不需要预先存在的对象，并在必要时分配一个
- 函数始终分配一个对象，并返回指向它的指针或分配一个对象指针，其地址已作为参数传递。

在大多数但并非所有情况下，从函数名称可以明显看出函数是构造函数还是仅使用对象。

### 5.4.3.2.1 ACD 数据构造

ACD 数据构造函数用于返回在应用程序 ACD 文件中定义的对象。它们都定义在 ajacd.h/c 中，并具有通用名称：

```
ajAcdGetDatatype
```

其中 Datatype 是受支持的 ACD 数据类型之一（第 A.2 节，“数据类型”）。

严格来说，它们不是构造函数，而是返回一个指向适当 AJAX 对象的指针，该对象已通过调用 embInit 函数分配，所有 EMBOSS 应用程序都必须使用该调用（参见第 6.3 节，“处理 ACD 文件”）。例如，ajAcdGetString 返回一个指向 AJAX 字符串对象（AjPStr）的指针，该对象通过解析 ACD 字符串（string）数据定义生成：

```
AjPStr ajAcdGetString (const char *token) ;
```

token 参数是要读取的 ACD 数据定义的名称。数据定义中的属性和/或在 ACD 文件处理期间收集的用户输入用于初始化对象。任何新对象的内存必须在 main() 函数中稍后释放。这些函数的用法在其他地方有详细说明（参见第 6.3 节，“处理 ACD 文件”）。

### 5.4.3.2.2 默认对象构造

默认对象构造函数是在源代码中创建未在 ACD 文件中定义的新对象的常用方法。它们的名称通常带有后缀 New，且没有参数。例如：

```
AjPStr ajStrNew (void) ; /* Create a string object. */
```

此类函数用于各个数据类型的用法在库编程指南中有描述（参见第 6.2 节，“编程指南”）。

### 5.4.3.2.3 替代对象构造

替代构造函数提供创建新对象的不同方式，通常具有用于初始化对象中元素的参数。它们的名称中包含 New 以明确其行为。例如：

```
AjPStr ajStrNewC (const char *txt);
/* Construct from
C-type string */
AjPStr ajStrNewResC (const char *txt, ajuint size);
/* Construct from
C-type string with reserved size */
```

此类函数用于各个数据类型的用法在库编程指南中有描述（参见第 6.2 节，“编程指南”）。

### 5.4.3.2.4 故障安全构造

大多数向通过参数传递的对象写入的函数会在必要时为对象分配内存。这种安全措施防止在传递未分配（NULL）指针的情况下出现故障和错误。在实践中，建议在适当的情况下，在使用之前在代码中显式分配所有对象指针。考虑字符串赋值函数 ajStrAssignS，它将一个字符串值（str）复制到另一个（Pstr）：

```
AjBool ajStrAssignS (AjPStr* Pstr, const AjPStr str);
```

从名称上完全看不出，如果传递 NULL，此函数会为 Pstr 分配一个字符串对象。因此，如果你依赖故障安全构造行为，这会使你的代码变得晦涩难懂。因此，你应该将此行为编码到你编写的任何新函数中，但不要依赖你调用的函数中的此行为。

### 5.4.3.3 对象销毁

析构函数（析构函数）释放对象指针指向的内存，并将其重置为 NULL，以便其准备好重复使用。对于大多数对象，都有一个默认析构函数，这是在源代码中删除对象的典型方法。这些函数有一个参数，即正在释放的对象指针的地址。在少数情况下，存在具有非标准行为的替代析构函数，例如带有参数以提供对对象中未释放的某些元素的句柄。通常，对象的所有析构函数都列在库文件的 C 源代码（和文档）的单个部分下，并且名称中包含 Del，最常作为后缀。例如：

```
AjPStr ajStrDel (AjPStr *Pstr); /* Delete a string object. */
```

## 5.5 使用对象进行编程

为了巩固你对指针、对象和内存管理的知识，我们将使用三个案例来说明它们在编程 EMBOSS 代码时的用法。首先看一下 AjPPdbtosp 对象，它保存序列代码。它不广泛使用，但很好地说明了许多关键点。然后是 AJAX 字符串对象 AjPStr 以及确保对象函数故障安全内存分配所需的特殊内存处理。最后是 AJAX 数组对象，以了解其他动态对象的实现方式。

### 5.5.1 示例对象：AjPPdbtosp

### 5.5.1.1 对象定义

考虑以下对象，它保存蛋白质数据库（PDB）代码的 SwissProt 代码和登录号：



/* @data AjPPdbtosp ***********************************************************
**
** Ajax Pdbtosp object.
**
** Holds swissprot codes and accession numbers for a PDB code.
**
** AjPPdbtosp is implemented as a pointer to a C data structure.
**
** @alias AjSPdbtosp
** @alias AjOPdbtosp
**
** @attr Pdb [AjPStr] PDB code
** @attr Acc [AjPStr*] Accession numbers
** @attr Spr [AjPStr*] Swissprot codes
** @attr n [ajint] No. entries for this pdb code
** @attr Padding [char[4]] Padding to alignment boundary
**
** @@
********************************************************************************/

typedef struct AjSPdbtosp
{
    AjPStr Pdb;
    AjPStr *Acc;
    AjPStr *Spr;
    ajint n;
    char Padding[4];
} AjOPdbtosp;
#define AjPPdbtosp AjOPdbtosp*

这里除了 Acc 和 Spr 之外没有什么新内容，它们都是指向 AjPStr 对象的指针。本应使用 AjPPStr 来声明它们，但此处并未这样做。由于 AjPStr 本身就是一个指针（指向字符串对象本身），可以看出我们正在处理指向指针的指针。在此例中，Acc 和 Spr 用于创建两个字符串数组，如下面的构造函数所示。

### 5.5.1.2 对象构造

以下是构造函数：

```
/* @func ajPdbtospNew ***********************************************************
**
** Pdbtosp object constructor. Fore-knowledge of the number of entries is
** required. This is normally called by the ajPdbtospReadCNew /
** ajPdbtospReadNew functions.
**
** @param [r] n [ajint] Number of entries
**
** @return [AjPPdbtosp] Pointer to a Pdbtosp object
** @@
********************************************************************************/
AjPPdbtosp ajPdbtospNew(ajint n) /* 1. */
{
    AjPPdbtosp ret = NULL; /* 2. */
    ajint i = 0;

    AJNEW0(ret); /* 3. */
    ret->Pdb = ajStrNew(); /* 5. */

    if (n)
    {
        AJCNEW0(ret->Acc, n); /* 4. */
        AJCNEW0(ret->Spr, n); /* 4. */
        for (i = 0; i < n; i++)
        {
            ret->Acc[i] = ajStrNew(); /* 6. */
            ret->Spr[i] = ajStrNew(); /* 6. */
        }
    }

    ret->n = n; /* 7. */

    return ret;
}
```

注释行说明如下：

- 1. 第一行声明该函数返回类型为 AjPPdbtosp 的对象指针。参数 ajint n 是 Acc 和 Spr 数组的大小，即对象将保存的 Acc / Spr 值对的数量。

- 2. 下一行声明一个名为 ret 的变量。这是即将分配内存并将返回给调用函数的对象指针。

- 3. AJNEW0(ret); 是为指针 ret 分配实际对象的行。此时它将指向一个 AjPPdbtosp 内存实例。当 AJNEW0(ret); 返回时，已为 AjPPdbtosp 对象预留内存空间。这意味着有足够空间容纳一个 AjPStr、一个 ajint 和两个指针（AjPStr *）。请注意，两个数组或任何实际字符串对象尚未分配！

AJNEW0 将结构体的所有元素设置为 0，这意味着元素 n 被设置为 0，三个指针被设置为 NULL。AJNEW0 是一个宏：它会为传递给它的任何指针分配正确类型的单个对象——它可以用于任何对象。

- 4. 将 AJNEW0 与两个 AJCNEW0 行进行比较。AJCNEW0 会分配任意类型的对象数组，并按要求将新变量初始化为 0 或 NULL。在此例中，将创建各包含 n 个对象的数组。这里需要牢记，ret->Acc 和 ret->Spr 被传递给了宏。它们的类型是 AjPStr *，这意味着它们所指向的‘对象’实际上是另一个指针变量。因此，这些宏调用将分配 n 个指针的数组，而不是人们可能（错误地）最初想象的 AjPStr 对象实例数组。

它们为 Acc 和 Spr 各创建一个包含 n 个 AjPStr 对象指针的数组。换句话说，ret->Acc 和 ret->Spr 将指向各自持有 n 个指针变量的内存块，这些指针目前为 NULL（未分配）。

- 5. 数组已创建，但字符串尚未创建。ret->Pdb = ajStrNew(); 为新对象中的 Pdb 指针分配字符串对象的内存。请注意，-> 用于解引用指针 ret 并访问 Pdb 元素。这是在 C 中通过指针访问数据结构元素的标准方式。

- 6. 行 ret->Acc[i] = ajStrNew(); 和 ret->Spr[i] = ajStrNew(); 为每个数组分配 n 个字符串对象的内存。这也说明了指针和数组表示法如何共同使用。在此例中，访问了 ret->Acc 和 ret->Spr 所指向数组的第 i 个元素。这些数组中的元素是 AjPStr（对象指针），并为每个元素分配了一个字符串对象。

- 7. 其余部分显而易见。对象中的整数被设置为数组的大小，指向新对象（包含已分配的字符串和两个字符串数组）的指针通过 return ret; 返回给调用函数。请注意，构造函数应以安全的方式处理负参数，但此处未实现。

### 5.5.1.3 对象销毁

析构函数的工作是释放对象本身及其成员元素可能指向的任何内存。析构函数会安全地清理构造函数分配的所有内存。这通过根据需要调用其他析构函数并使用 AJFREE 来实现。代码如下所示：

```
/* @func ajPdbtospDel *************************************************************
**
** Destructor for Pdbtosp object.
** *
** @param [w] thys [AjPPdbtosp*] Pdbtosp object pointer
**
** @return [void]
** @@
**********************************************************************************/

void ajPdbtospDel(AjPPdbtosp *thys) /* 1. */
{
    AjPPdbtosp pthis = NULL; /* 2. */
    ajint i;

    if (!thys)
        return;

    pthis = *thys;

    if (!pthis)
        return;

    ajStrDel(&pthis->Pdb); /* 3. */

    if (pthis->n)
    {
        for (i = 0; i < pthis->n; i++)
        {
            ajStrDel(&pthis->Acc[i]); /* 4. */
            ajStrDel(&pthis->Spr[i]); /* 4. */
        }

        AJFREE(pthis->Acc); /* 5. */
        AJFREE(pthis->Spr); /* 5. */
    }
    AJFREE(pthis); /* 6. */
    (*thys) = NULL; /* 6. */
    return;
}
```

同样，以下是逐条注释的说明：

- 1. 该函数（如同所有析构函数一样）接受要删除的对象指针的地址（AjPPdbtosp *thys）。

- 2. 为方便起见，声明了第二个指针，并在以下行中用于解引用 thys。这纯粹是为了清晰起见。如果传入了空地址或存储的指针为 NULL，则函数返回。

- 3. 首先通过传递字符串的地址调用默认析构函数来删除 AjPPdbtosp 中的字符串对象。

- 4. 通过数组引用的实际字符串对象，通过在两个数组的每个数组元素上循环调用 ajStrDel 来删除。

- 5. 然后调用 AJFREE 删除数组本身，由 pthis->Acc 和 pthis->Spr 引用。

- 6. 循环结束后，再次调用 AJFREE，这次释放 AjPPdbtosp 对象本身的内存。指针被设置为 NULL，以便调用函数可以重复使用。

应当清楚，虽然 AJFREE 会释放其参数所指向的内存，但在此处使用时，它释放的是数组本身，而不是所指向的实际字符串对象；释放实际字符串对象是前面代码中 ajStrDel 调用的工作。

### 5.5.1.4 使用示例

以下是一段代码片段，说明如何使用对象构造函数和析构函数。您会发现它们的使用方式与任何其他对象完全相同：

```
int main()
{
    AjPPdbtosp ptr = NULL;

    ptr = ajPdbtospNew(10);
    ajPdbtospDel(&ptr);

    /* ptr will have been reset to NULL now, and is ready for reuse */
    ptr = ajPdbtospNew(10);
    ajPdbtospDel(&ptr);
}
```





## 5.5.2 AJAX 动态字符串对象

### 5.5.2.1 简介

The string object (`AjPStr`) is one of the simplest of all the AJAX objects. AJAX strings have more functions than any other datatype and are used by many other objects. Two features distinguish its use from standard C-type (`char *`) strings. First, AJAX strings are dynamic objects, meaning that memory is dynamically reallocated as needed so that you never run out of space when using the object functions; a string will grow automatically as required.

字符串对象（`AjPStr`）是所有 AJAX 对象中最简单的一种之一。AJAX 字符串的功能比任何其他数据类型都多，并且被许多其他对象使用。有两个特点使其用法与标准 C 类型（`char *`）字符串有所不同。首先，AJAX 字符串是动态对象，这意味着内存会根据需要动态重新分配，因此在使用对象函数时永远不会用完空间；字符串会根据需要自动增长。

Second, AJAX strings are reference counted. This means that the object itself keeps track of how many references (pointers) to the string there are in the code that have been requested by calling library functions. It is not until all references to a string are deleted that the string itself is freed. This ensures that broken references to a string do not occur and that you always have a handle on objects in memory.

其次，AJAX 字符串是引用计数的。这意味着对象本身会跟踪代码中对字符串的引用（指针）数量，这些引用是通过调用库函数请求的。只有当对字符串的所有引用都被删除时，字符串本身才会被释放。这确保了不会出现对字符串的损坏引用，并且你始终可以掌控内存中的对象。

### 5.5.2.2 字符串定义

The string definition is shown below:

字符串定义如下：

```c
typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

A structure is defined called `AjSStr` of four elements (`Len`, `Res`, `Use` and `Ptr`) and with three new datatype names, `AjOStr` for the object itself, `AjPStr` for the object pointer and `AjPPStr` for a pointer to an `AjPStr`.

定义了一个名为 `AjSStr` 的结构体，包含四个元素（`Len`、`Res`、`Use` 和 `Ptr`），以及三个新的数据类型名称：`AjOStr` 表示对象本身，`AjPStr` 表示对象指针，`AjPPStr` 表示指向 `AjPStr` 的指针。

The `Ptr` pointer is just a standard C one which holds a character string and `Len` is its length. In contrast to C-type strings, the character string may or may not be NULL terminated; the library functions for printing `AjPStr` objects use the length field (`Len`) for how many characters to print and won't stop at the first NULL if there is one.

`Ptr` 指针只是一个标准的 C 指针，用于保存字符串，而 `Len` 是其长度。与 C 类型字符串不同，字符串可能以 NULL 结尾，也可能不是；打印 `AjPStr` 对象的库函数使用长度字段（`Len`）来确定打印多少个字符，即使存在 NULL 也不会在第一个 NULL 处停止。

The `Res` element indicates how much reserved dynamic memory is associated with the object. This is always at least equal to `Len` but is often more. `Res` is and should be outside your direct control. If you use a library call to add anything to the string then, if it'll fit within the memory given by `Res` then the operation is performed immediately. If the memory required is larger than `Res` then more memory is allocated and the `Res` item is updated. More memory than required is usually allocated.

`Res` 元素指示与对象关联的保留动态内存量。这始终至少等于 `Len`，但通常更多。`Res` 是且应超出你的直接控制范围。如果你使用库调用向字符串添加任何内容，那么如果它能放入 `Res` 给出的内存中，则操作会立即执行。如果所需内存大于 `Res`，则会分配更多内存并更新 `Res` 项。通常会分配比所需更多的内存。

`Use` is the string usage counter. Sometimes you'll want two or more references to a single string rather than making a genuine copy. EMBOS functions that do this increment the string's usage counter. The usage counter is decremented when a call to destroy either the string itself, or a reference to it, is made. When the usage counter reaches zero the object will be deleted. All of this is function internals, so you don't need to worry about it as long as you don't change the object elements directly. If you intend altering the contents of an object then safety is guaranteed if you use the available library functions.

`Use` 是字符串使用计数器。有时你希望对单个字符串有两个或多个引用，而不是制作真正的副本。执行此操作的 EMBOS 函数会递增字符串的使用计数器。当销毁字符串本身或对其引用的调用发生时，使用计数器会递减。当使用计数器达到零时，对象将被删除。所有这些都是函数内部机制，因此只要你不直接更改对象元素，就不需要担心它。如果你打算修改对象的内容，那么只要使用可用的库函数，安全性就有保障。

Finally, the Padding element indicates the number of characters used to pad the string to its alignment boundary and is used only to keep pedantic compilers happy.

最后，Padding 元素指示用于将字符串填充到其对齐边界的字符数，仅用于让吹毛求疵的编译器满意。

### 5.5.2.3 字符串构造

Code for the default constructor function is shown below:

默认构造函数的代码如下：

```c
/* @func ajStrNew ****************************************************
**
** Default string constructor which allocates memory for a string.
**
** The null string usage pointer is incremented.
**
** @return [AjPStr] Pointer to an empty string
** @@
****************************************************************************/
AjPStr ajStrNew(void)
{
    return ajStrNewRef(strPNULL);
}
```

You can see that the ajStrNew is a wrapper function to ajStrNewRef. It passes to ajStrNewRef an internal string object called strPNULL which is defined in ajstr.c:

你可以看到 ajStrNew 是 ajStrNewRef 的包装函数。它将一个名为 strPNULL 的内部字符串对象传递给 ajStrNewRef，该对象在 ajstr.c 中定义：

```c
#define NULL_USE 1
char charNULL[1] = "";

AjOStr strONULL = { 1, 0, charNULL, NULL_USE, 0 };
AjPStr strPNULL = &strONULL;
```

strPNULL is a global variable for an empty object called the 'AJAX NULL string'. This has a single character of reserved memory, length of zero, a C-type string which is set to NULL, a reference count of 1 and zero padding.

strPNULL 是一个全局变量，用于一个名为“AJAX NULL 字符串”的空对象。它具有一个字符的保留内存，长度为零，一个设置为 NULL 的 C 类型字符串，引用计数为 1 以及零填充。

If you look at ajStrNewRef:

如果你查看 ajStrNewRef：

```c
/* @func ajStrNewRef *****************************************************
**
** String referencing function which returns a pointer to the string passed in
** and increases its reference count.
**
** Not a true string copy, but if modified the new string will behave
** as a copy.
**
** @param [u] refstr [AjPStr] AJAX string object
** @return [AjPStr] Pointer to the string passed as an argument,
**                 with its use count increased by 1.
** @@
*****************************************************************************/
AjPStr ajStrNewRef(AjPStr refstr)
{
    if(!refstr)
        ajFatal("ajStrNewRef source string NULL");

    refstr->Use++;

    return refstr;
}
```

All this function does is increase the reference count of the object that was passed and return the same pointer. It raises a fatal error if NULL was passed.

此函数所做的全部就是增加传递对象的引用计数并返回相同的指针。如果传递了 NULL，它会引发致命错误。

In other words, a call to ajStrNew doesn't immediately instantiate an AjSStr object, it just returns the address of the 'global AJAX NULL string'. It's only when the char * string (Ptr) is given a non-NULL value (by whatever means) that memory for the string object proper will be allocated. AJAX is programmed in this way for maximum speed and efficiency of string handling. You can see this for yourself if you print the reference count of a string which you have just allocated using ajStrNew but not yet used. You might be surprised at the value of the usage count which is higher than you might expect. The reference count may well be in the hundreds owing to the call to embInit in the application code, which itself makes, indirectly, many calls to ajStrNew. If true objects had been allocated for all these strings the code would be less efficient.

换句话说，调用 ajStrNew 不会立即实例化一个 AjSStr 对象，它只是返回“全局 AJAX NULL 字符串”的地址。只有当 char * 字符串（Ptr）被赋予非 NULL 值（通过任何方式）时，才会为字符串对象本身分配内存。AJAX 以这种方式编程，以实现字符串处理的最大速度和效率。你可以自己验证这一点：打印使用 ajStrNew 刚刚分配但尚未使用的字符串的引用计数。你可能会对使用计数的值感到惊讶，它比你预期的要高。引用计数可能高达数百，这是因为应用程序代码中的 embInit 调用本身间接地进行了许多 ajStrNew 调用。如果为所有这些字符串都分配了真正的对象，代码效率会更低。

Things are different if you call the alternative constructor function ajStrNewRes, which allocates memory for a string with an initial reserved size:

如果你调用替代构造函数 ajStrNewRes，情况就不同了，它会为具有初始保留大小的字符串分配内存：

```c
/* @func ajStrNewRes ************************************************************
**
** String constructor which allocates memory for a string of an initial
** reserved size (including a possible null).
**
** @param [r] size [ajuint] Reserved size (including a possible null).
** @return [AjPStr] Pointer to an empty string of specified size.
**
** @@
**********************************************************************************/
AjPStr ajStrNewRes(ajuint size)
{
    AjPStr thys;

    thys = ajStrNewResLenC("", size, 0);

    return thys;
}
```

The function declares an AJAX string object (thys) then calls ajStrNewResLenC to allocate the string, passing to that function the size (size) of the required string:

该函数声明一个 AJAX 字符串对象（thys），然后调用 ajStrNewResLenC 来分配字符串，将所需字符串的大小（size）传递给该函数：

```c
/* @func ajStrNewResLenC ************************************************************
**
** String constructor which allocates memory for a string of a given length
** and of an initial reserved size (including a possible null) and initialises
** it with the text string provided.
**
** @param [r] txt [const char*] Null-terminated character string to initialise
** the new string.
** @param [r] size [ajuint] Reserved size (including a possible null).
** @param [r] len [ajuint] Length of txt to save calculation time.
** @return [AjPStr] Pointer to a string of the specified size
** containing the supplied text.
** @@
********************************************************************************/
AjPStr ajStrNewResLenC(const char* txt, ajuint size, ajuint len)
{
    AjPStr thys;
    ajuint minlen;

    minlen = size;

    if(size <= len)
        minlen = len+1;

    thys = strNew(minlen);
    thys->Len = len;
    if(txt)
        memmove(thys->Ptr, txt, len+1);

    thys->Ptr[len] = '\0';

    return thys;
}
```

This function is an alternative constructor function. It sets a minimum string length (minlen) to the requested reserved size (size), or to the current length (len) plus 1 (for a terminating NULL character) if the requested size is not greater than the current length. It then calls strNew which is a static function in ajstr.c to allocate a string object (this function is shown below). The string length (thys->Len) is set, and the specified text (txt, which is an empty string when called by ajStrNewRes as in this example) is copied (using memmove) to the C-type string pointer (thys->Ptr) in the AJAX string object. A terminating NULL character is added.

这是一个替代构造函数。它将最小字符串长度（minlen）设置为请求的保留大小（size），或者如果请求的大小不大于当前长度，则设置为当前长度（len）加 1（用于终止 NULL 字符）。然后它调用 strNew，这是 ajstr.c 中的一个静态函数，用于分配字符串对象（此函数如下所示）。字符串长度（thys->Len）被设置，指定的文本（txt，在 ajStrNewRes 调用时为空字符串，如本示例所示）被复制（使用 memmove）到 AJAX 字符串对象中的 C 类型字符串指针（thys->Ptr）。添加了一个终止 NULL 字符。

Let's look at the static constructor function which actually allocates the string object:

让我们看看实际分配字符串对象的静态构造函数：

```c
/* @funcstatic strNew ***********************************************************
**
** Internal constructor for modifiable AJAX strings. Used by all the string
** parameterized constructors to allocate the space for the text string.
** The exception is ajStrNew which returns a clone of the null string.
**
** @param [rE] size [ajuint] size of the reserved space, including the
** terminating NULL character. Zero uses a default string size STRSIZE.
** @return [AjPStr] A pointer to an empty string
** @@
********************************************************************************/

static AjPStr strNew(ajuint size)
{
    AjPStr ret;

    if(!size)
        size = STRSIZE;

    AJNEW0(ret);
    ret->Res = size;
    ret->Ptr = AJALLOCO(size);
    ret->Len = 0;
}
```





```
ret->Use = 1;
ret->Ptr[0] = '\0';
strAlloc += size;
strCount++;
strTotal++;
return ret;
}
```

该函数首先检查是否指定了保留大小，如果未指定，则将其设置为默认长度 STRSIZE。STRSIZE 在 ajstr.c 中定义：

```
#define STRSIZE 32
```

调用宏 AJNEW0。你会回想起，这相当于 calloc 的调用，为给定类型的单个对象（在此例中为字符串）分配内存到对象指针（ret）。内存被初始化为零。

该代码块的其余部分将正确值赋给字符串对象中的其他元素。你可以看到，保留大小被设置为 size，字符串的第一个字符被设置为 NULL 字符，这意味着你得到了一个带有指定保留大小的新空字符串，其指针被返回给调用函数。

代码还设置了一些内部用于统计和调试字符串的全局变量（strAlloc、strCount 和 strTotal）。你无需担心这些。

### 5.5.2.4 字符串销毁

字符串销毁的内部实现比构造更简单。默认析构函数 ajStrDel 如下所示：

```
/* @func ajStrDel **********************************************************************************************
**
** Default string destructor which frees memory for a string.
**
** Decrements the use count. When it reaches zero, the string is removed from
** memory. If the given string is NULL, or a NULL pointer, simply returns.
**
** @param [d] Pstr [AjPStr*] Pointer to the string to be deleted.
** The pointer is always deleted.
** @return [void]
** @cre The default null string must not be deleted. Calling this
** routine for copied pointers could cause this. An error message
** is issued and the null string use count is restored.
** @@
******************************************************************************************/
void ajStrDel(AjPStr* Pstr)
{
AjPStr thys;

if(!Pstr)
return;

if(!*Pstr)
return;

thys = *Pstr;

--thys->Use;
if (!thys->Use)
{   /* any other references? */
    if (thys == strPNULL)
    {
        ajErr("Error - trying to delete the null string constant\n");
        thys->Use = NULL_USE;   /* restore the original value */
    }
    else
    {
        AJFREE(thys->Ptr);      /* free the string */

        strFree += thys->Res;
        strFreeCount++;
        strCount--;
        thys->Res = 0;          /* in case of copied pointers */
        thys->Len = 0;

        AJFREE(*Pstr);          /* free the object */
    }
}

*Pstr = NULL;

return;
}
```

从 AjPStr* Pstr 可以清楚地看出，该函数接受字符串对象指针的地址。函数首先检查未传递 NULL（if (!Pstr)），且指针本身也不是 NULL（if (!*Pstr)）。换句话说，它确保按引用传入的 AjPStr 确实指向某个对象。函数必须假设它指向一个字符串，如果代码中没有错误，情况确实如此。这就是为什么声明指针时应将其设置为 NULL。如果不这样设置，且在启动时接收到某个垃圾值，那么此函数（以及许多类似函数）将错误地假设它引用了有效内存，在尝试访问该内存时，最好的结果也会导致段错误或总线错误。

行 --thys->Use; 将字符串的引用计数减 1。如果变为零，则使用 AJFREE 释放对象。它被调用两次，一次用于释放 C 类型字符串（AJFREE (thys->Ptr); ），另一次用于释放对象本身（AJFREE (*Pstr) ;）。一些内部用于调试和统计的全局变量（strFree、strFreeCount 和 strCount）也会被设置。

最后，传入的字符串对象指针被设置为 NULL（*Pstr = NULL;），以便程序可以重复使用它。

### 5.5.2.5 字符串函数

现在我们将查看两个字符串函数，以了解指针和内存是如何处理的。ajStrMatchS 是一个用于匹配两个 AJAX 字符串的简单函数：

```
/** @func ajStrMatchS ***********************************************************************
**
** Simple test for matching two strings.
```

## 5.5 使用对象进行编程

```
**
** @param [r] str [const AjPStr] String
** @param [r] str2 [const AjPStr] Second String
** @return [AjBool] ajTrue if two complete strings are the same
** @@
**********************************************************************************/
AjBool ajStrMatchS(const AjPStr str, const AjPStr str2)
{
    if(!str || !str2)
        return ajFalse;

    if(!strcmp(str->Ptr, str2->Ptr))
        return ajTrue;

    return ajFalse;
}
```

它接收两个 AJAX 字符串对象，并使用 C 函数 strcmp 比较对象中的 C 类型字符串，如果相同则返回 ajTrue，否则返回 ajFalse。该函数仅读取传入字符串的值，因此永远不需要分配内存。

ajStrAssignS 不同。该函数将一个字符串的值赋给另一个字符串。字符串被复制，而不仅仅是将引用（指针）设置到原始字符串：

```
/* @func ajStrAssignS **********************************************************
**
** Copy a string to a string.
**
** This is a genuine copy (reference count isn't used). Useful where both
** strings will be separately overwritten later so that they can both remain
** modifiable.
**
** @param [w] Pstr [AjPStr*] Target string.
** @param [rN] str [const AjPStr] Source string.
** @return [AjBool] ajTrue if string was reallocated
** @@
******************************************************************************/
AjBool ajStrAssignS(AjPStr* Pstr, const AjPStr str)
{
    AjBool ret = ajFalse;
    AjPStr thys;

    if(!str)
    {
        return ajStrAssignC(Pstr, "");
    }

    ret = ajStrSetRes(Pstr, str->Len+1); /* minimum reserved size, OR more */
    thys = *Pstr;

    thys->Len = str->Len;
    memmove(thys->Ptr, str->Ptr, str->Len+1);

    return ret;
}
```

该函数接受要复制的源字符串（str）和目标字符串（Pstr）。目标字符串（Pstr）将被修改，因此必须传递其地址（AjPStr* Pstr）。

你可以看到，如果为源字符串传递 NULL 指针，则通过调用 ajStrAssignC 将空字符串写入目标字符串。这是之前提到的故障安全机制。该函数还应作为安全措施检查是否为目标字符串的地址传递了 NULL，但目前它不这样做。

调用 ajStrSetRes（见下文）以确保目标字符串是一个新字符串，未被其他字符串对象引用，并且足够大以满足其预期用途。目标字符串的长度（thys->Len）被设置，源字符串中的 C 类型字符串（str->Ptr）被复制（使用 memmove）到目标字符串（thys->Ptr）。如果字符串被重新分配则返回 ajTrue，否则返回 ajFalse。

ajStrSetRes 确保字符串足够大以满足其预期用途：

```
/* @func ajStrSetRes ***********************************************************
**
** Ensures a string is modifiable and big enough for its intended purpose.
**
** The target string is guaranteed to have a reference count of 1 and a
** minimum reserved size.
**
** @param [u] Pstr [AjPStr*] String
** @param [r] size [ajuint] Minimum reserved size.
** @return [AjBool] ajTrue if the string was reallocated
** @@
******************************************************************************/

AjBool ajStrSetRes(AjPStr* Pstr, ajuint size)
{
    AjPStr thys;
    ajuint savesize;

    savesize = size; /* often part of *Pstr, about to vanish */

    if(!*Pstr)
    {
        *Pstr = ajStrNewRes(savesize);
        return ajTrue;
    }

    thys = *Pstr;

    if((thys->Use > 1) || (thys->Res < savesize))
    {
        strCloneL(Pstr, savesize);
        return ajTrue;
    }

    return ajFalse;
}
```

它接受目标字符串的地址和一个最小大小（size）。如果目标字符串为 NULL，则使用 ajStrNewRes 分配一个带有保留大小的字符串。该函数已有解释。否则，如果使用计数大于 1 或当前保留大小



少于请求的大小，将调用静态函数 strCloneL（见下文）来复制字符串，但使用计数为 1 且最小保留大小。如果字符串被重新分配，则返回 ajTrue，否则返回 ajFalse。

strCloneL 获取目标字符串（Pstr）的地址和一个保留大小（size）：

```
/* @func static strCloneL *********************************************************
**
** Makes a new clone of a string with a usage count of one and a minimum
** reserved size.
**
**
** @param [w] Pstr [AjPStr*] String
** @param [r] size [ajuint] Minimum reserved size.
** @return [void]
**
** @@
******************************************************************************/

static void strCloneL(AjPStr* Pstr, ajuint size)
{
    AjPStr thys;
    AjPStr ret;

    thys = *Pstr;
    ret = ajStrNewResLenC(thys->Ptr, size, thys->Len);
    ajStrDel(Pstr);
    *Pstr = ret;

    return;
}
```

它调用 ajStrNewResLenC 来分配带有保留大小的字符串，如前面已解释。传递的原始目标字符串通过调用析构函数 ajStrDel 来删除。

应该指出，字符串是一种特殊情况，而大多数其他对象的内存管理内部机制要简单得多。只有字符串，因为被其他库广泛使用，才出于安全和效率的原因需要特殊处理。

## 5.5.3 AJAX 动态数组对象

内存管理宏通过 ajarr.c 中的数组处理函数得到很好的说明。这里我们将考虑 AjPInt 和 AjPInt2d 对象的构造函数和析构函数。这些是整数的动态一维（1D）（AjPInt）和二维（2D）（AjPInt2d）数组。

### 5.5.3.1 对象定义

以下是对象定义：

```
typedef struct AjSInt
{
    ajuint Res;
    ajuint Len;
    ajint *Ptr;
} AjOInt;
```

```
#define AjPInt AjOInt*

typedef struct AjSInt2d
{
    ajuint Res;
    ajuint Len;
    AjPInt *Ptr;
} AjOInt2d;
#define AjPInt2d AjOInt2d*
```

两个对象都包含用于数组当前长度（Len）和保留大小（Res）的变量。AjPInt 包含指向 ajint 的指针（Ptr），在分配时，它将指向一个 ajint 值数组。相比之下，AjPInt2d 包含指向 AjPInt 的指针（Ptr），它最终将指向一个 AjPInt 对象指针数组。

### 5.5.3.2 AjPInt 构造和析构

ajIntNewRes 是 AjPInt 对象的构造函数，用于分配带有初始保留大小的数组。代码如下所示：

```
/* @func ajIntNewRes ***********************************************************
**
** Constructor given an initial reserved size.
**
** @param [r] size [ajuint] Reserved size
** @return [AjPInt] Pointer to an empty integer array struct of specified size.
** @category new [AjPInt] Constructor with reserved size
** @@
*******************************************************************************/
AjPInt ajIntNewRes(ajuint size)
{
    AjPInt thys;
    size = ajRound(size, RESERVED_SIZE);
    AJNEW0(thys);
    thys->Ptr = AJALLOC0(size*sizeof(ajint));
    thys->Len = 0;
    thys->Res = size;
    arrTotal++;
    arrAlloc += size*sizeof(ajint);
    ajDebug("ajIntNewRes size %d*%d %d\n",
            size, sizeof(ajint), size*sizeof(ajint));
    return thys;
}
```

AJNEW0 用于为单个 AjPInt 对象分配内存。AJALLOC0 被调用以创建大小为 size 的 AJAX 整数（ajint）数组。arrTotal 和 arrAlloc 也被设置，它们是用于调试数组的全局变量。ajIntDel 是 AjPInt 的析构函数：

```
/* @func ajIntDel ***********************************************************************
**
** Default destructor for AJAX integer arrays.
**
** If the given array is a NULL pointer, simply returns.
**
** @param [d] thys [AjPInt*] Pointer to the ajint array to be deleted.
**             The pointer is always deleted.
** @return [void]
** @category delete [AjPInt] Default destructor
** @@
**********************************************************************************/

void ajIntDel(AjPInt *thys)
{
    if(!thys || !*thys)
        return;

    ajDebug("ajIntDel Len %u Res %u\n",
            (*thys)->Len, (*thys)->Res);

    AJFREE((*thys)->Ptr);
    AJFREE(*thys);

    *thys = NULL;

    arrFreeCount++;

    return;
}
```

AJFREE 被调用两次。第一次调用（`AJFREE((*thys)->Ptr);`）释放整数数组。第二次调用（`AJFREE(*thys);`）释放对象本身。可以看到，传递给函数的指针（`thys`）使用代码 `*thys = NULL;` 设置为 NULL。

### 5.5.3.3 AjPInt2d 构造和析构

ajInt2dNewRes 是 AjPInt2d 对象的构造函数，用于为第一维分配带有初始保留大小的 2D 数组。代码如下所示：

```
/* @func ajInt2dNewRes *************************************************************
**
** Constructor given an initial reserved size.
**
** @param [r] size [ajuint] Reserved size 1st dim
** @return [AjPInt2d] Pointer to an empty integer 2d array struct of
**                  specified size.
** @category new [AjPInt2d] Constructor with reserved size
** @@
************************************************************************************/

AjPInt2d ajInt2dNewRes(ajuint size)
{
    AjPInt2d thys;
    ajuint i;

    size = ajRound(size, RESERVED_SIZE);

    AJNEW0(thys);
    thys->Ptr = AJALLOC0(size*sizeof(AjPInt));
    thys->Len = 0;
    thys->Res = size;

    for(i=0;i<size;++i)
        thys->Ptr[i] = NULL;

    arr2dAlloc++;

    return thys;
}
```

AJNEW0 再次被调用以创建基本对象，在此例中为 AjPInt2d 的实例。AJALLOC0 被调用以创建大小为 size 的指向 1D 整数数组对象（AjPInt）的指针数组。可以从代码中推断，数组的第二维（整数数组本身）在需要之前不会被创建。这是出于效率的考虑。

ajInt2dDel 是 AjPInt2d 的析构函数：

```
/* @func ajInt2dDel **********************************************************
**
** Default destructor for AJAX integer arrays.
**
** If the given array is a NULL pointer, simply returns.
**
** @param [d] thys [AjPInt2d*] Pointer to the ajint array to be deleted.
** The pointer is always deleted.
** @return [void]
** @category delete [AjPInt2d] Default destructor
** @@
******************************************************************************/

void ajInt2dDel(AjPInt2d *thys)
{
    ajint i;

    if(!thys || !*thys)
        return;

    ajDebug("ajInt2dDel Len %u Res %u\n",
            (*thys)->Len, (*thys)->Res);

    for(i=(*thys)->Res-1;i>-1;--i)
        if((*thys)->Ptr[i])
            ajIntDel(&((*thys)->Ptr[i]));

    AJFREE((*thys)->Ptr);
    AJFREE(*thys);

    *thys = NULL;

    arr2dFreeCount++;

    return;
}
```

该函数获取要释放的 AjPInt2d 对象（thys）的地址。要访问对象本身，必须解引用 thys，即在函数体中看到 *thys 的每个地方。你会回想，Ptr 引用一个 AjPInt 对象指针数组，每个指针都指向一个整数数组。

整数数组通过在循环中调用析构函数 ajIntDel 来释放。该析构函数获取一个 AjPInt 的地址。首先解引用 thys 后，使用数组表示法来索引 AjPInt 数组的第 i 个元素 ((*thys) ->Ptr[i])。这将检索一个单独的 AjPInt 对象，析构函数需要其地址，这就是为什么你有 ajIntDel(&((*thys) ->Ptr[i])) ;。

然后 AJFREE 被调用两次。第一次调用（AJFREE ( (*thys) ->Ptr) ;）释放 AjPInt 数组。第二次调用（AJFREE (*thys) ;）释放 AjPInt2d 对象本身。可以看到，传递给函数的指针（thys）使用代码 *thys = NULL; 设置为 NULL。

### 5.5.3.4 AjPInt2d 放置和获取数组元素

函数 ajInt2dGet 用于从 2D 整数数组中检索一个值。源代码如下：

```
/* @func ajInt2dGet *************************************************************
**
** Retrieve an element from an AJAX 2d integer array.
**
** If the given array is a NULL pointer, simply returns.
**
** @param [r] thys [const AjPInt2d] Pointer to the ajint array.
** @param [r] elem1 [ajuint] array element.
** @param [r] elem2 [ajuint] array element.
**
** @return [ajint] contents of array element
** @category cast [AjPInt2d] Retrieve an integer from an array
**
** @@
*******************************************************************************/

ajint ajInt2dGet(const AjPInt2d thys, ajuint elem1, ajuint elem2)
{
    AjPInt t;

    if(!thys || elem1>=thys->Len)
        ajErr("Attempt to access bad ajint array index [%d][%d]\n",elem1,
              elem2);

    t = thys->Ptr[elem1];
    if(!t)
        ajErr("Attempt to access bad 1st dimension [%d]\n",elem1);

    return ajIntGet(t,elem2);
}
```

将从数组 thys 中检索列 elem1 和行 elem2 的元素。如果尝试检查未分配的元素，将引发错误。否则，将返回元素的值。





# 5 C 语言编程

The function ajInt2dPut is used to load a 2D integer array element with a value. If the array is of insufficient size then the memory is extended as required. The source code is below:

函数 ajInt2dPut 用于将值加载到二维整数数组元素中。如果数组大小不足，则根据需要扩展内存。源代码如下：

```
/* *func:ajInt2dPut *****************************************************************
**
** Load an integer 2d array element.
**
** If the given array is a NULL pointer an error is generated.
** If the array is of insufficient size then the array is extended.
** Negative indices generate an error.
**
** @param [w] thys [AjPInt2d*] Pointer to the ajint array.
** @param [r] elem1 [ajuint] array element.
** @param [r] elem2 [ajuint] array element.
** @param [r] v [ajint] value to load.
**
** @return [AjBool] true if any array was extended.
** @category modify [AjPInt2d] Load an integer array element
** @@
********************************************************************************/

AjBool ajInt2dPut(AjPInt2d *thys, ajuint elem1, ajuint elem2, ajint v)
{
    if(!thys || !*thys)
        ajErr("Attempt to write to illegal array value [%d] [%d]\n",elem1,
              elem2);
    if(elem1 < (*thys)->Res)
    {
        ajDebug("ajInt2dPut [%u] [%u] %d ([%u] %x)\n",
                elem1, elem2, v, (*thys)->Len, (*thys)->Ptr[elem1]);
        if(elem1>=(*thys)->Len)
            (*thys)->Len = elem1+1;
        if(!(*thys)->Ptr[elem1])
            (*thys)->Ptr[elem1] = ajIntNew();
        return ajIntPut(&(*thys)->Ptr[elem1],elem2,v);
    }
    arrInt2dResize(thys, elem1);
    if(!(*thys)->Ptr[elem1])
        (*thys)->Ptr[elem1] = ajIntNew();
    ajIntPut(&(*thys)->Ptr[elem1],elem2,v);
    return ajTrue;
}
```

There is nothing new here that you haven't seen already. Work through it to test your understanding of pointers, particularly how pointer and array notation may be mixed.

这里没有你之前没见过的新内容。请通读以测试你对指针的理解，特别是指针和数组表示法如何混合使用。

## 6.1 演示应用程序

EMBOSS includes, for certain AJAX and NUCLEUS library files, applications which illustrate the correct usage of each function in that library. Currently these ‘demonstration applications’ are kept in the myembossdemo EMBASSY package and have the prefix ‘demo’. There is, of course, an ACD file for each application. For example the following files illustrate the use of the string library:

EMBOSS 为某些 AJAX 和 NUCLEUS 库文件包含演示应用程序，用于说明该库中每个函数的正确用法。目前，这些“演示应用程序”保存在 myembossdemo EMBASSY 包中，并带有前缀“demo”。当然，每个应用程序都有一个 ACD 文件。例如，以下文件说明了字符串库的使用：

```
/home/auser/emboss/emboss/embassy/myembossdemo/src/demostring.c
/home/auser/emboss/emboss/embassy/myembossdemo/emboss_acd/demostring.acd
```

> **注意**
>
> 演示应用程序仍在开发中，仅适用于少数库文件，可用函数的覆盖范围在所有情况下绝非全面。文件 demostring.c 最为完整，并展示了即将推出的内容的大致情况。

### 6.1.1 编译演示应用程序

If you open the two Makefile.am files (in the src and acd directories) and find the entries for demostring you’ll notice it occurs in the check_PROGRAMS section of the ‘src’ Makefile.am file. This section is reserved for programs that are included for testing, are undergoing active development or have yet to be fully tested, or which should be considered incomplete for some other reason, e.g. they are undocumented or quality assurance test data are not yet available for them. The demo* applications are there, reflecting their ‘demonstration’ status.

如果你打开两个 Makefile.am 文件（位于 src 和 acd 目录中）并找到 demostring 的条目，你会发现它出现在‘src’ Makefile.am 文件的 check_PROGRAMS 部分中。此部分保留用于用于测试的程序、正在积极开发或尚未完全测试的程序，或出于其他原因应被视为不完整的程序，例如，它们未记录文档或质量保证测试数据尚未可用。demo* 应用程序位于此处，反映了它们的“演示”状态。

To compile the “check_PROGRAMS” applications, type:

要编译“check_PROGRAMS”应用程序，请键入：

```
make check
```

from the applications directory. This will produce all the “check_PROGRAMS” applications, including the demonstration applications.

从应用程序目录中。这将生成所有“check_PROGRAMS”应用程序，包括演示应用程序。

You should now have a working demostring application. The source code and ACD file should contain sufficient comments to be comprehensible. To get a feel for the scope of the string library run demostring and inspect the output and the corresponding source code for each function call in turn. If it’s not obvious what each function is doing, or to test your understanding, edit the source code, recompile and run demostring again.

现在你应该有一个可用的 demostring 应用程序。源代码和 ACD 文件应包含足够的注释以便理解。要了解字符串库的范围，请运行 demostring 并依次检查每个函数调用的输出和相应的源代码。如果不清楚每个函数的作用，或要测试你的理解，请编辑源代码，重新编译并再次运行 demostring。

## 6.2 编程指南

Programming guides are available for most files in AJAX. These summarise the available C data structures and functions and methods for their use. For some files a programming guide is ‘Not available’, others say ‘See’ a guide only, without any deep coverage. In most cases, you are unlikely to need such files and should see the online library documentation for a description of the datatypes and functions included.

大多数 AJAX 文件都有编程指南。这些指南总结了可用的 C 数据结构和函数以及使用方法。对于某些文件，编程指南为“不可用”，其他文件仅说“参见”某个指南，没有深入覆盖。在大多数情况下，你不太可能需要此类文件，而应查看在线库文档以了解包含的数据类型和函数的描述。

| AJAX 库文件 | 编程指南 |
|---|---|
| acd/ajacd.c/h | 处理 ACD 文件 |
| core/ajalign.c/c | 处理比对 |
| core/ajalign.h/c | 处理比对 |
| core/ajarch.h | C 基本数据类型 |
| core/ajarr.c/h | 处理数组。另参见处理简单 |
| core/ajassert.h/c | 不可用 |
| core/ajax.h | C 基本数据类型，你的第一个 EMBOSS 应用程序 |
| core/ajbase.h/c | 处理序列 |
| core/ajcall.h/c | 参见处理图形 |
| core/ajcod.h/c | 处理密码子 |
| core/ajdan.h/c | 处理序列 |
| core/ajdmx.h/c | 不可用 |
| core/ajdefine.h | C 基本数据类型 |
| core/ajdomain.h/c | 不可用 |
| core/ajdom.h/c | 参见处理图形 |
| core/ajexcept.h/c | 处理异常 |
| core/ajfeat.h/c | 处理特征 |
| core/ajfeatdata.h | 处理特征 |
| core/ajfile.h/c | 处理文件 |
| core/ajfiledata.h/c | 不可用 |
| core/ajfileio.h/c | 不可用 |
| core/ajfmt.h/c | 处理字符串 |
| graphics/ajgraph.h/c | 处理图形 |
| graphics/ajgraphstruct.h | 处理图形 |
| graphics/ajgraphxml.h/c | 参见处理图形 |
| graphics/ajhist.h/c | 处理图形 |
| core/ajindex.h/c | 不可用 |
| core/ajjava.h/c | 不可用 |
| core/ajlist.h/c | 处理列表 |
| core/ajmath.h/c | 处理数学 |
| core/ajmatrices.h/c | 处理矩阵 |
| core/ajmem.h/c | 对象（C 数据结构） |
| core/ajmess.h/c | 处理异常 |
| core/ajnam.h/c | 不可用 |
| core/ajnexus.h/c | 参见处理 Phylip |
| core/ajpat.h/c | 处理模式。另参见处理简单 |
| core/ajpdb.h/c | 不可用 |
| core/ajpdbio.h/c | 不可用 |
| core/ajphylo.h/c | 处理 Phylip |
| core/ajrange.h/c | 处理简单 |
| core/ajreg.h/c | 处理模式。另参见处理简单 |
| core/ajreport.h/c | 处理报告 |
| core/ajseqabi.h/c | 参见处理序列 |
| core/ajseq.h/c | 处理序列 |
| core/ajseqdata.h | 处理序列 |
| ajaxdb/ajseqdb.h/c | 参见处理序列 |
| core/ajseqread.h/c | 处理序列 |
| core/ajseqtype.h/c | 处理序列 |
| core/ajseqwrite.h/c | 处理序列 |
| core/ajsort.h/c | 处理数组 |
| core/ajsql.h/c | 不可用 |
| core/ajstr.h/c | 处理字符串。另参见处理简单 |
| core/ajsys.h/c | 处理系统代码 |
| core/ajtable.h/c | 处理表格 |
| core/ajtime.h/c | 不可用 |
| core/ajtranslate.h/c | 处理序列 |
| core/ajtree.h/c | 不可用 |
| core/ajutil.h/c | 处理系统代码 |
| core/ajvector.h/c | 参见处理数学 |

| 文件 | 参考 |
|---|---|
| pcre/pcre.c | 参见处理模式 |
| pcre/pcre_chartables.c | 参见处理模式 |
| pcre/pcre_config.h | 参见处理模式 |
| pcre/pcre_get.c | 参见处理模式 |
| pcre/pcre.h | 参见处理模式 |
| pcre/pcre_internal.h | 参见处理模式 |
| pcre/pcreposix.c | 参见处理模式 |
| pcre/pcreposix.h | 参见处理模式 |
| pcre/pcre_printint.c | 参见处理模式 |
| pcre/pcre_study.c | 参见处理模式 |

> **注释**
>
> 目前 NUCLEUS 库没有编程指南。在某些情况下，你可能期望在 NUCLEUS 中找到的算法和数据结构实际上保存在 AJAX 中。这通常出于编译目的所必需。例如，在 ACD 文件处理期间调用的任何函数（由 AJAX 的一部分处理）也必须位于 AJAX 中。

## 6.3 处理 ACD 文件

### 6.3.1 简介

Basic housekeeping code is required by all EMBOSS and EMBASSY applications. This includes code to process the command line and application ACD file, handle user inputs, retrieve AJAX objects corresponding to data definitions in the ACD file, and to exit cleanly.

所有 EMBOSS 和 EMBASSY 应用程序都需要基本的管家代码。这包括处理命令行和应用程序 ACD 文件、处理用户输入、检索与 ACD 文件中的数据定义对应的 AJAX 对象以及干净退出的代码。

### 6.3.2 程序初始化

Every application must process the ACD file and user input. It must:

每个应用程序都必须处理 ACD 文件和用户输入。它必须：

- 读取本地数据库定义
- 找到要使用的正确 ACD 文件并解析它
- 解析命令行
- 提示用户输入命令行中未指定的所需值
- 验证用户输入并针对任何错误值重新提示
- 为每个 ACD 数据定义分配 AJAX 对象的内存
- 打开输入和输出文件
- 读取输入文件（从任何输入序列流中读取的第一个序列）
- 初始化 AJAX 对象（从读取输入文件）



对上述所有内容只需进行一次调用。

For EMBOSS applications:

```
embInit("ApplicationName", argc, argv);
```

For EMBASSY applications:

```
embInitP("ApplicationName", argc, argv, "PackageName");
```

所有应用程序必须在启动时立即调用上述函数之一。ApplicationName 是要解析的 ACD 文件的名称（ApplicationName.acd）。PackageName 是 EMBASSY 包的名称，例如 "myemboss"。需要命令行，因此从 main 传递 argc 和 argv。这些函数返回后，将不再与用户进行交互。在应用程序正式开始之前，所有输入都会被读取并保存在内存中。为每个 ACD 数据定义分配一个 AJAX 对象。

For a simple program with no ACD data definitions, the first few lines of the program would look like this:

```
int main(int argc, char **argv)
{
    embInit("helloworld", argc, argv);
```

### 6.3.3 检索 ACD 值

The ajAcdGet* family of functions return AJAX objects for data definitions in the application ACD file. They are defined in ajacd.h/c and have the general name:

```
ajAcdGetDatatype
```

where Datatype 是受支持的 ACD 数据类型之一（第 A.2 节，‘数据类型’）。为每个 ACD 数据类型提供一个 ajAcdGet 前缀函数。它们本身并非构造函数，而是返回指向由 embInit 或 embInitP 调用分配的适当 AJAX 对象的指针。例如，在检索 ACD 字符串时，ajAcdGetString 返回指向由 embInit 创建的字符串（AjPStr 对象）的指针。数据定义中的属性和命令行收集的用户输入用于初始化对象。任何新对象的内存必须在 main() 中稍后释放。

| ACD 数据类型 | AJAX 数据类型（返回值） | AJAX 函数 |
| --- | --- | --- |
| align | AjPAlign | ajAcdGetAlign |
| array | AjPFloat | ajAcdGetArray |
| boolean | AjBool | ajAcdGetBoolean |
| codon | AjPCod | ajAcdGetCodon |
| cpdb | AjPFile | ajAcdGetCpdb |
| datafile | AjPFile | ajAcdGetDatafile |
| directory | AjPDir | ajAcdGetDirectory |
| | AjPStr | ajAcdGetDirectoryName |
| dirlist | AjPList | ajAcdGetDirlist |
| discretestates | AjPPhyloState* | ajAcdGetDiscretestates |
| | AjPPhyloState | ajAcdGetDiscretestatesSingle |
| distances | AjPPhyloDist* | ajAcdGetDistances |
| | AjPPhyloDist | ajAcdGetDistancesSingle |
| featout | AjPFeattabOut | ajAcdGetFeatout |
| features | AjPFeattable | ajAcdGetFeatures |
| filelist | AjPList | ajAcdGetFilelist |
| float | float | ajAcdGetFloat |
| | double | ajAcdGetFloatDouble |
| frequencies | AjPPhyloFreq | ajAcdGetFrequencies |
| graph | AjPGraph | ajAcdGetGraph |
| graphxy | AjPGraph | ajAcdGetGraphxy |
| infile | AjPFile | ajAcdGetInfile |
| int | ajint | ajAcdGetInt |
| | ajlong | ajAcdGetIntLong |
| list | AjPStr* | ajAcdGetList |
| | AjPStr | ajAcdGetListSingle |
| matrix | AjPMatrix | ajAcdGetMatrix |
| matrixf | AjPMatrixf | ajAcdGetMatrixf |
| outcodon | AjPOutfile | ajAcdGetOutcodon |
| outcpdb | AjPOutfile | ajAcdGetOutcpdb |
| outdata | AjPOutfile | ajAcdGetOutdata |
| outdir | AjPDirout | ajAcdGetOutdir |
| | AjPStr | ajAcdGetOutdirName |
| outdiscrete | AjPOutfile | ajAcdGetOutdiscrete |
| outdistance | AjPOutfile | ajAcdGetOutdistance |
| outfile | AjPFile | ajAcdGetOutfile |
| outfileall | AjPFile | ajAcdGetOutfileall |
| outfreq | AjPOutfile | ajAcdGetOutfreq |
| outmatrix | AjPOutfile | ajAcdGetOutmatrix |
| outmatrixf | AjPOutfile | ajAcdGetOutmatrixf |
| outproperties | AjPOutfile | ajAcdGetOutproperties |
| outscop | AjPOutfile | ajAcdGetOutscop |
| outtree | AjPOutfile | ajAcdGetOuttree |
| pattern | AjPPatlistSeq | ajAcdGetPattern |
| properties | AjPPhyloProp | ajAcdGetProperties |
| range | AjPRange | ajAcdGetRange |
| regexp | AjPPatlistRegex | ajAcdGetRegexp |
| | AjPRegexp | ajAcdGetRegexpSingle |
| report | AjPReport | ajAcdGetReport |
| scop | AjPFile | ajAcdGetScop |
| select | AjPStr* | ajAcdGetSelect |
| | AjPStr | ajAcdGetSelectSingle |
| seq | AjPSeq | ajAcdGetSeq |
| seqall | AjPSeqall | ajAcdGetSeqall |
| seqout | AjPSeqout | ajAcdGetSeqout |
| seqoutall | AjPSeqout | ajAcdGetSeqoutall |
| seqoutset | AjPSeqout | ajAcdGetSeqoutset |
| seqset | AjPSeqset | ajAcdGetSeqset |
| seqsetall | AjPSeqset* | ajAcdGetSeqsetall |
| | AjPSeqset | ajAcdGetSeqsetallSingle |
| string | AjPStr | ajAcdGetString |
| toggle | AjBool | ajAcdGetToggle |
| tree | AjPPhyloTree* | ajAcdGetTree |
| | AjPPhyloTree | ajAcdGetTreeSingle |

建议处理 ACD 数据类型的变量应与相关参数或限定符同名，即 ACD 数据定义中给出的名称。这并非严格要求，但能使代码更易于理解。出于同样的原因，所有对 ajAcdGet* 函数的调用都应放在一个代码块中，以便阅读。

### 示例

Consider the following ACD file:

```
application: example
{
  documentation: "Example application."
}
```

```
string: astring
{
    default: "String to be printed to screen."
}
```

这里是将 astring 打印到屏幕上的 C 源代码：

```
int main(int argc, char **argv)
{
    AjPStr astring = NULL;
    embInit("example", argc, argv);
    astring = ajAcdGetString("astring");
    ajFmtPrint("%S\n", astring);
    ajStrDel(&astring);
    embExit();
    return 0;
}
```

该代码声明一个 AJAX 字符串对象（AjPStr）并调用 embInit 来调用 ACD 文件处理。embInit 为字符串对象分配内存，因此上述代码没有显式调用字符串构造函数。尽管如此，embInit 创建了一个字符串对象，在使用完毕后应将其释放。这就是调用 ajStrDel 的原因。

### 6.3.4 替代 ACD 检索函数

There are several alternative ACD retrieval functions. In all cases token is the name of the ACD data definition (the name of the parameter or qualifier):

| 类型 | 函数 |
| :--- | :--- |
| AjPStr | ajAcdGetDirectoryName (const char *token); |
| AjPPhyloState | ajAcdGetDiscretestatesSingle (const char *token); |
| AjPStr | ajAcdGetListSingle(const char *token); |
| AjPStr | ajAcdGetOutdirName (const char *token); |
| AjPRegexp | ajAcdGetRegexpSingle (const char *token); |
| AjPStr | ajAcdGetSelectSingle (const char *token); |
| AjPSeqset | ajAcdGetSeqsetallSingle (const char *token); |
| AjPPhyloTree | ajAcdGetTreeSingle (const char *token); |

与标准检索函数不同，这些函数返回从 ACD 数据类型派生的值，例如一组序列中的第一个序列或目录的名称。例如，ajAcdGetOutdirName 返回保存输出目录名称的 AjPStr，而标准检索函数 ajAcdGetOutdir 返回 AjPDir，即目录本身。它们的用法在相应的编程指南中说明。

当不需要完整对象时，提供这些替代函数以方便使用。ACD 会处理未传递给主程序的任何对象的内存管理。带有后缀 Single 的替代函数返回标准检索函数通常会返回的对象的一个元素。这使得调用程序无需遍历值列表，因为只能从列表中选择一个值（即 ACD 文件定义要返回的最小值和最大值均为一个值）。您只需释放返回的单个字符串。同样，带有后缀 Name 的替代函数返回一个全新的字符串。您只需稍后释放此字符串，ACD 会在程序退出时处理释放完整对象。

Consider the following ACD file:

```
application: example
{
  documentation: "Example application."
}
directory: dir
{
  help: "Directory for reading."
}
```

以下程序将打印目录名称：

```
int main(int argc, char **argv)
{
  embInit("example", argc, argv);
  AjPStr name = NULL;
  name = ajAcdGetOutdirName("dir");
  ajFmtPrint("Directory name is %S\n", name);
  ajStrDel(&name);
  embExit();
  return 0;
}
```

### 6.3.5 干净退出

您的应用程序必须干净退出。换句话说，所有已分配的内存都必须释放，并向操作系统返回适当的代码。

内存管理在其他地方有详细介绍（第 5.5 节，‘使用对象进行编程’）。简而言之，内存由以下方式分配：

- embInit 或 embInitP 为每个 ACD 数据定义分配 AJAX 对象的内存，该对象的指针由 ajAcdGet* 函数返回
- embInit 或 embInitP 还为内部维护目的分配一些内存
- 显式调用内存分配宏
- 显式调用构造函数
- 隐式调用构造函数，某些函数会作为故障保护机制进行此类调用，当需要对象但传递了未分配的对象指针时。

所有分配宏都必须与相应的释放宏匹配。所有构造函数调用（无论是显式还是隐式，包括对 ajAcdGet* 函数的调用）都必须与相应的析构函数匹配。要释放 EMBOSS 为内部维护分配的内存，必须调用以下函数之一：



void embExit (void);
void embExitBad (void);

这些函数定义在 embExit.h/c 中。embExit 返回成功代码 (0)，而 embExitBad 返回失败代码 (0)。
因此，大多数 EMBOSS 应用程序的最后两行是：

embExit();
return 0;

## 6.4 处理简单 ACD 数据类型

### 6.4.1 简介

本节介绍“简单”ACD 数据类型（第 A.2.1 节，“简单 ACD 数据类型描述”）的 ACD 文件处理：

- 整数 (integer)
- 浮点数 (float)
- 布尔值 (boolean)
- 切换 (toggle)
- 字符串 (string)
- 数组 (array)
- 范围 (range)

通过调用 ajAcdGet* 函数来检索值，这些函数返回相应类型的 AJAX 数据类型：对于 integer、float、boolean 和 toggle 返回基本类型，对于其他类型返回 EMBOSS 对象。处理范围的函数包括：

- 获取和设置范围对象的元素
- 查询范围对象的属性
- 根据范围对象中的规范处理字符串 (AjPStr) 和序列 (AjPSeq)

有关正则表达式（regexp ACD 数据类型）和序列模式（pattern ACD 数据类型），请参见第 6.6 节，“处理序列模式”。数组处理（第 6.17 节，“处理数组”）和字符串处理（第 6.5 节，“处理字符串”）在其他地方有详细描述。

### 6.4.2 AJAX 库文件

下表列出了用于处理简单 ACD 数据类型的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajrange | AJAX 范围表达式的处理 |
| ajstr | 字符串处理 |
| ajarr | 数组处理 |

ajrange.h/c. 定义范围规范对象 (AjPRange) 并包含处理范围规范的函数（参见第 A.2.1.5 节，“range”）。

ajstr.h/c. 定义用于处理来自 ACD 文件的字符串的字符串对象 (AjPStr)。它们包含您进行一般字符串处理所需的大部分函数（第 6.5 节，“处理字符串”）。

ajarr.h/c. 包含您进行一般数组处理所需的大部分函数（第 6.17 节，“处理数组”）。它们定义了用于处理来自 ACD 文件的数组的 AjPFloat 对象。它们包含用于低级处理数组的静态数据结构和函数。

### 6.4.3 ACD 数据类型

简单 ACD 数据类型用于应用程序输入：

- integer 简单整数
- float 简单浮点数
- boolean 简单布尔值
- toggle 简单布尔值
- string 简单字符串
- array 整数或浮点数列表
- range 序列位置范围

### 6.4.4 ACD 数据定义

典型的 ACD 定义如下所示。

##### 6.4.4.1 integer

用于整数输入：

integer: wordsize
[
   default: "4"
   minimum: "2"
   maximum: "20"
   information: "Word size"
]

##### 6.4.4.2 float

用于浮点数输入：

float: minscore
[
    default: "0.0"
    minimum: "0.0"
    information: "Minimum score of feature to display"
]

##### 6.4.4.3 boolean

用于布尔输入：

boolean: feature
[
    default: "N"
    information: "Use feature information"
]

##### 6.4.4.4 toggle

用于切换输入：

toggle: tolower
[
    default: "N"
    information: "Change masked region to lower case"
]

##### 6.4.4.5 string

用于字符串输入：

string: delimiter
[
    default: "|"
    information: "Delimiter of records in text output file"
    knowntype: "output delimiter"
]

##### 6.4.4.6 array

用于数组输入：

array: thresholds
[
    information: "Values to represent 'identical', 'similar' and 'related'"
    default: "-1.5,0.0,1.5"
    minimum: "0.0"
    size: "3"
    sum: "0"
    sumtest: "y"
]

##### 6.4.4.7 range

用于范围输入：

range: regions
[
    information: "Regions to put in uppercase (eg: 4-57,78-94)"
    default: ""
    help: "Regions to put in uppercase. If this is left blank, the sequence case is
left alone. A set of regions is specified by a set of pairs of integer positions
separated by any non-digit, non-alpha character. For example: \
24-45, 56-78 \
1:45, 67=99;765..888 \
1,5,8,10,23,45,57,99"
]

##### 6.4.4.8 参数名称

根据数据定义的特定用例，可能会提供标准参数名称；例如，用于定义间隙罚分的任何浮点输入的间隙罚分。请参见附录 A，ACD 语法参考。

##### 6.4.4.9 常见属性

通常指定的属性摘要如下。除非它们被指示为全局属性（第 A.4 节，“全局属性”），否则它们是特定于数据类型的（第 A.5 节，“特定于数据类型的属性”）。

- **默认：** 全局属性，指定默认值。
- **最小值：** 指定允许的最小值。
- **最大值：** 指定允许的最大值。
- **信息：** 全局属性，指定用户提示，也用于应用程序文档。
- **已知类型：** 此全局属性应始终为字符串输入指定。如果输出不是任何标准 EMBOSS 已知类型，则推荐使用 ApplicationName 输出。
- **大小：** 指定数组数据定义中允许的元素数量。
- **总和：** 指定数组数据定义中所有值的总和，除非 sumtest 属性为 false，否则会对其进行测试。
- **求和测试：** 布尔属性，如果设置为 false，则关闭对数组数据定义的 sum: 属性的测试。

### 6.4.5 AJAX 数据类型

用于处理 ACD 文件中定义的简单 ACD 数据类型，请使用：

- ajint 简单整数（用于 integer ACD 数据类型）。
- float 简单浮点数（用于 float ACD 数据类型）。
- AjBool 简单布尔值（用于 boolean 和 toggle ACD 数据类型）。
- AjPStr 字符串（用于 string ACD 数据类型）。
- AjPFloat 浮点数数组（用于 array ACD 数据类型）。
- AjPRange AJAX 序列范围规范（用于 range ACD 数据类型）。请参见第 A.2.1.5 节，“range”。

### 6.4.6 ACD 文件处理

通过 ACD 文件处理简单 ACD 数据类型的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
| --- | --- | --- |
| integer | ajint | ajAcdGetInt |
| float | float | ajAcdGetFloat |
| boolean | AjBool | ajAcdGetBoolean |
| toggle | AjBool | ajAcdGetToggle |
| string | AjPStr | ajAcdGetString |
| array | AjPFloat | ajAcdGetArray |
| range | AjPRange | ajAcdGetRange |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都读入内存。您可以通过 ajAcdGet* 函数系列来控制内存，该系列函数返回指向相应对象的指针。

> **注意**
>
> 您通常不会从 ACD 检索切换项，因为它们仅用于 ACD 文件内，通常用于控制对另一个参数的提示（参见第 4.5 节，“控制提示”）。

#### 6.4.6.1 简单 ACD 数据类型的检索

要从 ACD 文件检索数据，请按需要声明简单变量或对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

###### 6.4.6.1.1 integer

```c
ajint wordsize = 0;
wordsize = ajAcdGetInt("wordsize");
```

###### 6.4.6.1.2 float

```c
float minscore = 0.;
minscore = ajAcdGetFloat("minscore");
```

###### 6.4.6.1.3 boolean

```c
AjBool showall = ajFalse;
showall = ajAcdGetBoolean("showall");
```

###### 6.4.6.1.4 toggle

```c
AjBool tolower = ajFalse;
tolower = ajAcdGetToggle("tolower");
```

###### 6.4.6.1.5 string

```c
AjPStr delimiter = NULL;
delimiter = ajAcdGetString("delimiter");
```

###### 6.4.6.1.6 array

```c
AjPFloat thresholds = NULL;
thresholds = ajAcdGetArray("thresholds");
```

###### 6.4.6.1.7 range

```c
AjPRange regions = NULL;
regions = ajAcdGetRange("regions");
```

#### 6.4.6.2 处理命令行选项和 ACD 属性

##### 6.4.6.2.1 设置范围对象属性

设置范围对象属性的函数如下：

```c
/* Set the start and end values of a range element. */
AjBool ajRangeElementSet (AjPRange this, ajuint element, ajuint start, ajuint end);
/* Sets range values offset relative to a sequence -sbegin value */
AjBool ajRangeSetOffset (AjPRange this, ajuint begin);
```

ajRangeSetOffset 将把范围值设置为相对于指定位置 (begin) 的值，通常是命令行中通过 -sbegin 或序列的 USA 中指定的序列位置范围的起始位置（请参见 EMBOSS 用户指南）。例如，如果 begin 为 11 且范围为 11-12，则新范围将更改为 1-2。

#### 6.4.6.3 内存管理

在程序结束时释放内存是您的责任。您必须对 ajAcdGet* 调用返回的任何 AjPStr、AjPFloat 或 AjPRange 对象调用默认析构函数（见下文）。当然，对于基本数据类型，这不是必需的。

### 6.4.7 对象内存管理

#### 6.4.7.1 默认对象构造

要使用未在 ACD 文件中定义的字符串、数组或范围对象，您必须首先实例化相应的对象指针。默认构造函数如下：

```c
AjPStr ajStrNew (void);             /* String object. */
AjPFloat ajFloatNew (void);         /* Float array */
AjPRange ajRangeNewI (ajuint n);    /* Range object   */
```

ajRangeNewI 接受一个整数 (n)，即对象可以容纳的范围数量。所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的做法：

```c
AjPStr    delimiter = NULL;
AjPFloat  thresholds = NULL;
AjPRange  regions   = NULL;

delimiter = ajStrNew();
```





```c
thresholds = ajFloatNew();
/* Object with a single range */
regions = ajRangeNewI(1);
/* Do something with objects */
ajStrDel(&delimiter);
ajFloatDel(&thresholds);
ajRangeDel(&regions);
```

### 6.4.7.2 默认对象销毁

完成对象使用后，必须释放其占用的内存。析构函数如下：

```c
AjPStr ajStrDel (AjPStr *Pstr); /* String object. */
void ajFloatDel (AjPFloat* Parr); /* Float array */
void ajRangeDel (AjPRange *Prange); /* Range object */
```

使用方法如下：

```c
AjPStr delimiter = NULL;
AjPFloat thresholds = NULL;
AjPRange regions = NULL;
delimiter = ajAcdGetString("delimiter");
thresholds = ajAcdGetArray("thresholds");
regions = ajAcdGetRange("regions");
/* Do something with objects */
ajStrDel(&delimiter);
ajFloatDel(&thresholds);
ajRangeDel(&regions);
```

### 6.4.7.3 替代对象构造和加载

AjPRange 对象有多种替代构造函数：

```c
/* Copy a range object. */
AjPRange ajRangeNewRange (const AjPRange src);
/* Construct from a string. */
AjPRange ajRangeNewString (const AjPStr str);
/* Construct from a string with explicit specification. */
AjPRange ajRangeNewStringLimits (const AjPStr str, ajuint imin, ajuint imax,
ajuint minsize, ajuint size);
/* Construct from a file. */
AjPRange ajRangeNewFilename (const AjPStr name);
```

```c
/* Construct from a file with explicit specification. */
AjPRange ajRangeNewFilenameLimits (const AjPStr name,
                                   ajuint imin, ajuint imax,
                                   ajuint minsize, ajuint size);
```

ajRangeNewStringLimits 和 ajRangeNewFilenameLimits 均用于构造带有指定限制的范围对象：最小值 (imin)、最大值 (imax)、最小范围数量 (minsize) 和所需范围数量 (size)。size 为零表示没有所需数量。

ajRangeNewFilename 和 ajRangeNewFilenameLimits 从“范围文件”（range file）构造对象（参见第 A.2.1.5 节“范围”）。

有关 AjPStr 对象的替代构造函数，请参见第 6.5 节“字符串处理”。

## 6.4.8 获取范围对象元素

以下函数用于从范围对象中检索元素：

```c
/* Get the number of ranges */
ajuint ajRangeGetSize (const AjPRange thys);

/* Get text value of a range */
AjBool ajRangeElementGetText (const AjPRange thys, ajuint element,
                              AjPStr *text);

/* Get start and end values */
AjBool ajRangeElementGetValues (const AjPRange thys, ajuint element,
                                ajuint *start, ajuint *end);
```

ajRangeElementGetText 将从指定的范围元素 (element) 中检索文本。文本定义为一对范围数字之后的任何非数字字符。例如，对于范围对 10-20 potential exon 50-60 repeat，文本值为："potential exon" 和 "repeat"。用于保存文本的字符串对象 (text) 的地址会被传递。

## 6.4.9 查询范围对象属性

用于查询范围对象属性的函数包括：

```c
/* Tests if the set of ranges are in ascending non-overlapping order */
AjBool ajRangeIsOrdered (const AjPRange thys);

/* Tests if any range elements overlap to a region (of a sequence). */
ajuint ajRangeCountOverlaps (const AjPRange thys, ajuint pos, ajuint length);

/* Tests for a single range from the start to end of a sequence. */
AjBool ajRangeIsWhole (const AjPRange thys, const AjPSeq seq);
```

ajRangeCountOverlaps 返回范围对象中与由起始位置 (pos) 和长度 (length) 定义的序列区域重叠的范围数量。

ajRangeIsWhole 用于测试范围对象是否包含从给定序列 (seq) 开始到结束的单个范围。

## 6.4.10 序列操作函数

这些函数根据范围对象中的规范处理序列对象 (AjPSeq)：

```c
/* Remove all subsequences not corresponding to ranges */
AjBool ajRangeSeqExtract(const AjPRange thys, AjPSeq seq);

/* Store retained text as a list of strings. */
AjBool ajRangeSeqExtractList (const AjPRange thys,const AjPSeq seq, AjPList outliststr);

/* Insert spaces into sequence to pad out to the ranges. */
AjBool ajRangeSeqStuff (const AjPRange thys, AjPSeq seq);

/* Mask ranges of positions in a sequence. */
AjBool ajRangeSeqMask (const AjPRange thys, AjPSeq seq, const AjPStr maskchar);

/* Convert the ranges of characters in a sequence to lower-case. */
AjBool ajRangeSeqToLower (const AjPRange thys, AjPSeq seq);
```

ajRangeSeqExtract 保留序列中与范围对应的区域：不在范围内的区域将被删除。由 ajRangeSeqExtract 处理的序列将由原始序列中按范围集合指定的顺序连接的区域组成。如果这些范围不是按升序排列，则生成的序列也不会按位置顺序排列。

ajRangeSeqExtractList 与 ajRangeSeqExtract 相同，区别在于保留的子序列将写入列表。列表的顺序与范围集合中指定的顺序相同。如果这些范围不是按升序排列，则生成的字符串列表也不会按顺序排列。

ajRangeSeqStuff 接受一个字符串和一个有序、非重叠的范围集合，并写出一个用空格填充的字符串，使得不在范围内的所有位置都给出一个空格。例如，对于字符串 "abcde" 和范围 3-5、7-8，生成的字符串将是 " abc de"。

ajRangeSeqMask 将掩码序列中的范围位置，将范围内的所有字符替换为掩码字符 (maskchar)。

## 6.4.11 字符串操作函数

为字符串提供了一组等效于序列操作函数的函数：

```c
AjBool ajRangeStrExtract (const AjPRange thys, const AjPStr instr,
AjPStr *outstr);
AjBool ajRangeStrExtractList (const AjPRange thys, const AjPStr instr, AjPList outliststr);
AjBool ajRangeStrStuff (const AjPRange thys, const AjPStr instr, AjPStr *outstr);
AjBool ajRangeStrMask (const AjPRange thys, AjPStr *str, const AjPStr maskchar);
AjBool ajRangeStrToLower (const AjPRange thys, AjPStr *str);
```

它们的功能与序列对应函数相同，区别在于接受字符串 (`AjPStr`) 而不是序列 (`AjPSeq`)。此外，`ajRangeStrStuff` 为输入和输出字符串提供单独的参数。

## 6.5 字符串处理

### 6.5.1 简介

高效且灵活的字符串处理是分子序列操作的基础。因此，字符串处理是 AJAX 库中发展最完善的领域。该功能分布在多个库文件中，内容全面，包括：

- 字符串构造
- 字符串引用和取消引用，在需要对字符串的句柄而非副本时使用
- 用于向字符串赋值的赋值函数
- 用于合并两个字符串或字符串部分的函数。操作类型包括追加、插入和粘贴（覆盖字符位置）
- 用于从目标字符串中删除子字符串、区域或字符的剪切函数
- 用其他字符或子字符串替换字符串中的字符或子字符串
- 用于测试字符串属性的查询函数
- 检索字符和字符串属性（例如长度）
- 用于将字符串转换为其他数据类型的转换函数
- 字符串格式化
- 字符串比较函数
- 用于在字符串中查找子字符串或字符的搜索函数
- 用于从字符串中解析文本标记的字符串解析函数
- 字符串迭代，允许一次逐个字符地遍历字符串
- 字符串标记化
- 格式化和打印。所有 EMBOSS 基本数据类型（第 5.1 节“基本数据类型”）均定义了转换字符，并且是基本 C 转换代码的扩展。

为方便起见，大多数为 AJAX 字符串参数实现的函数都有对应的带有 C 类型 (`char *`) 字符串参数的函数。字符串可以在 ACD 文件中定义，并通过调用 `ajAcdGetString` 从 C 源代码中检索。不过，更典型的做法是直接在代码中创建字符串。

与标准 C 类型 (`char *`) 字符串相比，AJAX 字符串对象 (`AjPStr`) 是动态的；内存会根据需要（重新）分配，因此在调用字符串函数时永远不会用完空间。AJAX 字符串是引用计数的。对象会跟踪代码中字符串的引用数量（指向字符串的指针）。只有当字符串的所有引用都被删除后，字符串本身才会被释放。

字符串对象定义如下：



typedef struct AjOStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;

Ptr 持有字符串，Len 是其长度。与 C 类型字符串不同，该字符串可能以 NULL 结尾，也可能不是。用于打印 AjPStr 对象的库函数使用长度字段 (Len) 来确定打印多少个字符，即使存在 NULL 也不会在第一个 NULL 处停止。

Res 是与对象关联的保留动态内存，始终至少等于 Len，但通常更大。它用于处理字符串内存的动态重新分配。Use 是上面提到的字符串引用计数器。最后，Padding 元素将字符串填充到对齐边界（以安抚严格的编译器）。

字符串对象及字符串内存管理的内部细节在其他地方有更详细的描述（第 5.5 节，“使用对象编程”）。

## 6.5.2 AJAX 库文件

用于处理字符串的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| :--- | :--- |
| ajstr | 通用字符串处理 |
| ajfmt | 字符串格式化函数 |

ajstr.h/c. 大多数通用字符串处理所需的函数都在此。它们定义了基本字符串对象 AjPStr、字符串迭代对象 (AjIStr) 和字符串标记解析器对象 (AjPStrTok)，用于与这些函数配合使用。

ajfmt.h/c. 字符串格式化函数。这些函数类似于 C 函数 printf、fprintf 等，但转换说明符和其他功能的集合已扩展。它们还包含用于低级处理格式化的静态数据结构和函数（第 6.5.23 节，“处理字符串格式化”）。

除非您计划扩展字符串库，否则不太可能需要静态数据结构和函数。

## 6.5.3 ACD 数据类型

用于处理字符串输入的 ACD 数据类型是：

AjPStr String

## 6.5.4 ACD 数据定义

字符串输入的典型 ACD 定义：

```
string: delimiter
[
    default: "|"
    information: "Delimiter of records in text output file"
    knowntype: "output delimiter"
]
```

### 6.5.4.1 参数名称

可能会使用标准参数名称（第 A.1.3 节，“参数命名约定”）。这取决于数据定义的特定用例。

### 6.5.4.2 常见属性

通常指定的属性摘要如下。它们都是全局属性（第 A.4 节，“全局属性”）。

- `default:` 默认值（全局属性）
- `information:` 应用程序文档中使用的用户提示（全局属性）
- `knowntype:` 字符串输入应始终指定。如果输出不是任何标准 EMBOSS 已知类型（第 4.3.5.3.1 节，“应用程序数据已知类型文件 (knowntypes.standard)”），则 `ApplicationName` 输出是推荐值（全局属性）。

## 6.5.5 AJAX 数据类型

用于处理字符串（包括 ACD 文件中定义的字符串（`string` ACD 数据类型）），请使用：

```
AjPStr String
```

两种数据类型用于字符串相关操作：

- `AjIStr` 字符串迭代对象
- `AjPStrTok` 字符串标记解析器对象

## 6.5.6 ACD 文件处理

用于通过 ACD 文件处理字符串输入的数据类型和函数如下所示。

| 标题 | 读取字符串 |
| :--- | :--- |
| ACD 数据类型 | string |
| AJAX 数据类型 | AjPStr |
| 从 ACD 检索 | ajAcdGetString |

### 6.5.6.1 输入字符串检索

要检索输入字符串，需先声明对象指针，然后使用 ajAcdGetString 进行初始化：

```
AjPStr delimiter = NULL;
delimiter = ajAcdGetString("delimiter");
```

### 6.5.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

## 6.5.7 字符串对象内存管理

### 6.5.7.1 默认对象构造

要使用未在 ACD 文件中定义的字符串对象，必须首先实例化相应的对象指针。默认字符串构造函数是：

```
/* Create a string object. */
AjPStr ajStrNew (void);
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但最好如此：

```
AjPStr str = NULL;
str = ajStrNew();
/* The object is instantiated and ready for use */
```

### 6.5.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认字符串析构函数是：

```
/* Delete a string object. */
AjPStr ajStrDel (AjPStr *Pstr);
```

调用函数有责任销毁任何对象

```
AjPStr str = NULL;

str = ajStrNew();

/* Do something with the instantiated object */

ajStrDel(&str);

/* The memory is freed and the pointer reset to NULL, ready for re-use. */

str = ajStrNew();

/* Do something else with the new object. The pointer variable is reallocated. */

ajStrDel(&str);

/* Done with the object so the memory is freed. */
```

### 6.5.7.3 替代对象构造和加载

有多种替代字符串构造函数可用。字符串可以从现有字符串对象 (AjPStr) 或 C 类型 (char *) 字符串构造，并带有可选的保留大小：

```
/* Construct from C-type string */
AjPStr ajStrNewC (const char *txt);

/* Construct from C-type string with reserved size */
AjPStr ajStrNewResC (const char *txt, ajuint size);

/* Construct from C-type string with explicit reserved size */
AjPStr ajStrNewResLenC (const char *txt, ajuint size, ajuint len);

/* Construct with reserved size */
AjPStr ajStrNewRes(ajuint size);

/* Construct from string object */
AjPStr ajStrNewS (const AjPStr str);

/* Construct from string object with reserved size */
AjPStr ajStrNewResS (const AjPStr str, ajuint size);
```

ajStrNewResLenC 与 ajStrNewResC 相同，只是将字符串长度传递给 ajStrNewResLenC 以提高速度。

它们的用法与默认构造函数相同，即返回指向新对象的指针。

## 6.5.8 字符串引用和取消引用函数

有一个字符串引用函数：

```
/* Reference an existing string */
AjPStr ajStrNewRef (AjPStr str);
```

与其他构造函数不同，ajStrNewRef 不创建新对象，而是返回传入字符串的指针并增加其引用计数。
有一个字符串取消引用函数：

```
/* Dereference an existing string */
AjBool ajStrDelStatic (AjPStr* Pstr);
```

ajStrDelStatic 将字符串指针设置为 NULL 并减少其引用的字符串的使用计数。与默认析构函数不同，使用计数为 1 的字符串不会被释放，以避免在重复使用时释放和重新分配内存。此函数永远不会删除为字符串保留的内存，该内存可以重复使用。

## 6.5.9 字符串赋值函数

字符串赋值函数将值赋给字符串。字符串可以从字符、现有字符串对象 (AjPStr) 或 C 类型 (char *) 字符串，或适当数据类型的子字符串赋值。某些函数变体允许指定可选的保留大小：

```
/* Assign from character */
AjBool ajStrAssignK (AjPStr* Pstr, char chr);

/* Assign from C-type string */
AjBool ajStrAssignC (AjPStr* Pstr, const char* txt);

/* Assign from string object */
AjBool ajStrAssignS (AjPStr* Pstr, const AjPStr str);

/* Assign from C-type string up to a given length */
AjBool ajStrAssignLenC (AjPStr* Pstr, const char* txt, ajuint ilen);

/* Assign using a pointer_only. The reference count is incremented */
AjBool ajStrAssignRef (AjPStr* Pstr, AjPStr refstr);

/* Assign from C-type string with reserved size */
AjBool ajStrAssignResC (AjPStr* Pstr, ajuint size, const char* txt);

/* Assign from string object with reserved size */
AjBool ajStrAssignResS (AjPStr* Pstr, ajuint i, const AjPStr str);

/* Assign from substring of C-type string */
AjBool ajStrAssignSubC (AjPStr* Pstr, const char* txt, ajuint pos1, ajuint pos2);

/* Assign from substring of string object */
AjBool ajStrAssignSubS (AjPStr* Pstr, const AjPStr str, ajuint pos1, ajuint pos2);
```

ajStrAssignLenC 与 ajStrAssignC 相同，只是源字符串仅复制到指定长度。





如果需要，字符串内存会被分配给 NULL 目标指针。不过，为了保持调用代码的直观性，我们强烈建议在使用这些函数之前，先通过调用 ajStrNew 实例化一个字符串对象。

例如，在下面的代码中，很明显你正在处理两个独立的字符串：

```
AjPStr str       = NULL;
AjPStr strcopy   = NULL;

str      = ajStrNewC("A string");
strcopy  = ajStrNew();

if(!ajStrAssignC(&strcopy, str))
    ajFatal("String not assigned");

ajStrDel(&str);
ajStrDel(&strcopy);
```

相比之下，下面的代码完全有效，但不够清晰：

```
AjPStr str       = NULL;
AjPStr strcopy   = NULL;

str = ajStrNewC("A string");

if(!ajStrAssignC(&strcopy, str))
    ajFatal ("String not assigned");

ajStrDel(&str);
ajStrDel(&strcopy);
```

## 6.5.10 字符串组合函数

字符串组合函数将两个字符串组合在一起。它们分为下面描述的多个类别。

### 6.5.10.1 字符串追加函数

字符串追加函数将源字符串追加到目标字符串。可以追加单个字符或多个字符、现有的字符串对象（AjPStr）或 C 类型（char *）字符串，或后两者之一的子串：

```
/* Append a C-type string */
AjBool ajStrAppendC (AjPStr* Pstr, const char* txt);

/* Append a single character */
AjBool ajStrAppendK (AjPStr* Pstr, char chr);

/* Append a string object */
AjBool ajStrAppendS (AjPStr* Pstr, const AjPStr str);

/* Append multiples of a single character */
AjBool ajStrAppendCountK (AjPStr* Pstr, char chr, ajuint num);

/* Append a C-type string up to a given length */
AjBool ajStrAppendLenC (AjPStr* Pstr, const char* txt, ajuint len);

/* Append a substring of a string object */
AjBool ajStrAppendSubS (AjPStr* Pstr, const AjPStr str, ajuint pos1, ajuint pos2);
```

ajStrAppendLenC 与 ajStrAppendC 相同，只是追加源字符串中直到指定长度的一个区域。

### 6.5.10.2 字符串连接函数

字符串连接函数与追加函数类似，只是在追加之前会在指定位置截断源字符串和目标字符串：

```
/* Cut down string at pos1 and add string2 from position pos2. */
AjBool ajStrJoinC (AjPStr* Pstr, ajint pos1, const char* txt, ajint pos2);
AjBool ajStrJoinS (AjPStr* Pstr, ajint pos1, const AjPStr str, ajint pos2);
```

### 6.5.10.3 字符串插入函数

字符串插入函数将字符、现有的字符串对象（AjPStr）或 C 类型（char *）字符串插入到字符串中：

```
/* Insert a C-type string */
AjBool ajStrInsertC (AjPStr* pthis, ajint pos, const char* str);
/* Insert a character */
AjBool ajStrInsertK (AjPStr* pthis, ajint begin, char insert);
/* Insert a string */
AjBool ajStrInsertS (AjPStr* pthis, ajint pos, const AjPStr str);
```

### 6.5.10.4 字符串粘贴函数

字符串粘贴函数将在指定位置（pos）使用源字符串（或字符）覆盖目标字符串，（可选地）最多使用源字符串中指定数量的字符：

```
/* Paste string */
AjBool ajStrPasteS( AjPStr* Pstr, ajint pos, const AjPStr str);
/* Paste specified number of characters */
AjBool ajStrPasteCountK(AjPStr* Pstr, ajint pos, char chr, ajuint num);
/* Paste portion of C-type string */
AjBool ajStrPasteMaxC (AjPStr* Pstr, ajint pos, const char* txt, ajuint n);
/* Paste portion of string object */
AjBool ajStrPasteMaxS( AjPStr* Pstr, ajint pos, const AjPStr str, ajuint n);
```

此外还有一个字符串掩码函数，它将在指定范围内用掩码字符替换目标字符串中的所有字符：

```
/* Replace all characters in a region with mask characters */
AjBool ajStrMaskRange(AjPStr* str, ajint begin, ajint end, char maskchar);
```

## 6.5.11 字符串裁剪函数

字符串裁剪函数将从目标字符串中删除区域或单个字符。下面描述了各个功能类别中可用函数的选集。如果操作成功执行，所有函数都返回 ajTrue，否则返回 ajFalse。

### 6.5.11.1 简单裁剪函数

可以使用以下函数从字符串的开头、结尾或内部删除若干字符：

```
/* Removes a number of characters from the start of a string. */
AjBool ajStrCutStart(AjPStr* Pstr, ajuint len);

/* Removes a number of characters from the end of a string. */
AjBool ajStrCutEnd(AjPStr* Pstr, ajuint len);

/* Removes a region from a string. */
AjBool ajStrCutRange(AjPStr* Pstr, ajuint pos1, ajuint pos2);
```

### 6.5.11.2 从字符串中删除字符

从字符串中删除字符的函数包括：

```
/* Removes non-sequence characters (all but alphabetic characters and asterisk) */
AjBool ajStrRemoveGap(AjPStr* pthis);

/* Removes HTML mark-up from a string. */
AjBool ajStrRemoveHtml(AjPStr* pthis);

/* Removes last character from a string if it is a newline character. */
AjBool ajStrRemoveLastNewline(AjPStr* Pstr);

/* Removes all of a given set of characters from a string. */
AjBool ajStrRemoveSetC(AjPStr* Pstr, const char *txt);

/* Removes all whitespace characters from a string. */
AjBool ajStrRemoveWhite(AjPStr* Pstr);

/* Removes excess whitespace characters from a string. */
AjBool ajStrRemoveWhiteExcess(AjPStr* Pstr);

/* Removes excess space characters from a string. */
AjBool ajStrRemoveWhiteSpaces(AjPStr* Pstr);

/* Removes all characters after the first wildcard character (if found). */
AjBool ajStrRemoveWild(AjPStr* Pstr);
```

ajStrRemoveWhiteExcess 和 ajStrRemoveWhiteSpaces 都会删除字符串的首尾空白字符，并将多个空格替换为单个空格。此外，ajStrRemoveWhiteSpaces 将制表符转换为空格，但保留换行符不变。

### 6.5.11.3 保留字符串中的字符

可用的函数可以从字符串中删除一个区域，或删除字符串中除了定义集之外的所有字符。字符集可以作为字符串对象（AjPStr）或 C 类型（char *）字符串提供：

```
/* Trim sequence down to a defined range */
AjBool ajStrKeepRange(AjPStr* Pstr, ajint pos1, ajint pos2);

/* Removes all characters that are not in a given set. */
AjBool ajStrKeepSetC(AjPStr* Pstr, const char* txt);

/* Removes all characters that are not in a given set. */
AjBool ajStrKeepSetS(AjPStr* Pstr, const AjPStr str);

/* Removes all characters that are not alphabetic. */
AjBool ajStrKeepSetAlpha(AjPStr* Pstr);

/* Removes all characters that are not alphabetic and are not in a given set. */
AjBool ajStrKeepSetAlphaC(AjPStr* Pstr, const char* txt);
```

### 6.5.11.4 字符串修剪函数

下面的字符串修剪函数将从字符串的开头和/或结尾删除给定字符组成（在字符串 txt 中提供）的区域：

```
/* Remove from start of a string */
AjBool ajStrTrimStartC (AjPStr* Pstr, const char* txt);

/* Remove from end of a string */
AjBool ajStrTrimEndC (AjPStr* Pstr, const char* txt);

/* Remove from start and end of a string */
AjBool ajStrTrimC (AjPStr* pthis, const char* txt);
```

将从开头和/或结尾删除所有字符，直到遇到第一个不在提供的集合中的字符。

还提供了类似函数，用于从字符串的开头和结尾仅删除由空白字符组成的区域。

```
/* Remove from start and end of a string. */
AjBool ajStrTrimWhite (AjPStr* Pstr);

/* Remove from start of a string. */
AjBool ajStrTrimWhiteStart (AjPStr* Pstr);

/* Remove from end of a string. */
AjBool ajStrTrimWhiteEnd (AjPStr* Pstr);
```

还有两个截断函数，它们从字符串末尾删除字符，将其缩短到定义长度（ajStrTruncateLen），或在定义位置截断字符串末尾（ajStrTruncatePos）：

```
/* Remove characters from end, reduce to defined length */
AjBool ajStrTruncateLen (AjPStr* Pstr, ajuint len);

/* Cut end of defined position */
AjBool ajStrTruncatePos (AjPStr* Pstr, ajint pos);
```





# 6 使用 AJAX 进行编程

### 6.5.12 字符串替换函数

字符串替换函数将使用其他字符或子串来替换字符串中的字符或子串。

前缀为 ajStrExchange 的函数将把字符串中一个子串（或字符）的所有出现替换为另一个字符串（或字符）。该函数的变体支持用于目标和替换子串的字符串对象（AjPStr）和 C 类型（char *）字符串：

```c
/* C-type string target and replacement. */
AjBool ajStrExchangeCC (AjPStr* Pstr, const char* txt, const char* txtnew);

/* C-type string target, string replacement */
AjBool ajStrExchangeCS (AjPStr* Pstr, const char* txt, const AjPStr strnew);

/* Character target and replacement */
AjBool ajStrExchangeKK (AjPStr* Pstr, char chr, char chrnew);

/* String target, C-type string replacement */
AjBool ajStrExchangeSC (AjPStr* Pstr, const AjPStr str, const char* txtnew);

/* String target and replacement */
AjBool ajStrExchangeSS (AjPStr* Pstr, const AjPStr str, const AjPStr strnew);
```

前缀为 ajStrExchangeSet 的函数类似，只不过它们将把字符串中一组字符的所有出现替换为另一个字符或一组字符。该函数的变体使用字符串对象（AjPStr）和 C 类型（char *）字符串来定义这些集合：

```c
/* C-type string target and replacement sets */
AjBool ajStrExchangeSetCC (AjPStr* Pstr, const char* txt, const char* newc);

/* String target and replacement sets */
AjBool ajStrExchangeSetSS (AjPStr* Pstr, const AjPStr str, const AjPStr strnew);

/* Replace C-type target with single character */
AjBool ajStrExchangeSetRestCK (AjPStr* Pstr, const char* txt, char chr);

/* Replace string target with single character */
AjBool ajStrExchangeSetRestSK (AjPStr* Pstr, const AjPStr str, char chr);
```

### 6.5.13 字符串查询函数

字符串查询函数用于测试字符串的属性。所有前缀为 ajStrIs 的函数，如果字符串满足某些基本测试，则返回 ajTrue。以下函数说明了可以执行的查询测试范围，但完整列表请参阅在线文档：

```c
/* Alphanumeric characters only. */
AjBool ajStrIsAlnum (const AjPStr str);

/* Alphabetic characters only. */
AjBool ajStrIsAlpha (const AjPStr str);

/* Represents Boolean value. */
AjBool ajStrIsBool (const AjPStr str);

/* Represents integer value. */
AjBool ajStrIsInt (const AjPStr str);

/* Represents float value. */
AjBool ajStrIsFloat (const AjPStr str);

/* No uppercase alphabetic characters. */
AjBool ajStrIsLower (const AjPStr str);

/* Decimal digits only. */
AjBool ajStrIsNum (const AjPStr str);

/* Uppercase alphabetic characters only. */
AjBool ajStrIsUpper (const AjPStr str);
```

### 6.5.14 字符串属性和字符检索函数

为方便起见，提供了宏来检索字符串的属性，包括其长度、C 类型（char *）字符串、使用计数和当前保留大小。这些函数都返回字符串 C 数据结构的一个元素：

```c
#define MAJSTRGETLEN(str) str->Len /* String length */
#define MAJSTRGETPTR(str) str->Ptr /* String char * pointer */
#define MAJSTRGETRES(str) str->Res /* Reserved length */
#define MAJSTRGETUSE(str) str->Use /* Usage count */
```

可以使用函数从字符串中返回单个字符。

```c
/* Get first character */
char ajStrGetCharFirst (const AjPStr str);

/* Get last character */
char ajStrGetCharLast (const AjPStr str);

/* Get character from specified position */
char ajStrGetCharPos (const AjPStr str, ajint pos);
```

### 6.5.15 字符串转换函数

字符串可以使用以下某个函数转换为其他数据类型：

```c
AjBool ajStrToBool (const AjPStr str, AjBool* Pval); /* To boolean */
AjBool ajStrToDouble (const AjPStr str, double* Pval); /* To double */
AjBool ajStrToFloat (const AjPStr str, float* Pval); /* To float */
AjBool ajStrToHex (const AjPStr str, ajint* Pval); /* To hexadecimal */
AjBool ajStrToInt (const AjPStr str, ajint* Pval); /* To integer */
AjBool ajStrToLong (const AjPStr str, ajlong* result); /* To long */
AjBool ajStrToUint (const AjPStr str, ajuint* Pval); /* To unsigned integer */
```

在所有情况下，如果转换成功执行，函数均返回 ajTrue。它们采用适当类型变量的地址。例如，要将字符串转换为整数值：

```c
ajint val = 0;
AjPStr str = NULL;

str = ajStrNewC("10");

if (!ajStrToInt(str, &val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```

相反，可以使用以下函数将 C 数据类型转换为 EMBOSS 字符串：

```c
AjBool ajStrFromBool (AjPStr* Pstr, AjBool val); /* From bool */
AjBool ajStrFromDouble (AjPStr* Pstr, double val, ajint precision); /* From double */
AjBool ajStrFromDoubleExp (AjPStr* Pstr, double val, ajint precision); /* From double in exponential form. */
AjBool ajStrFromFloat (AjPStr* Pstr, float val, ajint precision); /* From float */
AjBool ajStrFromInt (AjPStr* Pstr, ajint val); /* From integer */
AjBool ajStrFromLong (AjPStr* Pstr, ajlong val); /* From long */
AjBool ajStrFromUint (AjPStr* Pstr, ajuint val); /* From unsigned integer */
```

同样，这些函数在转换成功执行时返回 ajTrue，并采用字符串的地址。例如，要将整数转换为字符串：

```c
ajint val = 0;
AjPStr str = NULL;

str = ajStrNew();
val = 100;

if (!ajStrFromInt(&str, val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```

### 6.5.16 字符串格式化函数

用于重新格式化字符串的函数具有前缀 ajStrFmt。例如，可以使用以下函数将字符串或字符串区域转换为大写或小写：

```c
/* Convert to lower-case */
AjBool ajStrFmtLower (AjPStr* Pstr);

/* Convert region to lower-case */
AjBool ajStrFmtLowerSub (AjPStr* Pstr, ajint pos1, ajint pos2);

/* Convert to upper-case */
AjBool ajStrFmtUpper (AjPStr* Pstr);

/* Convert region to upper-case */
AjBool ajStrFmtUpperSub (AjPStr* Pstr, ajint pos1, ajint pos2);
```

要重新格式化的字符串的地址会被传递，如果重新格式化成功，则返回 ajTrue。有关其他格式化函数，请参阅在线文档。

### 6.5.17 字符串比较函数

EMBOSS 提供全面的字符串比较函数。

前缀为 ajStrMatch 的函数将一个字符串与另一个字符串进行比较。这些函数执行区分大小写和不区分大小写的比较，可带通配符字符，也可不带。有关以 C 类型（char *）字符串作为第二个参数的变体函数可用，但此处未显示：

```c
/* Simple string to C-type string comparison */
AjBool ajStrMatchC (const AjPStr thys, const char* txt);

/* Simple string to string comparison */
AjBool ajStrMatchS (const AjPStr thys, const AjPStr str);

/* Case-insensitive string to string comparison */
AjBool ajStrMatchCaseS (const AjPStr thys, const AjPStr str);

/* String to string comparison with wildcards */
AjBool ajStrMatchWildS (const AjPStr thys, const AjPStr wild);

/* Case-insensitive string to string comparison with wildcards */
AjBool ajStrMatchWildCaseS (const AjPStr thys, const AjPStr wild);
```

以下函数将比较字符串中的前两个单词：

```c
/* String to C-type string comparison with wildcards. */
AjBool ajStrMatchWildWordC (const AjPStr str, const char* text);

/* String to string comparison with wildcards. */
AjBool ajStrMatchWildWordS (const AjPStr str, const AjPStr text);

/* Case-insensitive string to C-type string comparison with wildcards. */
AjBool ajStrMatchWildWordCaseC (const AjPStr str, const char* text);

/* Case-insensitive string to string comparison with wildcards. */
AjBool ajStrMatchWildWordCaseS (const AjPStr str, const AjPStr text);
```

### 6.5.18 字符串搜索函数

字符串搜索函数具有前缀 ajStrFind，用于在字符串中查找子串或字符：

```c
/* Find a string */
ajint ajStrFindS (const AjPStr str, const AjPStr str2);
/* Find a character */
ajint ajStrFindAnyK(const AjPStr str, char chr);
/* Find any character in a set */
ajint ajStrFindAnyS (const AjPStr str, const AjPStr str2);
/* Find a string (case-insensitive) */
ajint ajStrFindCaseS (const AjPStr str, const AjPStr str2);
/* Find any character not in a set */
ajint ajStrFindRestS (const AjPStr str, const AjPStr str2);
/* Find any character not in a set (case-insensitive) */
ajint ajStrFindRestCaseS (const AjPStr str, const AjPStr str2);
/* Find last occurence of a string */
ajint ajStrFindLastS (const AjPStr str, const AjPStr str2);
```

这些函数返回搜索文本在序列中的起始位置，如果未找到文本，则返回 -1。

ajStrFindAnyS、ajStrFindRestS 和 ajStrFindRestCaseS 使用作为字符串（str2）提供的一组字符。





## 6.5.19 字符串解析函数

用于从字符串中解析文本标记的函数具有前缀 ajStrExtract 或前缀 ajStrParse。

要从输入字符串 (str) 中提取第一个单词 (Pword) 和字符串的其余部分 (Prest)，请使用以下任一函数：

```
/* Remove first word (with no leading spaces) from a string *
AjBool ajStrExtractFirst (const AjPStr str, AjPStr* Prest, AjPStr* Pword);

/* Remove first word from a string, skipping spaces */
AjBool ajStrExtractWord (const AjPStr str, AjPStr* Prest, AjPStr* Pword);
```

ajStrExtractWord 会跳过任何前导空白，而如果输入字符串以空格开头，ajStrExtractFirst 将返回 ajFalse。与大多数字符串函数一样，如果需要，它们会为字符串分配内存，尽管手动分配字符串更为整洁。在下面的示例中，ajStrExtractFirst 将返回 ajFalse 且打印的字符串将为空，而 ajStrExtractWord 将打印第一个单词和字符串的其余部分：

```
AjPStr inputstring = NULL;
AjPStr word     = NULL;
AjPStr rest     = NULL;

inputstring = ajStrNewC(" First word in this string is 'First'");
word        = ajStrNew();
rest        = ajStrNew();

ajStrExtractFirst(inputstring, &rest, &word);
ajFmtPrint("word: %S\n", word);   /* Empty */
ajFmtPrint("rest: %S\n", rest);   /* Empty */

ajStrExtractWord(inputstring, &rest, &word);
ajFmtPrint("word: %S\n", word);   /* First */
ajFmtPrint("rest: %S\n", rest);   /* word in this string is 'First' */

ajStrDel(&inputstring);
ajStrDel(&word);
ajStrDel(&rest);
```

有一个函数可以将以换行符分隔的多行字符串拆分为字符串数组：

```
ajuint ajStrParseSplit(const AjPStr str, AjPStr **PStr);
```

该函数为字符串数组分配内存（稍后必须释放），并返回创建的数组元素数量：

```
AjPStr inputstring = NULL;
AjPStr *array      = NULL;
ajint    dim;
ajint    x;

inputstring = ajStrNewC("First line\nSecond line\nThird line\n");

dim = ajStrParseSplit(inputstring, &array);

for(x=0; x<dim; x++)
	 ajFmtPrint("array[%d] : %S\n", x, array[x]);

ajStrDel(&inputstring);

for(x=0; x<dim; x++)
	 ajStrDel(&array[x]);

AJFREE(array);
```

## 6.5.20 字符串迭代

字符串迭代允许您一次一个字符地遍历字符串。AJAX 用于此目的的数据类型是：

AjIStr 字符串迭代对象

要遍历字符串，必须首先实例化字符串迭代对象。提供了两个构造函数，用于正向（从开始到结束）或反向（从结束到开始）迭代：

```
/* Constructor for forward iteration */
AjIStr ajStrIterNew (const AjPStr thys);

/* Constructor for reverse iteration */
AjIStr ajStrIterNewBack (const AjPStr thys);
```

要遍历字符串，请使用以下任一函数。如果迭代无法继续，它们将返回 NULL：

```
/* Forward iteration */
AjIStr ajStrIterNext (AjIStr iter);

/* Reverse iteration */
AjIStr ajStrIterNextBack (AjIStr iter);
```

要检索当前位置的字符或字符串的其余部分，请使用：

```
/* Retrieve the character */
char ajStrIterGetK (const AjIStr iter);

/* Retrieve the remainder of the string */
const char* ajStrIterGetC (const AjIStr iter);
```

要更改当前位置的字符，请使用：

```
/* Change character */
void ajStrIterPutK (AjIStr iter, char chr);
```

以下函数如果迭代可以继续则返回 ajTrue，也用于控制迭代：

```
/* Test if iteration can continue */
AjBool ajStrIterDone (const AjIStr iter);

/* Test if reverse iteration can continue */
AjBool ajStrIterDoneBack (const AjIStr iter);
```

字符串迭代器可以重置，以便它指向字符串的开头或结尾：

```
/* Reset forward iteration to start of string */
void ajStrIterBegin (AjIStr iter);

/* Reset reverse iteration to end of string */
void ajStrIterEnd (AjIStr iter);
```

完成后，必须释放字符串迭代对象：

```
/* Destructor for iteration object */
void ajStrIterDel (AjIStr* iter);
```

下面的示例代码使用迭代函数遍历字符串，将所有连字符字符替换为句点并写入新字符串：

```
AjPStr str = NULL;
AjPStr seq = NULL;
AjIStr iter = NULL;
char chr;

str = ajStrNewC("- -AALIY- -TIWLASL- -");
seq = ajStrNew();

iter = ajStrIterNew(str);

while(ajStrIterNext(iter))
{
    if((chr = ajStrIterGetK(iter)) == '-')
        ajStrIterPutK(iter, '.');
    else
        ajStrAppendK(&seq, chr);
}

ajFmtPrint("str: %S\n", str);
ajFmtPrint("seq: %S\n", seq);

ajStrDel(&str);
ajStrDel(&seq);
ajStrIterDel(&iter);
```

## 6.5.21 字符串标记化

有一个专用的 AJAX 数据类型用于字符串标记化：

AjPStrTok 字符串标记化对象

字符串标记化函数具有前缀 ajStrToken，用于将字符串分隔为文本标记并提取它们。

要标记化字符串，必须首先实例化字符串标记化对象。提供的构造函数将分隔符字符作为 C 类型 (char *) 或 EMBOSS 字符串 (AjPStr)，并返回指向字符串标记化对象的指针：

```
/* Create string tokenisation object */
AjPStrTok ajStrTokenNewC (const AjPStr str, const char* txtdelim);
AjPStrTok ajStrTokenNewS (const AjPStr str, const AjPStr strdelim);
```

还可以为现有的字符串标记化对象设置要标记化的序列和分隔符字符串：

```
/* Specify string to be tokenised only */
AjBool ajStrTokenAssign (AjPStrTok* Ptoken, const AjPStr str);

/* Specify string and delimiters */
AjBool ajStrTokenAssignC (AjPStrTok* Ptoken, const AjPStr str, const char* txtdelim);

/* Specify string and delimiters */
AjBool ajStrTokenAssignS (AjPStrTok* Ptoken, const AjPStr str, const AjPStr strdelim);
```

如果需要，这些函数会分配字符串标记化对象，因此可以用作构造函数的替代方案。但是，只有在用于更新使用标准构造函数创建的对象时，它们才更清晰。

要从字符串中解析单个标记，请调用：

```
/* Parse tokens from a string */
AjBool ajStrTokenNextFind (AjPStrTok* Ptoken, AjPStr* Pstr);
AjBool ajStrTokenNextFindC (AjPStrTok* Ptoken, const char* strdelim, AjPStr* Pstr);
```

ajStrTokenNextFindC 将使用分隔符字符串 (strdelim) 更新字符串标记化对象。

要返回部分解析过的字符串的其余部分，请调用：

```
/* Get a string remainder */
AjBool ajStrTokenRestParse (AjPStrTok* Ptoken, AjPStr* Pstr);
```

如果希望将分隔符视为字符串而非单个字符，换句话说，要使用另一个字符串来标记化字符串，请使用以下函数从字符串中解析单个标记：

```
/* Tokenise a string using another string */
AjBool ajStrTokenNextParse (AjPStrTok* Ptoken, AjPStr* Pstr);
AjBool ajStrTokenNextParseC (AjPStrTok* Ptoken, const char* txtdelim, AjPStr* Pstr);
AjBool ajStrTokenNextParseS (AjPStrTok* Ptoken, const AjPStr strdelim, AjPStr* Pstr);
```

如果标记解析成功，这些函数将返回 ajTrue，否则返回 ajFalse。ajStrTokenNextParseC 和 ajStrTokenNextParseS 将使用提供的分隔符字符串 (strdelim 或 txtdelim) 更新字符串标记化对象。请注意，如果自上次调用以来更改了分隔符，这些函数可能会返回 ajTrue 但写入空标记 (Pstr)。

可以通过调用以下函数重置字符串标记化对象（清除所有字符串），以便其准备好重复使用：

```
void ajStrTokenReset (AjPStrTok* Ptoken);
```

完成后，必须释放字符串标记化对象：

```
/* String tokenisation object destructor */
void ajStrTokenDel (AjPStrTok* Ptoken);
```

下面的示例代码使用字符串标记化对象及其函数，从包含多个换行符的字符串中检索各个行：

```
AjPStr inputstring  = NULL;
AjPStr token        = NULL;
AjPStrTok tokens    = NULL;

inputstring = ajStrNewC("First line\nSecond line\nThird line\n");
tokens = ajStrTokenNewC(inputstring, "\n");

while(ajStrTokenNextFind(&tokens, &token))
    ajFmtPrint("token: %S\n", token);

ajStrTokenDel(&tokens);
ajStrDel(&inputstring);
```

字符串 (str 或 txt) 可以使用空白字符或作为文本字符串 (txtdelim) 给出的指定分隔符集进行标记化：

```
/* Tokenise C-type string by set of delimiters */
AjPStr ajCharParseC (const char* txt, const char* delim);

/* Tokenise by set of delimiters */
const AjPStr ajStrParseC (const AjPStr str, const char* txtdelim);

/* Tokenise by whitespace */
const AjPStr ajStrParseWhite (const AjPStr str);
```

这些函数使用 C strtok 函数并从字符串中返回标记。第一次调用函数时，会传入要解析的字符串。对同一字符串的后续调用，第一个参数传入 NULL。返回指向标记的指针，或者在所有标记都已解析时返回 NULL：



```c
AjPStr inputstring = NULL;
AjPStr token       = NULL;

inputstring = ajStrNewC(" First word in this string is 'First'");
token = ajStrParseWhite(inputstring);

/* Prints 'First' to the screen */
ajFmtPrint("token: %S\n", token);

/* Prints the rest of the words, one word at a time */
while(token = ajStrParseWhite(NULL))
    ajFmtPrint("token: %S\n", token);

ajStrDel(&inputstring);
```

要统计字符串中的标记数量，其中标记由空白字符或指定的分隔符集（strdelim）分隔，请使用：

```
/* Count tokens delimited by whitespace */
ajuint ajStrParseCount (const AjPStr line);

/* Count tokens delimited by set of delimiters */
ajuint ajStrParseCountS (const AjPStr line, const AjPStr strdelim);
```

## 6.5.22 处理 C 类型（char *）字符串

为方便起见，提供了多组用于处理 C 类型（char *）字符串的函数。它们都带有 ajChar 前缀，以便与其他函数区分。

### 6.5.22.1 C 类型字符串构造函数和析构函数

与 EMBOSS 字符串一样，C 类型字符串可以从起始的 C 类型（char *）或字符串对象创建，可以带有保留大小，也可以不带：

```
/* Create a string from a C-type string         */
char*   ajCharNewC (const char* txt);

/* Create a string from a string object         */
char*   ajCharNewS (const AjPStr this);

/* Create an empty string of reserved size.     */
char*   ajCharNewRes(ajuint size);

/* Create a string with reserved size from a C-type string */
char*   ajCharNewResC(const char* txt, ajuint size);

/* Create a string with reserved size from a string object */
char*   ajCharNewResS(const AjPStr str, ajuint size);

/* Create a string from a C-type string with specified length */
char*   ajCharNewResLenC(const char* txt, ajuint size, ajuint len);
```

在所有情况下，都会返回指向已分配内存的指针，使用完毕后必须释放它。要删除 C 类型字符串，请调用：

```
void ajCharDel (char** Ptxt);
```

示例：

```
char* string = NULL;
string = ajCharNewC("This is a text string");
ajCharDel(&string);
```

### 6.5.22.2 C 类型字符串比较函数

大多数字符串比较函数（第 6.5.17 节，“字符串比较函数”）也可用于 C 类型字符串：

```
AjBool ajCharMatchC (const char* txt1, const char* txt2);
AjBool ajCharMatchCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildNextC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildWordC (const char* str, const char* txt);
AjBool ajCharMatchWildNextCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildWordCaseC (const char* str, const char* txt);
AjBool ajCharPrefixC (const char* txt, const char* pref);
AjBool ajCharPrefixCaseC (const char* txt, const char* pref);
AjBool ajCharSuffixC (const char* txt, const char* suff);
AjBool ajCharSuffixCaseC (const char* txt, const char* suff);
```

这些函数的变体版本（未显示）接受字符串对象作为第二个参数，其后缀为 S 而非 C。

## 6.5.23 处理字符串格式化

用于格式化和打印字符串的函数定义在库文件 ajfmt.h/c 中。所有 EMBOSS 基本数据类型（第 5.1 节，“基本数据类型”）都定义了转换字符，它们是基本 C 转换代码的扩展。它们如下：

- AJAX 字符串对象 `AjPStr` 由 `%S` 打印
- C 类型（`char*`）字符串由 `%s` 打印。如果指针为 `NULL`，则打印 `<null>`
- AJAX 文件对象 `AjPFile` 的文件名由 `%F` 打印
- 布尔变量 `AjBool` 由 `%b` 打印（输出为“Y/N”）或 `%B`（“Yes/No”）
- 日期和时间（`AjPDate`）由 `%D` 打印

带有 ajFmtScan 前缀的函数相当于 C 的 *scan* 函数：

```
ajint ajFmtScanS (const AjPStr str, const char* fmt, ...);
ajint ajFmtScanC (const char* txt, const char* fmt, ...);
ajint ajFmtScanF (AjPFile this, const char* fmt, ...);
```

带有 ajFmtPrint 前缀的函数相当于 C 的 *print* 函数：

```
/* format and emit the "..." arguments according to fmt; writes to stdout */
void ajFmtPrint (const char *fmt, ...);

/* format and emit the "..." arguments according to fmt; writes to a file object */
void ajFmtPrintF (AjPFile file,
    const char *fmt, ...);

/* format and emit the "..." arguments according to fmt; writes to C FILE stream */
void ajFmtPrintFp (FILE *stream,
    const char *fmt, ...);

/* formats the "..." arguments into a buffer with a maximum size according to fmt */
ajint ajFmtPrintCL (char *buf, ajint size,
    const char *fmt, ...);

/* Block and print a string. String is split at given delimiters */
void ajFmtPrintSplit(AjPFile outf, const AjPStr str,
    const char *prefix, ajint len,
    const char *delim);

/* Formats the "..." arguments into an AjPStr according to fmt */
AjPStr ajFmtPrintS (AjPStr *pthis, const char *fmt, ...);

/* Formats the "..." arguments and appends to an AjPStr according to fmt */
AjPStr ajFmtPrintAppS (AjPStr *pthis, const char *fmt, ...);
```

## 6.6 处理序列模式

### 6.6.1 简介

正则表达式和其他模式用于识别分子序列中的基序。

### 6.6.2 AJAX 库文件

用于处理模式的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整说明及使用笔记）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajreg | 正则表达式处理 |
| ajpat | 模式处理 |

ajreg.h/c 定义了正则表达式对象（AjPRegexp）和用于处理正则表达式的函数。

ajpat.h/c 定义了序列模式列表对象（AjPPatlistSeq）和常规模式列表对象（AjPPatlistRegex）以及用于处理正则表达式模式列表的函数。它们包含用于在低级别处理序列模式的静态数据结构和函数。

除非您计划实现代码以扩展库本身的功能，否则不太可能需要这些静态数据结构和函数。

除上述库文件外，EMBOSS 还包含一个函数库，用于支持语法和语义尽可能接近 Perl 5 语言的正则表达式。库文件如下：

```
pcre_config.h
pcre_internal.h
pcre.h
pcre.c
pcreposix.h
pcreposix.c
pcre_printint.c
pcre_chartables.c
pcre_get.c
pcre_study.c
```

此处未对其进行描述，有关更多信息，请参阅在线库文档。

### 6.6.3 ACD 数据类型

有两种用于处理模式输入的数据类型：

- regexp：正则表达式模式
- pattern：序列模式

### 6.6.4 ACD 数据定义

典型的 ACD 定义如下所示。

### 6.6.4.1 regexp

正则表达式输入：

```
regexp: patterns
[
    information: "Regular expression patterns"
    upper: "Y"
    minlength: "3"
    minlength: "10"
]
```

### 6.6.4.2 pattern

模式输入：

```
pattern: seqpatterns
[
    information: "Sequence patterns"
    type: "nucleotide"
    pmismatch: "0"
]
```

### 6.6.4.3 参数名称

所有模式或正则表达式输入的数据定义都应具有标准参数名称 pattern（参见 ）。

### 6.6.4.4 常用属性

通常指定的属性摘要如下。这些属性包括各种特定于数据类型的属性（第 A.5 节，“特定于数据类型的属性”）。

- **最小长度：** 指定正则表达式的最小长度。这用于确保已定义表达式。
- **最大长度：** 指定正则表达式的最大长度。
- **最大大小：** 指定将从文件中读取的模式的最大数量。
- **大小写：** 将正则表达式的大小写设置为大写。`lower` 也可用（只能给出一个）。
- **类型：** 定义正则表达式或模式为 `nucleotide` 或 `protein`，这允许模式匹配使用序列歧义代码。默认情况下，类型为 `string`，它使用精确字符匹配。
- **模式不匹配数：** 设置模式中允许的不匹配数量。正则表达式算法不允许此操作，因此仅适用于序列模式。
- **模式名称：** 设置用于输出的模式名称。多个输入模式会在此名称后附加数字。
- **模式格式：** 定义模式或正则表达式输入格式。默认是将字符串用作模式，或（如序列输入一样）以 `@filename` 形式读取字符串作为模式文件。如果该文件的格式定义为 ‘fasta’，则它具有一个带有可选 `mismatch=nn` 项的 FASTA 风格标识符行，用于设置每个模式的不匹配数量（不匹配不适用于正则表达式）。默认格式是每行一个序列，名称使用 `-pname` 限定符自动定义。





## 6.6.5 AJAX 数据类型

处理模式的基本 AJAX 数据类型是：

- AjPRegexp 正则表达式

提供了两个 AJAX 数据类型用于处理模式列表，包括 ACD 文件中定义的输入模式。这些是使用以下数据类型的单个模式和正则表达式列表。

- AjPPatlistSeq 序列模式列表对象，保存一系列序列模式及其关联信息（用于 pattern ACD 数据类型）
- AjPPatlistRegex 通用模式列表对象，保存一系列通用模式及其关联信息（用于 regexp ACD 数据类型）

以下 AJAX 数据类型用于在低级别处理正则表达式，超出静态数据结构和函数提供的范围。您不太可能直接使用这些：

- AjPPatComp 编译和搜索所需的所有数据
- AjPPatternSeq 特征模式定义
- AjPPatternRegex 保存特征模式定义

## 6.6.6 ACD 文件处理

以下显示了用于通过 ACD 文件处理模式输入的数据类型和函数。

| 标题 | 读取正则表达式 | 读取序列模式 |
| :--- | :--- | :--- |
| ACD 数据类型 | regexp | pattern |
| AJAX 数据类型 | AjPPatlistRegex | AjPPatlistSeq |
| 从 ACD 检索 | ajAcdGetRegexp | ajAcdGetPattern |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存。您可以通过 ajAcdGet* 函数系列对内存进行控制，这些函数返回指向相应对象的指针。

### 6.6.6.1 输入模式检索

要检索输入模式，需声明一个对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

### 6.6.6.1.1 正则表达式

```
AjPPatlistRegex patterns=NULL;
patterns = ajAcdGetRegexp("patterns");
```

### 6.6.6.1.2 模式

```
AjPPatlistSeq seqpatterns=NULL;
seqpatterns = ajAcdGetPattern("seqpatterns");
```

### 6.6.6.2 替代 ACD 检索函数

在只需要单个正则表达式的情况下，使用 ajAcdGetRegexpSingle 返回单个 AjPRegexp 对象：

```
AjPRegexp ajAcdGetRegexpSingle (const char *token);
```

用法如下：

```
AjPRegexp regexp=NULL;
regexp = ajAcdGetRegexpSingle("patterns");
```

任何其他模式或正则表达式的内存将通过最终调用 embExit 自动释放。

### 6.6.6.3 处理命令行选项和 ACD 属性

目前没有用于此的函数。

### 6.6.6.4 内存管理

在程序结束时，关闭任何文件并释放内存是您的责任。必须对 ajAcdGetRegexp 或 ajAcdGetPattern 调用返回的任何对象调用默认析构函数（见下文）。

## 6.6.7 模式对象内存管理

### 6.6.7.1 默认对象构造

要使用未在 ACD 文件中定义的模式对象，必须首先实例化相应的对象指针。默认构造函数如下：

```
/* Create a new regular expression. */
AjPPatlistRegex ajPatlistRegexNew (void);

/* Create a new sequence pattern */
AjPPatlistSeq ajPatlistSeqNew (void);

/* Create a new prosite pattern object */
AjPPatComp ajPatCompNew (void);
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好实践：

```
AjPPatlistRegex  expression = NULL;
AjPPatlistSeq    pattern = NULL;

expression = ajPatlistRegexNew();
pattern    = ajPatlistSeqNew();
/* The objects are instantiated and ready for use */
```

### 6.6.7.2 默认对象销毁

在指针重复使用之前以及使用完对象后，必须释放对象的内存。默认析构函数如下：

```
/* Delete a regular expression.  */
void ajPatlistRegexDel (AjPPatlistRegex* this);
/* Delete a pattern list object */
void ajPatlistSeqDel (AjPPatlistSeq* this);

/* Delete a pattern object */
void ajPatternSeqDel (AjPPatternSeq* this);
/* Delete a prosite pattern object */
void ajPatCompDel (AjPPatComp* this);
```

用法如下：

```
AjPPatlistSeq plist = NULL;
AjPPatlistRegex rlist = NULL;
AjPRegexp patexp = NULL;
AjPSeqall seqall = NULL;
AjPSeq seq = NULL;

plist = ajAcdGetPattern("pattern");
rlist = ajAcdGetRegexp("regexp");
seqall = ajAcdGetSeqall("sequence");
while(ajSeqallNext(seqall, &seq))
/* Do something */

ajPatlistSeqDel(&plist);
ajPatlistRegexDel(&rlist);
```

### 6.6.7.3 替代对象构造和加载

这些函数在内部用于处理模式和正则表达式列表。开发者在使用列表时可调用这些函数：

```
/* Constructor for a sequence pattern list object
   (adds a pattern to a supplied list). */
AjPPatternSeq ajPatternSeqNewList (AjPPatlistSeq plist, const AjPStr name,
                                   const AjPStr pat, ajuint mismatch);
AjPPatternRegex ajPatternRegexNewList (AjPPatlistRegex plist,
                                       const AjPStr name,
                                       const AjPStr pat);
/* Constructor for a sequence pattern list object (parameter is true for a protein
pattern) */
AjPPatlistSeq ajPatlistSeqNewType (AjBool Protein);
/* Constructor for a pattern list object with a specified type */
AjPPatlistRegex ajPatlistRegexNewType (ajuint type);
/* Removes current pattern from pattern list. */
void ajPatlistSeqRemoveCurrent (AjPPatlistSeq this);
void ajPatlistRegexRemoveCurrent (AjPPatlistRegex this);
/* Adds pattern into patternlist */
void ajPatlistAddRegex (AjPPatlistRegex this, AjPPatternRegex pat);
void ajPatlistAddSeq (AjPPatlistSeq this, AjPPatternSeq pat);
```

## 6.6.8 读取函数

这些函数在 ACD 处理中用于将模式限定符值（模式或文件名引用）转换为模式或正则表达式列表。它们可用于从字符串或文件定义模式：

```
/* Parses a file of regular expressions into a pattern list object. */
AjPPatlistRegex ajPatlistRegexRead(const AjPStr patspec,
                                   const AjPStr patname,
                                   const AjPStr fmt,
                                   ajuint type,
                                   AjBool upper, AjBool lower);
/* Parses a file into pattern list object. */
AjPPatlistSeq ajPatlistSeqRead(const AjPStr patspec,
                               const AjPStr patname,
                               const AjPStr fmt,
                               AjBool protein,
                               ajuint mismatches);
/* Resets the pattern list iteration. */
void ajPatlistSeqRewind (AjPPatlistSeq this);
void ajPatlistRegexRewind (AjPPatlistRegex this);
```

## 6.6.9 获取对象元素

应用程序在模式和正则表达式列表级别工作。对于这些，有可用函数来返回列表中的项目数，并返回下一个项目。

```
/* Gets next available pattern from list. */
AjBool ajPatlistSeqGetNext (AjPPatlistSeq this,
                            AjPPatternSeq* pattern);

/* Gets number of patterns from list. */
ajuint ajPatlistSeqGetSize (const AjPPatlistSeq plist);

/* Gets number of patterns from list. */
ajuint ajPatlistRegexGetSize (const AjPPatlistRegex plist);

/* Gets next available pattern from list. */
AjBool ajPatlistRegexGetNext (AjPPatlistRegex this,
                              AjPPatternRegex* pattern);
```

还有进一步的函数可用于返回从列表中检索的每个项目的元素：

```
/* Returns the name of the pattern. */
const AjPStr ajPatternSeqGetName (const AjPPatternSeq this);

/* Returns pattern in string format. */
const AjPStr ajPatternSeqGetPattern (const AjPPatternSeq this);

/* Returns void pointer to compiled pattern. */
AjPPatComp ajPatternSeqGetCompiled (const AjPPatternSeq this);

/* Returns true if the pattern is for a protein sequence. */
AjBool ajPatternSeqGetProtein (const AjPPatternSeq this);

/* Returns the mismatch of the pattern. */
ajuint ajPatternSeqGetMismatch (const AjPPatternSeq this);

/* Returns the name of the pattern */
const AjPStr ajPatternRegexGetName (const AjPPatternRegex this);

/* Returns pattern in string format. */
const AjPStr ajPatternRegexGetPattern (const AjPPatternRegex this);

/* Returns void pointer to compiled pattern. */
AjPRegexp ajPatternRegexGetCompiled (const AjPPatternRegex this);

/* Returns the type of the pattern. */
ajuint ajPatternRegexGetType (const AjPPatternRegex this);
```

## 6.6.10 设置对象元素

模式列表对象中没有应设置的元素。





## 6.6.11 调试函数

当命令行上设置 -debug 时，这些函数会将模式对象的内部信息报告到调试文件。

```
void ajPatternSeqDebug (const AjPPatternSeq pat) ;
void ajPatternRegexDebug (const AjPPatternRegex pat) ;
```

## 6.6.12 杂项函数

这些函数将模式列表复制到字符串中，以供调试使用：

```
ajuint ajPatlistRegexDoc (AjPPatlistRegex thys, AjPStr* pdoc) ;
ajuint ajPatlistSeqDoc (AjPPatlistSeq thys, AjPStr* pdoc) ;
```

还有一个函数用于返回与命名正则表达式类型关联的类型：

```
ajuint ajPatternRegexType (const AjPStr type) ;
```

## 6.7 处理序列

### 6.7.1 简介

目前使用的序列格式种类繁多。它们定义了文件中文本的允许布局和内容，包括用于定义数据库中字段的必需文本标记。这些字段包括：

- 序列标识符名称
- 登录号
- 文献信息
- 序列注释，包括对任何特征的描述
- 序列本身
- 与序列关联的分子特征，例如蛋白质二级结构或分子识别位点，保存在特征表中。

文献信息包括诸如以下数据：

- 文献引用
- 实验详情
- 作者联系信息
- 指向其他数据库的交叉链接
- 围绕序列的描述、注释和评论
- 还有更多！

序列数据库中的条目通常会包含一个用于唯一标识数据库中条目的代码。该代码通常是 _登录号_ 和/或 _标识符名称 (ID)_。登录号是一个唯一的字母数字标识符，保证在数据库的整个生命周期内都与该序列保持关联。

> **注意**
> 
> 如果将两个序列合并为一个，则新序列将获得一个新的登录号；合并序列的登录号将保留为“次要”登录号。

EMBL、GenBank 和 SwissProt 共享一个登录号编号方案，因此给定的登录号在上述三个数据库中均可唯一标识一个序列。相比之下，ID 名称在不同版本的数据库之间不保证保持一致，尽管在实践中它们通常是一致的。

EMBOSS 可识别几乎所有已知的输入格式，且大多数格式也可用于输出。在 EMBOSS 命令行上，序列通过其统一序列地址 (USA) 进行引用（参见 _EMBOSS 用户指南_）。这是所有 EMBOSS 应用程序使用的标准序列命名方案。USA 指定一个或多个序列，这些序列可能从文件或较大的数据库中读取或写入。还可以指定其他序列源，例如应用程序或 Web 服务器。

还有一组用于序列输入和输出的命令行限定符。它们允许您设置文件格式、序列区域、数据库和条目名称等内容。此类限定符（第 A.5 节，“特定于数据类型的属性”）也可以作为属性硬编码在 ACD 文件中。

如您所料，AJAX 包含非常完善的序列处理功能。这包括：

- 获取或设置序列对象中的元素。
- 测试序列属性，例如序列是蛋白质还是核苷酸。
- 计算序列属性，例如核苷酸序列的碱基组成或蛋白质序列的分子量。
- 序列与字符串之间的相互转换。
- 处理序列，例如将其修剪到定义区域或删除间隙字符。
- 序列类型验证；序列是蛋白质还是核酸、是否包含间隙等等。这通常在 ACD 文件级别处理，但也可以直接完成。
- 将序列转换为数值形式以便于处理，例如作为评分矩阵的索引。
- 将遗传序列翻译为蛋白质。
- 核苷酸碱基和氨基酸代码之间的相互转换。
- 计算核苷酸序列的属性，例如 DNA 熔解和退火温度及能量。

应用程序的输入和输出序列通常在 ACD 文件中定义，并通过适当的 ajAcdGet* 函数调用检索。有用于输入单个序列、顺序访问多个序列或一个或多个集合中多个序列的 ACD 数据类型。还有相应的用于序列输出的数据类型。如果需要，也可以直接创建序列对象。序列在内部作为字符串保存，所需内存会根据需要动态重新分配。这意味着在使用带有序列对象的函数时没有任意限制。

### 6.7.2 AJAX 库文件

下表列出了用于处理序列的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
| :--- | :--- |
| ajseq | 通用序列处理 |
| ajseqdata | 序列数据类型 |
| ajseqread | 序列读取 |
| ajseqwrite | 序列写入 |
| ajseqdb | 序列数据库访问方法 |
| ajseqabi | 从 ABI 跟踪文件解析序列 |
| ajseqtype | 序列类型的验证和处理 |
| ajtranslate | 序列翻译 |
| ajbase | 碱基转换函数 |
| ajdan | 核酸函数 |

**ajseq.h/c.** 通用序列处理所需的大部分函数。它们定义了用于序列转换的 `AjPSeqCvt` 对象（第 6.7.14 节，“序列转换”）。

**ajseqdata.h/c.** 定义用于一般用途的基本序列对象（`AjPSeq`、`AjPSeqset` 和 `AjPSeqall`），例如通过 ACD 文件处理检索序列。它们还定义了一个序列输入对象（`AjPSeqin`）和一个序列查询对象（`AjPSeqQuery`），用于低级序列检索。

**ajseqread.h/c.** 用于处理序列查询和序列输入对象以及一些通用序列处理函数的函数。它们还定义了静态数据结构和函数，用于在低级别处理来自受支持格式的序列输入。

**ajseqwrite.h/c.** 定义序列输出对象（AjPSeqout）并包含将序列写入文件的函数。它们定义了静态数据结构和函数，用于在低级别处理受支持格式的序列输出。

**ajseqdb.h/c.** 定义一个序列数据库读取对象（SeqSAccess），用于 AjPSeqin 的定义，以及用于处理序列数据库访问所有方面的静态数据结构和函数。

**ajseqabi.h/c.** 提供从应用程序二进制接口 (ABI) 跟踪文件解析序列（和其他数据）的函数。

**ajseqtype.h/c.** 用于处理序列类型的函数。它们还包含用于在低级别验证和处理序列类型的静态数据结构和函数。

**ajtranslate.h/c.** 定义序列翻译对象（AjPTrn）并包含用于处理序列翻译的函数（第 6.8 节，“处理序列翻译”）。

**ajbase.h/c.** 包含用于核苷酸碱字符转换的函数以及用于分子序列的其他字符转换函数。有关更多信息，请参见第 6.7.16 节，“处理 IUB 碱基代码”。

**ajdan.h/c.** 包含用于计算核苷酸序列属性的函数，大多与 DNA 熔解/退火相关。有关更多信息，请参见第 6.7.17 节，“DNA 计算”。

> 注意
> 
> 除非您计划实现代码以支持 EMBOSS 的新序列格式，否则不太可能需要上述文件中的静态数据结构和函数。有关如何执行此操作的建议，请咨询 EMBOSS 开发人员。此处未提供 ajseqdata.h、ajseqread.h/c 和 ajseqwrite.h/c 的详细使用说明。有关如何使用数据类型和函数的建议，请咨询 EMBOSS 开发人员。

### 6.7.3 ACD 数据类型

有四种 ACD 数据类型和相应的方法用于处理序列输入。通常只需要一个序列。当需要多个序列时，可以按顺序读取（例如从数据库），或者读取并作为一个集合保存在内存中（例如来自序列比对）：

- sequence 读取单个序列
- seqall 顺序读取多个序列
- seqset 将多个序列读取为单个集合
- seqsetall 将多个序列读取为多个集合





用于处理序列输出以匹配其输入等价物的数据类型有三种。它们的行为相同：

- seqout 写入单个序列
- seqoutset 将多个序列作为一个集合写入
- seqoutall 逐个顺序写入多个序列

## 6.7.4 ACD 数据定义

序列输入的典型 ACD 定义：

```
# single input sequence
sequence: sequence
[
   parameter: "Y"
   type:      "gapany"
]

# multiple sequence input read sequentially
seqall: sequence
[
   parameter: "Y"
   type:      "gapany"
]

# multiple sequence input read as a single set
seqset: sequence
[
   parameter: "Y"
   type:      "gapany"
   aligned:   "N"
]

# multiple sequence input read as multiple sets
seqsetall: sequence
[
   parameter: "Y"
   type:      "gapany"
   aligned:   "N"
]
```

序列输出的典型 ACD 定义：

```
# single sequence
seqout: outseq
[
   parameter: "Y"
   type:      "gapany"
]

# multiple sequence output (sequential writing)
seqoutall: outseq
[
   parameter: "Y"
   type:      "gapany"
]

# multiple sequence output (written as a set)
seqoutset: outseq
[
   parameter: "Y"
   type:      "gapany"
]
```

### 6.7.4.1 参数名

所有序列输入和输出的数据定义都应具有标准参数名：

- sequence 用于任何序列输入
- outseq 用于任何输出
- 允许替代和变体（例如，多个输入的 asequence 和 bsequence）。

参见附录 A，ACD 语法参考。

### 6.7.4.2 常用属性

通常指定的属性摘要如下。除非它们被指示为全局属性（第 A.4 节，‘全局属性’），否则它们均为数据类型特定属性（第 A.5 节，‘数据类型特定属性’）。

**parameter:** 通常，序列是 EMBOSS 应用程序的主要输入或输出，因此应使用全局属性 parameter: "Y" 将其定义为参数。
**type:** 为验证目的指定输入或输出序列的类型。参见第 A.7 节，‘序列类型’。
**aligned:** 任何 seqset 或 seqsetall 数据类型都必须设置 aligned: 属性，以指示序列是否已排齐。
**features:** 如果为输入或输出序列设置了 features: ACD 属性，则会（如果可用）读取或写入序列特征（第 6.9 节，‘处理特征’）。
**osformat:** 输出序列默认使用 FASTA 格式。格式通常在命令行中设置，但可以通过 osformat: 硬编码默认值。支持所有常见序列格式（请参阅 EMBOSS 用户指南）。

## 6.7.5 AJAX 数据类型

有九种用于处理序列的 AJAX 数据类型。其中四种用于一般用途，包括处理 ACD 文件中定义的序列：

- AjPSeq: 单个序列（用于 sequence ACD 数据类型）
- AjPSeqall: 用于顺序访问多个序列的序列输入流（用于 seqall ACD 数据类型）
- AjPSeqset: 一个或多个集合中的多个序列（用于 seqset 和 seqsetall ACD 数据类型）
- AjPSeqout: 序列输出流（用于 seqout ACD 数据类型）

两种用于序列相关操作：

- AjPSeqCvt: 用于将序列转换为数值形式
- AjPTrn: 保存遗传代码规范以及翻译核苷酸序列和查找起始位点所需的信息

其余的用于超出各库文件中静态数据类型所提供的更低级别的序列处理：

- AjPSeqin: 保存序列 USA 规范以及读取序列和可能的后续序列所需的信息
- SeqSAccess: 保存从数据库读取序列所需的信息：为每种已知数据库类型定义访问方法，并使用定义的数据库访问函数从数据库读取序列。它用于 AjPSeqin 的定义中
- AjPSeqQuery: 用于解释 USA 的条目规范部分（请参阅 EMBOSS 用户指南）

除非您计划实现代码以支持 EMBOSS 的新序列格式，否则不太可能需要这些专用对象。有关如何执行此操作的建议，请咨询 EMBOSS 开发人员。

## 6.7.6 ACD 文件处理

通过 ACD 文件处理序列的数据类型和函数如下所示。

| 标题 | 读取单个序列 | 读取一组序列（例如比对） | 从数据库顺序读取序列 |
|---|---|---|---|
| 序列输入 | | | |
| ACD 数据类型 | sequence | seqall | seqset |
| AJAX 数据类型 | AjPSeq | AjPSeqall | AjPSeqset |
| 从 ACD 检索 | ajAcdGetSeq | ajAcdGetSeqall | ajAcdGetSeqset |
| 获取单个序列 | (ajAcdGetSeq) | ajSeqallNext | ajSeqsetGetSize, ajSeqsetGetseqSeq |

| 序列输出 | | | |
|---|---|---|---|
| | 写入单个序列 | 将序列写入数据库 | 写入一组序列（例如比对） |
| ACD 数据类型 | seqout | seqoutall | seqoutset |
| AJAX 数据类型 | AjPSeqout | AjPSeqout | AjPSeqout |
| 打开输出流 | ajAcdGetSeqout | ajAcdGetSeqoutall | ajAcdGetSeqoutset |
| 将序列写入文件 | ajSeqoutWriteSeq | ajSeqoutWriteSeq | ajSeqoutWriteSet |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，‘处理 ACD 文件’）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，该系列函数返回指向相应对象的指针。

### 6.7.6.1 输入序列检索

要检索输入序列，请使用相应的 ajAcdGet* 函数声明并初始化对象指针。

### 6.7.6.1.1 单个输入序列

```
AjPSeq seq = NULL;
seq = ajAcdGetSeq("sequence");
```

### 6.7.6.1.2 多个顺序输入序列

seqall 对象实际上是在循环中返回单个序列的一种手段。ajSeqallNext 用于遍历序列：

```
AjPSeqall seqall = NULL;
AjPSeq  seq  = NULL;

seqall = ajAcdGetSeqall("sequence");

while(ajSeqallNext(seqall, &seq))
{
  /* Do something with 'seq' */
}
```

### 6.7.6.1.3 集合中的多个输入序列

```
AjPSeqset seqset = NULL;
seqset = ajAcdGetSeqset("sequence");
```

### 6.7.6.1.4 多个集合中的多个输入序列

使用 ajAcdGetSeqsetall，它返回指向 seqset 对象数组的指针：

```
AjPSeqset *seqset = NULL;
seqset = ajAcdGetSeqsetall("sequence");
```

当然，要访问单个集合，请使用数组表示法。实现与 ajAcdGetSeqsetallSingle 相同效果的代码如下：

```
AjPSeqset *seqset = NULL;
AjPSeqset seqsetFirst = NULL;

seqset = ajAcdGetSeqsetall("sequence");
seqsetFirst = seqset[0]; /* Picks up the pointer to the first sequence set. */
```

### 6.7.6.2 输出序列流检索

要检索输出序列流，请使用相应的 ajAcdGet* 函数声明并初始化对象指针。请注意，多个序列集是使用 ajAcdGetSeqoutset 写入的。

### 6.7.6.2.1 单个输出序列

```
AjPSeqout seqout = NULL;
seqout = ajAcdGetSeqout("outseq");
```

### 6.7.6.2.2 多个输出序列

```
AjPSeqout seqout = NULL;
seqout = ajAcdGetSeqoutall("outseq");
```

### 6.7.6.2.3 输出序列集

```
AjPSeqout seqout = NULL;
seqout = ajAcdGetSeqoutset("outseq");
```

### 6.7.6.2.4 多个输出序列集

```
AjPSeqout seqout = NULL;
seqout = ajAcdGetSeqoutset("outseq");
```

### 6.7.6.3 替代 ACD 检索函数

在只需要多个集合中的第一个的情况下，使用 ajAcdGetSeqsetallSingle 返回单个 seqset 对象：

```
AjPSeqset ajAcdGetSeqsetallSingle (const char *token);
```

用法如下：

```
AjPSeqset seqset = NULL;
seqset = ajAcdGetSeqsetallSingle("sequence");
```

调用 embExit 时，会自动清理任何其他序列集的内存。

### 6.7.6.4 处理命令行选项和 ACD 属性

### 6.7.6.4.1 设置序列范围

所有序列输入数据类型都有各种内置命令行限定符（请参阅 EMBOSS 用户指南），包括 -sbegin 和 -send，它们指定序列的起始位置和结束位置。

读取序列时，这些值将保存在相应的序列对象中。无论其值如何，完整的序列都会加载到内存中。函数 ajSeqTrim（或用于 AjPSeqset 对象的 ajSeqsetTrim）用于将序列修剪为由 -sbegin 和 -send 定义的区域：

```
AjPSeq seq = NULL;
seq = ajAcdGetSeq("sequence");
ajSeqTrim(seq);
```

### 6.7.6.4.2 设置输出格式

有一个用于设置输出格式的函数，尽管这通常由用户指定并在 ACD 文件处理期间处理：

```
AjBool ajSeqoutSetFormatS (AjPSeqout thys, const AjPStr format);
```

### 6.7.6.5 写入序列

有两个 AJAX 函数用于写出序列信息。

```
void ajSeqoutWriteSeq (AjPSeqout outseq, const AjPSeq seq);
void ajSeqoutWriteSet (AjPSeqout seqout, const AjPSeqset seq);
```



> **注意**
> AjPSeq 对象用于从 seqall 对象写入序列。

## 6.7.6.5.1 写入序列

```
AjPSeq seq = NULL;
AjPSeqout seqout = NULL;
seq = ajAcdGetSeq("sequence");
seqout = ajAcdGetSeqout("outseq");
ajSeqoutWriteSeq(seqout, seq);
```

## 6.7.6.5.2 顺序写入序列

通常使用 ajSeqallNext 循环遍历序列并获取下一序列的指针（本例中为 seqPtr）以供写入：

```
AjPSeqall seqall = NULL;
AjPSeqout seqout = NULL;
AjPSeq seqPtr = NULL;
seqall = ajAcdGetSeqall("sequence");
seqout = ajAcdGetSeqout("outseq");
while(ajSeqallNext(seqall, &seqPtr))
{
    ajSeqoutWriteSeq(seqout, seqPtr);
}
```

## 6.7.6.5.3 写入序列集

此处将整个序列集写入文件：

```
AjPSeqset seqset = NULL;
AjPSeqout seqout = NULL;
seqset = ajAcdGetSeqset("sequence");
seqout = ajAcdGetSeqout("outseq");
ajSeqoutWriteSet(seqout, seqset);
```

## 6.7.6.5.4 写入多个序列集

多个序列集必须逐个写入。使用数组表示法访问各个集合：

```
AjPSeqset *seqset = NULL;
AjPSeqout seqout = NULL;
ajint i = 0;
seqset = ajAcdGetSeqsetall("sequence");
seqout = ajAcdGetSeqout("outseq");
for(i=0; seqset[i] != NULL; i++)
    ajSeqoutWriteSet(seqout, seqset[i]);
```

## 6.7.6.6 内存和文件管理

程序结束时，关闭所有文件并释放内存是您的责任。

### 6.7.6.6.1 关闭输出序列文件

要关闭输出序列流，请使用 `ajSeqoutClose`:

```
AjPSeqout seqout = NULL;
seqout = ajAcdGetSeqout("outseq");
...
ajSeqoutClose(seqout);
```

### 6.7.6.6.2 释放内存

必须对通过 `ajAcdGet*` 调用返回的任何序列对象调用默认析构函数（见下文）。

## 6.7.7 序列对象内存管理

### 6.7.7.1 默认对象构造

要使用未在 ACD 文件中定义的序列对象，必须先实例化相应的对象指针。为每种访问方法提供了三个默认构造函数：

```
AjPSeq ajSeqNew (void); /* Sequence */
AjPSeqset ajSeqsetNew (void); /* Sequence set */
AjPSeqall ajSeqallNew (void); /* Sequence stream */
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的编程习惯：

```
AjPSeq seq = NULL;
AjPSeqset seqset = NULL;
AjPSeqall seqall = NULL;

seq = ajSeqNew();
seqset = ajSeqsetNew();
seqall = ajSeqallNew();

/* The objects are instantiated and ready for use */
```

序列输出对象通常从 ACD 文件处理中加载（见上文）。在极少需要手动创建序列输出对象的情况下，可以使用默认的 seqout 对象构造函数：

```
AjPSeqout   seqout = NULL;

seqout = ajSeqoutNew();

/* The object is instantiated and ready for use */
```

### 6.7.7.2 默认对象销毁

为每种访问方法提供了序列对象销毁函数，并为序列集数组提供了一个：

```
void ajSeqDel (AjPSeq* Pseq);
void ajSeqallDel (AjPSeqall *Pseq);
void ajSeqsetDel (AjPSeqset *Pseq);
void ajSeqsetDelarray (AjPSeqset **PPseq);
```

用法如下：

```
AjPSeq seq = NULL;
AjPSeqall seqall = NULL;
AjPSeqset seqset = NULL;
AjPSeqset *seqsets = NULL;

seq   = ajAcdGetSeq("asequence");
seqall = ajAcdGetSeqall("bsequence");
seqset = ajAcdGetSeqset("csequence");
seqsets = ajAcdGetSeqsetall("dsequence");

...

ajSeqDel(&seq);
ajSeqallDel(&seqall);
ajSeqsetDel(&seqset);
ajSeqsetDelarray(&seqsets);
```

使用完对象后，必须释放其内存。提供了析构函数：

```
void   ajSeqDel   (AjPSeq* Pseq);   /* Sequence   */
void   ajSeqallDel (AjPSeqall *Pseq); /* Sequence stream */
void   ajSeqsetDel (AjPSeqset *Pseq); /* Sequence set   */
```

为方便起见，还提供了 seqset 对象数组的析构函数：

```
/* Destroy an array of sequence set objects and the array. */
void ajSeqsetDelarray (AjPSeqset **PPseq);
```

```
AjPSeq        seq = NULL;
AjPSeqset seqset = NULL;
AjPSeqall seqall = NULL;

seq        = ajSeqNew();
seqset = ajSeqsetNew();
seqall = ajSeqallNew();

/* Do something with the instantiated objects */

ajSeqDel(&seq);
ajSeqsetDel(&seqset);
ajSeqallDel(&seqall);

/* The memory is freed and the pointers reset to NULL, ready for re-use. */

seq        = ajSeqNew();
seqset = ajSeqsetNew();
seqall = ajSeqallNew();

/* Do something else with the new objects. The pointer variable is reallocated. */

ajSeqDel(&seq);
ajSeqsetDel(&seqset);
ajSeqallDel(&seqall);

/* Done with the objects so the memory is freed. */
```

同样，对于序列集数组：

```
AjPSeqset *seqset = NULL;
seqset = ajAcdGetSeqsetall("sequence");

/* Do something with the sequence set array */

ajSeqsetDelarray(&seqset);
```

### 6.7.7.3 替代对象构造和加载

在管理序列对象内存时，需要了解函数的行为。有三种情况需要区分：

- 函数需要一个预先存在的对象。
- 函数可以使用但不需要预先存在的对象，必要时会分配一个。
- 函数始终分配一个对象，并返回指向它的指针，或分配一个对象指针，其地址作为参数传递。

### 6.7.7.3.1 单个序列

创建序列对象有多种替代方法。要创建带有保留大小的序列，请使用：

```
AjPSeq ajSeqNewRes (size_t size);
```

可以从字符串创建序列，同时提供序列名称。创建序列时使用了其他字符串，因此稍后需要释放三个对象：

```
AjPSeq seq   = NULL;
AjPStr str   = NULL;
AjPStr strname = NULL;

str   = ajStrNewC("ASEQUENCE");
strname = ajStrNewC("Sequence Name");

seq = ajSeqNewNameS(str, strname);

/* Do something with sequence */

ajStrDel(&str);
ajStrDel(&strname);
ajSeqDel(&seq);
```

或者从定义了起始和结束区域（以偏移量给出）的字符串创建。字符串会被复制到序列对象中，并将序列修剪到定义的区域：

```
AjPSeq seq = NULL;
AjPStr str = NULL;
ajint offsetstart = 1;
ajint offend   = 8;

str = ajStrNewC("ASEQUENCE");

seq = ajSeqNewRangeS(str, offsetstart, offend, ajFalse);

ajStrDel(&str);
ajSeqDel(&seq);
```

上面的 ajSeqNewRangeS 调用将创建子序列“SEQUENCE”。最后一个函数参数是布尔值，如果设置为 true，则指定的偏移量值会被反转，并且打印时序列会被设置为反转。如果您这样调用该函数：

```
seq= ajSeqNewRangeS(str, offsetstart, offend, ajTrue);
```

则序列的起始设置为 offend（8），结束设置为 offsetstart（1），打印的（反转）序列将为 ECNEUQES：

```
seq= ajSeqNewRangeS(str, offsetstart, offend, 1);
```

也可以通过调用 ajSeqNewSeq 从现有序列创建并初始化序列，该函数会复制原始序列，因此稍后需要销毁两个对象：

```
AjPSeq seq   = NULL;
AjPSeq seqCopy = NULL;
seq = ajAcdGetSeq("sequence");
seqCopy = ajSeqNewSeq(seq);
/* Do something with the sequences */
ajSeqDel(&seq);
ajSeqDel(&seqCopy);
```

可以使用 ajSeqsetGetSeqarray 从现有序列集创建序列数组。将创建数组并获取序列的副本。将来该函数会被重命名，以反映它是构造函数的事实。为确保释放所有内存，会调用 ajSeqsetGetSize 来获取数组大小，并通过调用 AJFREE 释放数组本身：

```
AjPSeqset seqset = NULL;
AjPSeq * seqs = NULL;
ajint nseq; /*Number of sequences in set */
ajint x;

seqset=ajAcdGetSeqset("sequences");

seqs = ajSeqsetGetSeqarray(seqset);

/* Do something with the array of sequences */

ajSeqsetDel(&seqset);
nseq = ajSeqsetGetSize(seqset);

for(x=0; x<nseq; x++)
    ajSeqDel(&seqs[x]);

AJFREE(seqs);
```

### 6.7.7.3.2 序列集

提供了三个函数用于向预先存在的 AjPSeqset 对象加载序列。
可以使用 ajSeqsetFromPair 从一对序列（在此例中来自 ACD 文件处理）构建序列集。这会复制序列：

```
AjPSeq seqa = NULL;
AjPSeq seqb = NULL;
AjPSeqset seqset = NULL;
ajint nset = 0; /* Number of sequences in set */

seqa = ajAcdGetSeq("asequence");
seqb = ajAcdGetSeq("bsequence");

seqset = ajSeqsetNew();
nset = ajSeqsetFromPair(seqset, seqa, seqb);

/* Do something with set */

ajSeqDel(&seqa);
ajSeqDel(&seqb);
ajSeqsetDel(&seqset);
```





或者通过使用 ajSeqsetFromList 从序列列表中创建，与 ajSeqsetFromPair 不同，它将实际序列（而非副本）加载到集合中。因此，你必须小心不要尝试释放同一个对象两次。ajListFree 用于删除列表，但不删除节点（序列）。后者由 ajSeqsetDel 删除：

```
AjPSeq    seqa = NULL;
AjPSeq    seqb = NULL;
AjPList   list = NULL;
AjPSeqset seqset = NULL;
ajint     nset = 0; /* Number of sequences in set */

seqa = ajAcdGetSeq("asequence");
seqb = ajAcdGetSeq("bsequence");

/* Build list of sequences */
list = ajListNew();
ajListPush(list, (void *)seqa);
ajListPush(list, (void *)seqb);

seqset = ajSeqsetNew();
nset   = ajSeqsetFromList(seqset, list);

/* Do something with set */

ajSeqsetDel(&seqset);
ajListFree(&list);
```

你可以使用 ajSeqsetApp 将序列追加到序列集中，该函数会复制序列：

```
AjPSeq    seqa = NULL;
AjPSeq    seqb = NULL;
AjPSeqset seqset = NULL;
ajint     nset = 0; /* Number of sequences in set */

seqa = ajAcdGetSeq("asequence");
seqb = ajAcdGetSeq("bsequence");

seqset = ajSeqsetNew();
ajSeqsetApp(seqset, seqa);
ajSeqsetApp(seqset, seqb);

/* Do something with set */

ajSeqDel(&seqa);
ajSeqDel(&seqb);
ajSeqsetDel(&seqset);
```

## 6.7.7.3.3 序列输出

输出序列对象可以从已打开的文件创建。在这种情况下，ACD 文件处理期间不会创建输出文件。该文件由函数接管，因此只需调用一个析构函数：

```
AjPFile file = NULL;
AjPSeqout seqout = NULL;

/* Open a file called "InputFileName" */
file = ajFileNewInNameC ("InputFileName");

/* Create an output sequence object that uses this file */
seqout = ajSeqoutNewFile(file);

/* Do something with the output sequence object */
ajSeqoutDel(&seqout);
```

可以使用 ajSeqoutOpenFilename 加载现有的输出序列对象（并打开文件用于写入），给定有效文件名时，如果文件成功打开，则返回布尔值 ajTrue：

```
AjPSeqout seqout = NULL;
AjPStr name = NULL;

/* Create an empty seqout object */
seqout = ajSeqoutNew();

ajStrAssignC(&name, "InputFileName");

if(!ajSeqoutOpenFilename(seqout, name))
    /* Error handling */;

/* Do something with the output sequence object */
ajSeqoutDel(&seqout);
```

## 6.7.7.3.4 使用 USA 加载序列对象

提供了函数，可根据输入或输出序列（或序列流）的 USA（参见 EMBOSS 用户指南），将一个或多个序列加载到序列输入对象中，或初始化输出序列对象。

### 单个序列

可以使用 ajSeqGetFromUsa 将序列加载到序列对象中。如果序列是蛋白质，则第二个参数为 true，如果序列加载成功，则函数返回 ajTrue：

```
AjPSeq seq = NULL;
AjPStr usa = NULL;

usa = ajStrNewC("asis::ALVLLYNITEF"); /* "asis::ALVLLYNITEF" is a valid USA */
seq = ajSeqNew(); /* Create sequence object */

if(!ajSeqGetFromUsa(usa, 1, &seq))
    /* Do something to handle the failure */;

else
    /* Sequence was loaded successfully .. do something with it */;

ajSeqDel(&seq);
```

### 序列集

可以使用 ajSeqsetGetFromUsa 以与 ajSeqGetFromUsa 相同的方式创建序列集：

```
AjPSeqset seqset = NULL;
AjPStr usa = NULL;
seqset = ajSeqsetNew(); /* Create sequence object */

usa = ajStrNewC("swiss:hba_*"); /* "swiss:hba_*" is a valid USA */

if(!ajSeqsetGetFromUsa(usa, 1, &seqset))
    /* Do something to handle the failure */;
else
    /* Sequence set was loaded successfully .. do something with it */;

ajSeqsetDel(&seqset);
```

### 序列流

可以使用 ajSeqallFile 从 USA 创建序列输入流，与前两个函数不同，它返回指向新对象的指针。

```
AjPSeqall seqall = NULL;
AjPStr usa = NULL;

usa = ajStrNewC("swiss:hba_*"); /* "swiss:hba_*" is a valid USA */

if(!(seqall=ajSeqallFile(usa)))
    /* Do something to handle the failure */;
else
    /* Sequence input stream was opened successfully .. do something with it */;

ajSeqallDel(&seqall);
```

### 序列输出

ajSeqoutClearUsa 使用新的 USA 创建（如有必要）或重置序列输出对象：

```
AjPSeqout seqout = NULL;
AjPStr usa = NULL;

usa = ajStrNewC("asis:ALVLLYNITEF"); /* "asis:ALVLLYNITEF" is a valid USA */

seqout = ajSeqoutNew();
ajSeqoutClearUsa(&seqout, usa);

ajSeqoutDel(&seqout);
```

如果省略对构造函数的调用，代码同样可以正常工作。

## 6.7.8 获取和设置元素

AJAX 提供了函数，用于获取或设置基本序列对象中的元素（数据字段）。

### 6.7.8.1 设置单个值

用于向现有序列对象的一个元素赋值的函数具有前缀 ajSeqAssign。

在以下示例中，ajSeqAssignDescC 和 ajSeqAssignNameS 用于为输入序列的一个区域（由 -sbegin 和 -send 值用户定义）分配名称和描述：

```
AjPSeq      seq = NULL;
AjPSeq seqsub = NULL;

seq      = ajAcdGetSeq("sequence");
seqsub   = ajSeqNewSeq(seq);

ajSeqTrim(seqsub);
ajSeqAssignNameC(seqsub, "Subsequence");
ajSeqAssignDescC(seqsub, "Subsequence defined by 'sbegin and send values.'");
ajSeqAssignAccC(seqsub, "YZ456789");
```

其他序列对象元素也有赋值函数：

```
ajSeqAssignEntryC    /* entry name */
ajSeqAssignFileC     /* file name */
ajSeqAssignFullC     /* full sequence name */
ajSeqAssignGiC       /* NCBI GI number */
ajSeqAssignSeqC      /* sequence as a string */
ajSeqAssignSvC       /* EMBL sequence version */
ajSeqAssignUfoC      /* uniform feature object string for feature input */
ajSeqAssignUsaC      /* sequence input uniform sequence address */
```

### 6.7.8.2 其他赋值函数

ajSeqSet* 家族函数用于设置其他序列属性（而非单个元素）。例如，ajSeqSetRange 设置序列对象的范围，在此情况下设置为前 10 个残基：

```
AjPSeq seq=NULL;
ajint start=0;
ajint end=9;

seq = ajSeqNew();

...

ajSeqSetRange(seq, start, end);
```

其他序列对象元素也有设置函数：ajSeqSetOffsets（设置起始偏移量和完整长度以定义末尾偏移量），ajSeqSetRangeRev（设置如上范围并将序列设置为反向），ajSeqSetUnique（使序列唯一，以便在没有副作用的情况下修改序列字符）

'Set' 函数也可用于其他数据类型：

```
AjPSeqset seqset=NULL;
AjPSeqall seqall=NULL;
ajint start = 0;
ajint end = 9;

seqset = ajSeqsetNew();
seqall = ajSeqallNew();

...

ajSeqsetSetRange(seqset, start, end);
ajSeqallSetRange(seqall, start, end);
```

这些是序列流和序列集级别唯一有用的函数。其他属性使用序列 'Set' 或 'Assign' 函数为流或集中的每个单独序列设置。

### 6.7.8.3 获取单个值

ajSeqGet* 家族函数用于返回序列对象的内容。这些函数返回对象实际内容的指针，因此调用者必须小心不要以任何方式意外更改返回的值。这里使用了两种函数。ajSeqGetDescC 返回序列描述，而 ajSeqGetNameS 返回序列名称。后缀 S 用于返回 EMBOSS 字符串的情况，而 C 表示返回 C 类型（char *）字符串：

```
AjPSeq seq     = NULL;
AjPStr str     = NULL;
AjPStr strcopy = NULL;
char * strc    = NULL;

seq = ajAcdGetSeq("sequence");

strc = ajSeqGetDescC(seq);
str  = ajSeqGetNameS(seq);

/* Do something (but don't change) the returned strings */

ajStrAssignS(&strcopy, str);

/* Copy of string is now safe to change ... do something with it */

ajSeqDel(&seq);
ajStrDel(&str);
```

可以使用此方式检索所有常见序列属性，例如使用以下函数获取 accession 和 GI 编号：

```
const AjPStr ajSeqGetGiS (const AjPSeq seq)
const AjPStr ajSeqGetAccS (const AjPSeq seq) ;
```

序列本身使用以下函数之一检索：

```
const char* ajSeqGetSeqC (const AjPSeq seq) ;
const AjPStr ajSeqGetSeqS (const AjPSeq seq) ;
```

函数 ajSeqGetOffset 将返回用户指定的 -sbegin 值，即序列起始处的偏移量。ajSeqGetOffend 将返回根据序列长度和 -send 值定义的、需要从末尾移除的位置数：

```
AjPSeq seq = NULL;
ajint offset;
ajint offend;

seq = ajAcdGetSeq("sequence");

offset = ajSeqGetOffset(seq);
offend = ajSeqGetOffend(seq);

/* Do something here using offset and offend, perhaps code to
retain the trimmed regions. */

ajSeqTrim(seq);
```

'Get' 函数也可用于其他数据类型。例如，要获取序列集的序列数量和范围，或序列输入流的文件名和 USA：

```
AjPSeq     seqset = NULL;
AjPSeqall  seqall = NULL;
ajint      start;
ajint      end;
ajint      nseq;
AjPStr     name = NULL;
AjPStr     usa = NULL;

seqset = ajAcdGetSeqset("sequence");
seqall = ajAcdGetSeqall("sequences");

nseq = ajSeqsetGetSize(seqset);
ajSeqsetGetRange(seqset, &start, &end);

name = ajSeqallGetFilename(seqall);
usa = ajSeqallGetUsa(seqall);
```



存在返回集合中序列属性的‘Get’函数。这些函数的前缀为 ajSeqsetGetseq。需要指定所需序列的编号。例如，提供了三个函数来返回集合中给定的序列，可以作为序列对象指针、EMBOSS 字符串或 C 类型（char *）字符串。同样，应注意不要无意中以任何方式更改对象数据：

```
AjPSeq seqset = NULL;

AjPSeq seqPtr;
AjPStr seqS;
char * seqC;

seqset = ajAcdGetSeqset( "sequence" );

/* First sequence in call cases */
seqPtr = ajSeqsetGetseqSeq ( seqset, 1 );
seqS = ajSeqsetGetseqSeqS ( seqset, 1 );
seqC = ajSeqsetGetseqSeqC ( seqset, 1 );
```

返回流中序列属性的函数前缀为 ajSeqallGetseq，并返回流中*当前*序列的属性。例如，要获取当前序列的名称和长度：

```
AjPSeq seqall = NULL;
AjPStr name=NULL;
ajint len;

seqall = ajAcdGetSeqall( "sequences" );

name = ajSeqallGetseqName ( seqall );
len = ajSeqallGetseqLen(seqall);
```

## 6.7.9 测试序列属性

可以测试序列属性，例如序列是蛋白质还是核苷酸。此类函数返回 AjBool：

```
AjPSeq seq = NULL;
AjPSeqset seqset = NULL;

seq = ajAcdGetSeq( "sequence" );
seqset = ajAcdGetSeq( "sequences" );

if( ajSeqIsProt( seq ) )
    /* Protein sequence */;
else if( ajSeqIsNuc( seq ) )
    /* Nucleotide sequence */;
else
    /* Error handling */;

if( ajSeqsetIsNuc( seqset )
{
    if(ajSeqsetIsRna (seqset)
    /* Do something. */;
}
else if(ajSeqsetIsNuc(seqset)
{
    /* Do something else */
}
```

然而，此类测试很少需要，因为序列类型可以在 ACD 文件级别强制执行。

## 6.7.10 计算序列属性

可以计算序列的各种属性。例如，ajSeqCalcCount 将核苷酸序列中 A、C、G 和 T 核苷酸的数量写入数组，而 ajSeqCalcMolwt 计算蛋白质序列的分子量：

```
AjPSeq seq = NULL;
ajint nbases[5];
float molwt;

seq = ajAcdGetSeq("sequence");

if(ajSeqIsNuc(seq))
    ajSeqCalcCount(seq, *nbases);
else if(ajSeqIsProt(seq))
    molwt = ajSeqCalcMolwt(seq);
```

> **注意**
>
> 请注意，序列的各种计算属性（第 A.6 节，‘计算属性’），例如长度和类型，可在 ACD 文件级别使用。

## 6.7.11 序列字符串函数

有两个函数可将序列复制到字符串中，目标可以是 EMBOSS 字符串或 C 类型（char *）字符串：

```
char* ajSeqGetSeqCopyC (const AjPSeq seq) ;
AjPStr ajSeqGetSeqCopyS (const AjPSeq seq) ;
```

有几个函数用于处理使用 AjPStr 对象作为字符串保存的序列。这些函数的前缀为 ajSeqstr。这里首先使用 ajSeqGetSeqCopyS 将序列复制到字符串中。计算蛋白质序列的分子量，或核苷酸序列的反向互补：

```
AjPSeq seq = NULL;
AjPStr str = NULL;
float molwt;

seq = ajAcdGetSeq("sequence");
str = ajSeqGetSeqCopyS(seq);

if(ajSeqIsNuc(seq))
    ajSeqstrReverse(&str);
else if(ajSeqIsProt(seq))
    molwt = ajSeqCalcMolwt(str);
```

## 6.7.12 处理序列

提供了各种用于处理序列的函数。您已经接触过 ajSeqTrim 和 ajSeqsetTrim，用于将序列修剪到其起始和结束区域，但也可以进行其他操作。例如，可以使用以下函数处理间隙字符：

```
void ajSeqGapFill (AjPSeq seq, ajuint len);
void ajSeqGapStandard(AjPSeq seq, char gapchar);
void ajSeqGapLen (AjPSeq thys, char gapc, char padc, ajuint ilen);
```

ajSeqGapFill 将间隙字符追加到序列，直到达到指定的最大序列长度。ajSeqGapStandard 使字符串中的所有间隙都使用提供的标准间隙字符。字符串中的任何破折号、波浪号、句号、问号或空格字符（- . ? ）都会被转换。ajSeqGapLen 将任何非序列字符设置为有效的间隙字符，并在必要时用额外的间隙填充到指定长度。

要计算序列中的间隙数（计算任何可能的间隙字符），请调用 ajSeqCountGaps：

```
ajuint ajSeqCountGaps (const AjPSeq seq);
```

如果尚未从 ACD 或命令行处理中完成，则可用函数对核苷酸序列进行互补，或反向互补：

```
void ajSeqComplement (AjPSeq seq);
void ajSeqReverseDo (AjPSeq seq);
```

有几个函数可将序列或集合中所有序列转换为小写或大写：

```
void ajSeqsetFmtLower (AjPSeqset seq);
void ajSeqsetFmtUpper (AjPSeqset seq);
void ajSeqFmtLower (AjPSeq thys);
void ajSeqFmtUpper (AjPSeq thys);
```

ajSeqsetFill 可用于通过在任何短序列的末尾放置间隙来填充序列集：

```
ajint ajSeqsetFill(AjPSeqset seq);
```

## 6.7.13 序列类型验证

在大多数情况下，序列类型的验证（参见第 A.7 节，‘序列类型’），例如序列是用于蛋白质还是核酸，是否包含间隙等，是在 ACD 文件级别处理的。这意味着应用程序始终接收（通过调用 ajAcdGet*）与 ACD 文件中指定的精确类型相符的序列。

AJAX 中提供了几个函数用于直接处理序列类型。可以通过调用 ajSeqType 自动设置序列的类型，即从序列本身确定。否则，可以使用以下函数直接为序列或序列集设置为核苷酸或蛋白质之一：

```
void ajSeqType (AjPSeq thys);
void ajSeqSetNuc (AjPSeq thys);
void ajSeqSetProt (AjPSeq thys);
void ajSeqsetSetNuc (AjPSeqset thys);
void ajSeqsetSetProt (AjPSeqset thys);
```

## 6.7.14 序列转换

有时有必要将序列转换为数值形式以便于处理。AJAX 用于此目的的数据类型是：

- AjPSeqCvt 用于将序列转换为数值形式

常见用例是为评分矩阵生成序列字符转换表，例如氨基酸替换评分矩阵（参见第 6.10 节，‘处理比较矩阵’）。

## 6.7.15 处理序列翻译

将遗传序列翻译为蛋白质是一项常见任务，并在其他地方介绍（第 6.8 节，‘处理序列翻译’）。

## 6.7.16 处理 IUB 碱基代码

EMBOSS 支持下面所示的官方 IUB 碱基代码，还支持 X 表示未知碱基。

### 6.7.16.1 无歧义代码

无歧义碱基代码为：

- A（腺嘌呤）
- C（胞嘧啶）
- G（鸟嘌呤）
- T（胸腺嘧啶）或 U（尿嘧啶）

### 6.7.16.2 歧义代码

两种碱基之一：

- M（A 或 C）
- R（A 或 G）
- W（A 或 T/U）
- S（C 或 G）
- Y（C 或 T/U）
- K（G 或 T/U）

三种碱基之一：

- B（C、G 或 T/U）
- D（A、G 或 T/U）
- H（A、C 或 T/U）
- V（A、C 或 G）

四种碱基之一：

- N（A、C、G 或 T/U）

未知（或非标准）碱基：

- X（不是 A、C、G 或 T/U）

### 6.7.16.3 处理 IUB 碱基代码

标准 IUB 碱基代码有四种可能性，可以表示为 4 位二进制，以便快速比较，包括测试歧义代码。提供了用于碱基代码字符和二进制表示的函数。

歧义代码及其数值表示从本地数据文件 Ebases.iub 中读取。

```
/* Sets up binary OR representation of all IUB bases in
a table aj_base_table where A=1,
C=2, G=4 and T=8. Also sets up a match probability array aj_base_prob holding the
probability of one IUB base matching any other. Uses the Ebases.iub file. Is
initialised if necessary from other AJAX functions. *\/
/* Complements a nucleotide base. *\/
char ajBaseAlphacharComp(char base);
/* Returns an element of the base match probability array *\/
float ajBaseAlphaCompare(ajint base1, ajint base2);
```

要清理用于序列碱基处理内部维护的内存，请调用 ajBaseExit：

```
void ajBaseExit (void);
```

这由 embExit 自动调用。

### 6.7.16.4 碱基和氨基酸代码的转换

用于将碱基代码的整数表示转换为其他形式的函数：

```
/* Convert to string of matching base code(s). *\/
const AjPStr ajBaseGetCodes (ajint ibase);
/* Convert to base code: 0 to 'A', 1 to 'B' ... 25 to 'Z'. Returns an integer. *\/
ajint ajBasecodeFromInt (ajint n);
```

要将碱基代码转换为其他形式：

```
/*Convert to integer: 'A' to 0, 'B' to 1, ... 'Z' to 25. Returns an integer.*\/
ajint ajBasecodeToInt (ajint c);
/* Convert to binary OR representation of an IUB base. *\/
ajint ajBaseAlphaToBin (ajint c);
/* Convert to binary OR representation of an IUB base. *\/
char ajBaseAlphacharToBin (char c);
```

ajBaseAlphaToBin 和 ajBaseAlphacharToBin 返回 IUB 碱基的二进制 OR 表示，其中 A = 1、C = 2、G = 4 和 T = 8。这些函数使用内部碱基表。

要将 IUB 碱基的二进制 OR 表示转换为其他形式：

```
/* Converts a binary OR representation of an IUB base to an ambiguous DNA base code. *\/
char ajBaseBinToAlpha (ajint c);
```

ajBaseBinToAlpha 将 IUB 碱基的二进制 OR 表示（其中 A = 1、C = 2、G = 4 和 T = 8）转换为歧义 DNA 碱基代码（使用 T 而不是 U）。它使用内部碱基表。

要在单字母和三字母氨基酸代码之间相互转换：



/* Convert single letter to three letter amino acid code. */
AJBool ajResidueToTriplet (char c, AjPStr *Paa3);

/* Convert three letter to single letter amino acid code. */
AJBool ajResidueFromTriplet (char *aa3, char *Pc);

### 6.7.17 DNA 计算

ajdan.h/c 中提供了各种用于计算核苷酸序列属性的函数。这些函数使用 DNA 熔解对象（AjPMelt），但这对应用程序员是透明的，您永远不需要直接实例化或使用该对象：

| 对象 | 描述 |
|---|---|
| AjPMelt | 用于 DNA 熔解 |

### 6.7.17.1 DNA 熔解的通用函数

AjPMeltInit 和 AjPMeltExit 函数在内部用于初始化和清理内存。无需直接调用它们。AjPMeltGC 函数是一个用于计算 G+C 含量的实用工具：

```
/* Initialises melt entropies, enthalpies and energies. Different data files are
read for DNA or RNA heteroduplex. Also sets optional flag for array saving of the
above. */
void ajMeltInit (AJBool isDNA, ajint savesize);

/* Cleans up DNA melting processing internal memory */
void ajMeltExit (void);

/* Calculates GC fraction of a sequence allowing for ambiguity */
float ajMeltGC (const AjPStr strand, ajint len);
```

### 6.7.17.2 计算 DNA 熔解和退火温度及能量

AjPMeltEnergy 计算序列字符串的熔解能和焓/熵。AjPMeltEnergy2 是一个替代接口，它初始化一组“保存”数组，通过仅检查序列一次来使后续调用更高效。AjPMeltTemp 计算寡核苷酸的熔解温度，并有一个使用“保存”数组以提高效率的 AjPMeltTempSave 版本。AjPMeltTempProd 在给定盐浓度下计算寡核苷酸产物的熔解温度。AjPMeltTemp 在给定各自的熔解温度时，计算产物和引物的退火温度。

```
/* Calculate melt energy and enthalpy/entropy for a sequence */
float ajMeltEnergy(const AjPStr strand, ajint len,
                ajint shift, AJBool isDNA,
                AJBool maySave, float *enthalpy, float *entropy);

/* Calculate melt energy for programs like prima */
float ajMeltEnergy2(const char *strand, ajint pos, ajint len,
AJBool isDNA,
float *enthalpy, float *entropy,
float **saveentr, float **saveenth, float **saveener);

/* Calculate melt temperature of DNA or RNA */
float ajMeltTemp (const AjPStr strand, ajint len, ajint shift, float saltconc,
float DNAconc, AJBool isDNA);

/* Calculate melt temperature of DNA or RNA */
float ajMeltTempSave(const char *strand, ajint pos,
ajint len, float saltconc,
float DNAconc, AJBool isDNA,
float **saveentr, float **saveenth, float **saveener);

/* Calculate product melt temperature of DNA */
float ajMeltTempProd (float gc, float saltconc, ajint len);

/* Calculate annealing temperature of product and primer */
float ajAnneal (float tmprimer, float tmproduct);
```

## 6.8 处理序列翻译

### 6.8.1 简介

将核苷酸序列翻译成蛋白质序列是一项常见任务。AJAX 提供了您所期望的所有基本功能。核苷酸序列可以采用多种形式（AJAX 字符串 (AjPStr)、C 类型字符串 (char *) 或 AJAX 序列对象 (AjPSeq)），并可以在所有阅读框中进行翻译。序列的反向互补链也可以被翻译。

### 6.8.2 AJAX 库文件

用于处理序列翻译的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajtranslate | 序列翻译 |

ajtranslate.h/c。定义序列翻译对象 (AjPTrn) 并包含用于处理序列翻译的函数。

### 6.8.3 ACD 数据类型

没有专门用于处理翻译的 ACD 数据类型。此类操作在核苷酸序列上执行，因此需要适当类型的序列输入。还需要遗传代码，其选择通常通过由 list ACD 数据类型实现的菜单提供给用户。因此，您需要的 ACD 数据类型如下：

| 数据类型 | 描述 |
|---|---|
| list | 带有文本标签的选项列表（文本描述）。用户会看到一个有限的选项列表，可从中进行选择。选项可以由任意文本标签标记。 |
| sequence | 单个输入序列。 |

注意 有关菜单和序列处理的一般信息，请参见：第 6.19 节（'处理菜单'）和第 6.7 节（'处理序列'）。

### 6.8.4 ACD 数据定义

单个序列输入的典型 ACD 定义如下：

```
sequence: sequence
[
    parameter: "Y"
    type: "nucleotide"
]
```

可用的遗传代码必须在 ACD 文件中定义，并可为此使用 list 数据类型。EMBOSS 支持一组标准遗传代码，如下所示：

```
list: table
[
    additional: "Y"
    default: "0"
    minimum: "1"
    maximum: "1"
    header: "Genetic codes"
    values: "0:Standard; 1:Standard (with alternative initiation codons); 2:Vertebrate Mitochondrial; 3:Yeast Mitochondrial;
    4:Mold, Protozoan, Coelenterate Mitochondrial and
    Mycoplasma/Spiroplasma; 5:Invertebrate Mitochondrial; 6:Ciliate
    Macronuclear and Dasycladacean; 9:Echinoderm Mitochondrial;
    10:Euplotid Nuclear; 11:Bacterial; 12:Alternative Yeast Nuclear;
    13:Ascidian Mitochondrial; 14:Flatworm Mitochondrial;
    15:Blepharisma Macronuclear; 16:Chlorophycean Mitochondrial;
    21:Trematode Mitochondrial; 22:Scenedesmus obliquus;
    23:Thraustochytrium Mitochondrial"
    delimiter: ";"
    codedelimiter: ":"
    information: "Code to use"
]
```

代码的顺序目前很重要；列表必须按上述确切顺序给出。

### 6.8.5 AJAX 数据类型

为处理需要序列和菜单输入的序列翻译，请使用：

- AjPTrn 用于序列翻译
- AjPSeq 单个输入序列（用于 sequence ACD 数据类型）
- AjPStr 来自菜单的单个选择（用于 list ACD 数据类型）

### 6.8.6 ACD 文件处理

下表显示了通过 ACD 文件处理翻译的数据类型和函数。这里从列表中检索单个选择，但也可以使用其他类型的菜单、输入序列或访问方法。

| 标题 | 读取序列 | 从列表读取单个选择 |
|---|---|---|
| ACD 数据类型 | sequence | list |
| 对象 | AjPSeq | AjPStr |
| 从 ACD 检索 | ajAcdGetSeq | ajAcdGetListSingle |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节（'处理 ACD 文件'））。ACD 文件中的所有值都读入内存。您可以通过 ajAcdGet* 函数系列来控制内存，该系列函数返回指向相应对象的指针。

### 6.8.6.1 序列或菜单选择检索

要检索序列或菜单选择对象指针，需先声明指针，然后使用相应的 ajAcdGet* 函数进行初始化。

### 6.8.6.1.1 输入序列

要检索输入序列：

```
AjPSeq seq=NULL;
seq = ajAcdGetSeq("sequence");
```

### 6.8.6.1.2 菜单选择

从遗传代码列表中选择的选项需要作为整数。

ajAcdGetListSingle 将选择作为字符串返回，其初始部分使用 ajStrToInt 转换为整数。此整数传递给 ajTrnNewI 以创建翻译表对象。这就是为什么 ACD 文件中的列表顺序很重要！您还必须声明翻译对象指针：

```
AjPTrn trnTable = NULL; /* Translation object pointer */
AjPStr gcode = NULL; /* Genetic code (selection from list) */
ajint n = 0; /* Selection */
gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode, &n);
trnTable = ajTrnNewI(n);
```

### 6.8.6.2 内存管理

在程序结束时释放内存是您的责任。必须为用于 ACD 数据定义的翻译、序列和字符串对象调用默认析构函数：

```
/* Deletes a translation table object */
void ajTrnDel(AjPTrn* pthis);
/* Delete a string object. */
void ajStrDel (AjPStr *Pstr);
/* Delete a sequence object. */
void ajSeqDel (AjPSeq* Pseq);
```

函数 ajTrnExit 在退出时自动调用，以清理翻译处理内部管家所用的内存：

```
void ajTrnExit(void);
```

### 6.8.7 翻译对象内存管理

### 6.8.7.1 默认对象构造

要使用翻译对象，必须首先实例化相应的对象指针。提供了默认构造函数。它们将从 EMBOSS 数据搜索目录（参见 EMBOSS 用户指南）中读取名为 EGC.n 的翻译数据文件，其中 n 是要使用的遗传代码编号。此编号可以显式提供给 ajTrnNewI。或者，可以通过调用 ajTrnNew 或 ajTrnNewC 按文件名打开文件：

```
/* Reads EGC.trnFileNameInt where trnFileNameInt is supplied as a parameter. */
AjPTrn ajTrnNewI (ajint trnFileNameInt);
/* Reads trnFileName. */
AjPTrn ajTrnNew (const AjPStr trnFileName);
/* Reads trnFileName. */
AjPTrn ajTrnNewC (const char *trnFileName);
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的实践：



```
AjPStr gcode = NULL;
AjPTrn trnTable = NULL;
ajint n = 0;

gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode,&n);

trnTable = ajTrnNewI(n);
/* The object is instantiated and ready for use */
```

或者：

```
AjPStr name = NULL;
AjPStr gcode = NULL;
AjPTrn trnTable = NULL;
ajint n = 0;

gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode,&n);

name = ajStrNew();
ajFmtPrintS(&name, "EGC.%d", n); /* Create the string EGC.n */
trnTable = ajTrnNew(name);
/* The object is instantiated and ready for use */
```

### 6.8.7.2 默认对象销毁

对于上述示例，必须释放单个字符串和序列：

```
AjPSeq seq = NULL;
AjPStr gcode = NULL;

seq = ajAcdGetSeq("sequence");
gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode,&n);

/* Do something */

ajSeqDel(&seq);
ajStrDel(&str);
```

在指针重复使用之前以及使用完翻译对象后，必须释放其内存。提供了一个默认析构函数：

```
/* Deletes a translation table object */
void ajTrnDel(AjPTrn* pthis);
```

用法如下：

```
AjPStr gcode = NULL;
AjPTrn trnTable = NULL;
ajint n = 0;
gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode,&n);
trnTable = ajTrnNewI(n);
/* The object is instantiated and ready for use */
ajTrnDel(&trnTable);
/* The memory is freed and the pointer reset to NULL, ready for re-use. */
```

### 6.8.8 翻译

ajTrnSeqSeqOrig 创建一个肽序列，包含核苷酸序列的完整翻译，包括任何尾部的部分密码子（一个或两个碱基），这些部分密码子翻译为 X，除非前两个碱基只能定义一个氨基酸：

```
AjPSeq ajTrnSeqSeqOrig (const AjPTrn trnObj, const AjPSeq seq, ajint frame);
```

使用以下函数，可以将存储在 AJAX 字符串 (AjPStr)、C 类型字符串 (char *) 或 AJAX 序列对象 (AjPSeq) 中的核苷酸序列翻译成蛋白质：

```
void ajTrnSeqS (const AjPTrn trnObj, const AjPStr str, AjPStr *pep);
void ajTrnSeqC (const AjPTrn trnObj, const char *str, ajint len, AjPStr *pep);
void ajTrnSeqSeq (const AjPTrn trnObj, const AjPSeq seq, AjPStr *pep);
```

这些函数从第 1 读码框（从第一个碱基开始）翻译到最后一个完整的三联体密码子。如果末尾有一个或两个额外碱基，则将其忽略。

要翻译序列的反向互补，请调用：

```
void ajTrnSeqRevC (const AjPTrn trnObj, const char *str, ajint len, AjPStr *pep);
void ajTrnSeqRevS (const AjPTrn trnObj, const AjPStr str, AjPStr *pep);
void ajTrnSeqRevSeq (const AjPTrn trnObj, const AjPSeq seq, AjPStr *pep);
```

这些函数从第 -1 读码框（从最后一个碱基开始）翻译到第一个完整的三联体密码子。如果开头有一个或两个额外碱基，则将其忽略。所有函数都会将翻译结果追加到输入的肽中。

对于将第 -1 读码框定义为从反向互补序列的第一个碱基开始的读码框的人员，提供了替代翻译。要翻译序列的反向互补，请调用：

```
void ajTrnSeqAltRevC (const AjPTrn trnObj, const char *str, ajint len, AjPStr *pep);
void ajTrnSeqAltRevS (const AjPTrn trnObj, const AjPStr str, AjPStr *pep);
void ajTrnSeqAltRevSeq (const AjPTrn trnObj, const AjPSeq seq, AjPStr *pep);
```

## 6.8 处理序列翻译

这些函数从第 -4 读码框（从最后一个碱基开始）翻译到第一个完整的三联体密码子，即如果开头有一个或两个额外碱基，则将其忽略。所有函数都会将翻译结果追加到输入的肽中。

可以指定翻译读码框：

```
void ajTrnSeqFrameC (const AjPTrn trnObj, const char *seq, ajint len, ajint frame,
AjPStr *pep);
void ajTrnSeqFrameS (const AjPTrn trnObj, const AjPStr seq, ajint frame, AjPStr
*pep);
void ajTrnSeqFrameSeq (const AjPTrn trnObj, const AjPSeq seq, ajint frame, AjPStr
*pep);
AjPSeq ajTrnSeqFramePep (const AjPTrn trnObj, const AjPSeq seq, ajint frame);
```

所有函数都会将翻译结果追加到输入的肽中。相比之下，ajTrnSeqFramePep 返回一个带有新肽的 AjPSeq 对象。

这些函数在指定的读码框（必须为 1、2、3、-1、-2、-3、4、5、6、-4、-5、-6 之一）中翻译到最后一个完整的三联体密码子，即如果末尾有一个或两个额外碱基，则将其忽略。读码框 -6 到 -1 给出反向翻译，读码框 1 到 3 给出正常的前向翻译。读码框 4 到 6 先对 DNA 序列进行反向互补，然后再反转肽序列。因此，读码框 4 到 6 是反转的蛋白质序列，主要用于在原始 DNA 序列下方显示。

读码框 -1 定义为与读码框 1 中使用的密码子匹配的反向互补序列的翻译。例如，在序列 ACGT 中，读码框 1 的第一个密码子是 ACG，读码框 -1 的最后一个密码子是 ACG 的反向互补，即 CGT。

读码框 -4 定义为反向互补的翻译，从反转序列的第一个密码子开始翻译。在序列 ACGT 中，最后一个密码子是 CGT，因此读码框 -4 从 CGT 的反向互补（即 ACG）开始翻译——这是为那些在序列反向互补时将第 -1 读码框定义为使用第一个密码子的人员提供的。这也称为“替代读码框 -1”。

读码框 -5 从倒数第二个碱基开始（替代读码框 -2）。读码框 -6 从倒数第三个碱基开始（替代读码框 -3）。读码框 4 与读码框 -1 相同，5 与 -2 相同，6 与 -3 相同。

要通过尝试翻译读码框的最后一个或两个碱基来完成翻译，请调用：

```
ajint ajTrnSeqDangleC (const AjPTrn trnObj, const char *seq, ajint frame, AjPStr *pep);
ajint ajTrnSeqDangleS (const AjPTrn trnObj, const AjPStr seq, ajint frame, AjPStr *pep);
```

在这两种情况下，翻译结果都会追加到输入的肽中。

有函数可以将单个密码子翻译为单字母或三字母氨基酸代码。还提供了接受 C 类型 (char *) 字符串的替代函数，但此处未显示：

```
/* Translates a codon into a 3-letter code. */
char ajTrnCodonS (const AjPTrn trnObj, const AjPStr codon);

/* Translates the reverse complement of a codon into a 3-letter code. */
char ajTrnCodonRevS (const AjPTrn trnObj, const AjPStr codon);

/* Translates a codon into a 1-letter code. */
char ajTrnCodonC (const AjPTrn trnObj, const char *codon);

/* Translates the reverse complement of a codon into a 1-letter code. */
char ajTrnCodonRevC (const AjPTrn trnObj, const char *codon);
```

### 6.8.9 杂项函数

有几个函数用于检索翻译对象的元素：

```
AjPStr ajTrnGetTitle (const AjPTrn this);
AjPStr ajTrnGetFilename (const AjPTrn this);
```

要检查输入的密码子是起始密码子、终止密码子还是其他内容，请调用

```
ajint ajTrnCodonstrTypeC (const AjPTrn trnObj, const char *codon, char *aa);
ajint ajTrnCodonstrTypeS (const AjPTrn trnObj, const AjPStr codon, char *aa);
```

要返回给定翻译表文件名编号的遗传代码描述字符串，请调用：

```
const AjPStr ajTrnName(ajint trnFileNameInt);
```

要创建一个适当命名的序列对象以保存肽翻译，请调用：

```
AjPSeq ajTrnNewPep(const AjPSeq nucleicSeq, ajint frame);
```

要读取翻译数据文件（在初始化翻译时内部使用）：

```
void ajTrnReadFile(AjPTrn trnObj, AjPFile trnFile);
```

## 6.9 处理特征

### 6.9.1 简介

特征是分子序列中感兴趣的区域，例如限制性酶切位点、蛋白质二级结构预测状态、外显子位置、motif 匹配区域等。EMBOSS 支持用于输入和输出的大多数格式（参见 _EMBOSS 用户指南_），这些格式是为将特征输入主要基因组序列数据库而开发的。

许多应用程序不直接读写特征。特征也用于存储序列分析结果，并可以作为‘报告’写出，其中通过 ACD 定义的报告格式用于写出特征表和（对于某些格式）原始序列（参见第 6.15 节，‘处理应用程序报告’）。

特征是序列中简单范围（起始和结束）的注释，或是带编号的特征组的注释，这些特征组具有‘join’（用于合并编码序列中的外显子）或其他组合（‘group’或‘one-of’在 EMBL/Genbank 特征表中）。

这些复杂特征作为带有每个组件一组更简单特征的父特征存储。目前这些特征存储在同一特征表中。在未来版本中，这些特征可能成为子特征以简化排序操作。





功能对象模型基于通用特征格式 3（GFF3）特征数据格式，其中特征由以下内容描述：

- 开始和结束位置
- 描述特征的名称
- 链方向（在核苷酸序列中）
- 得分。

功能对象还包含以下数据：

- 对于开始或结束宽于单个碱基或残基的特征，第二个开始和结束位置。
- ‘Source’，记录特征来源的程序或数据库名称。
- 特征类型（特征键），使用源自序列本体（SO）的内部名称，并在 Efeatures.emboss（核苷酸）或 Efeatures.protein（蛋白质）数据文件中定义，包含所有 EMBL/GenBank 和 UniProt 特征类型。
- 标签名称和值列表，定义在 Etags.emboss（核苷酸）或 Etags.protein（蛋白质）数据文件中，包含所有 EMBL/GenBank 或 UniProt 特征限定符。
- 编码核苷酸特征的帧 1...3，-1...-3，非编码或蛋白质特征为 0。
- 用于 EMBL 位置的标志位掩码，用于记录碱基之间（1^2）的特征、join/order/one-of 类型以及其他属性。
- EMBL/GenBank 特征表中单个外显子和 join/order/one-of 特征位置的父级的组号。
- 远程 ID，特征位置（例如 join 使用的外显子）位于同一数据库中的另一个条目。
- 特征在另一个条目中位置的标签。
- 外显子号。

特征类型需要标准化，以允许格式间转换。EMBOSS 使用安装在 share/EMBOSS/data/ 目录中的一组数据文件，为每个输入/输出格式以及内部使用定义类型和标签名称。主要内部命名文件为核苷酸特征的 Efeatures.emboss 和 Etags.emboss，以及蛋白质特征的 Efeatures.protein 和 Etags.protein。这些文件包含主要特征格式定义，因此大多数特征类型和标签（在格式之间没有冲突的情况下）将被原样存储和返回。对于这些文件中未出现的任何类型或标签，将使用第一个定义的名称作为默认值（核苷酸类型为‘misc_feature’，蛋白质类型为‘polypeptide region’，标签名称为‘note’）。

特征表只是一组特征，存储在三种上下文之一中：

- 作为序列文件的一部分
- 作为数据库条目的一部分
- 作为原始特征表（不包含特征所引用序列的文件）。

**注意**

特征表定义具有受控词汇表，即有一个指定的可用特征类型和标签名称列表。这意味着您无法编辑特征表以添加具有新键的特征。如果您编辑特征表，必须坚持使用允许的特征键集。

'Named note' 标签是一种存储不在允许集中的特征标签名称的方法。默认（note）特征标签存储的值以 '*name' 开头，后跟值。这样在使用 EMBL 或 GFF3 等标准格式写出特征时，可以保持以可读形式保存的注释。

应用程序要读取或写入的特征在应用程序 ACD 文件中定义，尽管如果需要，也可以直接创建特征表。

特征文件的名称和文件中特征的格式通过命令行使用统一特征对象（UFO）指定（参见 _EMBOSS 用户指南_）。可用于特征的一组命令行限定符。这些允许您设置文件名、格式以及包含感兴趣特征的序列区域等内容。这些限定符可以作为属性硬编码在 ACD 文件中（参见第 A.5.2.8 节 ‘features’ 和第 A.5.3.2 节 ‘featout’）。

AJAX 提供了处理特征的全面功能，包括：

- 特征可以直接读取和写入，作为 ACD 处理的替代方案
- 处理特征的对象的元素可以直接检索或设置
- 特征标签处理
- 查询特征和特征表的属性
- 特征和特征表的处理。

### 6.9.2 AJAX 库文件

下表列出了用于处理特征的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajfeat | 通用序列特征处理 |
| ajfeatdata | 特征数据类型 |

ajfeat.h/.c。用于通用特征处理的大部分所需函数。它们还包含用于低级处理特征的静态函数。除非您计划实现代码以扩展库的核心功能，否则不太可能需要这些函数。

ajfeatdata.h/c。用于一般用途的基本特征对象（AjPFeattable、AjPFeature 和 AjPFeattabOut），例如通过 ACD 文件处理检索特征。它还定义了用于低级特征输入处理的特征输入对象（AjPFeattabIn）。

### 6.9.3 ACD 数据类型

特征表（而非单个特征）可以在 ACD 文件中指定为输入或输出。处理特征表输入的数据类型是：

- features 特征表输入

处理特征表输出的数据类型是：

- featout 特征表输出

如果设置了 features: ACD 属性，还可以从输入序列读取特征，并与输出序列一起写入。如果设置，则序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

序列输入的 ACD 数据类型包括：

- sequence 读取单个序列
- seqall 顺序读取多个序列，一次一个
- seqset 将多个序列读取为单个集合
- seqsetall 将多个序列读取为多个集合

序列输出的 ACD 数据类型包括：

- seqout 写入单个序列
- seqoutset 将多个序列写入为单个集合
- seqoutall 顺序写入多个序列，一次一个

### 6.9.4 ACD 数据定义

特征输入的典型 ACD 定义：

```
features: features
[
   parameter: "Y"
   type: "protein"
]
```

特征输出的典型 ACD 定义：

```
featout: outfeat
[
    parameter: "Y"
    type: "protein"
    multiple: "N"
]
```

带有特征的序列输入的典型 ACD 定义：

```
# single input sequence
sequence: sequence
[
    parameter: "Y"
    type: "gapany"
    features: "Y"
]
```

带有特征的序列输出的典型 ACD 定义：

```
# single sequence
seqout: outseq
[
    parameter: "Y"
    type: "gapany"
    features: "Y"
]
```

使用 sequence 数据类型仅为说明目的；也可以给出其他序列输入和输出类型。

### 6.9.4.1 参数名称

特征输入和输出的所有数据定义都应具有标准参数名称。这些包括：

- features 用于任何特征输入
- outfeat 用于任何输出
- 允许替代和变体（例如，用于多个输入的 afeatures、bfeatures）。

有关更多信息，请参见附录 A，ACD 语法参考。

### 6.9.4.2 常见属性

通常指定的属性摘要如下。它们是特定于数据类型的（第 A.5 节，‘特定于数据类型的属性’），除非它们被指示为全局属性（第 A.4 节，‘全局属性’）。

## 6.9 处理特征

parameter: 特征通常是 EMBOSS 应用程序的主要输入或输出，因此应使用全局属性 parameter: "Y" 将其定义为参数。

type: 指定特征所属的序列类型（蛋白质或核苷酸），并用于验证目的。

multiple: 一个布尔属性，可为 featout 数据定义设置，以指定特征注释适用于多个序列。

oformat: 输出特征默认使用 GFF 格式。格式通常在命令行上设置，但可以使用 oformat: 硬编码默认值。支持所有常见特征格式（参见 _EMBOSS 用户指南_）。

所有序列对象都可以包含特征表。通过 ACD 数据类型输入时，如果 ACD 定义中的 features: 属性为 true，则将读取特征。

### 6.9.5 AJAX 数据类型

用于处理特征表（包括在 ACD 文件中定义的输入特征表），请使用：

- AjPFtable 特征表，包含 AjPFeature 对象列表（用于 features ACD 数据类型）

用于处理在 ACD 文件中定义的特征表输出，请使用：

- AjPFtabOut 特征表输出（用于 featout ACD 数据类型）

还有一个用于处理单个特征的基本对象：

- AjPFeature 生物学特征

还有一个用于低级特征输入的数据类型，超出了各个库文件中提供的静态数据类型：

- AjPFtabIn 低级特征表输入

除非您计划实现代码以支持 EMBOSS 的新特征格式，否则不太可能需要 AjPFtabIn。有关如何执行此操作的建议，请咨询 EMBOSS 开发人员。

在开发应用程序时，特征表最有可能作为报告输出的一部分使用。读取序列，将分析结果生成作为特征，并以报告格式输出两者（参见第 6.15 节，‘处理应用程序报告’）。

### 6.9.6 ACD 文件处理

通过 ACD 文件处理特征的数据类型和函数如下所示。

| 标题 | 读取特征 | 写入特征 |
| --- | --- | --- |
| ACD 数据类型 | features | featout |





| AJAX 数据类型 | AjPFeattable | AjPFeattabOut |
| --- | --- | --- |
| 从 ACD 检索 | ajAcdGetFeatures | ajAcdGetFeatout |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.9.6.1 输入特征检索

要检索输入特征，需声明一个对象指针，然后使用 ajAcdGetFeatures 进行初始化：

```
AjPFeattable features=NULL;
features = ajAcdGetFeatures("features");
```

### 6.9.6.2 输出特征检索

要检索输出特征流，需声明并初始化一个对象指针，使用 ajAcdGetFeatout：

```
AjPFeattabOut outfeat=NULL;
outfeat = ajAcdGetFeatout("outfeat");
```

### 6.9.6.3 处理命令行选项和 ACD 属性

### 6.9.6.3.1 设置特征范围

特征输入数据类型包含多种内置命令行限定符，包括 -fbegin 和 -fend（用于指定特征的起始和结束位置），以及 -freverse（用于反转核苷酸特征的方向）。

读取特征表时，特征值将保存在相应的特征表对象中。无论范围值如何，整个表都会加载到内存中。函数 ajFeattableTrim 或 ajFeattableTrimOff 用于将特征修剪到 -fbegin 和 -fend 定义的区域：

```
AjFeattable ftable=NULL;
ftable = ajAcdGetFeatures("features");
ajFeattableTrim(ftable);
/* ajFeattableTrimOff(ftable,0,ajFeattableGetLen(ftable));*/
```

## 6.9 处理特征

读取序列时，特征值将保存在相应序列对象中的特征表里。无论序列范围值如何，整个序列都会加载到内存中。函数 ajSeqTrim（对于 AjPSeqset 对象则为 ajSeqsetTrim）用于将序列和特征修剪到 -sbegin 和 -send 定义的区域：

```
AjPSeq seq=NULL;

seq = ajAcdGetSeq("sequence");

ajSeqTrim(seq);
```

### 6.9.6.4 内存管理

在程序结束时释放内存是您的责任。必须对 ajAcdGet* 调用返回的任何对象调用默认析构函数（见下文）。

此外，您必须调用 embExit 来清理内部内存，包括为特征表管理分配的内存：

```
embExit();
```

### 6.9.7 内存管理

### 6.9.7.1 默认对象构造

要使用未在 ACD 文件中定义的特征表对象，必须首先实例化相应的对象指针。默认构造函数是 ajFeattableNew。
ajFeattableNew 会使特征表类型保持未初始化状态。当向表中添加特征时，会设置该类型。特定类型的函数 ajFeattableNewDna 和 ajFeattableNewProt 分别用于创建核苷酸和蛋白质特征表。函数 ajFeattableNewSeq 创建与序列对象类型和长度匹配的特征表。

特征表输出对象通常从 ACD 文件处理中加载（见上文）。在极少需要手动创建的情况下，可以使用默认构造函数 ajFeattabOutNew，或使用 ajFeattabOutNewCSF 和 ajFeattabOutNewSSF 函数（它们使用现有输出文件以及指定的类型和序列名称）。

要创建特征对象（通常存储在特征表中），可使用类似的一组函数。ajFeatNew 创建包含所有属性（包括类型）的特征。ajFeatNewProt 创建蛋白质特征所需的所有属性的特征（无链或框架）。
ajFeatNewII 和 ajFeatNewIIRev 是只需起始和结束值的通用构造函数。特征类型将默认为“杂项特征”或“多肽区域”值。
ajFeatNewFeat 是一个复制构造函数，用于从现有特征创建特征对象。

```
/* Constructor for feature which is added to table */
AjPFeature ajFeatNew (AjPFeattable thys,
                     const AjPStr source,
                     const AjPStr type,
                     ajint Start,
                     ajint End,
float score,
char strand,
ajint frame);
/* Constructor for protein feature */
AjPFeature ajFeatNewProt(AjPFeattable thys,
const AjPStr source,
const AjPStr type,
ajint Start, ajint End,
float score);
/* Simple constructor with only start and end positions */
AjPFeature ajFeatNewII (AjPFeattable thys,
ajint Start, ajint End);
/* Simple constructor, sets features to be on reverse strand */
AjPFeature ajFeatNewIIRev (AjPFeattable thys,
ajint Start, ajint End);
/* Copies a feature */
AjPFeature ajFeatNewFeat (const AjPFeature orig);
/* Feature Table Object Constructors */
AjPFeattable ajFeattableNew (const AjPStr name);
AjPFeattable ajFeattableNewDna (const AjPStr name);
AjPFeattable ajFeattableNewProt (const AjPStr name);
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
/* Output Feature Table Object constructors */
AjPFeattabOut ajFeattabOutNew (void);
AjPFeattabOut ajFeattabOutNewCSF (const char* fmt, const AjPStr name,
const char* type, AjPFile file);
AjPFeattabOut ajFeattabOutNewSSF (const AjPStr fmt, const AjPStr name,
const char* type, AjPFile file);
```

ajFeatNew 的参数如下：

- thys 指向添加新特征的特征表的指针
- source 特征的分析依据
- type 特征类型（例如 外显子）
- Start 特征的起始位置
- End 特征的结束位置
- score 特征的分析得分
- strand 特征的链
- frame 特征的框架

所有构造函数都返回新对象的地址。

### 6.9.7.2 默认对象销毁

使用完对象后，必须释放其内存。相关函数如下：

```
void ajFeatDel (AjPFeature *pthis);
void ajFeattableDel (AjPFeattable *pthis);
void ajFeattabOutDel (AjPFeattabOut* pthis);
```

### 示例

在以下示例中，特征表和单个特征是使用默认构造函数手动构建的。特征将写入从 ACD 处理中检索的特征表：

```
AjPFeattable feattable;
AjPStr name = NULL;
AjPStr source = NULL;
AjPStr type = NULL;
char strand = '+';
ajint frame = 0;
AjPFeature feature = NULL;
AjPFeattabOut output = NULL;
ajint i;
float score = 0.0;
embInit("demofeatures", argc, argv);

output = ajAcdGetFeatout("outfeat");

ajStrAssignC(&name,"seq1");

feattable = ajFeattableNew(name);

ajStrAssignC(&source,"demofeature");
score = 1.0;

for(i=1;i<11;i++)
{
    if(i & 1)
        ajStrAssignC(&type,"CDS");
    else
        ajStrAssignC(&type,"misc_feature");
    feature = ajFeatNew(feattable, source, type, i, i+10, score, strand,
                        frame);
}

ajFeattableWrite(output, feattable);

ajStrDel(&source);
ajStrDel(&name);
ajStrDel(&type);
ajFeattableDel(&feattable);
ajFeattabOutDel(&output);
```

### 6.9.7.4 替代对象构造和加载

### 6.9.7.4.1 单个特征

创建特征对象有多种替代方法。可以指定特征的起始和结束位置：

```
AjPFeature ajFeatNewII (AjPFeattable thys, ajint Start, ajint End);
AjPFeature ajFeatNewIIRev (AjPFeattable thys, ajint Start, ajint End);
```

```
AjPFeature ajFeatNewProt (AjPFeattable thys,
 const AjPStr source, const AjPStr type,
 ajint Start, ajint End, float score);
```

ajFeatNewIIRev 将特征设置为反向链，而 ajFeatNewProt 用于蛋白质特征。

在需要可安全修改和/或删除的特征副本的情况下，可以使用 ajFeatNewFeat：

```
AjPFeature ajFeatNewFeat (const AjPFeature orig);
```

### 6.9.7.4.2 特征表

创建特征表对象有多种替代方法，可以通过名称或从现有序列对象创建：

```
/* DNA feature table
 */
AjPFeattable ajFeattableNewDna (const AjPStr name);

/* Protein feature table */
AjPFeattable ajFeattableNewProt (const AjPStr name);

/* From existing sequence; type is determined by the sequence type. */
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
```

在需要可安全修改和/或删除的特征表副本的情况下，可以使用：

```
/* Copy whole feature table */
AjPFeattable ajFeattableNewFtable (const AjPFeattable orig);

/* Copy limited number of features */
AjPFeattable ajFeattableNewFtableLimit (const AjPFeattable orig, ajint limit);
```

可以使用以下函数从序列对象中检索特征表（定义在 ajseq.c 中）：

```
AjPFeattable ajSeqGetFeatCopy (const AjPSeq thys);
const AjPFeattable ajSeqGetFeat (const AjPSeq thys);
```

### 6.9.7.4.3 编辑特征表

要向特征表（AjPFeattable）添加新特征（AjPFeature），请调用：

```
void ajFeattableAdd (AjPFeattable thys, AjPFeature feature);
```





清除特征表中的所有特征，请调用：

```
void ajFeattableClear (AjPFeattable thys);
```

清除输出特征表中的所有特征，请调用：

```
void ajFeattabOutClear (AjPFeattabOut *thys);
```

## 6.9.8 读取特征

特征可以直接读取，使用特征表输入对象（这些是ACD处理所使用的函数）：

```
AjPFeattable ajFeattableNewRead (AjPFeattabIn ftin);
AjPFeattable ajFeattableNewReadUfo (AjPFeattabIn tabin,
const AjPStr Ufo);
```

ajFeattableNewReadUfo 将解析UFO，打开输入文件并读取特征表。
ajFeattableNewRead 是从特征表输入对象读取特征的通用接口函数。

## 6.9.9 写入特征

特征可以直接写入，即不使用ACD处理（默认使用GFF3格式或由环境变量EMBOSS_OUTFEATFORMAT定义的格式）。特征可以写入ajfeat.c中定义的数据结构FeatOOutFormat所定义的任何格式：

```
AjBool ajFeatOutFormatDefault (AjPStr* pformat);
AjBool ajFeattableWriteUfo (AjPFeattabOut tabout, const AjPFeattable thys,
const AjPStr Ufo);
AjBool ajFeattableWrite (const AjPFeattable ft, AjPFeattabOut ftout);
```

ajFeatOutFormatDefault 设置默认输出格式为“gff”，除非定义了EMBOSS_OUTFEATFORMAT变量或在pformat参数中传入了格式。

ajFeattableWriteUfo 和 ajFeattableWrite 与 ajFeattableNewRead 和 ajFeattableNewReadUfo 等效，但用于写入。
ajFeattableWriteUfo 将解析UFO，打开输出文件并将特征表写入其中。ajFeattableWrite 是给定文件句柄、映射类、输出数据格式以及可能的其他相关数据时，用于将特征写入文件的通用接口函数。

以下函数以指定格式写入特征表：

```
/* DDBJ format */
AjBool ajFeattableWriteDdbj (const AjPFeattable features, AjPFile file);

/* EMBL format */
AjBool ajFeattableWriteEmbl (const AjPFeattable features, AjPFile file);

/* Genbank format */
AjBool ajFeattableWriteGenbank (const AjPFeattable features, AjPFile file);

/* GFF format */
AjBool ajFeattableWriteGff2 (const AjPFeattable features, AjPFile file);

/* GFF format */
AjBool ajFeattableWriteGff3 (const AjPFeattable features, AjPFile file);

/* PIR format */
AjBool ajFeattableWritePir (const AjPFeattable features, AjPFile file);

/* SwissProt format */
AjBool ajFeattableWriteSwiss (const AjPFeattable features, AjPFile file);
```

特征表可以使用ajreport.h/c中定义的以下函数写入应用程序报告：

```
void ajReportSetType (AjPReport thys, const AjPFeattable ftable, const AjPSeq seq);
AjBool ajReportWrite (AjPReport thys, const AjPFeattable ftable, const AjPSeq seq);
void ajReportWriteHeader (AjPReport thys, const AjPFeattable ftable, const AjPSeq seq);
void ajReportWriteTail (AjPReport thys, const AjPFeattable ftable, const AjPSeq seq);
```

有关报告的更多信息，请参见第6.15节‘处理应用程序报告’。

## 6.9.10 输出特征表函数

此处描述的函数用于操作输出特征表对象。
要打开输出文件，请调用：

```
AjBool ajFeattabOutOpen (AjPFeattabOut thys, const AjPStr ufo);
```

输出特征表对象的元素可以使用以下方式检索和查询：

```
AjPFile ajFeattabOutFile (const AjPFeattabOut thys);
AjPStr ajFeattabOutFilename (const AjPFeattabOut thys);

/* These functions are used internally to test whether the output file
has been opened and used */
AjBool ajFeattabOutIsLocal (const AjPFeattabOut thys);
AjBool ajFeattabOutIsOpen (const AjPFeattabOut thys);
```

输出特征表的元素使用以下方式设置：

```
/* sets the UFO (format and filename) for feature output */
AjBool ajFeattabOutSet (AjPFeattabOut thys, const AjPStr ufo);

/* sets the base file name (.format) for feature output */
void ajFeattabOutSetBasename (AjPFeattabOut thys, const AjPStr basename);

/* sets the feature table type 'any', 'N' 'nucleotide' or 'P' 'protein' */
AjBool ajFeattabOutSetType (AjPFeattabOut thys, const AjPStr type);
AjBool ajFeattabOutSetTypeC (AjPFeattabOut thys, const char* type);
```

## 6.9.11 检索特征对象的元素

特征对象的元素可以使用以下方式检索：

```
/* End position */
ajuint ajFeatGetEnd (const AjPFeature thys);

/* Direction (ajTrue for a forward direction, ajFalse for reverse) */
AjBool ajFeatGetForward (const AjPFeature thys);

/* Reading frame */
ajint ajFeatGetFrame (const AjPFeature thys);

/* Sequence length */
ajuint ajFeatGetLength(const AjPFeature thys);

/* Finds a named note tag (a general tag value with a *name prefix) */
AjBool ajFeatGetNoteS (const AjPFeature thys, AjPStr* val, const AjPStr name);
AjBool ajFeatGetNoteSI (const AjPFeature thys, AjPStr* val, const AjPStr name,
                        ajint count);
AjBool ajFeatGetNoteC (const AjPFeature thys, AjPStr* val, const char* name);
AjBool ajFeatGetNoteCI (const AjPFeature thys,
                        AjPStr* val, const char* name, ajint count);

/* Returns the nth value of a named
feature tag. If not found as a tag, also searches for a named note tag*/
AjBool ajFeatGetTagC (const AjPFeature thys, const char* tname, ajint num,
                      AjPStr* val);
AjBool ajFeatGetTagS (const AjPFeature thys, const AjPStr name, ajint num,
                      AjPStr* val);

/* Score */
float ajFeatGetScore (const AjPFeature thys);

/* Source name */
const AjPStr ajFeatGetSource (const AjPFeature thys);

/* Start position */
ajuint ajFeatGetStart (const AjPFeature thys);

/* Strand */
char ajFeatGetStrand (const AjPFeature thys);

/* Returns the type (key) of a feature object. */
const AjPStr ajFeatGetType (const AjPFeature thys);
```

> **注意**
> 
> 请注意，`ajFeatGetType` 返回指向指定特征对象的类型（键）的指针的副本。该键仍由特征所有，不应销毁。

## 6.9.12 检索特征表对象的元素

特征表对象的元素可以使用以下方式检索：

```
/* Returns the feature table start position, or 1 if no start has been set.*/
ajint ajFeattableGetBegin (const AjPFeattable thys);

/* Returns the features table end position, or the
feature table length if no end has been set.*/
ajint ajFeattableGetEnd (const AjPFeattable thys);

/* Returns the name of a feature table object. */
const AjPStr ajFeattableGetName (const AjPFeattable thys);
const char* ajFeattableGetTypeC (const AjPFeattable thys);
const AjPStr ajFeattableGetTypeS (const AjPFeattable thys);

/* Returns the sequence length of a feature table */
ajint ajFeattableGetLen (const AjPFeattable thys);

/* Returns the number of features */
ajint ajFeattableGetSize (const AjPFeattable thys);
```

> **注意**
> 
> `ajFeattableGetName`、`ajFeattableGetTypeC` 和 `ajFeattableGetTypeS` 返回指向名称或类型（键）的指针的副本。这仍由特征表所有，因此不应销毁。

## 6.9.13 设置特征对象的元素

特征对象的元素（在注释中指示）可以使用以下方式设置：

```
/* Description */
void ajFeatSetDesc (AjPFeature thys, const AjPStr desc);

/* Append to description */
void ajFeatSetDescApp (AjPFeature thys, const AjPStr desc);

/* Score */
void ajFeatSetScore (AjPFeature thys, float score);

/* Strand */
void ajFeatSetStrand (AjPFeature thys, AjBool rev);
```

## 6.9.14 设置特征表对象的元素

特征表对象的元素可以使用以下方式设置：

```
/* Name */
void ajFeattableSetDefname (AjPFeattable thys, const AjPStr setname);

/* Sequence length */
void ajFeattableSetLength (AjPFeattable thys, ajuint len);

/* Type to nucleotide */
void ajFeattableSetNuc (AjPFeattable thys);

/* Type to protein */
void ajFeattableSetProt (AjPFeattable thys);

/* Begin and end range */
void ajFeattableSetRange (AjPFeattable thys, ajint fbegin, ajint fend);
```

ajFeattableSetDefname 为特征表的当前程序运行提供一个唯一名称。

## 6.9.15 处理特征标记的函数

特征标记（名称和值）作为列表中的对存储。标记可以作为数组返回或进行迭代。添加值时（对特征进行注释），它们通常简单地定义为名称和值对，这将替换任何具有相同标记名称的现有值。某些标记名称允许多个值（例如EMBL/Genbank特征‘note’用于一般注释，以及带有‘*name’前缀的‘命名标记标签’的值）。这些可以使用ajFeatTagAdd函数作为额外值添加。标记值根据最新的EMBL/GenBank特征表文档进行验证。如果变量EMBOSS_FEATWARN设置为true，则会生成警告消息，但默认情况下关闭，以避免来自其他来源的数据产生过多警告。处理特征标记的函数包括：

```
AjBool ajFeatTagAdd (AjPFeature thys, const AjPStr tag, const AjPStr value);
AjBool ajFeatTagAddC (AjPFeature thys, const char* tag, const AjPStr value);
AjBool ajFeatTagAddCC (AjPFeature thys, const char* tag, const char* value);
AjBool ajFeatTagSet (AjPFeature thys, const AjPStr tag, const AjPStr value);
AjBool ajFeatTagSetC (AjPFeature thys, const char* tag, const AjPStr value);
AjIList ajFeatTagIter (const AjPFeature thys);
AjBool ajFeatTagval (AjIList iter, AjPStr* tagnam, AjPStr* tagval);
void ajFeatTagTrace (const AjPFeature thys);
```





处理 FeattabIn 对象的函数是可用的，但此处未介绍，因为您通常不需要使用此对象。

## 6.9.16 查询特征属性

可用函数用于检查复杂特征位置以处理连接及其子（外显子）特征。提供了函数来测试特征是否定义了远程 ID（特征引用另一序列），并测试碱基范围是否在处理或输出所需的范围内。特征属性可使用以下内容查询：

```
/* Tests whether the feature is a child member of a join */
AjBool ajFeatIsChild (const AjPFeature gf);

/* Tests whether the feature is a member of a complement around a multiple
(join, etc.) */
AjBool ajFeatIsCompMult (const AjPFeature gf);

/* Tests whether the feature is a member of a join, group order or one_of */
AjBool ajFeatIsMultiple (const AjPFeature gf);

/* Checks whether the feature is in another (remote id) sequence */
AjBool ajFeatIsLocal (const AjPFeature gf);

/* ... and tests the location is within a specified range */
AjBool ajFeatIsLocalRange (const AjPFeature gf, ajint start, ajint end);
```

## 6.9.17 查询特征表属性

特征表的类型（核苷酸或蛋白质）可使用以下内容查询：

```
/* Returns ajTrue if nucleotide */
AjBool ajFeattableIsNuc (const AjPFeattable thys);

/* Returns ajTrue if protein */
AjBool ajFeattableIsProt (const AjPFeattable thys);
```

## 6.9.18 处理特征

有几个用于处理特征的函数：

```
void ajFeatReverse (AjPFeature thys, ajint ilen) ;
AjBool ajFeatTrimOfRange (AjPFeature ft, ajint ioffset,
ajint begin, ajint end,
AjBool dobegin, AjBool doend) ;
```

ajFeatReverse 将通过反转所有位置和链数据来反转特征。

ajFeatTrimOfRange 使用指定的 begin 和 end 值修剪特征表。

ajFeatTrimOfRange 在序列已被修剪的情况下会被调用，因此有必要指定开头处的任何缺失序列位置 (ioffset)。

## 6.9.19 处理特征表

特征表中的所有特征可使用以下内容进行反转或修剪：

```
/* Reverse the features in a feature table by iterating through and reversing all positions and strands. */
void ajFeattableReverse (AjPFeattable thys) ;

/* Trim a feature table using the Begin and Ends. */
AjBool ajFeattableTrimOff (AjPFeattable thys, ajuint ioffset, ajuint ilen);
```

要将特征表中的位置（起始或结束值）转换为源序列中的真实位置，可使用修剪特征表在设定范围内的任何偏移信息：

```
ajuint ajFeattablePos (const AjPFeattable thys, ajuint ipos);
ajuint ajFeattablePosI (const AjPFeattable thys, ajuint imin, ajuint ipos);
ajuint ajFeattablePosII (ajuint ilen, ajuint imin, ajuint ipos);
```

如果 ipos 为负数，则从字符串末尾而非开头开始计数。对于字符串，结果可能会超出末尾到达终止 NULL。对于序列，最大值为最后一个碱基。

最后，特征表中的特征可使用以下内容进行排序：

```
/* End position */
void ajFeatSortByEnd (AjPFeattable Feattab);

/* Start position */
void ajFeatSortByStart (AjPFeattable Feattab);

/* Type */
void ajFeatSortByType (AjPFeattable Feattab);
```

## 6.9.20 其他函数

有几个用于处理特征的其他函数：

```
/* Returns a sequence from a feature. */
AjBool ajFeatGetSeq(const AjPFeature thys, const AjPFeattable table,
                    const AjPSeq seq, AjPStr* Pseqstr);
```

## 6.10 处理比较矩阵

## 6.10.1 简介

比较矩阵通常用于分子序列分析，以比较两个或多个比对序列中相同位置的序列字符。

矩阵对象通过读取本地矩阵数据文件创建，可以通过 ACD（用户可选择文件）或直接读取文件名固定的命名文件来实现。EMBOSS 在数据目录中包含一组比较矩阵文件，可在创建新文件时作为示例使用。

矩阵对象有两种非常相似的形式，一种使用整数（AjPMatrix）以提高速度，另一种使用浮点数（AjPMatrixf）以提供灵活性。两种类型都包括一组列标签（通常是序列字符）和一组行标签（通常与列标签匹配；某些应用中使用非对称矩阵）。行和列还有一个矩阵大小值。数据文件中的数字成为比较值的二维表格。

分析序列比对的应用程序（例如 prettyplot）可以直接使用矩阵中的转换表和字符代码，通过 AjPSeqcvt 对象查找比较分数。

## 6.10.2 AJAX 库文件

用于处理矩阵的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajmatrices | 比较矩阵处理函数 |

ajmatrices.h/c。定义了用于处理比较矩阵的 AjPMatrix 和 AjPMatrixf 对象及函数。

## 6.10.3 ACD 数据类型

有两种用于处理比较矩阵输入的数据类型：

- matrix 整数比较矩阵
- matrixf 浮点比较矩阵

有两种用于处理比较矩阵输出的数据类型：

- outmatrix 输出整数比较矩阵
- outmatrixf 输出浮点比较矩阵

## 6.10.4 ACD 数据定义

比较矩阵输入的典型 ACD 定义：

```
#Integer matrix (input)
matrix: matrix
[
    information: "Matrix file"
    protein: "$(acdprotein)"
]
# Floating point matrix (input)
matrixxf: matrixxf
[
    information: "Matrix file"
    protein: "$(acdprotein)"
]
```

比较矩阵输出的典型 ACD 定义：

```
# Integer matrix (output)
outmatrix: outmatrix
[
    information: "Matrix file"
    protein: "$(acdprotein)"
]
# Floating point matrix (output) :
outmatrixf: outmatrixf
[
    information: "Matrix file"
    protein: "$(acdprotein)"
]
```

### 6.10.4.1 参数名

比较矩阵输入和输出的所有数据定义都应具有标准参数名，即 matrix。有关详细信息，请参阅附录 A，ACD 语法参考。

### 6.10.4.2 常用属性

通常指定的属性摘要如下。除非标记为全局属性（第 A.4 节，“全局属性”），否则它们均为特定于数据类型的属性（第 A.5 节，“特定于数据类型的属性”）。

information：全局属性。
它指定用户提示，并用于应用程序文档。

protein：布尔属性，如果设置，则指定矩阵用于蛋白质。
如果未设置，则假定矩阵用于核酸。

## 6.10.5 AJAX 数据类型

用于处理比较矩阵（包括在 ACD 文件中定义的输入矩阵），请使用：

- AjPMatrix 整数比较矩阵（用于 matrix ACD 数据类型）
- AjPMatrixf 浮点比较矩阵（用于 matrixf ACD 数据类型）
用于处理比较矩阵输出，请使用：
- AjPOutfile 通用输出文件（用于 outmatrix 和 outmatrixf ACD 数据类型）

有时有必要将序列转换为数值形式以便于处理。此用途的 AJAX 数据类型为：
- AjOSeqCvt 用于将序列转换为数值形式

## 6.10.6 ACD 文件处理

通过 ACD 文件处理比较矩阵的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
| --- | --- | --- |
| 比较矩阵输入 | | |
| matrix | AjPMatrix | ajAcdGetMatrix |
| matrixf | AjPMatrixf | ajAcdGetMatrixf |
| 比较矩阵输出 | | |
| outmatrix | AjPMatrix | ajAcdGetOutmatrix |
| outmatrixf | AjPMatrixf | ajAcdGetOutmatrixf |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行句柄控制，这些函数返回指向相应对象的指针。

### 6.10.6.1 输入比较矩阵检索

要检索比较矩阵，需声明对象指针，然后使用相应的 ajAcdGet* 函数进行初始化。

### 6.10.6.1.1 整数比较矩阵

```
AjPMatrix matrix = NULL;
matrix = ajAcdGetMatrix("matrix");
```





### 6.10.6.1.2 浮点比较矩阵

```
AjPMatrixf matrix = NULL;
matrix = ajAcdGetMatrixf("matrix");
```

### 6.10.6.2 输出比较矩阵检索

要检索输出比较矩阵，需使用相应的 ajAcdGet* 函数声明并初始化对象指针。

### 6.10.6.2.1 整数比较矩阵

```
AjPOutfile outmatrix=NULL;
outmatrix = ajAcdGetOutmatrix("outmatrix");
```

### 6.10.6.2.2 浮点比较矩阵

```
AjPOutfile outmatrixf=NULL;
outmatrixf = ajAcdGetOutmatrixf("outmatrixf");
```

### 6.10.6.3 处理命令行选项和 ACD 属性

目前未为此提供相关函数。

### 6.10.6.4 内存和文件管理

程序结束时，关闭所有打开的文件并释放内存是你的责任。

### 6.10.6.4.1 关闭文件

你必须通过调用 ajOutfileClose 并传递输出文件对象的地址，关闭 ACD 文件中任何 outmatrix 或 outmatrixf 定义的输出文件：

```
AjPOutfile outmatrix = NULL;
AjPOutfile outmatrixf = NULL;

outmatrix = ajAcdGetOutmatrix("outmatrix");
outmatrixf = ajAcdGetOutmatrixf("outmatrixf");

/* Do something with matrices */

ajOutfileClose(&outmatrix);
ajOutfileClose(&outmatrixf);
```

### 6.10.6.4.2 释放内存

你必须对 ajAcdGet* 调用返回的任何比较矩阵对象调用默认析构函数（详见下文）。

## 6.10.7 矩阵对象内存管理

### 6.10.7.1 默认对象构造

矩阵对象通常通过 ACD 定义创建，读取指定的 EMBOSS 本地数据文件。若要直接创建矩阵对象（例如无法选择矩阵文件名的情况），必须通过调用以下函数从给定的本地数据文件构造对象：

```
AjBool ajMatrixNewFile (AjPMatrix* pthis, const AjPStr filename);
AjBool ajMatrixxfNewFile (AjPMatrixf* pthis, const AjPStr filename);
```

这些函数接受要打开的数据文件名。该文件必须位于 EMBOSS 数据路径中，包括当前目录和已安装的数据文件。

所有构造函数均返回新对象的地址。指针无需初始化为 NULL，但这样做是良好的编程实践：

```
AjPMatrix intmatrix = NULL;
AjPMatrixf floatmatrix = NULL;
AjPStr filename = NULL;

filename = ajStrNewC("EBLOSUM62");

intmatrix = ajMatrixNewFile(filename);
floatmatrix = ajMatrixxfNewFile(filename);
```

所有构造函数均返回新对象的地址。指针无需初始化为 NULL，但这样做是良好的编程实践：

### 6.10.7.2 默认对象销毁

使用完对象后，必须关闭所有输出文件并释放对象占用的内存。

要关闭输出文件（AjPOutfile），请调用 ajOutfileClose；对于常规文件对象（AjPFile），请调用 ajFileClose：

```
void ajFileClose (AjPFile* Pfile);
void ajOutfileClose (AjPOutfile* Pfile);
```

对象通过调用析构函数释放：

```
void ajMatrixDel (AjPMatrix *thys);
void ajMatrixxfDel (AjPMatrixf *thys);
```

用法如下：

```
AjPMatrix matrix = NULL;
AjPMatrix matrixxf = NULL;

matrix = ajAcdGetMatrix("matrix");
matrixf = ajAcdGetMatrixf("matrixf");

/* Do something with matrices */

ajMatrixDel(&matrix);
ajMatrixfDel(&matrixf);
```

### 6.10.7.3 替代对象构造和加载

在内部，矩阵对象构造函数如下：

```
AjPMatrix ajMatrixNew (const AjPStr codes, ajint n, const AjPStr filename);
AjPMatrixf ajMatrixfNew (const AjPStr codes, ajint n, const AjPStr filename);
```

这些函数会创建一个值初始化为零的新矩阵。函数接受矩阵名（filename）、包含矩阵标签字符的字符串（codes）以及表示标签数量的整数（n）。如果矩阵是残基替换矩阵，则字符串应包含已定义的序列字符。

由 ajMatrixNew 和 ajMatrixfNew 创建的矩阵为方阵，行数和列数相同。要创建行数和列数不相等的矩阵，请调用：

```
AjPMatrix ajMatrixNewAsym (const AjPStr codes, ajint n, const AjPStr rcodes,
ajint rn, const AjPStr filename);
AjPMatrixf ajMatrixfNewAsym (const AjPStr codes, ajint n, const AjPStr rcodes,
ajint rn, const AjPStr filename);
```

这些函数会创建一个值初始化为零的新矩阵。函数接受矩阵名（filename）以及两个字符串（codes 和 rcodes），分别包含矩阵列和行标签的字符，还有两个整数（n 和 rn），分别表示列和行标签的数量。

EMBOSS 要求所有矩阵对象均从数据文件加载。未提供添加或更改矩阵对象值的函数。以下函数从 EMBOSS 数据文件读取。有关 EMBOSS 数据文件的更多信息，请参阅《EMBOSS 用户指南》。

可以通过调用以下函数从给定的本地数据文件构造矩阵：

```
AjBool ajMatrixNewFile (AjPMatrix* pthis, const AjPStr filename);
AjBool ajMatrixfNewFile (AjPMatrixf* pthis, const AjPStr filename);
```

这些函数接受要打开的数据文件名。

## 6.10.8 检索矩阵属性的函数

矩阵对象的大多数元素可以通过调用 ajMatrixGet* 或 ajMatrixfGet* 函数之一来检索：

要将比较矩阵作为整数或浮点数组的数组返回，请调用：

```
AjIntArray* ajMatrixGetMatrix (const AjPMatrix thys);
AjFloatArray* ajMatrixfGetMatrix (const AjPMatrixf thys);
```

序列字符在该数组中使用矩阵内部的序列转换表进行索引。AjIntArray 和 AjFloatArray 在 ajdefine.h 中定义为 C 类型整数和浮点数的数组：

```
typedef float* AjFloatArray;
typedef int* AjIntArray;
```

要返回矩阵行或列在位置 i 处的标签（序列字符或非对称矩阵的列名），请调用：

```
AjPStr ajMatrixGetLabelNum (const AjPMatrix thys, ajint i);
AjPStr ajMatrixfGetLabelNum (const AjPMatrixf thys, ajint i);
```

要返回矩阵的序列字符转换表，请调用：

```
AjPSeqCvt ajMatrixGetCvt (const AjPMatrix thys);
AjPSeqCvt ajMatrixfGetCvt (const AjPMatrixf thys);
```

该表将矩阵中定义的任何字符转换为正整数，任何其他字符均转换为零。

要返回矩阵中每个偏移量的字符代码，请调用：

```
AjPStr ajMatrixGetCodes (const AjPMatrix thys);
AjPStr ajMatrixfGetCodes (const AjPMatrixf thys);
```

要返回矩阵对象的名称（通常是读取该对象的文件名），请调用：

```
const AjPStr ajMatrixGetName (const AjPMatrix thys);
const AjPStr ajMatrixfGetName (const AjPMatrixf thys);
```

要返回比较矩阵的大小（或非对称矩阵的列数），请调用：

```
ajuint ajMatrixGetSize (const AjPMatrix thys);
ajuint ajMatrixfGetSize (const AjPMatrixf thys);
```

对于非对称矩阵，可以通过调用以下函数返回行数：

```
ajuint ajMatrixGetRows (const AjPMatrix thys);
ajuint ajMatrixfGetRows (const AjPMatrixf thys);
```

## 6.10.9 矩阵索引函数

要使用矩阵内部转换表将序列转换为索引号，请调用：

```
AjBool ajMatrixSeqIndex (const AjPMatrix thys, const AjPSeq seq, AjPStr* numseq);
AjBool ajMatrixfSeqIndex (const AjPMatrixf thys, const AjPSeq seq, AjPStr* numseq);
```

矩阵中未定义的序列字符转换为零。

## 6.10.10 序列转换

这些函数处理序列转换对象。基本构造函数 ajSeqcvtNewStr 使用字符串数组作为列标签。对于序列比较矩阵，这些字符串每个将为一个字符。其他构造函数会重新编码代码以满足一些旧版代码的特定要求，不建议用于一般用途。最有用的函数是返回碱基或残基数值代码的函数，常用于在转换表中查找序列字符。

```
/* constructors with base codes as a string*/
AjPSeqCvt ajSeqcvtNewStr (const AjPPStr bases, ajint n);
AjPSeqCvt ajSeqcvtNewC (const char* bases);
AjPSeqCvt ajSeqcvtNewNumberC (const char* bases);
AjPSeqCvt ajSeqcvtNewEndC (const char* bases);

/* asymmetric conversion table constructor */
AjPSeqCvt ajSeqcvtNewStrAsym (const AjPPStr bases, ajint n, const AjPPStr rbases,
ajint rn);

/* destructor */
void ajSeqcvtDel (AjPSeqCvt* thys);

/* return conversion table length */
ajuint ajSeqcvtGetLen (const AjPSeqCvt thys);

/* return numeric code for a residue code (matrix column label) */
ajint ajSeqcvtGetCodeK (const AjPSeqCvt thys, char ch);
ajint ajSeqcvtGetCodeS (const AjPSeqCvt thys, const AjPStr ch);

/* return numeric code for a column or row in an asymmetric matrix */
ajint ajSeqcvtGetCodeAsymS (const AjPSeqCvt cvt, const AjPStr str);
ajint ajSeqcvtGetCodeAsymrowS (const AjPSeqCvt cvt, const AjPStr str);
```





## 6.11 处理比对

### 6.11.1 简介

EMBOSS支持大多数常见的序列比对格式用于输入和输出（完整列表请参阅_EMBOSS 用户指南_）。要读取或写入的比对在应用程序ACD文件中定义，尽管如果需要，也可以直接创建比对对象。

大多数比对格式可以包含标准标题（位于比对文件开头）以及在某些情况下的尾部（位于文件末尾），其中提供包括程序、日期、输出文件名、序列ID名称以及比对的一些参数和统计信息在内的信息。还有一个子标题和子尾部，用于附加注释和注释。

尾部部分被一些应用程序（例如EMBOSS中的**merger**）用于报告比对的特殊特征。

所有比对都具有某些基本属性：

- 序列类型（蛋白质或核苷酸）
- 比对格式
- 比对中的序列数量
- 允许的最小序列数
- 允许的最大序列数
- 输出宽度。

此外，通常还有关联数据，包括：

- 整数或浮点矩阵
- 矩阵名称
- 间隙插入罚分
- 间隙延伸罚分。

对于全局比对，可以显示完整序列或仅匹配区域。可选地，比对可以包括比对序列的登录号、序列描述和完整USA。

上述选项通常在应用程序ACD文件中设置（通过数据定义的属性）或在命令行上设置（通过特定于比对的限定符）。如果需要，提供了函数来直接设置这些选项。有关这些属性和限定符的描述，请参见第A.5节，“数据类型特定属性”。

用于操作比对的函数分为四组：

- 写入比对
- 检索比对对象的元素
- 设置比对对象的元素
- 杂项函数。

### 6.11.2 AJAX库文件

下表列出了用于处理比对的AJAX库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| :--- | :--- |
| ajalign | 用于处理序列比对的函数 |
| ajseq | 通用序列处理 |

ajalign.h/c 定义了主比对对象（AjPAlign）。它可用于通过ACD文件处理来检索输入序列比对。头文件包含您用于一般序列比对处理所需的大多数函数。它包括用于低级处理比对的静态数据类型和函数。除非您计划实现代码以支持新的比对格式，否则不太可能需要后者。有关如何执行此操作的建议，请咨询EMBOSS开发人员。

ajseq.h/c 定义了AjPSeqset对象。这是一组用于一般用途的序列，用于处理来自ACD文件的输入比对。ajseq.h/c 包含用于处理序列集的大量函数，从而用于对序列比执行一般操作。

### 6.11.3 ACD数据类型

比对输入被处理为通用序列集输入的特殊情况。使用seqset ACD数据类型：

- seqset 将多个序列读取为单个集合。ACD数据定义必须包含aligned:属性（见下文）。

有一个专用于输出比对的数据类型：

- align 比对输出

### 6.11.4 ACD数据定义

输入比对的典型ACD定义：

```
# multiple sequence input read as a single aligned set
seqset: sequence
[
   parameter: "Y"
   type: "protein"
   aligned: "Y"
]
```

输出比对的典型ACD定义：

```
align: outfile
[
    parameter: "Y"
    aformat: "srspair"
    type: "protein"
    minseqs: "2"
    maxseqs: "2"
    aglobal: "Y"
]
```

### 6.11.4.1 参数名

比对输入和输出的所有数据定义都应具有标准参数名。这些包括：

- sequence 用于任何比对的输入序列
- outfile 用于比对输出
- 允许替代和变体（例如，afile、bfile用于多个输出）。

有关更多信息，请参见附录A，ACD语法参考。

### 6.11.4.2 常用属性

通常指定的属性摘要如下。除非它们被指示为全局属性（第A.4节，“全局属性”），否则它们是数据类型特定的（第A.5节，“数据类型特定属性”）。

parameter: 比对通常是EMBOSS应用程序的主要输入或输出，因此应使用全局属性parameter: "Y"将其定义为参数。

type: 指定输入或输出比对中序列的类型，并用于验证目的。

aligned: 任何seqset或seqsetall数据类型都必须设置aligned:属性，以指示序列是否已比对。

aformat: 输出格式通常在命令行上设置，但可以使用aformat:硬编码默认值。支持所有常见的比对格式（请参阅EMBOSS用户指南）。

minseqs: 指定预期的最小序列数，并用于验证输出。

maxseqs: 指定预期的最大序列数，并用于验证输出。

aglobal: 一个布尔属性，如果输出可以包含来自同一输入的多个比对，则将其设置为"Y"。

### 6.11.5 AJAX数据类型

用于处理比对（包括在ACD文件中定义的输入比对），请使用：

AjPSeqset 输入比对

用于处理在ACD文件中定义的输出比对，请使用：

AjPAlign 输出比对

### 6.11.6 ACD文件处理

下表显示了用于通过ACD文件处理比对的数据类型和函数。

| 标题 | 读取比对 | 写入比对 |
|---|---|---|
| ACD数据类型 | seqset | align |
| AJAX数据类型 | AjPSeqset | AjPAlign |
| 从ACD检索 | ajAcDGetSeqset | ajAcDGetAlign |

您的应用程序代码将调用embInit来处理ACD文件和命令行（参见第6.3节，“处理ACD文件”）。ACD文件中的所有值都读入内存，并根据需要打开文件。您可以通过ajAcDGet*系列函数对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.11.6.1 输入比对检索

要检索输入比对，需声明对象指针，然后使用ajAcDGetSeqset对其进行初始化：

```
AjPSeqset seqset=NULL;
seqset = ajAcDGetSeqset("sequence");
```

### 6.11.6.2 输出比对检索

要检索输出比对流，需声明对象指针并使用ajAcDGetAlign对其进行初始化：

```
AjPAlign outfile=NULL;
outfile = ajAcDGetAlign("outfile");
```

### 6.11.6.3 内存和文件管理

在程序结束时，关闭任何文件并释放内存是您的责任。

### 6.11.6.3.1 关闭输出比对文件

要关闭输出比对流，使用AJAX函数ajAlignClose：

```
ajAlignClose (outfile);
```

### 6.11.6.3.2 释放内存

您必须对 ajAcDGet* 调用返回的任何对象调用默认析构函数（见下文）。

此外，您必须调用ajAlignExit以清理为比对处理内务管理分配的内部内存：

```
ajAlignExit();
```

### 6.11.7 比对对象内存管理

### 6.11.7.1 默认对象构造

比对输出对象通常从ACD文件处理加载（见上文）。在不太可能需要手动创建对象的情况下，可以使用默认比对对象构造函数ajAlignNew。所有构造函数都返回新对象的地址。在以下代码中，指针不需要初始化为NULL，但这样做是良好实践：

```
AjPAlign align = NULL;
align = ajAlignNew();
/* The object is instantiated and ready for use */
```

### 6.11.7.2 默认对象销毁

在使用完对象后，必须释放其内存。默认析构函数是：

```
void ajAlignDel (AjPAlign* pthys) ; /* Destructor for Alignment objects */
```

用法如下：

```
AjPAlign align=NULL;
align = ajAcdGetAlign("align") ;
```


/* Do something with alignment */
ajAlignDel(&align);

### 6.11.7.3 替代对象构建与加载

创建比对输出的应用程序通常会生成已比对序列，然后用这些序列填充比对对象。以下函数可用：

```
/* Defines a sequence set as an alignment. The sequences
are stored internally and may
be edited by alignment processing. */
AJBool ajAlignDefine (AjPAlign thys, AjPSeqset seqset);

/* Defines a sequence pair as an alignment.
The sequences are stored internally and may
be edited by alignment processing. */
AJBool ajAlignDefineSS (AjPAlign thys,
                        AjPSeq seqa, AjPSeq seqb);

/* Defines a pair of char* strings as an alignment (names of sequences are also
required) */
AJBool ajAlignDefineCC (AjPAlign thys,
                        const char* seqa, const char* seqb,
                        const char* namea,const char* nameb);
```

### 6.11.8 写入比对

有多个 AJAX 函数可用于写出比对信息。应用程序通常会通过 ACD 处理创建比对对象，用已比对序列填充它（见上文），并调用 ajAlignWrite。

```
/* Writes an alignment file */
void ajAlignWrite (AjPAlign thys);

/* Reset to allow reuse of Alignment objects */
void ajAlignReset (AjPAlign thys);

/* Opens a new align file. Called by ACD processing */
AJBool ajAlignOpen (AjPAlign thys, const AjPStr name);

/* Writes an alignment header. Called by ajAlignWrite */
void ajAlignWriteHeader (AjPAlign thys);

/* Writes an alignment tail. Called by ajAlignWrite */
void ajAlignWriteTail (AjPAlign thys);

/* Sets the default format for an alignment to 'gff' if not already defined */
AJBool ajAlignFormatDefault (AjPStr* pformat);
```

### 6.11.9 检索比对对象的元素

比对对象的元素很少需要程序员检查。有可用函数来检索内部值。

```
/* Returns the filename for an alignment. If the alignment has more than
one subalignment, returns the total.*/
ajint ajAlignGetLen (const AjPAlign thys);

/* Returns the filename */
const char* ajAlignGetFilename (const AjPAlign thys);

/* Returns the sequence format */
const AjPStr ajAlignGetFormat (const AjPAlign thys);
```

### 6.11.10 设置比对对象的元素

比对对象具有用于填充输出的头部和尾部部分的元素（输出格式可以包含此类额外细节）。

比对头部中可设置的元素包括：

- 差距罚分
- 矩阵名称
- 比对得分。

以下是相关函数。注意矩阵名称可以直接设置，也可以从矩阵对象设置：

```
/* Setting elements of the alignment header */
void ajAlignSetGapI (AjPAlign thys, ajint gapen, ajint extpen);
void ajAlignSetGapR (AjPAlign thys, float gapen, float extpen);
void ajAlignSetMatrixName (AjPAlign thys, const AjPStr matrix);
void ajAlignSetMatrixNameC (AjPAlign thys, const char* matrix);
void ajAlignSetMatrixInt (AjPAlign thys, AjPMatrix matrix);
void ajAlignSetMatrixFloat (AjPAlign thys, AjPMatrixf matrix);
void ajAlignSetScoreI (AjPAlign thys, ajint score);
void ajAlignSetScoreL (AjPAlign thys, ajlong score);
void ajAlignSetScoreR (AjPAlign thys, float score);
```

比对子头部中的标准属性为：

- 长度
- 同一性
- 差距
- 相似性
- 得分。

设置这些属性的函数是：

## 6.11 处理比对

```
/* Setting elements of the alignment header */
void ajAlignSetSubStandard (AjPAlign thys, ajint ialli);
```

或者，您可以使用以下方式手动设置这些属性：

```
void ajAlignSetStats (AjPAlign thys, ajint iali, ajint len,
 ajint ident, ajint sim, ajint gaps,
 const AjPStr score);
```

头部部分可以包含可选注释。同样，尾部部分是可用于报告比对任何特殊说明的自由文本。注释可以在（子）头部和（子）尾部中设置，也可以追加或预添加，使用以下函数：

```
/* Setting comments of the alignment (sub)header and (sub)tail */
void ajAlignSetHeader (AjPAlign thys, const AjPStr header);
void ajAlignSetHeaderApp (AjPAlign thys, const AjPStr header);
void ajAlignSetHeaderC (AjPAlign thys, const char* header);
void ajAlignSetSubHeader (AjPAlign thys, const AjPStr subheader);
void ajAlignSetSubHeaderApp (AjPAlign thys, const AjPStr subheader);
void ajAlignSetSubHeaderC (AjPAlign thys, const char* subheader);
void ajAlignSetSubHeaderPre (AjPAlign thys, const AjPStr subheader);
void ajAlignSetSubTail (AjPAlign thys, const AjPStr tail);
void ajAlignSetSubTailC (AjPAlign thys, const char* tail);
void ajAlignSetSubTailApp (AjPAlign thys, const AjPStr tail);
void ajAlignSetTail (AjPAlign thys, const AjPStr tail);
void ajAlignSetTailApp (AjPAlign thys, const AjPStr tail);
void ajAlignSetTailC (AjPAlign thys, const char* tail);
```

比对类型（蛋白质或核酸）可以直接设置（如果尚未设置）：

```
void ajAlignSetType (AjPAlign thys);
```

可以使用以下方式设置要输出的序列范围（或子范围）：

```
/* Setting sequence range to output */
AjBool ajAlignSetRange (AjPAlign thys,
 ajint start1, ajint end1,
 ajint len1, ajint off1,
 ajint start2, ajint end2,
 ajint len2, ajint off2);

AjBool ajAlignSetSubRange (AjPAlign thys,
 ajint substart1, ajint start1,
 ajint end1, AjBool rev1, ajint len1,
 ajint substart2, ajint start2,
 ajint end2, AjBool rev2, ajint len2);
```

最后，有一个函数可将比对对象设置为使用外部序列引用，这些引用是实际序列的引用（复制的指针），而不是克隆：

```
/* Setting properties of alignment object */
void ajAlignSetExternal (AjPAlign thys, AjBool external);
```

这旨在用于大序列的比对，在这种情况下保留多个副本是不希望的。

### 6.11.11 杂项函数

ajAlignConsStats 函数为多重比对计算共识序列和统计信息（百分比同一性和相似性以及比对长度）。ajAlignFindFormat 在 ACD 处理中用于将指定的比对格式与内部已知格式列表进行匹配。

```
/* Calculates alignment statistics (and consensus) */
AjBool ajAlignConsStats (const AjPSeqset thys, AjPMatrix mymatrix,
	AjPStr *cons, ajint* retident,
	ajint* retsim, ajint* retgap,
	ajint* retlen);

/* Finds alignment format in internal definitions, returns index */
AjBool ajAlignFindFormat (const AjPStr format, ajint* ifomat);
```

## 6.12 处理系统发育数据

### 6.12.1 简介

EMBASSY phylipnew 包包含用于系统发育分析的各种应用程序。
有一组系统发育数据类型可用于复制 phylip 的可用输入数据类型，并自动检测数据格式（例如，距离矩阵文件）：

| AJAX 数据类型 | ACD 数据类型（读取） | ACD 数据类型（写入） |
| :--- | :--- | :--- |
| AjPPhyloDist 距离矩阵数据 | distances | outdistance |
| AjPPhyloFreq 频率数据 | frequencies | outfreq |
| AjPPhyloProp 属性数据 | properties | outproperties |
| AjPPhyloState 状态数据 | discretestates | outdiscrete |
| AjPPhyloTree 系统发育树数据 | tree | outtree |

### 6.12.2 AJAX 库文件

下表列出了用于处理系统发育数据的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：
http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajphylo | 用于处理 phylipnew 应用程序的数据结构和函数 |
| ajnexus | 用于解析 NEXUS 文件格式的数据结构和函数 |

ajphylo.h/c. 定义用于处理系统发育数据的对象和函数。这些包括：

- 系统发育距离矩阵对象 (AjPPhyloDist)
- 系统发育频率对象 (AjPPhyloFreq)
- 系统发育属性对象 (AjPPhyloProp)
- 系统发育离散状态数据对象 (AjPPhyloState)
- 系统发育树对象 (AjPPhyloTree)。

它们还包括用于在低级别处理系统发育数据的静态函数。除非您计划扩展系统发育处理代码，否则不太可能需要这些函数。

ajnexus.h/c. 用于解析 NEXUS 文件格式的函数和对象（包括静态数据结构和函数）。您不太可能需要此库文件。有关更多信息，请参阅在线库文档。

### 6.12.3 AJAX 数据类型

用于处理 ACD 文件中定义的系统发育数据输入文件，请使用：

- AjPPhyloState* 系统发育离散状态数据对象（用于 discretestates ACD 数据类型）
- AjPPhyloDist 系统发育距离矩阵对象（用于 distances ACD 数据类型）
- AjPPhyloFreq 系统发育频率对象（用于 frequencies ACD 数据类型）
- AjPPhyloProp 系统发育属性对象（用于 properties ACD 数据类型）
- AjPPhyloTree* 系统发育树对象（用于 tree ACD 数据类型）

用于处理 ACD 文件中定义的系统发育数据输出文件，请使用：

- AjPOutfile 输出文件（用于所有系统发育输出 ACD 数据类型）。

### 6.12.4 ACD 数据类型

用于处理系统发育数据输入的数据类型为：


- discretestates: 离散状态文件
- distances: 距离矩阵
- frequencies: 频率值
- properties: 属性值
- tree: 系统发育树

用于处理系统发育数据输出的数据类型如下：

- outdiscrete: 系统发育离散特征数据输出文件
- outdistances: 系统发育距离矩阵数据输出文件
- outfreq: 系统发育字符频率数据输出文件
- outproperties: 系统发育属性数据输出文件
- outtree: 系统发育树数据输出文件

## 6.12.5 ACD 数据定义

系统发育数据输入和输出的典型 ACD 定义如下。

### 6.12.5.1 discretestates

离散状态数据输入：

```
discretestates: discretestatesfile
[
   parameter: "Y"
   characters: "01PB?"
   knowntype: "discrete states"
   information: "Phylip discrete states file"
]
```

### 6.12.5.2 distances

距离数据输入：

```
distances: distancesfile
[
   parameter: "Y"
   knowntype: "distance matrix"
   information: "Phylip distance matrix file"
]
```

### 6.12.5.3 frequencies

频率数据输入：

```
frequencies: frequenciesfile
[
  parameter: "Y"
]
```

### 6.12.5.4 properties

属性数据输入：

```
properties: propertiesfile
[
  characters: "01"
  length: "$(infile.discretelength)"
  knowntype: "ancestral states"
  information: "Phylip ancestral states file"
]
```

### 6.12.5.5 tree

树数据输入：

```
tree: treefile
[
  parameter: "Y"
  knowntype: "newick"
  information: "Phylip tree file (optional)"
]
```

### 6.12.5.6 outdiscrete

离散状态数据输出：

```
outdiscrete: outdiscretefile
[
  parameter: "Y"
]
```

### 6.12.5.7 outdistance

距离数据输出：

```
outdistance: outdistancefile
[
  parameter: "Y"
]
```

### 6.12.5.8 outfreq

频率数据输出：

```
outfreq: outfreqfile
[
   parameter: "Y"
]
```

### 6.12.5.9 outproperties

属性数据输出：

```
outproperties: outpropertiesfile
[
   parameter: "Y"
]
```

### 6.12.5.10 outtree

树数据输出：

```
outtree: outtreefile
[
   parameter: "Y"
]
```

### 6.12.5.11 参数名

系统发育数据输入和输出的所有数据定义都应具有直观的名称。

有一些一般性指导原则，但目前未强制执行具体的命名规则。参见
附录 A，ACD 语法参考。

### 6.12.5.12 常用属性

下表汇总了通常指定的属性。除非它们被指示为全局属性（第 A.4 节，“全局属性”），否则它们均为数据类型特定属性（第 A.5 节，“数据类型特定属性”）。

parameter：如果系统发育数据是 EMBOSS 应用程序的主要输入或输出，则应使用全局属性
parameter: "Y" 将其定义为参数。

characters：分别指定 discretestates 或 properties 对象允许的离散状态或属性字符。

knowntype：此全局属性通常用于所有系统发育输入和输出类型。

information：用于用户提示和应用程序文档的全局属性。

length：指定每组的属性值数量（properties 数据类型）或每组的频率位点/值数量（frequencies 数据类型）。

size：指定离散状态集数量（discretestates 数据类型）、频率集数量（frequencies 数据类型）或树的数量（tree 数据类型）。

**注意**

各种计算属性（第 A.6 节，“计算属性”）在 ACD 文件级别可用。

## 6.12.6 ACD 文件处理

通过 ACD 文件处理系统发育数据的数据类型和函数如下。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
| :--- | :--- | :--- |
| *系统发育数据输入* | | |
| discretestates | AjPPhyloState* | ajAcdGetDiscretestates |
| distances | AjPPhyloDist | ajAcdGetDistances |
| frequencies | AjPPhyloFreq | ajAcdGetFrequencies |
| properties | AjPPhyloProp | ajAcdGetProperties |
| tree | AjPPhyloTree* | ajAcdGetTree |
| *系统发育数据输出* | | |
| outdiscrete | AjPOutfile | ajAcdGetOutdiscrete |
| outdistance | AjPOutfile | ajAcdGetOutdistance |
| outfreq | AjPOutfile | ajAcdGetOutfreq |
| outproperties | AjPOutfile | ajAcdGetOutproperties |
| outtree | AjPOutfile | ajAcdGetOuttree |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.12.6.1 系统发育数据检索

#### 6.12.6.1.1 输入系统发育数据

要检索输入系统发育数据，需声明对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

##### discretestates

```
AjPPhyloState *data=NULL;
data = ajAcdGetDiscretestates("discretestatesfile");
```

##### distances

```
AjPPhyloDist data=NULL;
data = ajAcdGetDistances("distancesfile");
```

##### frequencies

```
AjPPhyloFreq data=NULL;
data = ajAcdGetFrequencies("frequenciesfile");
```

##### properties

```
AjPPhyloProp data=NULL;
data = ajAcdGetProperties("propertiesfile");
```

##### tree

```
AjPPhyloTree* data=NULL;
data = ajAcdGetTree("treefile");
```

#### 6.12.6.1.2 输出系统发育数据

要检索输出系统发育数据流，需声明对象指针，并使用相应的 ajAcdGet* 函数对其进行初始化。

##### outdiscrete

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutdiscrete("outdiscretefile");
```

##### outdistance

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutdistance("outdistancefile");
```

##### outfreq

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutfreq("outfreqfile");
```

##### outproperties

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutproperties("outpropertiesfile");
```

##### outtree

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOuttree("outtreefile");
```

#### 6.12.6.1.3 替代 ACD 检索函数

存在用于从文件中检索单个（第一个）状态或树对象的函数：

```
AjPPhyloState ajAcdGetDiscretestatesSingle (const char *token);
AjPPhyloTree ajAcdGetTreeSingle (const char *token);
```

使用这些函数时，仍然需要调用相应的析构函数（见下文），以确保释放在 ACD 文件处理期间分配的状态或树对象数组。

### 6.12.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.12.6.3 内存和文件管理

程序结束时，关闭所有文件并释放内存是您的责任。

#### 6.12.6.3.1 关闭输出系统发育数据文件

要关闭输出系统发育数据流，请使用输出文件的地址调用 ajOutfileClose：

```
ajOutfileClose(&outfile);
```

#### 6.12.6.3.2 释放内存

您必须对 ajAcdGet* 调用返回的任何系统发育数据对象调用相应的析构函数（见下文）。

此外，您必须调用 ajPhyloExit 以释放内部用于管家工作的内存：

```
void ajPhyloExit (void);
```

## 6.12.7 系统发育对象内存管理

### 6.12.7.1 默认对象构造

要使用未在 ACD 文件中定义的系统发育数据对象，必须首先实例化相应的对象指针。默认构造函数如下：

```
AjPPhyloDist ajPhyloDistNew (void);
AjPPhyloFreq ajPhyloFreqNew (void);
AjPPhyloProp ajPhyloPropNew (void);
AjPPhyloState ajPhyloStateNew (void);
AjPPhyloTree ajPhyloTreeNew (void);
```

### 6.12.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认析构函数如下：

```
void ajPhyloDistDel (AjPPhyloDist* pthis);
void ajPhyloFreqDel (AjPPhyloFreq* pthis);
void ajPhyloPropDel (AjPPhyloProp* pthis);
void ajPhyloStateDel (AjPPhyloState* pthis);
void ajPhyloTreeDel (AjPPhyloTree* pthis);
```

默认构造函数和析构函数的用法如下：

```
AjPPhyloDist dist = NULL;
AjPPhyloFreq freq = NULL;
AjPPhyloProp prop = NULL;
AjPPhyloState state = NULL;
AjPPhyloTree tree = NULL;

/* Call constructor functions */
dist = ajPhyloDistNew();
freq = ajPhyloFreqNew();
prop = ajPhyloPropNew();
state = ajPhyloStateNew();
tree = ajPhyloTreeNew();

/* Do something with instantiated objects */
...

/* Call destructor functions */
ajPhyloDistDel (&dist);
ajPhyloFreqDel (&freq);
ajPhyloPropDel (&prop);
ajPhyloStateDel (&state);
ajPhyloTreeDel (&tree);
```

有两个替代析构函数用于释放状态和树对象数组：

```
void ajPhyloStateDelarray(AjPPhyloState** pthis);
void ajPhyloTreeDelarray(AjPPhyloTree** pthis);
```

它们用于状态和树对象，而非默认析构函数，以释放 ACD 文件处理产生的内存：



## 6.12.7.3 替代对象构建和加载

### 6.12.7.3.1 系统发育数据输入

目前没有用于此的函数。

### 6.12.7.3.2 系统发育数据输出

目前没有用于此的函数。

### 6.12.8 从文件读取系统发育数据

用于此的函数如下：

```
AjPPhyloDist* ajPhyloDistRead (const AjPStr filename, ajint size, AjBool missing);
AjPPhyloFreq ajPhyloFreqRead (const AjPStr filename, AjBool contchar, AjBool genedata, AjBool indiv);
AjPPhyloProp ajPhyloPropRead (const AjPStr filename, const AjPStr propchars, ajint len, ajint size);
AjPPhyloState* ajPhyloStateRead (const AjPStr filename, const AjPStr statechars);
AjPPhyloTree* ajPhyloTreeRead (const AjPStr filename, ajint size);
```

这些函数的提供是为了在ACD文件处理上下文之外处理系统发育数据时使用。有关更多信息，请参阅在线文档。

### 6.12.9 获取系统发育对象的元素

目前只有一个用于此的函数。它返回属性对象的大小：

```
ajint ajPhyloPropGetSize (const AjPPhyloProp thys);
```

### 6.12.10 调试函数

这些函数将每个对象的元素报告到调试文件。函数如下：

```
void ajPhyloDistTrace (const AjPPhyloDist thys);
void ajPhyloFreqTrace (const AjPPhyloFreq thys);
void ajPhyloPropTrace (const AjPPhyloProp thys);
void ajPhyloStateTrace (const AjPPhyloState thys);
void ajPhyloTreeTrace (const AjPPhyloTree thys);
```

## 6.13 处理密码子使用表

### 6.13.1 简介

EMBOSS提供一个密码子使用表对象，用于存储描述核苷酸序列中密码子使用情况的数组。

输入和输出的密码子使用表通常在ACD文件中定义，但如果需要，也可以直接创建。提供了用于读写数据、获取和设置对象元素、计算密码子使用表属性以及反向翻译的函数。还有一些杂项函数，主要用于三联体碱基代码与密码子索引之间的相互转换。

创建密码子使用表的代码需要先创建一个输出对象，然后用编码序列中的密码子使用数据填充它，计算密码子频率的统计信息，并写入使用用户选定格式的文件。

### 6.13.2 AJAX库文件

下表列出了用于处理密码子使用表的AJAX库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajcod | 密码子使用表处理 |

ajcod.h/c. 定义了AjPCod对象和用于处理密码子使用表的函数。它还包含用于在低级别处理它们的静态数据结构和函数。除非您打算扩展库的核心功能，否则不太可能需要这些。

### 6.13.3 ACD数据类型

用于处理密码子使用表的ACD数据类型是：

- codon 密码子使用表文件

### 6.13.4 ACD数据定义

密码子使用表输入的典型ACD定义：

```
codon: infile
[
  parameter: "y"
]
```

密码子使用表输出的典型ACD定义：

```
outcodon: outfile
[
  parameter: "Y"
]
```

### 6.13.4.1 参数名称

密码子使用表输入和输出的所有数据定义都应具有直观的名称：目前未定义标准名称。

### 6.13.4.2 常用属性

通常指定的属性总结如下。

parameter: 如果密码子使用表是EMBOSS应用程序的主要输入或输出，则应使用parameter: "Y"将其定义为参数（参见第A.4节“全局属性”）。

### 6.13.5 AJAX数据类型

用于处理密码子使用表（包括在ACD文件中定义的输入密码子使用表），请使用：

- AjPCod 密码子使用表对象（用于codon ACD数据类型）

用于处理在ACD文件中定义的输出密码子使用表，请使用：

- AjPOutfile 通用输出文件（用于outcodon ACD数据类型）

### 6.13.6 ACD文件处理

通过ACD文件处理密码子使用表的数据类型和函数如下所示。

| | 读取密码子使用表 | 写入密码子使用表 |
|---|---|---|
| ACD数据类型 | codon | outcodon |
| AJAX数据类型 | AjPCod | AjPOutfile |
| 从ACD检索 | ajAcdGetCodon | ajAcdGetOutcodon |

您的应用程序代码将调用embInit来处理ACD文件和命令行（参见第6.3节“处理ACD文件”）。ACD文件中的所有值都将读入内存，并根据需要打开文件。您可以通过ajAcdGet*函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.13.6.1 输入密码子使用表检索

要检索输入密码子使用表，需声明一个对象指针，然后使用ajAcdGetCodon对其进行初始化：

```
AjPCod cod = NULL;
cod = ajAcdGetCodon("infile");
```

### 6.13.6.2 输出密码子使用表检索

要检索输出密码子使用表流，需声明一个对象指针，并使用ajAcdGetOutcodon对其进行初始化：

```
AjPOutfile codout = NULL;
codout = ajAcdGetOutcodon("outfile");
```

### 6.13.6.3 处理命令行选项和ACD属性

目前没有用于此的函数。

### 6.13.6.4 内存和文件管理

程序结束时，关闭任何文件并释放内存是您的责任。

#### 6.13.6.4.1 关闭输出密码子使用表文件

要关闭输出密码子使用表，请使用ajOutfileClose：

```
ajOutfileClose(&codout);
```

#### 6.13.6.4.2 释放内存

您必须对通过ajAcdGetCodon或ajAcdGetOutcodon调用返回的任何对象调用默认析构函数（见下文）。

此外，您必须调用ajCodExit以清理为密码子使用处理内部管理分配的内存：

```
ajCodExit();
```

### 6.13.7 密码子使用表对象内存管理

#### 6.13.7.1 默认对象构建

要使用未在ACD文件中定义的密码子使用表对象，必须首先实例化相应的对象指针。默认构造函数是：

```
AjPCod ajCodNew(void);
```

所有构造函数都返回新对象的地址。在以下代码中，指针不需要初始化为NULL，但这样做是良好的做法：

```c
AjPCod cod = NULL;
cod = ajCodNew();
/* 对象已实例化并可供使用 */
```

#### 6.13.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认析构函数是：

```c
void ajCodDel (AjPCod *pthys) ;
```

使用方法如下：

```c
AjPCod cod = NULL;
AjPOutfile codout = NULL;
cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");
...
ajCodDel(&cod);
ajOutfileClose(&codout);
```

#### 6.13.7.3 替代对象构建和加载

有两个替代构造函数。ajCodNewCodenum使用标准遗传代码中的氨基酸分配创建密码子使用对象。相比之下，ajCodNewCod将复制现有的密码子对象并返回指向新对象的指针：

```c
AjPCod ajCodNewCodenum (ajint code) ;
AjPCod ajCodNewCod (const AjPCod thys) ;
```

### 6.13.8 读写密码子使用表

#### 6.13.8.1 读取密码子使用表

要使用直接创建的密码子使用表（即未在ACD文件中定义的表），有必要为其分配一个密码子索引。ajCodRead将从文件读取密码子使用数据

```
AjBool ajCodRead (AjPCod thys, const AjPStr fn, const AjPStr format);
```

密码子输入和输出格式由entrails实用程序使用ajCodPrintFormat函数打印。

#### 6.13.8.2 写入密码子使用表

有两个类似的函数用于将密码子使用表信息写入文件，它们的区别在于传递的文件对象类型（AjPFile和AjPOutfile）：

```
void ajCodWrite (AjPCod thys, AjPFile outf);
void ajCodWriteOut (const AjPCod thys, AjPOutfile outf);
```

通常，密码子使用表输出文件（AjPOutfile）是从ACD文件处理加载的（见上文）。因此，对于与outcodon：ACD数据定义对应的此类AjPOutfile，将调用ajCodWriteOut：

```
AjPCod cod = NULL;
AjPOutfile codout = NULL;

cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");

ajCodWriteOut(cod, codout);
```

使用ajCodWrite时，需要手动处理输出文件的创建。使用ajFileNewOutNameC（或其他函数）来执行此操作：

```
AjPCod cod = NULL;
AjPFile codout = NULL;

/* Open a file called "OutputFileName" */
codout = ajFileNewOutNameC ("OutputFileName");

ajCodWrite(cod, codout);
```

### 6.13.9 获取和设置元素

密码子使用表的以下元素可以检索或设置：

- 名称
- 发行版
- 描述
- 分区





## 6.13 处理密码子使用表

- 物种
- 遗传密码
- CDS 数量
- 密码子数量。

获取元素的函数名称中包含 Get。这些函数的变体可用于返回 C 类型（char *）字符串而非 AJPSTR，但此处未显示：

```
const AJPStr ajCodGetName (const AJPCod thys); /* Name */
const AJPStr ajCodGetRelease (const AJPCod thys); /* Release */
const AJPStr ajCodGetDesc (const AJPCod thys); /* Description */
const AJPStr ajCodGetDivision (const AJPCod thys); /* Division */
const AJPStr ajCodGetSpecies (const AJPCod thys); /* Species */
ajint ajCodGetCode (const AJPCod thys); /* Genetic code */
ajint ajCodGetNumcds (const AJPCod thys); /* Number of CDSs */
ajint ajCodGetNumcodon (const AJPCod thys); /* Number of codons */
```

此外，ajCodGetCodonlist 将把密码子三联体写入字符串列表：

```
void ajCodGetCodonlist(const AJPCod cod, AJPList list);
```

设置元素的函数名称中包含 Set。同样，C 类型字符串的变体也可用：

```
void ajCodSetDescs (AJPCod thys, const AJPStr desc); /* Description */
void ajCodSetDivisionS (AJPCod thys, const AJPStr division); /* Division */
void ajCodSetNameS (AJPCod thys, const AJPStr name); /* Name */
void ajCodSetReleaseS (AJPCod thys, const AJPStr release); /* Release */
void ajCodSetSpeciesS (AJPCod thys, const AJPStr species); /* Species */
void ajCodSetCodenum (AJPCod thys, ajint geneticcode); /* Genetic code */
void ajCodSetNumcds (AJPCod thys, ajint numcds); /* Number of CDSs */
/*
void ajCodSetNumcodons (AJPCod thys, ajint numcodon); /* Number of codons */
void ajCodSetBacktranslate (AJPCod thys); /* Amino acid index used for back-translation. */
void ajCodSetTripletsS (AJPCod thys, const AJPStr s, ajint *c); /* Number of codons */
```

### 6.13.9.1 清除密码子使用表

如果要重用密码子使用表，有两个函数可用于清除数据：

```
/* Zero all entries including the genetic codes (the amino acids for each codon) */
void ajCodClear(AJPCod thys);

/* Zero the name, number count and fraction codon elements. */
void ajCodClearData(AJPCod thys);
```

### 6.13.10 计算属性

可计算密码子使用表的各种属性，包括：

- 密码子适应指数（参见 *Nucleic Acids Research* 15:1281–1295）
- 密码子适应指数 W 值（参见 *Nucleic Acids Research* 15:1281–1295）
- Gribsjkov 统计量（每千计数）
- 有效密码子数（*Gene* 87:23–29）
- 分数计数和每千密码子数
- 序列组成。

函数如下：

```
/* Codon adaptive index from a codon usage table */
double ajCodCalcCaiCod (const AjPcod thys);

/* Codon adaptive index for a coding sequence */
double ajCodCalcCaiSeq (const AjPcod cod, const AjPstr str);

/* Gribsjkov statistic (count per thousand) */
void ajCodCalcGribsjkov (AjPcod thys, const AjPstr s);

/* Effective number of codons */
double ajCodCalcNc (const AjPcod thys);

/* Fractional count and codons per thousand */
void ajCodCalcUsage (AjPcod thys, ajint c);
```

### 6.13.11 回译

有函数可用于回译表示氨基酸序列的字符串。
ajCodBacktranslate 将执行简单回译，而
ajCodBacktranslateAmbig 将把字符串回译为完全模糊的核苷酸序列：

```
void ajCodBacktranslate (AjPstr*b, const AjPstr a, const AjPcod thys);
void ajCodBacktranslateAmbig (AjPstr*b, const AjPstr a, const AjPcod thys);
```

在调用这些函数之前，应先调用 ajCodSetBacktranslate。这将
用氨基酸最常用的三联体索引初始化密码子使用对象。

### 6.13.12 杂项函数

包括：

```
/* Return one codon value given a possibly ambiguous base */
ajint ajCodBase (ajint c);
```

```
/* Convert triplet index to triple */
char* ajCodTriplet (ajint idx);
/* Return a codon index given a three character codon */
ajint ajCodIndex (const AjPStr s);
/* Return a codon index given a three character codon */
ajint ajCodIndexC (const char *codon);
/* Tests the output format for an outcodon ACD type */
ajint ajCodOutFormat (const AjPStr name);
```

## 6.14 处理文件

### 6.14.1 简介

EMBOSS 提供全面且灵活的文件处理功能，包括：

- 输入和输出常规文件
- 输入和输出数据文件
- 输入和输出目录
- 文件列表
- 来自目录的文件列表。

提供了 ACD 数据类型来处理上述所有内容。此外，如果需要，还提供了读写文件和直接处理目录的函数。

### 6.14.2 AJAX 库文件

下表列出了用于处理文件的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajfile | 常规文件处理 |

ajfile.h/c。用于处理数据文件、常规文件和目录的对象和函数，以及用于低级操作它们的静态函数。除非您计划实现代码以扩展库的核心功能，否则不太可能需要静态函数。

### 6.14.3 ACD 数据类型

有五种用于处理文件输入的数据类型：

- infile 常规输入文件
- datafile 输入数据文件
- directory 带有可选指定文件扩展名和文件名前缀的目录
- dirllist 从带有可选指定文件扩展名和文件名前缀的目录读取的文件名列表
- filelist 输入文件列表

有四种用于处理文件输出的数据类型：
- outfile 常规输出文件
- outdata 输出数据文件
- outdir 用于写入多个输出文件的输出目录
- directory 可用于输入或输出的目录

### 6.14.4 ACD 数据定义

下面给出了文件输入和输出的典型 ACD 定义。

### 6.14.4.1 infile

输入文件：

```
infile: pepstatsfile
[
   parameter: "Y"
   information: "Pepstats program output file (optional)"
   knowntype: "pepstats output"
]
```

### 6.14.4.2 filelist

文件列表输入：

```
filelist: files
[
   parameter: "Y"
   information: "Molecular weights file list"
   knowntype: "molwt"
]
```

### 6.14.4.3 datafile

输入数据文件：

```
datafile: aaproperties
[
   name: "Eaa_properties.dat"
   information: "Amino acid chemical classes data file"
   knowntype: "amino acid classification"
]
```

### 6.14.4.4 dirlist

输入目录列表：

```
dirlist: directory
[
	parameter: "Y"
	information: "Codon usage directories"
	knowntype: "codon usage"
]
```

### 6.14.4.5 directory

输入目录：

```
directory: directory
[
	parameter: "Y"
	information: "Database directory"
	knowntype: "emboss database directory"
]
```

### 6.14.4.6 outfile

输出文件：

```
outfile: outfile
[
	parameter: "Y"
	information: "Pepstats program output file"
	knowntype: "pepstats output"
]
```

### 6.14.4.7 outdata

输出数据文件：

```
outdata: outfile
[
	default: "Eaa properties.dat"
	information: "Amino acid chemical classes data file"
	knowntype: "amino acid classification"
]
```

### 6.14.4.8 outdir

输出目录：

```
outdir: indexoutdir
[
  parameter: "Y"
  information: "Index file output directory"
  knowntype: "emboss database index"
]
```

### 6.14.4.9 directory

输出目录：

```
directory: directory
[
  parameter: "Y"
  information: "Database directory"
  knowntype: "emboss database directory"
]
```

### 6.14.4.10 参数名称

文件输入和输出的所有数据定义都应具有标准参数名称。这些包括：

- “infile” 用于 infile
- “*files” 用于 filelist
- “directory” 用于 dirlist
- “directory” 用于 directory
- “outfile” 用于 outfile
- “outdir” 用于 outdir。

允许替代和变体。有关更多信息，请参见附录 A，ACD 语法参考。

### 6.14.4.11 常用属性

通常指定的属性摘要如下。除非指明为全局属性（参见第 4 节，“全局属性”），否则它们均为数据类型特定属性（第 A.5 节，“数据类型特定属性”）。

- **parameter**：文件数据类型通常是 EMBOSS 应用程序的主要输入或输出，因此应使用全局属性 parameter: "Y" 将其定义为参数。
- **information**：一个全局属性，用于指定用户提示。它在应用程序文档中使用。
- **knowntype**：一个全局属性，通常为所有文件输入和输出类型指定，并且 outfile 和 outdir 所必需。如果输出不是任何标准



EMBOSS 已知类型（第 4.3.5.3.1 节，“应用程序数据已知类型文件（knowntypes.standard）”）然后 ApplicationName 输出是推荐值。

name: 数据文件通常具有硬编码的文件名。您可以使用 name: 属性来定义此项。

default: 数据文件通常具有硬编码的文件名。为 outdata: 定义了默认文件名，使用 default: 全局属性（如您所期望的，没有 name: 属性可用）。

## 6.14.5 AJAX 数据类型

用于处理 ACD 文件中定义的输入文件和目录，请使用：

- AjPFile: 非缓冲文件，可用于输入或输出（用于 infile 和 datafile ACD 数据类型）
- AjPList: 通用列表（用于 filelist 和 dirlist ACD 数据类型的文件列表）
- AjPDir: 可用于输入或输出的目录（用于 directory ACD 数据类型）

用于处理 ACD 文件中定义的输出文件和目录，请使用：

- AjPFile: 通用文件（用于 outfile ACD 数据类型）
- AjPDir: 目录（用于 outdir 和 directory ACD 数据类型）

用于处理 ACD 文件中定义的包括输出数据文件在内的通用输出文件，请使用：

- AjPOutfile: 非缓冲输出文件

用于处理缓冲文件，请使用：

- AjPFilebuff: 缓冲文件对象，保存缓冲输入文件的信息
- AjPFilebufflist: 文件缓冲区，保存缓冲行的简单链表。这是 AjPFilebuff 对象的子结构

## 6.14.6 ACD 文件处理

通过 ACD 文件处理文件的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
|---|---|---|
| 文件输入 | | |
| infile | AjPFile | ajAcdGetInfile |
| filelist | AjPList | ajAcdGetFilelist |
| datafile | AjPFile | ajAcdGetDatafile |
| dirlist | AjPList | ajAcdGetDirlist |
| directory | AjPDir | ajAcdGetDirectory |
| 文件输出 | | |
| outfile | AjPFile | ajAcdGetOutfile |
| outdata | AjPOutfile | ajAcdGetOutdata |
| outdir | AjPDir | ajAcdGetOutdir |
| directory | AjPDir | ajAcdGetDirectory |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，该系列函数返回指向相应对象的指针。

### 6.14.6.1 输入文件检索

要检索输入文件、文件列表等，需声明对象指针，然后使用相应的 ajAcdGet* 函数进行初始化。

### 6.14.6.1.1 输入文件

```
AjPFile pepstatsfile = NULL;
pepstatsfile = ajAcdGetInfile("pepstatsfile");
```

### 6.14.6.1.2 输入文件列表

```
AjPList files= NULL;
files = ajAcdGetFilelist("files");
```

### 6.14.6.1.3 输入数据文件

```
AjPFile aaproperties = NULL;
aaproperties = ajAcdGetDatafile("aaproperties");
```

### 6.14.6.1.4 从目录输入文件列表

```
AjPList filelist = NULL;
filelist = ajAcdGetDirlist("directory");
```

### 6.14.6.1.5 目录（输入或输出）

```
AjPDir directory = NULL;
directory = ajAcdGetDirectory("directory");
```

### 6.14.6.2 输出文件检索

要检索输出文件流、目录等，需声明对象指针并使用相应的 ajAcdGet* 函数进行初始化。

### 6.14.6.2.1 输出文件

```
AjPFile outfile = NULL;
outfile = ajAcdGetOutfile("outfile");
```

### 6.14.6.2.2 输出数据文件

```
AjPOutfile outfile = NULL;
outfile = ajAcdGetOutdata("outfile");
```

### 6.14.6.2.3 输出目录

```
AjPDir indexoutdir = NULL;
indexoutdir = ajAcdGetOutdir("indexoutdir");
```

### 6.14.6.2.4 目录（输入或输出）

```
AjPDir directory = NULL;
directory = ajAcdGetDirectory("directory");
```

### 6.14.6.3 替代 ACD 检索函数

要检索目录名而非目录本身，请调用 ajAcdGetDirectoryName（directory ACD 对象）或 ajAcdGetOutdirName（outdir ACD 对象）。这两个函数都将目录名作为字符串对象返回。目录和名称字符串由调用方所有，应在应用程序退出时释放。例如：

```
AjPDir directory  = NULL;
AjPDir indexoutdir = NULL;
AjPStr indir      = NULL;
AjPStr outdir     = NULL;

directory  = ajAcdGetDirectory("directory");
indexoutdir = ajAcdGetOutdir("indexoutdir");

indir  = ajAcdGetDirectoryName("directory");
outdir = ajAcdGetOutdirName("indexoutdir");

/* ... */

ajStrDel(&indir);
ajStrDel(&outdir);
ajDirDel(&indexoutdir);
```

### 6.14.6.4 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.14.6.5 内存和文件管理

在程序结束时，关闭任何文件并释放内存是您的责任。

### 6.14.6.5.1 关闭文件

要关闭输入文件或输入数据文件，请使用输入文件的地址调用 ajFileClose。要关闭输出文件，请使用输出文件的地址调用 ajOutfileClose。根据上述示例：

```
AjPFile pepstatsfile = NULL;
AjPFile outfile = NULL;

pepstatsfile = ajAcdGetInfile("pepstatsfile");
outfile = ajAcdGetOutfile("outfile");

/* Do something with files */

ajFileClose (&pepstatsfile);
ajOutfileClose(&outfile);
ajOutfileClose(&outfile);
```

在两种情况下，文件都会被关闭，文件对象的内存会被释放。

### 6.14.6.5.2 释放内存

您必须调用析构函数（见下文）来释放 ajAcdGet* 调用返回的任何对象所使用的内存。

## 6.14.7 文件和目录对象内存管理

### 6.14.7.1 默认对象构造

要使用未在 ACD 文件中定义的文件或目录对象，必须首先实例化相应的对象指针。下面描述的默认构造函数接受要打开的文件或目录的名称。

### 6.14.7.1.1 通用输入和输出文件

通用输入和输出文件的基本构造函数如下：

```
/* Input file */
AjPFile ajFileNewInNameS (const AjPStr name);
/* Input file */
AjPFile ajFileNewInNameC (const char* name);

/* Output file */
AjPFile ajFileNewOutNameS (const AjPStr name);

/* Output file */
AjPFile ajFileNewOutNameC (const char* name);

/* Perl-style Pipe. */
AjPFile ajFileNewInPipe (const AjPStr str);

/* Output file */
AjPOutfile ajOutfileNewNameS (const AjPStr name);
```

通常，您会将 AjPFile 用于输入，将 AjPOutfile 用于输出，因此应优先使用 ajOutfileNewNameS，而不是 ajFileNewOutNameS 或 ajFileNewOutNameC。

### 6.14.7.1.2 数据文件

输入数据文件的默认构造函数如下：

```
/* Input data file */
AjPFile ajDatafileNewInNameS (const AjPStr name);

/* Input data file */
AjPFile ajDatafileNewInNameC (const char* name);
```

这些函数将文件名作为 C 类型（char *）或字符串对象（AjPStr）接受，其余方面相同。如果在以下按所示顺序搜索的路径之一中存在指定文件，则它们将打开该文件：

1. .（当前工作目录）
2. ./.embossdata（EMBOSS 数据目录）
3. ~/(用户主目录）
4. ~/.embossdata（EMBOSS 数据目录）
5. $EMBOSS_DATA（EMBOSS 数据目录）

输出数据文件的默认构造函数如下：

```
AjPFile ajDatafileNewOutNameS (const AjPStr name);
```

ajDatafileNewOutNameS 将返回指向 EMBOSS 数据目录 ($EMBOSS_DATA) 中文件的文件对象指针。

### 6.14.7.1.3 缓冲输入文件

缓冲文件没有 ACD 数据类型，尽管有 AJAX 数据类型 (AjPFilebuff)。要使用缓冲文件，必须首先使用文件名、打开的文件或缓冲的数据行来实例化对象指针。基本构造函数如下：

```
/* Named buffered input file */
AjPFilebuff ajFilebuffNewNameS (const AjPStr name);

/* Named buffered input file and directory */
AjPFilebuff ajFilebuffNewNamePathS (const AjPStr name, const AjPStr path)

/* Named directory and wildcard filename to read all matching files */
AjPFilebuff ajFilebuffNewPathWild (const AjPStr path,
    const AjPStr wildname);

/* Named directory and wildcard filename to read all matching files with exceptions */
AjPFilebuff ajFilebuffNewPathWildExclude(const AjPStr path,
    const AjPStr wildname,
    const AjPStr exclude)

/* no file - to be loaded with data for re-reading */
AjPFilebuff ajFilebuffNewNofile (void);
```

ajFilebuffNewNofile 是一个原始构造函数，用于创建对象但不创建文件流，在 EMBOSS 的多个位置中使用，其中缓冲区将加载数据记录。示例可在处理序列数据库中找到。常用的构造函数是 ajFilebuffNewNameS，它将打开指定文件。

### 6.14.7.1.4 目录

为输入和输出提供了默认构造函数：

```
/* Directory for input */
AjPDir ajDirNewPath (const AjPStr path);

/* Directory for output */
AjPDir ajDiroutNewPath (const AjPStr path);
```

构造函数返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好实践：

```
AjPFile    filein   = NULL;
AjPFilebuff buffin  = NULL;
AjPFile    datain   = NULL;

AjPOutfile fileout  = NULL;

AjPDir     dirin    = NULL;
AjPDir     dirout   = NULL;

AjPStr     fileout_name = NULL;
AjPStr     buffin_name  = NULL;
AjPStr     dirin_name   = NULL;
AjPStr     dirout_name  = NULL;
```



fileout_name = ajStrNewC("outfile");
buffin_name = ajStrNewC("bufffile");
dirin_name = ajDirNewPath("./dirin");
dirout_name = ajDirNewPath("./dirout");

filein = ajFileNewInNameC("infile");
fileout = ajOutfileNewNameS(fileout_name);
datain = ajDatafileNewInNameC("datafile");
buffin = ajFilebuffNewNameS(buffin_name);
dirin = ajDirNewPath(dirin_name);
dirout = ajDiroutNewPath(dirout_name);

/* The objects are instantiated and ready for use */

一旦用完任何对象，就必须释放其内存。所有默认的析构函数都接受要释放的对象的地址：

```
/* File object destructor */
void ajFileClose (AjPFile* Pfile);

/* Output file object destructor */
void ajOutfileClose (AjPOutfile* Pfile);

/* Buffered file object constructor */
void ajFilebuffDel (AjPFilebuff* Pfile);

/* Directory destructor */
void ajDirDel (AjPDir* Pdir);
```

析构函数会关闭文件（如适用）并释放文件或目录对象的内存。根据上面的示例：

```
ajFileClose(&filein);
ajOutfileClose(&fileout);
ajFilebuffDel(&buffin);
ajDirDel(&dirin);
ajDirDel(&dirout);
```

对于文件列表（filelist 或 dirlist），在使用完毕后，有必要通过调用 ajListstrFreeData 来释放文件名列表（这些文件名存储为字符串）：

```
AjPList files   = NULL;
AjPList filelist = NULL;
AjIList iter    = NULL;
AjPFile infile  = NULL;
AjPStr filename = NULL;

files   = ajAcdGetFilelist("files");
filelist = ajAcdGetDirlist("directory");

/* both lists are filenames as strings */
```

```
iter = ajListIterNewread(filelist);
while(!ajListIterDone(iter))
{
    filename = (AjPStr) ajListIterGet(iter);
    infile = ajFileNewInNameS(filename);

    if(infile)
    {
        /* Do something with the file */
        ajFileClose(&infile);
    }
}
ajListIterDel(&iter);

ajListstrFreeData(&files);
ajListstrFreeData(&filelist);
```

无论目录是用于输入（directory）还是输出（outdir），在使用完毕后都必须调用目录析构函数 ajDirDel：

```
AjPDir indexoutdir = NULL;
AjPDir directory = NULL;
AjPList filelist = NULL;

indexoutdir = ajAcdGetOutdir("indexoutdir");
directory = ajAcdGetDirectory("directory");

filelist = ajListstrNew();
ajFilelistAddDirectory(filelist, directory);

/* Do something with directory or list of files */

ajDirDel(&indexoutdir);
ajDirDel(&directory);
ajListstrFreeData(&filelist);
```

## 6.14.7.3 替代对象构造和加载

下面描述的众多替代构造函数为文件对象的构造和加载提供了最大灵活性。所有构造函数都返回新对象的地址。

### 6.14.7.3.1 通用输入文件

对于 ajFileNewListinPathWild 和 ajFileNewListinPathWildExclude，文件名可以使用通配符，所有匹配的文件都将以读取方式打开。ajFileNewListinPathWildExclude 还接受第二个字符串（exclude），它是一个通配符字符串，指定要排除的文件名。ajFileNewListinNameDirS 和 ajFileNewListinDirPre 也会从目录中打开指定文件，但与上述其他函数不同，它们会添加目录对象（AjPDir）中定义的默认扩展名：

```
/* List of input file names as strings (AjPStr) */
AjPFile ajFileNewListinList (AjPList list);

/* Specify a directory object. */
AjPFile ajFileNewListinNameDirS (const AjPStr name, const AjPDir dir);

/* Specify a directory object and filename prefix. The directory object supplies the filename extension. */
AjPFile ajFileNewListinDirPre (const AjPDir dir, const AjPStr prefix);

/* Read all files matching wild card. */
AjPFile ajFileNewListinPathWild (const AjPStr name, const AjPStr path);

/* Read all files matching / excluding wild card. */
AjPFile ajFileNewListinPathWildExclude (const AjPStr name, const AjPStr path, const AjPStr exclude);

/* Read using blocked fread calls */
AjPFile ajFileNewInBlocks (const AjPStr name, ajuint blocksize);
```

以 ajFileNewFrom 为前缀的函数从其他实体构造文件对象；可以是 UNIX 管道、输入文件列表或 C 类型（FILE *）文件指针：

```
/* C-type FILE pointer. */
AjPFile ajFileNewFromCfile(FILE* file);
```

### 6.14.7.3.2 infile（数据文件）

可以通过调用以下函数从特定数据子目录读取命名的输入数据文件：

```
AjPFile ajDatafileNewInNamePathS (const AjPStr name, const AjPStr path);
```

该文件将在常规 EMBOSS 数据目录（见上文）和活动 EMBOSS 数据目录的子目录路径中查找。

### 6.14.7.3.3 缓冲输入文件

缓冲输入文件可以使用以下函数从指定目录读取，这些函数与名称相似的通用文件处理函数否则相同（见上文：）

```
/* Specify a path. */
AjPFilebuff ajFilebuffNewNamePathS (const AjPStr name, const AjPStr path);

/* Specify a path. */
AjPFilebuff ajFilebuffNewNamePathC (const char* name, const AjPStr path);

/* Read all files matching wild card. */
AjPFilebuff ajFilebuffNewPathWild (const AjPStr name, const AjPStr path);

/* Construct from all files matching / excluding wild card. */
AjPFilebuff ajFilebuffNewPathWildExclude (const AjPStr name, const AjPStr path, const AjPStr exclude);
```

缓冲输入文件可以从其他实体构造；可以是文件对象、C 类型（FILE *）文件指针、另一个缓冲输入文件（这种情况下文件会被复制）、字符串（而非文件）或文件名列表：

```
/* from an already open file */
AjPFilebuff ajFilebuffNewFromFile (AjPFile file);

/* from an already open C file */
AjPFilebuff ajFilebuffNewFromCfile (FILE* file);

/* no file, but with one line of buffered data */
AjPFilebuff ajFilebuffNewLine (const AjPStr line);

/* list of filenames to be read in turn */
AjPFilebuff ajFilebuffNewListinList(AjPList);
```

传递给 ajFilebuffNewLine 的字符串应包含一行用于读取的缓冲数据。
ajFilebuffNewFromFile 和 ajFilebuffNewFromCfile 都会接管传递的文件指针，因此在管理对象内存时，必须小心避免对同一个对象两次调用析构函数：

```
AjPFile file = NULL;
AjPFilebuff buff = NULL;

file = ajFileNewInNameC("infile");
buff = ajFilebuffNewFromCfile(file);

/* Do something with buffered file */

/* file is appropriated by buff so we only need to call one destructor (close) function
*/
ajFilebuffDel(&buff);
```

### 6.14.7.3.4 目录

可以构造目录对象，以专门读取或写入具有指定文件扩展名（ext）或指定前缀（pre）和文件扩展名的文件：

```
/* Input directory */
AjPDir ajDirNewPathExt (const AjPStr path, const AjPStr ext);
AjPDir ajDirNewPathPreExt (const AjPStr path, const AjPStr pre, const AjPStr ext);

/* Output directory */
AjPDirout ajDiroutNewPath (const AjPStr path);
AjPDirout ajDiroutNewPathExt (const AjPStr path, const AjPStr ext);
```

### 6.14.7.3.5 通用输出文件

可以在给定目录中构造命名的通用输出文件，该目录可以指定为目录对象（AjPDir）或文件路径：

```
/* Directory object. */
AjPFile ajFileNewOutNameDirS (const AjPStr name, const AjPDir dir);

/* Path. */
AjPFile ajFileNewOutNamePathS (const AjPStr name, const AjPStr path);
```

要以追加模式打开命名的通用输出文件，可以使用：

```
AjPFile ajFileNewOutappendNameS (const AjPStr name);
```

## 6.14.8 从文件读取

从通用文件读取行的函数以 ajReadline 为前缀。读取前可以保留文件位置，可以从行中修剪换行符，并且可以将行追加到提供的缓冲区：

```
/* Read a line from a file. */
AjBool ajReadline (AjPFile file, AjPStr* Pstr);

/* Read and retain file position before read. */
AjBool ajReadlinePos (AjPFile file, AjPStr* Pstr, ajlong* fpos);

/* Read and trim any trailing newline character. */
AjBool ajReadlineTrim (AjPFile file, AjPStr* Pstr);

/* Read, trim newline characters and retain file position before read. */
AjBool ajReadlineTrimPos (AjPFile file, AjPStr* Pstr, ajlong* fpos);

/* Read and append to buffer. */
AjBool ajReadlineAppend (AjPFile file, AjPStr* Pbuff);
```

要读取二进制文件，请调用：

```
/* Binary read from a file using the C 'fread' function. */
AjBool ajReadbinBinary (AjPFile file, size_t count, size_t element_size,
void* buffer);

/* Read unsigned int */
AjBool ajReadbinUint (AjPFile file, ajuint* ret);

/* Read unsigned int bigendian and converts if needed. */
AjBool ajReadbinUintEndian (AjPFile file, ajuint* ret);
```

ajReadbinBinary 将从输入文件中读取 count 个大小为 element_size 的元素。ajReadbinUint 和 ajReadbinUintEndian 读取无符号整数，并分别从 littleendian（用于二进制数据输出的形式，例如数据库索引文件）或 bigendian 进行转换。两个函数都使用 C 函数 fread。





### 6.14.8.1 缓冲文件

带有前缀 ajBuffRead 的函数从缓冲文件中读取一行。读取的行可以追加到字符串中，并且读取前的文件位置可以保留：

```c
/* Read a line from a buffered file. */
AjBool ajBuffReadLine (AjPFilebuff file, AjPStr* Pstr);

/* Read a line and note the file position. */
AjBool ajBuffReadLinePos (AjPFilebuff file, AjPStr* Pstr, ajlong* fpos);

/* Read a line and optionally append to a Pstore buffer */
AjBool ajBuffReadLinePosStore (AjPFilebuff buff, AjPStr* Pdest, ajlong* Ppos,
                               AjBool dostore, AjPStr *Pstore);
```

### 6.14.9 写入文件

### 6.14.9.1 一般文件

ajfmt.c/h 中有两个函数用于写入文件。最广泛使用的是 ajFmtPrintF，它写入 AJAX 文件对象。备选函数写入 C FILE 或标准输出：

```c
/* Format and emit the "..." arguments according to fmt; writes to a file object */
void ajFmtPrintF (AjPFile file,
                  const char *fmt, ...);

/* Format and emit the "..." arguments according to fmt; writes to C FILE stream: */
void ajFmtPrintFp (FILE *stream,
                   const char *fmt, ...);

/* Format and emit the "..." arguments according to fmt; writes to stdout */
void ajFmtPrint (const char *fmt, ...);
```

### 6.14.9.2 二进制文件

写入二进制文件的函数带有前缀 ajWritebin。单个字节、C 类型字符串（char *）或字符串对象可以写入到定义大小（len）的字段中，或者可以用正确的字节方向写入数值：

```c
/* Writes a single byte in a defined field. */
ajint ajWritebinByte (AjPFile file, char chr);
ajint ajWritebinChar (AjPFile file, const char* txt, ajint len);
ajint ajWritebinStr (AjPFile file, const AjPStr str, ajint len);

/* Writes a 2-byte integer. */
ajint ajWritebinInt2 (AjPFile file, ajlong i);

/* Writes a 4-byte integer. */
ajint ajWritebinInt4 (AjPFile file, ajlong i);
```

```c
/* Writes a 8-byte integer. */
ajint ajWritebinInt8 (AjPFile file, ajlong i);
```

### 6.14.9.3 缓冲文件

在某些情况下，有必要写入正在用于输入的缓冲文件。提供了三个函数来将行写入用于输入的缓冲文件。这些函数在内部使用，例如在读取二进制序列格式时。

```c
/* Writes a C-type string to the buffer */
void ajFilebuffLoadC (AjPFilebuff file, const char* txt);

/* Writes a string object to the buffer */
void ajFilebuffLoadS (AjPFilebuff file, const AjPStr str);

/* Writes all lines from a file into the buffer. */
void ajFilebuffLoadAll (AjPFilebuff file);
```

### 6.14.10 操作文件

提供了三个函数来设置文件对象的属性：

```c
/* Close current file and open next one. */
AjBool ajFileReopenNext (AjPFile* Pfile);

/* Reopens a file with a new name. */
FILE* ajFileReopenName (AjPFile* Pfile, const AjPStr name);

/* Sets the current position in an open file. */
ajint ajFileSeek (AjPFile* Pfile, ajlong offset, ajint from);
```

对于包含输入文件列表的文件对象，ajFileReopenNext 将关闭当前输入文件并打开下一个。成功时返回 ajTrue，否则返回 ajFalse。ajFileReopenName 调用 C 函数 freopen 来关闭当前文件并打开一个新名称的文件。ajFileSeek 本质上是 C 函数 fseek 的封装，并设置打开文件中的当前位置。在到达文件末尾并使用此函数移回文件中某个位置的情况下，文件对象中的文件末尾标志将被重置。

设置缓冲文件对象属性的函数带有前缀 ajFilebuffSet，包括：

```c
/* Sets file to be buffered. */
AjBool ajFilebuffSetBuffered (AjPFilebuff* Pfile);

/* Sets file to be unbuffered. */
AjBool ajFilebuffSetUnbuffered (AjPFilebuff* Pfile);

/* Sets next read to start at first buffered line. */
AjBool ajFilebuffReset (AjPFilebuff* Pfile);
```

```c
/* Sets next read position and resets file position. */
AjBool ajFilebuffResetPos (AjPFilebuff* Pfile);

/* Resets the pointer and current record and optionally clears Pstore buffer */
void ajFilebuffResetStore (AjPFilebuff buff, AjBool dostore, AjPStr *Pstore);

/* Deletes processed lines from a file buffer. */
AjBool ajFilebuffClear (AjPFilebuff* Pfile, ajint n);

/* Clears processed records and removes extra record(s) from the Pstore buffer */
AjBool ajFilebuffClearStore (AjPFilebuff buff, ajint lines, const AjPStr lastline,
    AjBool dostore, AjPStr *Pstore);
```

通过分别调用 ajFilebuffSetBuffered 和 ajFilebuffSetUnbuffered 可以打开和关闭文件输入的缓冲（AjPFilebuff 对象的缓冲默认处于开启状态）。带有前缀 ajFilebuffReset 的函数将下一个读取位置设置为第一个缓冲行的开头。ajFilebuffResetPos 还会将当前文件位置重置为最后已知的读取位置，以防其他函数可能更改了该位置。ajFilebuffResetStore 还会使用与 ajBuffReadLinePosStore 相同的控制参数清除调用者的已处理行记录。ajFilebuffClear 和 ajFilebuffClearStore 将删除迄今已处理的缓冲行。ajFilebuffClearStore 还会使用与 ajBuffReadLinePosStore 相同的控制参数清除调用者的已处理行记录。

### 6.14.11 查询文件属性

### 6.14.11.1 基本属性

文件对象的文件名、C 类型文件指针（FILE *）和文件长度可通过调用以下函数获取：

```c
/* File name. */
AjPStr ajFileGetNameS (const AjPFile file);

/* File name. */
const char* ajFileGetNameC (const AjPFile file);

/* C file pointer. */
FILE* ajFileGetFileptr (const AjPFile file);
```

这些函数（以及下面的其他 *获取* 函数）返回对象本身的元素（或从中计算出的值），因此在返回指针的情况下，必须小心不要意外更改对象。

带有前缀 ajFileIs 的函数检查文件是否为某个类型，或者对象是否满足其他属性：

```c
/* File is stderr. */
AjBool ajFileIsStderr (const AjPFile file);

/* File is stdin. */
AjBool ajFileIsStdin (const AjPFile file);

/* File is stdout. */
AjBool ajFileIsStdout (const AjPFile file);

/* File is set for appending. */
AjBool ajFileIsAppend (const AjPFile file);

/* File position is at end-of-file. */
AjBool ajFileIsEof (const AjPFile file);
```

这些函数（以及下面其他数据类型的 *判断* 函数）在满足条件时返回 ajTrue。

### 6.14.11.2 输出文件

可从输出文件对象中检索文件对象、来自文件对象的 C 类型文件指针（FILE *）和格式：

```c
/* File object. */
AjPFile ajOutfileGetFile (const AjPOutfile file);

/* Output format. */
AjPStr ajOutfileGetFormat (const AjPOutfile file);

/* C file pointer. */
FILE* ajOutfileGetFileptr (const AjPOutfile file);
```

### 6.14.11.3 缓冲文件

可从缓冲文件对象中检索文件对象、来自文件对象的 C 类型文件指针（FILE *）和标准记录缓冲区大小：

```c
/* File object */
AjPFile ajFilebuffGetFile (const AjPFilebuff file);

/* C file pointer from file object */
FILE* ajFilebuffGetFileptr (const AjPFilebuff file);
```

可以测试缓冲文件是否为空、是否缓冲、是否到达文件末尾，或者文件是否已耗尽（到达文件末尾且缓冲区为空）：

```c
/* File buffer is empty. */
AjBool ajFilebuffIsEmpty (const AjPFilebuff file);

/* Input file is buffered. */
AjBool ajFilebuffIsBuffered (const AjPFilebuff file);

/* File is exhausted (EOF is reached and buffer is empty). */
AjBool ajFilebuffIsExhausted (const AjPFilebuff file);

/* EOF is reached. */
AjBool ajFilebuffIsEof (const AjPFilebuff file);
```

### 6.14.11.4 目录

对于目录对象，可用于读取的文件的目录名和文件扩展名可用：

```c
AjPStr ajDirGetPath (const AjPDir Pdir);
AjPStr ajDirGetExt (const AjPDir Pdir);
AjPStr ajDirGetPrefix (const AjPDir Pdir);
```

目录对象可用于生成目录中匹配任何指定前缀和扩展名的文件的完整路径名称列表：

```c
ajint ajFilelistAddDirectory (AjPList list, const AjPDir dir);
```

### 6.14.12 查询和操作文件及目录名称

可以通过调用 ajFilenameHasPath 检查表示文件名的字符串是否包含路径，如果满足该属性则返回 ajTrue。带有前缀 ajFilenameTest 的函数测试文件名：

```c
/* Checks for path. */
AjBool ajFilenameHasPath (const AjPStr name);
```

有各种函数可以根据定义要包含或排除的文件名的通配符来测试文件名（带或不带路径规范）。默认情况下，文件名可以包含或排除。包含通配符用于选择文件，然后排除通配符用于再次排除选定的文件：

```c
/* Tests a filename. Default is to exclude */
AjBool ajFilenameTestExclude(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a full path file name. Default is to exclude. */
AjBool ajFilenameTestExcludePath(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a file name. Default is to include. */
AjBool ajFilenameTestInclude(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a full path file name. Default is to include. */
AjBool ajFilenameTestIncludePath(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);
```

有函数可以检查名为指定文件是否存在，并且处于指定模式（读取、写入或可执行）：



/* 文件存在 */
AjBool ajFilenameExists (const AjPStr filename);
/* 存在且是目录 */
AjBool ajFilenameExistsDir (const AjPStr filename);
/* 存在且可执行 */
AjBool ajFilenameExistsExec (const AjPStr filename);
/* 存在且可读 */
AjBool ajFilenameExistsRead (const AjPStr filename);
/* 存在且可写 */
AjBool ajFilenameExistsWrite (const AjPStr filename);

要返回文件大小，请调用 ajFilenameGetSize：

```
ajlong ajFilenameGetSize (const AjPStr name);
```

用于设置表示文件名的字符串的函数，如果它们从名称中删除路径和/或文件扩展名，则具有前缀 ajFilenameTrim。修剪函数包括：

```
/* 将文件名截断为基本文件名。 */
AjBool ajFilenameTrimAll (AjPStr* Pname);
/* 从文件名中删除目录路径和文件扩展名。 */
AjBool ajFilenameTrimPathExt (AjPStr* Pname);
/* 仅删除目录路径（如果有）。 */
AjBool ajFilenameTrimPath (AjPStr* Pname);
/* 仅删除扩展名（如果有）。 */
AjBool ajFilenameTrimExt (AjPStr* Pname);
```

前缀 ajFilenameReplace 的函数允许用其他值替换文件扩展名和路径。如果以其他方式设置文件名，则它们具有前缀 ajFilenameSet。例如，也可以通过调用 ajFilenameSetTempname 将文件名设置为可用的临时文件名（带可选路径）：

```
/* 设置文件扩展名。*/
AjBool ajFilenameReplaceExtS (AjPStr* Pname, const AjPStr extn);
AjBool ajFilenameReplaceExtC (AjPStr* Pname, const char* extn);
/* 设置目录路径。 */
AjBool ajFilenameReplacePathS (AjPStr* Pname, const AjPStr path);
AjBool ajFilenameReplacePathC (AjPStr* Pname, const char* path);
/* 将名称设置为带定义路径的可用临时文件名。 */
AjBool ajFilenameSetTempnamePathS (AjPStr* Pfilename, const AjPStr str);
/* 将名称设置为可用的临时文件名。 */
AjBool ajFilenameSetTempname (const char** Pname);
```

有几个用于操作表示文件路径的字符串的函数：

```
/* 将目录路径更改为上一级。 */
AjBool ajDirnameUp (AjPStr* Pname);

/* 如果缺少，则添加尾随 '/'。 */
AjBool ajDirnameFix (AjPStr* Path);

/* 检查有效路径，如果缺少则追加尾随 '/'。 */
AjBool ajDirnameFixExists (AjPStr* Ppath);

/* 检查有效路径并确保包含完整路径定义。 */
AjBool ajDirnameFillPath (AjPStr* Ppath);
```

ajDirnameFixExists 和 ajDirnameFillPath 检查指定的路径 (Ppath) 是否为有效目录。如果缺少，则会在路径末尾追加 /。ajDirnameFillPath 会根据需要向上导航目录结构并修改路径，以确保包含完整路径定义。

## 6.15 处理应用程序报告

### 6.15.1 简介

应用程序应尽可能使用标准报告格式集（参见 EMBOSS 用户指南）进行输出。每个报告定义文件中文本的内容和布局。大多数报告用于描述序列中的特征，通常是短序列基序。序列基序、ID 代码、序列位置编号及相应的特征可以以多种格式输出。一组命令行限定符（第 A.5.3.17 节，‘报告’）用于控制写入报告的数据，并设置文件名和格式等内容。因此不使用不可打印的控制字符，因此适合在屏幕上查看或打印。

报告具有一致的外观和感觉，这有助于最终用户并提高应用程序的互操作性。原则上，应用程序可以根据输出文件的用途，为不同目的使用不同的报告格式。对于最终用户，需要人类可读的报告；而如果输出要由另一个应用程序处理，则更紧凑的格式可能更合适。所有标准序列特征表格式（参见 EMBOSS 用户指南）也是报告格式。其他报告格式用于非序列信息。有关支持的报告格式的完整列表、描述和示例，请参见 EMBOSS 用户指南。

除 TAB 分隔 (excel) 格式和使用标准特征表格式的格式外，所有报告格式在报告开头都有一个参考信息块。这包括：

- 程序名称
- 生成报告的日期
- 输出文件名
- 序列的 ID 名称
- 正在报告特征的序列区域
- 报告的一些参数和统计信息

报告数据取自报告特征表。不同的报告格式从特征表中报告不同的值或不同的标记。可能报告的标记如下：

| 标记 | 描述 |
| --- | --- |
| start | 序列中匹配的起始位置 |
| end | 序列中匹配的结束位置 |
| length | 序列中匹配的长度 |
| name | 序列名称 |
| sequence | 匹配的序列 |
| strand | 特征出现的 DNA 链 |
| tagname | 特征的可打印名称 |
| tagvalue | 序列中的特征 |
| type | 特征类型 |

最后，报告末尾有一个包含摘要信息的信息块。

在内部，所有报告都以通用特征格式 (GFF) 的非常接近的类似物保存。这种灵活的文件格式以特征表中的标记/值对形式保存序列特征信息。特征可以轻松转换为任何支持的报告格式（参见 EMBOSS 用户指南），并可以通过使用 -rformat 内置限定符来选择。

GFF 有一些必须存在的字段，包括：

- 特征类型，可以是任何字符串，但最好使用序列本体论 (SO) 来指定（例如，EMBOSS 抗原使用 'SO:0001018'，因为预测特征的类型为 '表位'。使用 SO 术语允许某些报告格式，例如 GFF3 或 DAS（分布式注释系统），用生物属性正确标记特征。这些格式将任何无法识别的字符串报告为“杂项特征”或“区域”，并保留原始字符串并在特征标记中报告。
- 序列本身，可能会也可能不会根据所使用的输出报告格式进行输出。
- 特征的起始和结束位置。GFF 要求起始位置在结束位置之前，链用于标识反向的核苷酸特征。
- 分数（以防程序为特征报告分数）。

分数和大多数其他标准 GFF 标记由库自动设置为零或 NULL。如果需要，必须显式使用它们（为它们赋值），否则它们将被忽略。为了处理非标准特征值，AJAX 库使用默认的 '/note' 标记。这对程序员是透明的，除非您选择 EMBL 或另一个在其中 '/note' 标记可见的输出格式。

任何报告输出文件都应在应用程序 ACD 文件中定义，并通过调用 ajAcdGetReport 从 C 源代码中检索。需要一些编程来将数据加载到报告中并按如下所述将其写入文件。

### 6.15.2 AJAX 库文件

用于处理报告的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajreport | 应用程序报告 |

ajreport.h/c. 定义了 AjPReport 对象和用于处理报告的函数。它们还包含用于在低级别处理报告的静态数据结构和函数。除非您计划实现代码以支持 EMBOSS 的新报告格式，否则不太可能需要静态数据结构和函数。有关如何执行此操作的建议，请咨询 EMBOSS 开发人员。

### 6.15.3 AJAX 数据类型

用于处理在 ACD 文件中定义的应用程序报告输出文件，请使用：

- AjPReport 应用程序报告（用于报告 ACD 数据类型）

### 6.15.4 ACD 数据类型

用于处理报告输出的数据类型是：

- report 用于序列注释的输出文件（报告）

### 6.15.5 ACD 数据定义

报告输出的典型 ACD 定义：

```
report: outfile
[
    parameter: "Y"
    rformat: "diffseq"
    taglist: "int:start int:end int:length str:name str:sequence
    str:first_feature str:second_feature"
]
```

#### 6.15.5.1 参数名称

报告输出的所有数据定义都应具有标准参数名称（参见附录 A，ACD 语法参考）：

- outfile

- *文件





## 6.15.5.2 常用属性

通常指定的属性摘要如下。它们是特定于数据类型的（第 A.5 节，“特定于数据类型的属性”），除非它们被指示为全局属性（第 A.4 节，“全局属性”）。

- **参数**：报告通常是 EMBOSS 应用程序的主要输出，因此应使用全局属性 `parameter`: "Y" 将其定义为参数。

- **rformat**：指定要使用的报告格式，必须是受支持的报告格式之一（请参阅 *EMBOSS 用户指南*）。有一个默认的报告格式，如果用户不在命令行中使用 `-rformat` 更改它，则将使用该格式。

- **multiple**：布尔属性，如果输出可以包含来自同一输入的多个报告，则应将其设置为 "Y"。如果使用单个输入序列（`sequence` ACD 数据类型），则通常值为 "N"；如果从输入流处理多个序列（`seqall` ACD 数据类型），则值为 "Y"。

- **type**：指定报告格式是标准特征表格式之一（请参阅 *EMBOSS 用户指南*）。`type`：定义报告输出是 "protein" 还是 "nucleotide"。默认值基于任何输入序列的类型，但应始终指定一个值。

- **taglist**：定义要在输出中报告的内部特征表中的标签/值对。每个标签的一般格式为 `type:tagname`，并可（可选）附加 `[=columnname]` 以指示报告中要使用的列名：

```
`type: tagname [=columnname]`
```

例如：

```
`int:length`
`string:gc=GC%`
```

典型的 taglist 数据类型有：

- `float`
- `int`
- `str`

名称可以是任何合理的内容，但标签名称和类型 *必须* 与应用程序 C 源代码中使用的名称和类型匹配。

在给定的示例中，`int:length` 表示其中一列名为 length，并且将包含整数值。

## 6.15.6 ACD 文件处理

下面显示了通过 ACD 文件处理报告输出的数据类型和函数。

| | 编写报告 |
|---|---|
| ACD 数据类型 | report |
| AJAX 数据类型 | AjPReport |
| 从 ACD 检索 | ajAcdGetReport |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（请参阅第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.15.6.1 报告检索

要检索输出报告流，请使用 ajAcdGetReport 声明并初始化对象指针：

```
AjPReport report = NULL;
report = ajAcdGetReport( "report" );
```

### 6.15.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.15.6.3 内存和文件管理

程序结束时，关闭任何文件并释放内存是您的责任。

### 6.15.6.3.1 关闭报告文件

必须通过调用 ajReportClose 关闭任何报告文件

```
void ajReportClose (AjPReport this) ;
```

### 6.15.6.3.2 释放内存

必须对 ajAcdGetReport 调用返回的任何报告对象调用默认析构函数（见下文）。

此外，必须调用 ajReportExit 以释放为报告内务分配的任何内部内存：

```
void ajReportExit (void);
```

## 6.15.7 报告对象内存管理

### 6.15.7.1 默认对象构造

报告对象通常通过调用 ajAcdGetReport（见上文）从 ACD 文件处理中加载。因此，您永远不需要手动实例化报告对象（AjPReport）。在不太可能的情况下，如果您确实需要，则默认构造函数为：

```
AjPReport ajReportNew (void);
```

构造函数返回新报告对象的地址。在以下代码中，指针不需要初始化为 NULL，但这样做是良好的做法：

```
AjPReport       report = NULL;
report = ajReportNew();
/* The object is instantiated and ready for use */
```

### 6.15.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认析构函数为：

```
void ajReportDel (AjPReport* Preport);
```

使用方法如下：

```
AjPReport       report = NULL;
report = ajAcdGetReport("report");
...
ajReportDel(&report);
```

或者，如果您手动实例化了对象：

```
AjPReport report = NULL;
report = ajReportNew();
/* Do something with the instantiated objects */
ajReportDel(&report);
/* Done with the objects so the memory is freed. */
```

### 6.15.7.3 替代对象构造和加载

目前没有这些。

## 6.15.8 准备报告

每个报告都有标题、正文和尾部信息。准备报告以供输出的过程是：

- 1. 在 ACD 中定义合适的报告数据类型。
- 2. 在应用程序中将 ACD 报告信息收集到报告对象 (AjPReport) 中。
- 3. 使用 ajFeattableNewSeq 创建特征表对象 (AjPFeattable)。
- 4. 对于报告正文中的每一行“信息”，创建特征对象 (AjPFeature) 并使用您的数据值加载特征对象（通过使用 ajFeatNewII 和 ajFeatTagAdd）。
- 5. 设置报告标题和尾部的任何数据。
- 6. 将报告 (AjPReport) 和特征表 (AjPFeattable) 对象传递给通用报告写入函数 (ajReportWrite)。
- 7. 正常清理内存并退出。

## 6.15.9 示例报告应用程序

考虑一个简单的应用程序，用于报告序列长度和分子量。

### 6.15.9.1 ACD 文件

在以下 ACD 文件中，定义了序列输入和报告输出。datafile 数据类型只是为了可以读取 EMBOSS 数据区中的分子量数据文件。

```
application: wreport
[
    documentation: "Example report program"
]
section: input [ info: "input Section" type: page ]
sequence: sequence
[
    parameter: "Y"
    type: "Protein"
]
endsection: input
section: advanced [ info: "advanced Section" type: page ]
datafile: aadata
[
    information: "Amino acid data file"
    help: "Molecular weight data for amino acids"
    default: "Eamino.dat"
]
endsection: advanced

section: output [ info: "output Section" type: page ]

report: outfile
[
    parameter: "Y"
    rformat: "table"
    multiple: "N"
    precision: "1"
    taglist: "float:molwt int:len"
]
endsection: output
```

section: 和 endsection: 定义提供了一种方法，用于指示 GUI 在屏幕上组织 ACD 信息。每个 section 必须始终有相应的 endsection。标准做法是至少有一个输入和一个输出 section 定义，并根据需要添加其他 section。

### 6.15.9.2 C 源代码

应用程序的完整源代码如下所示。

```
/* @prog wreport ***************************************************************
**
** Show sequence length and molwt as a report
**
******************************************************************************/

int main(int argc, char **argv)

{
    AjPSeq    seq    = NULL;
    AjPReport report = NULL;
    AjPFeattable ftable = NULL;
    AjPFeature feat   = NULL;
    AjPStr    tmpstr = NULL;

    double    molwt;
    int       len;

    AjPFile   mfptr = NULL;

    embInit ("wreport", argc, argv);

    seq    = ajAcdGetSeq ("sequence");
    report = ajAcdGetReport("outfile");

    /* This bit just reads in an EMBOSS data table of molwt info */
    mfptr = ajAcdGetDatafile("aadata");

    embPropEaminoRead(mfptr);
    /* End of data file reading */

    /* Calculate the values to output */
    len   = ajSeqGetLen(seq);
    molwt = embPropCalcMolwt(ajSeqGetSeqC(seq), 0, len-1);

/* Create a feature table */
ftable = ajFeattableNewSeq(seq);

tmpstr = ajStrNew();

/* Fill head and tail information for the report */
ajFmtPrintS(&tmpstr,"This is some Header Text");
ajReportSetHeaders(report, tmpstr);

ajFmtPrintS(&tmpstr,"This is some Tail Text");
ajReportSetTails(report, tmpstr);

/* Create feature object and load with the output values */
feat = ajFeatNewII(ftable, 1, len);

ajFmtPrintS(&tmpstr,"*molwt %.1f", (float)molwt);
ajFeatTagAdd(feat,NULL,tmpstr);

ajFmtPrintS(&tmpstr,"*len %d", len);
ajFeatTagAdd(feat,NULL,tmpstr);

/* Write report and clean up */
ajReportWrite(report, ftable, seq);

ajFeattableDel(&ftable);
ajStrDel(&tmpstr);
ajFileClose(&mfptr);

embExit();
return 0; }
```

首先定义变量。需要序列 (AjPSeq) 和特征表 (AjPFeattable) 对象来保存包含列值的特征对象。还需要单个特征 (AjPFeature) 对象来包含将在报告中打印的值。需要一些内务变量，当然还有报告本身 (AjPReport)：

```
AjPSeq      seq      = NULL;    /* Input sequence      */
AjPReport   report   = NULL;    /* Output report       */
AjPFeattable ftable   = NULL;    /* Feature table       */
AjPFeature  feat     = NULL;    /* Individual feature  */
AjPStr      tmpstr   = NULL;

double      molwt;
int         len;

AjPFile     mfptr    = NULL;
```

然后可以初始化程序并处理 ACD 文件：

```
embInit ("wreport", argc, argv);

seq      = ajAcdGetSeq ("sequence");
report   = ajAcdGetReport("outfile");
```





然后需要代码来读取包含氨基酸分子量数据的EMBOSS数据文件，并计算要报告的分子量和长度值。请注意，len和molwt既用作变量名，也用作列名。这不是必须的，但能使代码更清晰：

```
mfptr = ajAcdGetDatafile("aadata");
embPropEaminoRead(mfptr);
len = ajSeqGetLen(seq);
molwt = embPropCalcMolwt(ajSeqGetSeqC(seq),0,len-1);
```

然后设置报告的头部和尾部信息。这可以在ajAcdGetReport之后、报告打印之前的任何时间完成。它们是可选的，但推荐使用。为此使用临时字符串对象：

```
tmpstr = ajStrNew();
ajFmtPrintS(&tmpstr,"This is some Header Text");
ajReportSetHeaderS(report, tmpstr);
ajFmtPrintS(&tmpstr,"This is some Tail Text");
ajReportSetTailS(report, tmpstr);
```

然后创建特征表对象。每个报告只需要一个特征表。将序列对象作为参数传递，以便序列名称可以自动加载到内部GFF格式中。现在可以创建一个特征对象，用于加载列值。每个输出值都使用一个带有标签/值对的单个特征对象。列值被打印到一个字符串对象（tmpstr）中，该对象用于加载特征对象。

ajFeatNewII需要三个参数。第一个是特征表对象，最后两个是序列的起始和结束位置。相当调皮地，在本示例中它们被硬编码了（如上所述）。最终报告的每一行输出都必须创建一个特征对象。ajFeatTagAdd用于将分子量和长度值加载到特征对象中：

```
ftable = ajFeattableNewSeq(seq);
feat = ajFeatNewII(ftable,1,len);
ajFmtPrintS(&tmpstr,"*molwt %.1f", (float)molwt);
ajFeatTagAdd(feat,NULL,tmpstr);
ajFmtPrintS(&tmpstr,"*len %d", len);
ajFeatTagAdd(feat,NULL,tmpstr);
```

这里是ACD列名（molwt和len）必须与ajFmtPrintS调用中的列名匹配的部分。在C程序中，这些名称前必须加上星号（*）。ACD文件中指定的数据类型（float和int）也必须与C代码中给出的类型匹配。NULL参数仅表示只添加一个值（库会自动添加/note标签）。

现在可以写入报告了。传递了三个对象。传递序列对象的原因是，以防你选择一种打印所用（子）序列的报告格式：

```
ajReportWrite(report, ftable, seq);
```

最后，在退出前进行清理以回收动态内存：

```
ajFeattableDel(&ftable);
ajStrDel(&tmpstr);
ajFileClose(&mfptr);
embExit();
return 0;
```

### 6.15.10 报告文件管理

作为ACD处理的替代方案，可以通过调用ajReportOpen直接打开报告文件。报告文件通过调用ajReportClose关闭：

```
AjBool ajReportOpen (AjPReport thys, const AjPStr name);
void ajReportClose (AjPReport thys);
```

要向报告添加额外的文件名和描述，请调用ajReportAddFileF：

```
void ajReportAddFileF (AjPReport report, AjPFile file, const AjPStr type);
```

文件名和类型将作为“附加文件”列在报告标题中，以让用户知道有关联的输出文件可用。

要写入报告文件，请调用ajReportWrite：

```
AjBool ajReportWrite (AjPReport report, const AjPFeattable ftable, const AjPSeq seq);
```

该函数为给定序列（seq）的特征表对象（ftable）写入报告文件（report）。如果已写入数据则返回ajTrue，如果已达到最大输出则返回ajFalse。准备报告所需的步骤将在下面详细描述。

可以通过调用ajReportWriteHeader或ajReportWriteTail分别写入报告标题和尾部。这些函数以正在报告的序列对象作为参数：

```
void ajReportWriteHeader (AjPReport report, const AjPFeattable ftable, const AjPSeq seq);
void ajReportWriteTail (AjPReport report, const AjPFeattable ftable, const AjPSeq seq);
```

通常您永远不需要调用这些函数，因为在调用ajReportWrite时，标题和尾部会自动写入。

### 6.15.11 设置报告对象的元素

本节中的函数用于直接设置报告对象中的元素。

要将一些初始文本（标题）设置为报告标题或子标题，请调用ajReportSetHeaders或ajReportSetSubheaders：

```
void ajReportSetHeaders (AjPReport report, const AjPStr header);
void ajReportSetHeaderC (AjPReport report, const char* header);
void ajReportSetSubheaders (AjPReport report, const AjPStr header);
void ajReportSetSubheaderC (AjPReport report, const char* header);
```

要将一些文本追加到报告标题或子标题中，请调用ajReportAppendHeaders或ajReportAppendSubheaders：

```
void ajReportAppendHeaders (AjPReport report, const AjPStr header)
void ajReportAppendHeaderC (AjPReport report, const char* header);
void ajReportAppendSubheaders (AjPReport report, const AjPStr header)
void ajReportAppendSubheaderC (AjPReport report, const char* header);
```

要将一些尾随文本（尾部）设置为报告尾部或子尾部，请调用ajReportSetTails或ajReportSetSubtails：

```
void ajReportSetTails (AjPReport report, const AjPStr tail);
void ajReportSetTailC (AjPReport report, const char* tail);
void ajReportSetSubtails (AjPReport report, const AjPStr tail);
void ajReportSetSubtailC (AjPReport report, const char* tail);
```

要将一些文本追加到报告尾部或子尾部中，请调用ajReportAppendTails或ajReportAppendSubtails：

```
void ajReportAppendTails(AjPReport report, const AjPStr tail)
void ajReportAppendTailC (AjPReport report, const char* tail);
void ajReportAppendSubtails (AjPReport report, const AjPStr tail)
void ajReportAppendSubtailC (AjPReport report, const char* tail);
```

要设置报告的标签列表，请调用ajReportSetTagsS：

```
AjBool ajReportSetTagsS (AjPReport report, const AjPStr taglist);
```

如果尚未设置报告类型，请调用ajReportSetType：

```
void ajReportSetType (AjPReport report, const AjPFeattable ftable, const AjPSeq seq);
```

要设置特征报告的默认格式，请调用ajReportFormatDefault：

```
AjBool ajReportFormatDefault (AjPStr* pformat);
```

### 6.15.12 获取报告对象的元素

有时需要查询报告对象的属性。虽然您通常不需要本节中的函数，但如果您手动创建了报告对象（使用构造函数），而不是从ACD处理中获取一个，则这些函数很有用。

要根据报告对象中的设置（源自ACD和命令行-rusashow选项）返回序列名称或USA，请调用ajReportGetSeqnameSeq：

```
const AjPStr ajReportGetSeqnameSeq (const AjPReport report, const AjPSeq seq);
```

### 6.15.13 调试报告对象

要测试报告是否有效，请调用：

```
AjBool ajReportValid (AjPReport report);
```

这将检查指定的格式是否与标签数量以及序列的类型（蛋白质或核苷酸）兼容。如果序列格式尚未定义，则会设置序列格式。

要打印当前报告格式的信息，请调用ajReportPrintFormat。如果full参数为ajTrue，则会生成所有报告格式的信息：

```
void ajReportPrintFormat (AjPFile outf, AjBool full);
```

## 6.16 处理列表

### 6.16.1 简介

AJAX提供用于实现双向链表并对其进行迭代的对象。提供了您期望的所有基本功能。这包括：

- 不删除的节点获取（窥视）
- 列表迭代，以在列表中向前和向后移动
- 列表查询，以返回由提供的查询函数识别的节点
- 列表编辑，用于从列表中添加（push）和删除（pop）节点，将整个列表推入另一个列表并反转节点顺序
- 垃圾回收，用于删除由提供的查询函数识别的节点
- 对节点数据中最多三个字段（C数据结构元素）进行列表排序
- 列表到数组转换
- 在列表节点上调用提供的函数进行列表处理





列表和列表迭代器对象直接从 C 源代码创建和处理。`list` ACD 数据类型不用于通用列表；它用于处理菜单中的选择。

## 6.16.2 AJAX 库文件

用于处理列表的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：

`http://emboss.open-bio.org/rel/dev/libs/`

| 库文件文档 | 描述 |
| --- | --- |
| ajlist | 通用列表处理 |

`ajlist.h/c`。您可能需要的所有用于创建和控制链表的函数。它们定义了基本列表对象（`AjPList`），其中包含作为嵌套子结构的列表节点对象（`AjPListNode`）以及列表迭代对象（`AjIList`）。它还包括用于在低级别处理列表的静态数据结构和函数。除非您计划实现代码以扩展库的核心功能，否则不太可能需要低级代码。

## 6.16.3 ACD 数据类型

没有专门用于处理通用列表的 ACD 数据类型，`list` ACD 数据类型用于处理菜单中的选择（参见第 6.19 节，“处理菜单”）。对于数值数组，可以使用 `array` 数据类型（参见第 6.17 节，“处理数组”）。

## 6.16.4 用于处理列表的 AJAX 数据类型

用于处理列表的 AJAX 数据类型有三种：

- `AjPList`：基本链表
- `AjPListNode`：链表中的节点，作为嵌套子结构包含在 `AjPList` 中
- `AjIList`：用于列表迭代。

## 6.16.5 列表类型

函数处理包含指向节点数据的指针变量的节点列表。通用列表处理函数具有 `void *` 参数，在传递参数时必须将其转换为正确的类型。为方便起见，提供了一组专门用于处理字符串列表的函数，这些函数会转换为适当的类型。此类函数都带有前缀 `ajListstr`，以将其与通用函数（带有前缀 `ajList`）区分开来。

## 6.16.6 列表对象内存管理

### 6.16.6.1 默认对象构造

要使用列表，必须首先实例化列表对象指针。默认构造函数分配一个空列表（无节点或节点数据）：

```
/* Default generic list constructor */
AjPList ajListNew (void)

/* Default string list constructor */
AjPList ajListstrNew (void);
```

所有构造函数都返回新列表的地址。指针不需要初始化为 NULL，但最好这样做：

```
AjPList list = NULL;
AjPList liststr = NULL;

list = ajListNew();
liststr = ajListstrNew();

/* The objects are instantiated and ready for use */
```

### 6.16.6.2 默认对象销毁

使用完列表后，必须释放其内存。默认析构函数会释放列表和节点，但不会释放节点数据本身：

```
/* Default generic list destructor */
AjPList ajListFree (AjPList* Plist);

/* Default string list destructor */
AjPList ajListstrFree (AjPList* Plist);
```

对象销毁的典型代码如下：

```
AjPList list = NULL;
AjPList liststr = NULL;

list = ajListNew();
liststr = ajListstrNew();

/* The objects are instantiated and ready for use ... do something with the list */

ajListFree(&list);
ajListFree(&liststr);

/* The lists are freed and the pointers reset to NULL, ready for reuse. */
```

```
list = ajListNew();
liststr = ajListstrNew();

/* The pointer variable is reallocated. Do something else with the new lists. */

ajListFree(&list);
ajListstrFree(&liststr);

/* Free the lists once you are done with them. */
```

### 6.16.6.3 管理节点数据

在实际操作中，您会为列表中的节点分配数据，使用完后必须释放这些数据。必须小心，不要在程序中丢失对节点数据的句柄（C 指针），不要忘记释放节点，也不要尝试释放两次节点数据。这些都是容易犯的错误。

在以下示例中，两个字符串（str1 和 str2）分别使用 ajListPushAppend 和 ajListstrPushAppend 被推送到通用列表（list）和字符串列表（liststr）中。这仅用于说明目的。在实际操作中，您始终应使用列表字符串函数（ajListstr*）来处理字符串列表：

```
AjPList   list   = NULL;
AjPList   liststr = NULL;
AjPStr    str1   = NULL;
AjPStr    str2   = NULL;
AjPStr    strtmp = NULL;
AjIList   iter   = NULL;

/* Create the strings and lists */
str1 = ajStrNewC("String 1");
str2 = ajStrNewC("String 2");

list   = ajListNew();
liststr = ajListstrNew();

/* Push the strings onto the generic list. The strings must be cast to void *. */
ajListPushAppend(list, (void *)str1);
ajListPushAppend(list, (void *)str2);

/* Push the same strings onto the string list. The cast is not needed. */
ajListstrPushAppend(liststr, str1);
ajListstrPushAppend(liststr, str2);
```

由于相同的两个字符串被推送到两个列表中，因此两个字符串对象和两个列表都需要释放。仅对于字符串列表，有一个析构函数可以释放列表 *和* 列表引用的节点数据（字符串）：

```
/* String list and nodes destructor */
AjPList ajListstrFreeData (AjPList* Plist);
```

因此，上述代码分配的内存可以按以下方式释放：

```
/* Free the string list and strings using ajListstrFreeData. Free the generic list
using ajListFree */
ajListFree(&list);
ajListstrFreeData(&liststr);

/* All memory is freed now and the list pointers are set to NULL and ready for reuse. */
```

对于通用列表，必须手动释放节点数据。以下代码很典型，它使用列表迭代器对象（iter）通过 ajListIterGet 遍历列表，并对每个节点依次调用析构函数（在此示例中为字符串析构函数）。除了使用 ajListstrFreeData，上述代码分配的内存也可以按以下方式释放：

```
/* Iterate through the list deleting the node data */
iter = ajListIterNew(list);

while(strtmp = (AjPStr) ajListIterGet(iter))
    ajStrDel(&strtmp);

/* Free the list and list iterator */
ajListIterDel(&iter);
ajListFree(&list);
```

### 将所有内容整合在一起：

```
AjPList list = NULL;
AjPList liststr = NULL;
AjPStr str1 = NULL;
AjPStr str2 = NULL;
AjPStr strtmp = NULL;
AjIList iter = NULL;

/* Create the strings and lists */
str1 = ajStrNewC("String 1");
str2 = ajStrNewC("String 2");

list = ajListNew();
liststr = ajListstrNew();

/* Push the strings onto the generic list. The strings must be cast to void *. */
ajListPushAppend(list, (void *)str1);
ajListPushAppend(list, (void *)str2);

/* Push the same strings onto the string list. The cast is not needed. */
ajListstrPushAppend(liststr, str1);
ajListstrPushAppend(liststr, str2);

/* Free the string list and strings using ajListstrFreeData. Free the generic list
using ajListFree */
ajListFree(&list);
ajListstrFreeData(&liststr);

/* All memory is freed now and the list pointers are set to NULL and ready for
reuse. */

/* Re-allocate the strings and push them onto the generic list. */
str1 = ajStrNewC("String 1");
```

```
str2 = ajStrNewC("String 2");

list = ajListNew();
ajListPushAppend(list, (void *)str1);
ajListPushAppend(list, (void *)str2);

/* Iterate through the list deleting the node data */
iter = ajListIterNew(list);
while(strtmp = (AjPStr) ajListIterGet(iter))
    ajStrDel(&strtmp);

/* Free the list and list iterator */
ajListFree(&list);
ajListIterDel(&iter);

/* All memory is freed now */
```

### 6.16.6.4 替代对象构造和加载

提供了各种替代构造函数和析构函数。对于构造函数，您必须知道函数是仅复制节点（节点数据在两个列表之间共享），还是将节点和节点数据从一个列表物理复制到另一个列表。同样，对于析构函数，您必须区分是仅删除列表，还是删除列表和节点数据。

### 6.16.6.4.1 列表复制

用于复制节点列表但不复制节点数据本身的函数包括：

```
/* Copy a generic list */
AjPList ajListNewListref (const AjPList list);

/* Copy a string list */
ajListstrNewListref (const AjPList list);
```

在以下示例中，ajListstrNewListref 用于复制列表：

```
AjPList list = NULL;
AjPList listcopy = NULL;
AjPStr str1 = NULL;
AjPStr str2 = NULL;

/* Create a list of strings */
list = ajListNew();
str1 = ajStrNewC("String 1");
str2 = ajStrNewC("String 2");
ajListPushAppend(list, (void *)str1);
ajListPushAppend(list, (void *)str2);

/* Copy the list */
listcopy = ajListstrNewListref(list);

/* Do something with the lists */

/* Free the original list and node data */
```





```
ajListstrFreeData(&list);

/* Free the copy of the list */
ajListstrFree(&listcopy);
```

### 6.16.6.4.2 列表创建（来自提供的节点数据）

遍历数据并使用 ajListPushAppend 调用。

例如，要从两个序列创建列表：

```
AjPList  list  = NULL;
AjPSeq   seq1  = NULL;
AjPSeq   seq2  = NULL;
AjPSeq   seqtmp = NULL;
AjIList  iter  = NULL;

/* Create the sequences */
list = ajListNew();
seq1 = ajSeqNewNameC("AAAAAAAAAA");
seq2 = ajSeqNewNameC("LLLLLLLLLL");

/* Create the list */
list = ajListNew();
ajListPushAppend(list, seq1);
ajListPushAppend(list, seq2);

/* Do something with the lists */

/* Free the list and node data */
iter = ajListIterNew(list);

while(seqtmp = (AjPSeq) ajListIterGet(iter))
    ajSeqDel(&seqtmp);

ajListFree(&list);
```

## 6.16.7 列表节点检索

提供了从列表中返回节点而不删除它的函数。可以返回当前节点、第一个节点、最后一个节点或编号节点：

```
/* Retrieve the current node in a generic list */
AjBool ajListPeek (const AjPList list, void** Pptr);

/* Retrieve the current node in a string list */
AjBool ajListstrPeek (const AjPList list, AjPStr* Pstr);

/* Retrieve the nth node in a generic list */
AjBool ajListPeekNumber (const AjPList list, void** Pptr, ajint n);

/* Retrieve the first node in a generic list */
AjBool ajListPeekFirst (const AjPList list, void** Pptr);

/* Retrieve the last node in a generic list */
AjBool ajListPeekLast (const AjPList list, void** Pptr);
```

如果成功检索节点，所有函数都返回 ajTrue，并使用适当的对象指针来获取检索到的节点。例如，这里检索序列列表中的第一个节点。未显示创建序列列表的代码：

```
AjPSeq seqtmp = NULL;
AjPList list = NULL;

... /* Code to allocate list of sequences */

if(ajListPeekFirst(list, &seqtmp))
    /* Do something with list */;
else
    /* Error handling */;
```

## 6.16.8 列表迭代

### 6.16.8.1 列表迭代器构建

要遍历列表，必须首先构建一个列表迭代对象。为此有四个函数：

```
/* Default list iterator constructor, start to end iteration. */
AjIList ajListIterNew (AjPList list);

/* Start to end iteration through read-only list */
AjIList ajListIterNewread (const AjPList list);

/* End to start iteration */
AjIList ajListIterNewBack (AjPList list);

/* End to start iteration through read-only list */
AjIList ajListIterNewreadBack (const AjPList list);
```

您已经接触过 ajListIterNew。其他函数的使用方式完全相同，只是它们设置迭代器以从只读列表读取（ajListIterNewread）、从列表末尾到开头进行迭代（ajListIterNewBack）或从只读列表末尾到开头进行迭代（ajListIterNewreadBack）。

### 6.16.8.2 列表迭代

可以为列表迭代构建灵活的控制语句。有三个函数用于从头到尾遍历列表：

```
/* Returns the next item in a list */
void* ajListIterGet (const AjIList iter);

/* Returns true if iteration is complete */
AjBool ajListIterDone (const AjIList iter);
```

您已经使用过 ajListIterGet 来返回列表中的下一项（如果到达列表末尾则为 NULL）。如果迭代已完成，ajListIterDone 将返回 ajTrue。

另外三个函数具有相同的功能，但用于从列表末尾到开头进行迭代：

```
/* As above, but end to start iteration */
void* ajListIterGetBack (const AjIList iter);
/* As above, but end to start iteration */
AjBool ajListIterDoneBack (const AjIList iter);
```

### 6.16.8.3 列表迭代器销毁

如您已经看到，使用完列表迭代器后，必须使用以下方式销毁该对象：

```
void ajListIterDel (AjIList* Piter);
```

## 6.16.9 查询列表

要搜索列表并确定是否有节点根据给定函数匹配，请使用：

```
/* Search a generic list */
AjBool ajListMap (const AjPList list, AjBool apply(void** Pptr, void* cl);
/* Search a string list */
AjBool ajListStrMap (const AjPList list, AjBool apply(AjPStr* Pstr), void* cl);
```

必须提供搜索函数，其类型与垃圾回收中使用的比较函数相同（见下文）。cl 参数通常为 NULL，但可用于向函数传递外部数据。使用相同的示例，如果使用的匹配函数是：

```
AjBool Compare(const void * ptr, void* cl)
{
   if(ajSeqGetLen((AjPSeq)ptr) > 1000)
      return ajTrue;
   return ajFalse;
}
```

如果任何节点是长度大于 1000 的序列，则 ajListMap 将返回 ajTrue：

```
if (ajListMap(list, Compare, NULL))
/* List contains a sequence > 1000 residues */;
else
/* List does not contain such a sequence */;
```

## 6.16.10 列表编辑

提供了几个基本的列表编辑函数。这些包括：

- 从列表开头或结尾弹出一个节点
- 将节点推入列表开头或结尾
- 将整个节点列表推入另一个列表
- 在列表中的任何位置添加或删除列表节点
- 反转列表中节点的顺序

### 6.16.10.1 向列表添加节点

以下函数向列表添加节点（字符串列表有等效函数）：

```
/* Push a node onto the start of a list */
void ajListPush (AjPList list, void* ptr);

/* Push a node onto the end of a list */
void ajListPushAppend (AjPList list, void* ptr);

/* Push a list of nodes onto the start of a list */
void ajListPushlist (AjPList list, AjPList* Plist);

/* Insert a node into a list using an iterator */
void ajListIterInsert (AjPIter iter, void* ptr);
```

ajListPushlist 会删除节点来源的列表，因此必须小心不要尝试两次删除节点数据。在以下示例中，所有内存都被正确释放：

```
AjPList list = NULL;
AjPList listnew = NULL;
AjPSeq seq1 = NULL;
AjPSeq seq2 = NULL;
AjPSeq seqtmp = NULL;
AjPIter iter = NULL;

/* Create a list of sequences */
list = ajListNew();
seq1 = ajSeqNewNameC("AAAAAAAAAA", "seqA");
seq2 = ajSeqNewNameC("CCCCCCCCCC", "seqC");

ajListPushAppend(list, seq1);
ajListPushAppend(list, seq2);

/* Create a new list and add the nodes to it (the original list is deleted) */
listnew = ajListNew();
ajListPushList(list, &listnew);

/* Free the list and node data */
iter = ajListIterNew(listnew);

while(seqtmp = (AjPSeq) ajListIterGet(iter))
ajSeqDel(&seqtmp);

ajListFree(&listnew);
```

ajListIterInsert 将在传递的列表迭代器当前位置向列表插入一个节点。在此示例中，将新序列插入列表中间：

```
AjPList  list = NULL;
AjPSeq   seq1 = NULL;
AjPSeq   seq2 = NULL;
AjPSeq   seq3 = NULL;
AjIList  iter = NULL;

/* Create a list from seq1 and seq3 */
list = ajListNew();
seq1 = ajSeqNewNameC("AAAAAAAAAA");
seq3 = ajSeqNewNameC("CCCCCCCCCC");
ajListPushAppend(list, seq1);
ajListPushAppend(list, seq3);

iter = ajListIterNew(list);

while(seqtmp = (AjPSeq) ajListIterGet(iter))
{
    /* Insert a new node once node with sequence "CCCCCCCCCC" is found */
    if(ajStrMatchC(ajSeqGetSeqS(seqtmp), "CCCCCCCCCC"))
    {
        seq2 = ajSeqNewNameC("BBBBBBBBBB");
        ajListIterInsert(iter, (void *) seq2);
        break;
    }
}

/* The order of sequences in the list is now seq1, seq2, seq3 */
```

### 6.16.10.2 从列表删除节点

以下函数从列表删除节点（字符串列表有等效函数）：

```
/* Pop a node from the start of a list */
AjBool   ajListPop (AjPList list, void** Pptr);

/* Pop a node from the end of a list */
AjBool ajListPopLast (AjPList list, void** Pptr);

/* Remove current node at a list iterator position */
void ajListIterRemove (AjIList iter);
```

ajListIterRemove 只是删除传递的列表迭代器当前位置的节点。必须小心不要丢失对节点数据的句柄并意外创建内存泄漏，这就是为什么在此示例中（承接上述代码），序列 seq3 被显式删除：

```
iter = ajListIterNew(list);
while(seqtmp = (AjPSeq) ajListIterGet(iter))
{
    /* Simply delete the node */
    if(ajStrMatchC(ajSeqGetSeqS(seqtmp), "CCCCCCCC"))
    {
        ajListIterRemove(iter); /* Delete the node */
        ajSeqDel(&seqtmp); /* Delete the node data to avoid a memory leak */
        break;
    }
}
```

相比之下，使用 ajListPop 或 ajListPopLast 弹出节点时，数据由第二个参数捕获，处理完后应将其释放：

```
...
ajListPopLast(list, &seqtmp);
/* Do something with the popped sequence before deleting it */
ajSeqDel(&seqtmp);
```

### 6.16.10.3 反转列表中节点的顺序

要反转列表中节点的顺序，请使用：

```
void ajListReverse (AjPList list); /* Generic list */
void ajListstrReverse (AjPList list); /* String list */
```

### 6.16.10.4 垃圾回收

可以对列表执行垃圾回收以删除其节点数据满足特定约束的节点。使用 ajListPurge，它接受三个参数：要清理的列表（list）、用于检查约束的比较函数（test）以及用于删除节点数据的析构函数（nodedelete）：

```
void ajListPurge (AjPList list,
AjBool (*test)(const void *),
void (*nodedelete)(void **));
```





必须提供比较函数和析构函数。从原型可以看出，比较函数返回一个 AjBool（如果约束匹配则为 ajTrue），并接受一个通用的 void * 参数，而析构函数必须是 void 返回类型，并接受一个通用的 void ** 参数。

假设你有一个序列（AjPSeq）对象列表需要进行垃圾回收，要从列表中删除所有长度超过 1000 个字符的序列。比较函数如下：

```
AjBool Compare(const void * ptr)
{
    if(ajSeqGetLen((AjPSeq)ptr) > 1000)
        return ajTrue;

    return ajFalse;
}
```

我们不能使用默认的序列析构函数，因为其参数类型不正确：

```
void ajSeqDel (AjPSeq* Pseq);
```

需要一个 const 指针，这意味着你必须在默认析构函数周围提供一个包装函数：

```
void mySeqDelWrap(const void **ptr)
{
    ajSeqDel((AjPSeq *) ptr);

    return;
}
```

要对序列列表（list）执行垃圾回收，你将调用：

```
void ajListPurge (list, Compare, mySeqDelWrap);
```

### 6.16.11 列表排序

列表可按节点数据中的最多三个字段（C 数据结构的元素）进行排序。当使用多个字段时，列表首先按字段 1 排序。字段 1 排序顺序相同的节点随后按字段 2 重新排序，以保持字段 1 的相对排序顺序。同样，如果使用第三个字段，字段 1 和 2 排序顺序相同的节点将按字段 3 重新排序，以保留按字段 1 和 2 排序后的相对顺序。函数如下：

```
void ajListSort (AjPList list,int (*sort1) (const void*, const void*));
void ajListSortTwo (AjPList list,int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*));
void ajListSortTwoThree (AjPList list,int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*),
int (*sort3) (const void*, const void*));
```

列表还可以按最多两个字段排序并删除重复节点（排序顺序相同的节点）。函数如下：

```
void ajListSortUnique (AjPList list,
int (*compar) (const void*, const void*),
void (*nodelete)(void**, void*));
void ajListSortTwoUnique(AjPList list,
int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*),
void (*nodelete)(void**, void*));
```

必须提供一个或多个比较函数 sort*。这些函数接受两个传递对象的通用 void * 参数，并以整数形式返回对象的排序顺序：如果第一个对象排序高于第二个对象，则应为 -1，否则为 +1。对于 ajListSortUnique* 函数，析构函数与 ajListMap（见上文）相同：它必须是 void 返回类型，并接受一个通用 void ** 参数和一个（通常为 NULL）第二个参数，该参数可用于向函数传递外部数据。

假设你有一个序列（AjPSeq 对象）列表，想要按长度（最短优先）排序并使其唯一，删除列表中长度与另一个序列相同的任何序列，使最终序列列表具有唯一长度。比较函数如下：

```
int Compare(const void *ptr1, const void * ptr2)
{
    if(ajSeqGetLen((AjPSeq)ptr1) < ajSeqGetLen((AjPSeq)ptr2))
        return -1;
    return 1;
}
```

析构函数与上述列表删除回收中的相同。

要对列表进行排序并删除重复长度的序列，你将调用：

```
void ajListSortUnique (list, Compare, mySeqDelWrap);
```

### 6.16.11.1 字符串比较函数

ajstr.c 中提供了各种字符串比较函数，可用于对字符串列表进行排序。这些函数执行区分大小写和不区分大小写的比较，支持带通配符和不带通配符的字符。函数的变体支持字符串对象（AjPStr）和 C 类型（char *）字符串（未全部显示）：

```
/* String to C-type string */
int ajStrCmpC (const AjPStr thys, const char *text);

/* String to string */
int ajStrCmpS (const AjPStr str, const AjPStr str2);

/* Case-insensitive string to string */
int ajStrCmpCaseS (const AjPStr str1, const AjPStr str2);

/* String to C-type string using the first len characters only */
ajint ajStrCmpLenC (const AjPStr thys, const char *text, ajuint len);

/* String to string using the first len characters only */
int ajStrCmpLenS (const AjPStr str, const AjPStr str2, ajuint len);

/* String to C-type string with wildcards.*/
int ajStrCmpWildC (const AjPStr thys, const char* text);

/* String to string with wildcards.*/
int ajStrCmpWildS (const AjPStr thys, const AjPStr str);

/* Case-insensitive string to C-type string with wildcards.*/
int ajStrCmpWildCaseC (const AjPStr thys, const char* text);

/* Case-insensitive string to string with wildcards.*/
int ajStrCmpWildCaseS (const AjPStr thys, const AjPStr str);

/* Same as ajStrCmpS but strings are cast as void */
int ajStrVcmp (const void* str1, const void* str2);
```

还有用于处理 C 类型字符串的比较函数：

```
/* Case-insensitive C-type string to C-type string */
int ajCharCmpCase (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C-type string using the first len characters only */
int ajCharCmpCaseLen (const char* txt1, const char* txt2, ajuint len);

/* C-type string to C-type string using wildcards. */
ajint ajCharCmpWild (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C type string using wildcards. */
ajint ajCharCmpWildCase (const char* txt1, const char* txt2);
```

这些函数返回一个表示排序顺序的整数：如果第一个字符串应排在第二个字符串之前，则为 -1；如果第二个字符串应排在第一个字符串之前，则为 +1；如果两者相同，则为 0。

### 6.16.12 列表转换

可以使用以下方法将列表转换为数组：

```
ajint ajListToarray (const AjPList list, void*** PParray);
ajint ajListstrToarray (const AjPList list, AjPStr** PParray);
```

可以使用以下方法将字符串列表追加到现有数组：

```
ajint ajListstrToarrayAppend (const AjPList list, AjPStr** PParray);
```

这些函数返回数组的大小，在所有情况下，数组内存会根据需要（重新）分配，原始列表保持不变。节点数据不会被复制，因此这些函数返回后，必须释放列表、数组和节点数据。下面的示例中未显示创建序列列表的代码：

```
AjPSeq *seqarray = NULL;
AjPList list = NULL;
AjPSeq seqtmp = NULL;
AjIList iter = NULL;

... /* Code to allocate list of sequences */

ajListToarray(list, &seqarray);

/* Do something with the array */

/* Free the list and node data */
iter = ajListIterNew(list);

while(seqtmp = (AjPSeq) ajListIterGet(iter))
    ajSeqDel(&seqtmp);

ajListFree(&list);

/* Delete the iterator */
ajListIterDel(&iter);

/* Free the array */
AJFREE(seqarray);
```

### 6.16.13 列表节点函数

要在列表的所有节点上调用函数，请使用以下之一：

```
void ajListMap (AjPList list, void apply(void** Pptr, void* ptr), void* cl);
void ajListstrMap (AjPList list, void apply(AjPStr* Pstr, void* ptr), void* cl);
void ajListMapread (const AjPList list, void apply(void* ptr, void* cl), void* cl);
void ajListstrMapread (const AjPList list, void apply(AjPStr str, void* ptr), void* cl);
```

应用的函数再次与用于垃圾回收的比较函数类型相同（见上文）。*MapRead 函数确保应用的函数（apply）不会修改列表元素，因此接受一个 const 列表。相比之下，ajListMap 和 ajListstrMap 允许任何类型的操作。

## 6.17 处理数组

### 6.17.1 简介

在 EMBOSS 中，数组处理大大简化。AJAX 提供了动态数组对象，可根据需要自动增长，从而省去了你自己管理内存的麻烦。这使你的代码更简洁且不易出错。提供了用于处理以下 C 数据类型的各种维度（1D、2D 或 3D）数组的对象：

- 字符（char）
- 短整数（ajshort）
- 无符号整数（ajuint）
- 整数（ajint）
- 浮点数（float）
- 长浮点数（ajlong）
- 双精度浮点数（double）。

对象可以分配到默认或指定的保留大小。每个对象都会跟踪可用的保留空间（以防调用必须扩展数组的函数）和数组的实际长度。高维数组可以嵌套低维数组。

提供了用于返回当前长度以及获取和设置数组元素的函数。数组元素应仅使用这些函数访问。如果你向超出当前数组大小的元素赋值，则数组将动态重新分配到足够大的大小以容纳新元素。相比之下，如果你尝试检索超出当前数组大小的元素，将生成一个错误。

如果需要，可以从任何数组对象中检索 C 类型数组。这允许使用标准数组表示法访问数组元素。提供了以各种方式对整数、无符号整数和浮点数的 C 类型数组进行排序的函数。

数组对象通常直接在 C 源代码中创建。但是，浮点数组可以在 ACD 文件（数组 ACD 数据类型）中指定，程序可以检索到相应 AJAX 对象（AjPFloat）的指针。

### 6.17.2 AJAX 库文件

下表列出了用于处理数组的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查看：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajarr | 通用数组处理 |
| ajsort | 数组排序 |





ajarr.h/c. 定义了用于处理动态数组的各种数组对象和函数。它还包含用于在低级别处理它们的静态函数。除非您计划扩展库的核心功能，否则不太可能需要这些。

ajsort.h/c. 用于对数组进行排序的函数（第 6.17.10 节，“对数组进行排序”）。

## 6.17.3 AJAX 数据类型

用于处理在 ACD 文件中定义的输入数组，请使用：

AjPFloat 浮点数数组（用于数组 ACD 数据类型）

AJAX 为基本 C 数据类型（第 5.1 节，“基本数据类型”）提供了以下动态数组对象。

## 6.17.3.1 char 数组

- AjPChar 一维字符数组

## 6.17.3.2 short 数组

- AjPShort 一维 short 数组
- AjPShort2d 二维 short 数组
- AjPShort3d 三维 short 数组

## 6.17.3.3 unsigned int 数组

- AjPUint 一维无符号整数数组
- AjPUint2d 二维无符号整数数组
- AjPUint3d 三维无符号整数数组

## 6.17.3.4 int 数组

- AjPInt 一维整数数组
- AjPInt2d 二维整数数组
- AjPInt3d 三维整数数组

## 6.17.3.5 float 数组

- AjPFloat 一维 float 数组
- AjPFloat2d 二维 float 数组
- AjPFloat3d 三维 float 数组

## 6.17.3.6 long 数组

- AjPLong 一维 long 数组
- AjPLong2d 二维 long 数组
- AjPLong3d 三维 long 数组

## 6.17.3.7 double 数组

- AjPDouble 一维 double 数组
- AjPDouble2d 二维 double 数组
- AjPDouble3d 三维 double 数组

## 6.17.4 ACD 数据类型

用于处理数组输入的 ACD 数据类型是：

- array 整数或浮点数列表

## 6.17.5 ACD 数据定义

数组输入的典型 ACD 定义：

```
array: thresholds
[
  information: "Values to represent 'identical', 'similar' and 'related'"
  default: "-1.5,0.0,1.5"
  minimum: "0.0"
  size: "3"
  sum: "0"
  sumtest: "Y"
]
```

## 6.17.5.1 参数名称

所有数组输入的数据定义都应具有直观的名称（附录 A.1.3，“参数命名约定”），尽管不强制执行标准命名方案。

## 6.17.5.2 常用属性

通常指定的属性摘要如下。除非它们被指示为全局属性（附录 A.4，“全局属性”），否则它们都是特定于数据类型的（附录 A.5，“特定于数据类型的属性”）。

- default：一个全局属性，用于指定默认值。

- minimum：指定允许的最小值。

size: 指定数组数据定义中允许的元素数量。

sum: 指定数组数据定义中所有值的总和，除非 sumtest 属性为 false，否则会对其进行测试。

sumtest: 一个布尔属性，如果关闭，则会关闭对数组数据定义的 sum: 属性的测试。

## 6.17.6 ACD 文件处理

通过 ACD 文件处理数组的数据类型和函数如下所示。

| 标题 | 读取数组 |
| :--- | :--- |
| ACD 数据类型 | array |
| AJAX 数据类型 | AjPFloat |
| 从 ACD 检索 | ajAcdGetArray |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并在必要时打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，该系列函数返回指向相应对象的指针。

## 6.17.6.1 输入数组检索

要检索输入数组，需声明一个对象指针，然后使用 ajAcdGetArray 进行初始化：

```
AjPFloat thresholds=NULL;
thresholds = ajAcdGetArray("thresholds");
```

## 6.17.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

## 6.17.6.3 内存管理

在程序结束时释放内存是您的责任。您必须对 ajAcdGetArray 调用返回的任何数组对象调用默认析构函数（见下文）。

## 6.17.7 函数名称

处理数组的函数名称具有一致的前缀，其一般形式如下：

```
ajTypeDim
```

Type 是数组的类型，为以下之一：

- Chararr（字符数组）
- Short（ajshort 数组）
- Uint（ajuint 整数数组）
- Int（ajint 数组）
- Float（float 数组）
- Long（ajlong 数组）
- Double（double 数组）

Dim 是数组的维度。对于一维数组，*不*给出：

- 2d（二维数组）
- 3d（三维数组）。

例如，所有处理无符号整数二维数组的函数都具有前缀 ajUint2d，而所有处理 float 一维数组的函数都具有前缀 ajFloat。提供了用于处理一维、二维和三维数组的函数；但是，仅支持一维字符数组。

## 6.17.8 数组对象内存管理

### 6.17.8.1 默认对象构造

要使用未在 ACD 文件中定义的数组对象，必须首先实例化相应的对象指针。默认构造函数的后缀为 New：

```
AjPChar		 ajCharrNew (void);
AjPShort		 ajShortNew (void);
AjPShort2d	 ajShort2dNew (void);
AjPShort3d	 ajShort3dNew (void);
AjPUint		 ajUintNew (void);
AjPUint2d	 ajUint2dNew (void);
AjPUint3d	 ajUint3dNew (void);
AjPInt		 ajIntNew (void);
AjPInt2d	 ajInt2dNew (void);
AjPInt3d	 ajInt3dNew (void);
AjPFloat		 ajFloatNew (void);
AjPFloat2d	 ajFloat2dNew (void);
AjPFloat3d	 ajFloat3dNew (void);
AjPLong		 ajLongNew (void);
AjPLong2d	 ajLong2dNew (void);
AjPLong3d	 ajLong3dNew (void);
AjPDouble		 ajDoubleNew (void);
AjPDouble2d	 ajDouble2dNew (void);
AjPDouble3d	 ajDouble3dNew (void);
```

所有构造函数都返回新对象的地址。指针不需要事先初始化为 NULL，但这样做是良好的实践。上述所有函数的使用方式相同：

```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The objects are instantiated and ready for use */
```

### 6.17.8.2 默认对象销毁

在使用完对象后，必须释放其内存。默认析构函数的后缀为 Del，并以相应对象的地址作为参数：

```
void ajCharrDel (AjPChar* Parr);
void ajShortDel (AjPShort* Parr);
void ajShort2dDel (AjPShort2d* Parr);
void ajShort3dDel (AjPShort3d* Parr);
void ajUintDel (AjPUint* Parr);
void ajUint2dDel (AjPUint2d* Parr);
void ajUint3dDel (AjPUint3d* Parr);
void ajIntDel (AjPInt* Parr);
void ajInt2dDel (AjPInt2d* Parr);
void ajInt3dDel (AjPInt3d* Parr);
void ajFloatDel (AjPFloat* Parr);
void ajFloat2dDel (AjPFloat2d* Parr);
void ajFloat3dDel (AjPFloat3d* Parr);
void ajLongDel (AjPLong* Parr);
void ajLong2dDel (AjPLong2d* Parr);
void ajLong3dDel (AjPLong3d* Parr);
void ajDoubleDel (AjPDouble* Parr);
void ajDouble2dDel (AjPDouble2d* Parr);
void ajDouble3dDel (AjPDouble3d* Parr);
```

例如，要释放由 ACD 文件中的数组输入分配的内存，请使用：

```
void ajFloatDel (AjPFloat* Parr);
```

其用法如下：

```
AjPFloat thresholds=NULL;
thresholds = ajAcdGetArray("thresholds");
/* Do something with the array */
ajFloatDel(&thresholds);
```

调用函数有责任在使用完对象后将其销毁：

```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The object is instantiated and ready for use */
/* Do something with the instantiated objects */
ajShort2dDel(&shorts);
/* The memory is freed and the pointers reset to NULL, ready for re-use. */
shorts = ajShort2dNew();
/* Do something else with the new objects. The pointer variable is reallocated. */
```

```
ajShort2dDel(&shorts);
/* The objects are done with so the memory is freed. */
```

### 6.17.8.3 替代对象构造和加载

可以使用后缀为 NewRes 的函数构造具有固定预留大小的数组。此类函数接受一个整数参数（size）作为预留大小，但其余部分与默认构造函数相同。以下仅显示部分可用函数：

```
AjPChar ajCharrNewRes (ajint size);
AjPShort ajShortNewRes (ajint size);
AjPShort2d ajShort2dNewRes (ajint size);
AjPShort3d ajShort3dNewRes (ajint size);
AjPUint ajUintNewRes (ajint size);
AjPUint2d ajUint2dNewRes (ajint size);
...
```

## 6.17.9 获取和设置数组元素

如果您将值分配给超出当前数组大小的数组元素，则数组将动态重新分配到足够大的大小以容纳新元素。如果您尝试检索超出当前数组大小的数组元素，将生成错误。

因此，预先知道数组的大小很有用。用于检索数组大小的函数具有后缀 Len，对于一维数组，它们返回数组长度；对于二维和三维数组，它们通过参数写入长度。同样，此处仅显示部分函数：

```
ajint ajCharrLen (const AjPChar arr);
ajint ajShortLen (const AjPShort arr);
void ajShort2dLen (const AjPShort2d arr, ajint* Pn1, ajint* Pn2);
void ajShort3dLen (const AjPShort3d arr,ajint* Pn1, ajint* Pn2, ajint* Pn3);
ajint ajUintLen (const AjPUint arr);
void ajUint2dLen (const AjPUint2d arr, ajint* Pn1, ajint* Pn2);
...
```

例如，要获取三维 double 数组的大小：

```
AjPDouble3d arr = NULL;
ajint dim1;
ajint dim2;
ajint dim3;
/* Allocate array */
ajDouble3dLen(arr, &dim1, &dim2, &dim3);
```

用于检索数组元素的函数具有后缀 Get。它们接受要检索的元素的索引并返回相应的数据类型：



char		 ajChararrGet (const AjPChar arr, ajint n);
short		 ajShortGet (const AjPShort arr, ajint n);
short		 ajShort2dGet (const AjPShort2d arr, ajint n1, ajint n2);
short		 ajShort3dGet (const AjPShort3d arr, ajint n1, ajint n2, ajint n3);
ajuint		 ajUintGet (const AjPUint arr, ajint n);
ajuint		 ajUint2dGet (const AjPUint2d arr, ajint n1, ajint n2);
...

For example, to retrieve the very first element of a 3D float array:

```c
AjPFloat3d arr = NULL;
float val;
...
/* Allocate array */
val = ajFloat3dGet(arr, 0, 0, 0);
```

Functions to set an element of an array have the suffix Put. They take the address of an array, the index of the element to set and of course the value to set. They return ajTrue if the element was set successfully:

```c
AjBool	 ajCharrarrPut (const AjPChar* Parr, ajint n, char chr);
AjBool	 ajShortPut (const AjPShort* Parr, ajint n, short i);
AjBool	 ajShort2dPut (const AjPShort2d* Parr, ajint n1, ajint n2, short i);
AjBool	 ajShort3dPut (const AjPShort3d* Parr, ajint n1, ajint n2, ajint n3, short i);
AjBool	 ajUintPut (const AjPUint* Parr, ajint n, ajuint i);
AjBool	 ajUint2dPut (const AjPUint2d* Parr, ajint n1, ajint n2, ajuint i);
...
```

For example, to set the very first element of a 3D float array:

```c
AjPFloat3d arr = NULL;
float	 val = 1.0;
arr = ajFloat3dNew();
ajFloat3dPut(&arr, 0, 0, 0, val);
```

## 6.17.10 对数组进行排序

Functions are provided in ajsort.h/c to sort C-type arrays of integers, unsigned integers and floating point numbers. Arrays may be sorted in the following ways:

- 对单个数组进行基本排序
- 按另一个数组中元素的顺序对单个数组进行排序
- 同时对两个数组进行排序
- 按升序或降序排序。

Functions for array sorting have the prefix ajSortInc (for sorting in incremental ascending order) or prefix ajSortDec (for sorting in descending order), followed by the datatype (Int, Uint or Float) of the array(s) that is sorted. The array size must be provided. The basic sort functions include:

```c
extern void ajSortIntDec (ajint *a, ajuint n);
extern void ajSortUintDec (ajuint *a, ajuint n);
extern void ajSortFloatDec (float *a, ajuint n);
extern void ajSortIntInc (ajint *a, ajuint n);
extern void ajSortUintInc (ajuint *a, ajuint n);
extern void ajSortFloatInc (float *a, ajuint n);
```

There are functions for sorting a single array (p) by the order of elements in another array (a):

```c
void ajSortFloatDecI (const float *a, ajuint *p, ajuint n);
void ajSortIntDecI (const ajint *a, ajuint *p, ajuint n);
void ajSortUintDecI (const ajuint *a, ajuint *p, ajuint n);
void ajSortFloatIncI (const float *a, ajuint *p, ajuint n);
void ajSortIntIncI (const ajint *a, ajuint *p, ajuint n);
void ajSortUintIncI (const ajuint *a, ajuint *p, ajuint n);
```

Functions for sorting two arrays simultaneously:

```c
void ajSortTwoIntIncI (ajint *a, ajuint n, ajuint *p);
void ajSortTwoUintIncI (ajuint *a, ajuint n, ajuint *p);
```

## 6.17.11 检索 C 类型数组

The C-type array may be retrieved from any of the array objects using the following functions. The function naming scheme should be obvious. Again, not all variants are shown:

```c
char* ajChararrChararr (const AjPChar arr);
short* ajShortShort (const AjPShort arr);
short** ajShort2dShort (const AjPShort2d arr);
short*** ajShort3dShort (const AjPShort3d arr);
ajuint* ajUintUint (const AjPUint arr);
ajuint** ajUint2dUint (const AjPUint2d arr);
...
```

Once the C-type array is retrieved then standard array notation can be used to access array elements. It is of course your responsibility to ensure you do not try to access an array element that is out of bounds. To help avoid doing so you can use the *Len functions (see above) to return the array size(s).

## 6.18 处理表

### 6.18.1 简介

A hash table is a data structure holding key:value pairs which allows for very efficient retrieval of a value given a key. For example, a key might be the accession number of a sequence and a value might be the sequence itself. Hash tables work by translating the key into a number called a ‘hash’ using a hashing function. The hash then provides the index of an array element or ‘bucket’ in the data structure holding the value. Hash tables have the great advantage that the search time is independent of the number of items stored, and that new key:value pairs can be added efficiently.

EMBOSS supports a standard hash table using strings for keys and generic hash tables with keys of arbitrary datatype. All the basic functionality you would expect for creating, manipulating and using hash tables is provided. This includes:

- 用于构建字符串哈希函数的哈希函数
- 用于添加和删除键值对或更改与键关联的值的函数
- 用于返回给定键关联的真实键或值的函数
- 能够对每个键值对应用函数
- 打印字符串哈希表。

There is no ACD datatype for hash tables, they are always created directly from within the C source code.

### 6.18.2 AJAX 库文件

AJAX library files for handling hash tables are listed in the table below. Library file documentation, including a complete description of datatypes and functions with usage notes is available at: http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajtable | 哈希表函数 |

ajtable.h/c. Defines the hash table object (AjPTable) and functions for handling hash tables. They also contains static functions for handling same at a low level. You are unlikely to need the static functions unless you plan to extend the hash table code.

### 6.18.3 ACD 数据类型

There are no ACD datatypes dedicated for tables.

### 6.18.4 AJAX 数据类型

For handling tables use:

AjPTable Hash table – a set of key:value pairs using a simple hash function to provide rapid searching for keys. Tables can hold any data type.

### 6.18.5 表对象内存管理

### 6.18.5.1 默认对象构造

To use a hash table object you must first instantiate the appropriate object pointer. Default constructor functions are provided for generic hash tables and EMBOSS string (AjPStr) hash tables:

```c
/* Generic hash table */
AjPTable ajTableNewLen(ajuint size)

/* Generic hash table with compare and hash functions */
AjPTable ajTableNewFunctionLen (ajuint n,
                 ajint cmp(const void* x, const void* y),
                 unsigned hash(const void* key, unsigned hashsize)) ;

/* String hash table */
AjPTable   ajTablestrNew (ajuint n);
AjPTable   ajTablestrNewLen (ajuint n);
AjPTable   ajTablestrNewCaseLen (ajuint n);
```

Both functions will create, initialise and return a new empty hash table that can hold an arbitrary number of key:value pairs. For a generic hash table, created with ajTableNewFunctionLen, an estimate of the number of unique keys (n) is passed, and functions for comparison (cmp) and for hashing the keys (hash) should be provided. If either of the cmp or hash arguments are NULL then it will use a default general-purpose hash function. The ajTableNewLen uses the general-purpose functions. Note that these cannot inspect the data, and can only use the addresses or values provided.

All constructors return the address of a new object. In the following code comp is the comparison function and hash is the hash function. An initial size of 50 is used. The pointer does not need to be initialised to NULL but it is good practice to do so:

```c
AjPTable table = NULL;

table   = ajTableNewFunctionLen(50, comp, hash);

/* The table is instantiated and ready for use */
```

The comparison function must return the result of comparing two keys as an integer which is 0 if the comparison is equal, +1 if the x is higher than y or -1 otherwise. The hash function must return the hash value for a given key.

Assume that you want a hash table with a case-insensitive C-type character string (char *) key. The comparison function may then be defined as ajCharCmpCase (available from ajstr.h) which returns the sort order of two text strings:



```c
ajint comp(const void* x, const void* y)
{
    const char* sx;
    const char* sy;

    sx = (const char*) x;
    sy = (const char*) y;

    return (ajint) ajCharCmpCase(sx, sy);
}
```

可使用以下哈希函数：

```c
ajuint hash(const void* key, ajuint hashsize)
{
    ajuint hash;
    const char* s;

    s = (const char*) key;

    for(hash = 0; *s; s++)
        hash = (hash * 127 + toupper((ajint)*s)) % hashsize;

    return hash;
}
```

### 6.18.5.2 默认对象销毁

使用完对象后必须释放其内存。为通用哈希表和字符串哈希表提供了默认析构函数：

```c
void	 ajTableFree (AjPTable* Ptable);
void	 ajTablestrFree (AjPTable* Ptable);
```

调用函数有责任在使用完对象后将其销毁：

```c
AjPTable table = NULL;

table = ajTableNewFunctionLen(50, comp, hash);

/* Do something with the instantiated table */

ajTableFree(&table);

/* The memory is freed and the pointer reset to NULL, ready for re-use. */

table = ajTablestrNew(50);

/* The pointer variable is reallocated. Do something else with the new table. */

ajTableFree(&table);

/* Done with the object so the memory is freed. */
```

### 6.18.5.3 替代对象构建和加载

要创建具有显式（而非估计）数量的键值对的通用哈希表，请使用：

```c
AjPTable ajTableNewLen (ajint n,
    ajint cmp(const void* x, const void* y),
    unsigned hash(const void* key, unsigned hashsize));
```

### 6.18.6 表哈希函数

在哈希表构建期间（见上文）提供的少数表哈希函数仅为字符串表提供便利。这些函数为EMBOSS字符串（AjPStr）和C类型（char *）字符串的哈希表提供区分大小写和不区分大小写的哈希：

```c
/* Case-insensitive hashing of EMBOSS strings */
unsigned ajTableStrHash (const void* key, unsigned hashsize);
/* Case-sensitive hashing of EMBOSS strings */
unsigned ajTableStrHashCase (const void* key, unsigned hashsize);
```

### 6.18.7 表比较函数

在哈希表构建期间（见上文）提供的少数表比较函数仅为字符串表提供便利。这些函数为EMBOSS字符串（AjPStr）的哈希表提供区分大小写和不区分大小写的比较：

```c
/* Case-sensitive comparison of EMBOSS strings */
ajint ajTableStrCmp (const void* ptrx, const void* ptry);
/* Case-insensitive comparison of EMBOSS strings */
ajint ajTableStrCmpCase (const void* ptrx, const void* ptry);
```

### 6.18.8 表编辑函数

可以将键值对添加到表中，从表中删除，或更改与键关联的值。

ajTablePut用于设置哈希表中给定键关联的值。它将返回先前的值，或者，如果表中不包含指定的键，则它将添加键和值并返回NULL。

```c
void* ajTablePut (AjPTable table, const void* key, void* value);
```

ajTableRemove将从表中删除键值对并返回被删除的值。如果表中不包含指定的键，则该函数仅返回NULL：

```c
void* ajTableRemove (AjPTable table, const void* key);
```

### 6.18.9 表查询函数

可以使用以下函数返回给定键关联的真实键或值：

```c
/* Return the value */
void* ajTableFetch (const AjPTable table, const void* key);

/* Return the key */
void* ajTableFetchKey (const AjPTable table, const void* key);
```

ajTableFetch是给定查询键返回值的标准函数。ajTableFetchKey用于在使用不区分大小写的哈希表时返回真实键（带有任何大小写）。

要返回哈希表中键值对的数量，请使用：

```c
ajint ajTableGetLength (const AjPTable table);
```

### 6.18.10 表映射函数

可以使用以下函数将函数应用于哈希表中的每个键值对：

```c
void ajTableMap (AjPTable table, void apply(const void* key, void** Pvalue, void* ptr), void* ptr);
void ajTableMapDel (AjPTable table, void apply(const void** Pkey, void** Pvalue, void* ptr), void* ptr);
```

ajTableMap调用的函数不应删除任何键（尽管可以修改值），而ajTableMapDel调用的函数可以删除键。在两种情况下都必须提供一个函数。

假设你有一个具有EMBOSS字符串键和整数值的哈希表，并且想要应用一个函数来打印键值对，另一个函数来释放键值对。

打印函数将类似于：

```c
static void print(const void* key, void** value, void* cl)
{
    AjPStr keystr;
    ajint *valptr;

    keystr = (AjPStr) key;
    valptr = (ajint *) *value;

    ajUser("type '%S' found %d times", keystr, *valptr);

    return;
}
```

而删除函数将是：

```c
static void delete(const void** key, void** value, void* cl)
{
    AjPStr keystr;
    ajint *valptr;

    keystr = (AjPStr) *key;
    valptr = (ajint *) *value;

    ajStrDel(&keystr);
    AJFREE(valptr);

    *key = NULL;
    *value = NULL;

    return;
}
```

要调用这些函数，可以使用类似：

```c
AjPTable table = NULL;

/* Allocate table */
ajTableMap(table, print, NULL);
ajTableMapDel(table, delete, NULL);
```

### 6.18.11 打印函数

提供了用于打印EMBOSS字符串（AjPStr）字符串哈希表的函数：

```c
void ajTablestrPrint (const AjPTable table);
```

## 6.19 处理菜单

### 6.19.1 简介

在分子生物学程序中，从选项列表中选择通常是必要的。两种ACD数据类型（list和selection）提供略有不同的列表样式，但都向用户展示一个可供选择的选项列表。对于用户，list和selection数据类型之间的区别很小，仅在于选择项的标记方式。在selection数据类型中，选择项会自动从1开始编号。在list数据类型中，选择项可以用任何任意文本标记。用户可以通过输入数字（对于selection类型）或标签文本（对于list类型），或者（两种list类型）输入数字或标签后给出的描述性文本本身的非歧义部分来选择其中一个选项。在实践中，更倾向于使用list数据类型。

### 6.19.2 AJAX库文件

没有专门用于处理菜单的AJAX库文件。菜单中的选择作为字符串或字符串数组处理。有关字符串处理的更多信息，请查阅文档。库文件文档可在线查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajstr | 字符串处理 |

ajstr.h/c. 定义了用于处理ACD文件中字符串的字符串对象（AjPStr）（参见第6.4节“处理简单ACD数据类型”）。它们包含你进行一般字符串处理所需的大部分函数（第6.5节“处理字符串”）。

### 6.19.3 ACD数据类型

有两种用于处理菜单的ACD数据类型：

- **list**：带有文本标签的选项列表（文本描述）。用户会看到一个可供选择的有限选项列表。选择项可以用任何任意文本标签标记。选项描述通常比selection数据类型更详细。
- **selection**：带有自动生成数字标签的选项列表（文本描述）。用户会看到一个可供选择的有限选项列表。选择项会自动从1开始编号。

### 6.19.4 ACD数据定义

### 6.19.4.1 list菜单

list菜单的典型ACD定义：

```
list: frame [
  standard: "Y"
  help: "Allows selection from a set of reading frames"
  default: "1"
  minimum: "1"
  maximum: "1"
  header: "Translation frames"
  values: "1:1, 2:2, 3:3, F:Forward three frames, -1:-1, -2:-2, -3:-3, R:
Reverse three
frames, 6:All six frames"
  delimiter: ","
  codedelimiter: "::"
  information: "Frame(s) to translate"
}
```

用户将看到来自header:属性的菜单标题。之后将出现来自values:属性的标签/文本信息。随后将显示来自information:属性的提示。它将类似于：

```
Translation frames
1       1
2       2
3       3
F       Forward three frames
-1      -1
-2      -2
-3      -3
R       Reverse three frames
6       All three frames
Frame(s) to translate[1] :
```

用户通常可以从上述选项中提供一个逗号分隔的列表；这取决于最小值和最大值。在上述示例中，最小选择数和最大选择数均设置为1，因此只允许一个选择值。选择是通过输入标签值来完成，因此如果最大计数设置为3，则用户输入"-1,F,6"将是有效的输入。

codedelimiter属性允许你选择任何字符来分隔values属性中的标签和文本。delimiter属性允许你选择一个字符来分隔values属性中的标签/文本对。

### 6.19.4.2 selection菜单

selection菜单的典型ACD定义：

```
select: order
[
    casesensitive: "N"
    default: "score"
    delimiter: ","
    header: "Sort order of results"
    help: "Name of the output file which holds the results of the analysis."
    information: "Sort order of results"
    maximum: "1"
    minimum: "1"
    information: "Select sort order of results"
    standard: "Y"
]
```



```
values: "length, position, score"
]
```

**注意**

`selection` 数据类型与 `list` 数据类型非常相似。`values:` 属性仅包含由分隔符分隔的文本条目列表（忽略前导空格）。选择基于文本值进行，没有标签。另外，请注意有一个 `casesensitive:` 属性，通常设置为 `"N"`，以便带 Shift 和不带 Shift 的字符都同样可接受。用户可以选择文本，直到文本长度与其他值没有歧义为止。

## 6.19.4.3 参数名

菜单的参数名称应直观，但不强制执行任何标准。

## 6.19.4.4 常用属性

下表汇总了通常指定的属性。除非它们被指示为全局属性（第 A.4 节，“全局属性”），否则它们均为数据类型特定属性（第 A.5 节，“数据类型特定属性”）。

- **值：** 对于 `list` 和 `selection` 数据类型菜单，用户可选择的值在 `values:` 属性中定义为字符串。
- **分隔符：** 对于 `list` 和 `selection` 数据类型菜单，`values:` 字符串中的值由 `delimiter:` 属性给定的字符分隔，默认值为 `';'`（分号）。
- **代码分隔符：** 对于 `list` 数据类型，`codedelimiter:` 属性定义的字符是分隔标签和值的分隔符，默认值为 `':'`（冒号）。
- **最小值：** 定义用户可做选择的最小数量。
- **最大值：** 定义用户可做选择的最大数量。
- **标题：** 存储显示在选项列表上方的文本。
- **信息：** 此全局属性（针对所有数据类型定义）定义列表后用作提示的文本。
- **区分大小写：** 控制选项是否区分大小写。无论用户使用何种大小写，参数的值将完全是相应列表值的内容。
- **按钮：** 此属性提供给界面开发人员使用。它是一个布尔值，可以是 "Y"（是）或 "N"（否），指示是否应使用图形按钮（如单选按钮、复选框或选择列表）来选择值，或者是否应使用文本输入框显示列表以输入选项。

## 6.19.5 AJAX 数据类型

AJAX 字符串数据类型用于处理在 ACD 文件中定义的菜单：
`AjPStr * Array of strings (for list and selection ACD datatypes)`

## 6.19.6 ACD 文件处理

通过 ACD 文件处理菜单的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
|---|---|---|
| list 菜单 | | |
| list | AjPStr * | ajAcdGetList |
| selection 菜单 | | |
| selection | AjPStr * | ajAcdGetSelect |

您的应用程序代码将调用 `embInit` 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存。您可以通过 `ajAcdGet*` 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.19.6.1 菜单检索

要检索菜单，需声明一个对象指针，然后使用相应的 `ajAcdGet*` 函数对其进行初始化。

### 6.19.6.1.1 list 菜单

```
...
AjPStr *flist=NULL;
...
flist = ajAcdGetList("frame");
...
```

该声明表明 `flist` 将是一个字符串对象数组。字符串中保存的值是值列表中的标签，列表由 `NULL` 指针终止。因此，根据我们的示例，由于只允许一个值，并假设用户对提示回答了 '6'，则生成的数组将是：

| flist[0] | 包含 "6" 的字符串对象 |
| flist[1] | NULL 指针 |

如果 maximum 大于 1，您的代码可能会使用类似以下的内容遍历列表：

```
n = 0;
while(flist[n])
{
    if (ajStrMatchC(flist[n],"6"))
    {
        /* Do something */
    }
    ...
    ++n;
}
```

### 6.19.6.1.2 selection 菜单

```
...
AjPStr *oselect=NULL;
...
    oselect = ajAcdGetSelect("order");
...
```

否则，代码与 list 数据类型相同，只是它会测试字符串 'length'、'position' 和 'score'。

### 6.19.6.2 替代 ACD 检索函数

```
AjPStr ajAcdGetListSingle (const char *token);
AjPStr ajAcdGetSelectSingle (const char *token);
```

在程序结束时释放内存是您的责任。您只检索了一个字符串；其余内部数据将由 ACD 处理自动清理。您应该调用 ajStrDel 来释放这些函数返回的字符串。

### 6.19.6.3 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.19.6.4 内存管理

在程序结束时释放内存是您的责任。您必须对 ajAcdGetList 或 ajAcdGetSelect 调用返回的字符串数组调用析构函数。

字符串数组的析构函数如下：

```
void ajStrDelarray (AjPStr** PStr);
```

用法如下：

```
AjPStr *flist=NULL;
flist = ajAcdGetList("frame");
...
ajStrDelarray(&flist);
```

## 6.20 处理图形输出

### 6.20.1 简介

EMBOSS 可以生成两种类型的图形输出。第一种是“绘制”图形。它们允许用户在图形窗口中使用（例如）线条和点绘图原语进行绘制。另一种更常用的图形是“图表”绘图。提供了多种函数来简化图表的显示，例如自动绘制坐标轴以及为其设置标题的功能。图形目前通过 PLplot 的包装函数生成。在 EMBOSS 开发初期，PLplot 是唯一可用的带有 LGPL 许可证的多平台 C 图形库。

图形对象通过 ACD 数据类型创建。库调用提供对 PLplot 库的接口，该库管理输出到屏幕或文件。PLplot 定义了一个图形视口用于工作。视口尺寸取决于每个设备的 PLplot 驱动程序中的定义，大小或比例不尽相同。当应用程序需要操作对象的缩放（例如 EMBOSS 应用程序 cirdna）时，建议使用毫米（或 4 像素）单位工作，而不是在不同设备上使用时无法缩放的任意单位。

图形输出的一般特性包括：

- 图形函数可以定义颜色、线条样式、标题、坐标轴标签和绘图缩放因子。
- 绘制的对象可以是线条、形状或文本。
- 提供了用于计算缩放字符大小、极坐标和绘图坐标之间距离的函数。
- 最有用的内部数据是 PLplot 缩放信息，包括当前缩放因子和以毫米为单位的绘图尺寸。
- 当绘图输出到文件时，有函数可用于控制目录和输出文件名。
- PLplot 库具有与任何单个绘图无关的通用设置。因此，您应避免在任何 EMBOSS 应用程序中使用多个活动图形对象。

### 6.20.2 AJAX 库文件

用于处理图形的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajgraph | 通用图表处理函数 |
| ajgraphstruct | 用于图表的数据结构 |
| ajgraphxml | 图表 XML 文件对象及用于操作它的函数 |
| ajhist | 直方图。 |
| ajcall | 图形包访问 |
| ajdom | 文档对象模型库调用 |

- ajgraph.h/c. 用于绘制和打印图表的基本函数。它还包含用于低级处理图表的静态数据结构和函数。
- ajgraphstruct.h. 用于处理图表的对象，包括基本图表对象 (AjPGraph) 和 **PLplot** 图表数据对象 (AjPGraphdata)。
- ajhist.h. 定义用于处理直方图的直方图对象 `AjPHist`，其中包含直方图数据对象 (AjPHistdata) 作为子结构。它包含用于处理直方图的基本函数（第 6.20.17 节，“直方图”）。
- ajcall.h/c. 用于允许访问不同图形包的函数，以防将来实现 **PLplot** 的替代方案。它们目前未在此处使用或记录，有关更多信息，请参阅在线库文档。
- ajdom.h/c. 用于处理文档对象模型的数据结构和函数，以及静态函数。它正在开发中，未在此处记录。有关更多信息，请参阅在线库文档。

除非您计划实现代码以扩展库的核心功能，否则不太可能需要上述文件中的静态数据结构和函数。

### 6.20.3 ACD 数据类型

用于处理图形输出有两种数据类型：

- graph: 任何一般类型的图形输出。
- graphxy: 作为简单二维 (2D) XY 图的图形输出，序列沿 x 轴排列。

### 6.20.4 ACD 数据定义

图形输出（graph 数据类型）的典型 ACD 定义：

```
graph: graph
[
  gxtitle: "Residue Position"
]
```

图形输出（xygraph 数据类型）的典型 ACD 定义：

```
xygraph: graph
[
  gxtitle: "Residue Position"
]
```



### 6.20.4.1 参数名

所有图形输出的数据定义都应具有标准参数名 `graph`。参见附录 A，_ACD 语法参考_。

### 6.20.4.2 常用属性

通常指定的属性摘要如下。这些包括两个特定于数据类型的属性（第 A.5 节，“特定于数据类型的属性”）。

- `gtitle`: 指定任一类型图形的图形标题。可以使用属性设置许多其他图形元素。

- `multiple`: 指定 `graph` ACD 数据类型单个输出中多个 XY 图形的数量。

## 6.20.5 程序初始化

在 EMBOSS 的早期版本中，任何进行图形调用的应用程序都需要先初始化图形库函数。EMBOSS 6.2.0 中库的重构使开发变得容易得多。现在所有应用程序只需调用 `embInit` 或 `embInitPV`。

## 6.20.6 AJAX 数据类型

用于处理 ACD 文件中定义的图形输出，请使用：

- `AjPGraph` 基本图形对象（用于 `graph` 和 `graphxy` ACD 数据类型）

还有一种数据类型用于处理直方图图形：

- `AjPHist` 直方图对象

上述基本数据类型作为嵌套子结构包含以下 AJAX 数据类型：

- `AjPGraphobj` PLplot 图形对象（`AjPGraph` 的子结构）

- `AjPGraphdata` PLplot 图形数据对象（`AjPGraph` 的子结构）

- `AjPHistdata` 直方图数据对象（`AjPHist` 的子结构）。

除非您计划扩展图形库代码，否则不太可能需要静态函数。

## 6.20.7 ACD 文件处理

通过 ACD 文件处理图形输出的数据类型和函数如下所示。

| | 编写 graph 图形 | 编写 graphxy 图形 |
|---|---|---|
| ACD 数据类型 | graph | graphxy |
| AJAX 数据类型 | AjPGraph | AjPGraph |
| 从 ACD 检索 | ajAcdGetGraph | ajAcdGetGraphxy |

### 6.20.7.1 输出图形检索

要检索输出图形对象，需声明一个对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

### 6.20.7.1.1 graph

```
AjPGraph graph=NULL;
graph = ajAcdGetGraph("graph");
```

### 6.20.7.1.2 graphxy

```
AjPGraph graph=NULL;
graph = ajAcdGetGraphxy("graph");
```

### 6.20.7.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.20.7.3 内存和文件管理

您的应用程序代码将调用 embInit 或 embInitPV 来处理 ACD 文件和命令行。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。在程序结束时，调用图形库关闭任何文件并释放内存是您的责任。

### 6.20.7.3.1 关闭图形文件

要关闭输出图形文件，请调用 ajGraphicsClose。它通过 PLplot 库关闭图形输出，关闭任何输出文件和屏幕显示：

```
AjPGraph graph=NULL;
graph = ajAcdGetGraphxy("graph");
/* Do something with graph */
ajGraphicsClose();
```

### 6.20.7.3.2 释放内存

您必须对 ajAcdGetGraph 或 ajAcdGetGraphxy 调用返回的任何图形对象调用默认析构函数（见下文）。

## 6.20.8 图形对象内存管理

### 6.20.8.1 默认对象构造

图形对象通常通过调用 ajAcdGetGraph 或 ajAcdGetGraphxy 从 ACD 文件处理中加载（见上文）。因此，您永远不需要手动实例化图形对象 (AjPGraph)。在极不可能的情况下需要这样做，提供了两个构造函数，即默认构造函数和 ajGraphxyNewI（用于指定图形数量）：

```
AjPGraph ajGraphNew (void);
AjPGraph ajGraphxyNewI (ajint numsets);
```

您还可能需要创建图形数据对象。提供了两个构造函数，即默认构造函数和 ajGraphdataNewI（用于指定数据点数量）：

```
AjPGraphdata ajGraphdataNew (void);
AjPGraphdata ajGraphdataNewI (ajint numsets);
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的做法：

```
AjPGraph             graph        = NULL;
AjPGraph             graphxy      = NULL;
AjPGraphdata         gdata1       = NULL;
AjPGraphdata         gdata2       = NULL;

graph        = ajGraphNew ();
graphxy      = ajGraphxyNewI (2);
gdata1       = ajGraphdataNew ();
gdata2       = ajGraphdataNew ();

/* The objects are instantiated and ready for use */
```

### 6.20.8.2 默认对象销毁

在指针重复使用之前以及使用完对象后，必须释放对象的内存。默认析构函数如下：

```
void   ajGraphxyDel   (AjPGraph* pmult);
void   ajGraphdataDel(AjPGraphdata *thys);
```

使用方法如下：

```
AjPGraph graph=NULL;

graph = ajAcdGetGraphxy("graph");

/* Do something with graph */

ajGraphicsClose();
ajGraphxyDel(&graph);
```

另一个示例：

```
AjPGraph graph = NULL;
AjPGraph graphxy = NULL;
AjPGraphdata gdata1 = NULL;
AjPGraphdata gdata2 = NULL;

graph = ajGraphNew();
graphxy = ajGraphxyNewI(2);
gdata1 = ajGraphdataNew();
gdata2 = ajGraphdataNew();

/* Do something with the objects */
ajGraphxyDel(&graph);
ajGraphxyDel(&graphxy);
ajGraphdataDel(&gdata1);
ajGraphdataDel(&gdata2);
```

## 6.20.9 图形文件管理

处理图形输出文件的函数具有前缀 ajGraph。文件名和目录可以指定（通常通过调用这些函数的 ACD 属性和命令行限定符）。为不直接写入屏幕的 PLplot 输出设备创建文件。该库还提供数据文件输出，用于绕过 PLplot 并直接将图形结果传递给 Staden 包：

- `ajGraphicsSetFilename` /* 设置输出文件的名称和扩展名。 */
- `ajGraphSetOutfileS` /* 设置输出文件的名称。 */
- `ajGraphSetOutdirS` /* 设置输出文件的目录。 */
- `ajGraphIsData` /* 检查图形是否正在创建 Staden 数据文件。 */
- `ajGraphxyDisplay` /* 显示 xy 图形 */

以下函数设置输出文件名。通常不需要调用这些函数，因为文件在 ACD 文件处理期间已接收到名称。

```
/* Set name and extension of output file. */
void ajGraphicsSetFilename (const AjPGraph thys);

/* Set name of output file. */
void ajGraphSetOutfileS (AjPGraph thys, const AjPStr txt);
```

/* Set directory of output file. */
void ajGraphSetOutdirS(AjPGraph thys, const AjPStr txt);

ajGraphxyDisplay 用于将图形对象中的图形显示到绘图设备。任何带有图形输出的程序都必须调用它一次。第二个参数 (closeit) 为 ajTrue，表示在显示后关闭图形输出文件：

```
void ajGraphxyDisplay (AjPGraph thys, AjBool closeit );
```

最后，如果图形正在创建数据文件，ajGraphIsData 将返回 ajTrue：

```
AjBool ajGraphIsData (const AjPGraph thys);
```

## 6.20.10 初始化函数

有多种用于初始化和更新图形对象的赋值函数：

| 函数 | 描述 |
| :--- | :--- |
| ajGraphDataAdd | /* 添加图形。 */ |
| ajGraphDataAdd | /* 向多图形添加另一个图形。 */ |
| ajGraphDataReplace | /* 替换图形。 */ |
| ajGraphDataReplaceI | /* 替换指定编号的图形。 */ |
| ajGraphInitSeq | /* 根据序列设置图形的默认值。 */ |
| ajGraphxyNewI | /* 创建用于容纳多个图形的图形对象。 */ |
| ajGraphxySetRanges | /* 设置数据点的最小值和最大值。 */ |
| ajGraphClear | /* 删除与图形关联的可绘制对象 */ |

ajGraphSetMulti 用于向图形对象添加多个图形。指定图形数量 (numsets)：

```
void ajGraphSetMulti (AjPGraph thys, ajint numsets);
```

ajGraphDataAdd 用于向图形对象添加图形。传递图形数据（存储在 AjPGraphdata 对象中），函数在成功时返回 1（否则返回 0）：

```
ajint ajGraphDataAdd (AjPGraph thys, AjPGraphdata graphdata);
```

该函数可以多次调用以添加任意数量的图形。图形数据对象由图形使用，在完成对图形本身的使用之前不应将其删除：

```
AjPGraph graphs = NULL;
AjPGraphdata gdata = NULL;

graphs = ajAcdGetGraphxy("graphs");





## 6.20 处理图形输出

```
gdata = ajGraphdataNew();

/* Set up graph data */

ajGraphDataAdd(graphs,gdata);

/* Do something with the graph */

ajGraphdataDel(&gdata);
ajGraphxyDel(&graphs);
```

ajGraphDataReplace 和 ajGraphDataReplaceI 用于用另一个图替换图对象中的一个图。新图数据（存储在 AJPGraphdata 对象中）被传递，被替换的图数据对象被删除。函数在成功时返回 1（否则返回 0）：

```
ajint ajGraphDataReplace (AJPGraph thys, AJPGraphdata graphdata);
ajint ajGraphDataReplaceI (AJPGraph thys, AJPGraphdata graphdata, ajint num);
```

ajGraphDataReplace 替换第一个图，而 ajGraphDataReplaceI 替换编号的图。
ajGraphInitSeq 用于根据传递的序列为图对象定义默认值：

```
void ajGraphInitSeq (AJPGraph thys, const AJPSeq seq);
```

图表标题设置为序列名称，x 轴设置为序列大小。用法如下：

```
int main(int argc, char **argv)
{
    AJPSeq seq      = NULL;
    AJPGraph graph  = NULL;

    embInit("isochore", argc, argv);

    seq   = ajAcdGetSeq("sequence");
    graph = ajAcdGetGraphxy("graph");

    ajGraphInitSeq(graph, seq);
}
```

最后，ajGraphxySetRanges 将计算数据点的最小值和最大值，并将值存储在图对象中：

```
void ajGraphxySetRanges (AJPGraph thys);
```

要删除连接到图对象的所有可绘制对象（以便重用它来创建新图表页面）调用：

```
void ajGraphClear (AjPGraph thys);
```

### 6.20.11 创建窗口

以下函数用于管理绘图窗口：

| 函数 | 说明 |
|---|---|
| ajGraphOpenWin | /* 打开窗口。 */ |
| ajGraphOpenPlotset | /* 打开带有多个图表的窗口。 */ |
| ajGraphOpenMm | /* 打开窗口并以毫米返回尺寸 */ |
| ajGraphicsClose | /* 关闭窗口。 */ |
| ajGraphClear | /* 清除屏幕或新页面。 */ |

每个要绘制的图（屏幕或页面）都需要一个窗口。前缀为 ajGraphOpen 的函数将打开用于图形绘图的窗口：

```
void ajGraphOpenWin (AjPGraph thys, float xmin, float xmax, float ymin, float ymax);
void ajGraphOpenPlotset (AjPGraph thys, ajint numofsets);
void ajGraphOpenMm (AjPGraph thys, float * xmm, float * ymm);
```

ajGraphOpenWin 通常使用，每个图应调用一次，通常每个应用程序调用一次。窗口由提供的最小和最大 x 和 y 值定义。或者，ajGraphOpenPlotset 将为多个图表打开一个窗口。ajGraphOpenMm 打开一个窗口并以毫米返回物理尺寸，应用程序随后可以将其映射到自己的绘图单位。这是处理可缩放可绘制对象的安全方法，因为 PLplot 设备页面大小不一致。

ajGraphClear 用于清除屏幕（用于屏幕输出）或创建新页面（用于绘图仪/PostScript 输出）。它接收一个布尔参数，如果为 ajTrue，则会为下一页重置当前笔颜色、字符大小、图表标题和副标题等。

```
void ajGraphClear (AjPGraph thys, AjBool resetdefaults);
```

完成向窗口绘图后（见下文），必须使用 ajGraphicsClose 关闭它：

```
void ajGraphicsClose (void)
```

### 6.20.12 绘图函数

前缀为 ajGraphicsDraw 的函数用于向绘图设备绘制图形元素。函数如下：

| 函数 | 说明 |
|---|---|
| ajGraphicsDrawposBox | /* 绘制一个框。 */ |
| ajGraphicsDrawposBoxFill | /* 绘制一个框并填充。 */ |
| ajGraphicsDrawposDia | /* 绘制一个菱形。 */ |
| ajGraphicsDrawposDiaFill | /* 绘制一个菱形并填充。 */ |
| ajGraphicsDrawsetPoly | /* 绘制一个多边形。 */ |
| ajGraphicsDrawsetPolyFill | /* 绘制一个多边形并填充。 */ |
| ajGraphicsDrawposRect | /* 绘制一个矩形。 */ |
| ajGraphicsDrawposRectFill | /* 绘制一个矩形并填充。 */ |
| ajGraphicsDrawarcRect | /* 沿曲线绘制矩形。 */ |
| ajGraphicsDrawarcRectFill | /* 沿曲线绘制矩形并填充。 */ |
| ajGraphicsDrawposTri | /* 绘制一个三角形。 */ |
| ajGraphicsDrawposTriFill | /* 绘制一个三角形并填充。 */ |
| ajGraphicsDrawposCircle | /* 绘制一个圆。 */ |
| ajGraphicsDrawsetDots | /* 绘制一组点。 */ |
| ajGraphicsDrawbarsHoriz | /* 绘制水平误差条。 */ |
| ajGraphicsDrawbarsVert | /* 绘制垂直误差条。 */ |
| ajGraphicsDrawposLine | /* 在两点之间绘制一条线。 */ |
| ajGraphicsDrawsetLines | /* 绘制多条线。 */ |
| ajGraphicsDrawsetSymbols | /* 绘制一组点。 */ |
| ajGraphicsDrawposTextAtend | /* 在终点绘制文本。 */ |
| ajGraphicsDrawposTextAtmid | /* 在中点绘制文本。 */ |
| ajGraphicsDrawposTextAlineJustify | /* 沿线绘制文本。 */ |
| ajGraphicsDrawposTextAtstart | /* 在起点绘制文本。 */ |
| ajGraphicsDrawarcTextJustify | /* 沿曲线绘制文本。 */ |
| ajGraphicsDrawarcArc | /* 绘制圆的一部分（弧）。 */ |

应查阅在线文档以了解如何使用这些函数的说明。

### 6.20.13 设置要渲染的图形元素

前缀为 ajGraphicsSet 的函数用于设置在绘制图表时要渲染的图形元素。ajGraphSetFlag 函数在内部使用。开发者应优先为每个标志调用单独的 ajGraphxyShow 函数。函数如下：

| 函数 | 说明 |
|---|---|
| ajGraphicsSetBgcolourBlack | /* 背景颜色设为黑色。 */ |
| ajGraphicsSetBgcolourWhite | /* 背景颜色设为白色。 */ |
| ajGraphicsSetFgcolour | /* 前景颜色设为某种颜色。 */ |
| ajGraphicsSetLabelsC | /* 图表标签。 */ |
| ajGraphicsSetRlabelC | /* 右 Y 轴标签。 */ |
| ajGraphSetDescC | /* 图表描述。 */ |
| ajGraphicsSetLinestyle | /* 线条样式。 */ |
| ajGraphicsSetPortrait | /* 页面方向。 */ |
| ajGraphicsSetPenwidth | /* 笔宽。 */ |
| ajGraphxyShowPointsCircle | /* 将点绘制为圆形。 */ |
| ajGraphxyShowPointsJoin | /* 在点之间绘制线条。 */ |
| ajGraphSetFlag | /* 设置 PLplot 标志以添加或减去。 */ |
| ajGraphxySetRanges | /* 所有图表的数据点最大值和最小值。 */ |
| ajGraphxySetflagOverlay | /* 设置图表是否相互叠加。 */ |
| ajGraphSetSubtitleC | /* 副标题。 */ |
| ajGraphShowSubtitle | /* 设置是否显示副标题。 */ |
| ajGraphSetTitleC | /* 标题。 */ |
| ajGraphShowTitle | /* 设置是否显示标题。 */ |
| ajGraphxySetflagGaps | /* 设置图表是否启用间隙。 */ |
| ajGraphicsSetDefcharsize | /* 默认字符大小（毫米）。 */ |
| ajGraphicsSetCharscale | /* 字符缩放因子。 */ |
| ajGraphicsSetFillpat | /* 填充图案类型。 */ |

前缀为 ajGraphxySetX 和 ajGraphxySetY 的函数分别用于设置 x 轴或 y 轴的图形属性。函数如下：

| 函数 | 说明 |
|---|---|
| ajGraphxyShowXaxis | /* 底部 x 轴。 */ |
| ajGraphxyShowUnum | /* 顶部 x 轴上的标签。 */ |
| ajGraphxyShowXTick | /* x 轴上的刻度标记。 */ |
| ajGraphxyShowXAxis | /* 顶部的左侧 X 轴。 */ |
| ajGraphxySetXendF | /* 图中 x 的结束位置。 */ |
| ajGraphxyShowXgrid | /* 显示 x 轴刻度标记的网格。 */ |
| ajGraphxyShowXInvert | /* x 轴上图表内部的刻度标记。 */ |
| ajGraphxyShowXlabel | /* 标记 x 轴。 */ |
| ajGraphxySetXrangeII | /* 使用整数的 x 轴范围。 */ |
| ajGraphxySetXstartF | /* 图中 x 的起始位置。 */ |
| ajGraphxyShowYnum | /* 左侧轴上的标签。 */ |
| ajGraphSetXlabelC | /* 单个图上多个图表的 x 轴标题。 */ |
| ajGraphxyShowYaxis | /* 左侧 y 轴。 */ |
| ajGraphxyShowRaxis | /* 右侧 y 轴。 */ |
| ajGraphxyShowYtick | /* y 轴上的刻度标记。 */ |
| ajGraphxySetYendF | /* 图中 y 的结束位置。 */ |
| ajGraphxyShowYgrid | /* 显示 y 轴刻度标记的网格。 */ |
| ajGraphxyShowYInvert | /* y 轴上图表内部的刻度标记。 */ |
| ajGraphxyShowYlabel | /* 标记 y 轴。 */ |
| ajGraphxySetYrangeII | /* 使用整数的 y 轴范围。 */ |
| ajGraphxySetYstartF | /* 图中 y 的起始位置。 */ |
| ajGraphSetYlabelC | /* 单个图上多个图表的 y 轴标题。 */ |

上述函数与用于添加要渲染的图形元素的函数配合使用：

| 函数 | 说明 |
|---|---|
| ajGraphAddLine | /* 添加一条线。 */ |
| ajGraphAddRect | /* 添加一个矩形。 */ |
| ajGraphAddTextC | /* 添加文本。 */ |
| ajGraphAddTextScaleC | /* 添加带缩放因子的文本 */ |

可用于在图数据对象中设置要渲染元素的函数集更有限：

| 函数 | 说明 |
|---|---|
| ajGraphdataSetMinmax | /* 所有图表的数据点最小值和最大值。 */ |
| ajGraphdataSetTruescale | /* 数据点的最小值和最大值的缩放 */ |
| ajGraphdataSetTypeC | /* 用于数据输出的图表类型。 */ |
| ajGraphdataSetSubtitleC | /* 副标题 */ |
| ajGraphdataSetTitleC | /* 标题 */ |
| ajGraphAppendTitleC | /* 来自描述的标题。 */ |
| ajGraphdataSetXlabelC | /* x 轴标题。 */ |
| ajGraphdataSetYlabelC | /* y 轴标题。 */ |
| ajGraphdataSetColour | /* 单个图表的绘图颜色。 */ |
| ajGraphdataSetLinetype | /* 单个图表的绘图线条类型。 */ |

这些函数与用于添加要渲染的图形元素的函数配合使用：

| 函数 | 说明 |
|---|---|
| ajGraphdataAddposLine | /* 添加一条线。 */ |
| ajGraphdataAddposRect | /* 添加一个矩形。 */ |
| ajGraphdataAddposTextC | /* 添加文本。 */ |
| ajGraphdataAddXY | /* 添加 X,Y 数据点。 */ |
| ajGraphdataCalcXY | /* 从增量添加 X,Y 数据点。 */ |

应查阅在线文档以了解如何使用这些函数的说明。





### 6.20.14 获取图表属性

获取图表属性的函数具有前缀 ajGraphGet：

```
ajGraphGetSubtitleC		/* Graph subtitle. */
ajGraphGetTitleC		/* Graph title. */
ajGraphGetXlabelC		/* x-axis title */
ajGraphGetYlabelC		/* y-axis title */
ajGraphicsGetFgcolour		/* Current foreground colour. */
ajGraphicsBasecolourNewNuc	/* Base colours array for nucleotide sequence. */
ajGraphicsBasecolourNewProt	/* Base colours array for protein sequence. */
ajGraphicsGetCharsize		/* Character size. */
ajGraphGetParamsPage		/* Output device parameters. */
```

返回图表标题的函数返回字符串对象本身（而非副本），因此必须小心，不要无意中更改或删除它。

ajGraphicsGetFgcolour 将当前前景颜色作为整数返回：

```
ajint ajGraphicsGetFgcolour (void);
```

ajGraphicsCheckColourC 接受一个表示颜色的字符串参数，并返回与该颜色对应的整数，如果未找到该颜色，则返回 -1。

```
ajint ajGraphicsCheckColourS (const AjPStr colour);
ajint* ajGraphicsBasecolourNewNuc (const AjPStr codes);
ajint* ajGraphicsBasecolourNewProt (const AjPStr codes);
```

下面的代码从 ACD 文件处理中获取用户指定为字符串的颜色。会调用 ajGraphicsCheckColourC 来获取颜色的整数值，然后将其传递给 ajGraphicsSetFgcolour 以设置前景颜色：

```
AjPStr colour = NULL;
ajint colouri;
colour = ajAcdGetString("colour");
colouri = ajGraphicsCheckColourC(colour);
if(colouri == -1)
    colouri = GREY;
ajGraphicsSetFgcolour(colouri);
```

ajGraphicsGetCharsize 检索默认和当前字符大小。在设置其他图形元素的大小时很有用：

```
void ajGraphicsGetCharsize (float *defheight, float *currentheight);
```

ajGraphicsGetParamsPage 获取在 PLplot 内部定义的输出设备参数。这些参数的用处可能不如人们预期的那样大，因为有些参数针对每个设备驱动程序是硬编码的，或者只是 PLplot 中被忽略的用户值副本。在需要绘图尺寸时，请使用 ajGraphOpenMm 并以毫米为单位工作。

### 6.20.15 图表的计算属性

以下函数返回从图表中派生的一些计算值（以用户坐标表示）：

```
ajGraphicsCalcCoord    /* coordinates of a point on a circle knowing the angle. */
ajGraphicsCalcDistance /* Distances between 2 points. */
ajGraphicsCalcTextlengthC /* Text length. */
ajGraphicsCalcTextheight /* Text height. */
ajGraphicsCalcCharsize /* Text size (mm) to needed for given text length and height. */
```

有关如何使用这些函数的说明，请参阅在线文档。

### 6.20.16 图表调试函数

用于调试图表对象的函数具有前缀 ajGraphDebug。有关更多信息，请参阅在线文档。

### 6.20.17 直方图

直方图是图形绘制的一种特殊情况。提供了一组专用函数来处理底层图表对象和函数调用，因此您无需自行处理。

要绘制直方图，您首先必须创建一个直方图对象。提供了两个构造函数，它们接受数据集的数量（numofsets），每个集合都必须具有相同数量的数据点（numofpoints）：

```
AjPHist ajHistNew (ajint numofsets, ajint numofpoints);
AjPHist ajHistNewG (ajint numofsets, ajint numofpoints, AjPGraph graph);
```

ajHistNewG 还会将图表对象（作为参数传递）分配给返回的直方图。若干（numofsets）个图表会被添加到图表对象中。还会设置图表设备以及输出文件的名称和扩展名。

要为单集直方图设置标题，请使用以下函数之一：

```
/* Title */
void ajHistSetTitleC (AjPHist hist, const char* string);

/* x-axis label */
void ajHistSetXlabelC (AjPHist hist, const char* string);

/* y-axis left label */
void ajHistSetYlabelC (AjPHist hist,const char* string);

/* y-axis right label */
void ajHistSetRlabelC (AjPHist hist, const char* string);
```

要为多集直方图设置标题，请使用以下函数之一。index 是集中要将其标题设置为 title 的直方图的编号：

```
/* Title for histogram with multiple sets */
void ajHistSetmultiTitleC (AjPHist hist, ajint index, const AjPStr title);
/* x-axis title */
void ajHistSetmultiXlabelC (AjPHist hist, ajint index, const AjPStr title);
/* y-axis title */
void ajHistSetmultiYlabelC (AjPHist hist, ajint index, const AjPStr title);
```

ajHistSetmultiColour 和 ajHistSetmultiPattern 将为指定集（index）设置颜色或线型：

```
/* Set colour for bars in histogram */
void ajHistSetmultiColour(AjPHist hist, ajint index, ajint colour);
/* Set linestyle for set of bars */
void ajHistSetmultiPattern (AjPHist hist, ajint index, ajint style);
```

ajHistSetMono 对于单色打印很有用：

```
/* Set patterns instead of colours */
void ajHistSetMono (AjPHist hist, AjBool set);
```

要显示直方图，请调用 ajHistDisplay：

```
void ajHistDisplay (const AjPHist hist);
```

使用完直方图后，必须关闭输出文件并删除直方图对象。相关函数如下：

```
void ajHistogramClose (void);
void ajHistDel (AjPHist* hist);
```

ajHistDataAdd 和 ajHistDataCopy 用于为集中指定的直方图（index）指定一组数据点：

```
void ajHistDataAdd (AjPHist hist, ajint index, PLFLT *data);
void ajHistDataCopy (AjPHist hist, ajint index, const PLFLT *data);
```

ajHistDataAdd 将直方图设置为指向传递的数据，而 ajHistDataCopy 则复制数据。

下面的示例展示了一个函数，用于将整数数组（results）中保存的一组数据复制到直方图（hist）中。使用 ajHistDataCopy 来复制数据数组，因此可以删除 farray。如果改用 ajHistDataAdd，则不会调用 AJFREE：

```
void func(AjPHist hist, const ajint * results, ajint npts, ajint hist_num)
{
    ajint i;

    float *farray;

    AJCNEW(farray, npts);
    for(i=0; i<npts; i++)
        farray[i] = (float) results[i];

    ajHistDataCopy(hist, hist_num, farray);
    AJFREE(farray);
}
```

## 6.21 处理数学

### 6.21.1 简介

EMBOSS 提供了一个基本数学库，包括用于数据类型转换、随机数生成、舍入和其他基础功能的函数。

### 6.21.2 AJAX 库文件

用于处理数学的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajmath | 通用数学函数 |
| ajvector | 用于处理向量的函数 |

ajmath.h/c。用于数字舍入、坐标转换、随机数生成等的通用数学函数。

ajvector.h/c。用于处理 3D 空间中向量的数据结构和函数。本文未对该库进行描述，有关更多信息，请参阅在线库文档。

### 6.21.3 ACD 数据类型

没有专门用于数学的 ACD 数据类型。

### 6.21.4 AJAX 数据类型

没有专门用于数学的 AJAX 数据类型。

### 6.21.5 转换函数

提供了用于在一种数据类型与另一种数据类型之间转换的函数。这些函数都具有前缀 ajCvt。要在极坐标和笛卡尔坐标之间相互转换、将弧度转换为角度，或根据高斯分布返回概率，请使用：

```
float ajCvtDegToRad (float degrees);
void ajCvtPolToRec (float radius, float angle, float* Px, float* Py);
float ajCvtRadToDeg (float radians);
void ajCvtRecToPol (float x, float y, float* Pradius, float* Pangle);
double ajCvtGaussToProb (float mean, float sd, float score);
```

序列位置通常由用户在命令行中指定。EMBOSS 支持序列位置的负值，这些值被解释为从序列 _末尾_ 开始的偏移量。提供了两个函数，用于将 EMBOSS 序列位置转换为真实位置（例如，可用于对序列本身进行索引）。这些函数返回 0（序列起始位置）到序列长度减 1 之间的整数：

```
ajint ajCvtSposToPos (ajint len, ajint ipos);
ajint ajCvtSposToPosStart (ajint len, ajint imin, ajint ipos);
```

在这两种情况下，len 是序列的长度，ipos 是位置。值 0 表示序列的起始位置，而负数表示从序列末尾开始的偏移量。可以指定最小相对位置（imin）。

### 6.21.6 随机数函数

有三个用于随机数生成的函数。这些函数基于 dprand 和 sdprand，并经 N. M. Maclaren（版权所有，剑桥大学）许可使用。ajRandomSeed 初始化随机数生成，必须在 ajRandomNumber（返回 0 到 32767 之间的随机整数）和 ajRandomDouble（返回 0.0 到 1.0 之间的随机双精度值）之前调用：

```
void ajRandomSeed (void);
double ajRandomNumber (void);
double ajRandomDouble (void);
```

### 6.21.7 舍入

有两个函数用于对数字进行舍入，要么将 float 舍入为 int，要么将 float 舍入为 float，并为累加指定保留的位数：

```
ajint ajRound (ajint i, ajint round);
float ajRoundFloat (float f, ajint nbits);
```





### 6.21.8 杂项函数

提供了各种杂项函数，例如，用于计算几何平均数、两个数的模数，或蛋白质序列的 32 位或 64 位 SwissProt 风格校验和：

```c
float ajMathGmean (const float* Parr, ajint n);
ajint ajMathModulo (ajint i1, ajint i2);
ajuint ajMathCrc32 (const AjPStr str);
unsigned long long ajMathCrc64 (const AjPStr str);
```

## 6.22 处理系统代码

### 6.22.1 简介

EMBOSS 提供了与系统交互和处理系统特定代码的基本功能。涵盖的领域包括：

- 用于调用外部应用程序的系统调用
- 用于解析应用程序命令行的代码
- 用于将一种类型转换为另一种类型的函数
- 低级文件处理
- 调用（经过一些修改）标准 C 函数的包装函数，主要用于克服标准 C 函数的系统相关限制
- 调用带有或不带有内部清理和报告的 C 函数 exit 的函数
- 用于反转不同数据类型中字节顺序的函数

### 6.22.2 AJAX 库文件

用于处理系统调用的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| :--- | :--- |
| ajsys | 系统函数 |
| ajutil | 系统函数 |

ajsys.h/c. 系统函数，主要用于文件和目录的低级处理以及系统特定函数。

ajutil.h/c. 用于干净退出、内存清理、操作字节等功能的函数。

### 6.22.3 ACD 数据类型

没有专门用于系统处理的 ACD 数据类型。

### 6.22.4 AJAX 数据类型

没有专门用于系统处理的 AJAX 数据类型。

### 6.22.5 系统调用

有两个函数用于调用外部应用程序。ajSysSystem 将在当前路径中调用用户可执行文件，而 ajSysSystemEnv 将使用其中提供的包括 PATH 在内的环境：

```c
void ajSysSystem (const AjPStr str);
void ajSysSystemEnv (const AjPStr str, char* const env[]);
```

### 6.22.6 应用程序参数

函数 ajSysArglistBuild 从任何应用程序命令行中提取应用程序名称（name）和参数列表（PParlist）：

```c
AjBool ajSysArglistBuild (const AjPStr cmdline, char** name, char*** PParlist);
```

该函数分配一个字符串（name）和一个以 NULL 结尾的字符串数组（PParlist），稍后通过调用 AJFREE 和 ajSysArglistFree 释放：

```c
AjPStr cmdline = NULL;
char **arglist = NULL;
char *name;

/* The command line must be assigned to a string */
cmdline = ajStrNewC("ApplicationName arg1 arg1val arg2 arg2val");

ajSysArglistBuild (cmdline, &name, &arglist);

/* Do something with the name and argument list. Individual args are in arglist[0],
   arglist[1] etc. */

AJFREE(name);
ajSysArglistFree(&arglist);
```

### 6.22.7 强制转换函数

提供了将整数强制转换为字符类型的函数：

```c
char ajSysCastItoc (ajint i);
unsigned char ajSysCastItouc (ajint i);
```

### 6.22.8 文件函数

有三个函数可用于低级文件处理。
ajSysFileWhich 将在当前路径中搜索用户可执行文件，而
ajSysFileWhichEnv 将使用由参数提供的环境中的 PATH。
如果找到了可执行文件，则函数返回 ajTrue：

```c
AjBool ajSysFileWhich (AjPStr* Pstr);
AjBool ajSysFileWhichEnv (AjPStr* Pstr, char* const env[]);
```

ajSysFileUnlink 用于安全删除文件或链接：

```c
AjBool ajSysFileUnlink (const AjPStr str);
```

### 6.22.9 C 函数包装器

提供了各种函数，用于包装（经过一些修改）标准 C 函数。在大多数情况下，这些函数是为了克服标准 C 函数的系统相关限制而提供的。这些函数带有前缀 ajSysFunc，包括：

```c
char* ajSysFuncStrtok (const char* txt1, const char* txt2);
char* ajSysFuncStrtokR (const char* txt1, const char* txt2, char** Ptxt, AjPStr* Pbuf);
char* ajSysFuncFgets (char* buf, int n, FILE* fp);
char* ajSysFuncFopen (const char* txt, const char* flags);
FILE* ajSysFuncFdopen (ajint filedes, const char* mode);
```

### 6.22.10 来自 ajutil.c/h 的函数

以下函数调用 C 函数 exit。从应用程序代码中调用以退出应用程序的 embExit* 函数（定义在 embexit.h/c 中）使用这些函数：

```c
/* Exits with a success code (zero) after cleanup routines */
__noreturn void ajExit (void);

/* Exits with an unsuccessful code without flushing files or clean-up. */
__noreturn void ajExitAbort (void);

/* Exits with an unsuccessful code without clean-up. */
__noreturn void ajExitBad (void);
```

ajExit() 在调用报告资源使用情况等的清理例程后，以成功代码（零）调用 exit。

ajExitAbort() 以不成功代码（EXIT_FAILURE，定义在 stdlib.h 中）调用 exit，而不刷新任何文件。这对于从失败的系统调用（例如 ajFileNewInPipe）中退出是必需的，在这种情况下，父进程有打开的输出文件，子进程需要在不影响它们的情况下退出。以这种方式未能退出可能意味着输出缓冲区被刷新两次。不会调用任何清理或报告例程。

ajExitBad() 以不成功代码（EXIT_FAILURE）调用 exit()。不会调用任何清理或报告例程。

以下函数都会反转指示数据类型中的字节顺序：

```c
void ajByteRevLen2 (short* i);        /* 2 byte integer    */
void ajByteRevLen4 (ajint* i);        /* 4 byte integer    */
void ajByteRevLen8 (ajlong* i);       /* 8 byte integer    */
void ajByteRevInt (ajint* sval);      /* integer           */
void ajByteRevShort (short* ival);    /* unsigned integer  */
void ajByteRevLong (ajlong* lval);    /* long              */
void ajByteRevUint (ajuint* ival);    /* unsigned integer  */
```

最后，还有几个有用的杂项函数：

```c
/* If a log file is in use then this writes run details to end of file. */
void ajUtilLoginfo (void);

/* Dummy function for use in debugging */
void ajUtilCatch (void);

/* Tests whether the host system uses big endian byte order. */
AjBool ajUtilGetBigendian (void);

/* Returns the user's userid. */
AjBool ajUtilGetUid (AjPStr* dest);

/* Returns a command line with all options changed by the user */
const AjPStr ajUtilGetCmdline (void);

/* Returns the user non-default inputs in commandline form */
const AjPStr ajUtilGetInputs (void);

/* Return the program name */
const AjPStr ajUtilGetProgram (void);
```

ajUtilCatch 应在使用 GDB 调试时的特殊情况下调用。要使用，只需在代码中放入对 ajUtilCatch() 的调用，并在 GDB 中使用“break ajUtilCatch”以获取回溯。

## 6.23 处理异常消息

### 6.23.1 简介

EMBOSS 提供了一组有用的异常处理函数，这些函数在调用输出消息的函数之前格式化异常消息。可用的行为如下：

- 调用注册的异常处理函数（见下文）
- 报告信息性消息
- 报告警告消息
- 报告错误消息
- 转储诊断数据
- 退出
- 崩溃（终止）应用程序
- 调试

最广泛使用的是函数 ajFatal（崩溃应用程序）、ajWarn（警告消息）和 ajDebug（调试）（参见第 3.3 节，‘调试’）。

在极少数情况下，编写自己的自定义异常处理函数是可取的，并为此提供了函数。还有用于查询或设置消息处理内部状态的函数。您通常不需要这些函数，但在编写自己的异常处理代码时它们可能会很有用。

### 6.23.2 AJAX 库文件

用于处理消息的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajmess | 消息处理 |
| ajexcept | 内部异常处理函数 |
| ajassert | 用于处理断言的函数 |

ajmess.h/c. 定义错误消息对象（AjPError）和消息处理函数。它还包含用于在低级别处理消息的静态数据结构和函数。除非您计划扩展核心库功能，否则不太可能需要静态数据类型和函数。

ajexcept.h/c. 包含用于引发异常的 ajExceptRaise 函数。

ajassert.h/c. 包含用于处理断言的函数。最简单的用法是添加一行：

```c
AjPStr mystring = NULL;

/* ... some code ... */

assert(mystring);
```

当 mystring 为 NULL 值时，这将引发致命异常。

### 6.23.3 ACD 数据类型

没有专门用于消息的 ACD 数据类型。





## 6.23.4 处理消息的 AJAX 数据类型

处理消息请使用：

- AjPError 错误消息级别信息

这些在内部使用。用于处理异常，请定义带有文本描述的 Except_T，并使用 AJRAISE 宏来报告文本字符串以及源文件的名称和行号。异常处理数据类型如下：

- Except_T 异常类型
- Except_Frame 用于异常堆栈

就所有实际目的而言，您无需直接处理这些对象。

## 6.23.5 消息函数

用于格式化消息（作为字符串提供）的函数都带有名称简短易记的便捷包装函数：

```
void ajDebug (const char *fmt, ...);
void ajDie (const char *format, ...);
void ajErr (const char *format, ...) ;
void ajUser (const char *format, ...) ;
void ajWarn (const char *format, ...);
void ajMessDump (const char *format, ...);
void ajMessExitmsg(const char *format, ...);
```

所有这些函数都会调用内部定义的消息输出函数。

调用函数时传入消息文本，例如：

```
ajWarn("This is a silly warning message");
```

调用当然可以包含要打印的变量：

```
ajint x=0;
...
ajWarn("This is a silly warning message which prints integer value %d", x);
```

如果已启用调试，ajDebug 会将调试消息写入调试文件。调试通常通过在命令行中添加 -debug 或定义环境变量 EMBOSS_DEBUG 来启用。您应避免在可能在命令行处理完成之前被调用的任何代码中使用 ajDebug，因为调试文件尚未创建。

ajMessExitmsg 在退出前不会提供输出已记录错误消息的机会，但对于处理那些虽然不可恢复但并非 EMBOSS 代码本身问题的错误很有用。

## 6.23.6 查询消息处理状态

提供了一些函数来查询消息处理的内部状态。这些函数都带有前缀 ajMessGet。例如，可以检索错误例程被调用的次数、当前消息文本、来自标准 C 函数 strerror 的系统错误消息文本或用于调试输出的文件：

```c
ajint ajMessGetCountError (void);
const char* ajMessGetMessageC (void);
const char* ajMessGetSysmessageC (void);
FILE* ajMessGetDebugfile (void);
```

## 6.23.7 与用户交互

在 EMBOSS 应用程序的初始化期间，一个函数用于所有用户提示。ajUserGet 向用户写入提示并读取一行响应。ajMessBeep 生成可听警告：

```c
ajint ajUserGet (AjPStr* pthis, const char* fmt, ...);
void ajMessBeep (void);
```

## 6.23.8 杂项函数

要手动引发异常，可以使用 ajExceptRaise（定义在 ajexcept.h/c 中）。该函数作为名为 (AJRAISE) 的宏提供：

```c
__noreturn void ajExceptRaise(const T* e, const char* file, ajint line);
#define AJRAISE(e) ajExceptRaise(&(e), __FILE__, __LINE__)
```

它会检查异常，如果捕获到异常，则会调用注册的异常例程。否则，它将在中止程序之前，带有源代码文件名和代码行号的异常消息引发异常。

应始终使用宏版本。例如：

```c
static const Except_T Mem_Failed =
{
    "Allocation failed, insufficient memory available"
};

static const Except_T Mem_Badcount =
{
    "Allocation bad byte count"
};
/* Allocates memory using malloc, and fails with an error message if unsuccessful:
   nbytes : number of bytes required
   file   : source file name (generated by macro)
   line   : source line number (generated by a macro)
```

## 6.23 处理异常消息

```c
void *ajMemAlloc(size_t nbytes, const char* file, ajint line)
{
    void *ptr;

    if(nbytes <= 0)
        ajExceptRaise(&Mem_Badcount, file, line);

    ptr = malloc(nbytes);

    if(ptr == NULL)
    {
        if(file == NULL)
            AJRAISE(Mem_Failed);
        else
            ajExceptRaise(&Mem_Failed, file, line);
    }
}
```

# 质量保证

### 7.1 一般质量保证

为保持软件包的质量和完整性，对 EMBOSS 代码和文档执行了各种质量保证（QA）测试。

- 在各种平台上进行测试构建，以突出任何编译器警告
- 在测试数据（包括预期的失败条件）上运行应用程序测试
- 使用 valgrind 进行应用程序内存泄漏测试
- 验证 C 源代码文档和 SRS 中的索引
- 验证和标准化应用程序 ACD 文件
- 验证 EMBOSS 文档，包括完整性测试
- 自动更新应用程序文档（主要是命令行限定符和用法示例，包括输入和输出文件）。

这些测试由 EMBOSS 开发人员执行，但有办法可以提供帮助。您应该为开发的任何应用程序提供带有测试数据的测试（见下文），并为任何新的库代码（见附录 D，代码文档标准）和应用程序（见第 8 章，应用程序文档标准）提供充分的文档。

### 7.2 应用程序质量保证

测试数据由一个或多个输入文件、应用程序参数和相应的输出文件组成。每组对应应用程序的一次运行。应尽可能提供多组测试数据，特别是针对异常输入条件，以提供尽可能强健的测试。

### 注意

QA 测试定义用于为应用程序文档的三个部分生成包含文件：用法、输入和输出。这些文件为任何带有后缀 -ex（示例）、-keep（由其他测试重用的输出）或 -check 的 QA 测试创建。所有其他测试名称仅用于 QA 测试，不会成为应用程序文档的一部分。

测试定义在文件中：

```
.../emboss/test/qatest.dat
```

qatest.dat 中条目的示例如下所示：

```
ID myprogram-ex
AB myemboss
AA myprogram
IN
FI stderr
FC =2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI P10932.myprogram
FC =5
FP /^Usa: temb1-id:P10932\n/
FP /^Length: 2167\n/
//
```

测试包括有关参数（命令行）以及输出文件中预期内容的信息。qatest.dat 开头的文档描述了用于定义测试的记录。

### 7.2.1 测试记录

文件 qatest.dat 中使用的记录如下表总结。

| 记录 | 简短描述 | 要求 |
| :--- | :--- | :--- |
| ID | 测试标识符 | 必需 |
| AA ApplicationName-Tag | EMBASSY 应用程序的应用程序名称 | EMBASSY 应用程序必需 |
| AB PackageName | EMBASSY 包名称 | 使用 AA 记录时必需 |
| AP ApplicationName | 标准 EMBOSS 应用程序的应用程序名称 | 标准 EMBOSS 应用程序必需 |
| AQ ApplicationName | ‘make check’ EMBOSS 应用程序的应用程序名称 | ‘make check’ EMBOSS 应用程序必需 |
| CC comment | 注释 | 可选 |
| CL command | 命令行参数 | 可选 |
| DI directory | 输出子目录 | 使用输出子目录时必需 |
| DF FileName | 输出子目录中文件的名称 | 可选 |
| DL directive | 测试完成时结果目录的指令 | 可选 |
| ER ErrorCode | 错误返回代码 | 可选 |
| FI FileName | 结果目录中输出文件的名称 | 主结果目录中创建的所有文件必需 |
| FC [<=] NumberLines | 测试前一个 FI 文件中的行数 | 如果未定义 FZ 记录，则除 stdout 和 stderr 外的所有文件必需，否则可选 |
| FP count / regexp / | 测试前一个 FI 文件中的模式 | 除 stdout 和 stderr 外的所有文件必需 |
| FZ [<=] FileSize | 测试前一个 FI 文件的大小 | 如果未定义 FC 记录，则除 stdout 和 stderr 外的所有文件必需，否则可选。 |
| IC text | 输入上的注释 | 可选 |
| IN UserInput | 用于响应 EMBOSS 提示的值 | 应用程序将提示的每个应用程序选项必需 |
| OC text | 输出上的注释 | 可选 |
| PP command | 预处理器命令 | 可选 |
| QQ command | 后处理器命令 | 可选 |
| RQ RequiredApps | 所需的外部程序 | 需要其他应用程序才能运行的应用程序必需，例如应用程序包装器 |
| TI seconds | 测试时间限制 | 可选 |
| UC text | 用法示例上的注释 | 可选 |
| ## | 注释 | 可选 |

### 7.2.1.1 ID ApplicationName-Tag

标识符的一般形式为 ApplicationName-Tag，其中 ApplicationName 是正在测试的应用程序的名称，Tag 指示正在执行什么类型的测试。

运行测试时，会在 /emboss/test/ 下创建一个目录来保存测试运行的输出。这包括所有应用程序输出文件以及应用程序写入 UNIX 文件流 stdout 和 stderr 的任何输出的文件。标识符定义名称



的目录。例如，如果标识符为 myprogram-ex，则会创建名为 test/qa/myprogram-ex 的目录。

标记可以是以下任意一种：

- -ex 用于在应用程序 HTML 文档中创建第一个用法示例的测试。-ex 后面可以跟一个数字，以指示第二个及后续测试（见下文）。

- -ex2、-ex3 等。文档中用于用法示例的进一步测试。通常，所有此类示例都应对应 qatest.dat 中定义的测试，以确保文档正确。

- -keep 用于测试在文档中使用且测试完成后保留测试输出的情况。该测试应包含 DL keep 记录。当测试输出被后续测试读取时使用此项，如数据库索引的情况。重要的是，此测试必须出现在使用结果的任何测试之前。

- -keep2、-keep3 等。-keep 后面可以跟一个数字，以指示第二个及后续测试。

- -fail 用于故障条件的测试。此类测试通常包含 ER 记录，以指示错误返回码。

## 7.2.1.2 AA ApplicationName

此项用于生成命令行并用于报告统计信息。如果为 EMBASSY 包指定了 AA 记录，则必须在测试定义中使用 AB 记录对其进行标识。应用程序（ApplicationName）必须通过对包使用 make 来构建。如果未找到应用程序，qatest 将假设未安装此 EMBASSY 包且不会运行测试。

## 7.2.1.3 AB PackageName

此项告知 qatest 脚本，测试依赖于安装 EMBASSY 包（PackageName），如果未安装该包，可能无法找到二进制文件。

## 7.2.1.4 AP ApplicationName

此项用于生成命令行并用于报告统计信息。应用程序（ApplicationName）必须通过使用 make 来构建。测试始终由 qatest 脚本执行。

## 7.2.1.5 AQ ApplicationName

此项用于生成命令行并用于报告统计信息。应用程序（ApplicationName）必须通过使用 make check 来构建。qatest 脚本将在构建目录中查找可执行文件，因为此应用程序不会被安装。如果未找到应用程序，qatest 将假设未运行 make check 并跳过测试。

## 7.2.1.6 CC comment

用于对失败测试进行注释。注释（_注释_）将在失败时出现在测试输出中，作为可接受故障条件的指南。在这种情况下，错误消息的文本将使用例如 FP 记录（见下文）进行验证。

记录 ##（见下文）用于测试定义中的更通用注释。

## 7.2.1.7 CL command

这是不带应用程序名称的命令行（_命令_）。命令行可以跨越多个 CL 记录，在这种情况下，CL 标记后的文本将被追加，并在每行文本之间插入一个空格。

## 7.2.1.8 DI directory

这是在结果目录（由 ID 记录定义）中创建的目录（_目录_）的名称，可用于在应用程序打开新输出目录时保存输出。目前，测试检查每个文件是否在 DF 行中命名，但无法直接为这些子目录中的文件内容定义测试。但是，可以使用 QQ 后处理命令（见下文）将内容复制到另一个文件（在主结果目录中），然后可以对其进行测试，例如针对大小和模式。

## 7.2.1.9 DF FileName

这是在结果目录的子目录中创建的文件（_文件名_）的名称。文件所属的子目录由前面的 DI 记录标识；DF 记录必须列在相应的 DI 记录下。必须写入这些文件，测试才能通过。

## 7.2.1.10 DL directive

此项控制测试完成后对结果目录的处理方式。_指令_ 可以是以下之一：

- - success：成功时删除测试目录。这是默认行为。
- - all：始终删除测试目录。
- - keep：始终保留测试结果目录。当另一个测试重用结果时使用此项，如数据库索引的情况。

## 7.2.1.11 ER ErrorCode

预期的错误代码（_错误代码_）。此项用于测试故障条件的测试。如果应用程序未返回指定的错误代码，测试将报告错误。所有成功的应用程序返回 0，失败的返回 1。

## 7.2.1.12 FI FileName

目前，FI 记录只能引用主结果目录中的文件，而不能引用结果目录子目录中的文件。文件名（_文件名_）无需给出 `stdout` 和 `stderr`，它们被假定存在且可能为空，除非另有定义。

## 7.2.1.13 FC [<=] NumberLines

为了使测试通过，行数（NumberLines）可以按以下方式检查：

- = 必须有 NumberLines 行
- < 必须有多于 NumberLines 行
- > 必须有少于 NumberLines 行

## 7.2.1.14 FP count / regexp /

为了使测试通过，斜杠之间给出的 Perl 正则表达式 regexp 必须在前面的 FI 文件中找到。表达式前可以加上一个可选整数（count）来检查模式的精确数量。

此记录可用于检查 stderr（通常包含用户提示）中是否缺少异常消息（警告、错误或致命错误）。

## 7.2.1.15 FZ [<=] FileSize

为了使测试通过，文件大小（FileSize）可以按以下方式检查：

- = 文件必须恰好为 FileSize
- < 文件必须大于 FileSize
- > 文件必须小于 FileSize

存在一个隐式测试，即 stdout 和 stderr 的大小必须为零，除非另有说明。

## 7.2.1.16 IC text

这是用于输入的注释（text），由 makeexample.pl 在创建 HTML 文档文件时使用。该信息不用于 QA 测试。

## 7.2.1.17 IN UserInput

将使用值 UserInput。如果行中没有内容，则向应用程序输入一个空行，应用程序将使用选项的默认值（如果已定义）。在有条件地提示选项的地方需要小心。

## 7.2.1.18 OC text

这是用于输出的注释（text），由 makeexample.pl 在创建 HTML 文档文件时使用。该信息不用于 QA 测试。

## 7.2.1.19 PP command

这是在运行测试前执行（由 /bin/sh）的命令。每个 PP 行定义一个命令：长命令不能像 CL 记录允许的那样跨多行连接。

典型用途是为应用程序设置所需的环境变量。变量应始终导出（这是 /bin/sh），例如：

```
PP EMBOSS_ACDROOT=.../acd
PP export EMBOSS_ACDROOT
```

## 7.2.1.20 QQ command

这是在运行测试后执行（由 /bin/sh）的命令。每个 QQ 行定义一个命令：长命令不能像 CL 记录允许的那样跨多行连接。

目前未使用此项，但最可能的应用是将目录内容列出到另一个文件中，然后可以对其进行大小和模式测试。

## 7.2.1.21 RQ RequiredApps

这是测试所依赖的应用程序。每个 RQ 记录应给出一个所需的'助手'应用程序。例如，使用 getz 的测试需要 srs，或者 emma 需要 clustalw。

## 7.2.1.22 TI seconds

这是测试超时的时间限制。默认值为 60 秒。在负载较高的系统上，一些示例可能需要更长时间。

## 7.2.1.23 UC text

这是用于 QA 测试本身的注释（text），由 makeexample.pl 在创建 HTML 文档文件时使用。该信息不用于 QA 测试。

## 7.2.1.24 ##

这是测试定义中的一般注释，不会被报告。应使用 CC 记录来对失败测试进行注释。

## 7.2.2 编写应用程序质量保证测试

新应用程序的质量保证测试必须添加到文件 qatest.dat 的相应位置。例如，如果您正在为 EMBASSY 包 myemboss 中的应用程序编写测试，则应搜索行 "AB myemboss" 并在其下添加测试。测试至少应包括以下记录：

- - 带有测试标识符代码的 ID 记录
- - 用于应用程序名称的 AA（EMBASSY）或 AP 或 AQ（EMBOSS）记录，以及带有 EMBASSY 包名称的 AB 记录（如果适用）
- - 给出测试命令行中任何选项的 CL 记录和/或一个或多个 IN 行，以响应程序的任何输入请求。每个提示都需要一个 IN 记录，如果默认响应可接受，则可以为空
- - 每个输出文件名称的 FI 记录





- 每个 FI 文件下的 FC 记录用于测试正确的行数，或 FZ 记录用于测试文件大小
- 每个 FI 记录下的一个或多个 FP 测试用于测试文件内容
- 一个或多个 DI 记录用于其被使用的输出子目录
- 一个 RQ 记录用于所需应用程序的名称（如果有的话）
- 应为 stderr 和 stdout 中的每一个提供 FI、FZ（或 FC）和 FP 记录

## 7.2.2.1 测试数据的位置

任何测试数据，即应用程序所需的输入文件，都应添加到目录：

```
emboss/test/data
```

如果需要许多输入文件，为了保持整洁，可以将它们放在上述目录的子目录下。无论哪种情况，都不应不必要地创建文件：很可能，emboss/test/data 下已经存在一个适合您需求的文件。有关此目录内容的更多信息将在下文介绍（第 7.2.4 节，*有用的文件和目录*）。

## 7.2.3 运行应用程序质量保证测试

要执行测试，必须编辑您的 .embossrc 文件（在您的主目录中）或 emboss.default 文件，以将 EMBOSS 环境变量 emboss_qadata 设置为测试目录，例如：

```
/home/auser/emboss/emboss/test
```

要运行测试，必须运行脚本：

```
/emboss/scripts/qatest.pl
```

从目录 /emboss/test/qa 运行。命令的形式如下：

```
qatest.pl TestIdentifier
```

其中 TestIdentifier 是 qatest.dat 中相应条目的 ID 记录上给出的测试标识符。

### 7.2.3.1 示例测试

假设您想运行先前在 qatest.dat 中显示的示例条目：

```
ID myprogram-ex
AB myemboss
AA myprogram
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI P10932.myprogram
FC = 5
FP /^Usage: embl-id:P10932\n/
FP /^Length: 2167\n/
//
```

还假设您位于目录 emboss/test 中。要运行测试 myprogram-ex，您将键入：

```
cd qa
../../scripts/qatest.pl myprogram-ex -keep
```

如果测试完成后要保留输出文件，对于不包含 DL keep 记录的测试，则必须使用 -keep 限定符调用 qatest.pl。如果不这样做，输出文件将被删除。因此，如果测试包含以下行：

```
ID myprogram-keep
DL keep
```

则将这样调用它：

```
../../scripts/qatest.pl myprogram-ex
```

无论哪种情况，输出文件都将在主结果目录中创建。如果测试标识符行是

```
ID myprogram-ex
```

则结果目录将是：

```
emboss/qa/myprogram-ex
```

对于其他测试，文件也可能写入主结果目录中的子目录（请参阅 DI 和 DF 记录）。

如果在未在 qatest.dat 中定义的内容上运行 qatest.pl，它将报告：

```
Tests total: 0.
```

如果成功，除非测试条目包含 DL keep 行，或命令行上指定了 -keep，否则所有文件都将被删除。

如果失败，它将报告原因，并且所有结果都将保存在结果目录中以供检查。例如，您会检查 myprogram-ex，然后确定问题，更新测试定义，并重试直到成功。

典型会话如下所示：

```
../scripts/qatest.pl -without=srs
Tests total: 1586 pass: 1586 fail: 0
Skipped: 12 check: 1 embassy: 0 requirements: 11
Missing documentation html: 0 text: 0 sourceforge: 0
Time: 677 seconds
```

## 7.2.4 有用的文件和目录

在 /emboss/test/ 下存放了一些有用的文件。目录如下：

- **acd**: 测试应用程序的 ACD 文件。这些文件用于测试 ACD 文件解析。除非您扩展 ACD，否则不需要此目录。
- **data**: 已提及的测试数据目录。您的测试数据输入文件应放在此处，或放在其下的子目录中。
- **gb**: NBRF/GCG 数据库格式中的一些 GenBank 数据文件。
- **qa**: 必须从中运行所有测试的目录。应用程序输出文件写入其下方的各自结果目录，并在测试成功完成后删除，除非另有说明。
- **rc**: 此目录用于数据库和资源定义测试。您不需要它。
- **swnew**: 来自 SwissProt 数据库的文件，用于创建 tsw 测试数据库。
- **embl**: 来自 EMBL 数据库的文件，用于创建 tembl 测试数据库。
- **genbank**: 用于创建 tgenbank 测试数据库的一些 GenBank 数据文件。
- **memtest**: 用于跟踪内存泄漏的文件：您不需要此文件。
- **pir**: 来自 PIR 数据库的数据文件，用于创建 tpir 测试数据库。
- **swiss**: 来自 SwissProt 数据库的数据文件。
- **wormpep**: 来自 WormPep（蠕虫肽）数据库的数据文件。

## 8.1 简介

此处的准则描述了如何编写符合在线使用的 EMBOSS 风格的新应用程序文档：

```
http://emboss.open-bio.org/rel/dev/apps/
```

它们还涵盖 EMBASSY 包的文档：

```
http://emboss.open-bio.org/rel/dev/apps/EMBASSYPackagesTable.html
```

要了解文档情况，例如，请查看 seqret 应用程序的文档：

```
http://emboss.open-bio.org/rel/dev/apps/seqret.html
```

以及 HMMER 包的文档：

```
http://emboss.open-bio.org/rel/dev/apps/hmmer.html
```

您会注意到，应用程序和包文档被组织成各个部分，以便于导航。下文将解释各个部分以及生成文档的流程。

## 8.2 应用程序文档

### 8.2.1 ACD 文件文档

应用程序 ACD 文件（请参见第 5 章，C 编程）不需要显式文档，但在某些情况下，添加注释会很有帮助。注释行以 # 开头并持续到行尾（请参见第 4.1 节，*ACD 文件开发简介*）。

ACD 文件包括描述应用程序本身的应用程序定义，以及描述参数的一个或多个数据定义。定义具有详细描述应用程序或参数的属性。数据定义在文件中组织为“输入”、“输出”等部分。在生成应用程序文档时，会解析 ACD 文件。使用的组件包括：

- 应用程序名称（来自应用程序定义）和简短描述（来自应用程序定义的 `documentation:` 属性）
- 示例数据文件（来自“输入”部分）
- 命令行概要
- 应用程序选项表（来自数据定义）
- 相关应用程序链接列表（来自应用程序定义的 `groups:` 属性）。

因此，您应使用为此目的提供的实用程序来确保应用程序 ACD 文件有效且格式正确。

### 8.2.1.1 应用程序质量保证测试

应用程序 QA 测试的命令行会话包含在应用程序文档中。因此，您应在记录应用程序之前编写并运行这些测试（请参见第 7.2 节，*应用程序质量保证*），以确保示例文件能够正确生成。

如果您在记录应用程序之前未编写 QA 测试，请重新运行 `autodoc.pl`，它将创建其余三个包含文件（用法示例以及输入和输出文件），完整的 HTML 文档将创建在 `embassy/myemboss/emboss_doc/html/myprogram.html`

### 8.2.2 应用程序文档的各个部分

应用程序文档中的各个部分在下表中描述。

### 8.2.3 应用程序文档生成流程

生成应用程序文档的流程结合了手动编写的组件和自动生成的部分（主要来自解析 ACD 文件和 QA 测试）。该流程在很大程度上是自动化的，涉及运行 `autodoc.pl` 脚本，该脚本生成一个部分完成的*应用程序模板*，您需要手动完成它。

应用程序名称和索引术语直接写入应用程序模板。但是，大部分自动生成的内容保存在*包含文件*中，这些文件从模板 XML 包含文件生成。

`autodoc.pl` 包含在 EMBOSS 发行版的 `scripts` 目录下，例如：

```
/home/auser/emboss/emboss/scripts/autodoc.pl
```



| 章节 | 描述 | 生成方式 |
|---|---|---|
| Name | 应用程序名称、简短描述和版本号。 | 从应用程序 C 源代码和 ACD 文件自动生成。 |
| Function | 对应用程序输入、输出和功能的简洁、正式描述。 | 由应用程序作者编写。 |
| Description | 适合生物学最终用户的应用程序描述。 | 由应用程序作者编写。 |
| Command line arguments | 如何在命令行中使用应用程序的概要，包括命令行概要和参数表。 | 自动生成。 |
| Usage | 用法示例，即命令行会话，或例如 wEMBOSS、Jemboss 或 SOAPLAB 中的等效内容。 | 从质量保证测试用例自动生成。 |
| Input Files | 示例输入文件。可选的输入文件描述（例如文件格式）或指向同一文件的 URL。 | 示例输入文件从测试用例自动生成。描述由应用程序作者编写。 |
| Data Files | 数据文件示例。可选的数据文件描述（例如文件格式）或指向同一文件的 URL。 | 示例数据文件从 ACD 文件自动生成。描述由应用程序作者编写。 |
| Output Files | 示例输出文件。可选的输出文件描述（例如文件格式）或指向同一文件的 URL。 | 示例输出文件从测试用例自动生成。描述由应用程序作者编写。 |
| Algorithm | 适合计算机科学家的算法技术描述。 | 由应用程序作者编写。 |
| Notes | 外围文档，例如使用说明。 | 由应用程序作者编写。 |
| Warnings | 谨慎的使用建议、已知错误等。 | 由应用程序作者编写。应用程序特定的消息可以通过搜索代码找到。 |
| Diagnostics | 应用程序可能生成的诊断警告和错误消息。 | 由应用程序作者编写。应用程序特定的消息可以通过搜索代码找到。 |
| Authors | 作者联系信息。 | 从源代码自动生成。 |
| Revision History | 应用程序修订历史，包括上次修订日期、修订作者姓名和关于修订的简要说明。 | 用于主要修订。EMBOSS 代码的详细历史记录可在 CVS 中查找。 |
| References | 文献参考和如何引用应用程序的说明。 | 如何引用 EMBOSS 的说明会自动包含。否则，由应用程序作者编写。 |
| See Also | 同一组中应用程序的链接列表。 | 从 ACD 文件自动生成。 |
| Target Users | 应用程序面向的用户群（例如生物学家、生物信息学家、系统管理员等）。 | 由应用程序作者编写。 |
| Exit Status | 应用程序退出时可能返回给操作系统的值。 | 从源代码自动生成。 |

要记录一个新程序，首先确保你有一组最新的已编译程序，并且你编写但不属于主 EMBOSS 包的任何程序都已删除其可执行文件。否则，对它们的引用可能出现在自动生成的 "See Also" 部分中（见上文）。ACD 文件应完整且经过验证，并且应用程序的 QA 测试应已运行。

要生成文档，请依次对要记录的每个应用程序运行 autodoc.pl。

对于 EMBOSS 应用程序：

```
autodoc.pl ApplicationName
```

对于 EMBASSY 应用程序：

```
autodoc.pl -embassy=PackageName ApplicationName
```

应将 PackageName 和 ApplicationName 替换为合适的名称。以下示例假设你正在 EMBASSY 包 myemboss 中工作，并编写名为 myprogram 的程序。要记录该应用程序：

- 1. 移动到文档目录：

```
cd embassy/myemboss/emboss_doc/master
```

- 2. emboss_doc/master 目录中有一个用于记录 myemboss 应用程序的模板文件。将应用程序模板复制到同一目录下名为 myprogram.html 的文件：

```
cp template.html.save myprogram.html
```

- 3. 编辑此文件，将 'ProgramNameToBeReplaced' 替换为应用程序名称。这为文档的自动生成元素定义了命名的包含文件。

- 4. 运行 autodoc.pl：

```
autodoc.pl -embassy=myemboss myprogram
```

- 5. 在指定位置（见下文）编写文档文本以完成 myprogram.html。

该脚本将运行 wossname 以检查 myprogram 是否确实存在，然后生成带有包含指令的应用程序模板文档文件（供你填写），以及以下部分的包含文件：

- Name（整个部分）
- Synopsis（整个部分）
- Data Files（数据文件示例）
- Authors（整个部分）
- Revision History（整个部分）
- References（仅关于如何引用 EMBOSS 的说明）。

以下部分的包含文件是通过运行 QA 测试生成的，这就是为什么（通常）应在记录应用程序之前编写 QA 测试：

- Usage（整个部分）
- Input Files（仅输入文件示例）
- Output Files（仅输出文件示例）。

应用程序模板中的应用程序名称和索引术语也已正确设置。完成所有操作后，HTML 应用程序模板将创建在：

```
embassy/myemboss/emboss_doc/html/myprogram.html
```

要完成应用程序模板 myprogram.html，请按以下方式添加文档文本：

- 1. 编写 "Function" 部分。
- 2. 在 "Input Files" 部分编写输入文件描述（可选）。
- 3. 在 "Data Files" 部分编写数据文件描述（可选）。
- 4. 在 "Output Files" 部分编写输出文件描述（可选）。
- 5. 在 "Description" 部分编写应用程序描述。
- 6. 在 "Algorithm" 部分编写算法描述。
- 7. 在 "Notes" 部分编写外围文档。
- 8. 在 "Warnings" 部分编写使用建议、已知错误等。
- 9. 在 "Diagnostics" 部分编写警告和错误消息。
- 10. 在 "References" 部分编写参考文献（如适用）。

模板中已包含足够的注释，供你了解如何填写。

autodoc.pl 还生成纯文本格式的文档（包含所有包含文件中的文本），用于手册页，并在运行以下命令时显示：

```
application_name -help
```

完成模板并保存后，文档（HTML 和纯文本格式，以及包含文件）即可提交给 EMBOSS 作者以供在线发布。引用新文档的其他在线文件（例如应用程序索引 http://emboss.open-bio.org/rel/dev/apps/）将自动更新。

## 8.2.3.1 不使用 myemboss 时记录应用程序

记录 EMBOSS 应用程序时，请在以下目录中工作：

```
doc/programs/master/emboss/apps/
```

从 autodoc.pl 命令行中省略 -embassy=myemboss 限定符：

```
autodoc.pl ApplicationName
```

最终文档将写入：

```
doc/programs/html/myprogram.html
```

## 8.2.3.2 示例

以下示例适用于 seqret。所有路径均相对于文档目录，例如 /home/auser/emboss/emboss/doc/。

带有包含指令的应用程序模板文件为：

```
./programs/master/emboss/apps/seqret.html
```

## autodoc.pl 生成的文件

包含文件如下。所有文件均写入 /programs/master/inc/：

| 文件 | 描述 |
|---|---|
| ../secret.itable | 通过运行 acdtable 生成 |
| ../secret.ione | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.ihelp | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.itable | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.isee | 由 autodoc.pl 使用 ACD 文件中的组从 seealso 生成 |
| ../secret.usage | 从 QA 测试生成（使用 UsageExampleTemplate.xml） |
| ../secret.input | 从 QA 测试生成（使用 InputFilesTemplate.xml） |
| ../secret.output | 从 QA 测试生成（使用 OutputFilesTemplate.xml） |
| ../secret.comment | 由 autodoc.pl 生成，供手动编辑 |
| ../secret.history | 由 autodoc.pl 生成，供手动编辑 |

autodoc.pl 生成用于在线的最终 HTML 文件，包含所有数据：

```
./programs/html/secret.html
```

autodoc.pl 还编写一个纯文本文档文件，包含与完成的应用程序模板中完全相同的文档，但包含所有包含的文本：

```
./programs/text/secret.txt
```

## 8.3 EMBASSY 包文档

### 8.3.1 EMBASSY 包文档的章节

EMBASSY 包文档中的章节在下表中描述。

### 8.3.2 EMBASSY 包文档过程

生成 EMBASSY 包文档的过程与应用程序类似。手动编写的组件与自动生成的文本相结合。该过程再次涉及运行 autodoc.pl 脚本，该脚本生成一个部分完成的包模板，你需要手动完成它。

要记录一个新包，首先确保你有一组最新的已编译程序。要生成文档，请对包运行 autodoc.pl：

```
autodoc.pl PackageName
```





| Section | Description | Generation |
|---|---|---|
| 名称 | 包名称、简短描述和版本号。 | 从应用程序 C 源代码和 ACD 文件自动生成。 |
| 内容 | 文档中各部分链接。 | 自动生成。 |
| 应用程序列表 | 包中应用程序的名称、简短描述和完整文档链接。 | 从应用程序 ACD 文件自动生成。 |
| 功能 | 使用受控词汇中的术语，对包及其主要输入、输出和功能进行简洁、正式的描述。 | 由应用程序作者编写。 |
| 描述 | 适合生物学最终用户的包描述。 | 由应用程序作者编写。 |
| 安装说明 | 包的安装说明。 | 常规说明自动生成。特定于包的信息（如所需文件或版本）应由应用程序作者编写。 |
| 附注 | 使用说明等外围文档。 | 由应用程序作者编写。 |
| 警告 | 谨慎的使用建议、已知错误等。 | 由应用程序作者编写。 |
| 作者 | 作者联系信息。 | 从源代码自动生成。 |
| 修订历史 | 包修订历史，包括上次修订日期、修订作者姓名和关于修订的简要说明。 | 由应用程序作者编写。 |
| 参考文献 | 文献参考和如何引用应用程序的说明。 | 如何引用 EMBOSS 的说明自动生成。否则，由应用程序作者编写。 |

以下示例假设您已创建名为 mypackage 的新 EMBASSY 包。要为该包编写文档：

1. 切换到文档目录：

```
cd embassy/mypackage/emboss_doc/master
```

2. 将应用程序模板复制到同一目录下名为 mypackage.html 的文件中。示例模板在 EMBASSY 包 myemboss 中提供。编辑模板文件时，将 MYEMBOSS 改为您的包名：

```
cp template.html.save mypackage.html
```

3. 运行 autodoc.pl：

```
autodoc.pl -embassy=mypackage
```

4. 在指定位置（见下文）编写文档文本以完成 mypackage.html。

该脚本将生成一个模板文档文件（供您填写），包含包含指令，以及以下部分的包含文件：

- Name（整个部分）
- List of Applications（整个部分）
- Authors（整个部分）
- Revision History（整个部分）
- Installation Notes（仅常规说明）
- References（仅关于如何引用 EMBOSS 的说明）

模板中的 EMBASSY 包名和索引术语也已正确设置。HTML 应用程序模板创建在：

```
embassy/mypackage/emboss_doc/html/mypackage.html
```

要完成模板 mypackage.html，请在指定位置添加文本：

1. 编写“Function”部分。
2. 在“Description”部分中编写包的描述。
3. 在“Installation Notes”部分中编写包特定的安装信息（可选）。
4. 在“Notes”部分中编写外围文档。
5. 在“Warnings”部分中编写使用建议、已知错误等。
6. 在“Notes”部分中编写外围文档。
7. 在“References”部分中编写参考文献（如适用）。

同样，模板已添加注释，因此清楚在哪里添加文本。

autodoc.pl 还会生成纯文本格式的文档（包含所有包含的文本），该文档包含在包的 README 文件中。

完成模板并保存后，文档（HTML 和纯文本格式，以及包含文件）即可提交给 EMBOSS 作者以供在线发布。引用新包的其他文件，例如 EMBASSY 包的主表（http://emboss.open-bio.org/rel/dev/apps/EMBASSYPackagesTable.html），将自动更新。

# 完整的应用程序：secret

secret 是第一个 EMBOSS 应用程序，其名称部分源于其功能（可用于从数据库中检索序列），部分源于应用程序源代码掩盖了底层库代码的复杂性。简单来说，该程序读取一个序列并再次写出，但有许多选项使其功能非常强大。其命令行界面将提示输入一个或多个任意类型序列的输入流，并提示输出流。secret 读取和写入 EMBOSS 支持的任何序列格式，并使用统一序列地址（USA）（参见 EMBOSS 用户指南）来指定序列数据的位置和格式。

下面公开了 secret 的 C 源代码、ACD 文件、质量保证测试和文档，以让您了解功能齐全的 EMBOSS 应用程序的所有基本组件。

### 9.1 ACD 文件（secret.acd）

ACD 文件指定输入序列流（sequence）和输出序列流（outseq）。

```
application: secret [
  documentation: "Reads and writes (returns) sequences"
  groups: "Edit"
]

section: input [
  information: "Input section"
  type: "page"
]

boolean: feature [
  information: "Use feature information"
]

seqall: sequence [
  parameter: "Y"
  type: "gapany"
  features: "$(feature)"
]
endsection: input

section: advanced [
  information: "Advanced section"
  type: "page"
]
boolean: firstonly [
    information: "Read one sequence and stop"
]
endsection: advanced
section: output [
    information: "Output section"
    type: "page"
]
seqoutall: outseq [
    parameter: "Y"
    features: "$(feature)"
]
endsection: output
```

sequence 和 outseq 的数据定义指定为参数，这意味着可以在命令行上为它们提供值（即 USA），而无需指定标志（参数名，即 -sequence 或 -outseq）。但是，仍然可以提供标志。

因此，seqret 可以这样调用：

```
seqret InputSequenceUSA OutputSequenceUSA
```

在这种情况下，参数必须按所示顺序排列（InputSequenceUSA 和 OutputSequenceUSA 分别是输入和输出序列的 USA）。

它也可以这样调用：

```
seqret -sequence InputSequenceUSA -outseq OutputSequenceUSA
```

在这种情况下，参数可以按任何顺序给出，因此这也是可以接受的：

```
seqret -outseq OutputSequenceUSA -sequence InputSequenceUSA
```

### 9.1.1 应用程序定义

应用程序定义在文件顶部给出：

```
application: seqret
[
    documentation: "Reads and writes (returns) sequences"
    groups: "Edit"
]
```

### 9.1 ACD 文件（SEQRET.ACD）

应用程序名称（secret）在 application: 标记后给出。应用程序功能的简洁描述（"Reads and writes (returns) sequences"）在 documentation: 属性后给出，运行程序时将打印到屏幕上。使用 -help 限定符运行程序时也会显示此文本。wossname 实用程序也会搜索此文本，在搜索关键字后显示应用程序。

groups: 属性的值为 "Edit"，表示 seqret 属于 "Edit" 组，即序列编辑应用程序。所有 EMBOSS 和 EMBASSY 应用程序都被分组到相关功能中（第 4.2.4.1 节，‘应用程序组名称文件（groups.standard）’）。

应用程序定义中还可以给出其他属性（参见第 4.2 节，‘应用程序定义’）。

### 9.1.2 ACD 文件部分

ACD 文件组织为 Input、Advanced 和 Output 部分，这些部分包含在文本标记中（section: input、endsection: input 等）：

```
section: input
[
   information: "Input section"
   type: "page"
]
.
.
.
endsection: input
```

显然，Input 和 Output 部分分别用于应用程序的输入和输出。Advanced 用于命令行永远不会提示的应用程序选项（本例中没有）。在实践中，ACD 文件中可能出现其他类型的应用程序参数和相应部分（参见第 4.1 节，‘ACD 文件开发简介’）。

### 9.1.3 数据定义

这些部分包含定义应用程序输入和输出数据及其他参数的 ACD 数据定义。从概念上讲，数据定义可视为两种基本类型：基本输入和输出文件，或控制应用程序的其他类型。例如，sequence 和 outseq 是输入和输出文件的数据定义：

```
seqall: sequence
[
   parameter: "Y"
   type: "gapany"
   features: "$(feature)"
]
.
.
```





seqoutall: outseq
[
    parameter: "Y"
    features: "$(feature)"
]

相比之下，boolean: feature 是一个控制定义，如果由用户设置，将导致 **seqret** 读取输入文件中的序列特征信息（如果可用）。

boolean: firstonly 是另一个控制定义，如果设置，将导致只读取单个序列：

```
boolean: feature
[
    information: "Use feature information"
]
boolean: firstonly
[
    information: "Read one sequence and stop"
]
```

在实践中，有多种不同的 ACD 数据类型（第 A.2 节，“数据类型”）可用。对这些数据定义的编程在第 5.5 节“使用对象编程”中有更详细的介绍。

## 9.1.4 属性

每个 ACD 定义都有属性，属性是名称：值对。属性有两种基本类型。_全局属性_ 可用于所有数据类型，而 _特定于数据类型的属性_ 可用于单个或一组相关数据类型。

考虑 `feature` 和 `sequence` 的定义：

```
boolean: feature
[
    information: "Use feature information"
]
seqall: sequence
[
    parameter: "Y"
    type: "gapany"
    features: "$(feature)"
]
```

`parameter:` 和 `information:` 是全局属性，而 `type:` 和 `features:` 是特定于数据类型的属性。

`parameter:` "Y" 将数据定义定义为 _参数_，而不是某种 _限定符_。如上所述，参数的值可以在命令行上带或不带标志（参数名称）给出。应用程序需要所有参数，如果命令行上未给出值，将提示输入值。

布尔定义未给出 parameter: "Y"，这意味着，在没有 standard: "Y" 或 additional: "Y" 属性的情况下，它们将默认为高级限定符。高级限定符永远不会提示输入。如果已定义 standard: "Y" 或 additional: "Y"，则数据定义将是标准或附加限定符。有关限定符和参数行为的更多信息可用（第 4.1 节，“ACD 文件开发简介”）。

information: 为数据定义提供非常简洁的描述。该文本用于 Web 表单和其他 GUI。它也是用于在命令行上提示用户输入值的文本。您会注意到，序列输入和输出未定义 information:。EMBOSS 为这些数据类型提供默认提示。所有 boolean: 数据类型的默认值均为 False，这意味着无需在 ACD 文件中显式定义默认值。

type: 属性特定于序列数据类型。type: "gapany" 表示输入序列可以是任何类型，并可能包含间隙字符。在实践中，支持多种不同的序列类型（第 A.7 节，“序列类型”）。

features: 属性也是特定于序列的。属性定义看起来有点奇怪：

```
features: "$(feature)"
```

$ 语法的意思是“检索……的值”，在此情况下是“检索 feature ACD 定义的值”，因此 outseq 的 features: 属性将设置为该值。换句话说，如果用户通过在命令行上给出它（例如 secret -feature）打开了 feature 高级限定符，则输入序列将包含特征。虽然严格来说不需要 features: "$(feature)"（毕竟信息在 boolean: feature 中已指定），但这使应用程序源代码更加整洁。

除了全局属性和特定于数据类型的属性之外，ACD 文件中还可能出现另外两种属性。计算属性在处理 ACD 文件并读取应用程序输入文件后接收值。最后，还有特定于数据类型的命令行限定符，它们为单个或一组 ACD 数据类型定义，并可以作为属性硬编码在 ACD 文件中。参见第 A.4 节（“全局属性”）、第 A.5 节（“特定于数据类型的属性”）和第 A.6 节（“计算属性”）。

## 9.2 C 源代码 (secret.c)

应用程序 C 源代码（见下文）非常简单。其基本功能包括：

- 声明用于保存来自 ACD 文件的值的变量（AjP* 类型声明）
- 处理 ACD 文件和命令行（embInit）
- 将值（输入和输出序列流）从 ACD 文件读入内存（ajAcdGet 函数系列）
- 遍历输入序列并将序列加载到内存中（ajSeqallNext）
- 写出序列（ajSeqoutWriteSeq）
- 关闭输出文件
- 干净退出（embExit）

源代码如下：

/*@source secret application
**
** Return a sequence
**
** @author Copyright (C) Peter Rice
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
******************************************************************************/

#include "emboss.h"

/* @prog secret **************************************************************
**
** Reads and writes (returns) sequences
**
******************************************************************************/

int main(int argc, char **argv)
{
    AjPSeqall seqall;
    AjPSeqout seqout;
    AjPSeq seq = NULL;
    AjBool firstonly;

    embInit("secret", argc, argv);

    seqout = ajAcdGetSeqoutall("outseq");
    seqall = ajAcdGetSeqall("sequence");
    firstonly = ajAcdGetBoolean("firstonly");

    while(ajSeqallNext(seqall, &seq))
    {
        ajSeqoutWriteSeq(seqout, seq);
        if(firstonly)
            break;
    }

    ajSeqoutClose(seqout);

    embExit();

    return 0;
}
```

### 9.2.1 变量声明

`main()` 中的第一个代码块声明用于保存来自 ACD 文件的值的变量：

```c
AjPSeqall seqall=NULL;
AjPSeqout seqout=NULL;
AjPSeq seq = NULL;
AjBool firstonly;
```

以 `AjP` 开头的变量都是指向 EMBOSS 对象（相应类型的 C 数据结构）的 C 指针。这些包括 `AjPSeqall`、`AjPSeqout` 和 `AjPSeq`。许多 EMBOSS 对象（包括复杂生物类型和其他类型）定义在 AJAX 和 NUCLEUS 编程库中。相比之下，`AjBool` 是 EMBOSS 用于简单布尔变量的数据类型。您会注意到指针变量初始化为 `NULL`。在首次定义指针时始终将其初始化为 `NULL` 是良好做法。有关原因的解释以及使用对象编程的详细信息，请参见第 5.3 节“对象（C 数据结构）”。

`AjPSeq` 用于单个序列输入，`AjPSeqall` 用于多个序列输入，`AjPSeqout` 用于单个序列输出。对于 **seqret** 应用程序，`AjPSeqall seqall` 用于输入序列流，`AjPSeq seq` 用于保存该流中单个序列的数据，`AjPSeqout seqout` 用于输出序列流。`AjBool firstonly` 用于保存来自 ACD 文件的 `firstonly` 控制属性的值。

您会注意到，`feature` 数据定义不需要变量。此选项的值在输入序列流上设置，在 ACD 文件本身中，通过 ACD 代码 `features: "$(feature)"`。换句话说，是否将特征信息与序列一起包含是在 ACD 文件中设置并存储在 `seqall` 对象中的，因此 C 代码中不需要为它添加其他变量。

### 9.2.2 ACD 文件和命令行处理

以下代码：

```c
embInit("secret", argc, argv);
```

用于处理 ACD 文件和命令行。它处理所有用户输入处理，这就是为什么它首先被调用。`embInit` 读取本地数据库定义，找到要使用的正确 ACD 文件（第一个参数是 "secret"，因此它在 ACD 目录中查找 `secret.acd`），读取 ACD 文件，并使用 `main` 中的 `argc` 和 `argv` 处理命令行。

当 `embInit` 返回时，输入序列流（`sequence`）将打开以供读取，第一个序列将读入内存，布尔变量 `feature` 和 `firstonly` 将接收值（可能是默认值），并且将为 `outseq` 打开输出文件。为这些对象分配内存并可供程序使用。

`embInit` 处理提示用户输入未在命令行上输入的值，包括重新提示用户输入超出范围的值等功能。





## 9.2.3 从 ACD 文件中检索值

要检索这些数据项的 C 指针，使用以下代码：

```
seqout = ajAcdGetSeqoutall("outseq");
seqall = ajAcdGetSeqall("sequence");
```

同样，要检索简单数据类型变量 firstonly 的值：

```
firstonly = ajAcdGetBoolean("firstonly");
```

可以看到，ajAcdGet* 函数的参数是要检索的 ACD 定义的名称。

## 9.2.4 序列处理

要遍历输入序列并将序列加载到内存中，使用以下代码：

```
while(ajSeqallNext(seqall, &seq))
{
    ajSeqoutWriteSeq(seqout, seq);
    if(firstonly)
        break;
}
```

ajSeqallNext 在循环中被调用，以便从输入流中依次检索连续序列。第二个参数 (&seq) 将指针设置为流中的当前序列。ajSeqoutWriteSeq 用于将此序列写入输出流 seqout。如果 firstonly 已设置，循环将在第一个序列后终止。

## 9.2.5 干净退出

通过调用 ajSeqoutClose() 关闭输出流。应用程序在调用 embExit() 后干净终止，然后向操作系统返回 0：

```
ajSeqoutClose(seqout);
embExit();
return 0;
}
```

## 9.3 内置功能

seqret 具有丰富的内置功能：

- 它可以读写 EMBOSS 支持的任何序列格式（参见 EMBOSS 用户指南），其中包括所有常见格式。
- 它使用强大的 USA 语法（参见 EMBOSS 用户指南）来指定序列数据的位置和格式。
- seqret 可以从数据库、文件、listfile（USA 文件）、命令行或其他程序的输出中读取一个或多个序列，然后将其写入文件、数据库或 stdout（可重定向到另一个程序）。因此，它对于从数据库中提取序列并显示它们很有用。
- seqret 支持许多未在 ACD 文件中列出的命令行选项。这些包括全局限定符和特定于数据类型的限定符。还有许多其他限定符可用，可以组合使用，在无需任何额外编程的情况下提供更大的灵活性。
- 它支持全局限定符（参见 EMBOSS 用户指南），这些限定符可用于所有 EMBOSS 应用程序。
- 它支持各种特定于数据类型的限定符（参见 EMBOSS 用户指南）；在此情况下，序列数据类型包括来自 ACD 文件的 seqall：序列输入和 seqoutall：outseq 输出定义。

例如，您可以使用 -sformat FormatName（输入）和 -osformat FormatName（输出）选项来指定输入和输出格式。如果不指定输入格式，它将尝试所有已知格式，直到成功为止；如果不指定输出格式，则默认使用 FASTA。seqret 对于重新格式化序列很有用，也许是为输入到另一个程序做准备。

-sbegin 和 -send 选项指定输入序列中子序列的起始和结束位置。此片段将写入输出文件，因此 seqret 对于简单提取序列区域很有用。-sreverse 开关将使用核酸序列的反向互补。

正如您从 seqret.c 中所见，无需应用程序代码即可受益于此内置功能。此外，随着 EMBOSS 中添加新的序列格式，seqret 将自动能够使用它们；无需更改应用程序代码。那么，很明显，此内置功能为您作为软件开发人员节省了大量时间。

## 9.3.1 示例用法

下面展示了说明 seqret 许多用例中几个示例。

这里 seqret 正在用于从 SwissProt 数据库中检索条目 5HT1D_FUGRU 并以 FASTA 格式写出该条目：

```
% seqret
Reads and writes (returns) sequences
Input (gapped) sequence(s) : swissprot:5HT1D_FUGRU
Output sequence [5ht1d_fugru.fasta] :
% more 5ht1d_fugru.fasta
>5HT1D_FUGRU P79748 5-hydroxytryptamine receptor 1D (5-HT-1D)
MELDNNSLDYFSSNFTDIPSNTTVAHWTEATLLGLQISVSVVLAIVTLATMLSNAFVIAT
IFLTRKLHTPANFLIGSLAVTDMLVSILVMPISIVYTVSKTWSLGQIVCDIWLS SDITFC
TASILHLCVIALDRYWAITDALEYSKRRTMRRAAVMVAVVWVISISISMPPLFWRQAKAH
EELKECMVNTDQISYTLYSTFGA FYVPTVLLIILYGRIYVAARSRIFKTPYSYGKRFTTA
QLIQTSAGSSLCSLNSASNQEAHLHSGAGGEGGGS PLFVNSVKVKLADNVLERKR LCAAR
```

使用 USA（参见 EMBOSS 用户指南）机制在命令行上指定相同的输入和输出序列，也可以实现同样的效果：

```
seqret swissprot:5HT1D_FUGRU fasta:5ht1d_fugru.fasta
```

此示例从输入流中检索所有序列。这不是一件非常明智的事，但它说明 USA 机制支持序列的通配符指定：

```
% seqret swissprot:"*"
Reads and writes (returns) sequences
Output sequence [ubr5_rat.fasta]: all.fasta
% more all.fasta
>UBR5_RAT Q62671 E3 ubiquitin-protein ligase UBR5 (6.3.2.-)
MMSARGDFLNYALSLMRSHNDEHSDVLPVLDVCSLKHVAYVFQALIYWIKAMNQQTTLDT
PQLERKRTRELLELGIDNEDSEHENDDDTSQSATLNDKDDESLPAETGQNHPFFRRSD SM
TFLGCIPPNPFEVPLAEAIPLADQPHLLQPNARKEDLFGRPSQGLYSSSAGSGKCLVEVT
MDRNCLEVLPTEKMSYAANLKNVMNMQNRQKKAGEDQSMLAEEADSSKPGPSAHDVAAQLK
SSLLLAEIGLTESEGPLTSFRPQCSFMGMVISHMLLGRWRLSLELFGRVFMEDVGAEPG
SILTELGGFEVKESKFREMEKLRNQQSRDLSLEVDRDRDLLIQQTMRQILNNHFGRRCAT
TPMAVHRVKVTFKDEPEGESGVARSFYTAIAQAFLSNEKLPLNLDCIQNANKGTHTSLMQR
LRNRGERDREREREREMRRSGLRAGSRRDRDRDFRRQLSIDTRPFPASEGNPSDDP DP
LPAHRQALGERLYPRVQAMQPAFASKITGMLELSPAQLLLLLLASEDSLRARVEEAMELI
VAHGRENGADSILDLGLLDSSEKVQENRKHGGSSRSVVDMDLDDTDGDDDNAPLFYQPGK
RGFYTPRPGKNTEARLNCFRNIGRILGLC LLQNELCPITLNRHVIKVLLGRKVNWHDFAF
FDPVMYESLRQLILASQSSDADAVFSAMDLAFAVDLCKEEGGGQVELIPNGVNI PVTPQN
VYEYVRKYAEHRMLVVAEQPLHAMRKGLLDVLPKNSLEDLTAEDFR LLVNGCGEVNVQML
ISFTSFNDESGENAEKLLQFKRWFSIVERMSMTERQDLVYFWTSSPSLPASEEGFQPMP
SITIRPPDDQHLPTANT CISRLYVPLYSSKQILKQLLLLAIKTKNFGFV
>5HT1D_FUGRU P79748 5-hydroxytryptamine receptor 1D (5-HT-1D) (5HT1D)
MELDNNSLDYFSSNFTDIPSNTTVAHWTEATLLGIQISVSVVLAIVTLATMLSNAFVIAT
IFLTRKLHTPANFLIGSLAVTDM LVSILVMPISIVYTVSKTWSLGQIVCDIWLSSDITFC
TASILHLCVIALDRYWAITDALEYSKRRTMRRAAVMVAVVWVISISISMPP LFWQAKAH
EELKECMVNTDQISYTLYSTFGAFYVPTVLLIILYGRIYVAARSRIFKTPSYSGKRFTTA
QLIQTSAGSLSLSLNSASNQEAHLHSGAGGEGGGSPLFVNSVKVKLADNVLERKRLCAAR
ERKATKTLGIILGAFIICWLPFFVVTLVWAICKECSFDPLLFDVFTWLGYLNSLINPVIY
TVF NDEFKQAFQKLIKFRR
>ACTB1_FUGRU P68142 Actin, cytoplasmic 1 (Beta-actin A)
MEDEIAALVVDNGSGMCKAGFAGDDAPRAVFPSIVGRPRHQGVMVGMGQKDSYVGDEAQS
KRGI LT LKYPIEHGIVTNWDDMEKIWHHTFYNELRVAPEEHPVLLTEAPLNPKANREKMT
QIMFETFNTAMYVAIQAVLSLYASGRTTGI VMDSGGDVTH TVPIYEGYALPHAILRLDL
... data omitted
```

以下示例说明了 -firstonly 选项的用法。这是一个高级选项，因此永远不会被提示；每当使用时，都必须在命令行上指定：

```
% seqret swissprot:"" -outseq all.fasta -firstonly
Reads and writes (returns) sequences
% more all.fasta
>UBR5_RAT Q62671 E3 ubiquitin-protein ligase UBR5 (6.3.2.-)
MMSARGDFLNYALSLMRSHNDEHSDVLPVLDVCSLKHVAYVFQALIYWIKAMNQQTTLDT
PQLERKRTRELLELGIDNEDSEHENDDDTSQSATLNDKDDESLPAETGQNHPFFRRSD SM
TFLGCIPPNPFEVPLAEAIPLADQPHLLQPNARKEDLFGRPSQGLYSSSAGSGKCLVEVT
MDRNCLEVLPTKMSYAANLKNVMNMQNRQKKAGEDQSMLAEEADSSKPGPSAHVDVAAQLK
SSILAAEIGLTESKGPLLTSFRPQCSFMGMVTSHDMLLGRWRLSLELFGRVFMEDVGAEPG
SILTEIGGFEVEKSKEFREMEKLRNQQSRDL SLEVDRDRDLLIQQTMRQLNNHFGRRCAT
TPMAVHRVKVTFKDEPEGSGSVARSFYTAIAQAFLSNEKLPNLDCIQNANKGTHTSLMQR
LRNRGERDREREREREMRRSSGLRAGSRRDDRDFRQRLSIDTRPFRPASEGNPSDDPDP
LPAHRQALGERLYPRVQAMQPAFASKITGMLELSLPAQLLLLLLASEDSLRARVEEAMELI
VAHGRENGADSILDLGLLDSSEKVQENRKRHGSSRSVVDMDLDDTDDGDDNAPLFYQPGK
RGFYTPRPGKNTEARLNCFRNIGRILGLCLLQNELCPITLNRHVIKVLLGRKVNVWHDFAF
FDPVMYESLRQLILASQSSDADAVFSAMDLAFAVDLCKEEGGGQVELIPNGVNIPVTPQN
VYEYVRKYAEHRMLVVAEQPLHAMRKGLLDVLPKNSLEDLTAEDFRLLVNCGEVNVQML
ISFTSFNDDESGENAEKLLQFKRWFWSIVERMSMTERQDLVYFWTS SPSLPASEEGFQMP
```

这里，通过使用 -help 全局限定符生成使用信息：

```
% seqret -help
Standard (Mandatory) qualifiers:
[-sequence] seqall (Gapped) sequence(s) filename and optional
format, or reference (input USA)
[-outseq] seqoutall Sequence set(s) filename and optional format
(output USA)
Additional (Optional) qualifiers: (none)
Advanced (Unprompted) qualifiers:
-feature boolean Use feature information
-firstonly boolean Read one sequence and stop
General qualifiers:
-help boolean Report command line options. More
information on associated and general
qualifiers can be found with -help -verbose
```

在以下示例中，特定于序列的命令行选项 -sbegin 和 -send 用于指定序列区域：

```
% seqret swissprot:5HT1D_FUGRU -sbegin 10 -send 20 fasta:5ht1d_fugru.fasta
Reads and writes (returns) sequences
% more 5ht1d_fugru.fasta
>5HT1D_FUGRU P79748 5-HYDROXYTRYPTAMINE 1D RECEPTOR (5-HT-1D) (SEROTONIN RECEPTOR).
YFSSNFTDIPS
```

## 9.4 文档 (seqret.html)

最终用户文档按部分组织，以便于导航。您可以在在线应用程序文档中亲自查看：

http://emboss.open-bio.org/rel/dev/apps/seqret.html

有关更多信息，请参见第 8 章，应用程序文档标准。





## 9.5 质量保证测试

seqret 的质量保证测试定义在文件中：

```
.../emboss/emboss/test/qatest.dat
```

该应用程序的测试数据位于 /test 目录下，由输入文件、应用程序参数和相应的输出文件组成。

检查该文件可知，为该应用程序定义了许多测试，在各种输入条件下对其进行测试，以尽可能增强其鲁棒性。这些测试会频繁执行，以确保应用程序按宣传的方式工作，并且不会因（例如）库代码的最近更改而损坏。

质量保证测试（包括如何在 qatest.dat 中编写条目）在其他地方有详细介绍（第 7 章，质量保证）。

### Test 1

此测试从数据库中提取一个条目并将其写入文件：

```
ID seqret-ex1
UC Extract an entry from a database and write it to a file:
AP seqret
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_1.dat seqret-ex1
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 2

在屏幕上显示序列内容：

```
ID seqret-ex2
UC Display the contents of the sequence on the screen:
AP seqret
IN embl:x65923
IN stdout
FI stdout
FP /X65923/
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_2.dat seqret-ex2
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 3

使用限定词 -osformat 将结果以 GCG 格式写入：

```
ID seqret-ex3
UC Write the result in GCG format by using the qualifier '-osformat'.
AP seqret
CL -osf gcg
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_3.dat seqret-ex3
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 4

在命令行的输出 USA 中指定格式，将结果以 GCG 格式写入：

```
ID seqret-ex4
UC Write the result in GCG format by specifying the format
UC in the output USA on the command line.
AP seqret
CL -outseq gcg::x65923.gcg
IN embl:x65923
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_4.dat seqret-ex4
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 5

在提示符处的输出 USA 中指定格式，将结果以 GCG 格式写入：

```
ID seqret-ex5
UC Write the result in GCG format by specifying the format
UC in the output USA at the prompt.
AP seqret
IN embl:x65923
IN gcg::x65923.gcg
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_5.dat seqret-ex5
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 6

写入序列的反向互补：

```
ID seqret-ex6
UC Write the reverse-complement of a sequence:
AP seqret
CL -srev
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_6.dat seqret-ex6
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 7

提取位置从 5 开始到 25 结束之间的碱基：

```
ID seqret-ex7
UC Extract the bases between the positions starting at 5 and ending at 25:
AP seqret
CL -sbegin 5 -send 25
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_7.dat seqret-ex7
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 8

提取位置从 5 开始到序列结束前 5 个碱基处之间的碱基：

```
ID seqret-ex8
UC Extract the bases between the positions starting at 5
UC and ending at 5 bases before the end of the sequence:
AP seqret
CL -sbegin 5 -send -5
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_8.dat seqret-ex8
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 9

读取 embl 数据库中所有以 h 开头的条目并将其写入文件：

```
ID seqret-ex9
UC Read all entries in the database 'embl' that start with 'h'
UC and write them to a file:
AP seqret
IN embl:h*
IN hall.seq
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI hall.seq
FP /H45989/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_9.dat seqret-ex9
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 10

此测试读取 embl 数据库中所有以 ab 开头的条目并将其写入文件。在此示例中，规范完全在命令行上完成。为了防止 UNIX 被 * 字符搞混，其前有一个反斜杠（\）：

```
ID seqret-ex10
UC Read all entries in the database 'embl' that start with 'ab'
UC and write them to a file.
UC In this example the specification is all done in the command line
UC and to stop Unix getting confused by the '*' character,
UC it has to have a backslash ('\\') before it:
AP seqret
CL 'embl:ab*' aball.seq
FI stderr
FC = 1
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI aball.seq
FP /^>AB000095/
FP 4 /^>/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_10.dat seqret-ex10
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 11

seqret 默认不读取特征，因为这会带来略微更快的性能。但是，如果您希望随序列一起读取特征并将其写出，则使用 -feature 将更改默认行为。请注意，输出文件使用 EMBL 格式。默认的 FASTA 格式将以 GFF 格式报告特征（文件 seqname.gff，其中 seqname 是输入序列的名称）：

```
ID seqret-ex11
UC seqret does not read in features by default because this results in
UC slightly faster performance. If however you wish to read in features
UC with your sequence and write them out on output, using '-feature' will
UC change the default behaviour to use any features present in the sequence.
UC N.B. use embl format for the output file as the default format 'fasta'
UC reports the features in gff (file "<seqname>.gff")
AP seqret
CL -feature
IN embl:x65923
IN embl::x65923.embl
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.embl
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_11.dat seqret-ex11
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

## 10.1 将应用程序纳入 EMBOSS 的好处

将第三方应用程序纳入 EMBOSS 有很多充分的理由，下面列举了其中几点。

- **分发** 显然，触达尽可能多的用户是可取的。EMBOSS 拥有数千名用户，许多网站会定期下载最新版本，因此任何纳入的软件都将被广泛分发。

- **培训成本** 纳入的软件的使用方式与所有其他 EMBOSS 应用程序完全相同。熟悉 EMBOSS 的人将能够使用任何已移植或封装的应用程序。当然，除了学习应用程序实现的特定方法之外，不需要额外的培训要求。无论应用程序是否在 EMBOSS 中，这都是一个要求。

- **支持成本** 纳入的应用程序将通过邮件列表获得 EMBOSS 提供的基本级别支持。支持级别取决于具体情况。对于已完全移植并理解将被 EMBOSS 采纳的应用程序，将获得全面支持。至少，用户对任何电子邮件查询都会得到回复，并被转发到可以获得更多帮助的地方。在应用程序的原作者已离开当前维护该应用程序的机构的情况下，这尤其有价值。

- **维护成本** 维护成本可能会有所节省。这同样取决于集成程度和具体安排。至少，EMBOSS 将调查任何错误并将相应报告转发给原始软件的作者。维护移植或封装以及原始代码会有额外成本，但这远远被收益所抵消。




## Web 服务、工作流和界面

EMBOSS 已被集成到许多图形界面和工作流软件中，例如 SRS、Pipeline Pilot、Taverna、wEMBOSS 和 Jemboss。此外，得益于 SOAPLAB 的持续开发，将 EMBOSS 应用程序部署为 Web 服务相对容易。如果您的软件已被集成，那么在这些环境中设置它几乎没有或没有额外成本。

## 数据库支持

EMBOSS 支持序列、序列特征和序列比对的输入和输出的所有常见格式。还支持许多其他常见数据格式。您集成的任何软件都将能够使用这些格式。此外，当 EMBOSS 更新以支持格式更改或全新格式时，您的软件将自动从这些更改中受益。

## 10.2 包装器和移植

集成第三方应用程序有两种基本方法。您可以为应用程序编写一个“包装器”，也可以对应用程序源代码本身进行移植。包装器仅仅是一个程序，其主要目的是调用另一个程序，后者通常（但不总是）不是 EMBOSS 原生的。相比之下，“移植”是指修改被集成应用程序的源代码，使其适合原生系统（EMBOSS）。

下面概述了包装和移植应用程序的基本方法。过于规定性是没有意义的，因为所需内容很大程度上取决于具体的应用程序。包装和移植应用程序的优缺点进行了总结。所使用的方法、C 源代码和 ACD 文件，以将 HMMER 包集成到 EMBOSS 的经验为例进行了说明。

## 注意

HMMER 包是由 Sean Eddy 编写的一组用于蛋白质序列隐马尔可夫模型分析的工具。版本 2.2.1 被移植到 EMBOSS 中作为 HMMER EMBASSY 包。HMMER 采用 GPL 许可证，因此在修改源代码时无需考虑许可问题。然而，此版本被证明难以维护，因此对于最新版本 v2.3.2，开发了一个 EMBASSY 包（HMMERNEW）的应用程序包装器。

在移植应用程序时，有必要识别从用户读取输入的函数，编写一个定义相同值的 ACD 文件，然后添加代码从 ACD 文件中获取值，而不是像原始程序那样处理它们。

包装应用程序时仍然需要 ACD 文件，通常编写该文件以紧密遵循原始界面。参数命名存在缺点，如您稍后将看到。包装器必须根据用户规范构建适当的命令行。主要困难是确保序列和其他数据处于第三方应用程序所需的格式。在启动底层程序之前，包装器可能需要读取输入并根据需要进行转换。

在这两种情况下，输出文件可以保留原始应用程序生成的任何格式，或者数据可以转换为用户指定的格式。对于移植，这可能涉及修改原始源代码并用对 EMBOSS 库的适当调用替换输出函数。或者，这是开发某些包装器时采用的方法，可以使用临时文件来实现转换。

## 10.3 优缺点

以下是关于在 EMBOSS 下包装和移植应用程序所涉及的各种成本的主观看法：

| 类别 | 包装器 | 移植 |
|---|---|---|
| 开发成本 | 低到中等 | 中到高 |
| 灵活性 | 低到中等 | 高 |
| 局限性 | 中等 | 低 |
| 维护成本 | 低到中等 | 中到高 |
| 支持成本 | 低 | 高 |
| 感知风险 | 低到中等 | 中到高 |

### 10.3.1 开发成本

包装器或移植都或多或少需要编写相同的 ACD 文件。主要困难在于第三方软件通常不如 EMBOSS 灵活，并且要求以特定格式提供输入文件，例如 FASTA 格式的序列。在这种情况下需要做出决定——要么支持 EMBOSS 支持的所有输入数据类型，要么遵循原始程序的限制。

完全支持的输入需要额外的代码来操作临时文件，以将输入数据转换为第三方软件可接受的格式。如果不这样做，则有必要在 ACD 文件级别（如果可能）强制执行任何输入约束，或者记录它们，如果应用程序接收到格式错误的数据则引发异常。在 ACD 中限制序列输入的允许格式将违背 EMBOSS 的整体理念，因此除了添加重新格式化代码或引发异常外，别无选择。

编写包装器的最大优势是您不需要担心第三方源代码本身。包装器代码需要做的一切（在重新格式化输入文件和处理 ACD 文件之后）是构建适当的命令行，调用命令，然后（可能）重新格式化输出（使用临时文件）。构建正确的命令行通常涉及对参数值进行一些比较，因此需要一些辅助代码，但这或多或少是微不足道的。

在移植软件时，必须仔细考虑第三方源代码。通常不需要新的代码文件，但 `main()` 函数需要重写以处理 ACD 文件处理。此外，任何其他读取输入数据的函数（这些函数可能位于不同的文件中）都需要重写，以便它们能够处理通过 ACD 读取的数据。

因此可能需要编辑多个文件。编辑本身可能不会太困难，但可能构成障碍。此外，知道在哪里编辑当然需要了解第三方代码，可能需要相当深入的知识。出于这些原因，移植的初始开发成本往往显著高于包装器。

### 10.3.2 灵活性

正如刚才解释的，移植后的软件在支持输入和输出格式方面提供了最大的灵活性。事实上，支持程度与任何 EMBOSS 应用程序一样完整。相比之下，包装器的灵活性可能较低，但这可以通过涉及使用临时文件的额外编码来缓解。

### 10.3.3 局限性

除了更大的灵活性之外，由于技术原因，移植可能具有更少的固有限制。例如，在 MS Windows 下报告了让一个程序执行另一个程序的困难。进程间通信也可能出现问题。

### 注意

原则上，可以使用对 `system()` 或 `exec()` 的调用来调用第三方应用程序。`system()` 和 `exec()` 都会创建一个新进程。区别在于 `system()` 会生成一个 shell 来调用程序，而 `exec()` 只是调用程序。使用 `system()` 时，shell 可能会妨碍设置进程间通信。

### 10.3.4 维护成本

维护包装器时，您只需要担心界面的更改。向 ACD 文件和相应的包装器代码添加一两个新选项相对容易。但是，在主要版本发布时，许多选项可能已更改，从头开始可能比逐步修改现有内容更简单。无论哪种情况，都必须更新包文档。

对于移植，除了界面更改之外，还必须集成对应用程序代码的任何更改。由于没有方便的自动机制来做到这一点，例如使用共同的 CVS 存储库，因此必须要么在代码上使用 `diff` 来检测更改，要么从头开始，将移植中的 EMBOSS 特定代码添加到新版本的代码中。后者可能是更简单、更安全的选择。如果所有 EMBOSS 特定代码的插入都有良好文档，则这更容易。尽管如此，可能不明显应该在哪里进行更改，即使代码有良好文档，也需要代码检查。出于这些原因，移植软件更容易出错。

### 10.3.5 支持成本

支持包装器的成本远低于移植。这是因为您没有编写第三方应用程序，只是编写了一个包装器。因此您可以合理地


将任何查询转发给原作者，前提是您确定错误不是由包装器代码引起的。在移植的情况下，您已修改了原始源代码，因此可以合理地期望您为其提供支持。

### 10.3.6 认知风险

“认知风险”是主观的，但归根结底取决于最终用户是否足够信任您的软件而愿意使用它。不可避免地，移植的软件会受到一些怀疑，因为除了原作者之外的其他人修改了代码，无论他们是否实际上修复了错误或以其他方式改进了它。因此，如果用户谨慎行事并试图避免结果出现任何差异的可能性，移植版本可能会被忽视。他们也可能坚持使用原版，尽管有瑕疵，仅仅因为那是他们熟悉并过去使用过的东西。相比之下，使用包装器时认知风险较低，因为人们理解包装器只是调用被包装的软件。

### 10.3.7 总结

是否应该移植或包装软件取决于具体情况。通常，优先选择包装器应用程序，因为它们保持了原始代码与EMBOSS代码之间的分离，并且更易于开发、维护和支持。但是，如果您是原始代码的作者，或者将EMBOSS视为访问软件的主要入口，那么移植应用程序可能更可取。

## 10.4 如何包装第三方应用程序

下面描述了包装HMMER软件包所采取的步骤。不可能提供完全通用的指南，因为要求取决于被包装的软件。尽管如此，您可能采取的所有基本步骤都在此处说明。

- 1. 规划与设计
- 2. ACD文件开发
- 3. C源代码开发
- 4. 质量保证测试
- 5. 文档
- 6. 集成。

### 10.4.1 规划与设计

采取的步骤如下：

- 1. 下载源代码和文档
- 2. 阅读文档
- 3. 决定在EMBOSS版本中保留哪些选项
- 4. 决定是否需要新参数，例如用于应用程序输出（通常输出到stdout）。

### 10.4.1.1 文档

HMMER包含一份出色的*用户指南*。有必要阅读简介，学习教程，然后依次阅读每个应用程序的手册页面。并非所有应用程序和软件包都记录得同样详尽！熟悉整个软件包至关重要，特别是要识别所有应用程序的所有可能参数及其交互。在获得这些信息之前，不应开始编码。

### 10.4.1.2 应用程序选项

第一个设计步骤是决定在EMBOSS版本中保留哪些应用程序选项。如果选项符合以下情况，应予以舍弃：

- 冗余于EMBOSS内置功能
- 由新的EMBOSS限定符合理地涵盖
- 始终设置，因此无需在ACD文件中定义

您应该熟悉EMBOSS内置的功能（参见第3.1节，“EMBOSS编程”），以帮助确定哪些选项是冗余的。例如，HMMER帮助选项`-h`不需要，因为`-help`是所有EMBOSS应用程序的内置限定符。

一个或多个选项可能合理地由单个EMBOSS限定符覆盖；例如，**hmmbuild**中有五个用于设置序列加权的选项，这些选项由EMBASSY包装器等效项中的单个加权选项处理。

某些选项应始终在EMBOSS版本中设置，因此无需在ACD文件中定义；例如，用于强制覆盖文件的`-F`选项始终被设置。

### 10.4.1.3 新选项

第二步是决定是否需要任何新参数。通常需要一个输出文件参数来捕获默认写入`stdout`的输出。

### 10.4.2 ACD文件开发

需要考虑的关键事项如下：

- 应用程序名称
- 应用程序简短描述
- 程序选项文档
- 限定符名称
- 验证和重新格式化ACD。

### 10.4.2.1 应用程序名称

对于**HMMER**，使用了原始应用程序名称，只是EMBOSS版本前面加上了前缀“e”。除非在不可避免的情况下，例如EMBOSS或系统中已存在同名应用程序，否则应使用原始名称或其简单派生名称。

### 10.4.2.2 应用程序简短描述

应用程序简短描述直接从_用户指南_中获取，并粘贴到应用程序定义的documentation:属性中。每个选项的描述和文档同样从_用户指南_中获取，并根据需要粘贴到`help:`和`information:`属性中。这是至关重要的文档，不能省略。

### 10.4.2.3 应用程序选项

尽可能选择的限定符名称与原始选项名称相同。但是，在与原始保持一致性与与EMBOSS保持一致性之间存在妥协。如果有疑问，请咨询EMBOSS开发人员。

### 10.4.2.4 ACD文件

使用EMBOSS实用程序`acdc`和`acdpretty`对ACD文件进行了测试和重新格式化。开发ACD文件时应常规使用这些工具。有关ACD文件开发的更多信息可参见第5章_“C编程”_，有关ACD实用程序的信息可参见第4.6节_“ACD实用程序”_。

### 10.4.3 C源代码开发

应用程序C源代码按以下顺序实现：

- 1. 应用程序头文档
- 2. `main()`函数
- 3. 处理ACD数据项的变量
- 4. 调用`embInitP`
- 5. 调用`ajAcdGet*`函数以检索ACD数据定义的对象
- 6. 重新格式化输入文件的代码（如有必要）
- 7. 构建和调用**HMMER**命令行的代码
- 8. 重新格式化输出文件的代码（如有必要）
- 9. 清理ACD变量的代码。

### 10.4.3.1 应用程序头

应用程序头文档（第D.3节_“应用程序代码文档”_）是从另一个EMBOSS应用程序中粘贴过来的。然后添加了一个空的`main()`函数和用于处理ACD数据项的变量。添加了对`embInitP`的调用以处理ACD文件，并使用`ajAcdGet*`函数来检索ACD值。

### 10.4.3.2 文件重新格式化和维护

在必要且可能的情况下，添加了使用临时文件重新格式化输入文件的代码。同样在必要时，添加了使用临时文件重新格式化输出文件的代码。最后，添加了清理ACD变量内存的代码。

### 10.4.3.3 命令行生成

代码中最困难的部分是构建对HMMER命令行的调用，但一旦所有选项都被正确理解，这就非常简单。在生成命令行时出现了一些棘手的问题，您将在代码中稍后看到这些问题。这些问题已在代码中记录，以节省他人未来的时间。您应始终在自己的代码中记录此类棘手步骤。

### 10.4.4 质量保证测试

为应用程序编写了质量保证测试（第7.2节_“应用程序质量保证”_）。这些测试基于教程中的示例，这些示例使用HMMER发行版中的文件。在测试数据尚未可用的情况下，则需要收集这些数据。

### 10.4.5 文档

文档包括软件包分发的README文件以及标准的EMBASSY软件包和应用程序文档。

为软件包分发编写了README文件，涵盖了所有基础知识，并包含了以下主题：

- 如何下载HMMER的原始版本和EMBASSY版本
- 在哪里获取安装说明和文档
- 要求、注意事项等
- 两个版本之间应用程序的差异（见下文）。

为每个应用程序做了说明，以描述：

- 作为ACD限定符支持的HMMER选项
- EMBOSS版本中的任何新限定符和参数
- 参数顺序是否已更改。

然后按照指南（第8.2节_“应用程序文档”_）为软件包生成了正式文档。在应用程序文档的许多部分中，文本可以直接从原始文档粘贴。除了已经描述过的README文件外，没有编写新文档。插入文本后，使用EMBOSS提供的脚本自动生成完整的文档文件。





## 10.4.6 集成

最后的步骤是将新包代码提交到 EMBOSS CVS 服务器（参见第 1.5 节，“向 EMBOSS 贡献软件”）并更新 EMBOSS ftp 和网站。此类集成问题由 EMBOSS 开发人员处理。

## 10.5 HMMER wrapper：概述

EMBASSY HMMER 包（用于原始 HMMER v2.3.2 应用程序的包装器）概述如下。

- HMMER v2.3.2 必须安装在与 EMBOSS 相同的系统上，并且 HMMER 可执行文件的位置必须定义在您的路径中，EMBASSY HMMER 才能工作。
- 尽可能使用与原始 HMMER 相同的命令行限定符名称和参数顺序。但是，存在几个不可避免的差异，这些差异已明确记录。
- 原始 HMMER 用户指南中记录为“专家”的几乎所有选项在 ACD 中都作为“高级”选项给出。必须在命令行上指定 -options 才能提示输入它们的值。
- 原始 HMMER 使用（如果已定义）BLAST 环境变量来定位文件，而 EMBASSY HMMER 则不使用。
- 比对和序列的输入和输出仅限于原始 HMMER 支持的格式。调整代码以支持所有 EMBOSS 支持的格式将相当简单。
- 不支持自动处理 gzip 文件。
- HMMER v2.3.2 因此 EMBASSY HMMER 仅推荐用于蛋白质序列。如果您提供非蛋白质序列，系统会重新提示您输入蛋白质序列——这是通过在 ACD 文件中将序列输入的 type: 属性设置为 protein 来实现的。要接受核酸序列，您需要将 protein 替换为 nucleic。

## 10.6 HMMER wrapper：hmmbuild

hmmbuild 的基本功能是读取多序列比对文件，构建新的 profile HMM 并将 HMM 保存到文件。调用方式如下：

```
ehmmbuild[options] alignfile hmmfile
```

默认情况下，模型配置为查找一个或多个与模型全局且与序列局部的非重叠比对。可以通过使用相应选项设置各种其他比对策略。

一个限制是，用户必须为 `alignfile` 选项提供比对的完整文件名，而不是对一组序列的间接引用，因此 USA（参见 *EMBOSS 用户指南*）是 *不可接受* 的。这是因为 **hmmbuild**（由 **ehmmbuild** 包装）需要一个比对且不支持 USAs。

包装器与原始软件之间的差异如下：

- 请注意，`alignfile` 参数（用于输入）和 `hmmfile` 参数（用于输出）在原始 **HMMER** 中指定顺序相反。这是因为在 EMBOSS 中，输入参数始终在输出参数之前指定。
- 原始 **HMMER** 的几个选项不受支持。使用 `-help` 代替 `-h HMMER` 选项，用于设置比对策略的三个 **HMMER** 选项被替换为 `-strategy` 限定符，该限定符在 ACD 中是一个列表。
- 不需要选项来指定是否追加到输出文件，因为可以通过在 ACD 文件中使用 `append:` 属性来设置。可以说这应该是一个受支持的选项。
- `-F` 选项（用于强制覆盖现有 HMM 文件）始终被设置，因为应用程序应尽可能始终生成输出，并且 EMBOSS 信任其用户正确指定文件。
- 不需要 `-amino` 和 `-nucleic` 选项，因为它们通过在 ACD 文件中使用 `type:` 属性来设置。
- 不支持 `-informat`，因为这会让用户困惑，用户不应该指定输入文件的格式。
- 用于指定序列加权算法的六个选项均由 ACD 文件中定义为列表的单个 `-weighting` 限定符处理。这纯粹是为了方便。
- 最后，使用 `-verbosity` 代替 `-verbose`。

## 10.6.1 HMMER wrapper：ehmmbuild.acd

### 10.6.1.1 应用程序定义和输入

ACD 文件的开头如下所示。`help:` 属性的文本未显示，但在 ACD 文件中给出。

可以看到，`alignfile` 选项由 `seqset` 序列输入类型处理。如前所述，这必须是比对文件，而不是间接引用一组序列的 USA。可以通过首先将 USA 转换为本地文件来克服此限制，但此版本的包装器未执行此操作：

```
application: ehmmbuild
[
# EMBOSS wrapper to hmmbuild from Sean Eddy's HMMER package
# v2.3.2
  documentation: "Build a profile HMM from an alignment."
  groups: "HMM"
  gui: "yes"
  batch: "yes"
  cpu: "medium"
  embassy: "hmmernew"
]
section: input
[
    information: "Input section"
    type: "page"
]
seqset: alignfile
[
# User must provide the full filename of an alignment, not an
# indirect reference to a set of sequences, e.g. a USA is NOT
# acceptable.
    parameter: "Y"
    type: "gapstopprotein"
    aligned: "Y"
]
...
```

然后有三个 infile ACD 定义来处理各种 HMMER 输入文件。所有这些都是高级 ACD 选项，通常不由用户设置。请注意，为它们设置了 NULL 默认值，这需要指定 nullok: 属性并将其设置为 True。

```
infile: prior
[
# Advanced input file
    information: "Dirichlet prior file."
    knowntype: "dirichlet prior"
    default: ""
    nullok: "Y"
]
infile: null
[
# Advanced input file
    information: "NULL model file"
    knowntype: "hmmmer null model"
    default: ""
    nullok: "Y"
]
infile: pam
[
# Advanced input file
    information: "PAM file"
    knowntype: "hmmmer matrix file"
    default: ""
    nullok: "Y"
]
float: pamwgt
[
    default: "20.0"
    information: "Weighting for PAM."
]
endsection: input
```

### 10.6.1.2 必需部分

必需部分如下所示。如您所见，它相当简单。它包含一个用于指定 HMM 名称的字符串和一个用于设置比对策略的列表。该列表替换了三个单独的 HMMER 选项。还有一个默认设置，因此此列表总共有四个条目：

```
section: required
[
    information: "Required section"
    type: "page"
]

string: n
[
    standard: "Y"
    default: ""
    information: "Name for this HMM."
    word: "Y"
    knowntype: "name"
]

list: strategy
[
    standard: "Y"
    default: "D"
    minimum: "1"
    maximum: "1"
    values: "D:global-multidomain,F:local-multidomain,G:global-singledomain,S:local-singledomain"
    delimiter: ","
    codedelimiter: ":"
    header: "Alignment preference"
    information: "Select preference"
    button: "Y"
]

endsection: required
```

### 10.6.1.3 高级部分

大部分 HMMER 选项在原始 HMMER 文档中定义为“专家”选项，因此在 ACD 文件的高级部分中给出。这些选项通常不由用户设置，并给出了从 HMMER 文档中获取的默认值：

```
section: advanced
[
    information: "Advanced section"
    type: "page"
]

integer: pbswitch
[
    default: "1000"
    information: "Threshold to switch to position-based weights."
]

float: archpri
[
  default: "0.85"
  information: "Architecture prior"
]

boolean: binary
[
  default: "N"
  information: "Write HMM as binary."
]

boolean: fast
[
  default: "N"
  information: "Work in fast mode"
]

float: gapmax
[
  default: "0.5"
  information: "Fast mode control"
]

boolean: hand
[
  default: "N"
  information: "Specify model by hand."
]

float: sidlevel
[
  default: "0.62"
  information: "Cutoff ID threshold"
]
```

序列加权算法也作为高级 ACD 限定符指定。这个列表替换了原始 HMMER 中给出的六个命令行选项：

```
boolean: noeff
[
  default: "N"
  information: "Turn off the effective sequence number calculation."
]

float: swentry
[
  default: "0.5"
  information: "Probability control for local entries"
]

float: swexit
[
  default: "0.5"
  information: "Probability control for exits"
]
```



boolean: verbosity
[
    default: "N"
    information: "详细程度。"
]

list: weighting
[
    default: "G"
    minimum: "1"
    maximum: "1"
    values: "B:Blosum, G:Gerstein/Sonnhammer/Chothia, K:Krogh/Mitchison, W:Henikoff, V:Sibbald/Argos Voronoi, N:None"
    delimiter: ","
    codedelimiter: ":"
    header: "加权方法"
    information: "选择加权"
    button: "Y"
]

endsection: advanced

## 10.6.1.4 输出部分

此处显示输出部分。其中包含为 HMM 输出文件定义的新参数（该参数直接写入 stdout），以及 HMMER 使用的另外两个输出文件。

```
section: output:
[
    information: "Output section"
    type: "page"
]

outfile: hmmfile
[
    parameter: "y"
    knowntype: "hmm file"
    append: "y"
]

outfile: o
[
    nullok: "Yes"
    nulldefault: "Yes"
    information: "Resave starting alignment."
    knowntype: "selex file"
]

outfile: cfile
[
    nullok: "Yes"
    nulldefault: "Yes"
    information: "Emission and transition count file"
    knowntype: "hmmmer count file"
]

endsection: output
```

## 10.6.2 HMMER 包装器：ehmmbuild.c

### 10.6.2.1 头文件文档

以下显示了 C 源代码文件的开头。这仅显示了任何 EMBOSS 应用程序都应提供的标准文档。还有一行（#include emboss.h）用于导入 AJAX 和 NUCLEUS 库接口：

```
/* @source ehmmbuild application
**
** EMBOSS wrapper to hmmbuild from Sean Eddy's HMMER package v.2.3.2
** Build a profile HMM from an alignment.
**
** @author Copyright (C) Jon Ison
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
******************************************************************************/

#include "emboss.h"
```

### 10.6.2.2 main() 函数

以下显示了 main() 函数及其变量声明。所有用于处理 ACD 数据项的变量都与相应的限定符同名。这种风格并非强制要求，但推荐使用，因为它能使阅读源代码更加容易。

内务变量被赋予了合理的名称。所有变量都初始化为 NULL 或零。这样做是良好的做法，事实上不这样做很危险，因为 EMBOSS 库的某些部分假设非 NULL 指针已分配了内存；如果在运行时向它们赋予了垃圾值，则可能会导致段错误。

```
/* @prog ehmmbuild ***********************************************************************
**
** EMBOSS wrapper to hmmbuild from Sean Eddy's HMMER package v.2.3.2
** Build a profile HMM from an alignment.
**
******************************************************************************/

int main(int argc, char **argv)
{
    /* ACD data item variables */
    AjPSeqset alignfile = NULL;
    AjPFile prior = NULL;
    AjPFile null = NULL;
    AjPFile pam = NULL;
    float pamwgt = 0.0;
    AjPStr n = NULL;
    AjPStr *strategy = NULL;
    ajint pbswitch = 0;
    float archpri = 0.0;
    AjBool binary = ajFalse;
    AjBool fast = ajFalse;
    float gapmax = 0.0;
    AjBool hand = ajFalse;
    float idlevel = 0.0;
    AjBool noeff = ajFalse;
    float swentry = 0.0;
    float swexit = 0.0;
    AjBool verbosity = ajFalse;
    AjPStr *weighting = NULL;
    AjPFile hmmfile = NULL;
    AjPFile o = NULL;
    AjPFile cfile = NULL;

    /* Housekeeping variables */
    AjPStr cmd = NULL;
    AjPStr rnd1 = NULL;
    AjPStr rnd2 = NULL;
    AjPStr tmp = NULL;
    AjPStr fmt = NULL;
    char option;
    AjBool fmtok = ajFalse;
    AjPStr hmmfilename = NULL;
}
```

### 10.6.2.3 处理 ACD 文件

以下代码显示了处理 ACD 文件的函数调用。embInitP 处理 ACD 文件，并提示用户输入命令行中未指定的任何必需值。前缀为 ajAcdGet 的函数系列用于从 ACD 数据定义中检索值，并将其存储在先前定义的变量中：

```
/* ACD file processing */
embInitP("ehmmbuild",argc,argv,"HMMERNEW");

alignfile = ajAcdGetSeqset("alignfile");
prior = ajAcdGetInfile("prior");
null = ajAcdGetInfile("null");
pam = ajAcdGetInfile("pam");
pamwgt = ajAcdGetFloat("pamwgt");
n = ajAcdGetString("n");
strategy = ajAcdGetList("strategy");
pbswitch = ajAcdGetInt("pbswitch");
archpri = ajAcdGetFloat("archpri");
binary = ajAcdGetBoolean("binary");
fast = ajAcdGetBoolean("fast");
gapmax = ajAcdGetFloat("gapmax");
hand = ajAcdGetBoolean("hand");
idlevel = ajAcdGetFloat("idlevel");
noeff = ajAcdGetBoolean("noeff");
swentry = ajAcdGetFloat("swentry");
swexit = ajAcdGetFloat("swexit");
verbosity = ajAcdGetBoolean("verbosity");
weighting = ajAcdGetList("weighting");
hmmfile = ajAcdGetOutfile("hmmfile");
o = ajAcdGetOutfile("o");
cfile = ajAcdGetOutfile("cfile");
```

### 10.6.2.4 内务处理和文件格式处理

以下显示了应用程序代码的主体部分。首先是一些内务处理代码。然后是一段代码块，用于检查序列比对输入文件是否为 HMMER 可理解的格式。如果指定了不支持的格式，则会引发异常。未来可以将其替换为将比对文件重新格式化为适当格式的代码。在撰写本文时，尚未完全测试所有比对格式（包括 SELEX 和 Stockholm）是否可以在不丢失任何数据或注释的情况下相互转换，因此选择了安全的选项：

```
/* MAIN APPLICATION CODE */
/* 1. Housekeeping */
cmd = ajStrNew();
rnd1 = ajStrNew();
rnd2 = ajStrNew();
tmp = ajStrNew();
fmt = ajStrNew();
hmmfilename = ajStrNew();

ajStrAssignC(&hmmfilename, ajFileGetNameC(hmmfile));
/* 2. Ensure alignfile is in format HMMER can understand. These include
FASTA, GENBANK, EMBL, GCG, PIR, STOCKHOLM, SELEX, MSF,CLUSTAL and PHYLIP.
EMBOSS name definitions are taken from seqInFormatDef in ajseqread.c and
seqOutFormat in ajseqwrite.c */
fmtok=ajFalse;
ajStrAssignS(&fmt, ajSeqsetGetFormat(alignfile));
if(ajStrMatchC(fmt, "fasta")
|| ajStrMatchC(fmt, "genbank")
|| ajStrMatchC(fmt, "embl")
|| ajStrMatchC(fmt, "gcg")
|| ajStrMatchC(fmt, "pir")
|| ajStrMatchC(fmt, "stockholm")
|| ajStrMatchC(fmt, "selex")
|| ajStrMatchC(fmt, "msf")
|| ajStrMatchC(fmt, "clustal")
|| ajStrMatchC(fmt, "phylip"))
fmtok = ajTrue;
/* This could be replaced with code to reformat the file. */
if(!fmtok)
ajFatal("Input alignment ('alignfile' ACD option) is not in a format "
"HMMER understands. Please use a file in FASTA, GENBANK,"
"EMBL, GCG, PIR, STOCKHOLM, SELEX, MSF,CLUSTAL or PHYLIP format.");
```

### 10.6.2.5 构建命令行

以下显示了构建命令行的第一部分代码。命令行按特定顺序构建，以便更轻松地为新版本更新包装器。首先将应用程序名称粘贴到字符串中，然后按 ACD 文件中出现的顺序给出原始 HMMER 选项。接着给出在 ACD 文件中没有对应项的 HMMER 选项。最后，给出特定于 EMBASSY 包装器的新参数和选项：

```
/* 3. Build hmmbuild command line */
/* Command line is built in this order:
   i. Application name.
   ii. HMMER 'options' (in order they appear in ACD file)
   iii.HMMER 'options' (that don't appear in ACD file)
   iv. HMMER and new parameters.
   */
ajFmtPrintS (&cmd, "hmmbuild ");

if(prior)
   ajFmtPrintAppS (&cmd, " -prior %s ", ajFileGetNameC(prior));

if(null)
   ajFmtPrintS (&cmd, " -null %s ", ajFileGetNameC(null));

if(pam)
   ajFmtPrintAppS (&cmd, " -pam %s -pamwgt %f ",
                   ajFileGetNameC(pam), pamwgt);

ajFmtPrintAppS (&cmd, " -n %S ", n);

/* ACD option only allows one selection */
option = ajStrGetCharFirst (strategy[0]);

if(option == 'F')
   ajStrAppendC (&cmd, " -f ");
else if(option == 'G')
   ajStrAppendC (&cmd, " -g ");
else if(option == 'S')
   ajStrAppendC (&cmd, " -s ");

/* else go with default ('D' option in ACD file) */
ajFmtPrintAppS (&cmd, " -pbswitch %d ", pbswitch);
ajFmtPrintAppS (&cmd, " -archpri %f ", archpri);

if(binary)
   ajStrAppendC (&cmd, " -binary ");

if(fast)
   ajFmtPrintAppS (&cmd, " -fast -gapmax %f ", gapmax);

if(hand)
   ajStrAppendC (&cmd, " -hand ");

ajFmtPrintAppS (&cmd, " -idlevel %f ", idlevel);

if(noeff)
   ajStrAppendC (&cmd, " -noeff ");

ajFmtPrintAppS (&cmd, " -swentry %f ", swentry);
```





ajFmtPrintAppS(&cmd, " --swexit %f ", swexit);

if(verbosity)
    ajStrAppendC(&cmd, " --verbose ");

构建命令行的其余代码如下。唯一需要指出的是，**append** 选项始终被设置。这意味着输出应始终追加到指定输出文件中的内容。不过，EMBOSS 默认会清除其输出文件，因此要使此功能生效，hmmfile ACD 数据项的 append : 属性必须设置为 True：

```
/* ACD option only allows one selection */
option = ajStrGetCharFirst(weighting[0]);

if(option == 'B')
    ajStrAppendC(&cmd, " -wblosum ");
else if(option == 'G')
    ajStrAppendC(&cmd, " -wgsc ");
else if(option == 'K')
    ajStrAppendC(&cmd, " -wme ");
else if(option == 'W')
    ajStrAppendC(&cmd, " -wpb ");
else if(option == 'V')
    ajStrAppendC(&cmd, " -wvoronoi ");
else if(option == 'N')
    ajStrAppendC(&cmd, " -wnone ");

if(o)
    ajFmtPrintAppS(&cmd, " -o %s ", ajFileGetNameC(o));

if(cfile)
    ajFmtPrintAppS(&cmd, " -cfile %s ", ajFileGetNameC(cfile));

/* -A (append) always set but file will be wiped by EMBOSS first unless
** append: "Y" is set for "hmmfile" in the ACD file.
*/
ajStrAppendC(&cmd, " -A -F ");
ajFmtPrintAppS(&cmd, " %S %S", hmmfilename, ajSeqsetGetFilename(alignfile));
```

## 10.6.2.6 调用应用程序

下面的代码展示了使用刚刚构建的命令行调用 **hmmbuild** 应用程序的系统调用。请注意，此处使用了 `system()`，但如前所述，可能应将其替换为对 `exec()` 的调用。还有一些用于内存管理的清理代码，以确保应用程序可以干净地关闭：

```
/* 4. Close ACD files */
ajSeqsetDel(&alignfile);
ajFileClose(&prior);
ajFileClose(&null);
ajFileClose(&pam);
ajFileClose(&hmmfile);
ajFileClose(&o);
ajFileClose(&cfile);

/* 5. Call hmmbuild */
ajFmtPrint("\n%s\n", cmd);
system(ajStrGetPtr(cmd));
/* 6. Exit cleanly */
ajStrDel(&n);
ajStrDel(&cmd);
ajStrDel(&rnd1);
ajStrDel(&rnd2);
ajStrDel(&tmp);
ajStrDel(&fmt);
ajStrDel(&hmmfilename);

embExit();

return 0;
}
```

## 10.7 HMMER 包装器：hmmalign

我们现在将介绍另一个 HMMER 应用程序 hmmalign。其基本功能是读取 HMM 配置文件和一组序列，将序列与配置文件比对，并输出多序列比对。调用方式如下：

```
hmmalign [options] hmmfile seqfile outfile
```

序列集可以是未比对的，也可以是已比对的。如果已比对，则会忽略现有的比对，hmmalign 将按其意愿对其进行比对。

hmmalign 仅作基本介绍，因为之前关于 hmmbuild 的几乎所有内容都适用于所有其他 HMMER 应用程序。

-outfile 参数是 EMBOSS HMMER 中的新增参数。多序列比对始终写入 outfile，而不是写入 stdout。

与 hmmbuild 不同，用户可以为序列输入指定 USA。这是因为 HMMER 会忽略任何比对，因此包装器可以将文件视为未比对序列，并在必要时将其转换为 HMMER 可理解的格式。应用程序会对其输入序列数据制作临时本地副本。由用户确保运行目录中有足够的磁盘空间。

原始 HMMER 的一些选项不受支持。再次强调，-h 是多余的。-informat、-oneline 和 -outformat 是为用户指定输入序列文件和输出比对的格式而提供的。包装器中不需要这些选项。

几乎任何序列格式都会被理解，而比对格式可以在 ACD 文件中指定，或通过使用内置的 -aformat 命令行限定符来指定。

## 10.7.1 HMMER 包装器：hmmalign.acd

ACD 文件非常简单。它只包含输入和输出部分。

## 10.7.1.1 输入部分

此处显示了输入部分的摘录。请注意，HMM 文件使用 infile，而序列输入使用 seqset。如前所述，EMBOSS 通常支持的所有序列格式均受到完全支持。

```
application: ehmmalign
[
# EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package
# v.2.3.2
    documentation: "Align sequences to an HMM profile"
    groups: "HMM"
    gui: "yes"
    batch: "yes"
    cpu: "medium"
    embassy: "hmmernew"
]

section: input
[
    information: "Input section"
    type: "page"
]

infile: hmmfile
[
    parameter: "Y"
    information: "HMM file"
    knowntype: "hmm file"
    help: "File containing a HMM profile"
]

seqset: seqfile
[
    parameter: "Y"
    type: "gapstopprotein"
    help: "File containing a (set of) sequence(s)"
    aligned: "N"
]

...
endsection: input
```

## 10.7.1.2 输出部分

此处显示了输出部分。唯一需要指出的是，输出文件由 align 数据项处理，且比对格式由 aformat : 属性设置：

```
section: output
[
    information: "Output section"
    type: "page"
]

align: o
[
    parameter: "y"
    help: "Multiple sequence alignment output file."
    aformat: "fasta"
]

boolean: m
[
    additional: "Y"
    default: "N"
    information: "Only show match state alignment symbols."
]

boolean: q
[
    additional: "Y"
    default: "N"
    information: "Suppress all output except the alignment."
]
endsection: output
```

## 10.7.2 HMMER 包装器：ehmmalign.c

## 10.7.2.1 文档标题

此处显示了 C 源代码的开头。文档与 hmmbuild 的完全相同。

```
/* @source ehmmalign application
**
** EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package v.2.3.2
** Align sequences to an HMM profile.
**
** @author Copyright (C) Jon Ison
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
********************************************************************************/
#include "emboss.h"

/* @prog ehmmalign *********************************************************************************
**
** EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package v.2.3.2
** Align sequences to an HMM profile.
**
******************************************************************************************/
```

## 10.7.2.2 main() 函数、清理和 ACD 文件处理

此处显示了 main() 函数、变量声明、处理 ACD 文件的代码以及一些清理代码。

```
int main(int argc, char **argv)
{
	/* ACD data item variables */
	AjPFile hmmfile = NULL;
	AjPSeqset seqfile = NULL;
	AjPFile mapali = NULL;
	AjPFile withali = NULL;
	AjPAlign o = NULL;
	AjBool m = ajFalse;
	AjBool q = ajFalse;

	/* Housekeeping variables */
	AjPStr cmd = NULL;
	AjPStr tmp = NULL;
	AjPStr fmt = NULL;
	AjBool fmtok = ajFalse;
	AjPStr rnd = NULL;
	AjPSeqout rndo = NULL;

	/* ACD file processing */
	embInitP("ehmmalign",argc,argv,"HMMERNEW");

	hmmfile = ajAcdGetInfile("hmmfile");
	seqfile = ajAcdGetSeqset("seqfile");
	mapali = ajAcdGetInfile("mapali");
	withali = ajAcdGetInfile("withali");
	o = ajAcdGetAlign("o");
	m = ajAcdGetBoolean("m");
	q = ajAcdGetBoolean("q");

	/* MAIN APPLICATION CODE */
	/* 1. Housekeeping */
	cmd = ajStrNew();
	tmp = ajStrNew();
	fmt = ajStrNew();
	rnd = ajStrNew();
```

## 10.7.2.3 文件格式处理

此处显示了将输入文件重新格式化为 HMMER 适用格式（即 FASTA）所需的代码。必须这样做，因为 hmmalign 仅在输入时理解 FASTA 格式，而且序列可能是通过 USA 指定的，需要将其转换为序列文件。

使用 ajFilenameSetTempname 设置可用的随机文件名，然后使用 ajSeqoutOpenFilename 以该文件名初始化 seqout 对象。

通过 ajSeqoutSetFormatS 设置输出格式。使用 ajSeqoutWriteSeq 写入序列。最后，使用 ajSeqoutClose 关闭文件并删除 seqout 对象：

```
/* 2. Re-write seqfile to a temporary file in a format (FASTA) HMMER can understand.
   We cannot just pass the name of seqfile to HMMER as the name provided might be
   a USA which HMMER would not understand. */
rnd = ajStrNew();
ajFilenameSetTempname(&rnd);
rndo = ajSeqoutNew();
```





if(!ajSeqoutOpenFilename(rndo, rnd))
    ajFatal("Failed to open file '%s'", rnd);
ajSeqoutSetFormatC(rndo, "fasta");
ajSeqoutWriteSet(rndo, seqfile);
ajSeqoutClose(rndo);
ajSeqoutDel(&rndo);

## 10.7.2.4 构建命令行

以下是构建命令行的代码。再次强调，命令行是按特定顺序构建的，以便将来更易于维护。

这里需要指出的是，EMBOSS 支持某些原始 HMMER 不支持的比对格式，而 HMMER 支持某些 EMBOSS 不支持（或在撰写本文时不支持）的格式。

如果用户指定的格式不受支持，则会引发异常并将格式设置为 Stockholm。将来，这可以替换为根据需要重新格式化输出文件的代码。

```
/* 3. Build hmmalign command line */
/* Command line is built in this order:
i. Application name.
ii. HMMER 'options' (in order they appear in ACD file)
iii.HMMER 'options' (that don't appear in ACD file)
iv. HMMER and new parameters.
*/
ajFmtPrintS(&cmd, "hmmalign ");

if(mapali)	ajFmtPrintAppS(&cmd, " -mapali %s ", ajFileGetNameC(mapali));

if(withali)	ajFmtPrintAppS(&cmd, " --withali %s ", ajFileGetNameC(withali));

if(m)	ajStrAppendC(&cmd, " -m ");

if(q)	ajStrAppendC(&cmd, " -q ");

/* Ensure output alignment is in user-specified format. */
fmtok=ajTrue;
ajStrAssignS(&fmt, ajAlignGetFormat(o));
/* fasta and a2m are identical formats. */

if(ajStrMatchC(fmt, "fasta"))	ajStrAssignC(&fmt, "A2M");
else if(ajStrMatchC(fmt, "a2m"))	ajStrAssignC(&fmt, "A2M");
else if(ajStrMatchC(fmt, "msf"))	ajStrAssignC(&fmt, "MSF");
else if(ajStrMatchC(fmt, "phylip"))	ajStrAssignC(&fmt, "PHYLIP");
/* hmmmer also supports stockholm, SELEX and Clustal output, EMBOSS does not.
** EMBOSS supports unknown/multiple/simple and srs output, hmmmer does not.
*/
else
fmtok = ajFalse;
if(!fmtok)
{
    /* This could be replaced with code to reformat the file. */
    ajWarn("Specified output alignment format ('o' ACD option) is "
           "not understood by HMMER. Using stockholm format instead.");
    ajStrAssignC(&fmt, "Stockholm");
}
```

## 10.7.2.5 调用应用程序

这展示了调用 hmmalign 应用程序的代码。同样，对 system() 的调用可能应该替换为对 exec() 的调用。可以看到，一个名为 rnd 的临时变量用于重写的序列输入文件的名称。必须使用 -inform 选项显式指定 FASTA 格式。

```
/* rnd is the name of the rewritten seqfile. MUST specify FASTA format explicitly. */
ajFmtPrintAppS(&cmd, " --inform FASTA --outformat %S -o %s %s %S",
               fmt,
               ajAlignGetFilename(o),
               ajFileGetNameC(hmnfile),
               rnd);

/* 4. Close ACD files */
ajFileClose(&hmnfile);
ajSeqsetDel(&seqfile);
ajFileClose(&mapali);
ajFileClose(&withali);
ajAlignDel(&o);

/* 5. Call hmmalign */
ajFmtPrint("\n%s\n\n", cmd);
system(ajStrGetPtr(cmd));

/* 6. Exit cleanly */
ajFmtPrintS(&tmp, "rm %s", rnd);
system(ajStrGetPtr(tmp));

ajStrDel(&cmd);
ajStrDel(&tmp);
ajStrDel(&fmt);
ajStrDel(&rnd);

embExit();

return 0;
}
```

## 10.8 减少命令行长度

在封装具有许多可能命令行限定符的应用程序时，可能会出现问题。MIRA 包就是一个例子，它大约有一百个限定符。对于这样的包，不能明智地采用构建包含所有可能限定符的命令行的方法；命令行可能对 shell 来说太长，而且肯定难以阅读和调试。

MIRA 封装器采用两种方法来避免命令行混乱。第一种是使用 ajAcdIsUserdefinedC 库函数。下面的代码片段演示了这一点：

```
...
AjPStr cl = NULL;
AjPStr squal = NULL;
...
if(ajAcdIsUserdefinedC("genome"))
{
    squal = ajAcdGetListSingle("genome");
    ajFmtPrintAppS(&cl, " -genome%S", squal);
    ajStrDel(&squal);
}
```

ajAcdIsUserdefinedC 函数调用检查用户是否针对命名的 ACD 限定符名称输入了任何内容，或者是否在命令行上为该限定符指定了值。如果其中任何一种情况为真，则上述代码从 ACD 检索值，并将限定符和值添加到命令行中。如果用户未提供值，则（正确）假设 MIRA 程序将使用默认值，因此命令行保持不变。

这种方法效果相当不错，但有一个缺点。如果用户输入了任何内容，ajAcdIsUserdefinedC 调用将返回真值；这包括输入 ACD 中给定限定符的默认值。最好是命令行中不包含不必要的指定的默认值。MIRA 封装器中其余代码（即第二种方法）所做的正是如此。研究这段代码是一个有用的练习。

由于 MIRA 允许用户可选地提供一个可以附加到命令行限定符的前缀，因此代码变得稍微复杂了一点。例如，限定符 -project 也可以指定为 -GE:project，因为它属于“GEneral”输入选项类。因此，封装器首先在静态数组中列出所有限定符及其前缀。然后，它将它们全部加载到 AjPTable 查找表中，作为 main() 中的第一项工作之一（代码很简单，因此此处未显示）

```
typedef struct MiraSPrefix
{
    const char* qname;
    const char* prefix;
} MiraOPrefix;
#define MiraPPrefix MiraOPrefix*

static MiraOPrefix miraprefix[] = {
    {"project", "GE:"},
    {"lj", "GE:"},
    {"fo", "GE:"},
    {"mxti", "GE:"},
    {"rns", "GE:"},
    {"eq", "GE:"},
    {"eqo", "GE:"},
    {"droeqe", "GE:"},
    {"uti", "GE:"},
    {"ess", "GE:"},
    {"ps", "GE:"},
    ...
    {NULL, NULL}
};
```

在解释了这一复杂性之后，现在可以描述封装器使用的策略了。封装器程序员浏览 ACD 文件，并为 C 代码将所有不同的数据类型分组。换句话说，封装器将把所有字符串数据类型作为一个代码部分来处理，然后是所有输入文件数据类型，等等。以字符串数据类型为例，封装器在另一个静态块中定义了这些内容。

```
typedef struct MiraSquals
{
    const char* qname;
    const char* mname;
    const char* def;
} MiraOQuals;
#define MiraPQuals MiraOQuals*

static MiraOQuals miraStrings[] =
{
    {"project", "project", "mira"},
    {"bsn", "bsn", ""},
    {"np", "np", "mira"},
    {"gapfda", "gap4da", "gap4da"},
    {"log", "log", "miralog"},
    {"co", "co", "mira_out.caf"},
    ...
    {NULL, NULL, NULL}
};
```

MiraSquals 结构体用于定义所有其他数据类型名称块以及字符串。对于每个定义块，变量 qname 是 ACD 中指定的限定符名称，变量 mname 是要在命令行上打印的名称（如您所见，对于 gapfda 它们不同），而 def 是 ACD 文件中指定的限定符的默认值。这就是该方法的微小缺点所在，即您必须在 ACD 文件和 C 代码中都指定默认值。您还显然应该确保它们匹配，尽管如果不匹配也不会造成太大危害——您只是会在命令行上看到一个意外的限定符。在这种情况下，优点大于缺点。接下来需要做的就是为每种数据类型编写一个简单的函数，并从 main() 中调用该函数。处理字符串的函数如下所示：

```
static void emira_dostrings (AjPStr *cl, AjPTable table)
{
    ajuint i;
    AjPStr squal = NULL;
    AjPStr prefix = NULL;
    AjPStr key = NULL;
    AjPStr value = NULL;

    prefix = ajStrNew();
    key = ajStrNew();

    i = 0;
    while(miraStrings[i].qname)
    {
        squal = ajAcdGetString(miraStrings[i].qname);
        ajStrAssignC(&key,miraStrings[i].qname);
        ajStrAssignC(&prefix,"");
        value = ajTableFetch(table, key);
        if(value)
            ajStrAssignS(&prefix,value);
        if(!ajStrMatchC(squal,miraStrings[i].def))
            ajFmtPrintAppS(cl, " -%Ss=%S",prefix,miraStrings[i].mname,squal);
            ajStrDel(&squal);
            ++i;
    }
    ajStrDel(&key);
    ajStrDel(&prefix);
    return;
}
```

代码按顺序查看定义的字符串静态表。首先，代码从 ACD 检索关联值。然后，它在限定符前缀表中查找任何关联的前缀值，并相应地设置变量（对于大多数包不需要这样做，因此代码可以简化）。然后，它将从 ACD 检索的值与静态定义块中给出的默认值进行比较，只有在两个值不匹配时才将限定符添加到命令行中。

这段代码的结果是一个整洁干净的命令行。该代码的另一个优点是，它避免了在封装器开头定义一长串难看的 `ajAcdGet*` 函数调用块。尽管您可能认为这种方法对于封装接口更简单的包来说有些过度设计，但它仍然值得考虑，因为生成的封装器更易于维护。

## 10.9 如何移植第三方应用程序

开发封装器时完成的大部分步骤在移植软件时也需要完成。仍然需要 ACD 文件。主要区别在于编写源代码。基本步骤相同：

- 1. 实现 C 源代码
- 2. 头文件文档
- 3. 空 main() 函数
- 4. 调用 embInitPV
- 5. 用于处理 ACD 数据项的变量
- 6. 调用 ajAcdGet* 以检索 ACD 值
- 7. 清理 ACD 变量的代码。

对于移植，需要考虑的事情要多得多。main() 函数需要重写以处理 ACD 文件处理，如下所示：



- 1. 添加代码，从 ACD 文件处理中获取应用程序选项，而不是像原始代码那样处理它们
- 2. 识别从用户读取输入的函数，并更新函数调用
- 3. 将输出函数替换为对 EMBOSS 库的适当调用（如果可能）。

您必须识别任何从用户读取输入的函数，然后添加代码从 ACD 文件中获取值，而不是像原始代码那样处理它们。输出可以保留为原始应用程序生成的任何格式。您可以添加代码以使用 EMBOSS 库提供的输出函数。

显然，有必要仔细熟悉第三方源代码。可能需要在多个文件中进行编辑。这是移植软件的主要缺点。

其余部分说明了 ohmmalign 移植所采用的方法。

## 10.10 HMMER 移植

### 10.10.1 HMMER 移植：ohmmalign.acd

ACD 文件基本上与包装器中的相同，只是由于两个版本之间选项的差异而有一些更改。需要指出的一点是输出部分。在移植中，排列输出由 outfile ACD 数据项处理。包装器使用的 align 数据类型在当时不可用。

```
section: output
[
    information: "Output section"
    type: "page"
]

outfile: outfile
[
    parameter: "Y"
    knowntype: "hmmalign output"
]

endsection: output
```

### 10.10.2 HMMER 移植：ohmmalign.c

### 10.10.2.1 标题代码

这显示了 C 源代码的顶部。您可以立即看到，这里是原始 HMMER 代码和针对 EMBOSS 的添加的混合体。例如，EMBOSS 接口在第一个 include 指令之前导入。

```
/******************************
* HMMER - Biological sequence analysis with profile HMMs
* Copyright (C) 1992-1998 Washington University School of Medicine
* All Rights Reserved
*
* This source code is distributed under the terms of the
* GNU General Public License. See the files COPYING and LICENSE
* for details.
***********************************************************************/
/* hmmalign.c
* SRE, Thu Dec 18 16:05:29 1997 [St. Louis]
*
* main() for aligning a set of sequences to an HMM.
* RCS $Id: DevWrappingPorting.xml,v 1.30 2010/07/08 14:21:05 jonsourceforge Exp $
* Modified for EMBOSS by Alan Bleasby (ISMB 2001)
*/
#include "emboss.h"
#include <stdio.h>
#include <stdlib.h>

#include "structs.h"       /* data structures, macros, #define's */
#include "config.h"        /* compile-time configuration constants */
#include "funcs.h"         /* function declarations */
#include "globals.h"       /* alphabet global variables */
#include "squid.h"         /* general sequence analysis library */

#ifdef MEMDEBUG
#include "dbmalloc.h"
#endif

extern void emboss_rseqs(AjPSeqset seqset, char ***ret_rseqs,SQINFO **ret_sqinfo,int *ret_num);

static void include_alignment(char *seqfile, struct plan7_s *hmm, int do_mapped,
char ***rseq, char ***dsq, SQINFO
**sqinfo, struct p7trace_s ***tr, int *nseq);
```

### 10.10.2.2 main() 函数变量声明

此处显示了 main() 函数和变量声明。在尽可能保持原始代码不变的同时，有必要添加 AJAX 特定类型的变量来保存从 ACD 文件中检索的值。这些变量与之前一样设置为 NULL。

```
int main(int argc, char **argv)
{
const char *hmmfile;       /* file to read HMMs from */
HMMFILE *hmmfp;            /* opened hmmfile for reading */
const char *seqfile;       /* file to read target sequence from */
char **rseq;               /* raw, unaligned sequences */
SQINFO *sqinfo;            /* info associated with sequences */
char **dsq;                /* digitized raw sequences */
int nseq;                  /* number of sequences */
char **aseq;               /* aligned sequences */
AINFO ainfo;               /* alignment information */
float *wgt;                /* per-sequence weights */
int i;
struct plan7_s *hmm;       /* HMM to align to */
struct p7trace_s **tr;     /* traces for aligned sequences */
int be_quiet; /* TRUE to suppress verbose banner */
int matchonly; /* TRUE to show only match state syms */
const char *outfile; /* optional alignment output file */
FILE *ofp; /* handle on alignment output file */
AjPFile ajwithali; /* name of additional alignment file to align */
AjPFile ajmapali; /* name of additional alignment file to map */
AjBool ajmap = ajFalse;
AjPFile outf = NULL;
AjPStr outfname = NULL;
AjPFile inf = NULL;
AjPStr infname = NULL;
AjPSeqset seqset = NULL;
AjPStr ajseqfile = NULL;
char* mapali = NULL;
char* withali = NULL;
```

### 10.10.2.3 ACD 文件处理

这显示了从 ACD 检索值的代码。为此需要一些管家变量。mapali 和 withali 是 C 类型字符串（char *），用于保存 EMBOSS 输入文件的名称。名称通过调用 ajFileGetNameS 检索。然后关闭文件，使其准备好供 HMMER 使用。其他 HMMER 输入和输出文件也做了类似的操作：

```
/**********************************************************************/
* Parse command line
**********************************************************************/
matchonly = FALSE;
outfile = NULL;
be_quiet = FALSE;
withali = NULL;
mapali = NULL;

embInitP("ohmmalign",argc,argv,"HMMER");

ajmatch = ajAcdGetBoolean("matchonly");

if(ajmatch)
    matchonly=TRUE;
else
    matchonly=FALSE;

ajmapali = ajAcdGetInfile("mapalifile");

if (ajmapali)
    mapali = ajCharNewS(ajFileGetNameS(ajmapali));

ajFileClose(&ajmapali);
ajwithali = ajAcdGetInfile("withalifile");

if (ajwithali)
    withali = ajCharNewS(ajFileGetNameS(ajwithali));

ajFileClose(&ajwithali);

be_quiet=TRUE;

outf = ajAcdGetOutfile("outfile");
outfname = ajStrNewC((char *)ajFileGetNameC(outf));

if(*ajStrGetPtr(outfname)>31)
    ajFileClose(&outf);
outfile = ajStrGetPtr(outfname);

inf = ajAcdGetInfile("hmmfile");
infname = ajStrNewC((char *)ajFileGetNameC(inf));
ajFileClose(&inf);
hmmfile = ajStrGetPtr(infname);

seqset = ajAcdGetSeqset("sequences");
ajseqfile = ajStrNewC(ajStrGetPtr(seqset->Filename));
seqfile = ajStrGetPtr(ajseqfile);
```

### 10.10.2.4 处理输入数据

此处是管理数据输入的代码。您可以看到，用于保存 ACD 值的管家变量被传递到 HMMER 函数中。这里需要指出的唯一一点是，异常处理是通过调用 EMBOSS 函数 ajFatal 来处理的。显然，在编写移植时，有必要通读原始源代码：

```
/**********************************************************************
* Open HMM file (might be in HMMERDB or current directory).
* Read a single HMM from it.
*
* Currently hmmalign disallows the J state and
* only allows one domain per sequence. To preserve
* the S/W entry information, the J state is explicitly
* disallowed, rather than calling a Plan7*Config() function.
* this is a workaround in 2.1 for the 2.0.x "yo!" bug.
**********************************************************************/
if ((hmmfp = HMMFileOpen(hmmfile, "HMMERDB")) == NULL)
    ajFatal("Failed to open HMM file %s\n", hmmfile);

if (!HMMFileRead(hmmfp, &hmm))
    ajFatal("Failed to read any HMMs from %s\n", hmmfile);

HMMFileClose(hmmfp);

if (hmm == NULL)
    ajFatal("HMM file %s corrupt or in incorrect format? Parse failed", hmmfile);

hmm->xt[XTE] [MOVE] = 1.;    /* only 1 domain/sequence ("global" alignment)
/*hmm->xt[XTE] [LOOP] = 0.; */
P7Logoddssify(hmm, TRUE);

/* do we have the map we might need? */
if (mapali != NULL && ! (hmm->flags & PLAN7_MAP))
    ajFatal("HMMER: HMM file %s has no map; you can't use -mapali.", hmmfile);

/**********************************************************************
* Open sequence file in current directory.
* Read all seqs from it.
**********************************************************************/





## 10.10.2.5 干净退出

然后有大量未显示的本机代码。最后，程序必须通过调用 embExit() 来退出：

```
if (outfile != NULL && (ofp = fopen(outfile, "w")) != NULL)
{
WriteSELEX(ofp, aseq, &ainfo, 50);
printf("Alignment saved in file %s\n", outfile);
fclose(ofp);
}
else
WriteSELEX(stdout, aseq, &ainfo, 50);

/********************************************************************
* Cleanup and exit
********************************************************************/
for (i = 0; i < nseq; i++)
{
P7FreeTrace(tr[i]);
FreeSequence(rseq[i], &(sQinfo[i]));
free(dsq[i]);
}

FreeAlignment(aseq, &ainfo);
FreePlan7(hmm);
free(sQinfo);
free(rseq);
free(dsq);
free(wgt);
free(tr);

SqdClean();

ajStrDel(&outfname);
ajStrDel(&infname);
ajStrDel(&ajseqfile);

#ifdef MEMDEBUG
current_size = malloc_inuse(&histid2);
if (current_size != orig_size) malloc_list(2, histid1, histid2);
else fprintf(stderr, "[No memory leaks.]\n");
#endif
```

```
embExit();
return 0;
}
```

## 10.11 总结

将第三方应用程序集成到 EMBOSS 中需要大量工作，无论应用程序是被包装还是移植。不过，这项工作非常值得，因为在分发方面（软件将触达更多用户）以及在某些情况下，培训、支持和维护成本会降低。此外，任何集成的软件都可以使用 EMBOSS 的内置功能，例如对常见序列格式的支持，并将集成到众多可用的 EMBOSS 接口中。这些接口包括图形用户界面、工作流软件和 Web 服务。

完全移植的软件提供最大的灵活性，但这伴随着相对较高的维护成本。尽管如此，当代码将被 EMBOSS 本质上采纳时，这是首选路径。通过使用临时文件，包装器中也可以实现或多或少相同的灵活性，尽管这种方法有缺点和潜在的复杂性。例如，需要用于相互转换文件格式的代码。

# 附录 A ACD 语法参考

### A.1 ACD 语法简介

#### A.1.1 一般语法

Ajax 命令定义（ACD）语言专为编写 EMBOSS 应用程序的 ACD 文件而设计。ACD 语法允许对应用程序的参数及其命令行界面进行非常灵活的描述。它可以指定命令行或其他界面（例如网页）上可以出现的所有内容。

ACD 文件是纯 ASCII 文本文件，*必须*具有 .acd 扩展名。通常它们与应用程序同名，但这不是强制性的。

##### A.1.1.1 空白字符

在解析 ACD 文件时，整个文件内容实际上被视为一个字符串，并被解析为由 *空格* 字符分隔的标记。各个标记之间需要一个空格：多余的空白字符将被忽略。

##### A.1.1.2 注释

可以添加注释行，注释行以 “#” 开头，并持续到行尾。

### A.1.2 ACD 定义

ACD 文件包含一个 *应用程序定义* 和每个参数的 *数据定义*。先给出应用程序定义，然后是数据定义。数据定义组织成各个部分（第 A.1.6 节，‘ACD 文件部分’）。

应用程序和数据定义具有以下一般形式：一个文本标记，后跟冒号 ‘:’（或 ‘=’）和一个空格，然后是第二个标记。定义体紧随其后，由一个或多个属性组成，这些属性由强制的一对方括号 [ ] 分隔，可以跨多行。每个属性都是一个 *名称*: *值* 对，属性值放在引号（“ ”）中：

或者：

```
token: token
{
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
}
```

或：

```
token=token
[
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
]
```

第一个标记要么是 application:（用于应用程序定义），要么是数据定义的 AJAX 数据类型（例如 sequence）。第二个标记要么是应用程序的名称（例如 secret），要么是参数的名称（例如 asequence）。

应用程序定义：

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

数据定义：

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

应用程序标记以及数据类型和属性名称的标记可以缩写，直到不再产生歧义为止。不过，不推荐这种缩写，因为它们往往会使 ACD 文件更难以阅读。

属性值通常用双引号括起来，但这仅对包含空白字符的值（通常是字符串）是强制性的。

### A.1.2.1 应用程序定义

应用程序定义必须是文件中的第一个定义：

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

应用程序名称是任意的，但通常与 ACD 文件名相同。应用程序 C 源代码中用于将其与 ACD 文件关联的是 ACD 文件名（如果不同，则不是 ApplicationName）。这样，可以为单个应用程序 C 源代码文件开发多个 ACD 文件（因此也有多个命令行界面）。

有关可用应用程序属性的完整描述，请参见第 A.3 节 ‘应用程序属性’。

### A.1.2.2 数据定义

所有应用程序参数都必须有数据定义。数据定义紧随应用程序定义之后，并且必须放在适当的文件部分中（第 A.1.6 节，‘ACD 文件部分’）：

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

Datatype 必须是有效的 ACD 数据类型（参见第 A.2 节，‘数据类型’）。

ParameterName 是参数的名称。它是一个必须符合某些约定的字符串（第 A.1 节，‘ACD 语法简介’）。此名称用于从命令行和 C 源代码中引用数据定义（参见第 6.3 节，‘处理 ACD 文件’）。

有关可用属性的完整描述，请参见：第 A.4 节 (‘全局属性’)、第 A.5 节 (‘特定于数据类型的属性’) 和第 A.6 节 (‘计算属性’)。

### A.1.3 参数命名约定

#### A.1.3.1 一般约定

参数和限定符名称：

- 不得包含空白字符
- 通常不应为单个字符
- 应尽可能是有意义的单词，并指示选项的功能
- 不区分大小写。

#### A.1.3.2 特定于数据类型的约定

参数名称的一些约定适用于单个数据类型。在 ACD 文件中指定多个同一数据类型的实例时，可以将字符 a、b 等追加到标志：asequence、bsequence 等。这在表中通过参数名称中的星号表示，例如 *sequence。

| 数据类型 | 名称 | 用途 |
|---|---|---|
| sequence | sequence, *sequence | 主要输入序列，通常是必需的 |
| seqall | sequence, *sequence, seqall | 主要输入序列数据库，通常是必需的 |

### A.1 ACD 语法简介

| 参数 | 类型/名称 | 描述 |
| :--- | :--- | :--- |
| seqset | sequence, *sequence, sequences | 主要输入序列，通常是必需的 |
| seqsetall | sequence, *sequence, sequences | 主要输入序列，通常是必需的 |
| seqout, seqoutset, seqoutall | outseq, *outseq, *outfile | 主要输出序列，通常是必需的，通常应默认为主要输入序列名称，扩展名默认为输出序列格式的名称 |
| outfile | outfile, *file | 主要输出非序列结果文件，通常是必需的。文件扩展名应允许默认为应用程序名称。outfile 应用于第一个输出文件。outfile 或 *file 可用于第二个及后续输出文件 |
| report | outfile, *file | 报告输出文件。outfile 应用于第一个报告文件。outfile 或 *file 可用于第二个及后续报告文件 |
| align | outfile, *file | 比对输出文件。outfile 应用于第一个输出比对。outfile 或 *file 可用于第二个及后续输出比对 |
| infile | infile, *file | 主要输入非序列文件 |
| infile | data | 主要辅助输入数据文件，通常是可选的 |
| infile | patterns | 用于在序列中搜索的模式文件 |
| integer | minlen | 要查找的序列特征的最小长度 |
| integer | maxlen | 要查找的序列特征的最大长度 |
| integer | wordsize | 用于哈希表等的字长。通常最小值 = 2（蛋白质），4（DNA） |
| integer | window | 用于计算点图、特征等的窗口长度 |
| integer | shift | 每次迭代中窗口移动的量 |
| boolean | consensus | 是否应输出共识序列的标志 |
| float | gap | 间隙罚分 |





| 数据类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| 浮点数 | gapext | 间隙延伸惩罚 |
| 整数 | from | 指定操作（例如删除）的输入序列起始位置，默认为序列起始位置，最小值 = 1，最大值 = <序列长度> |
| 整数 | to | 指定操作（例如删除）的输入序列结束位置，默认为 from 值，最小值 = from 值，最大值 = <序列长度> |
| 浮点数或整数 | threshold | 各种操作的阈值 |
| 布尔值 | left | 操作应在序列起始处执行 |
| 布尔值 | right | 操作应在序列结束处执行 |
| 字符串 | pattern | 在序列中搜索的模式 |
| 图形 | graph | 图形输出 |
| xygraph | graph | 图形输出 |
| 目录 | directory, *dir, *path | 文件目录 |
| outdir | outdir, *outdir | 文件输出目录 |
| dirlist | directory | 文件目录 |
| filelist | *files | 文件列表 |
| 矩阵 | matrix | 矩阵 |
| 数据文件 | datafile | 数据文件 |
| 特征 | feature, *feature | 特征输入 |
| featout | outfeat, *outfeat | 特征输出 |
| regexp | pattern | 正则表达式 |

#### A.1.3.3 验证的参数名

对于某些数据类型，约定被更严格地强制执行：如果在 ACD 处理过程中未为以下数据类型使用标准名称，将生成警告：

- 序列输入（类型为 `sequence`、`seqall`、`seqsetall` 或 `seqset` 的任何数据定义）和序列输出（`seqout`、`seqoutall` 和 `seqoutset` 数据类型）
- 特征输入（类型为 `feature` 的任何数据定义）和特征输出（`featout` 数据类型）
- 比对（`align` 数据类型）
- 文件输入和输出（类型为 `infile`、`filelist`、`directory`、`dirlist` 或 `outfile` 的任何数据定义）

### A.1.4 属性类型

应用程序属性可为应用程序定义定义（第 A.3 节，“应用程序属性”）。

可为数据定义定义三种基本类型的属性：

- 全局属性（第 A.4 节，“全局属性”）
- 特定于数据类型的属性（第 A.5 节，“特定于数据类型的属性”）
- 计算属性（第 A.6 节，“计算属性”）。

此外，某些 ACD 数据类型内置了各种“数据类型关联”命令行限定符（或简称为“关联限定符”），也可以在相应的数据定义中定义为属性。这些在数据类型描述（第 A.2 节，“数据类型”）中列出。

### A.1.5 参数和限定符

ACD 文件中的每个数据定义都可以通过适当的属性定义为以下之一：

- 参数
- 标准限定符
- 其他限定符

默认值为：

- 高级限定符。

它们在提示方式、命令行上如何指定以及是否显示帮助信息方面有所不同。

下表总结了此行为。‘Flag’ 表示是否必须在命令行上给出标志（参数或限定符名称）。‘Prompt’ 表示如果未在命令行上指定值，是否会提示输入值。只有在指定 -options 时，才会提示输入其他限定符。‘Help’ 表示显示内置 -help 限定符的信息位置。有关更多信息，请参见第 4.5 节，“控制提示”。

| 类型 | 属性 | 标志 | 提示 | 帮助 |
|---|---|---|---|---|
| 参数 | parameter: "y" | 否 | 是 | 必需部分 |
| 标准 | standard: "y" | 是 | 是 | 必需部分 |
| 其他 | additional: "y" | 是 | 是（与 -options 一起）或 否（需要默认值） | 高级部分 |
| 高级（默认） | 不需要属性 | 是 | 否 | 高级部分 |

### A.1.6 ACD 文件节

ACD 文件中的任何数据定义 *必须* 包含在适当的节中，并按正确顺序给出。节必须按以下顺序出现：

- 输入
- 必需
- 其他
- 高级
- 输出

也可以定义带有任意名称的子节。它们可以以任何顺序出现，但必须嵌套在主节中。

节和子节具有以下一般语法：

```
section: SectionName
[
   information: "SectionName section"
   type: "page"
]
.
   (data definitions go here)
.
   section: NestedSectionName
[
   information: "NestedSectionName section"
   type: "page"
]
.
   (data definitions go here)
.
   endsection: NestedSectionName
.
endsection: SectionName
```

例如：

```
section: input
[
   information: "Input section"
   type: "page"
]
.
   (input data definitions go here)
.
   section: inputsubSection
[
   information: "Input sub-section"
   type: "page"
]
.
   (input sub-Section data definitions go here)
.
endsection: inputsubsection
endsection: input
```

### A.1.6.1 节的验证

节的顺序以及哪些数据定义可以出现在哪些节中的限制在 EMBOSS 系统文件 sections.standard 中定义（参见第 4.1 节，“ACD 文件开发简介”）。这些限制在 ACD 处理期间强制执行，并在以下情况下生成错误：

- 如果主节出现顺序错误
- 如果子节出现在错误的主节中
- 如果参数（带有 parameter: "Y" 属性的数据定义）或标准限定符（standard: "Y" 属性）出现在“高级”或“其他”节中
- 如果其他限定符（additional: "Y" 属性）出现在“高级”或“必需”节中
- 如果高级限定符（没有 parameter: "Y"、standard: "Y" 或 additional: "Y" 属性）出现在“其他”或“必需”节中

| 节名称 | 描述 |
| :--- | :--- |
| 输入 | 简单输入值和任何会读取输入的 ACD 类型，包括 infile、sequence、seqset、seqall、matrix、fmatrix 和 codon。任何其他与输入相关的参数和限定符也可以放在此节中。目前 datafile 也包括在内。 |
| 必需 | 参数和标准限定符，包括任何 standard: 属性可以为 true 但取决于条件操作的参数。任何由参数和标准限定符使用的 toggle: 定义。请注意，输入和输出参数及限定符必须位于各自的节中。 |
| 其他 | 其他限定符，包括任何 additional 属性可以为 true 但取决于条件操作的限定符。任何由其他限定符使用的 toggle: 定义。输入和输出参数及限定符必须位于各自的节中。 |
| 高级 | 任何未定义 standard: 或 additional: 属性的限定符（输入和输出限定符除外）。 |
| 输出 | 任何会写入输出的数据类型，包括任何 outfile、outdata、seqout、seqoutall、seqoutset 和 outtree。其他与输出相关的限定符也可以放在此节中。 |

## A.2 数据类型

为方便起见，可用的 ACD 数据类型按反映相似属性或使用模式的五组进行组织，如下所示：

- 简单
- 输入
- 选择
- 输出
- 图形。

可用的数据类型将在下面详细描述。

### A.2.1 简单 ACD 数据类型描述

#### A.2.1.1 array

整数或浮点数的列表。

数据值 数据值是由空格或逗号分隔的数字列表。
例如：

```
"1 2 3 4 5"
"1.5, 2.0, 2.5, 3.0"
```

默认值 默认值使用 default: 全局属性设置。

关键属性 ACD 属性控制验证，例如允许的值数量（size: 属性），或数字列表必须加起来的总值 sumtest:，在一定容差 tolerance: 范围内，仅当布尔属性 sum: 设置时才进行测试。

#### A.2.1.2 boolean

简单布尔值。

数据值 数据值具有“真”或“假”值，可以按以下方式指定：

```
"y"
"yes"
"true"
"N"
"no"
"false"
```





如果参数名在命令行中作为标志输入，则值将为 "Y"，例如 -BooleanOption。如果命令行中没有该限定符，则使用默认值。标志也可以加 no 前缀，例如 -noBooleanOption，以强制值为 "N"。如果默认值为 "Y"，则需要此操作。

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 无。

## A.2.1.3 整数

简单整数。

**数据值** 数据值可以是任何整数值。例如：

```
"100"
```

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 许多应用程序会规定最小值和/或最大值，例如最小值为 0 或 1。允许的值范围由 minimum: 和 maximum: 属性控制。

## A.2.1.4 浮点数

简单浮点数。

**数据值** 数据值可以是任何有效的浮点数。例如：

```
"100.24"
```

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 值范围由 minimum: 和 maximum: 属性控制，最大精度由 precision: 属性控制。

## A.2.1.5 范围

序列位置的范围。

**数据值** 可以在命令行或范围文件中定义一个或多个范围。

在命令行中，范围由一对整数定义，可以给出多个范围。数字可以由任何非数字、非字母字符分隔。例如：

```
"24-45, 56-78"
"1:45, 67=99;765.888"
"1,5,8,10,23,45,57,99"
```

范围文件包含一对数字的列表，可带可选文本注释。每行必须给出一对数字，文件可以包含以 # 字符开头的注释行。例如：

```
# A set of ranges in a range file.
12	23
4	5	This is an optional comment.
67	10348	Another comment.
```

范围文件在命令行中通过在文件名前加 @filename 来指定。例如：

```
@filename RangeFileName
```

在数字为序列位置的情况下，上下界实际上取决于应用它们的序列长度。应牢记序列位置可以是负数，在这种情况下，它们从序列末尾开始倒数。

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 无。

## A.2.1.6 正则表达式

正则表达式模式。

EMBOSS 使用“Perl 兼容正则表达式库”（PCRE）来处理正则表达式。

**数据值** 任何在 Perl 5.0 中有效的正则表达式（http://search.cpan.org ~nwclark/perl-5.8.7/pod/perlre.pod）在此处也应有效。

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 属性提供验证，例如，控制正则表达式的长度（minlength: 和 maxlength 属性）和大小写，可以设置为仅大写（upper: "Y"）或仅小写（lower: "Y"）。

## A.2.1.7 模式

序列模式。

**数据值** 使用氨基酸的标准 IUPAC 一字母代码。符号 x 用于接受任何氨基酸的位置。歧义通过列出给定位置可接受的氨基酸，并用方括号 [ ] 括起来来表示。例如：

```
[ALT]
```

表示 Ala 或 Leu 或 Thr。歧义也通过列出给定位置不可接受的氨基酸，并用一对花括号 { } 括起来来表示。例如：

```
{AM}
```

表示除 Ala 和 Met 以外的任何氨基酸。模式中的每个元素与其邻居之间用短横线 (-) 分隔。模式元素的重复可以通过在该元素后跟一个数值或括号内的数值范围来表示。例如：

```
x (3) corresponds to x-x-x
x (2 , 4) corresponds to x-x or x-x-x or x-x-x-x-x
```

当模式限制在序列的 N 端或 C 端时，该模式要么以 < 符号开头，要么分别以 > 符号结尾。句号结束模式。例如：

```
[DE] (2) HS{P}X(2) PX (2 , 4) C.
```

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 属性提供验证，例如，控制模式的长度（minlength: 和 maxlength 属性）和大小写，可以设置为仅大写（upper: "Y"）或仅小写（lower: "Y"）。模式的类型（核苷酸或蛋白质）可以使用 type: 属性设置。

## A.2.1.8 字符串

简单字符串。

大多数字符串值是自由文本，尽管如果字符串随后被解析，程序可以将字符串用于其他 ACD 数据类型未覆盖的任何输入。

**数据值** 数据值可以是任何有效的 ASCII 文本字符串，应用双引号括起来。例如：

```
"This is a valid text string"
```

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 每当定义字符串数据类型时，应使用 knowntype: 属性为其指定类型，否则在 ACD 处理期间将生成警告消息。

如果需要，可使用 ACD 属性来控制长度或提供正则表达式模式以验证字符串。

## A.2.1.9 切换

用于控制其他参数的简单布尔开关。

toggle 参数的工作方式与 boolean 参数相同，但旨在用于打开或关闭对其他参数的提示（参见第 4.5 节“控制提示”）。通常，这是通过使用计算来确定正在控制的数据定义的 standard: 或 additional: 属性的值来完成的。在这种情况下，toggle 参数用于计算值中，并且即使它们本身未定义为标准限定符（使用 standard: 属性），也可以放置在 ACD 文件的“Required”部分中。

**数据值** 数据值具有“真”或“假”值，可以按以下方式指定：

```
"Y"
"yes"
"true"
"N"
"no"
"false"
```

与 boolean 参数完全相同，如果在命令行中输入了参数的标志（例如 -ToggleOption），则值将为 "Y"。如果命令行中没有该限定符，则值将为默认值。标志也可以加 no 前缀（例如 -noToggleOption）以强制值为 "N"（false）。如果默认值为 "Y"，则需要此操作。

**默认值** 默认值使用 default: 全局属性设置。

**关键属性** 无。

## A.2.2 输入 ACD 数据类型描述

### A.2.2.1 密码子

密码子用法表文件。

密码子用法表文件是 ASCII 文本文件，可以以包括 GCG 在内的多种格式读取。密码子用法文件分布在 EMBOSS 数据目录中。

**数据值** 数据值是 EMBOSS 数据搜索路径中的密码子用法表文件名（参见 EMBOSS 用户指南）。

**默认值** EMBOSS 默认使用 EMBOSS 发行版中提供的人类密码子用法表 Ehum.cut，但通常会被用户覆盖。密码子用法表是物种特定的，在某些情况下特定于物体内的一类基因，因此能够按应用程序特定基础设置密码子用法表很有用。默认值使用 default: 全局属性设置。

**关键属性** 无。

### A.2.2.2 cpdb

CCF（干净坐标文件）格式的蛋白质坐标数据。
CCF 格式是一种用于蛋白质和域坐标数据的简单“干净”文件格式。请参阅 pdbparse 的文档，它是 EMBOSS domainatrix 包的一部分，可从 PDB 文件输入生成 CCF 文件。

**数据值** 数据值是 CCF 文件名。

**默认值** 默认值使用 `default:` 全局属性设置。
内部定义了默认值 ("lazu")，但通常不适合使用它。

**关键属性** 无。

### A.2.2.3 datafile

从标准 EMBOSS 数据搜索路径读取的格式化数据文件（参见 EMBOSS 用户指南）。

许多数据文件已有自己的 ACD 数据类型，例如 matrix、matrixf 和 codon。其他数据文件没有或不需要自己的 ACD 定义，datafile 用于这些文件。

**数据值** 数据值是 EMBOSS 数据搜索路径中的数据文件名（参见 EMBOSS 用户指南）。

**默认值** 默认值使用 `default:` 全局属性设置。
默认数据文件名也可以由两个 ACD 属性定义，用于文件基本名（`name:`）和文件扩展名（`extension:`）。

**关键属性** 数据文件通常具有硬编码文件名。您可以自由使用 `name:` 来覆盖该名称。

### A.2.2.4 directory

可用于输入或输出的目录。

**数据值** 数据值可以是任何有效目录的名称。例如：

```
"."
"/data"
"/data/sequences"
```

**默认值** 默认值使用 `default:` 全局属性设置。

**关键属性** 属性对用户输入提供额外验证。

### A.2.2.5 dirlist

从目录读取的文件名列表。

**数据值** 数据值可以是任何有效目录的名称。例如：




```
", "
"/data"
"/data/sequences"
```

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性对用户输入提供额外验证。

文件中的数据类型可以通过为 `knowntype :` 属性指定值来识别。这允许将输入与输出匹配，前提是 `knowntype :` 属性已设置，例如，对于 `outfile` 定义。

## A.2.2.6 `discretestates`

离散状态文件。

`discretestates` 是为 **phylipnew** EMBASSY 包实现的。
`discretestates` 输入由 **phylip** 的“离散字符”应用程序使用。
`discretestates` 可以在 GUI 中被一个简单的输入文件替代，用户需要提供正确的数据格式。

**数据值** 数据值是 **phylip** “离散状态”文件的名称。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性提供详细的类型检查，并可以自动检测和验证 **phylip** 支持的各种替代格式，而无需复杂的额外命令行选项。

## A.2.2.7 `distances`

距离矩阵。

`distances` 特定于 **phylipnew** EMBASSY 包。`distances` 输入由 **phylip** 的“距离矩阵”应用程序使用。

距离矩阵数据类型可以在 GUI 中被一个简单的输入文件替代，用户需要提供正确的数据格式。

**数据值** 数据值是距离矩阵文件的名称。接受的文件格式包括 **phylip** 读取的所有格式，并支持自动相互转换。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性提供详细的类型检查，并可以自动检测和验证 **phylip** 支持的各种替代格式，而无需复杂的额外命令行选项。

## A.2.2.8 `features`

任何已知特征格式的序列特征注释。

**数据值** 数据值是特征文件的名称。特征文件包含序列特征信息。支持多种特征格式（请参阅 _EMBOSS 用户指南_）。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 可以通过设置 `type :` 属性来限制特征类型，例如，使程序仅接受 DNA 特征。特征类型必须是蛋白质或核苷酸之一。有一个基于输入序列类型（如果使用）的默认值，但应指定一个值，以便应用程序可以验证输入是指定的类型。如果未为输入特征指定类型，并且没有可用于获取默认类型的序列输入，则在 ACD 处理期间将生成错误。

如果设置了它们的 `features :` 属性，特征也可以从输入序列（sequence、seqall、seqset 和 seqsetall 数据类型）中读取，并与输出序列（seqout、seqoutall 和 seqoutset 数据类型）一起写入。

## A.2.2.9 `filelist`

输入文件列表。

**数据值** 数据值是用逗号分隔的文件名列表。例如：

```
"../data/file1.dat, file2.dat"
```

Filelist 等效于 infile 数据类型，但允许用户指定一个或多个输入文件。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性对用户输入提供额外验证。可以通过为 `knowntype :` 属性指定值来识别数据类型。这允许将输入与输出匹配，前提是 `knowntype :` 属性已设置，例如，对于 outfile 定义。

## A.2.2.10 `frequencies`

频率值。

frequencies 特定于 phylipnew EMBASSY 包，并由 phylip 的“基因频率和连续字符”应用程序使用。

frequencies 数据类型可以在 GUI 中被一个简单的输入文件替代，用户需要提供正确的数据格式。

**数据值** 数据值是频率文件的名称。接受的文件格式包括 phylip 读取的所有格式，并支持自动相互转换。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性提供详细的类型检查，并可以自动检测和验证 phylip 支持的各种替代格式，而无需复杂的额外命令行选项。

## A.2.2.11 `infile`

通用输入文件。

infile 用于其他 ACD 数据类型未涵盖的数据文件。例如，infile 通常不包含序列数据。

**数据值** 数据值是输入文件的名称。

例如：

```
"data.in"
"/data/infile.1"
```

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 可以通过为 `knowntype :` 属性指定值来识别数据类型。这允许将输入与输出匹配，前提是 `outfile` 定义中也设置了 `knowntype :` 属性。可以通过环境变量使用 `directory:` 指定包含文件的目录。

## A.2.2.12 `matrix`

比较矩阵文件（整数值）。

这些通常是氨基酸或核苷酸替换矩阵。与 BLAST 分发的矩阵文件也在 EMBOSS 数据目录中与 EMBOSS 一起分发。`matrix` 数据类型定义整数矩阵，通常比浮点矩阵更快。如果需要，可使用浮点矩阵（`matrixf` 数据类型），整数矩阵文件当然也可以作为浮点数读取。通常，在指定比较矩阵时，还需要间隙罚分。这些必须在一个或多个其他数据定义中单独指定。

**数据值** 数据值是 EMBOSS 数据搜索路径中的整数比较矩阵文件的名称（请参阅 _EMBOSS 用户指南_）。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** `matrix` 数据类型的属性定义特征，并允许验证生物数据的整数矩阵。matrix 数据类型具有一个 `protein:` 属性，用于强制选择核酸或蛋白质比较矩阵。在 ACD 文件中，输入序列的类型通常用于设置矩阵类型。

## A.2.2.13 `matrixf`

比较矩阵文件（浮点值）。

`matrixf` 数据类型定义浮点矩阵，通常比浮点矩阵更慢。整数矩阵文件当然也可以作为浮点数读取。这些通常是氨基酸或核苷酸替换矩阵。与 BLAST 分发的矩阵文件也在 EMBOSS 数据目录中与 EMBOSS 一起分发。通常，在指定比较矩阵时，还需要间隙罚分。这些必须在一个或多个其他数据定义中单独指定。

**数据值** 数据值是 EMBOSS 数据搜索路径中的浮点比较矩阵文件的名称（请参阅 _EMBOSS 用户指南_）。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** matrixf 数据类型的属性定义特征，并允许验证生物数据的浮点数矩阵。matrixf 数据类型具有一个 protein: 属性，用于强制选择核酸或蛋白质比较矩阵。在 ACD 文件中，输入序列的类型通常用于设置矩阵类型。

## A.2.2.14 `properties`

属性值。

properties 特定于 phylipnew EMBASSY 包。Properties 输入由 phylip 应用程序用于定义权重、祖先状态和因子（多态字符）。

properties 数据类型可以在 GUI 中被一个简单的输入文件替代，用户需要提供正确的数据格式。

**数据值** 数据值是 properties 文件的名称。接受的格式包括 phylip 读取的所有格式，并支持自动相互转换。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 这些属性提供详细的类型检查，并可以自动检测和验证 phylip 支持的各种替代格式，而无需复杂的额外命令行选项。

## A.2.2.15 `scop`

DCF（域分类文件）格式的 SCOP 和 CATH 域分类数据。DCF（域分类文件）格式是域分类数据的简单“干净”文件格式。请参阅 domainainer 的文档，它是 EMBASSY domainamatrix 包的一部分，可从 SCOP 和 CATH 文件输入生成 DCF 文件。

**数据值** 数据值是 DCF 文件的名称。

**默认值** 默认值是使用 `default :` 全局属性设置的。

域分类文件输入有一个内部定义的默认值 ("d3sdha")，虽然通常不适合使用此默认值。

**关键属性** 无。

## A.2.2.16 `sequence`

用于读取的单个序列。

**数据值** 数据值是单个序列的 USA（请参阅 _EMBOSS 用户指南_）。例如，USA 可能是数据库引用或文件。

**默认值** 默认值是使用 `default :` 全局属性设置的。

**关键属性** 可以通过设置 `type :` 属性来限制序列类型，例如，使程序仅接受 DNA 序列。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。如果设置了 `features :` ACD 属性，可以读取序列特征（第 6.9 节，“处理特征”）。





### A.2.2.17 seqall

一组单个序列，逐个寻址。

**数据值** 数据值是一组单个序列的USA。例如，USA（参见EMBOSS用户指南）可能指定用于顺序读取条目的序列数据库。

**默认值** 使用default:全局属性设置默认值。

**关键属性** 通过设置type:属性可以限制序列类型，例如，使程序仅接受DNA序列。序列类型必须是标准序列类型（第A.7节，“序列类型”）。如果设置了features: ACD属性，可以读取序列特征（第6.9节，“处理特征”）。

### A.2.2.18 seqset

一组可以同时使用的单个序列。

**数据值** 数据值是一组单个序列的USA（参见EMBOSS用户指南）。例如，来自多重比对文件的序列集，或来自数据库的序列。

**默认值** 使用default:全局属性设置默认值。

**关键属性** 通过设置type:属性可以限制序列类型，例如，使程序仅接受DNA序列。序列类型必须是标准序列类型（第A.7节，“序列类型”）。如果设置了features: ACD属性，可以读取序列特征（第6.9节，“处理特征”）。

aligned:属性必须设置：否则在ACD处理期间将生成错误。

### A.2.2.19 seqsetall

一个或多个可以同时使用的单个序列集。

**数据值** 数据值是一个或多个单个序列集的USA（参见EMBOSS用户指南）。例如，来自两个数据库或两个比对文件的序列集。数据值通常是一个“列表文件”（包含USA列表的文件）。

**默认值** 使用default:全局属性设置默认值。

**关键属性** 通过设置type:属性可以限制序列类型，例如，使程序仅接受DNA序列。序列类型必须是标准序列类型（第A.7节，“序列类型”）。如果设置了features: ACD属性，可以读取序列特征（第6.9节，“处理特征”）。aligned:属性必须设置：否则在ACD处理期间将生成错误。

### A.2.2.20 tree

系统发育树。

tree数据类型特定于phylipnew包。phylip应用程序使用树输入来定义一个或多个系统发育树。

在GUI中，tree数据类型可以由简单的输入文件替换，用户需要提供正确的数据格式。

树目前由phylip本身解析，但未来可能会实现本地解析方法。

**数据值** 数据值是树文件的名称。接受的格式包括phylip读取的所有格式，并自动相互转换。

**默认值** 使用default:全局属性设置默认值。

**关键属性** 属性提供详细的类型检查，并可以自动检测和验证phylip支持的各种替代格式，而无需复杂的额外命令行选项。

## A.2.3 输出ACD数据类型描述

### A.2.3.1 align

序列比对的输出文件。

数据作为序列存储，支持所有常见的比对格式（参见EMBOSS用户指南）。

**数据值** 数据值是任何有效的文件名。

**默认值** 如果指定了数据类型特定的限定词-aname和-aextension，将构建格式为name.extension的比对文件名。值可以使用相应的aname:和 aextension:属性硬编码。通过定义default:全局属性也会设置默认值。

**关键属性** 比对输出文件的定义方式与普通输出文件（outfile数据类型）相同，但具有额外的限定词，以允许选择比对格式，并具有属性来指定比对是否包含两个或多个序列（这限制了可能的格式）。如果输出可以包含来自同一输入的多个比对，则应将multiple:布尔属性设置为“Y”。输出格式通常在命令行上设置，但可以使用aformat:属性硬编码默认值。

### A.2.3.2 featout

序列特征注释的输出文件。

数据作为特征表存储，支持大多数常见的序列特征格式（参见EMBOSS用户指南）。

**数据值** 数据值是任何有效的文件名。

**默认值** 输出文件名的格式为name.extension，并从name:和 extension:属性构建（由-ofname和 oformat内置命令行限定词覆盖（参见*EMBOSS用户指南*）。如果ACD文件中未定义`name:`属性，它将默认为读取的*第一个*序列的计算属性`name:`。如果序列参数名为`asequence`，则获取此值的ACD操作是`$(asequence.name)`。`extension:`属性将默认为输出特征格式，例如`.gff`。

通过定义`default:`全局属性也会设置默认值。

**关键属性** 如果设置了`features:`属性，可以从输入序列（`sequence`、`seqall`、`seqset`和`seqsetall`数据类型）读取特征，并将其与输出序列（`seqout`、`seqoutall`和`seqoutset`数据类型）一起写入。

默认情况下，输出特征使用GFF格式。格式通常在命令行上设置，但可以使用`oformat:`属性硬编码默认值。

通过设置`type:`属性可以限制特征类型，例如，使程序仅接受DNA特征。特征类型必须是`protein`或`nucleotide`之一。

有一个基于输入序列类型（如果使用）的默认值，但应指定一个值，以便应用程序可以验证输入是否为指定类型。如果未为输入特征指定类型，并且没有可用于获取默认类型的序列输入，则在ACD处理期间将生成错误。

### A.2.3.3 outcodon

密码子使用数据的输出文件。

**数据值** 数据值是任何有效的文件名。数据作为密码子使用表存储。密码子使用表文件是ASCII文本文件，可以以多种格式读取（参见*EMBOSS用户指南*）。

**默认值** 输出文件名的格式为`name.extension`，并从`name:`和`extension:`属性构建。`name:`属性将默认为`outfile`。`extension:`属性将默认为格式，其中`cut`被定义为默认格式以匹配常见的密码子使用文件命名约定。此格式也称为*EMBOSS密码子格式*。通过定义`default:`全局属性也会设置默认值。

**关键属性** 默认数据格式可以通过`oformat:`属性指定，该属性可由关联的`-oformat`限定词覆盖。

### A.2.3.4 outcpdb

CCF（干净坐标文件）格式的蛋白质坐标数据的输出文件。

CCF（干净坐标文件）格式是一种用于蛋白质和域坐标数据的简单“干净”文件格式。有关文档，请参见**pdbparse**，它是EMBASSY **domainatrix**包的一部分，可从PDB文件输入生成CCF文件。

**数据值** 数据值是任何有效的文件名。

**默认值** 使用`default:`全局属性设置默认值。

**关键属性** 默认数据格式可以通过`oformat:`属性指定，该属性可由关联的`-oformat`限定词覆盖。

### A.2.3.5 outdata

格式整齐的表格或列表数据的输出文件。

ACD文件中多个outdata定义对应的输出将追加到单个文件中。各个ACD定义允许定义每个文件部分的格式。

**数据值** 数据值是任何有效的文件名。

**默认值** 使用`default:`全局属性设置默认值。

**关键属性** 默认数据格式可以通过`oformat:`属性指定，该属性可由关联的`-oformat`限定词覆盖。

### A.2.3.6 outdir

用于写入多个输出文件的输出目录。

**数据值** 数据值是任何有效目录的名称。

例如：

```
"."
"/data"
"/data/sequences"
```

**默认值** 使用`default:`全局属性设置默认值。

**关键属性** 可以使用`extension:`属性设置默认文件扩展名。

### A.2.3.7 outdiscrete

系统发育离散特征数据的输出文件。

**数据值** 数据值是任何有效的文件名。

**默认值** 使用`default:`全局属性设置默认值。

**关键属性** 默认数据格式可以通过`oformat:`属性指定，该属性可由关联的`-oformat`限定词覆盖。

### A.2.3.8 outdistance

系统发育距离矩阵数据的输出文件。

**数据值** 数据值是任何有效的文件名。

**默认值** 使用`default:`全局属性设置默认值。

**关键属性** 默认数据格式可以通过`oformat:`属性指定，该属性可由关联的`-oformat`限定词覆盖。

### A.2.3.9 outfile

通用输出文件。





outfile 用于其他输出 ACD 数据类型未涵盖的数据。它适用于以纯文本形式进行通用应用程序输出。例如，输出文件通常不包含序列数据。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。`extension:` 属性将默认为程序名称，通常保留为默认值。

还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 数据类型可通过 `knowntype:` 属性进行标识，并与 `infile` 数据定义的标准类型匹配，以供另一个程序用作输入。标准 EMBOSS 已知类型在其他地方有描述（第 4.3 节，“数据定义”）。

### A.2.3.10 outfileall

多个通用输出文件。

outfileall 用于其他输出 ACD 数据类型未涵盖的数据。它适用于以纯文本形式进行通用应用程序输出。例如，输出文件通常不包含序列数据。

**数据值** 数据值是输出文件的基本文件名。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。`extension:` 属性将默认为程序名称，通常保留为默认值。

还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 数据类型可通过 `knowntype:` 属性标识为标准类型（第 A.4 节，“全局属性”）。该类型可以与 `infile` 数据定义的类型匹配，以供另一个程序用作输入。

### A.2.3.11 outfreq

系统发生学字符频率数据的输出文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 使用 `default:` 全局属性设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.12 outmatrix

整数比较矩阵数据的输出文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 使用 `default:` 全局属性设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.13 outmatrixf

浮点比较矩阵数据的输出文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 使用 `default:` 全局属性设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.14 outproperties

系统发生学属性数据的输出文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 使用 `default:` 全局属性设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.15 outscop

SCOP 和 CATH 域分类信息的 DCF（域分类文件）格式输出文件。

DCF（域分类文件）格式是一种用于域分类数据的简单‘干净’文件格式。请参阅 **domainner** 的文档，它是 EMBASSY **domainmatrix** 包的一部分，该工具可从 SCOP 和 CATH 文件输入生成 DCF 文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 使用 `default:` 全局属性设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.16 outtree

系统发生树数据的输出文件。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。`extension:` 属性将默认为输出文件格式，通常保留为默认值。还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 默认数据格式可通过 `oformat:` 属性指定，该属性可由 `-oformat` 关联限定符覆盖。

### A.2.3.17 report

序列注释的输出文件。

报告数据在内部作为特征表存储，因此支持的格式（请参阅 _EMBOSS 用户指南_）包括最常见的特征格式。

**数据值** 数据值可以是任何有效的文件名。

**默认值** 如果指定了数据类型特定的限定符 `-rname` 和 `-rextension`，则将构建格式为 `name.extension` 的报告文件名。值可以通过相应的 `rname:` 和 `rextension:` 属性硬编码。还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 报告文件的定义方式与普通输出文件（`outfile`）相同，但具有额外的限定符，以允许选择报告格式。

- `rformat`: 指定要使用的报告格式，必须是受支持的报告格式之一（请参阅 *EMBOSS 用户指南*）。
- `multiple`: 是一个布尔属性，如果输出可以包含来自同一输入的多个报告，则应将其设置为 "Y"。
- `type`: 定义为 "protein" 或 "nucleotide" 之一，其中报告格式是标准特征表格式之一（请参阅 *EMBOSS 用户指南*）。
- `taglist`: 定义要在输出中报告的内部特征表中的 tag:value 对。

### A.2.3.18 seqout

单个序列的输出文件。

**数据值** 数据值是序列输出流的 USA（请参阅 *EMBOSS 用户指南*）。例如，USA 可能是数据库引用或文件。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。如果在 ACD 文件中未定义 `name:` 属性，则它将默认为读取的 *第一个* 序列的计算属性 `name:`。如果序列参数名为 `asequence`，则获取此值的 ACD 操作是 $ (`asequence.name`)。还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 可以通过设置 `type:` 属性来限制序列类型。序列类型必须是标准类型（第 A.7 节，'序列类型'）。如果设置了 `features:` ACD 属性，则可以写入序列特征（第 6.9 节，'处理特征'）。输出序列默认使用 FASTA 格式。格式通常在命令行上设置，但可以使用 `osformat:` 硬编码默认值。

### A.2.3.19 seqoutall

多个序列的输出文件。

**数据值** 数据值是序列输出流的 USA（请参阅 *EMBOSS 用户指南*）。例如，USA 可能是数据库引用或文件。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。如果在 ACD 文件中未定义 `name:` 属性，则它将默认为读取的 *第一个* 序列的计算属性 `name:`。如果序列参数名为 `asequence`，则获取此值的 ACD 操作是 $ (`asequence.name`)。还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 可以通过设置 `type:` 属性来限制序列类型。序列类型必须是标准类型（第 A.7 节，‘序列类型’）。如果设置了 `features:` ACD 属性，则可以写入序列特征（第 6.9 节，‘处理特征’）。输出序列默认使用 FASTA 格式。格式通常在命令行上设置，但可以使用 `osformat:` 硬编码默认值。

### A.2.3.20 seqoutset

一组序列的输出文件。

**数据值** 数据值是存储在内存中并将一组单个序列写入文件的序列输出流的 USA（请参阅 *EMBOSS 用户指南*）。例如，USA 可能是数据库引用或文件。

**默认值** 输出文件名的格式为 `name.extension`，由 `name:` 和 `extension:` 属性构建。如果在 ACD 文件中未定义 `name:` 属性，则它将默认为读取的 *第一个* 序列的计算属性 `name:`。如果序列参数名为 `asequence`，则获取此值的 ACD 操作是 $ (`asequence.name`)。还可以通过定义 `default:` 全局属性来设置默认值。

**关键属性** 可以通过设置 `type:` 属性来限制序列类型。序列类型必须是标准类型（第 A.7 节，‘序列类型’）。如果设置了 `features:` ACD 属性，则可以写入序列特征（第 6.9 节，‘处理特征’）。输出序列默认使用 FASTA 格式。格式通常在命令行上设置，但可以使用 `osformat:` 硬编码默认值。

## A.2.4 选择 ACD 数据类型的描述

### A.2.4.1 list

带有文本标签的选项列表（文本描述）。

用户将看到一个可供选择的有限选项列表。选择可以用任意文本标签标记。选项描述通常比 `selection` 数据类型更详细。

**数据值** 数据值是有效选项中的一个（或多个）。

选项由标签文本或标签后给出的描述文本本身的非歧义部分指定。如果允许多选，用户必须提供逗号分隔的标签（选项）列表。例如，以下 ACD 定义：

```
list: frame [
  standard:"Y"
  help: "Allows selection from a set of reading frames"
  default: "1"
  minimum: "1"
```





```
maximum: "1"
header: "Translation frames"
values: "1:1, 2:2, 3:3, F:Forward three frames, -1:-1, -2:-2, -3:-3, R: Reverse three frames, 6:All six frames"
delimiter: ","
codedelimiter: ":"
information: "Frame(s) to translate"
]
```

将向用户呈现类似如下内容：

```
Translation frames
1 1
2 2
3 3
F Forward three frames
-1 -1
-2 -2
-3 -3
R Reverse three frames
6 All six frames
Frame(s) to translate:
```

要从列表中选择，用户指定一个（或有时多个）标签，或部分文本描述。程序将获得一组文本标签作为输入。在此示例中，ACD 定义中设置的最小和最大选择数均为 1，因此只允许一个选择值。例如，以下都是有效的选择：

```
"1"
"F"
"Forward"
"For"
"R"
"Reverse"
"Rev"
```

如果最大计数设置为 3，例如，则以下也是有效的：

```
"-1,F,6"
```

默认值 使用 default: 全局属性设置默认值。

关键属性 无。

### A.2.4.2 selection

带有自动生成数字标签的选项列表（文本描述）。

用户面前呈现一个可供选择的有限选项列表。选项会自动从 1 开始编号。选项描述通常比列表定义更详细。

数据值 数据值是有效选项中的一个（或多个）。
选项通过编号或标签后的描述文本本身中非歧义部分来指定。如果允许多选，用户必须提供逗号分隔的数字（选项）列表。
例如，以下是 ACD 定义：

```
selection: reject [
   default: "3, 5, 6"
   minimum: "1"
   maximum: "6"
   values: "None, AAINDEX, CVS, CODONS, PRINTS, PROSITE, REBASE"
   delimiter: ","
   header: "Directories to ignore"
   information: "Select directories"
   help: "This specifies the names of the sub-directories of the
           EMBOSS data directory that should be ignored when displaying data
           directories."
   button: "Y"
]
```

将向用户呈现类似如下内容：

```
Directories to ignore
1      None
2      AAINDEX
3      CVS
4      CODONS
5      PRINTS
6      PROSITE
7      REBASE
Select directories[3, 5, 6]:
```

要从列表中选择，用户指定一个（或有时多个）数字，或部分文本描述。程序将获得一组文本标签作为输入。在此示例中，ACD 定义中设置的最小选择数为 1，最大选择数为 6。以下是一些有效的选择：

```
"3,5,6"
"3"
"CVS"
"5"
"PRINTS"
"PRI"
```

默认值 使用 default: 全局属性设置默认值。

关键属性 无。

列表数据类型优于 selection:。

## A.2.5 图形 ACD 数据类型说明

### A.2.5.1 Graph

可生成任意类型的图形输出，例如点图。

**数据值** 数据值是图形设备，由 EMBOSS 当前使用的 **PLplot** 图形库指定。

当前支持的设备包括：

- ps (Postscript)
- png (PNG 文件)
- X11 (X-Windows)。

在提示符处输入 ? 将列出您安装中可用的图形设备。因此，一些允许的值为：

```
"ps"
"png"
"X11"
"?"
```

**默认值** 使用 default: 全局属性设置默认值。

**关键属性** gtitle: 指定图形标题（可设置许多其他图形元素）。

### A.2.5.2 graphxy

作为沿 x 轴排列序列的简单二维 (2D) XY 图的图形输出。

**数据值** 数据值是由 EMBOSS 当前使用的 **PLplot** 图形库指定的图形。

当前支持的设备包括：

- ps (Postscript)
- png (PNG 文件)
- X11 (X-Windows)。

在提示符处输入 ? 将列出您安装中可用的图形设备。因此，一些允许的值为：

```
"ps"
"png"
"X11"
"?"
```

**默认值** 使用 default: 全局属性设置默认值。

**关键属性** multiple: 指定单个输出中多个 XY 图的数量。gtitle: 指定图形标题（可设置许多其他图形元素）。

## A.3 应用程序属性

应用程序属性描述应用程序本身，且应仅在 application: 定义中给出。可用的应用程序属性将在下面详细说明。其一般格式为：

```
ApplicationAttributeName: "ApplicationAttributeValue"
```

### A.3.1 documentation:

这是对应用程序功能的简要描述，在运行程序以及使用 -help 限定符运行程序时将打印到屏幕上。documentation: 字符串还会被 wossname 实用程序搜索，该实用程序通过在 documentation: 文本和应用程序组中搜索关键字来查找应用程序。如果 documentation: 属性缺失，运行程序时将发出警告。documentation: 字符串必须符合以下约定：

- 文本应以大写字母开头。
- 长度应保持在 63 个字符或更短，以便 wossname 实用程序能够在一行 80 个字符中显示每个程序名称及其文档。

| 属性定义 | 描述 | 默认值 |
|---|---|---|
| documentation: VT_STR | 应用程序功能的简短描述 | " " |
| groups: VT_STR | wossname 和 GUI 的标准应用程序组 | " " |
| keywords: VT_STR | wossname 和 GUI 的标准应用程序组 | " " |
| gui: VT_STR | 适合在 GUI 中启动 | " " |
| batch: VT_STR | 适合在批处理中运行 | " " |
| embassy: VT_STR | EMBASSY 包名称 | " " |
| external: VT_STR | 此程序所需的第三方工具 | " " |
| cpu: VT_STR | 估计的最大 CPU 使用量 | " " |
| supplier: VT_STR | 供应商名称 | " " |
| version: VT_STR | 版本号 | " " |
| nonemboss: VT_STR | SoapLab 的非 EMBOSS 应用程序名称 | " " |
| executable: VT_STR | SoapLab 的非 EMBOSS 可执行文件 | " " |
| template: VT_STR | SoapLab ACD 文件的命令行模板 | " " |
| comment: VT_STR | SoapLab ACD 文件的注释 | " " |

- 文本不应以 '.' 字符结尾
- 文本中的任何缩写或简称都应写成大写
  (例如："SNPs", "EST", "DNA", "ABI", "SRS", "ASCII", "CDS", "mRNA",
  "B-DNA", "RNA", "CpG", "ORFs", "MAR/SAR", "PCR", "STS", "REBASE",
  "SCOP", "PROSITE", "PRINTS", "EMBL", "TRANSFAC", "AAINDEX",
  "BLAST", "GCG", "EMBOSS")。

### A.3.2 groups:

这允许根据功能将 EMBOSS 程序放入组或子组中。同一子组中的程序通常执行类似的操作，而同一组但不同子组中的程序执行不同的操作，但属于同一常规领域。`groups:` 字符串由 **wossname** 程序搜索，给定一个关键字，它将返回在 `groups:` 文本或 `documentation:` 文本中包含该关键字的所有应用程序。`groups:` 字符串还由 **seealso** 应用程序使用，该应用程序获取 EMBOSS 程序的名称并返回与其共享某些功能的程序列表。

`groups:` 属性后跟一个字符串值，包含应用程序所属的一个或多个组和一个或多个子组的名称。子组是可选的，但如果指定，组和子组必须用冒号 (`:`) 分隔。当应用程序属于多个组（或子组）时，组名称必须用逗号 (`,`) 或分号 (`;`) 分隔。

`groups:` 属性的一般格式如下：

```
application: ApplicationName
[
    groups: "GroupName1, GroupName2, ... : SubgroupName1, SubgroupName2, ..."
]
```

`groups:` 字符串必须符合以下约定：

- 理想情况下，组名称应取自应用程序 ACD 文件目录中 EMBOSS 系统文件 `groups.standard` 定义的标准组名称列表（参见第 4.2.4.1 节，“应用程序组名称文件 (`groups.standard)””）。可以定义新组，但定义应发送给 EMBOSS 开发人员，以便将其添加到标准集中。
- 组名称可以包含空格。
- 子组是可选的，但如果指定，组和子组必须用冒号 (`:`) 分隔。
- EMBOSS 支持任意数量的子组级别；但是，几个第三方接口依赖于总共最多两个级别，因此请勿使用超过一个。
- 当应用程序属于多个组（或子组）时，组名称必须用逗号 (`,`) 或分号 (`;`) 分隔。





### A.3.3 关键字：

描述应用程序功能的一组关键字。这些关键字由应用程序 embossname 和一些面向 EMBOSS 的 GUI 使用。

### A.3.4 gui：

该属性的值为 "Yes" 或 "No"，反映了在 GUI 中启动应用程序的适用性。

### A.3.5 batch：

该属性的值为 "Yes" 或 "No"，反映了在批处理队列中启动应用程序的适用性。

### A.3.6 EMBASSY：

EMBASSY 包名称（如果适用）。

### A.3.7 external：

此程序所需的第三方工具。此属性由封装（调用）第三方应用程序的应用程序使用，因此依赖于运行 EMBOSS 的系统上存在该软件。

### A.3.8 cpu：

估计的最大 CPU 使用量。

### A.3.9 supplier：

供应商名称，适用于应用程序由 EMBOSS 核心开发者以外的机构提供的情况。

### A.3.10 version：

应用程序的版本号，用于需要与 EMBOSS 或 EMBASSY 包版本号不同的版本号的情况。

### A.3.11 nonemboss：

此布尔属性指定应用程序是否属于 EMBOSS 或 EMBASSY。它仅由 SoapLab 使用。

### A.3.12 executable：

不属于 EMBOSS 或 EMBASSY 的应用程序名称。这用于（例如 SoapLab）等环境，其中应用程序使用 ACD 语法定义，但不属于 EMBOSS 或 EMBASSY 本身。

### A.3.13 template：

这是 SoapLab ACD 文件的命令行模板。

### A.3.14 comment：

用于关于应用程序的注释，并由 SoapLab 的 ACD 文件使用。

## A.4 全局属性

### A.4.1 简介

全局属性适用于所有数据类型，可以在任何 ACD 数据定义中按如下方式定义：

```
GlobalAttributeName: "GlobalAttributeValue"
```

大多数全局属性具有字符串或布尔值，这些值在 ACD 文件中显式设置。布尔值具有硬编码的默认值，可以通过显式说明值来覆盖。"Y"、"Yes"、"N" 或 "No" 中的任何值（字符串不区分大小写）都是可接受的。

下面描述了全局属性，为了方便，它们按功能分组如下：

- 参数和限定符
- 用户提示
- 数据类型定义
- 帮助信息和文档
- GUI 提示
- 供 SoapLab 使用。

在属性描述中，值类型和默认值按如下方式指示：

```
GlobalAttributeName: Type ("Default")
```

例如，以下内容表示 parameter: 全局属性具有布尔值，默认值为 "N"：

```
parameter: Boolean ("N")
```

相比之下，以下内容表示 help: 全局属性具有字符串值，默认值为 ""（空字符串）：

```
help: "String" ("")
```

### A.4.2 全局属性表

全局属性如下表所示：

### A.4.3 参数和限定符

每个 ACD 数据定义可以定义为以下之一：

- 参数
- 标准限定符
- 附加限定符

默认值为：

- 高级限定符。

| 全局属性 | 描述 | 默认值 |
|---|---|---|
| `default: string` | 默认值 | `""` |
| `information: string` | 用于菜单等的信息以及默认提示 | `""` |
| `prompt: string` | 提示（如果 information: string 不清楚） | `""` |
| `code: string` | 用于在 codes, english 中搜索的信息/提示的代码名称 | `""` |
| `help: string` | 帮助文档文本 | `""` |
| `parameter: boolean` | 命令行参数。可以不带限定符名称指定。隐含标准限定符 | `"N"` |
| `standard: boolean` | 标准限定符，需要值。如果缺失则进行交互式提示 | `"N"` |
| `additional: boolean` | 附加限定符。如果命令行上有 -options 则需要值 | `"N"` |
| `missing: boolean` | 允许命令行上的 NULL 值 | `"N"` |
| `valid: string` | `help: String` 对 `-help` 输出允许值的描述，如果默认帮助不清楚则使用 | `""` |
| `expected: string` | `help: String` 对 `-help` 输出预期值的描述，如果默认帮助不清楚则使用 | `""` |
| `needed: boolean` | 包含在 GUI 表单中，用于在 GUI 中不清楚时隐藏选项 | `"Y"` |
| `knowntype: string` | 已知标准类型，用于定义工作流的输入和输出类型 | `""` |
| `relations: string` | 此 ACD 项目与其他项目之间的关系，定义为特殊格式的文本 | `""` |
| `outputmodifier: boolean` | 以可能破坏解析器的方式修改输出 | `"N"` |
| `style: string` | SoapLab ACD 文件的样式 | `""` |
| `qualifier: string` | SoapLab ACD 文件的限定符名称 | `""` |
| `template: string` | SoapLab ACD 文件的命令行模板 | `""` |
| `comment: string` | SoapLab ACD 文件的注释 | `""` |
| `pformat: "string"` | 文件格式 | `""` |
| `pname: "string"` | 模式基本名称 | `""` |

应使用的属性如下：

```
Parameter: "Y"
Standard: "Y"
Additional: "Y"
```

在数据定义中，parameter : "Y"、standard : "Y" 或 additional : "Y" 只能给出一个。如果使用了多个，ACD 处理期间将生成错误消息。

绝不应显式指定 parameter : "N"、standard : "N" 或 additional : "N"；如果这样做，ACD 处理期间将生成错误。之前定义中的 "Y" 是为了保持一致性而给出的，因为每个 ACD 属性作为标签:值对，都必须有一个值。在实践中，计算出的 "N" 值实际上是受支持的，可以在特殊情况下用于覆盖这些属性的默认行为（参见第 4.5 节“控制提示”）。

有关更多信息，请参见第 A.1.5 节“参数和限定符”。

#### A.4.3.1 parameter:

将数据定义定义为参数。

参数的值可以在命令行上带或不带标志（参数名称）给出。任何未指定标志的参数必须按照它们在 ACD 文件中出现的相同顺序出现。应用程序需要所有参数，如果命令行上未给出某个值，将提示输入。

例如：

```
application: acddemo
[
    documentation: "Test application"
    groups: "Test"
]
sequence: asequence
```

```
[
    parameter: "Y"
]
```

上述应用程序可以使用命令行标志运行：

```
acddemo -asequence filename.seq
```

或不使用它：

```
acddemo filename.seq
```

在两个示例中，`filename.seq` 是 EMBOSS 程序 **acddemo** 中名为 asequence 的参数的值。

在以下示例中，定义了两个参数：

```
application: acddemo
[
    documentation: "Test application"
    groups: "Test"
]
sequence: asequence
[
    parameter: Y
]
outseq: outseq
[
    parameter: Y
]
```

除非使用命令行标志，否则它们在命令行上出现的顺序必须与 ACD 文件中的相同：

```
acddemo infilename.seq outfilename.seq
```

这将把名称 `infilename.seq` 分配给参数 asequence，把 `outfilename.seq` 分配给参数 outseq。

但是如果使用标志，值可以以任何顺序给出：

```
acddemo -outseq outfilename.seq -asequence infilename.seq
```

某些 ACD 数据类型（见下文）通常是主输入或输出，因此应定义为参数。ACD 文件中第一个此类数据类型 *必须* 定义为参数（否则 ACD 处理期间将生成错误）。建议该数据类型的后续定义也是参数（如果不是，将生成警告）。例外情况是如果设置了 `default:` 或 `nullok:` 属性，在这种情况下不会生成警告或错误消息，因为应用程序可以使用默认值或没有该定义的任何值运行。

数据类型如下：

- 文件输入（`infile`、`filelist`、`directory` 或 `dirlist`）
- 序列输入（`sequence`、`seqall`、`seqsetall` 或 `seqset`）
- 序列特征输入（`feature`）
- 比对输出（`align`）
- 报告输出（`report:`）
- 序列特征输出（`featout`）
- 文件输出（`outdir`）。

#### A.4.3.2 standard:

将数据定义定义为 *标准限定符*。

标准限定符的行为与参数相同，只是在命令行上给出值时必须始终使用命令行标志。应用程序需要所有标准限定符，如果命令行上未给出值，将提示输入。

任何程序都预期具有一个或多个必需输入。定义为 `parameter:` 的 ACD 数据定义会自动计为必需。所有其他必需输入都应设置 `standard:` 属性。当程序运行时，用户将被提示输入命令行上尚未提供的任何“必需”值。

在以下示例中，定义了两个标准限定符：

```
application: acddemo
[
    documentation: "Test application"
    groups: "Test"
]
sequence: asequence
[
    standard: Y
]
outseq: outseq
[
    standard: Y
]
```

命令行上必须使用标志，值可以以任何顺序给出：

```
acddemo -asequence infilename.seq -outseq outfilename.seq
acddemo -outseq outfilename.seq -asequence infilename.seq
```





如果任一值被省略，系统将提示用户输入。

## A.4.3.3 additional: “Boolean” (“N”)

将数据定义定义为_附加限定符_。

附加限定符的行为与标准限定符相同，只是如果在命令行中未给出值，则_不会_提示输入，_除非_应用程序使用 `-options` 全局限定符运行，在这种情况下，所有附加限定符都将提示输入。

附加限定符被视为应用程序非绝对必需。

当在命令行中给出值时，必须始终使用命令行标志。

在以下示例中，定义了两个附加限定符：

```
application: acddemo
[
    documentation: "Test application"
    groups: "Test"
]
sequence: asequence
[
    additional: Y
]
outseq: outseq
[
    additional: Y
]
```

标志必须在命令行中使用，值可以按任何顺序给出：

```
acddemo -asequence infilename.seq -outseq outfilename.seq
acddemo -outseq outfilename.seq -asequence infilename.seq
```

如果任一值被省略，用户_不会_被提示输入，_除非_应用程序使用 `-options` 运行：

```
acddemo -asequence infilename.seq -options
```

在此示例中，为 `asequence` 指定了值，但为 `outseq` 省略了值。`-options` 标志已设置，这意味着用户将被提示为 `outseq` 输入一个值。

## A.4.4 User prompting

### A.4.4.1 information: “String” (“”)

对参数的非常简洁的描述。

该文本用于 Web 表单和其他 GUI。它也是在命令行中提示用户输入值时使用的文本。`code:`、`prompt:` 或 `information` 中只应定义一个。建议使用 information:（带有标准名称，见下文），而不是 code: 或 prompt:。

为提供标准提示，为大多数常见数据类型定义了 information: 字符串的默认值。默认值位于应用程序 ACD 文件目录中的 EMBOSS 系统文件 codes.english 中（参见第 4.3.5.2.1 节，“标准提示文件 (codes.english)”）。

标准做法是尽可能使用默认提示。如果 information: 属性缺失，或者如果有标准值可用但值不是标准值，则在 ACD 处理期间会生成警告。

如果使用非标准提示，则 information: 属性后给出的文本应符合以下约定（否则在 ACD 处理期间将生成警告）：

- 字符串应以大写字母字符开头
- 字符串不应以句号结尾

### A.4.4.2 code: “String” (“”)

一个代码词，在 EMBOSS 系统文件 codes.english（第 4.3.5.2.1 节，“标准提示文件 (codes.english)”）中搜索，以给出标准提示。codes.english 为所有常见 ACD 数据类型提供标准提示。

例如，间隙插入和延伸罚值可以定义为整数或浮点值。这些值的标准提示由 codes.english 中的代码 GAP 或 GAPEXT 标识。这些提示可以与 code: 属性一起使用，例如 code: "GAP"。代码词不区分大小写，因此 code: "gap" 也是可接受的。

在实践中，GUI 开发者发现 code: 属性难以使用，因此倾向于使用 information: 属性。

### A.4.4.3 prompt: “String” (“”)

用于在命令行中提示用户输入值的字符串。

prompt: 的使用现已弃用；建议使用 information:。但是，在 information: 字符串具有误导性的罕见情况下，可以定义 prompt: 字符串。

prompt: 属性后给出的文本应符合以下约定（否则在 ACD 处理期间将生成警告）：

- 字符串应以大写字母字符开头
- 字符串不应以句号结尾

## A.4.5 Datatype definition

### A.4.5.1 knowntype: “String” (“”)

来自已知值类型受控词汇表的数据定义的已知类型。

当类型本身从数据类型中不明显时，应定义 knowntype:。它通常为 string、infile、outfile 和 outfileall 数据类型定义，但例如不为 sequence: 定义。

如果未指定，则对 string、outfile 和 outdir ACD 数据类型生成警告。

标准值（已知类型）列在应用程序 ACD 文件目录中的 EMBOSS 系统文件 knowntypes.standard 中。

还接受 knowntypes.standard 中未列出的少数其他值，例如 outfile : 数据类型的“ApplicationName output”。这些与数据类型一起记录（第 A.5 节，“数据类型特定属性”）。如果给出的值不是标准已知类型或其他可接受值，则在 ACD 处理期间将生成警告消息。acdvalid 实用程序将检查 ACD 文件中的所有 knowntype 值，并报告需要已知类型的数据定义中缺少的任何值。

### A.4.5.2 default: “Value” (“”)

参数的默认值。

对于许多但并非所有数据定义，定义默认值是合适的。对于某些数据类型，默认值是硬编码的或由数据类型特定属性的命名方案生成。有关更多信息，请参阅数据类型描述（第 A.5 节，“数据类型特定属性”）。

默认值可以依赖于先前定义的参数的值；这是通过使用 ACD 操作来设置值完成的（参见第 A.8 节，“操作”）。

### A.4.5.3 relations: “String” (“”)

用于描述此 ACD 数据定义与其他数据定义之间关系的文本。

### A.4.5.4 outputmodifier: “boolean” (“N”)

对于控制应用程序输出中写入字段的数据定义，此项设置为 "True"。

在实践中，outputmodifier: 专用于 boolean 和 toggle 数据类型，这些类型以可能在解析软件中造成问题的方式修改输出。

### A.4.5.5 missing: “boolean” (“N”)

指示是否可以在命令行中为参数指定空值。这仅在输出文件中需要，即有默认文件命名方案可用但 ACD 文件中也指定了默认值的情况下。在这种情况下，如果在命令行中为参数给出空值 ("")，则可以覆盖 ACD 文件中的默认值并使用命名方案。

## A.4.6 Help information and documentation

### A.4.6.1 help: “String” (“”)

当应用程序在命令行中使用 -help 限定符运行时显示的参数有用信息，并用于应用程序文档。

help: 通常仅在需要更深入解释应用程序参数时才定义。如果未定义 help:，则改用 information: 属性的值（如果可用）或默认帮助字符串。EMBOSS 系统文件 codes.english 文件（第 4.3.5.4.1 节，“标准帮助字符串文件 (codes.english 文件)”）中为每种数据类型提供了默认帮助字符串。

help: 属性后给出的文本应符合以下约定（否则在 ACD 处理期间将生成警告）：

- 字符串应以大写字母字符开头
- 字符串不应以句号结尾

### A.4.6.2 valid: “String” (“”)

参数允许值的描述。
用于应用程序文档的命令行语法表中的“允许值”列。此表自动从 ACD 文件生成。在大多数情况下，会自动生成合理的值，但如果没有合适的值，则应使用此属性来提供一个。

### A.4.6.3 expected: “String” (“”)

参数预期值的描述。
用于应用程序文档的命令行语法表中的“预期值”列。此表自动从 ACD 文件生成。在大多数情况下，会自动生成合理的值，但如果没有合适的值，则应使用此属性来提供一个。

## A.4.7 Hints for GUIs

### A.4.7.1 needed: boolean (“Y”)

指示参数是否预期包含在 GUI 表单中。这是供 GUI 开发者使用的提示。某些参数在命令行中可用，但对用户通常不太有用，或者在 GUI 表单中与所有其他选项一起呈现时可能会造成混淆。

## A.4.8 For use by SoapLab

### A.4.8.1 qualifier: “String” (“”)

SoapLab ACD 文件的限定符名称。不应在标准 EMBOSS 应用程序 ACD 文件中使用。

### A.4.8.2 template: “String” (“”)

SoapLab ACD 文件的命令行模板。不应在标准 EMBOSS 应用程序 ACD 文件中使用。

### A.4.8.3 comment: “String” (“”)

SoapLab ACD 文件的注释。不应在标准 EMBOSS 应用程序 ACD 文件中使用。





## A.5 数据类型特定属性

数据类型特定属性仅适用于（可定义于）特定的 ACD 数据类型。每种数据类型都有自己的一组此类属性。此外，还有各种与数据类型关联的命令行限定符（或简称为“关联限定符”），它们是某些 ACD 数据类型内置的，也可以作为属性硬编码在相应的数据定义中。下面将详细描述这两种类型的属性。它们的值在 ACD 数据定义中显式设置，如下所示：

```
DataAttributeName: "DataAttributeValue"
```

在属性描述中，值类型和默认值的指示方式如下：

```
DataAttributeName: Type ("Default")
```

### A.5.1 简单属性描述

### A.5.1.1 array

- size: "integer" ("1") 数组中的元素数量。
- minimum: "float" ("-FLT_MIN") 下限值。默认为系统设置指定的边界。
- maximum: "float" ("+FLT_MAX") 上限值。默认为系统设置指定的边界。
- sum: "float" ("1.0") 数组中所有值的总和（除非 sumtest: 属性为 false，否则会进行测试）。
- sumtest: "boolean" ("Y") 如果为 false，则关闭对 sum: 属性的测试。
- tolerance: "float" ("0.01") 指定 sum: 应与总和匹配的紧密程度。大多数浮点小数无法在二进制形式中准确表示。
- warnrange: "boolean" ("Y") 控制是否在给出超出范围的值时发出警告。
- increment: "integer" ("0") 定义在迭代时数组值可以采取的步长。increment: 可以是任何有效的浮点值。仅为 EMBOSS 的 GUI 实现，EMBOSS 本身不使用（在 ACD 文件处理期间会被忽略）。
- precision: "integer" ("0") 定义为此值考虑的最大有效小数位数。仅为 EMBOSS 的 GUI 实现，EMBOSS 本身不使用（在 ACD 文件处理期间会被忽略）。

### A.5.1.1.1 关联限定符

array 数据类型没有关联限定符。

### A.5.1.2 boolean

boolean 当前没有特定属性。

### A.5.1.2.1 关联限定符

boolean 数据类型没有关联限定符。

### 注意

定义 information: 和 help: 全局属性时应谨慎。这些属性用于提示用户（交互式或通过 GUI），并提供帮助文本。每种情况下提供的文本都应反映布尔选项的预期默认值，这可能与名称所暗示的相反。例如，如果默认设置为 "Y"，则命令行选项通常为 -noFlag，其中 Flag 是限定符。如果默认设置为 "N"，则默认操作可能与信息或帮助文本所暗示的相反。如果值是计算得出的，用户可能需要一些额外的指导。

### A.5.1.3 float

minimum: "float" ("-FLT_MIN") 下限值。默认为系统设置指定的边界。

maximum: "float" ("+FLT_MAX") 上限值。默认为系统设置指定的边界。

increment: "float" ("1") 此参数允许采取的步长，以防需要迭代此参数。increment: 属性可以是任何有效的浮点值。

precision: "integer" ("3") 为此值考虑的最大有效小数位数。

warnrange: "boolean" ("Y") 控制是否在给出超出范围的值时发出警告。

### A.5.1.3.1 关联限定符

float 数据类型没有关联限定符。

### A.5.1.4 integer

minimum: "integer" ("INT_MIN") 下限值。默认为系统设置指定的边界。

maximum: "integer" ("INT_MAX") 上限值。默认为系统设置指定的边界。

increment: "integer" ("0") 定义此参数允许采取的步长，以防需要迭代此参数。

warnrange: "boolean" ("Y") 控制是否在给出超出范围的值时发出警告。

### A.5.1.4.1 关联限定符

integer 数据类型没有关联限定符。

### A.5.1.5 range

minimum: "integer" ("1") 下限值。

maximum: "integer" ("INT_MAX") 上限值。默认为系统设置指定的边界。

minsize: "integer" ("0") 当定义多个范围时，minsize: 定义必须定义的最小范围数量。

size: "integer" ("0") 所需值的精确数量。对于任何范围，只应定义 size: 或 minsize: 中的一个。

### A.5.1.5.1 关联限定符

range 数据类型没有关联限定符。

### A.5.1.6 regexp

minlength: "integer" ("1") 正则表达式字符串可以具有的最小长度。

maxlength: "integer" ("INT_MAX") 正则表达式字符串可以具有的最大长度。

upper: "boolean" ("N") 在编译前将正则表达式转换为大写。

lower: "boolean" ("N") 在编译前将正则表达式转换为小写。

maxsize: "integer" ("INT_MAX") 模式的最大数量。

type: 模式的类型，当前为 string、nucleotide 或 protein 之一。

### A.5.1.6.1 关联限定符

regexp 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

### A.5.1.7 pattern

minlength: "integer" ("1") 模式可以具有的最小长度。

maxlength: "integer" ("INT_MAX") 模式可以具有的最大长度。

upper: "boolean" ("N") 在编译前将模式转换为大写。

lower: "boolean" ("N") 在编译前将模式转换为小写。

maxsize: "integer" ("INT_MAX") 模式的最大数量。

type: 模式的类型，当前为 string、nucleotide 或 protein 之一。

### A.5.1.7.1 关联限定符

pattern 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 值 | 类型 | 间隙 | 歧义代码 | 转换 | 描述 |
|---|---|---|---|---|---|
| any | 核苷酸或蛋白质 | 移除 | 是 | '?'=> 'X' | 任何有效序列 |
| gapany | 核苷酸或蛋白质 | 保留 | 是 | '?'=> 'X' | 带间隙的任何有效序列 |
| dna | 仅核苷酸 | 移除 | 是 | '?'=> 'N'<br>'X'=> 'N'<br>'U'=> 'T' | DNA 序列 |
| puredna | 仅核苷酸 | 移除 | 否 | 'U'=> 'T' | DNA 序列，仅碱基 ACGT |
| gapdna | 仅核苷酸 | 保留 | 是 | '?'=> 'N'<br>'X'=> 'N'<br>'U'=> 'T' | 带间隙的 DNA 序列 |
| gapdnaphylo | 仅核苷酸 | 保留 | 是 | 'U'=> 'T' | 带间隙和查询的 DNA 序列 |
| rna | 仅核苷酸 | 移除 | 是 | '?'=> 'N'<br>'X'=> 'N'<br>'T'=> 'U' | RNA 序列 |
| purerna | 仅核苷酸 | 移除 | 否 | 'T'=> 'U' | RNA 序列，仅碱基 ACGU |
| gaprna | 仅核苷酸 | 保留 | 是 | '?'=> 'N'<br>'X'=> 'N'<br>'T'=> 'U' | 带间隙的 RNA 序列 |
| gaprnaphylo | 仅核苷酸 | 保留 | 是 | 'T'=> 'U' | 带间隙和查询的 RNA 序列 |
| nucleotide | 仅核苷酸 | 移除 | 是 | '?'=> 'N'<br>'X'=> 'N' | 核苷酸序列 |
| purenucleotide | 仅核苷酸 | 移除 | 否 | | 核苷酸序列，仅碱基 ACGTU |
| gapnucleotide | 仅核苷酸 | 保留 | 是 | '?'=> 'N'<br>'X'=> 'N' | 带间隙的核苷酸序列 |
| gapnucleotidephylo | 仅核苷酸 | 保留 | 是 | | 带间隙和查询的核苷酸序列 |
| protein | 仅蛋白质 | 移除 | 是 | '?'=> 'X'<br>'*'=> 'X' | 蛋白质序列 |
| pureprotein | 仅蛋白质 | 移除 | 否 | | 不含 BZ U X 或 * 的蛋白质序列 |
| stopprotein | 仅蛋白质 | 移除 | 是 | '?'=> 'X' | 带可能终止符的蛋白质序列 |
| gapprotein | 仅蛋白质 | 保留 | 是 | '?'=> 'X'<br>'*'=> 'X' | 带间隙的蛋白质序列 |
| gapstopprotein | 仅蛋白质 | 保留 | 是 | '?'=> 'X' | 带间隙和可能终止符的蛋白质序列 |
| gapproteinphylo | 仅蛋白质 | 保留 | 是 | | 带间隙、终止符和查询的蛋白质序列 |
| proteinstandard | 仅蛋白质 | 移除 | 是 | '?'=> 'X'<br>'*'=> 'X'<br>'U'=> 'X' | 不含硒半胱氨酸的蛋白质序列 |
| stopproteinstandard | 仅蛋白质 | 移除 | 是 | '?'=> 'X'<br>'U'=> 'X' | 带可能终止符但不含硒半胱氨酸的蛋白质序列 |
| gapproteinstandard | 仅蛋白质 | 保留 | 是 | '?'=> 'X'<br>'*'=> 'X'<br>'U'=> 'X' | 带间隙但不含硒半胱氨酸的蛋白质序列 |

- pformat: "string" ("") 文件格式
- pmismatch: "integer" ("") 模式不匹配
- pname: "string" ("") 模式基本名称

### A.5.1.8 string

minlength: "integer" ("0") 字符串的最小长度。默认最小长度为零。

maxlength: "integer" ("INT_MAX") 字符串的最大长度。没有默认最大长度。





pattern: "string" ("") 定义用于验证字符串值的正则表达式：无效字符串将提示重新输入。EMBOSS 使用 Perl 兼容正则表达式库 (PCRE)，因此任何 Perl 兼容正则表达式都应可用。

word: "boolean" ("N") 如果设置，要求结果为不含空白的有效单词。注意默认最小长度为零允许空字符串；但是，这不被接受为单词。

upper: "boolean" ("N") 将字符串的大小写在内部转换为大写。

lower: "boolean" ("N") 将字符串的大小写在内部转换为小写。upper: 或 lower: 中只应指定一个。

### A.5.1.8.1 关联限定符

字符串数据类型没有关联限定符。

### A.5.1.9 切换开关

虽然目前针对 toggle ACD 类型没有特定属性，但应谨慎定义 information: 和 help: 属性。这些属性用于提示用户（交互式或通过 GUI），并提供帮助文本。每种情况下提供的文本应反映切换选项的预期默认值，这可能与名称所暗示的相反。例如，如果默认设置为 "Y"，则命令行选项通常为 -noFlag，其中 Flag 是限定符。如果默认设置为 "N"，则默认操作可能与信息或帮助文本所暗示的相反。如果值是计算得出的，用户可能需要一些额外指导。

### A.5.1.9.1 关联限定符

切换开关数据类型没有关联限定符。

## A.5.2 输入属性描述

### A.5.2.1 密码子

name: "string" ("Ehum.cut") 各个密码子数据定义可以使用 name: 属性设置其自己的默认密码子使用表。或者，可以通过全局属性 default: 设置。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有密码子使用表的情况下运行，则必须将 nullok: 属性设置为 "Y"。在这种情况下，数据定义可能不会指定密码子使用文件（在 ACD 文件或命令行上）。这种情况可能发生在应用程序仅在特定情况下需要密码子使用表时。

### A.5.2.1.1 关联限定符

密码子数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

format: "string" ("") 数据格式。

### A.5.2.2 cpdb

name: "string" ("") 各个 cpdb 输入可以使用 name: 属性设置其自己的默认名称，在当前版本中这与设置 default: 全局属性效果相同。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有干净 PDB 文件输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。在这种情况下，数据定义可能不会指定干净坐标文件（在 ACD 文件或命令行上）。这种情况可能发生在文件仅在应用程序特定情况下需要时。

### A.5.2.2.1 关联限定符

cpdb 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

format: "string" ("") 数据格式。

### A.5.2.3 数据文件

name: "string" ("") 默认数据文件的基本名称。

extension: "string" ("") 默认数据文件的文件扩展名。

directory: "string" ("") 要搜索的 EMBOSS 数据子目录。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有数据文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上指定 -noFlag（其中 Flag 是定义的名称）。

### A.5.2.3.1 关联限定符

数据文件数据类型没有关联限定符。

### A.5.2.4 目录

extension: "string" ("") 从目录读取的所有文件的文件扩展名。其他扩展名的文件不会被读取。

fullpath: "boolean" ("N") 如果设置为 "Y"，则将指定的目录解释为全路径而非相对路径。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有目录的情况下运行，则必须将 nullok: 属性设置为 "Y"。在这种情况下，可能不会设置默认目录，或者命令行上可能会给出 -noFlag，其中 Flag 是数据定义标志的名称。

nulldefault: "boolean" ("N") 默认情况下，目录中文件的名称从上述路径和扩展名构建。nulldefault: 属性覆盖默认名称生成，默认使用空字符串（无目录）。这对于仅偶尔需要目录的程序很有用。如果在命令行上为目录指定空字符串，则将使用默认名称生成。与 `nullok:` 结合使用，这允许限定符默认为空，并从命令行启用。

### A.5.2.4.1 关联限定符

`directory` 数据类型没有关联限定符。

### A.5.2.5 目录列表

- `extension: "string" ("")` 从目录读取的所有文件的扩展名。其他扩展名的文件不会被读取。
- `fullpath: "boolean" ("N")` 如果设置为 "Y"，则将给定路径解释为全路径而非相对路径规范。
- `nullok: "boolean" ("N")` 如果应用程序可以接受此定义的空值，并且可以在没有目录的情况下运行，则必须将 `nullok:` 属性设置为 "Y"。在这种情况下，可能不会设置默认目录，或者命令行上可能会给出 `-noFlag`，其中 `Flag` 是数据定义标志的名称。

### A.5.2.5.1 关联限定符

`dirlist` 数据类型没有关联限定符。

### A.5.2.6 离散状态

- `length: "integer" ("0")` 每组中状态值的数量（离散字符字符串的长度）。
- `size: "integer" ("1")` 值集的数量（通常为 1），但某些程序会接受多个集。
- `characters: "string" ("01")` 定义可以指定哪些离散状态字符。这定义为包含所有可能字符的字符串。
- `nullok: "boolean" ("N")` 如果应用程序可以接受此定义的空值，并且可以在没有 `discretestates` 文件的情况下运行，则必须将 `nullok:` 属性设置为 "Y"。这允许应用程序在没有默认值的情况下运行，或在命令行上使用 `-noFlag`（其中 `Flag` 是数据定义的名称）运行。

### A.5.2.6.1 关联限定符

`discretestates` 数据类型没有关联限定符。

### A.5.2.7 距离

- `size: "integer" ("1")` 距离矩阵中的行数。
- `missval: "boolean" ("N")` 如果设置为 "Y"，表示矩阵可以包含缺失值。
- `nullok: "boolean" ("N")` 如果应用程序可以接受此定义的空值，并且可以在没有距离矩阵文件的情况下运行，则必须将 `nullok:` 属性设置为 "Y"。这允许应用程序在没有默认值的情况下运行，或在命令行上使用 `-noFlag`（其中 `Flag` 是数据定义标志）运行。

### A.5.2.7.1 关联限定符

`distances` 数据类型没有关联限定符。

### A.5.2.8 特征

type: "string" ("") 特征输入是 'protein' 还是 'nucleotide'。基于任何输入序列的类型有一个默认值，但应始终指定一个值。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有特征输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许应用程序在没有默认值的情况下运行，或在命令行上使用 -noFlag（其中 Flag 是数据定义标志）运行。

### A.5.2.8.1 关联限定符

特征数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| fformat: "string" ("") | 特征格式 |
| fopenfile: "string" ("") | 特征文件名 |
| fask: "boolean" ("N") | 提示开始/结束/反向 |
| fbegin: "integer" ("0") | 要使用的特征的开始位置 |
| fend: "integer" ("0") | 要使用的特征的结束位置 |
| freverse: "boolean" ("N") | 反向（如果是 DNA） |

### A.5.2.9 文件列表

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有文件列表输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这指定缺失的输入文件对应用程序是可接受的，并且可以在命令行上使用 -noFlag（其中 Flag 是数据定义标志）。

### A.5.2.9.1 关联限定符

文件列表数据类型没有关联限定符。

### A.5.2.10 频率

length: "integer" ("0") 定义频率文件中的位点（或值）数量。

size: "integer" ("1") 值集的数量，通常为 1，但某些程序会接受多个集。

continuous: "boolean" ("N") 指定具有连续字符数据值的频率文件。

genedata: "boolean" ("N") 指定具有遗传位点数据值的频率文件。

within: "boolean" ("N") 指定具有多个个体连续数据的频率文件（每行附加值）。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有频率文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许应用程序在没有默认值的情况下运行，或在命令行上使用 -noFlag（其中 Flag 是数据定义标志的名称）。

### A.5.2.10.1 关联限定符

频率数据类型没有关联限定符。





### A.5.2.11 infile

nullok: "boolean" ("N") 指定缺少的输入文件对应用程序是可接受的。应用程序可以在没有默认值的情况下运行，或者在命令行中使用 -noFlag（其中 Flag 是数据定义的名称）。

directory: "@(value:ENVNAME)" 指定用于查找文件的目录。目录由环境变量 ENVNAME 给出，首先将其解析为 EMBOSS_ENVNAME（在 emboss.default 中或通过 setenv 调用设置）。然后它会检查 ENVNAME（使用 setenv 设置）。如果用户在文件名中给出了显式路径，则忽略该目录。

### A.5.2.11.1 关联限定符

infile 数据类型没有关联限定符。

### A.5.2.12 matrix

protein: "boolean" ("Y") 如果设置为 "Y"，将指定评分矩阵是蛋白质矩阵。如果未设置，则假定矩阵用于核酸。

pname: "string" ("EBLOSUM62") 定义要使用的默认蛋白质矩阵。蛋白质矩阵的系统默认值为 EBLOSUM62。

nname: "string" ("EDNAFULL") 定义要使用的默认核苷酸矩阵。核苷酸矩阵的系统默认值为 EDNAFULL。

### A.5.2.12.1 关联限定符

matrix 数据类型没有关联限定符。

### A.5.2.13 matrixf

protein: "boolean" ("Y") 如果设置为 "Y"，将指定评分矩阵是蛋白质矩阵。如果未设置，则假定矩阵用于核酸。

pname: "string" ("EBLOSUM62") 定义要使用的默认蛋白质矩阵。蛋白质矩阵的系统默认值为 EBLOSUM62。

nname: "string" ("EDNAFULL") 定义要使用的默认核苷酸矩阵。核苷酸矩阵的系统默认值为 EDNAFULL。

### A.5.2.13.1 关联限定符

matrixf 数据类型没有关联限定符。

### A.5.2.14 properties

length: "integer" ("0") 属性文件中的值的数量。

size: "integer" ("1") 值集的数量，通常为 1，但某些程序会接受多个集。

characters: "string" ("") 定义可以指定的属性字符。这定义为包含所有可能字符的字符串。

## A.5 数据类型特定属性

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有属性文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行中使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

### A.5.2.14.1 关联限定符

properties 数据类型没有关联限定符。

### A.5.2.15 scop

nullok: "boolean" ("N") 用于设置单个 scop 输入的默认值，其效果与设置 default: 属性相同。

### A.5.2.15.1 关联限定符

scop 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

```
format: "string" ("") 数据格式。
```

### A.5.2.16 sequence

type: "string" ("") 强制序列为给定类型。默认情况下接受任何序列类型。理想情况下，type: 属性应始终设置，以便明确接受的输入序列类型。序列类型必须是标准序列类型（第 A.7 节，‘序列类型’）。

features: "boolean" ("N") 如果设置了 features: 属性，序列输入将包含特征信息，无论是在同一文件中（如果序列格式支持），还是在单独的文件中，默认情况下为 GFF 格式。

entry: "boolean" ("N") 设置后，序列输入将包含输入序列或数据库条目的完整原始文本。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有序列输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行中使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

### A.5.2.16.1 关联限定符

sequence 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 限定符 | 描述 |
| --- | --- |
| sbegin: "integer" ("0") | 要使用的序列的开始位置 |
| send: "integer" ("0") | 要使用的序列的结束位置 |
| sreverse: "boolean" ("N") | 反向（如果是 DNA） |
| sask: "boolean" ("N") | 询问开始/结束/反向 |
| snucleotide: "boolean" ("N") | 序列是核苷酸 |
| sprotein: "boolean" ("N") | 序列是蛋白质 |
| slower: "boolean" ("N") | 转换为小写 |
| supper: "boolean" ("N") | 转换为大写 |
| sformat: "string" ("") | 输入序列格式 |
| sdbname: "string" ("") | 数据库名称 |
| sid: "string" ("") | 条目名 |
| ufo: "string" ("") | UFO 特征 |
| fformat: "string" ("") | 特征格式 |
| fopenfile: "string" ("") | 特征文件名 |

### A.5.2.17 seqall

type: "string" ("") 强制序列为给定类型。默认情况下接受任何序列类型。通常会设置 type: 属性，以便明确接受的输入序列类型。序列类型必须是标准序列类型（第 A.7 节，‘序列类型’）。

features: "boolean" ("N") 如果设置了 features: 属性，序列输入将包含特征信息，无论是在同一文件中（如果序列格式支持），还是在单独的文件中（默认情况下为 GFF 格式）。

entry: "boolean" ("N") 如果设置，序列输入将包含输入序列或数据库条目的完整原始文本。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有序列输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行中使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

minseqs: "integer" ("1") 要读取的最小序列数。默认情况下，最小可接受一个序列。

maxseqs: "integer" ("INT_MAX") 要读取的最大序列数。默认情况下，没有最大值。

### A.5.2.17.1 关联限定符

seqall 数据类型具有以下关联限定符，这些限定符可以作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 限定符 | 描述 |
| --- | --- |
| sbegin: "integer" ("0") | 要使用的序列的开始位置 |
| send: "integer" ("0") | 要使用的序列的结束位置 |
| sreverse: "boolean" ("N") | 反向（如果是 DNA） |
| sask: "boolean" ("N") | 询问开始/结束/反向 |
| snucleotide: "boolean" ("N") | 序列是核苷酸 |
| sprotein: "boolean" ("N") | 序列是蛋白质 |
| slower: "boolean" ("N") | 转换为小写 |
| supper: "boolean" ("N") | 转换为大写 |
| sformat: "string" ("") | 输入序列格式 |
| sdbname: "string" ("") | 数据库名称 |
| sid: "string" ("") | 条目名 |
| ufo: "string" ("") | UFO 特征 |
| fformat: "string" ("") | 特征格式 |
| fopenfile: "string" ("") | 特征文件名 |

### A.5.2.18 seqset

type: "string" ("") 强制序列集为给定类型。默认情况下接受任何序列类型。理想情况下，type: 属性应始终设置，以便始终明确接受的输入序列类型。序列类型必须是标准序列类型（第 A.7 节，‘序列类型’）。

aligned: "boolean" ("N") 如果设置，指定输入中的所有序列预期都是已比对的。如果为 false，则假定序列未比对，并简单地一起读入内存进行处理。我们建议始终定义 aligned: 属性，以便明确定义序列集的性质。

features: "boolean" ("N") 如果设置了 features: 属性，序列输入将包含特征信息，无论是在同一文件中（如果序列格式支持），还是在单独的文件中（默认情况下为 GFF 格式）。

entry: "boolean" ("N") 如果设置，序列输入将包含输入序列或数据库条目的完整原始文本。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有序列输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行中使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无序列输入）作为仅偶尔需要序列输入的程序的默认值。如果在命令行中指定了空字符串，则将生成标准默认值。结合 nullok: 和 missing: 属性，这允许限定符默认为空，并从命令行打开。





minseqs: "integer" ("1") 要读取的最小序列数。默认情况下，最少可接受一个序列。

maxseqs: "integer" ("INT_MAX") 要读取的最大序列数。默认情况下，没有最大值。

### A.5.2.18.1 关联限定符

seqset 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 限定符 | 类型/默认值 | 描述 |
|---|---|---|
| sbegin | "integer" ("0") | 要使用的序列起始位置 |
| send | "integer" ("0") | 要使用的序列结束位置 |
| sreverse | "boolean" ("N") | 反向（如果是 DNA） |
| sask | "boolean" ("N") | 询问起始/结束/反向 |
| snucleotide | "boolean" ("N") | 序列为核苷酸 |
| sprotein | "boolean" ("N") | 序列为蛋白质 |
| slower | "boolean" ("N") | 转换为小写 |
| supper | "boolean" ("N") | 转换为大写 |
| sformat | "string" ("") | 输入序列格式 |
| sdbname | "string" ("") | 数据库名称 |
| sid | "string" ("") | 条目名 |
| ufo | "string" ("") | UFO 特征 |
| fformat | "string" ("") | 特征格式 |
| fopenfile | "string" ("") | 特征文件名 |

## A.5.2.19 seqsetall

type: "string" ("") 强制序列集为给定类型。默认情况下接受任何序列类型。理想情况下应设置 type: 属性，以明确接受的输入序列类型。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

aligned: "boolean" ("N") 如果为 true，则指定输入中的所有序列预期已比对。如果为 false，则假设序列未比对，并简单地一起读入内存进行处理。理想情况下应始终设置 aligned: 属性，以明确定义序列集的性质。

features: "boolean" ("N") 如果设置，序列输入将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

entry: "boolean" ("N") 如果设置，序列输入将包含输入序列或数据库条目的完整原始文本。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在没有序列输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无序列输入）作为仅偶尔需要序列输入的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并可从命令行打开。

minsets: "integer" ("1") 要读取的最小序列集数。默认情况下，最少可接受一个序列集。

maxsets: "integer" ("INT_MAX") 要读取的最大序列集数。默认情况下，没有最大值（整数大小的系统限制除外）。

minseqs: "integer" ("1") 要读取的最小序列数。默认情况下，最少可接受一个序列。

maxseqs: "integer" ("INT_MAX") 要读取的最大序列数。默认情况下，没有最大值。

### A.5.2.19.1 关联限定符

seqsetall 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
|---|---|
| sbegin: "integer" ("0") | 要使用的序列起始位置 |
| send: "integer" ("0") | 要使用的序列结束位置 |
| sreverse: "boolean" ("N") | 反向（如果是 DNA） |
| sask: "boolean" ("N") | 询问起始/结束/反向 |
| snucleotide: "boolean" ("N") | 序列为核苷酸 |
| sprotein: "boolean" ("N") | 序列为蛋白质 |
| slower: "boolean" ("N") | 转换为小写 |
| supper: "boolean" ("N") | 转换为大写 |
| sformat: "string" ("") | 输入序列格式 |
| sdbname: "string" ("") | 数据库名称 |
| sid: "string" ("") | 条目名 |
| ufo: "string" ("") | UFO 特征 |
| fformat: "string" ("") | 特征格式 |
| fopenfile: "string" ("") | 特征文件名 |

## A.5.2.20 tree

size: "integer" ("0") 输入文件中的树的数量。有些只能接受单棵树，因此对于这些，值应设置为 "1"。值为 "0" 表示可接受任意数量的树。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在没有树输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

### A.5.2.20.1 关联限定符

tree 数据类型没有关联限定符。

## A.5.3 输出属性描述

### A.5.3.1 align

minseqs: "integer" ("1") 输出比对中预期的最小序列数。

minseqs: 和 maxseqs: 属性可用于验证应用程序输出，例如，在命令行上使用 -aformat 限定符选择格式时。

maxseqs: "integer" ("INT_MAX") 输出比对中预期的最大序列数。

minseqs: 和 maxseqs: 属性可用于验证应用程序输出，例如，在命令行上使用 -aformat 限定符选择格式时。

multiple: "boolean" ("N") 如果输出可以包含来自同一输入的多个比对，则应设置为 "Y"。

type: 序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以明确输出序列类型。

taglist: "string" ("") 定义要为比对序列从内部特征表中报告的其他标记。标记名称和类型必须与应用程序源代码匹配。每个标记的格式为 type:tagname[=columnname]，例如 int:length 或 string:gc=GC%。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在不生成比对输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无比对文件）作为仅偶尔需要比对文件的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。

#### A.5.3.1.1 关联限定符

align 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
|---|---|
| aformat: "string" ("") | 比对格式 |
| aextension: "string" ("") | 文件名扩展名 |
| adirectory: "string" ("") | 输出目录 |
| aname: "string" ("") | 基础文件名 |
| awidth: "integer" ("0") | 比对宽度 |
| aaccshow: "boolean" ("N") | 在标题中显示登录号 |
| adesshow: "boolean" ("N") | 在标题中显示描述 |
| ausashow: "boolean" ("N") | 在比对中显示完整 USA |
| aglobal: "boolean" ("N") | 在比对中显示完整序列 |

align 数据类型有两个关联限定符（-aformat 和 -aglobal），这些限定符通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。aformat: 定义 -aformat 限定符的默认值，即默认比对格式。aglobal: 定义 -aglobal 限定符的默认值，对于生成全局比对的程序，应将其设置为 "Y"。

### A.5.3.2 featout

- name: "string" ("") 输出文件的基本名称。优先使用 -ofname（见下文）。
- extension: "string" ("") 输出文件的扩展名。优先使用 -oformat（见下文）。
- type: "string" ("") 定义特征输出是 "protein" 还是 "nucleotide"。基于任何输入序列的类型有一个默认值，但应始终指定一个值。
- multiple: "boolean" ("N") 如果特征注释针对多个序列，则应设置为 "Y"。
- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在不生成特征输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。
- nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无特征输出）作为仅偶尔需要特征输出的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并可从命令行打开。





### A.5.3.2.1 关联限定符

The featout datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| oformat: "string" ("") | 输出特征格式 |
| ofopenfile: "string" ("") | 特征文件名 |
| ofextension: "string" ("") | 文件名扩展名 |
| ofdirectory: "string" ("") | 输出目录 |
| ofname: "string" ("") | 基础文件名 |
| ofsingle: "boolean" ("N") | 每个条目单独文件 |

The featout datatype has two associated qualifiers (-oformat and -ofname) which are often hard-coded as attributes in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the feature format and default file extension. ofname: defines the default value for the -ofname qualifier which is the default base file name

### A.5.3.3 outcodon

- name: "string" ("") 输出文件名的基本名称。
- extension: "string" ("") 输出文件名的扩展名。
- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成密码子输出的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。
- nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.3.1 关联限定符

The outcodon datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | 输出目录 |
| oformat: "string" ("") | 特定于此数据类型的输出格式 |

The outcodon datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format.

### A.5.3.4 outcpdb

extension: "string" ("") 输出文件名的扩展名。extension: 属性将默认为输出文件格式。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成坐标文件输出的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.4.1 关联限定符

The outcpdb datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | 输出目录 |
| oformat: "string" ("") | 特定于此数据类型的输出格式 |

The outcpdb datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.5 outdata

type: "string" ("") 定义输出数据类型。建议始终定义一个值以使输出数据类型清晰。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成格式化数据输出的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.5.1 关联限定符

The outdata datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | 输出目录 |
| oformat: "string" ("") | 特定于此数据类型的输出格式 |

The outdata datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.6 outdir

- fullpath: "boolean" ("N") 如果设置为 "Y"，则在将路径传递给程序时要求指定完整路径，尽管用户可以提供相对于当前工作目录的路径。

- extension: "string" ("") 写入目录的所有文件的默认扩展名。

- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在没有输出目录的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

- nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.6.1 关联限定符

The outdir datatype has no associated qualifiers.

### A.5.3.7 outdiscrete

- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成输出文件的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

- nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.7.1 关联限定符

The outdiscrete datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | 输出目录 |
| oformat: "string" ("") | 特定于此数据类型的输出格式 |

## A.5 数据类型特定属性

The outdiscrete datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.8 outdistance

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成距离矩阵文件的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.8.1 关联限定符

The outdistance datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | 输出目录 |
| oformat: "string" ("") | 特定于此数据类型的输出格式 |

The outdistance datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.9 outfreq

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成输出频率文件的情况下运行，则 nullok: 属性必须设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.9.1 关联限定符

The outfreq datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described elsewhere (see the EMBOSS User's Guide):


odirectory: "string" ("") 输出目录

oformat: "string" ("") 特定于该数据类型的输出格式

outfreq 数据类型具有一个与数据类型关联的命令行限定词 (-oformat)，该限定词通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。oformat: 定义了 -oformat 限定词的默认值，即文件格式和默认文件扩展名。

## A.5.3.10 outfile

name: "string" ("") 输出文件的基本名称。默认情况下，将使用任何输入文件或序列名称。如果迄今未处理任何输入文件，则默认名称为 "outfile"。

extension: "string" ("") 输出文件的扩展名。

append: "boolean" ("N") 如果设置，指定将输出追加到现有输出文件的末尾。默认情况下，输出文件将被覆盖。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成输出文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无输出文件）作为默认值，用于仅偶尔需要输出文件的程序。示例包括原始输出格式可用的程序，通常适用于仍需要它用于在自动化脚本中解析的用户。结合 nullok: 和 missing: 属性，这允许限定词默认为空，并可从命令行启用。

knowntype: 全局属性（第 A.4 节，“全局属性”）应始终定义。如果输出不是任何标准 EMBOSS 已知类型，则建议将 ApplicationName output 作为推荐值。

### A.5.3.10.1 关联限定词

outfile 数据类型具有以下可能作为属性硬编码在 ACD 文件中的关联限定词。这些限定词在 EMBOSS 用户指南中有描述：

- odirectory: "string" ("") 输出目录

## A.5.3.11 outfileall

name: "string" ("") 输出文件的基本名称。默认情况下，将使用任何输入文件或序列名称。如果迄今未处理任何输入文件，则默认名称为 "outfile"。

extension: "string" ("") 输出文件的扩展名。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成输出文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无输出文件）作为默认值，用于仅偶尔需要输出文件的程序。示例包括原始输出格式可用的程序，通常适用于仍需要它用于在自动化脚本中解析的用户。结合 nullok: 和 missing: 属性，这允许限定词默认为空，并可从命令行启用。knowntype: 全局属性（第 A.4 节，“全局属性”）应始终定义。如果输出不是任何标准 EMBOSS 已知类型（第 A.4 节，“全局属性”），则 "ApplicationName output" 是推荐值。

### A.5.3.11.1 关联限定词

outfileall 数据类型具有以下可能作为属性硬编码在 ACD 文件中的关联限定词。这些限定词在 EMBOSS 用户指南中有描述：

- odirectory: "string" ("") 输出目录

## A.5.3.12 outmatrix

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成矩阵文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无数据输出）作为默认值，用于仅偶尔需要数据输出的程序。如果在命令行上指定空字符串，则将生成标准默认值。结合 nullok: 和 missing: 属性，这允许限定词默认为空，并可从命令行启用。

### A.5.3.12.1 关联限定词

outmatrix 数据类型具有以下可能作为属性硬编码在 ACD 文件中的关联限定词。这些限定词在 EMBOSS 用户指南中有描述：

- odirectory: "string" ("") 输出目录
- oformat: "string" ("") 特定于该数据类型的输出格式

outmatrix 数据类型具有一个与数据类型关联的命令行限定词 (-oformat)，该限定词通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。oformat: 定义了 -oformat 限定词的默认值，即文件格式和默认文件扩展名。

## A.5.3.13 outmatrixf

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成矩阵文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无数据输出）作为默认值，用于仅偶尔需要数据输出的程序。如果在命令行上指定空字符串，则将生成标准默认值。结合 nullok: 和 missing: 属性，这允许限定词默认为空，并可从命令行启用。

### A.5.3.13.1 关联限定词

outmatrixf 数据类型具有以下可能作为属性硬编码在 ACD 文件中的关联限定词。这些限定词在 EMBOSS 用户指南中有描述：

- odirectory: "string" ("") 输出目录
- oformat: "string" ("") 特定于该数据类型的输出格式

outmatrixf 数据类型具有一个与数据类型关联的命令行限定词 (-oformat)，该限定词通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。oformat: 定义了 -oformat 限定词的默认值，即文件格式和默认文件扩展名。

## A.5.3.14 outproperties

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成属性文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无数据输出）作为默认值，用于仅偶尔需要数据输出的程序。如果在命令行上指定空字符串，则将生成标准默认值。结合 nullok: 和 missing: 属性，这允许限定词默认为空，并可从命令行启用。

### A.5.3.14.1 关联限定词

outproperties 数据类型具有以下可能作为属性硬编码在 ACD 文件中的关联限定词。这些限定词在 EMBOSS 用户指南中有描述：

- odirectory: "string" ("") 输出目录
- oformat: "string" ("") 特定于该数据类型的输出格式

outproperties 数据类型具有一个与数据类型关联的命令行限定词 (-oformat)，该限定词通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。oformat: 定义了 -oformat 限定词的默认值，即文件格式和默认文件扩展名。




## A.5.3.15 outscop

- **nullok:** "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成输出文件的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

- **nulldefault:** "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.15.1 关联限定符

outscop: 数据类型具有以下可能在 ACD 文件中硬编码为属性的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

- **odirectory:** "string" ("") 输出目录

- **oformat:** "string" ("") 特定于此数据类型的输出格式

outscop 数据类型具有一个与数据类型关联的命令行限定符 (-oformat)，该限定符通常在 ACD 文件中硬编码为属性（参见 *EMBOSS 用户指南*）。oformat : 定义 -oformat 限定符的默认值，即文件格式和默认文件扩展名。

## A.5.3.16 outtree

- **name:** "string" ("") 输出文件的基本名称。

- **extension:** "string" ("") 输出文件的扩展名。

- **nullok:** "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成系统发育树的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

- **nulldefault:** "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无数据输出）作为仅偶尔需要数据输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.16.1 关联限定符

outtree: 数据类型具有以下可能在 ACD 文件中硬编码为属性的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

- **odirectory:** "string" ("") 输出目录

- **oformat:** "string" ("") 特定于此数据类型的输出格式

outtree 数据类型具有一个与数据类型关联的命令行限定符 (-oformat)，该限定符通常在 ACD 文件中硬编码为属性（参见 *EMBOSS 用户指南*）。oformat : 定义 -oformat 限定符的默认值，即文件格式和默认文件扩展名。

## A.5.3.17 report

- **multiple**: "boolean" ("N") 如果输出可以包含来自同一输入的多个报告，应将其设置为 "Y"。
- **precision**: "integer" ("3") 任何报告得分值的浮点精度。对于整数得分值，可以将其设置为 "0"。
- **type**: "string" ("") 当报告格式是标准特征表格式之一（参见 *EMBOSS 用户指南*）时，`type :` 属性定义报告输出是 "protein" 还是 "nucleotide"。基于任何输入序列的类型有一个默认值，但应始终指定一个值。
- **taglist**: "string" ("") 定义要从内部特征表中报告的其他标签。标签名称和类型必须与应用程序的源代码匹配。每个标签的格式为 `type:tagname [=columnname]`，例如 `int:length` 或 `string:gc=GC%`。
- **nullok**: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成报告输出的情况下运行，则必须将 `nullok :` 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 `-noFlag` 运行应用程序（其中 `Flag` 是数据定义标志）。
- **nulldefault**: "boolean" ("N") `nulldefault :` 属性会覆盖默认名称生成，并将空字符串（无报告输出）作为仅偶尔需要报告输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 `nullok :` 和 `missing :` 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.17.1 关联限定符

`report :` 数据类型具有以下可能在 ACD 文件中硬编码为属性的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

| Qualifier | Description |
|---|---|
| `rformat`: "string" ("") | 报告格式 |
| `rname`: "string" ("") | 基本文件名 |
| `rextension`: "string" ("") | 文件扩展名 |
| `rdirectory`: "string" ("") | 输出目录 |
| `raccshow`: "boolean" ("N") | 在报告中显示 accession 号 |
| `rdesshow`: "boolean" ("N") | 在报告中显示描述 |
| `rscoreshow`: "boolean" ("N") | 在报告中显示得分 |
| `rusashow`: "boolean" ("N") | 在报告中显示完整 USA |
| `rmaxall`: "integer" ("0") | 要报告的最大总命中数 |
| `rmaxseq`: "integer" ("0") | 对于单个序列要报告的最大命中数 |

`report` 数据类型有三个关联限定符（`-rextension`、`-rscoreshow` 和 `-rformat`），这些限定符通常在 ACD 文件中硬编码为属性（参见 *EMBOSS 用户指南*）。`rextension :` 属性设置 `-rextension` 限定符的默认值，通常为程序名。`rscoreshow:` 布尔属性指定特征得分值是否应出现在报告中。如果程序未设置得分，可以通过将值设置为 "N" 来排除默认 0.0 得分。`rformat:` 属性是必需的。它定义 `-rformat` 限定符的默认值，即报告格式。

## A.5.3.18 seqout

- name: "string" ("") 输出文件的基本名称。
- extension: "string" ("") 输出文件的扩展名。
- features: "boolean" ("N") 如果设置，序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。
- type: "string" ("") 输出序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以使输出序列类型清晰。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。
- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成序列输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。
- nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无序列输出）作为仅偶尔需要序列输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.18.1 关联限定符

seqout 数据类型具有以下可能在 ACD 文件中硬编码为属性的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

| Attribute | Description |
|---|---|
| osformat: "string" ("") | 输出序列格式 |
| osextension: "string" ("") | 文件扩展名 |
| osname: "string" ("") | 基本文件名 |
| osdirectory: "string" ("") | 输出目录 |
| osdbname: "string" ("") | 要添加的数据库名 |
| ossingle: "boolean" ("N") | 每个条目单独文件 |
| oufo: "string" ("") | UFO 特征 |
| offormat: "string" ("") | 特征格式 |
| ofname: "string" ("") | 特征文件名 |
| ofdirectory: "string" ("") | 输出目录 |

## A.5.3.19 seqoutall

- name: "string" ("") 输出文件的基本名称。





extension: "string" ("") 输出文件扩展名。

features: "boolean" ("N") 如果设置，序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

type: "string" ("") 输出序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以使输出序列类型清晰。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

minseqs: "integer" ("1") 输出文件中预期的最小序列数。

maxseqs: "integer" ("INT_MAX") 输出文件中预期的最大序列数。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成序列输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无序列输出）作为仅偶尔需要序列输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.19.1 关联限定符

seqoutall 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
| :--- | :--- |
| osformat: "string" ("") | 输出序列格式 |
| osextension: "string" ("") | 文件扩展名 |
| osname: "string" ("") | 基础文件名 |
| osdirectory: "string" ("") | 输出目录 |
| osdbname: "string" ("") | 要添加的数据库名称 |
| ossingle: "boolean" ("N") | 每个条目单独文件 |
| oufo: "string" ("") | UFO 特征 |
| oformat: "string" ("") | 特征格式 |
| ofname: "string" ("") | 特征文件名 |
| ofdirectory: "string" ("") | 输出目录 |

seqoutall 数据类型具有一个数据类型关联的命令行限定符 (-ossingle)，它通常在 ACD 文件中作为属性硬编码（参见 EMBOSS 用户指南）。ossingle: 定义 -ossingle 限定符的默认值，并可以设置为 "Y" 以将输出定向到多个序列文件。例如，EMBOSS 程序 seqretsplit 使用此属性将输入序列拆分为多个文件。

## A.5.3.20 seqoutset

name: "string" ("") 输出文件的基本名称。

extension: "string" ("") 输出文件扩展名。

features: "boolean" ("N") 如果设置，序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

type: "string" ("") 输出序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以使输出序列类型清晰。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

minseqs: "integer" ("1") 输出文件中预期的最小序列数。

maxseqs: "integer" ("INT_MAX") 输出文件中预期的最大序列数。

aligned: "boolean" ("N") 如果为 true，则指定输出中的所有序列预期是已比对的。如果为 false，则假设序列未比对。我们建议始终定义 aligned: 属性，以便明确定义序列集的性质。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成序列输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无序列输出）作为仅偶尔需要序列输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.20.1 关联限定符

seqoutset 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
| :--- | :--- |
| osformat: "string" ("") | 输出序列格式 |
| osextension: "string" ("") | 文件扩展名 |
| osname: "string" ("") | 基础文件名 |
| osdirectory: "string" ("") | 输出目录 |
| osdbname: "string" ("") | 要添加的数据库名称 |
| ossingle: "boolean" ("N") | 每个条目单独文件 |
| oufo: "string" ("") | UFO 特征 |
| oformat: "string" ("") | 特征格式 |
| ofname: "string" ("") | 特征文件名 |
| ofdirectory: "string" ("") | 输出目录 |

## A.5.4 选择属性描述

### A.5.4.1 列表

values: "string" ("") 包含选项标签和描述列表的字符串，这些标签和描述定义了用户可以选择的选项。delimiter: 和 codedelimiter: 属性指定如何将此字符串解析为单个列表项。

delimiter: "string" (";") values: 字符串中用于分隔列表项的字符。默认为分号 (;)。

codedelimiter: "string" (":") values: 字符串中用于将选项标签与其描述分开的字符。默认为冒号 :。

minimum: "integer" ("1") 所需的最小选择数。默认需要一个选择。

maximum: "integer" ("1") 允许的最大选择数。默认正好需要一个选择。较高的值允许多个选择。

header: "string" ("") 显示在选项列表上方的文本。

button: "boolean" ("N") 为界面开发人员提供。它有一个布尔值，用于建议列表在界面中最好表示为复选框或单选按钮（值为 "Y"），还是应使用文本框来输入值（"N"）。

casesensitive: "boolean" ("N") 定义用户输入是否必须匹配列表项的精确大小写。无论用户使用何种大小写，参数的值都将完全是相应列表值的内容。

### A.5.4.1.1 关联限定符

列表数据类型没有关联限定符。

### A.5.4.2 选择

values: "string" ("") 包含选项描述列表的字符串，这些描述定义了用户可以选择的选项。delimiter: 属性指定如何将此字符串解析为单个选择列表项。

delimiter: "string" (":") values: 字符串中用于分隔列表项的字符。默认为分号 (;)。

minimum: "integer" ("1") 所需的最小选择数。默认需要一个选择。

maximum: "integer" ("1") 允许的最大选择数。默认正好需要一个选择。较高的值允许多个选择。

header: "string" ("") 显示在选项列表上方的文本。

button: "boolean" ("N") 为界面开发人员提供。它有一个布尔值，用于建议列表在界面中最好表示为复选框或单选按钮（值为 "Y"），还是应使用文本框来输入值（"N"）。

casesensitive: "boolean" ("N") 定义输入是否必须匹配列表项的精确大小写。无论用户使用何种大小写，参数的值都将完全是相应列表值的内容。

**注意**
所有数据类型定义的 information: 属性定义在列表或选择类型列表后用作提示的文本。

### A.5.4.2.1 关联限定符

选择数据类型没有关联限定符。

## A.5.5 图形属性描述

### A.5.5.1 图表

`nullok: "boolean" ("N")` 如果应用程序可以接受此定义的空值，并且可以在不生成图形输出的情况下运行，则必须将 `nullok:` 属性设置为 `"Y"`。这允许省略默认值，或在命令行上使用 `-noFlag` 运行应用程序（其中 `Flag` 是数据定义标志）。

`nulldefault: "boolean" ("N")` 覆盖默认名称生成，并将空字符串（无图表）作为仅偶尔需要图表的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。

### A.5.5.1.1 关联限定符

`graph` 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

| 属性 | 描述 |
| :--- | :--- |
| `gprompt: "boolean" ("N")` | 图表提示 |
| `gdesc: "string" ("")` | 图表描述 |
| `gtitle: "string" ("")` | 图表标题 |
| `gsubtitle: "string" ("")` | 图表副标题 |
| `gxtitle: "string" ("")` | 图表 x 轴标题 |
| `gytitle: "string" ("")` | 图表 y 轴标题 |
| `goutfile: "string" ("")` | 非交互式显示的输出文件 |
| `gdirectory: "string" ("")` | 输出目录 |

`graph` 数据类型有四个关联限定符，通常在 ACD 文件中作为属性硬编码（参见 *EMBOSS 用户指南*）。`-gtitle`、`-gxtitle` 和 `-gytitle` 用于控制图表及其轴的标题，并通过属性 `gtitle:`、`gxtitle:` 和 `gytitle:` 设置。`goutfile:` 属性指定输出的基本文件名。例如，EMBOSS 程序 **tmap** 使用它将输出定向到命名文件，而不是默认名称（即读取的第一个输入序列的名称，如果有的话）。





### A.5.5.2 xygraph

multiple: "integer" ("1") multiple: 属性指定单个输出中多个 XY 图的数量。默认值为 1，但 ACD 文件中可以定义任何整数值。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成图形输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无图）作为仅偶尔需要图形的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。

### A.5.5.2.1 关联限定符

xygraph 数据类型具有以下可作为 ACD 文件中属性硬编码的关联限定符。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
| --- | --- |
| gprompt: "boolean" ("N") | 图形提示 |
| gdesc: "string" ("") | 图形描述 |
| gtitle: "string" ("") | 图形标题 |
| gsubtitle: "string" ("") | 图形副标题 |
| gxtitle: "string" ("") | 图形 x 轴标题 |
| gytitle: "string" ("") | 图形 y 轴标题 |
| goutfile: "string" ("") | 非交互式显示的输出文件 |
| gdirectory: "string" ("") | 输出目录 |

图形数据类型有四个常作为 ACD 文件中属性硬编码的关联限定符（参见 EMBOSS 用户指南）。-gtitle、-gxtitle 和 -gytitle 用于控制图形及其坐标轴的标题，并通过属性 gtitle:、gxtitle: 和 gytitle: 设置。goutfile: 属性指定输出的基本文件名。它用于将输出定向到指定文件，否则将使用读取的第一个输入序列的名称（如果有）作为默认值。

## A.6 计算属性

计算属性是特定于数据类型的属性，在处理数据定义后被赋值，例如，在从文件读取序列后。它们的值在 ACD 文件处理过程中自动计算。这允许数据定义引用其值取决于输入数据的属性。可用的计算属性在下表中汇总，并将在下面详细描述。

ACD 数据定义中计算属性的值通过 ACD 文件内的操作检索。这是通过在括号前使用 $() 语法来完成的，括号内包含参数名和属性名，如下所示：

```
$(ParameterName.CalculatedAttributeName)
```

### A.6.1 简单 ACD 数据类型

### A.6.1.1 字符串

length: integer
字符串的长度。

### A.6.2 输入 ACD 数据类型

### A.6.2.1 序列

### A.6.2.1.1 seqall

begin: integer
使用的第一个序列的起始位置。

end: integer
使用的第一个序列的结束位置。

length: integer
第一个序列的总长度。

protein: Y/N
布尔值，指示序列是否为蛋白质。

nucleic: Y/N
布尔值，指示序列是否为 DNA。

name: string
序列的名称/ID/访问号。

### A.6.2.1.2 seqset

begin: integer
序列选择的起始位置。

end: integer
序列选择的结束位置。

length: integer
序列集的最大长度。

protein: Y/N
布尔值，指示序列集是否为蛋白质。

nucleic: Y/N
布尔值，指示序列集是否为 DNA。

name: string
序列集的名称。

totweight: float
浮点数，一组序列的总权重。

count: integer
整数，集合中的序列数量。

### A.6.2.1.3 seqsetall

begin: integer
序列选择的起始位置。

end: integer
序列选择的结束位置。

length: integer
序列集的最大长度。

protein: Y/N
布尔值，指示序列集是否为蛋白质。

nucleic: Y/N
布尔值，指示序列集是否为 DNA。

name: string
序列集的名称。

totweight: float
浮点数，每组序列的总权重。

count: integer
整数，每组中的序列数量。

multicount: integer
整数，序列集的数量。

### A.6.2.1.4 sequence

begin: integer
使用的序列的起始位置。

end: integer
使用的序列的结束位置。

length: integer
序列的总长度。

protein: Y/N
布尔值，指示序列是否为蛋白质。

nucleic: Y/N
布尔值，指示序列是否为 DNA。

name: string
序列的名称/ID/访问号。

### A.6.2.2 序列特征

### A.6.2.2.1 特征

fbegin: integer
要使用的特征的起始位置。

fend: integer
要使用的特征的结束位置。

flength: integer
序列的总长度（fsize 是特征计数）。

fprotein: Y/N
特征表为蛋白质。

fnucleic: Y/N
特征表为核苷酸。

fname: string
特征表的名称。

fsize: integer
整数，特征数量。

### A.6.2.3 其他输入（非序列或特征）

### A.6.2.3.1 距离

distancesize: integer
距离行数。

replicates: Y/N
输入中发现的重复数据。

hasmissing: Y/N
发现缺失值（replicates = N）。

### A.6.2.3.2 频率

freqlength: integer
每组的频率值数量。

freqsize: integer
频率集的数量。

freqloci: integer
频率位点的数量。

freqgenedata: Y/N
基因频率数据。

freqcontinuous: Y/N
连续频率数据。

freqwithin: Y/N
物种内个体频率数据。

### A.6.2.3.3 属性

propertylength: integer
每组的属性值数量。

propertysize: integer
属性集的数量。

### A.6.2.3.4 正则表达式

length: integer
正则表达式的长度。

### A.6.2.3.5 树

treecount: integer
树的数量。

speciescount: integer
物种的数量。

hashlengths: Y/N
已定义分支长度。

## A.7 序列类型

所有序列 ACD 数据类型都有一个名为 `type:` 的属性。这用于限制 EMBOSS 将接受的序列类型，这并不奇怪。`type:` 属性将序列类型描述为单个标记。EMBOSS 初始化例程将尝试通过读取（第一个）序列并检查内容来确定类型。`type:` 属性的可能值在下表中列出。

表 A.6. ACD 序列类型

| 值 | 类型 | 间隙 | 歧义代码 | 转换 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| any | 核苷酸或蛋白质 | 移除 | 是 | `'?'=>'X'` | 任何有效序列 |
| gapany | 核苷酸或蛋白质 | 保留 | 是 | `'?'=>'X'` | 带间隙的任何有效序列 |
| dna | 仅核苷酸 | 移除 | 是 | `'?'=>'N'`<br>`'X'=>'N'`<br>`'U'=>'T'` | DNA 序列 |
| puredna | 仅核苷酸 | 移除 | 否 | `'U'=>'T'` | DNA 序列，仅碱基 ACGT |
| gapdna | 仅核苷酸 | 保留 | 是 | `'?'=>'N'`<br>`'X'=>'N'`<br>`'U'=>'T'` | 带间隙的 DNA 序列 |
| gapdnaphylo | 仅核苷酸 | 保留 | 是 | `'U'=>'T'` | 带间隙和查询的 DNA 序列 |
| rna | 仅核苷酸 | 移除 | 是 | `'?'=>'N'`<br>`'X'=>'N'`<br>`'T'=>'U'` | RNA 序列 |
| purerna | 仅核苷酸 | 移除 | 否 | `'T'=>'U'` | RNA 序列，仅碱基 ACGU |
| gaprna | 仅核苷酸 | 保留 | 是 | `'?'=>'N'`<br>`'X'=>'N'`<br>`'T'=>'U'` | 带间隙的 RNA 序列 |
| gaprnaphylo | 仅核苷酸 | 保留 | 是 | `'T'=>'U'` | 带间隙和查询的 RNA 序列 |

## 附录 A ACD 语法参考

| 值 | 类型 | 间隙 | 歧义代码 | 转换 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| nucleotide | 仅核苷酸 | 移除 | 是 | `'?'=>'N' 'X'=>'N'` | 核苷酸序列 |
| purenucleotide | 仅核苷酸 | 移除 | 否 | | 核苷酸序列，仅碱基 ACGTU |
| gapnucleotide | 仅核苷酸 | 保留 | 是 | `'?'=>'N' 'X'=>'N'` | 带间隙的核苷酸序列 |
| gapnucleotidephylo | 仅核苷酸 | 保留 | 是 | | 带间隙和查询的核苷酸序列 |
| protein | 仅蛋白质 | 移除 | 是 | `'?'=>'X' '*'=>'X'` | 蛋白质序列 |
| pureprotein | 仅蛋白质 | 移除 | 否 | | 不含 BZ U X 或 * 的蛋白质序列 |
| stopprotein | 仅蛋白质 | 移除 | 是 | `'?'=>'X'` | 带可能终止密码子的蛋白质序列 |
| gapprotein | 仅蛋白质 | 保留 | 是 | `'?'=>'X' '*'=>'X'` | 带间隙的蛋白质序列 |
| gapstopprotein | 仅蛋白质 | 保留 | 是 | `'?'=>'X'` | 带间隙和可能终止密码子的蛋白质序列 |
| gapproteinphylo | 仅蛋白质 | 保留 | 是 | | 带间隙、终止密码子和查询的蛋白质序列 |
| proteinstandard | 仅蛋白质 | 移除 | 是 | `'?'=>'X' '*'=>'X' 'U'=>'X'` | 不含硒半胱氨酸的蛋白质序列 |
| stopproteinstandard | 仅蛋白质 | 移除 | 是 | `'?'=>'X' 'U'=>'X'` | 带可能终止密码子但不含硒半胱氨酸的蛋白质序列 |
| gapproteinstandard | 仅蛋白质 | 保留 | 是 | `'?'=>'X' '*'=>'X' 'U'=>'X'` | 带间隙但不含硒半胱氨酸的蛋白质序列 |





## A.8 操作

### A.8.1 操作类型

算术运算符为：

- @(a + b)（加法）
- @(a - b)（减法）
- @(a * b)（乘法）
- @(a / b)（除法）

逻辑运算符为：

- @(!a)（布尔非）
- @(a|b)（或）
- @(a&b)（与）

相等运算符为：

- @(token1==token2)（相等）
- @(token1!=token2)（不相等）
- @(token1<token2)（小于）
- @(token1>token2)（大于）

条件运算符为：

- @(boolval ? iftrue : iffalse)（如果）
- @(testval =A : 1 B : 2 else : 0)（情况）

### A.8.2 检索数据值

ACD 文件中给定数据定义的属性值可能取决于其他数据定义的值。可以检索以下内容的值：

- 数据定义（应用程序参数）
- 数据定义的属性
- 数据定义的计算属性
- ACD 变量定义。

此类值使用 ACD“获取值”语法检索，该语法由前面带有美元符号（$）并用括号括起来的 ParameterName.AttributeName 项组成：

```
$(ParameterName.AttributeName)
```

如果只检索数据定义的值，则省略 AttributeName 组件：

```
$(ParameterName)
```

也可以给出变量名。变量没有属性，因此语法为：

```
$(VariableName)
```

### A.8.3 计算和测试类型

可以在 ACD 中使用 @ 语法执行计算。计算可用于加、减、乘或除，或测试相等、不等、'大于'或'小于'。测试值可以是整数、浮点数和字符串。

每组括号只允许一个操作。这意味着在某些情况下需要两个或多个括号组。在这个嵌套操作示例中，需要两个括号组，第一个围绕 a 和 b 的加法，结果为 @(a + b)。第二个围绕将 @(a + b) 加到 c，结果为 @(@(a + b)+c)：

```
integer: n
{
default: "@(@(a + b)+c)"
}
```

但是，当需要多个操作时，通常会使用内部 ACD 变量来保存中间结果。

#### A.8.3.1 算术运算

支持的算术运算为加法、减法、乘法和除法。算术运算使用标准字符：+、-、* 和 /：

```
@(a + b) (Addition)
@(a - b) (Subtraction)
@(a * b) (Multiplication)
@(a / b) (Division)
```

操作数 a 和 b 必须解析为数值（整数或浮点数），否则结果未定义，但很可能在 ACD 处理过程中导致错误。

#### A.8.3.2 相等性测试

支持的相等性测试（括号中的符号）为“相等”（==）、“不相等” (!=)、“小于”（<）和“大于”（>）：

```
@(token1 == token2) (Equality)
@(token1 != token2) (Non-equality)
@(token1 < token2) (Less-than)
@(token1 > token2) (Greater-than)
```

上述相等性测试可用于字符串，在这种情况下将使用字符串的字典排序顺序。

#### A.8.3.3 布尔测试

支持的布尔运算为逻辑 AND、逻辑 OR 和逻辑 NOT。同样使用标准字符：&、| 和 !：

```
@(!a) (NOT)
@(a|b) (OR)
@(a&b) (AND)
```

在以下示例中，仅当 fubar 的值为 3 或 7 时，才会提示输入整数 rtfm。每个相等性测试都是一个计算，布尔测试是另一个计算。因此有三个 @() 实例：

```
integer: rtfm
{
    standard: "@($(fubar) == 3) | @($(fubar) == 7)) "
    etc
}
```

### A.8.4 条件语句

ACD 中有三种条件语句：一元、三元和 case 类型。

#### A.8.4.1 一元条件语句

一元条件语句的典型用途是开启或关闭提示。

在以下示例中，如果序列是蛋白质，则 window 的提示实际上被关闭（有关否定的更多信息，请参见第 4.5 节“控制提示”）：

```
sequence: sequence
{
    parameter: "Y"
    type: gapany
}
integer: window
{
    standard: "$(sequence.protein)"
    etc
}
```

#### A.8.4.2 三元条件语句

三元条件语句的一般形式为：

```
@(conditional ? value-if-true : value-if-false)
```

它们在为应用程序设置两种不同的使用模式时很有用，例如在排列程序中为蛋白质和核酸设置不同的间隙罚金值。

在以下示例中，penalty 对于蛋白质设置为 14，对于核酸设置为 16：

```
integer: penalty
{
   standard: "N"
   default: "@($(sequence.protein) ? 14 : 16)"
   etc
}
```

#### A.8.4.3 Case 条件语句

它们的一般形式为：

```
@(testval=poss_valA : ass_valA
   poss_valB : ass_valB
   else : default_val)
```

测试值（testval）与可能值列表（poss_valA 等）进行比较。如果找到匹配项，则操作将解析为与该可能值关联的结果（ass_valB 等）。测试值被解析为字符串，如果没有可能值匹配，则操作将解析为默认结果（default_val）。else : default 值对是可选的，如果未定义，则按需要使用默认值 NULL。

如果测试值无法明确分配给单个关联值，则操作将解析为匹配其可能值的最后一个关联值。

### A.8.5 变量的使用

变量用于保存部分计算或值，可以使您的 ACD 文件保持整洁。它们的一般语法为：

```
VariableName : Variable value
```

例如，以下是确定序列窗口最大大小的计算：

```
integer: start
{
   standard: "Y"
   maximum: "@(@($(sequence.length) - $(window)) + 1)"
}
```

可以通过将其中一个计算存储为部分结果来整理，如下所示：

```
variable: lminusw "@($(sequence.length) - $(window))"
integer: start
{
  standard: "Y"
  maximum: "@($(lminusw) + 1)"
}
```

#### A.8.5.1 自动变量

目前只有一个这样的变量（acdprotein），它根据读取的第一个序列的类型设置为 true 或 false。

# 附录 B C 编程库

EMBOSS 包含广泛的 C 编程库（AJAX 和 NUCLEUS）。这些库包含用于应用程序开发的 C 数据结构和函数，以及可用于扩展库自身核心功能的静态数据结构和函数。AJAX 提供低级功能，例如数组和字符串处理。NUCLEUS 包含用于更高级别任务的代码，例如序列排列算法。

### B.1 库文档

AJAX 和 NUCLEUS 的文档可在 EMBOSS 网站上找到，适用于 CVS（开发者）版本和稳定版的主要版本。

| CVS（开发者）版本文档 | http://emboss.open-bio.org/rel/dev/libs/ |
| 稳定版 6 文档 | http://emboss.open-bio.org/rel/rel6/libs |

### B.2 SRS 中的源代码

库源代码在 EBI SRS 服务器的 SRS 中编入索引：http://srs.ebi.ac.uk 对象（C 数据结构）和函数有单独的 SRS 数据库：

| EFUNC：CVS（开发者）版本中的函数 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EFUNC |
| EDATA：CVS（开发者）版本中的对象 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EDATA |
| EFUNCREL：稳定版 6.0.0 中的函数 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EFUNCREL |
| EDATAREL：稳定版 6.0.0 中的对象 | http://srs.ebi.ac.uk/srs7bin/cgi-bin/wgetz?-newId+-page+LibInfo+-lib+EDATAREL |

### B.3 AJAX 库文件

| 主题 | 库文件 | 简短描述 |
| :--- | :--- | :--- |
| AJAX 数据库读取库 | | |
| 序列数据库 | ajseqdb | 定义序列数据库读取对象（SeqSAccess）以及用于处理序列数据库访问所有方面的静态数据结构和函数。 |
| AJAX 图形库 | | |
| 图形输出 | ajgraph | 您可能需要用于绘图和打印图表的所有基本函数。 |
| 直方图图形函数 | ajhist | 定义直方图对象（AjPHist）用于处理直方图，其中包括直方图数据对象（AjPHistdata）。它包含用于处理直方图的基本函数。 |
| 图形输出 | ajgraphstruct | 用于处理图表的对象，包括基本图表对象（AjPGraph）和 PLplot 图表数据对象（AjPGraphdata）。 |
| AJAX ACD 库 | | |
| AJAX 命令定义 | ajacd | ajAcdGet* 函数系列，用于返回应用程序 ACD 文件中数据定义的 AJAX 对象。 |
| AJAX 核心库文件 | | |
| 排列 | ajalign | 定义主要排列对象（AjPAlign）。它可用于通过 ACD 文件处理检索输入序列排列。您处理序列排列所需的大多数函数。 |
| 数组处理 | ajarr | 用于处理动态数组的各种对象和函数。 |
| 断言函数 | ajassert | 用于处理断言的函数。 |
| 基码函数 | ajbase | 用于核苷酸碱基字符转换以及用于分子序列的其他字符转换函数。 |
| 调用注册函数 | ajcall | 用于允许访问不同图形包的函数，以防将来实现 PLplot 的替代方案。 |





| 描述 | 模块 | 详细信息 |
|---|---|---|
| 密码子分析函数 | ajcod | 定义 AjPCod 对象及用于处理密码子使用表的函数。 |
| DNA 熔解函数 | ajdan | 用于计算核苷酸序列属性的函数，大多与 DNA 熔解/退火有关。 |
| Domainatrix 函数 | ajdmx | 用于处理结构的对象和函数，供某些 EMBASSY 应用程序使用。 |
| DOM 解析器 | ajdom | DOM XML 解析器函数 |
| 域函数 | ajdomain | 定义 scop 对象 (AjPScop)、cath 对象 (AjPCath) 和通用域分类对象 (AjPDomain) 对象，用于存储蛋白质结构域数据。用于处理蛋白质域数据的函数，包括读取 SCOP 和 CATH 域分类数据库可解析文件以及读取和写入 DCF（域分类文件）格式文件。 |
| 异常处理 | ajexcept | 包含用于引发异常的 ajExceptRaise 函数。 |
| 特征表函数 | ajfeat | 通用特征处理所需的大多数函数。 |
| 文件处理 | ajfile | 用于处理数据文件、常规文件和目录的对象和函数，以及用于在低级别操作它们的静态函数。 |
| 数据文件处理 | ajfiledata | 数据文件处理。 |
| 文件 I/O 处理 | ajfileio | 文件输入/输出处理。 |
| 格式化输出 | ajfmt | 用于字符串格式化的函数。这些函数类似于 C 函数 printf、fprintf 等，但转换说明符和其他功能的集合已扩展。 |
| 索引函数 | ajindex | 数据库索引函数。 |
| Java 函数 | ajjava | Java 函数。 |
| 列表 | ajlist | 你可能需要用于创建和控制链表的所有函数。它们定义了基本列表对象 (AjPList)，其中包括作为嵌套子结构的列表节点对象 (AjPListNode) 和列表迭代对象 (AjIList)。 |
| 数学实用程序 | ajmath | 用于四舍五入数字、坐标转换、随机数生成等的常规数学函数。 |

## B.3 AJAX 库文件

| 描述 | 模块 | 详细信息 |
|---|---|---|
| 比较矩阵函数 | ajmatrices | 定义 AjPMatrix 和 AjPMatrixf 对象及用于处理比较矩阵的函数。 |
| 内存分配 | ajmem | 内存分配。 |
| 消息处理 | ajmess | 定义错误消息对象 (AjPError) 和用于消息处理的函数。 |
| 名称：变量和数据库定义 | ajnam | 用于 EMBOSS 系统变量和数据库定义的对象和函数。 |
| Nexus 数据函数 | ajnexus | 用于解析 NEXUS 文件格式的函数和对象（包括静态数据结构和函数）。 |
| 模式函数 | ajpat | 定义序列模式列表对象 (AjPPatlistSeq) 和通用模式列表对象 (AjPPatlistRegex) 以及用于处理正则表达式模式列表的函数。 |
| 蛋白质数据库数据函数 | ajpdb | 蛋白质数据库数据函数。 |
| 蛋白质数据库数据 I/O 函数 | ajpdbio | 蛋白质数据库数据输入/输出函数。 |
| 系统发育数据函数 | ajphylo | 定义用于处理系统发育数据的对象和函数。 |
| 序列范围函数 | ajrange | 定义范围规范对象 (AjPRange) 和用于处理范围规范的函数。 |
| 正则表达式 | ajreg | 定义正则表达式对象 (AjPRegexp) 和用于处理正则表达式的函数。 |
| 特征报告函数 | ajreport | 定义 AjPReport 对象和用于处理报告的函数。 |
| 序列 | ajseq | 通用序列处理所需的大多数函数。定义用于序列转换的 AjPSeqCvt 对象。 |
| 序列 ABI 痕迹 | ajseqabi | 提供用于从 ABI 痕迹文件解析序列（和其他数据）的函数。 |
| 序列读取 | ajseqread | 用于处理序列查询和序列输入对象以及一些常规序列处理函数的函数。 |
| 序列类型 | ajseqtype | 用于处理序列类型的函数。静态数据结构和函数用于 |
| **序列写入** | ajseqwrite | 定义序列输出对象 (AjPSeqout) 和用于将序列写入文件的函数。定义用于在低级别处理序列输出（在支持的格式中）的静态数据结构和函数。 |
| **排序实用程序函数** | ajsort | 用于对数组进行排序的函数（第 6.17.10 节，“对数组进行排序”）。 |
| **SQL** | ajsql | SQL 数据库访问。 |
| **字符串操作** | ajstr | 用于常规字符串处理的函数。定义基本字符串对象 AjPStr、字符串迭代对象 (AjIStr 和字符串标记解析器对象 (AjPStrTok) 以供与函数一起使用。 |
| **系统实用程序函数** | ajsys | 系统函数，大多用于文件和目录的低级处理以及特定于系统的函数。 |
| **表** | ajtable | 定义哈希表对象 (AjPTable) 和用于处理哈希表的函数。 |
| **时间函数** | ajtime | 时间函数。 |
| **序列翻译函数** | ajtranslate | 序列翻译对象 (AjPTrn) 和包含用于处理序列翻译的函数。 |
| **系统发育树函数** | ajtree | 创建和操作系统发育树。 |
| **实用程序** | ajutil | 干净退出、内存清理、操作字节等等。 |
| **数学向量函数** | ajvector | 用于处理 3D 空间中向量的数据结构和函数。 |
| **特定于系统的定义** | ajarch | 特定于系统的类型定义。 |
| **通用数据定义** | ajax | 主 AJAX 包含文件。 |
| **通用数据定义** | ajdefine | 通用类型定义。 |
| **特征表数据** | ajfeatdata | 用于常规用途的基本特征对象 (AjPFeattable, AjPFeature 和 AjPFeattabOut)，例如通过 ACD 文件处理检索特征。它还定义了用于低级特征输入处理的特征输入对象 (AjPFeattabIn)。 |
| **序列数据** | ajseqdata | 定义用于常规用途的基本序列对象 (AjPSeq, AjPSeqset 和 AjPSeqall)，例如检索序列 |

## B.4 NUCLEUS 库文件

| 描述 | 库文件 | 主题 |
|---|---|---|
| 比对 | embaln | 序列比对 |
| 注释 | embcom | 序列复杂度计算 |
| 共识序列 | embcons | 共识 |
| 数据文件实用程序 | embdata | 数据文件处理 |
| 使用 EMBL-CD 索引的数据库索引 | embdbi | 数据库索引 |
| Domainatrix 包算法 | embdmx | Domainatrix 方法 |
| 域算法 | embdomain | 域方法 |
| EST 算法 | embest | EST 方法 |
| 应用程序退出调用 | embexit | 退出方法 |
| 应用程序组 | embgroup | 组 |
| 等电点实用程序 | embiep | 蛋白质属性 |
| 使用 B+ 树的数据库索引 | embindex | 索引 |
| 初始化内部 | embinit | 初始化 |
| 比较矩阵 | embmat | 比较矩阵 |
| 杂项方法 | embmisc | 杂项方法 |
| 分子片段算法 | embmol | 分子片段 |
| N-mer (字) 算法 | embnmer | 字 (n-mer) 方法 |
| 模式匹配算法 | embpat | 模式匹配方法 |
| 模式列表文件读取 | embpatlist | 模式列表输入方法 |
| 蛋白质数据库 (PDB) 结构文件实用程序 | embpdb | 蛋白质数据库 |
| 蛋白质序列属性 | embprop | 序列属性 |
| 读取数据文件 | embread | 读取数据文件 |
| 以漂亮格式显示序列 | embshow | 显示 (显示) 方法 |
| 蛋白质域签名 | embsig | 签名方法 |
| 字匹配算法 | embword | 字方法 |
| 所有应用程序的包含文件 | emboss | 主包含文件 |

# 附录 C C 编码标准

### C.1 一般准则

EMBOSS C 编码标准总结如下。它们主要涉及代码布局、一些公认的 C 编程原则，以及编程 EMBOSS 对象（C 数据结构）和函数的技巧。编写 EMBOSS 代码时，应尽量遵循以下几条准则。

#### C.1.1 库的使用

毫无必要地编写代码非常浪费；通常所需功能在 AJAX 或 NUCLEUS 中已可用。编码前请检查库，并贡献任何新代码，以便将其纳入库中。

#### C.1.2 过度设计的代码

一个常见的错误是浪费时间实现你总有一天可能会用到但实际上永远不会用到的功能。过度设计的代码令人困惑且难以维护。只编写你今天需要的代码，但要设计你的代码，以便在必要时可以将来扩展。

#### C.1.3 重复代码

重复代码容易出错且难以维护。不要复制代码块，而是编写一个函数。当两个函数基本做同样的事情但参数不同时，让一个函数直接调用另一个函数。

#### C.1.4 管理代码变更

你的代码应该易于修改以实现新功能。如果你发现自己需要修改多个对象或函数来实现单一更改，那么你的数据模型或程序结构可能不理想。考虑定义一个包含所需元素的新对象或适当的新函数。

#### C.1.5 保持对象整洁

对象中每个元素的目的都应该很明显。包含很少使用或用于内务维护（例如保存临时


值，可能难以理解。检查您的代码，确定变量是否真的需要在对象中，或者是否最好移到其他地方。

### C.1.6 避免冗余

当两个或多个不同对象共享公共元素时，很可能存在在整个代码中删除冗余的空间。考虑是否创建一个封装公共元素的新对象，会使您的代码更易于理解和维护。

### C.1.7 管理您的变量

变量列表非常长的函数难以理解和维护。如果一组变量始终一起使用，请考虑将它们封装在新对象中，尤其是当该组在代码的其他地方出现时。

### C.1.8 长函数

大型函数难以理解。较小的函数更容易记录，因此程序员更容易识别。拆分为较小函数的功能更有可能被重用。考虑将大型函数分解为较小的函数。如果需要，保留带有原始名称的函数，该函数可以调用新的较小函数。不过，不要过度，并尽量避免过多层级的函数调用（参见第 C.1.10 节，“函数嵌套”）。

### C.1.9 长参数列表

参数众多的函数难以理解、使用和维护。尽可能传递对象指针，而不是单个对象的各个元素。如果参数不属于某个对象，请考虑定义一个新对象来封装它们，并传递指向该对象的指针。

### C.1.10 函数嵌套

使用深度嵌套函数链的代码可能极难理解。请在设计代码时避免这种情况。

## C.2 代码布局

### C.2.1 应用程序代码布局

使用以下顺序来布置应用程序 C 源代码：

- 1. 应用程序标准头部
- 2. 系统头文件包含
- 3. 本地头文件包含
- 4. 常量定义
- 5. 数据类型定义
- 6. 全局变量（尽量完全避免使用这些）
- 7. 函数原型
- 8. main() 函数
- 9. 函数。

myemboss 应用程序目录中提供了一个模板应用程序 C 源代码文件，例如：

```
../embassy/myemboss/src/template.c
```

文件如下所示：

```
** @source_ApplicationName_
**
** _ShortDescription_
**
** @author Copyright (C) _Year_ _AuthorName_
** @version _VersionNumber_ _description of version_
** @modified _EditDate_ _EditorName_ _description of edit_
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
*******************************************************************************/
/* ======================================================================= */
/* ======================================================================= */
/* ================= include files ======================================= */
/* ======================================================================= */
/* ======================================================================= */
#include "emboss.h"
/* Inclusion of system and local header files goes here */
/* ======================================================================= */
/* ======================================================================= */
/* ================= constants =========================================== */
/* ======================================================================= */
/* ======================================================================= */
/* #define and enum statements go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- global variables ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Global variables definitions go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- data ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Definition of datatypes go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- function prototypes ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Function prototypes for public (external) functions go here */

/* @prog __ApplicationName ***************************************************************
**
** __ShortDescription__
******************************************************************************************/

int main(int argc, char **argv)
{
}

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- functions ---------------------------------------------------------- */
/* ---------------------------------------------------------- */
```

### C.2.1.1 标准文件部分

文件 ../embassy/myemboss/src/template.c 中的标准部分如下总结。

### C.2.1.1.1 应用程序标准头部

所有应用程序源代码文件都必须以标准文档头部开始（参见附录 D，代码文档标准）。

### C.2.1.1.2 头文件包含

首先包含 EMBOSS 头文件 emboss.h，然后包含任何所需的系统文件。例如：

```
#include "emboss.h"
#include <limits.h>
#include <float.h>
```

emboss.h 包含 EMBOSS 头文件 ajax.h，后者包含以下内容：

```
#include <stdio.h>
#include <stdarg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

因此，无需在应用程序源代码中显式包含这些文件。

### C.2.1.1.3 常量定义

应将这些内容放在一个块中，并在必要时进行文档记录。例如：

```
#define TIMEOUT 30			/* Arbitrary pipe timeout (secs) */
#define TIMEBUFFER 256		/* Arbitrary length buffer for time printing */
#define PUTTIMEOUT 120		/* Max no. of secs to write a file */
#define R_BUFFER 2048		/* Arbitrary length buffer for reentrant syscalls */
```

或者：

```
enum blastdbtype [BLAST1P, BLAST1N, BLAST2P, BLAST2N] ;
```

### C.2.1.1.4 全局变量定义

除非绝对必要，否则不应使用全局变量。如果使用它们，应进行文档记录。

### C.2.1.1.5 数据类型定义

特定于应用程序的任何联合和 C 数据结构定义应接下来给出。所有数据类型都应采用 EMBOSS 风格定义。建议（但非强制要求）以标准方式记录应用程序数据结构（参见附录 D，代码文档标准）。

### C.2.1.1.6 函数原型

所有函数都必须使用完整的 ANSI C 样式进行原型声明。

### C.2.1.1.7 main() 函数

main 函数前带有标准文档头部（参见附录 D，代码文档标准）。main() 函数应放在其他函数之前。这样可以省去人们在找到它之前浏览许多函数的麻烦，还有助于避免意外的隐式函数声明。

### C.2.1.1.8 函数

函数应按其原型声明的顺序列出，并用空白（四个换行符）分隔。所有特定于应用程序的函数都应声明为 static，并以应用程序名称开头命名。理想情况下，所有应用程序函数都应以标准方式记录（参见附录 D，代码文档标准）。




## C.2.2 库代码布局

### C.2.2.1 库头文件

在头文件中，按以下顺序排列代码：

- 1. 标准预处理器指令
- 2. 包含系统头文件
- 3. 包含本地头文件
- 4. 常量定义
- 5. 公共（外部）数据类型定义
- 6. 公共（外部）函数的函数原型。

所有导出的原型定义必须由以下注释定义界定：

```
/*
** Prototype definitions
*/
... exported function prototypes here ...
/*
** End of prototype definitions
*/
```

这样做是为了允许提取信息以用于 Windows 编译。导出原型的函数名必须与其返回数据类型在同一行。

AJAX 和 NUCLEUS 目录中提供了一个模板头文件，例如：

```
.../emboss/ajax/core/template.h
```

该文件（AJAX 和 NUCLEUS 相同）如下所示：

```
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef LibraryFileName_h
#define LibraryFileName_h

/* ---------------------------------------------------------------- */
/* ---------------------------------------------------------------- include files ---------------------------------------------------------------- */
/* ---------------------------------------------------------------- */

/* Inclusion of system and local header files goes here */

/* ---------------------------------------------------------------- */
/* ---------------------------------------------------------------- constants ---------------------------------------------------------------- */
/* ---------------------------------------------------------------- */

/* #define and enum statements go here */

/* ============================================================ */
/* ===================== public data ========================== */
/* ============================================================ */

/* Definition of public (external) data types go here */

/* ============================================================ */
/* ===================== public functions ===================== */
/* ============================================================ */

/* Function prototypes for public (external) functions go here */

#endif
#ifdef __cplusplus
}
#endif
```

### C.2.2.2 库源文件

源文件请按以下顺序排列：

- 1. 标准库文档头
- 2. 包含系统头文件
- 3. 包含本地头文件
- 4. 常量定义
- 5. 全局变量定义（避免使用！）
- 6. 私有数据类型定义
- 7. 私有（静态）函数的函数原型
- 8. 函数定义。

AJAX 和 NUCLEUS 目录中提供了一个模板源文件，例如：

```
.../emboss/ajax/core/template.c
```

该文件如下所示：

```
** @source__AJAX or NUCLEUS____LibraryArea__functions
**
** __ShortDescription__
**
** @author Copyright (C) __Year____AuthorName__
** @version __VersionNumber____description of version__
** @modified __EditDate__ __EditorName__ __description of edit__
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
******************************************************************************/
/*
****************************************************************************** include files *****************************************************************************
/*
** Inclusion of system and local header files goes here */

/*
****************************************************************************** constants *****************************************************************************
/*
** #define and enum statements go here */

/*
****************************************************************************** global variables *****************************************************************************
/*
** Global variables definitions go here */

/*
****************************************************************************** private data *****************************************************************************
/*
** Definition of private datatypes go here */

/*
****************************************************************************** private functions *****************************************************************************
/*
** Function prototypes for private (static) functions go here */

/*
****************************************************************************** All functions by section *****************************************************************************
/*
** Functions definitions go here, organised into sections */
```

### C.2.2.3 标准文件节

库头文件和 C 源文件中的标准节总结如下。

#### C.2.2.3.1 标准预处理器指令

每个头文件 (*.h) 的内容都必须用标准预处理器指令（如下）括起来。LibraryFileName 是库文件的名称，例如 ajstr.h/c 中的 str：

```
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajLibraryFileName_h
#define ajLibraryFileName_h

/* Everything else goes here */

#endif
#ifdef __cplusplus
}
#endif
```

#### C.2.2.3.2 标准库文档头

标准文档头（参见附录 D，代码文档标准）应放在每个库源文件 (*.c) 的顶部。

#### C.2.2.3.3 包含头文件

编译所需的任何文件都应在任何实际代码之前包含。系统文件的包含应在本地文件之前。您绝不应使用嵌套包含。

#### C.2.2.3.4 常量定义

这些包括 #define 和 enum 语句，应以块形式给出并在必要时进行文档记录。

#### C.2.2.3.5 全局变量定义

全局变量在库源文件 (*.c) 中位于常量之后。如果全局变量的功能从其名称中不明显，则通常应加以注释。应尽可能避免使用它们。

#### C.2.2.3.6 数据类型定义

任何私有（应声明为 static）的联合体和 C 数据结构（对象）都在库源文件 (*.c) 中给出。任何公共（外部）联合体和结构体都在库头文件 (*.h) 中给出。所有数据类型都应按 EMBOS 风格定义（第 C.8 节，‘结构体和联合体’）。所有公共数据类型必须以标准方式记录（参见附录 D，代码文档标准）。私有结构体和联合体不需要此类文档，但建议添加。

#### C.2.2.3.7 函数原型

避免将名称导出到单个 C 源文件之外，即尽可能将每个函数（即任何未知为外部所需的函数）声明为 `static`（在库源文件 *.c 中）。所有函数都必须使用完整的 ANSI C 风格进行原型声明。

#### C.2.2.3.8 函数定义

函数在库源文件 (*.c) 中最后给出。所有公共函数都必须以标准方式记录（参见下文附录 D，*代码文档标准*）。私有函数不需要此类文档，但建议添加。

## C.2.3 易读性

您的代码应该易于阅读。这或许比代码实际运行更重要。如果代码易于阅读，那么至少其他人有机会修复它；而如果代码难以阅读，没有人能轻易修改或改进它。

### C.2.3.1 行长度

行通常不应超过 79/80 个字符，以避免屏幕上的换行（或打印输出时的过早行终止），这可能会令人困惑。如果这样做能使代码更易读，则允许例外。

### C.2.3.2 变量名

变量名不应太短或太长。过长的变量名会使代码难以阅读，过短的变量名会使代码难以理解。话虽如此，单个字符（i、j、k 等）用于标准循环计数器是可以的。请运用常识取得平衡。例如，如果您正在根据论文编写数学公式或算法，则使用与符号同名的变量。如果变量是临时变量，则在其名称中明确这一点。请考虑：

```
for (elementindex = 0; elementindex < DIMENSION; ++elementindex)
    printf("%d\n", element[elementindex]);

for (i = 0; i < DIMENSION; ++i)
    printf("%d\n", element[i]);
```

在第一个示例中，您需要阅读更多文本才能识别 `for` 循环惯用法，然后还需要更多努力来解析循环体。既然清晰是目标，名称应仅包含识别变量所需的必要和充分信息。但是，如果变量的声明和使用仅限于代码的一小部分本地区域，则信息性名称是不必要的。较长、更具信息性的名称通常适用于作用域较大的变量。





### C.2.3.3 大括号

匹配的大括号应出现在同一列，且缩进应保持一致。以下是良好的示例：

```c
int fred(void)
{
    ...
    for(i=0; i<LIMIT; ++i)
    {
        ...
    }
    return 0;
}
```

而以下示例则混乱不堪：

```c
int fred(void) {
    ...
    for(i=0; i<LIMIT; ++i) {
        ...
    }
    return 0;
}
```

以下示例同样混乱：

```c
int fred(void)
{
    ...
    for(i=0; i<LIMIT; ++i)
        {
        ...
        } ...
    return 0;
}
```

不要不必要地使用大括号。以下是良好的示例：

```c
for(i=0; i<LIMIT; ++i)
    sum += i;
```

但此代码显得杂乱：

```c
for(i=0; i<LIMIT; ++i)
{
    sum += i;
}
```

for 语句的主体应出现在与 for 语句本身分离的独立块中。如果嵌套在较大的代码体中，以下示例可能会令人困惑：

```
for (i=0; i<LIMIT; ++i) sum += i;
```

### C.2.3.4 缩进

推荐使用四个字符的缩进，但更重要的是保持一致。如果发现嵌套循环中的缩进导致许多行换行，则应检查代码结构是否可以改进。

可以在 `.emacs` 文件中添加一些行，这些行通常会自动将大括号放置在正确位置并正确缩进。它们可在文件 http://emboss.open-bio.org/downloads/EmacsConfig 中找到，如下所示：

```
(defun set-if-void (symbol value)
 (or (boundp symbol)
   (set symbol value)))

(require 'cc-mode)
(setq auto-mode-alist
   (append
     '(("\\.C$" . c++-mode)
       ("\\.H$" . c++-mode)
       ("\\.cc$" . c++-mode)
       ("\\.hh$" . c++-mode)
       ("\\.c$" . c-mode)
       ("\\.h$" . c-mode)
       ("\\.m$" . objc-mode)
       ("\\.java$" . java-mode))
     auto-mode-alist))

(defconst emboss-c-style
   '((c-tab-always-indent
     . t)
   (c-comment-only-line-offset
     . 0)
   (c-hanging-braces-alist
     . ((brace-list-open)))
   (c-hanging-colons-alist
     . ((member-init-intro before)
       (inher-intro)
       (case-label after)
       (label after)
       (label after)))
   (c-cleanup-list
   . (scope-operator
      empty-defun-braces
      defun-close-semi))

;; Uncomment the following line if you don't want newlines after semicolons
;;   (c-hanging-semi&comma-criteria)
   (c-offsets-alist
     . ((arglist-close . c-lineup-arglist)
        (substatement-open . 0)
        (case-label . 4)
        (block-open . 0)
        (knr-argdecl-intro . -))))

)
"EMBOSS C Programming Style")

;; Customisations for all of c-mode, c++-mode, and objc-mode
(defun emboss-c-mode-common-hook ()
 ;; add EMBOSS style and set it for the current buffer
(c-add-style "EMBOSS" emboss-c-style t)
;; offset customisations not in emboss-c-style
(c-set-offset 'member-init-intro '++)
;; other customisations
(setq tab-width 8
      ;; this will make sure spaces are used instead of tabs
      indent-tabs-mode nil)
;; auto-newline [for hungry-delete use (c-toggle-auto-hungry-state 1)]
(c-toggle-auto-state 1)

;; keybindings for C, C++, and Objective-C. Can put these in
;; c-mode-map because c++-mode-map and objc-mode-map inherit it
(define-key c-mode-map "\C-m" 'newline-and-indent)
)

(add-hook 'c-mode-common-hook 'emboss-c-mode-common-hook)
```

这还允许你使用 Emacs 命令 `M-x indent-region` 重新格式化现有代码（需要一些手动干预）。

## C.3 ANSI C 标准

EMBOSS C 源代码应遵循 ANSI C 标准（ANSI X3.159-1989 ‘Programming Language C’）。该语言版本通常称为‘ANSI C’、‘Standard C’ 或 ‘C89’。其语义在以下书籍中给出：

> The C Programming Language, 2nd edn
> Brian Kernighan and Dennis Ritchie
> Prentice Hall 1988; ISBN 0-13-110362-8

作为权威参考手册，请参见：

> C: A Reference Manual, 5th edn
> Samuel P. Harbison and Guy L. Steele
> Prentice Hall 2002; ISBN 0-13-089592-X.

该标准引入了：

- Function prototypes
- C++ style parameter declarations (argument types are specified in the function declarations)
- void pointers
- Support for international character sets and locales
- A more capable preprocessor
- Enumerated types (enum)
- Ability to pass structures to functions and have structures as return values.

其中大多数都是受欢迎的新增内容。在 EMBOSS 中，不推荐传递整个结构体，因为这可能会浪费栈内存且速度较慢。每个 EMBOSS 对象（C 数据结构）都有为其定义的指针，应使用该指针进行引用（见下文）。

如果需要编写系统相关代码，请尝试将此类函数放在单独的头文件中，以尽可能将其隔离。AJAX 库文件 `ajsys.c` 可能非常适合此类代码。请记住，你的代码需要在多种操作系统下工作，例如 Linux、Windows、MacOSX 等。

## C.4 预处理器的使用

每个头文件 (`*.h`) 的内容都必须用上面所示的预处理器指令括起来。

预处理器可用于：

- System-dependent code (but see the ajsys corollary above.)
- Commenting out code with `#if 0`
- Conditionals arising from system limits
- Definitions (`#define`); but consider `enum` or `static const` instead (see below).

由系统限制引起的条件编译示例：

```c
#include <limits.h>

#if INT_MAX > UCHAR_MAX
...
#else
#error "need int wider than char"
#endif
```

### C.4.1 常量

对于常量，请考虑使用 `enum` 和变量，而不是 `#define`，因为 `#define` 在调试器中很少可见。例如：

```c
enum { Red = 0xF00, Blue = 0x0F0, Green = 0x00F };
static const float pi = 3.14159265358;
```

### C.4.2 宏

宏应避免副作用。如果可能，每个参数只提及一次。为所有参数加上括号。当宏是表达式时，为整个宏体加上括号。如果宏是某个函数的内联展开，则将名称大写并以 `M` 开头：

```c
#define MAJFUBAR (X) \
(save = (X), \
dosomethingwith(X);
(X) = save);
```

尝试编写宏，使其在语法上是表达式，即你可以在其使用末尾加上分号。

## C.5 注释

避免在注释中使用花哨的布局或装饰。使用的样式如下：

```
/* single line comments look like this */

/*
** Important single line comments look like multi-line comments.
*/

/*
** Multi-line comments look like this. Put the opening and closing
** comment sequences on lines by themselves. Use complete sentences
** with proper English grammar, capitalisation and punctuation.
*/

/* but you don't need to punctuate or capitalise one-liners */
```

所有注释的开头斜杠 (`/`) 应缩进到与其适用的代码相同的级别，例如：

```c
if (fubar())
{
    /* Print a message before exiting. */
    ajFatal("Program is FUBAR");
}
```

避免将注释放在代码本身的同一行上。如果为了整洁而被认为是必需的，请使用空格将其与代码分开。尝试将此类注释缩进到同一列，并且不要跨多行继续：

```c
func1(); /* useless comment */
func2(); /* useless comment */
func3(); /* useless comment */
```

有关何时以及如何使用注释的指南，请参见第 3.1 节 ‘EMBOSS 编程’。

## C.6 变量

### C.6.1 全局变量

除非有非常充分的理由，否则不要使用它们，因为它们往往会使代码非常难以理解。然而，如果在某些情况下谨慎且明智地使用，它们可以大大简化代码。请自行判断。

### C.6.2 函数中的静态变量

此类函数不是可重入的，因此如果希望代码在多线程上下文中工作，请完全不要使用它们。偶尔有非常充分的理由使用它们，但否则应避免使用。

### C.6.3 变量声明

在每个函数的顶部声明所有变量。每行声明一个变量。如果数据类型和变量对齐，则更易于阅读。以下是整洁的示例：

```c
{
    ajint   a;
    ajint   b;
    ajlong  c;
    ...
}
```

而以下示例则混乱：

```c
{
    ajint a,b;
    ajlong c;
    ...
}
```

以下代码符合最新的 C 标准（C99），但不清晰（并且 C99 不受 EMBOSS 应运行的所有平台支持）：

```c
{
    .
    .
    .
        for (ajint a=0; a<b; a++)
    .
    .
    .
}
```

推荐的布局是：

```c
{
    ajint a;
    ajint b;
    ...
    for (a=0; a<b; a++)
    .
    .
}
```

### C.6.4 变量初始化

始终将对象指针变量初始化为 `NULL`。在 EMBOSS 中，不这样做有时可能有风险（参见第 5.3 节 ‘对象（C 数据结构）’）。在代码中根据需要初始化其他数据类型。对齐初始化语句以便于阅读：



```c
AjPStr seqsubstring = NULL;
AjPDouble xarray = NULL;
```

不要在声明中用函数进行初始化。切勿例如使用：

```c
AjPStr seqsubstring = ajStrNew();
```

## C.6.5 int、ajint、long 和 ajlong 的使用

为避免因变量大小取决于系统而引起的任何问题（参见第 5.1 节“基本数据类型”），EMBOSS 假设 ajint 通常为 32 位，ajlong 通常为 64 位（参见第 5.1 节“基本数据类型”）。如果 32 位足够，请使用 ajint 而非 int。请使用 ajlong 而非 long 或 long long。

将数据类型与您的需求相匹配。例如，如果您使用的是 Alpha 机器，那么 int 和 long 变量都将是 64 位。在这种情况下，不要出于懒惰而只使用 ajlong，因为您的代码在其他平台上运行会更慢。

在某些情况下，应使用标准 C 的 int 和 long，例如，作为 C 系统库函数的参数。

## C.7 运算符优先级

避免因依赖运算符优先级而引入的混淆。这可能会令人困惑：

```c
a = b * c + 1;
```

而这是清晰的：

```c
a = (b * c) + 1;
```

## C.8 结构体和联合体

### C.8.1 声明

库源文件中定义的所有应用程序数据类型和私有数据类型都应声明为 static。库头文件中声明的公共数据类型不应包含此关键字！

始终使用 EMBOSS 声明结构体和联合体的方法，即以所示方式使用 #define 和 typedef：

```c
typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

声明必须包含结构体名称（AjSStr）、对象名称（AjOStr）和指针名称（AjPStr），即使这些未被使用。在上述示例中，还定义了指向对象指针的指针（AjPPStr）。这是可选的，仅在需要时才应包含。

### C.8.2 命名约定

AJAX 公共（外部）结构体的命名约定如下：

| 结构体名称 | AjSName |
| 对象名称 | AjOName |
| 指针名称 | AjPName |

NUCLEUS 公共（外部）结构体的命名约定如下：

| 结构体名称 | EmbSName |
| 对象名称 | EmbOName |
| 指针名称 | EmbPName |

使用此约定，即指针的 P 前缀，可避免指针看起来像是一个独立对象的问题。

例如，这是命名方面的不良实践：

```c
typedef struct T *T;
...
T t;
```

从变量名无法看出 t 是一个指针。

私有结构体的命名约定去掉 Aj 和 Emb 前缀。无论在 AJAX、NUCLEUS 还是应用程序代码中，私有结构体均使用：

| 结构体名称 | SName |
| 对象名称 | OName |
| 指针名称 | PName |

例如：

```c
/* @datastatic PBlastType *****************************************************
**
** DbiBlast types
**
** @attr ExtT [const char*] Table filename extension
** @attr ExtH [const char*] Header filename extension
** @attr ExtS [const char*] Sequence filename extension
** @attr IsProtein [AjBool] true for protein
** @attr IsBlast2 [AjBool] blast2.x or blast 1.x
** @attr Type [ajint] enumerated type
** @attr Padding [char[4]] Padding to alignment boundary
********************************************************************************/;

typedef struct SBlastType
{
    const char* ExtT;
    const char* ExtH;
    const char* ExtS;
    AjBool    IsProtein;
    AjBool    IsBlast2;
    ajint     Type;
    char      Padding[4];
} OBlastType;

#define PBlastType OBlastType*
```

### C.8.3 数据类型文档

所有公共对象必须以标准方式记录（附录 D，*代码文档标准*）。用适当的空白（四个换行符）分隔各个对象。

## C.9 函数

### C.9.1 函数原型

库中的所有应用程序函数和私有函数都应声明为 `static`。库中的公共函数不应包含此关键字。

所有函数必须使用完整的 ANSI C 样式进行原型声明，并缩进以提高清晰度。例如：

```c
/**
** Prototype definitions
*/

void             ajListPushAppend (AjPList list, AjPListNode* tail);
AjPList          ajListNewListref (const AjPList list);
void             ajListExit       (void);
AjBool           ajListPeekFirst  (const AjPList thys, void** x);
void             ajListFree       (AjPList *list);
```

### C.9.2 隐式声明

示例如下：

```c
extern fubar(int x);
main(int argc, char **argv)
```

不要使用它们。始终指定函数应返回的内容。这样更好：

```c
extern int fubar(int x);
int main(int argc, char **argv)
```

### C.9.3 函数和参数名称

应用程序函数名称应：

- 以应用程序名称（小写）加下划线开头：applicationname_FunctionName
- 有意义
- 尽可能短
- 当名称包含多个单词时，使用“句子大小写”
- 仅使用字母字符（单个下划线除外）

例如：

```c
static void abiview_TextDisplay(AjPGraph graphs, ajint nstart, ajint nstop,
                                const AjPStr nseq, float tmax, float scale);
static ajint abiview_getResColour(char B);
```

库函数和函数参数名称遵循上述除第一条外的所有约定，此外：

- 所有 AJAX 公共（外部）函数应以 aj 开头
- 所有 NUCLEUS 公共（外部）函数应以 emb 开头

例如：

```c
AjBool ajStrAssignSubs(AjPStr* Pstr, const AjPStr str,
                         ajint pos1, ajint pos2);
double embIepPhFromHconc (double H);
```

当将函数添加到现有的 AJAX 和 NUCLEUS 库文件中，并且更改将被纳入发行版时，函数和参数名称必须遵守在头文件中定义并用代码中的标记 @namXrule 标记的规则（附录 D，*代码文档标准*）。

### C.9.4 函数布局

函数中代码布局的推荐顺序如下：

- 变量声明
- 构造函数调用
- 函数体
- 析构函数调用和返回。

始终在每个函数的末尾显式声明返回，即使是 void 函数。

例如：

```c
/* @func ajStrAssignK *****************************************************
**
** Copy a single character to a string.
**
** @param [w] Pstr [AjPStr*] Target string.
** @param [r] chr [char] Source text.
**
** @return [AjBool] ajTrue if string was reallocated
**
** @@@
****************************************************************************/

AjBool ajStrAssignK(AjPStr* Pstr, char chr)
{
    AjBool ret = ajFalse;
    AjPStr thys;

    if(!*Pstr)
        *Pstr=ajStrNewRes(2);

    thys = *Pstr;

    if(thys->Use != 1 || thys->Res <= 1)
    {
        ret = ajStrSetRes(Pstr, 2);
        thys = *Pstr;
    }

    thys->Ptr[0] = chr;
    thys->Ptr[1] = '\0';
    thys->Len =1;

    return ret;
}
```

### C.9.5 函数文档

所有公共（外部）函数必须以标准方式记录（附录 D，*代码文档标准*）。用适当的空白（四个换行符）分隔对象。

## C.10 程序流程

### C.10.1 循环

在大块代码中，除非有充分理由，否则不要使用 `continue` 语句，因为它们会使代码难以跟踪。

### C.10.2 goto

除非实在别无选择，否则不要使用 `goto`，也不要使用用于非局部跳转的函数。它们会使代码非常难以跟踪。

### C.10.3 switch 语句

考虑使用 `switch` 语句来改善代码可读性，当您有过长的 `if else` 链时。但是，如果同一个 `switch` 语句在代码中到处重复，这将难以维护。考虑更改您的代码（可能是数据模型），以便不需要 `switch`。

## C.11 内存分配

### C.11.1 一般内存管理

不要在函数内的变量声明中定义大型数组。它们会放在栈上并可能引起许多问题。

不要显式使用 `malloc()` 或 `calloc()`；而是使用 AJAX 宏，例如 `AJALLOC`、`AJNEW`、`AJCNEW`、`AJNEW0`、`AJCNEW0` 等（参见第 5.3 节“对象（C 数据结构）”）。

### C.11.2 对象构造

显式调用构造函数，即像这样：

```c
int main(int argc, char **argv)
{
    AjPStr tmpstr = NULL;

    tmpstr = ajStrNew();
    ajStrAssignC(&tmpstr, "Hello");
}
```

而不是像这样，其中发生构造（默认字符串构造函数由 `ajStrAssignC` 调用），但代码中不清楚：



```
AjPStr tmpstr = NULL;
ajStrAssignC(&tmpstr,"Hello");
```

如果可能，在函数开始处调用所有必要的构造函数。它们将提醒你在函数底部放置析构函数。这样做可以避免内存泄漏。

### C.11.3 对象销毁

你的代码不应泄漏内存。始终根据需要对任何对象调用析构函数。这适用于所有函数，包括 main() 函数：不要依赖操作系统来释放进程内存：

```
int main(int argc, char **argv)
{
    AjPStr tmpstr = NULL;

tmpstr = ajStrNew();
ajStrAssignC(&tmpstr,"Hello");
ajStrDel(&tmpstr);

    return 0;
}
```

# 附录 D 代码文档标准

### D.1 简介

代码文档指南涵盖：

- 记录源代码的一般注释
- 每个应用程序源文件开头的结构化注释和许可证信息
- 每个库源文件开头的结构化注释和许可证信息
- 描述每个函数的结构化注释
- 描述每个数据类型（C 结构定义）的结构化注释

代码中的一般 C 风格注释推荐采用特定样式（见下文）。此类注释是记录代码的一种非正式但有价值的方式。对于文档的主体部分，使用结构化注释。

所采用的方法大致基于 JavaDoc。嵌入式文档使用文本标记进行标记，这些标记以 @ 开头，后跟标识项目的代码，然后是自由文档文本。@ 之前不应给出任何文本，尽管任何前导星号（*）或空格在解析前都会被删除。例如：

```
** @source ApplicationName
```

行中标记后的文本不得包含 HTML 标记（这会使将文本转换为 XML 以用于生成在线文档的解析器复杂化）。标记后的文本一直持续到遇到新标记或找到表示 C 风格注释结束的标记 (*/) 为止。

### D.2 一般注释

注释可以使程序更易于理解，但使用过多或位置不当会使优秀的代码变得难以阅读。请谨慎使用。适合添加注释的位置包括：

- 程序或函数中的主要逻辑步骤
- 程序或函数中的棘手步骤
- 关键变量，但不要记录单个管家变量，例如循环计数器
- 你做一些非同寻常的地方（这将帮助其他人调试代码）
- 你做一些特别巧妙的地方（该技术可能对其他人有用）。

只有当代码属性不明显时，才应对其进行注释。相比之下，即使看似明显的全局属性和不变量也可能需要明确说明。然而，这不一定要通过注释来实现。assert() 宏是一个出色的可执行注释。编写注释时有几条准则：

- 如果你的代码需要注释才能理解，那么你应该寻找重写它的方法，使其更清晰。
- 注释应让其他人能够理解，而不仅仅是你自己。
- 永远不要编写可能变得不正确或过时的注释。不准确或具有误导性的注释比没有注释更糟糕。
- 注释的大小应与其引用的代码大小成比例。
- 所有注释都应正确格式化（参见附录 C，C 编码标准）。

### D.3 应用程序代码文档

应用程序代码文档包括：

- 一般注释（见上文）
- 包含 GPL 的标准标题
- main() 函数文档
- 数据类型的结构化注释
- 函数的结构化注释。

### D.3.1 标准标题

应用程序源文件必须以包含通用公共许可证（GPL）声明的标准标题开头，应尽可能使用。标题如下所示。前几行特定于每个源文件，其余部分是固定的：

```
/********************************************************************
 * @source ApplicationName
 ***
 * ShortDescription
 ***
 * @author Copyright (C) Year AuthorName
 * @version VersionNumber description of version
 * @modified EditDate EditorName description of edit
 * @@@
 **
 ** This program is free software; you can redistribute it and/or
 ** modify it under the terms of the GNU General Public License
 ** as published by the Free Software Foundation; either version 2
 ** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
***********************************************************************/
```

其中：

- ApplicationName 是应用程序的名称。
- ShortDescription 是应用程序的简短描述，应与应用程序 ACD 文件中 documentation: 属性之后的文本以及 main() 函数文档（见下文）中的文本相同。
- Year 是首次发布年份，AuthorName 是原作者。
- VersionNumber 是版本号，后面可以跟可选描述。
- EditDate 和 EditorName 是最后一次重要编辑的日期和作者，后面可以跟可选的修订描述。标题可以包含所需数量的这些行。

例如：

```
/* @source water
**
** Smith-Waterman local alignment
**
** @author: Copyright (C) Alan Bleasby
** @
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
***********************************************************************/
```

### D.3.2 main() 函数

这应该前面有一个与以下格式匹配的标题块：

```
/* @prog ApplicationName ********************************
**
** ShortDescription
**
******************************************************************/
```

其中

- `ApplicationName` 是应用程序的名称。
- `ShortDescription` 是应用程序的简短描述，应与应用程序 ACD 文件中 `documentation:` 属性之后的文本以及应用程序代码标准标题（见上文）中的文本相同。

例如：

```
/** @prog water ******************************************************************/
**
** Smith-Waterman local alignment
**
******************************************************************/
```

### D.3.3 应用程序数据类型和函数

应用程序函数和数据类型的记录方式与库代码完全相同（见下文）。理想情况下应使用结构化注释，但并非严格要求。否则，使用一般 C 风格注释。

### D.4 库代码文档

库代码文档包括：

- 一般注释（见上文）
- 包含 GPL 的标准标题
- 所有数据类型的结构化注释
- 所有函数的结构化注释
- 功能部分（仅限库源文件）。

### D.4.1 标准标题

每个库源文件 (*.c) 必须以标准标题开头。这基本上与应用程序标题相同，并包含 GPL：

```
/******************************************************************
** @source AJAX Library Area functions
**
** ShortDescription
**
** @author Copyright (C) Year AuthorName
** @version VersionNumber description of version
** @modified EditDate EditorName description of edit
```





```
** @@
**
** This library is free software; you can redistribute it and/or
** modify it under the terms of the GNU Library General Public
** License as published by the Free Software Foundation; either
** version 2 of the License, or (at your option) any later version.
**
** This library is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
** Library General Public License for more details.
**
** You should have received a copy of the GNU Library General Public
** License along with this library; if not, write to the
** Free Software Foundation, Inc., 59 Temple Place - Suite 330,
** Boston, MA 02111-1307, USA.
**********************************************************************/
```

标签与应用程序头中的标签相同，但 LibraryArea 描述库的一般区域，例如 "string"。
示例：

```
/**********************************************************************
** @source AJAX string functions
**
** AjPStr objects are reference counted strings
** Any change will need a new string object if the use count
** is greater than 1, so the original AjPStr is provided as a pointer
** so that it can be reallocated in any routine where string modification
** may be needed.
**
** In many cases the text is always a copy, even of a constant original, so
** that it can be simply freed.
**
** @author Copyright (C) 1998 Peter Rice
** @version 1.0
** @modified Jun 25 pmr First version
** @@
**
** This library is free software; you can redistribute it and/or
** modify it under the terms of the GNU Library General Public
** License as published by the Free Software Foundation; either
** version 2 of the License, or (at your option) any later version.
**
** This library is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
** Library General Public License for more details.
**
** You should have received a copy of the GNU Library General Public
** License along with this library; if not, write to the
** Free Software Foundation, Inc., 59 Temple Place - Suite 330,
** Boston, MA 02111-1307, USA.
**********************************************************************/
```

## D.4.2 库数据类型和函数

所有库函数和数据类型都需要结构化注释（见下文）。

## D.4.3 功能章节

库源文件 (*.c) 中的函数被组织为章节，这些章节定义了具有相关功能的函数组。这些章节使用结构化注释进行文档化，该注释定义了函数命名规则、函数参数命名和数据类型规则以及返回数据类型定义规则。这确保了库文件内部，以及在一定程度上跨库文件的函数，呈现出直观且一致的 API。

向现有库文件添加新函数时，应将其放置在文件的相应章节下。创建新库文件时，建议但不强制要求向文件添加章节。

章节分为三种类型。结构化注释的开始由给定的标签指示：

- 文件章节 (@filesection)
- 数据章节 (@datasection)
- 标准章节 (@section)。

函数本身之前应给出一个文件章节。这包含整个库的基本文档和规则。文件章节包含若干数据章节，每个主要数据类型对应一个，由函数处理。

通常会为头文件中定义的所有公共数据类型（由 @data 标识）提供数据章节。例如，ajstr.h 定义了三种新数据类型，AjPStr、AjIStr 和 AjPStrTok，但也存在主要参数为 C 风格 (char*) 字符串的函数。因此，在文件章节下总共列出了四个数据章节。

标准章节位于数据章节之下。这些章节定义了具有相关功能、相似名称和相似参数的函数组。标准章节所属的数据章节取决于返回值或主要参数的数据类型。例如，默认字符串构造函数没有参数但返回一个 AjPStr 字符串，因此列在 AjPStr 数据章节下。什么定义了“主要”参数在一定程度上是主观的。对于所有具有多个参数的函数，如果主要参数不是由返回类型确定的，则应为列表中的第一个参数。

每个 @filesection、@datasection 和 @section 包含下文描述的标准文本标签。

### D.4.3.1 函数章节文档标签

可用标签以 @ 开头。

| 标签 | 说明 |
|---|---|
| @filesection | 文件章节结构化注释的开始，后跟库名称，以及任意数量的带标记的自由文本行。 |
| @datasection | 数据章节结构化注释的开始，后跟数据类型、数据类型描述，以及任意数量的带标记的自由文本行。 |
| @section | 一般章节结构化注释的开始，后跟章节名称，以及任意数量的带标记的自由文本行。 |
| @fnote | 用于关于章节的一般注释，例如，其与其他章节的关系。 |
| @namXrule | 定义函数命名规则。后跟一个文本标记，指示函数名称的一个组件（子字符串），以及一行或多行描述具有该命名组件的函数功能的自由文本。X 是一个整数，定义该组件在函数名称中的顺序（见下文）。 |
| @suffix | 定义命名规则，用于区分功能本质相同但仅在单个参数数据类型上不同的函数。例如，两个字符串插入函数都向 EMBOS (AjPStr) 字符串插入内容，但一个插入 AjPStr，另一个插入 C 类型 (char *) 字符串。首先给出可能出现在函数名称中的后缀（在 @namXrule 标签定义的组件之后，见下文）。随后是括号中的数据类型以及描述该数据类型的自由文本。 |
| @fdata（仅限标准章节） | 仅出现在标准章节中，且必须存在。它定义章节中函数操作或返回的主要数据类型（括号中）。该数据类型必须与当前数据章节中给出的相同。会检查函数，以确保数据类型针对函数类别被适当使用和传递（参见 @fcategory）。 |
| @argrule | 定义函数参数命名和数据类型规则，以及（可选）函数名称后缀定义规则。后跟一个文本标记，指示函数名称的后缀，如果未指定则为 ‘*’。第二个文本标记给出参数名称。然后给出参数数据类型（括号中），后跟一行或多行描述参数的自由文本。 |
| @valrule | 定义函数返回类型。后跟一个文本标记，指示适用此返回类型的函数名称后缀。返回数据类型随之而来（括号中），随后是描述在各种条件下返回值的一行或多行自由文本。 |
| @fcategory（仅限标准章节） | 定义用于功能类别的标准名称。这用于验证数据类型（参见 @fdata）传递给函数的方式。值可以是："new","delete", "assign", "modify", "cast", "derive", "use", "iterate", "input", "output", "misc" 或 "internals"。 |

### D.4.3.2 示例

以下显示了 ajstr.c 的摘录，指示文件中的第一个文件章节、数据章节和标准章节：

```
/* filesection ajstr ************************************************************************
**
** @nam1rule aj Function belongs to the AJAX library.
**
** @suffix Len [size_t] length
** @suffix C [char*] C character string
** @suffix S [AjPStr] string object
** @suffix K [char] single character
*/
```

```
/* @datasection [AjPStr] String ************************************************************************
**
** Functions for manipulating AJAX (AjPStr) strings
**
** @nam2rule Str Function is for manipulating strings
**
*/
```

```
/* @section comparison
**
** Functions for comparing strings
**
** @fdata [AjPStr]
**
** @nam3rule Match Compare two complete strings.
** @nam4rule MatchCase Case-insensitive comparison.
** @nam4rule MatchWild Comparison using wildcard characters.
** @nam5rule MatchWild Case Case-insensitive comparison
** using wildcard characters.
** @nam5rule MatchWildWord Case-sensitive wildcard comparison of
** first words within two strings.
** @nam5rule MatchWildWordCase Case-insensitive wildcard comparison of
** first words within two strings.
** @nam4rule MatchWord Comparison using whole words.
** @nam5rule MatchWordOne Comparison using whole words matching any one.
** @nam5rule MatchWordAll Comparison using whole words matching every one.
**
** @nam3rule Prefix Compare start of string to given prefix.
** @nam4rule Prefix Case Case-insensitive comparison.
** @nam3rule Suffix Compare end of string to given suffix.
** @nam4rule Suffix Case Case-insensitive comparison.
**
** @argrule * str [const AjPStr] String
** @argrule C txt2 [const char*] String
** @argrule S str2 [const AjPStr] String
**
** @valrule * [AjBool] True on success
**
** @fcategory use
**
*/
```

‘comparison’ 章节中的函数原型如下：

```
AjBool ajStrMatchC (const AjPStr thys, const char* txt);
AjBool ajStrMatchS (const AjPStr thys, const AjPStr str);
AjBool ajStrMatchCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchCaseS (const AjPStr thys, const AjPStr str);
```





AjBool ajStrMatchWildC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildCaseS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildWordC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWildWordCaseC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordCaseS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWordAllS(const AjPStr str, const AjPStr str2);
AjBool ajStrMatchWordOneS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixC(const AjPStr str, const char* txt2);
AjBool ajStrPrefixS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixCaseC (const AjPStr str, const char* pref);
AjBool ajStrPrefixCaseS (const AjPStr str, const AjPStr pref);
AjBool ajStrSuffixC (const AjPStr thys, const char* suff);
AjBool ajStrSuffixS (const AjPStr thys, const AjPStr suff);
AjBool ajStrSuffixCaseC (const AjPStr str, const char* pref);
AjBool ajStrSuffixCaseS (const AjPStr str, const AjPStr pref);

让我们来看看函数 ajStrMatchWildWordCaseS 的命名规则是如何工作的。这是你可能遇到的最难的示例：

- 1. @nam1rule aj 函数属于 AJAX 库。

  此规则在文件部分中定义第一个函数名组件为 aj。AJAX 库中的所有函数都带有此前缀。

- 2. @nam2rule Str 函数用于操作字符串。

  此规则在 AJAX (AjPStr) 字符串的数据部分中定义第二个函数名组件为 Str。AJAX 字符串库 (ajstr.h/c) 中所有操作 AJAX (AjPStr) 字符串的函数都带有前缀 ajStr。

- 3. @nam3rule Match 比较两个完整字符串。

  此规则在标准部分中用于‘比较’函数，定义第三个函数名组件为 Match。自由文本表明，所有带有前缀 ajStrMatch* 的函数都是用于比较两个完整字符串。

- 4. @nam4rule MatchWild 使用通配符字符进行比较。

  此规则定义第四个函数名组件为 Wild，并表明带有前缀 ajStrMatchWild* 的函数使用通配符字符比较两个（完整）字符串。

- 5. @nam5rule MatchWildWord 对两个字符串内首个单词进行区分大小写的通配符比较。

  此规则定义第五个函数名组件为 Word，并表明带有前缀 ajStrMatchWildWord 的函数使用通配符字符比较两个完整字符串，仅使用两个字符串内的首个单词。

- 6. @nam6rule MatchWildWordCase 对两个字符串内首个单词进行不区分大小写的通配符比较。

  此规则定义第六个函数名组件为 Case，并表明带有前缀 ajStrMatchWildWordCase 的函数使用通配符字符比较两个完整字符串，仅使用两个字符串内的首个单词，且不区分大小写。

- 7. @suffix C [char*] C 字符字符串。

  此规则在文件部分中定义，表明带有后缀 C 的函数接受 C 类型 (char *) 字符串参数。

> **重要**
>
> 命名规则应仅在严格需要区分现有函数时才定义。不应在可以在语义上*可能*拆分功能，但因没有其他类似函数而无理由这样做的情况下使用。在这种情况下，函数在基本前缀之后应只有一个组件（例如 ajStr）。此组件通常是一个大写单词，但如果使用多个单词能真正提高清晰度，则应使用 `SentenceCase`。

## D.5 数据类型文档

出现在 C 数据结构之前的结构化注释具有以下一般格式：

```
/* @data PointerName ***********************************************************
**
** DatatypeDescription
** DatatypeDescription cont.
**
** @alias StructName
** @alias ObjectName
**
** @new Description
** @delete Description
** @assign Description
**
** @attr Element1 [Datatype1] Description
** @attr Element2 [Datatype2] Description
**
** @@
** Comments
** Comments cont.
**
**********************************************************************************/

typedef struct StructName
{
    Datatype1 Element1;
    Datatype2 Element2;
} ObjectName

#define PointerName ObjectName*
```

### 其中：

- `PointerName` 是指针数据类型，例如 AjPStr。
- `StructName` 是结构名称，例如 AjSStr。
- ObjectName 是对象数据类型，例如 AjOStr。
- DatatypeDescription 是出现在在线文档中的数据类型描述。它可能跨多行。
- Element* 是结构中元素的变量名。
- Datatype* 是结构中元素的数据类型。
- Description 是对结构中元素或对其进行操作的函数的描述（有关标签的使用，请参见下文）。
- Comments 是可选注释，不会出现在在线文档中。

在下面的示例中，有一个额外的指针数据类型 (AjPStr)。这对于大多数数据类型不是必需的：

```
/* @data AjPStr ****************************************************************
**
** Ajax string object.
**
** Holds a null terminated character string with additional data.
** The length is known and held internally.
** The reserved memory size is known and held internally.
** The reference count is known and held internally.
** New pointers can refer to the same string without needing
** to duplicate the character data.
**
** If a string has multiple references it cannot be changed. Any
** instance to be changed is first copied to a new string. This
** means that any function which can change the character data must
** pass a pointer to the string so that the string can be moved.
**
** A default null string is provided. New strings are by default
** implemented as pointers to this with increased reference counters.
**
** AjPStr is implemented as a pointer to a C data structure.
**
** @alias AjPPStr
** @alias AjSStr
** @alias AjOStr
** @iterator AjIStr
**
** @attr Res [ajuint] Reserved bytes (usable for expanding in place)
** @attr Len [ajuint] Length of current string, excluding NULL at end
** @attr Ptr [char*] The string, as a NULL-terminated C string.
** @attr Use [ajuint] Use count: 1 for single reference, more if several
**                     pointers share the same string.
**                     Must drop to 0 before deleting. Modifying means making
**                     a new string if not 1.
** @attr Padding [ajuint] Padding to alignment boundary
** @@
*******************************************************************************/

typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
};

} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

### D.5.1 数据类型文档标签

可用标签以 @ 开头。一些标签引用作用于数据结构的函数。

| Tag | Description |
| :--- | :--- |
| @data | 结构化注释的开始。给出指向数据结构的指针的数据类型（例如 AjPStr），后面可跟任意数行带标记的自由文本。如果数据结构不对外可见，请使用 @datastatic。 |
| @datastatic | 与 @data 相同，但用于静态（内部）数据类型。 |
| @alias | 相关数据类型和名称的别名。标准做法是使用指针名称（AjPStr 等）作为主名称，并使用对象名称（AjOStr 等）和结构名称（AjSStr 等）作为别名。这些用于在源代码中通过别名标记引用。 |
| @iterator | 与此数据类型关联的迭代器数据类型的名称（例如 AjIStr），如果有的话。 |
| @other | 与此数据类型关联的任何其他数据类型的名称。 |
| @new | 构造函数。给出函数名称，后跟函数描述的副本。 |
| @delete | 析构函数。给出函数名称，后跟函数描述的副本。 |
| @assign | 赋值（覆盖值）。给出函数名称，后跟函数描述的副本。 |
| @modify | 修改器（更新值）。给出函数名称，后跟函数描述的副本。 |
| @cast | 将值转换为其他内容作为返回类型或另一个参数。给出函数名称，后跟函数描述的副本。 |
| @use | 使用值但不修改它或返回任何部分。给出函数名称，后跟函数描述的副本。 |
| @input | 输入函数（读取输入源并填充数据类型）。给出函数名称，后跟函数描述的副本。 |
| @output | 输出函数（将值写入输出文件）。给出函数名称，后跟函数描述的副本。 |
| @iterate | 迭代函数（对值或值数组进行迭代）。给出函数名称，后跟函数描述的副本。 |
| @attr | 属性名称、类型和描述。属性按其在结构中出现的相同顺序定义。名称和类型必须与真实定义匹配。 |
| @cc | 在属性组之间插入的注释。结构本身不允许有注释（以提供干净的解析），因此注释插入在标题中。 |





## D.6 函数文档

静态函数的结构化注释以 @funcstatic 开头，而导出函数则标记为 @func。对于导出函数，原型在相关头文件中声明。每个函数前的结构化注释必须采用以下一般格式：

```
/* @func FunctionName ***********************************************************
**
** FunctionDescription
** FunctionDescription cont.
**
** @param [ParameterCode1] ParameterName1 [Datatype1] Description
** @param [ParameterCode2] ParameterName2 [Datatype2] Description
** @return [Datatype] Description
** @cre Description
** @ure Description
** @exception ExceptName Description
** @see RelatedFunctionName
** @@
**
** Comments
** Comments cont.
***********************************************************************************/
Datatype FunctionName (Datatype ParameterName1, Datatype ParameterName2)
{
    /* Function C code goes here */
}
```

其中：

- FunctionName 是函数的名称。
- FunctionDescription 是出现在在线文档中的函数描述。它可以跨多行。
- ParameterCode* 是描述参数的参数代码（见下文），后跟对参数的简短描述。
- Datatype 是参数的数据类型或函数返回的数据类型（对于 void 函数则为 void）。
- RelatedFunctionName 是与所讨论函数相关的函数的名称。
- Comments 是可选注释，不会出现在在线文档中。

例如：

```
/* @func ajStrMatchC *************************************************************
**
** Simple test for matching a string and a text string.
**
** @param [r] str [const AjPStr] String
** @param [r] txt2 [const char*] Text
** @return [AjBool] ajTrue if two complete strings are the same
** @@
********************************************************************************/
AjBool ajStrMatchC(const AjPStr str, const char* txt2)
{
    if(!str || !txt2)
        return ajFalse;

    if(!strcmp(str->Ptr, txt2))
        return ajTrue;

    return ajFalse;
}
```

### D.6.1 函数文档标签

可用标签以 @ 开头，并基于 JavaDoc 中定义的集合。

| Tag | Description |
| :--- | :--- |
| @func | 结构化注释的开始，后跟函数名称和任意数量的带标记的自由文本行。如果函数不公开可见，请使用 @funcstatic。 |
| @funcstatic | 与 @func 相同，但用于静态（内部）函数。 |
| @param | 每个参数使用一次。参数名称（ParameterName）和类型（Datatype）与函数中定义的相同。还给出了参数代码（ParameterCode）（见下文）。 |
| @cre | 参数的已检查运行时错误的描述。 |
| @ure | 参数的未检查运行时错误的描述。 |
| @return | 成功执行时返回值的数据类型和描述。 |
| @error | 错误条件下返回值的描述。如果合适，可以使用多次。 |
| @exception | 此函数抛出的异常。如果合适，可以使用多次。 |
| @see | 相关函数的交叉引用。必须给出一个函数名称（RelatedFunctionName），它与同一或不同源文件中 @func 标签后给出的名称相同。 |
| @@ | 有效地结束结构化注释。任何后续文本都会被 HTML 转换解析器忽略，不会出现在在线文档中。 |

### D.6.2 参数代码

代码由基本类型的小写字母和大写修饰符组成。

| Code | Mnemonic | Description |
|---|---|---|
| *参数代码（基本类型）* | | |
| r | 读取 | 参数值被使用但不会以任何方式更改。 |
| w | 写入 | 参数值被忽略。除非满足特定条件（应予以文档化），否则始终会写入新值。 |
| u | 更新 | 参数值被使用，并且（通常）会写入新值。 |
| d | 删除 | 参数值是指向要释放的内存的指针。指针将被设置为 NULL。 |
| f | 函数指针 | 参数值是指向函数的指针。描述应指示函数类型。 |
| v | 可变参数 | 参数值是某种形式的可变长度参数列表。 |
| *参数代码（修饰符）* | | |
| C | 已检查 | 值会被检查。有关已检查的运行时错误，请参见 @cre 标签。 |
| E | 空 | 将接受空值，例如长度为零的字符串。 |
| N | 空 | 将接受 NULL 值。 |
| P | 指针 | 如果指针本身可能被写入，而不仅仅是它指向的数据，请使用此项。 |

# 附录 E 资源

### E.1 EMBOSS 编程接口

下面描述了 EMBOSS 的编程接口。

> **注意**
> 接口列表绝非详尽无遗。如果您了解其他与 EMBOSS 相关的接口，请将详细信息发送至 emboss-bug@emboss.open-bio.org。

可用的编程接口包括：

| Interface | Link | Description |
|---|---|---|
| Biopython | http://www.biopython.org | 各种模块使用 EMBOSS 程序。 |
| Bio-Emboss | http://search.cpan.org/dist/Bio-Emboss/ | 一个 Perl 接口，用于 EMBOSS 库，允许您编写看起来和感觉像典型 EMBOSS 程序的 Perl 程序。 |
| BioPerl 类用于 EMBOSS 应用程序 Bio::Tools::Run::EMBOSS Application | http://doc.bioperl.org/releases/bioperl-1.0.2/Bio/Tools/Run/EMBOSSApplication.html | EMBOSSApplication 类可以表示任何 EMBOSS 应用程序。它由 Bio::Factory::EMBOSS 对象创建，该对象通过读取应用程序 ADC 文件对其进行初始化。 |
| BioPerl EMBOSS 应用程序工厂类 Bio::Factory::EMBOSS | http://doc.bioperl.org/bioperl-run/Bio/Factory/EMBOSS.html | EMBOSS 工厂类封装了对现有 EMBOSS 程序的访问。 |
| BioPerl 类用于 EMBOSS 应用程序限定符 Bio::Tools::Run::EMBOSSacd | http://search.cpan.org/~birney/bioperl-run-1.4/Bio/Tools/Run/EMBOSSacd.pm | EMBOSSacd 类表示可以传递给 EMBOSS 应用程序的所有可能命令行参数。 |
| BioMoby | http://biomoby.open-bio.org/ | MOBY 是一个本体学系统，用于生物服务提供商（无论是数据主机还是分析服务）之间的互操作性。EMBOSS 应用程序已被纳入。 |

### SOAPLAB

http://www.ebi.ac.uk/Tools/webservices/soaplab/overview

**SoapLab** 为命令行程序生成 Web 服务。可能有两种 Web 服务接口（通用接口和类型化接口）。通用接口允许将输入数据作为弱类型名称:值对发送。这允许将各种应用程序集成在单个编程接口下。类型化 Web 服务接口在 WSDL/XSD 级别定义输入/输出类型描述，允许 Web 服务客户端使用标准方法检查输入/输出数据类型。

## 索引

### 符号

-debug 选项（参见 调试）
./configure 命令（参见 配置脚本）
.embossrc 文件（参见 EMBOSS 配置文件）
ACD 应用程序属性，91, 92, 485, 513
ACD 应用程序定义，25, 61, 83, 91, 425, 434, 459, 484, 485
属性（参见 ACD 应用程序属性）
检索某个的值（参见 操作）
ACD 属性，81, 436, 484, 489
应用程序（参见 ACD 应用程序属性）
计算的（参见 计算属性）
数据（参见 ACD 数据属性）
全局的（参见 全局属性）
ACD 计算，123, 140
类型，564
变量和，127, 566
ACD 数据属性，83, 96, 486, 525, 556
计算的（参见 计算属性）
特定于数据类型的，109（参见 特定于数据类型的属性）
用于与数据类型关联的限定符，114
用于定义数据输出，113, 522
用于定义帮助信息，108, 523
用于定义最大值和最小值，96, 132
用于图形 ACD 数据类型，114, 555
用于输入 ACD 数据类型，110, 530, 557
用于命名和定位文件，111, 112
用于输出 ACD 数据类型，111, 540
用于选择 ACD 数据类型，113, 554
用于设置默认值，96, 131
用于简单 ACD 数据类型，525, 557
用于类型检查输入，110, 111, 522
用于用户提示，105, 129, 133, 521
用于验证应用程序输出，113
用于验证用户输入，107, 110, 523
全局的（参见 全局属性）
检索值（参见 操作）
类型，103, 489
ACD 数据定义，96, 435, 485, 486
属性（参见 ACD 数据属性）
检索某个的值（参见 操作）
ACD 数据类型，51, 98, 492
图形（参见 图形 ACD 数据类型）
输入（参见 输入 ACD 数据类型）
输出（参见 输出 ACD 数据类型）
选择（参见 选择 ACD 数据类型）
简单（参见 简单 ACD 数据类型）

ACD 定义
用于应用程序定义（参见 ACD 应用程序定义）
用于数据定义（参见 ACD 数据定义）
ACD 文件名（参见 ACD 文件）
ACD 文件节，96, 486, 490, 491
附加，491
高级，491
输出，491
所需，491
验证，491
ACD 文件节文件（参见 sections.standard 文件）
ACD 文件，19, 25, 34, 38, 61, 81, 433, 455
属性（参见 ACD 数据属性）
中的数据类型（参见 ACD 数据类型）
调试（参见 调试）
文档化，424, 425
处理，188
位置，30
命名，92, 485
中的操作（参见 操作）
处理，189, 439, 465, 471, 480
重新格式化，143
从中检索值（参见 ajAcdGet 函数）
中的节（参见 ACD 文件节）
语法（参见 ACD 语法）
测试，26, 46, 62, 139, 142, 143
用于的实用程序（参见 ACD 实用程序）
ACD 操作（参见 操作）
ACD 运算符，121, 563
使用的否定，133, 565
ACD 语法，19, 82, 139, 484
ACD 实用程序，26, 62, 82, 136, 425, 456
ACD 变量，122, 127, 566
自动，39, 128, 567
定义，128
acdvalid, 139
由其测试的功能，140
aclocal, 4
其他限定符（参见 命令行限定符）
ACD 文件中的其他节（参见 ACD 文件节）
高级限定符（参见 命令行限定符）
ACD 文件中的高级节（参见 ACD 文件节）
ajAcdGet 函数，34, 43, 50, 162, 165, 189, 192, 193, 437, 440, 465, 477, 569
AJAX, 186, 569
文档，13, 19, 185, 568
扩展，60, 63, 72, 73, 154
AJAX 命令定义（参见 ACD 语法）
AJAX 命令定义文件（参见 ACD 文件）
AJAX 数据类型（参见 对象）
ajax.h 文件，64, 75, 147, 577





## 索引

- ajax/ 目录, 63
- ajdebug 函数 (参见 调试)
- 比对 (参见 序列比对)
- 输入 (参见 序列比对输入)
- 输出 (参见 序列比对输出)
- ANSI 标准 C, 61, 149, 578, 586
- API, xxiii, xxiv, 602
- 应用程序, 91, 185, 433, 513
- 添加新的 EMBASSY, 68
- 添加新的 EMBOSS, 66
- 参数, 407
- 代码布局 (参见 代码布局)
- 数据文件 (参见 数据文件)
- 调试 (参见 调试)
- 开发, 58, 62, 65
- 错误消息 (参见 应用程序错误消息)
- 查找和运行, 35
- 输入文件, 111
- 命名, 92, 435, 455, 485
- 选项 (参见 应用程序选项)
- 参数 (参见 应用程序选项)
- 移植, 59, 450
- 限定符 (参见 命令行限定符)
- 简短描述, 27, 425, 456, 599, 600, 609
- 用法示例, 414, 417, 425
- 版本号 (参见 版本号)
- 包装器, 60, 69, 139, 450
- 应用程序 ACD 文件 (参见 ACD 文件)
- 应用程序代码文档, 598
- 应用程序数据已知类型文件 (参见 knowntypes.standard 文件)
- 应用程序定义 (参见 ACD 应用程序定义)
- 应用程序文档, 12, 58, 72, 424, 457
  - 过程, 425
  - 各部分, 425, 443
- 标准 (参见 文档标准)
- 使用 autodoc.pl (参见 autodoc.pl 脚本)
- 应用程序错误消息, 77, 137, 409
- 应用程序函数名 (参见 函数名)
- 应用程序函数 (参见 函数)
- 应用程序组, 93
- 应用程序组名称文件, 94
- 应用程序头 (参见 应用程序文档)
- 应用程序关键字文件 (参见 keywords.standard 文件)
- 应用程序选项, 52, 81, 96, 109, 455, 456
- 应用程序输出 (参见 输出文件)
- 应用程序参数 (参见 ACD 文件中的参数)
- 应用程序质量保证测试, 33, 66, 414, 425, 444
  - 数据, 423
  - 文件 (参见 qatest.dat 文件)
  - 运行, 421
  - 编写, 420, 444
- 应用程序报告格式, 342
- 设置, 345
- 应用程序报告, 270, 275, 342
  - ACD 数据类型, 102, 344, 507, 550
  - ACD 定义, 344, 507, 550
  - AJAX 函数, 282, 344
  - AJAX 对象, 344
  - 命令行规范, 112, 345, 508
  - 数据类型关联限定符 (参见 数据类型关联限定符)
  - 调试 (参见 调试)
  - 文件管理, 346, 352
  - 准备, 348
  - 从 ACD 文件中检索, 346
  - 使用 rformat 设置格式, 345
  - 支持的文件格式 (参见 应用程序报告格式)
- 应用程序测试数据 (参见 应用程序质量保证测试)
- 应用程序版本号 (参见 版本号)
- 任意限制, 159, 236
- 算术运算 (参见 运算)
- 数组函数, 373
  - 用于构建, 158, 159, 160, 168, 180, 374, 376, 595
  - 用于销毁, 158, 159, 160, 170, 180, 375
  - 用于获取和设置元素, 376
  - 用于检索 C 类型数组, 147, 160, 378
  - 用于对数组排序, 377
- 数组, 370
  - 二维, 168, 179, 371
  - 三维, 371
  - ACD 数据类型, 372, 492, 525
  - ACD 定义, 372, 492, 525
  - AJAX 函数 (参见 数组函数)
  - AJAX 对象, 160, 179, 371
  - 命令行规范, 372, 492
  - 从 ACD 文件中检索, 373
- 断言 (参见 异常消息)
- 关联限定符 (参见 数据类型关联限定符)
- 属性 (参见 ACD 属性)
  - ACD 应用程序定义的属性 (参见 ACD 应用程序属性)
  - ACD 数据定义的属性 (参见 ACD 数据属性)
- autoconf, 2, 4, 5, 8, 11, 65, 69
- autodoc.pl 脚本, 425, 429, 430
- automake, 2, 4, 8, 11, 65
- 自动变量 (参见 ACD 变量)
- 回译 (参见 序列翻译)
- BBSRC, xx
- 二进制文件, 6
- 生物数据类型 (参见 ACD 数据类型)
- BioMoby, 612
- BioPerl, 612
- BLAST 数据库, 500
- 布尔 ACD 数据类型, 135, 195, 492
  - 命令行规范, 492
- 布尔测试 (参见 运算)
- 错误报告, 22
- C 编码标准, 19, 574
- C 注释 (参见 代码中的注释)
- C 数据结构 (参见 对象)
- C 函数包装器, 408
- C 指针, 80, 150, 440
  - 声明, 151
  - 指向指针, 153
- C 预处理器, 28, 147, 582, 587
- C 编程库, xxiii, xxiv, 147, 568
  - AJAX (参见 AJAX)
  - NUCLEUS (参见 NUCLEUS)
- 计算属性, 103, 115, 437, 556, 563
  - 用于特征, 118, 503, 559

- 计算属性, (续)
  - 用于系统发育数据, 309, 560
  - 用于序列, 115, 257, 508, 509, 557
  - 检索值, 115, 116, 121, 123, 128
- 计算 (参见 ACD 计算)
- 情况条件语句 (参见 条件语句)
- CATH, 501, 507, 569
- ChangeLog 文件 (参见 更改日志文件)
- checkout 命令, 3
- 代码文档标准 (参见 文档标准)
- 代码布局, 575
  - 应用程序, 575
  - 库, 579
- 代码提交, 21, 162
- codes.english 文件 (参见 标准提示文件)
- 编码标准 (参见 C 编码标准)
- 密码子使用表, 314
  - ACD 数据类型, 100, 102, 314, 496, 504, 530, 542
  - ACD 定义, 264, 314, 496, 504, 530, 542
  - AJAX 函数, 314, 318
  - AJAX 对象, 315
  - 命令行规范, 496, 504
  - 数据类型关联限定符 (参见 数据类型关联限定符)
  - 默认, 496, 504
  - 读取, 317
  - 从 ACD 文件中检索, 315, 316
  - 写入, 112, 318
- 合作, 55, 60
- 命令行
  - 标志 (参见 命令行限定符)
  - 验证, xxiii, 110
- 命令行限定符, 52, 112, 114, 525
  - 数据类型关联 (参见 数据类型关联限定符)
  - 数据类型特定 (参见 数据类型关联限定符)
  - 命名, 140, 456, 486
- 代码中的注释, 27, 59, 65, 424, 588, 597
  - 用于数据类型 (参见 对象)
  - 用于函数 (参见 函数)
- 比较矩阵, 287
  - ACD 数据类型, 99, 101, 288, 500, 506, 507
  - ACD 定义, 288, 500, 506, 507
  - AJAX 函数, 288, 293
  - AJAX 对象, 289
  - 命令行规范, 500, 506, 507
  - 从 ACD 文件中检索, 290, 291
- 编译, 6, 32, 63, 65
  - EMBASSY 的 (参见 EMBASSY 包)
  - EMBASSY 包的 (参见 EMBASSY 包)
  - 静态, 8
  - 使用 make, 6, 44, 48, 66
  - 使用 make check, 66, 144, 185, 417
  - 使用 make clean, 7
  - 使用 make install, 5, 6, 9, 44, 48, 66, 68
- 条件语句, 118, 126, 565
  - 情况, 127, 566
  - 三元, 126, 565
  - 一元, 126, 565
- 配置, 4
  - EMBASSY 包的 (参见 EMBASSY 包)
  - 使用 configure 脚本 (参见 configure 脚本)
- configure 脚本, 5
- configure.in 文件, 4, 64, 72
- 构造函数 (参见 对象)
- 构造函数 (参见 对象)
- CVS, 2, 69
- 数据属性 (参见 ACD 数据属性)
- 数据定义 (参见 ACD 数据定义)
- 数据文件, 52, 99, 101, 140, 425, 497
- 数据格式, 52
  - 报告的 (参见 应用程序报告格式)
  - 序列的 (参见 序列格式)
- 库 C 文件中的数据部分 (参见 库 C 文件中的部分)
- 数据结构 (参见 对象)
- 数据库
  - 配置 (参见 数据库配置)
  - 定义 (参见 数据库定义)
  - 序列, 9, 330
- 数据库配置, 52
- 数据库定义, 439
- 数据类型 (参见 对象)
- 数据类型定义 (参见 对象)
- 数据类型文档 (参见 对象)
- 数据类型文档标记 (参见 对象)
- 数据类型关联限定符, 52, 440
  - 定义为 ACD 属性, 103, 109, 112, 436, 489, 525
  - 定义为属性 (参见 ACD 数据属性)
  - 用于比对 (align), 112, 541
  - 用于应用程序报告 (report), 112, 345, 550
  - 用于密码子使用表文件 (codon, outcodon), 530, 542
  - 用于图形输出 (graph, xygraph), 555, 556
  - 用于输出数据文件 (outdata), 543
  - 用于输出文件 (outfile, outfileall), 546, 547
  - 用于输出矩阵 (outmatrix, outmatrixf), 547, 548
  - 用于系统发育数据 (outdiscrete, outdistance, outfreq, outproperties, outtree), 549
  - 用于蛋白质坐标数据 (cpdb, outcpdb), 531, 543
  - 用于正则表达式 (regexp), 527
  - 用于 SCOP 和 CATH 域分类数据 (scop, cath, outscop), 535, 549
  - 用于序列模式 (pattern), 527
  - 用于序列集 (seqset, seqsetall, seqoutset), 538, 539, 553
  - 用于序列流 (seqall, seqoutall), 536, 552
  - 用于序列 (sequence, seqout), 535, 551





## 索引

GDB, 409
图表, 402
- 来自图表的日志消息, 77
- 内存泄漏, 80
- 系统发生数据, 313
- 序列模式, 234
- 使用 -debug 调试图表, 77, 78, 137, 411
- 使用调试器调试图表, 79
- 使用 ajDebug 调试图表, 78, 411

默认值（参见 ACD data attributes）

演示应用程序, 18, 185

依赖项, 2, 81

析构函数, 49, 158, 161, 166, 169, 179, 596

析构函数（参见 Object）

开发者 (CVS) 版本（参见 Release）

目录, 321
  - 用于目录的 ACD 数据类型, 99, 101, 321, 497, 505, 531, 544
  - 目录的 ACD 定义, 323, 324, 531, 544
  - 用于目录的 AJAX 函数, 321, 330, 334, 340
  - 用于目录的 AJAX 对象, 325
  - 命令行中目录的规范, 99, 101, 497, 505
  - 从 ACD 文件中检索目录, 326, 327

DNA 计算, 262

文档, 12, 33, 61, 64, 92, 108, 424, 443, 455, 523, 568, 582, 592, 594, 597
  - 应用程序（参见 应用程序文档）
  - 数据类型（参见 Object）
  - 函数（参见 函数）
  - 库（参见 库文档）
  - 对象（参见 Object）

文档标准, 19, 597
  - 应用程序, 19, 424, 598
  - 代码, 597
  - 库, 600

文档标记, 597
  - 用于函数部分, 602
  - 用于函数, 610（参见 函数）
  - 用于对象, 592, 608
  - 用于结构（参见 Object）

点图, 512

下载
  - 通过 CVS, 3

动态数组（参见 数组）

动态库, 7

动态内存管理（参见 内存）

动态对象, 159, 166, 171

动态字符串（参见 字符串）

动态链接库（参见 动态库）

EBI（参见 EMBL-EBI）

EDATA（参见 SRS 数据库）

EDATAREL（参见 SRS 数据库）

EFUNC（参见 SRS 数据库）

EFUNCREL（参见 SRS 数据库）

EMBASSY 安装, 11

EMBASSY 包文档, 64, 430
  - 流程, 430
  - 部分, 430

EMBASSY 包
  - 向其中添加应用程序, 62, 63, 68
  - 添加新包, 63, 68
  - 编译（参见 编译）
  - 依赖项（参见 依赖项）
  - 下载（参见 下载）
  - 安装, 11（参见 EMBASSY 安装）
  - 许可（参见 许可）

EMBASSY 版本号（参见 版本号）

embExit 函数, 29, 194, 243, 261, 277, 408, 440

embInit 函数, 29, 44, 50, 92, 137, 162, 189, 193, 439

embInitP 函数, 44, 50, 137, 189, 193, 392, 393, 465, 477

EMBL-EBI, xx, xxiv

EMBOSS, xxiii
  - 编译（参见 编译）
  - 开发者, xx, xxiii, 19, 21, 51
  - 移植（参见 应用程序）

EMBOSS 配置文件, 10, 79

EMBOSS 版本号（参见 版本号）

emboss-announce（参见 邮件列表）

emboss-bug（参见 邮件列表）

emboss-dev（参见 邮件列表）

emboss.default 文件（参见 EMBOSS 配置文件）

emboss.default.template 文件, 10

emboss.h 文件, 27, 64, 75, 147, 464, 577

环境变量, 5, 79, 420

错误处理, 76

示例应用程序（参见 演示应用程序）

异常处理函数, 78, 409, 410

异常消息, 77, 159, 409
  - 自定义, 410

特征计算属性（参见 计算属性）

功能请求, 22

特征表（参见 序列特征）

特征（参见 序列特征）

文件格式, 52
  - 报告（参见 应用程序报告格式）
  - 序列（参见 序列格式）

文件输入, 499
  - 用于文件输入的 ACD 数据类型, 99, 321, 499, 533, 534
  - 文件输入的 ACD 定义, 111, 322, 499, 533, 534
  - 用于文件输入的 AJAX 函数, 321, 333, 335
  - 用于文件输入的 AJAX 对象, 325
  - 命令行中文件输入的规范, 99
  - 与数据类型关联的限定符（参见 与数据类型关联的限定符）
  - 从 ACD 文件中检索文件输入, 326

文件输出
  - 用于文件输出的 ACD 数据类型, 101, 322, 505, 546
  - 文件输出的 ACD 定义, 112, 113, 323, 505, 546
  - 用于文件输出的 AJAX 函数, 321, 334, 336
  - 用于文件输出的 AJAX 对象, 325
  - 命令行中文件输出的规范, 101
  - 与数据类型关联的限定符（参见 与数据类型关联的限定符）
  - 从 ACD 文件中检索文件输出, 327

ACD 文件中的文件部分（参见 ACD 文件部分）

库 C 文件中的文件部分, 603（参见 库 C 文件中的部分）

文件列表, 105, 322, 325, 326, 331, 499, 533

文件, 321
  - 处理缓冲文件, 338
  - 查询文件属性, 338
  - 读取（参见 文件输入）
  - 写入（参见 文件输出）

标志（参见 命令行限定符）

自由软件, xxiii

函数名, 17, 579, 602, 605, 610
  - 应用程序, 593
  - 库, 593
  - 参数名和, 593, 602

功能部分（参见 函数）

函数, 592
  - 添加, 72
  - 应用程序, 593
  - 类别, 602, 603
  - 代码布局, 62, 149, 575, 583, 589, 594, 602
  - 关于函数的文档, 14, 15, 17, 19, 568
  - 文档, 65, 594, 602, 609
  - 文档标记, 602, 608, 610
  - 库, 593
  - 命名规则, 593, 602, 605
  - 参数代码（参见 参数代码）
  - 原型, 156, 164, 578, 579, 592

getz, 420

全局属性, 103, 523

全局限定符（参见 命令行限定符）

全局变量（参见 变量）

GNU 通用公共（参见 许可）

GNU 通用公共许可证（参见 许可）

GNU 宽通用公共（参见 许可）

GNU 宽通用公共许可证（参见 许可）

GNU 工具, 32, 65

GPL（参见 许可）

图表函数, 390, 395
  - 用于计算图表属性, 402
  - 用于创建窗口, 398
  - 用于绘图, 398
  - 用于图表初始化, 396
  - 用于图形文件管理, 395
  - 用于检索图表属性, 401
  - 用于设置要渲染的图形元素, 399

图形 ACD 数据类型, 102, 512
  - 属性, 114

图形设备, 512
  - png, 6
  - ps, 512
  - X11, 512

图表, 390
  - 用于图表的 ACD 数据类型, 391, 512
  - 图表的 ACD 定义, 391, 555
  - AJAX 函数（参见 图表函数）
  - 用于图表的 AJAX 对象, 392
  - 命令行中图表的规范, 512, 555
  - 与数据类型关联的限定符（参见 与数据类型关联的限定符）（参见 调试）
  - 从 ACD 文件中检索图表, 393

groups.standard 文件（参见 应用程序组名称文件）

哈希表, 379
  - 用于哈希表的 AJAX 数据类型, 379
  - 函数, 379, 382

头文件, 23, 28, 63, 64, 75, 147, 149, 577, 579, 582, 587, 590, 602, 609

帮助信息（参见 ACD 数据属性）

隐马尔可夫模型, 451

内置功能, 51

包含文件（参见 头文件）

输入 ACD 数据类型, 98, 496
  - 属性, 98, 496

输入文件（参见 文件输入）

ACD 文件中的输入部分（参见 ACD 文件部分）

安装, 2, 66
  - EMBASSY 包的安装（参见 EMBASSY 安装）
  - 库的安装, 7

将代码集成到 EMBOSS 中, 65, 458

接口
  - 编程式, 612

IUB 基础代码, 259

关键字（参见 keywords.standard 文件）
  - keywords.standard 文件, 93
  - knowntypes.standard 文件, 107, 140, 523

LGPL（参见 许可）

libpng, 6

库（参见 C 编程库）
  - AJAX（参见 AJAX）
  - NUCLEUS（参见 NUCLEUS）

库代码文档（参见 文档标准）

库文档, 12, 13, 568, 582

库函数（参见 函数）

libtool, 2, 5, 65

许可, xxiii, 1, 27, 61
  - AJAX, 1
  - EMBASSY, 2
  - EMBOSS, 1
  - GPL, 1
  - LGPL, 2
  - NUCLEUS, 1

链接到 EMBOSS 库, 60

列表函数, 250, 355, 369
  - 用于列表构建, 356, 357, 359, 360, 363
  - 用于列表转换, 368
  - 用于列表销毁, 356, 357, 364, 365
  - 用于列表编辑, 363
  - 用于列表迭代, 361
  - 用于列表排序, 366
  - 用于节点检索, 360
  - 用于查询列表, 362

列表, 354
  - 用于列表的 ACD 数据类型, 102, 113, 263, 355, 509, 554
  - 列表的 ACD 定义, 461
  - 列表的 ACD 定义, 113, 385, 509, 554
  - AJAX 函数（参见 列表函数）
  - 用于列表的 AJAX 对象, 355
  - 命令行中列表的规范, 102
  - 与数据类型关联的限定符（参见 与数据类型关联的限定符）
  - 文件列表, 326, 331, 337, 497, 499
  - 序列模式列表, 227, 232
  - 从 ACD 文件中检索列表, 388

更改日志文件, 69

调试消息的日志记录（参见 调试）

邮件存档, 21

邮件列表, 20, 56

main() 函数, 26, 28, 33, 42, 189, 438, 439, 477, 578, 599

维护, xxiii, 51, 65, 450, 453

make check 命令（参见 编译）

make clean（参见 编译）

make 命令（参见 编译）

make install 命令（参见 编译）

make uninstall（参见 编译）

Makefile.am 文件, 30, 32, 38, 63, 65, 66, 68, 70, 73, 144, 185

Makefile.in 文件, 4, 65

Makefile 文件, 5, 6, 32, 63, 65, 66, 68

数学函数, 404

成员数据, 154

内存, 157
  - 地址, 16, 150, 156, 162
  - 分配, 164, 167, 595
  - 释放, 166, 169, 596
  - 用于 ACD 数据, 29, 165, 439
  - 泄漏, 80, 161, 596
  - 管理, 37, 49, 154, 157, 162, 166
  - 管理宏, 158, 160, 179
  - 使用测试, 414

菜单, 384
  - 用于菜单的 ACD 数据类型, 102, 385
  - 菜单的 ACD 定义, 113, 385
  - 用于菜单的 AJAX 函数, 385
  - 用于菜单的 AJAX 对象, 388
  - 列表, 385
  - 从 ACD 文件中检索菜单, 265, 388, 389
  - 选择, 385

缺少的输入文件, 111, 533, 534

MRC, xx

myemboss, 23, 62, 63, 65, 66, 70, 185, 420, 427, 576

命名结构（参见 Object）

ACD 文件中的否定, 133
  - 运算符（参见 ACD 运算符）

NUCLEUS, 13, 58, 74, 185, 188, 569, 591

对象, 148, 154, 166, 590
  - 构建, 158, 164, 167, 595
  - 定义, 149, 155, 166, 582, 590
  - 销毁, 158, 166, 169, 596
  - 文档, 600, 606
  - 文档标记（参见 文档标记）
  - 函数, 156, 592
  - 宏, 158, 160
  - 内存管理（参见 内存）
  - 命名, 156, 591
  - 指针, 16, 156, 591

开源, xxiii

操作, 120, 136, 139, 563
  - 算术, 124, 564
  - 布尔逻辑, 125, 565
  - 用于条件语句, 565（参见 条件语句）
  - 相等性测试, 125, 564
  - 用于检索数据定义值, 115, 121, 557, 563
  - 类型, 120, 121
  - 用于计算（参见 ACD 计算）
  - 用于条件语句（参见 条件语句）

运算符（参见 ACD 运算符）

输出 ACD 数据类型, 100, 321, 503
  - 属性, 540

输出文件
  - 缺失, 112
  - 命名, 110, 112, 134
  - 限定符（参见 与数据类型关联的限定符）
  - 写入（参见 文件输出）

ACD 文件中的输出部分（参见 ACD 文件部分）

pam, 113, 460

参数代码, 609, 610

参数名（参见 命令行限定符）

ACD 文件中的参数, 36, 37, 59, 61, 84, 104, 435, 455, 457, 517
  - 声明, 86, 104, 129, 434, 436, 486, 489, 518
  - 名称验证, 140
  - 命名约定, 97, 458, 469, 486

C 函数的参数, 14, 17, 156, 575, 602, 609
  - 代码（参见 参数代码）

名称验证, 593

模式匹配, 226

Perl 兼容正则表达式库 (PCRE), 494, 530

系统发生 ACD 数据类型（参见 系统发生数据）

系统发生数据, 304
  - 用于系统发生数据的 ACD 数据类型, 100, 101, 305, 503, 505, 506, 507, 549
  - 系统发生数据的 ACD 定义, 306, 549
  - 用于系统发生数据的 AJAX 函数, 304
  - 用于系统发生数据的 AJAX 对象, 305
  - 命令行中系统发生数据的规范, 503, 505, 506, 507
  - 与数据类型关联的限定符（参见 与数据类型关联的限定符）
  - 调试（参见 调试）
  - 读取, 313, 503
  - 从 ACD 文件中检索系统发生数据, 309, 310

系统发生学（参见 系统发生数据）

规划 EMBOSS 开发, 25, 58

PNG（参见 图形设备）

指针（参见 C 指针）

移植（参见 应用程序）

Postscript（参见 图形设备）

程序流, 595

程序初始化, 92, 188, 392

编程式接口（参见 接口）

编程指南, 19

项目管理, 53

提示, 29, 52, 105, 129, 412, 496, 521
  - 用于控制的 ACD 属性（参见 ACD 数据属性）
  - 行为, 86, 129
  - 用于布尔值, 135
  - 设置, 133
  - 启用, 39, 86

原型（参见 函数）

ps 文件（参见 图形设备）

qatest.dat 文件, 415, 444
  - 用于其中的测试记录, 415

限定符名（参见 命令行限定符）

限定符（参见 命令行限定符）

质量保证 (QA), 64, 414
  - 应用程序（参见 应用程序质量保证测试）





## INDEX

随机数生成, 405

范围文件, 202, 493

范围, 194
ACD 数据类型用于, 195, 493, 527
ACD 定义用于, 197, 527
AJAX 函数用于, 195, 200, 201, 202
AJAX 对象用于, 198
命令行规范用于, 493
从 ACD 文件检索用于, 200

重构,

正则表达式, 226, 494, 527, 560
用于验证用户输入, 110
函数用于, 226

发布, 53
开发者 (CVS), 2

远程数据服务器, 52

报告格式 (参见 应用程序报告格式)

报告输出 (参见 应用程序报告)

报告错误 (参见 错误报告)

报告 (参见 应用程序报告)

ACD 文件中的必需部分 (参见 ACD 文件部分)

资源定义, 79, 423

检索 ACD 值 (参见 ACD 文件)

rformat 限定符 (参见 应用程序报告)

舍入, 405

SCOP, 501, 507, 569

库 C 文件中的部分, 602

sections.standard 文件, 90, 491

选择 ACD 数据类型, 102, 388, 509
属性, 387, 509, 554

序列, 234
登录号, 235
应用程序, 433
命令行规范 (参见 统一序列地址)
比较, 38, 287, 296
文件格式 (参见 序列格式)
属性, 256, 257
翻译 (参见 序列翻译)

序列比对, 287, 296
ACD 数据类型用于, 38, 101, 105, 297, 540
ACD 定义用于, 297, 503, 540
AJAX 函数用于, 42, 297, 301
AJAX 对象用于, 42, 299
应用程序用于, 38
命令行规范用于, 112, 503
数据类型关联限定符用于 (参见 数据类型关联限定符)
调试 (参见 调试)
输入 (参见 序列比对输入)
输出 (参见 序列比对输出)
从 ACD 文件检索用于, 299

序列比对输入, 297
ACD 数据类型用于, 237, 297, 502
ACD 定义用于, 238, 240, 297, 502
AJAX 对象用于, 239, 299
命令行规范用于, 112

序列比对输出, 297
ACD 数据类型用于, 297, 503
ACD 定义用于, 298, 503
AJAX 对象用于, 299
命令行规范用于, 112

序列计算属性 (参见 计算属性)

序列比较 (参见 序列函数)

序列数据库 (参见 数据库)
读取 (参见 序列输入)
写入 (参见 序列输出)

序列特征输入, 273
ACD 数据类型用于, 99, 273, 498
ACD 定义用于, 273, 498
AJAX 函数用于, 272, 279, 281
AJAX 对象用于, 275
命令行规范用于, 498
数据类型关联限定符用于 (参见 数据类型关联限定符)
从原始特征表, 273, 281
从序列文件, 110, 273, 436, 439, 501, 502
从 ACD 文件检索用于, 276

序列特征输出, 273, 342
ACD 数据类型用于, 101, 273, 503
ACD 定义用于, 273, 503
AJAX 函数用于, 272, 279, 281, 282
AJAX 对象用于, 275
命令行规范用于, 503
数据类型关联限定符用于 (参见 数据类型关联限定符)
从 ACD 文件检索用于, 276
指定文件名用于, 111
到序列文件, 111, 273, 508, 509

序列特征, 270, 343
读取 (参见 序列特征输入)
写入 (参见 序列特征输出)

序列格式, 234
设置输出 (参见 序列输出)
指定输入, 535, 536, 538, 539
指定输出, 239, 551, 552, 553

序列函数, 203, 236, 272, 365, 368, 437
用于转换, 259, 295
用于调试 (参见 调试)
用于输出, 243, 250, 252
用于从 ACD 文件检索序列, 240

序列处理 (参见 序列函数)

序列输入, 241, 469, 472
ACD 数据类型用于, 99, 237
ACD 定义用于, 104, 238, 240, 433
AJAX 对象用于, 239
命令行规范用于, 52, 97, 486, 535, 536, 538, 539 (参见 统一序列地址)
用于序列集, 242, 249, 252
用于序列流, 241, 252
用于单个序列, 241, 247, 251
格式规范, 535, 536, 538, 539
从数据库, 10, 241
从文件, 241
多个, 241
范围规范, 122, 123, 127, 200, 243, 405, 493, 535, 536, 538, 539
从 ACD 文件检索, 241
类型规范, 126, 259, 535, 536, 538, 539
带序列特征, 274, 504

序列操作 (参见 序列函数)

序列对象, 239
用于操作的函数 (参见 序列函数)
获取和设置元素, 253
加载, 247, 249, 251
内存管理, 245

序列输出, 242, 243
ACD 数据类型用于, 100, 238, 501, 502, 508, 509, 535, 536, 537, 538, 551, 553
ACD 定义用于, 104, 238, 240, 433, 501, 502, 508, 509, 535, 536, 537, 538, 551, 553
AJAX 对象用于, 239
命令行规范用于, 52, 97, 486, 551, 552, 553
用于多个序列集, 242, 244
用于序列集, 242, 244
用于序列流, 244
用于单个序列, 244
格式规范, 239, 243, 551, 552, 553
多个, 242
范围规范, 405, 493
从 ACD 文件检索, 242
单个, 242
到数据库, 244
到文件, 244
带序列特征, 239, 274, 281, 342, 504

序列模式, 226
ACD 数据类型用于, 227, 489, 527
ACD 定义用于, 110, 228, 527
AJAX 对象用于, 229 (参见 调试)
命令行规范用于, 489
函数用于, 227, 232
从 ACD 文件检索, 229

序列范围 (参见 序列输入)

序列读取 (参见 序列输入)

序列集, 237, 239, 242, 243, 244, 249, 252, 297, 537, 538, 553, 557, 558
输入 (参见 序列输入)
输出 (参见 序列输出)

序列集, 249

序列流, 237, 239, 241, 244, 252, 256, 439, 502, 536, 557
输入 (参见 序列输入)
输出 (参见 序列输出)

序列翻译, 263, 314
ACD 数据类型用于, 263
ACD 定义用于, 264
函数用于, 263
对象, 265
反向, 268, 320

序列类型, 561

ACD 文件中的规范, 39, 437, 528

ACD 文件中的规范, 110, 111, 127, 535, 536, 537, 538, 540, 551, 553

命令行上的规范 (参见 序列输入)

验证, 259

序列写入 (参见 序列输出)

设置提示符 (参见 提示)

设置你的路径, 8

共享库, 1

简单 ACD 数据类型, 98, 109, 194, 492, 557

站点范围配置 (参见 配置)

SoapLab, 109, 451, 515, 524, 612

软件, 51
设计, 58
开发模型, 55
生命周期, 55
发布模型, 53
用户需求 (参见 用户需求)

软件需求 (参见 依赖项)

SourceForge, 22

SRS, 15, 568
EBI 服务器, 15, 568
SRS 数据库, 16, 568
EDATA, 16, 568
EDATAREL, 16, 568
EFUNC, 16, 568
EFUNCREL, 16, 568

稳定版本 (参见 发布)

Staden, 395

标准 ACD 文件部分文件 (参见 ACD 文件部分文件)

标准文档标题 (参见 应用程序文档)

标准标题 (参见 应用程序文档)

标准提示文件, 105

标准限定符 (参见 命令行限定符)

库 C 文件中的标准部分 (参见 库 C 文件中的部分)

存储类和链接, 149

字符串, 204
ACD 数据类型用于, 205, 495, 529
ACD 定义用于, 46, 206, 529, 557
AJAX 函数用于 (参见 字符串函数)
AJAX 对象用于, 155, 171, 206, 607
C 类型, 224
命令行规范用于, 495
构造 (参见 字符串函数)
销毁 (参见 字符串函数)
从 ACD 文件检索用于, 206, 207

字符串函数, 47, 48, 176, 203, 205, 234, 248, 257, 269, 340, 341, 357, 360, 379, 605
用于赋值, 209
用于组合, 210
用于比较, 217
用于转换, 215
用于格式化, 225
用于迭代, 220
用于对象构造, 162, 168, 172, 207, 208
用于对象销毁, 162, 175, 207
用于解析, 219
用于属性, 215
用于查询, 214
用于引用, 208
用于替换, 214
用于标记化, 222

字符串处理, 45, 204

字符串类型, 110

字符串类型文件 (参见 knowntypes.standard 文件)

结构化注释 (参见 代码中的注释)

子序列 (参见 序列输入)

替换矩阵 (参见 比较矩阵)

建议新功能 (参见 功能请求)

系统调用, 406, 407, 468

标签 (参见 文档标签)

三元条件语句 (参见 条件语句)

测试数据库, 9, 423

测试目录, 10, 418, 421

相等性测试 (参见 操作)

输入的类型检查 (参见 ACD 数据属性)

UFO (参见 统一特征对象)

一元条件语句 (参见 条件语句)

统一特征对象, 52, 253, 270

统一序列地址, 52, 99, 100, 101, 235, 253, 501

USA (参见 统一序列地址)

用户提示 (参见 提示)

用户需求, 56

变量, 575, 588
ACD (参见 ACD 变量)
地址 (参见 内存)
声明, 150, 439, 464, 589
环境 (参见 环境变量)
全局, 578, 582, 588
初始化, 589
命名, 583
variables.standard 文件 (参见 环境变量文件)

版本号, 5, 9, 53, 72, 515, 599

Wellcome Trust, xx

包装器 (参见 应用程序)

X-Windows (参见 图形设备)

X11 (参见 图形设备)

XML, 569





欧洲分子生物学开源软件套件（EMBOSS）是一个高质量、文档齐全的开源软件工具包，用于分子生物学。它在统一的命令行界面下包含超过200个生物信息学应用程序，并由许多图形界面和工作流软件支持。EMBOSS包含广泛且可扩展的C编程库，为从零开始开发新的生物信息学工具提供了强大且健壮的工具包。

- 利用丰富的内置功能，几乎无需或无需额外编码。
- 全面且一致的应用程序编程接口（API）。
- 强大的命令行界面自动处理。
- 提供大量限定符，用于控制程序行为和指定IO数据。
- 支持简单和复杂（生物学）数据类型，并具有易于配置的数据库。
- 利用自动文件格式处理——无需自行编码。
- 代码文档齐全并已编入索引，便于搜索和导航；无需深入了解内部实现。
- 所有代码均采用ANSI标准C编写，并制定了编码和文档标准。

《EMBOSS开发者指南》是在EMBOSS下开发软件的官方权威指南。它包含全面的参考信息和指南，包括逐步说明和现实世界的代码示例：

- 了解如何在EMBOSS开发人员的指导下编写功能齐全的工具。
- 内容全面且及时更新——您需要的所有信息触手可及。
- 编写EMBOSS应用程序的逐步指南，配有功能性、已部署的代码示例。
- ACD文件开发——了解如何在不编码的情况下自定义现有工具，或设计和编写全新的应用程序界面。
- EMBOSS API编程指南——按主题组织，帮助您快速掌握应用程序开发。
- 在EMBOSS下封装和移植应用程序——了解如何集成第三方工具。
- 无需事先具备EMBOSS经验。

EMBOSS团队感谢慷慨支持该项目的组织，包括威康信托、医学研究委员会、生物技术与生物科学研究委员会（BBSRC）和EMBL-EBI。

剑桥大学出版社 www.cambridge.org ISBN 978-0-521-60724-7 9 780521 607247>


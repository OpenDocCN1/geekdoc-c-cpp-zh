

弗兰克·M·卡拉诺 • 蒂莫西·M·亨利

# 使用 C++ 进行数据抽象与问题求解

# 墙与镜子

第七版

## C++ 保留关键字

C++ 为以下关键字保留并赋予预定义含义。您不得重新定义关键字或将其用于其他目的。以彩色显示的关键字是自 C++11 以来新增的。

| alignas | decltype | namespace | struct |
| :--- | :--- | :--- | :--- |
| alignof | default | new | switch |
| and | delete | noexcept | template |
| and_eq | do | not | this |
| asm | double | not_eq | thread_local |
| auto | dynamic_cast | nullptr | throw |
| bitand | else | operator | true |
| bitor | enum | or | try |
| bool | explicit | or_eq | typedef |
| break | export | private | typeid |
| case | extern | protected | typename |
| catch | false | public | union |
| char | float | register | unsigned |
| char16_t | for | reinterpret_cast | using |
| char32_t | friend | return | virtual |
| class | goto | short | void |
| compl | if | signed | volatile |
| const | inline | sizeof | wchar_t |
| const_cast | int | static | while |
| constexpr | long | static_assert | xor |
| continue | mutable | static_cast | xor_eq |

| 运算符 | 含义 | 结合性 | 用法 |
|---|---|---|---|
| `*` | 乘法 | 左 | `expr * expr` |
| `/` | 除法 | 左 | `expr / expr` |
| `%` | 取模 | 左 | `expr % expr` |
| `+` | 加法 | 左 | `expr + expr` |
| `-` | 减法 | 左 | `expr - expr` |
| `<<` | 按位左移‡ | 左 | `expr << expr` |
| `>>` | 按位右移‡ | 左 | `expr >> expr` |
| `<` | 小于 | 左 | `expr < expr` |
| `<=` | 小于或等于 | 左 | `expr <= expr` |
| `>` | 大于 | 左 | `expr > expr` |
| `>=` | 大于或等于 | 左 | `expr >= expr` |
| `==` | 等于 | 左 | `expr == expr` |
| `!=` | 不等于 | 左 | `expr != expr` |
| `&` | 按位 AND | 左 | `expr & expr` |
| `^` | 按位异或 | 左 | `expr ^ expr` |
| `` `|` `` | 按位 OR | 左 | `expr \| expr` |
| `&&` | 逻辑 AND | 左 | `expr && expr` |
| `\|\|` | 逻辑 OR | 左 | `expr \|\| expr` |
| `? :` | 条件运算符 | 左 | `expr ? expr : expr` |
| `=` | 赋值 | 左 | `lvalue = expr` |
| `*=` | 乘法并赋值 | 左 | `lvalue *= expr` |
| `/=` | 除法并赋值 | 左 | `lvalue /= expr` |
| `%=` | 取模并赋值 | 左 | `lvalue %= expr` |
| `+=` | 加法并赋值 | 左 | `lvalue += expr` |
| `-=` | 减法并赋值 | 左 | `lvalue -= expr` |
| `<<=` | 左移并赋值 | 左 | `lvalue <<= expr` |
| `>>=` | 右移并赋值 | 左 | `lvalue >>= expr` |
| `&=` | AND 并赋值 | 左 | `lvalue &= expr` |
| `\|=` | OR 并赋值 | 左 | `lvalue \|= expr` |
| `^=` | 异或并赋值 | 左 | `lvalue ^= expr` |
| `,` | 逗号 | 左 | `expr, expr` |

‡ 通常用于 I/O 重载

# 使用 C++ 进行数据抽象与问题求解

# 墙与镜子

弗兰克·M·卡拉诺  
罗德岛大学

蒂莫西·亨利  
罗德岛大学

皮尔逊

- ECS 副总裁兼编辑总监：Marcia J. Horton
- 执行编辑：Tracy Johnson
- 副编辑：Carole Snyder
- 市场总监：Christy Lesko
- 市场经理：Yez Alayan
- 市场助理：Jon Bryant
- 制作总监：Erin Gregg
- 主编：Jeff Holcomb
- 副主编：Robert Engelhardt
- 制造采购员：Lisa McDowell
- 美术总监：Anthony Gemmellaro
- 封面设计师：Liz Harasymczuk
- 版权主管：Michael Joyce
- 版权管理员：Jennell Forscher
- 图像资产服务总监：Annie Atherton
- 视觉研究经理：Karen Sanatar
- 封面艺术：Shutterstock/SVLuma
- 媒体项目经理：Renata Butera
- 全方位项目经理：Rose Kernan
- 排版：Cenveo Publisher Services / Nesbitt
- 印刷/装订：Edwards Brothers
- 封面印刷：Lehigh-Phoenix Color/Hagerstown

美国国会图书馆出版数据已存档。

欢迎阅读《使用 C++ 进行数据抽象与问题求解：墙与镜子》第六版。自第一版出版以来，我们都在使用 C++ 以面向对象的方式教授数据抽象方面积累了经验。本版反映了这些经验，以及来自教师和学生的众多评论和建议。

我很高兴介绍我的合著者、罗德岛大学的同事蒂莫西·亨利博士。我们共同对本书进行了急需的修订和全新设计。然而，我们的目标始终是为学生提供数据抽象、面向对象编程及其他现代问题求解技术的卓越基础。所有 C++ 代码均已重写，重点在于安全可靠的编程实践。它还遵循 C++11 标准。

希望您喜欢阅读本书。和您之前的许多人一样，您可以以高效且可持续的方式学习——或教授——数据结构。

# 与我们联系

《墙与镜子》在不断发展。您的评论、建议和纠错将不胜感激。以下是联系我们的几种方式：

- 电子邮件：carrano@acm.org
- Facebook：www.facebook.com/makingitreal
- Twitter：twitter.com/Frank_M_Carrano
- 博客：frank-m-carrano.com/makingitreal

![](img/288a0c22d14d2450c1e772f228f867b0_5_0.png)

## 致学生

本书涵盖的主题涉及组织数据的各种方式，以便给定应用程序能够高效地访问和操作数据。这些主题对您未来的计算机科学学习至关重要，因为它们为创建复杂可靠的软件提供了所需的知识基础。无论您对设计视频游戏还是机器人控制手术软件感兴趣，数据结构的学习对您的成功都至关重要。即使您现在不学习本书中的所有主题，以后也可能会遇到它们。希望您喜欢阅读本书，并希望它能成为您未来课程的有用参考工具。

标题中的“墙”与“镜子”代表了贯穿本书的两种基本问题求解技术。数据抽象将模块的实现细节与程序的其余部分隔离并隐藏，很像一堵墙可以将您与邻居隔开并隐藏起来。递归是一种重复技术，通过求解完全相同但更小的问题来解决一个问题，很像面对面的镜子中的图像随着每次反射而变小。

请务必浏览本序言的其余部分，了解有助于您学习的功能。为了帮助您学习和复习考试，我们包含了视频教程（VideoNotes）、带答案的检查点问题、页边注释、编程提示、章节摘要和术语表等学习辅助工具。在编程过程中，您将在附录和书籍封面内找到 C++ 参考资料。您应该查阅本序言后面“用于增强学习的功能”部分中给出的本书功能列表。

本书的讲解对您的 C++ 知识做了一些基本假设。你们中的一些人可能需要通过查阅本书的附录来复习这门语言或第一次学习它。本书在特定章节之间的新 C++ 插曲中介绍了 C++ 类和语言的其他相关方面。这些插曲不假设您已经了解其主题。我们假设您没有递归函数的经验，这些函数包含在第 2 章和第 5 章中。

本书中出现的所有 C++ 源代码均可供您使用。本序言后面关于补充材料的描述将告诉您如何获取这些文件，以及 VideoNotes 和其他在线文档。

# 组织结构

本书的组织、排序和主题覆盖节奏通过一次专注于一个概念、提供覆盖主题顺序的灵活性，以及清晰区分抽象数据类型（ADT）的规范与实现，使学习和教学更加容易。为了实现这些目标，我们将材料组织为 21 个章节。大多数章节侧重于 ADT 的规范和使用或其各种实现。您可以选择先覆盖 ADT 的规范，再覆盖其实现，也可以在考虑任何实现问题之前，先处理多个 ADT 的规范和使用。本书的组织使您可以轻松选择您偏好的主题顺序。

# 目录概览

以下列表显示了本书的总体构成。进一步的章节描述将在后面出现。请注意，灰色高亮部分可在线查阅。

- 第 1 章 数据抽象：墙
- C++ 插曲 1 C++ 类
- 第 2 章 递归：镜子
- 第 3 章 基于数组的实现
- C++ 插曲 2 指针、多态性和内存分配
- 第 4 章 基于链接的实现
- 第 5 章 递归作为问题求解技术
- 第 6 章 栈
- C++ 插曲 3 异常
- 第 7 章 列表实现
- 第 8 章 列表
- 第 9 章 列表实现
- 第 10 章 算法效率
- 第 11 章 排序算法及其效率
- C++ 插曲 4 类关系与复用
- 第 12 章 有序列表及其实现
- 第 13 章 队列与优先队列
- 第 14 章 队列实现
- C++ 插曲 5 重载运算符和友元访问
- 第 15 章 树
- 第 16 章 树的实现
- C++ 插曲 6 迭代器
- 第 17 章 堆
- 第 18 章 字典及其实现
- 第 19 章 平衡搜索树
- 第 20 章 图
- 第 21 章 处理模板库
- C++ 插曲 7 标准 C++ 基础
- 附录 A 编程主题回顾
- 附录 B Java 编程语言简介
- 附录 C 统一建模语言
- 附录 D 软件生命周期
- 附录 E 数学归纳法
- 附录 F 算法验证
- 附录 G 文件
- 附录 H 头文件和标准函数
- 附录 I C++ 头文件和标准函数
- 附录 J 文档系统
- 附录 K ASCII 字符代码
- 附录 L 面向 Java 程序员的 C++
- 附录 M 面向 Python 程序员的 C++
- 索引
- 术语表
- 检查点问题答案




## SIXTH EDITION

## C++ 数据抽象与问题求解

## 墙与镜子

FRANK M. CARRANO | TIMOTHY HENRY

## C++ Reserved Keywords

C++ reserves and gives predefined meanings to the following keywords. You may not redefine keywords or use them for other purposes. Keywords that appear in color are new since C++11.

| alignas | decltype | namespace | struct |
| --- | --- | --- | --- |
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
| * | 乘法 | 左 | `expr * expr` |
| / | 除法 | 左 | `expr / expr` |
| % | 取模 | 左 | `expr % expr` |
| + | 加法 | 左 | `expr + expr` |
| - | 减法 | 左 | `expr - expr` |
| << | 按位左移‡ | 左 | `expr << expr` |
| >> | 按位右移‡ | 左 | `expr >> expr` |
| < | 小于 | 左 | `expr < expr` |
| <= | 小于或等于 | 左 | `expr <= expr` |
| > | 大于 | 左 | `expr > expr` |
| >= | 大于或等于 | 左 | `expr >= expr` |
| == | 等于 | 左 | `expr == expr` |
| != | 不等于 | 左 | `expr != expr` |
| & | 按位与 | 左 | `expr & expr` |
| ^ | 按位异或 | 左 | `expr ^ expr` |
| `|` | 按位或 | 左 | `expr | expr` |
| && | 逻辑与 | 左 | `expr && expr` |
| || | 逻辑或 | 左 | `expr || expr` |
| ? : | 条件运算 | 左 | `expr ? expr : expr` |
| = | 赋值 | 左 | `lvalue = expr` |
| *= | 乘法赋值 | 左 | `lvalue *= expr` |
| /= | 除法赋值 | 左 | `lvalue /= expr` |
| %= | 取模赋值 | 左 | `lvalue %= expr` |
| += | 加法赋值 | 左 | `lvalue += expr` |
| -= | 减法赋值 | 左 | `lvalue -= expr` |
| <<= | 左移赋值 | 左 | `lvalue <<= expr` |
| >>= | 右移赋值 | 左 | `lvalue >>= expr` |
| &= | 按位与赋值 | 左 | `lvalue &= expr` |
| \|= | 按位或赋值 | 左 | `lvalue \|= expr` |
| ^= | 按位异或赋值 | 左 | `lvalue ^= expr` |
| , | 逗号 | 左 | `expr, expr` |

‡ 通常用于 I/O 重载

## C++ 数据抽象与问题求解

## 墙与镜子

## SIXTH EDITION

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_3_0.png)

Frank M. Carrano
University of Rhode Island

Timothy Henry
University of Rhode Island

PEARSON

ECS 副总裁兼编辑总监：Marcia J. Horton
执行编辑：Tracy Johnson
副编辑：Carole Snyder
市场总监：Christy Lesko
市场经理：Yez Alayan
市场助理：Jon Bryant
制作总监：Erin Gregg
主编：Jeff Holcomb
副主编：Robert Engelhardt
制造采购员：Lisa McDowell
美术总监：Anthony Gemmellaro

封面设计师：Liz Harasymczuk
版权主管：Michael Joyce
版权管理员：Jennell Forscher
图像资产服务总监：Annie Atherton
视觉研究经理：Karen Sanatar
封面艺术：Shutterstock/SVLuma
媒体项目经理：Renata Butera
全方位项目经理：Rose Kernan
排版：Cenveo Publisher Services / Nesbitt
印刷/装订：Edwards Brothers
封面印刷：Lehigh-Phoenix Color/Hagerstown

本教材中从其他来源借用并经许可复制的致谢和鸣谢出现在正文的相应页面上。

版权 © 2013, 2007, 2005 Pearson Education, Inc.，以 Addison-Wesley 名义出版。版权所有。在美国印刷。本出版物受版权保护，在任何禁止的复制、存储在检索系统中或以任何形式或任何方式（电子、机械、影印、录制或其他）传播之前，应事先获得出版商的许可。如需获取使用本作品材料的许可，请将书面请求提交至 Pearson Education, Inc., Permissions Department, One Lake Street, Upper Saddle River, New Jersey 07458，或将请求传真至 201-236-3290。

制造商和卖家用于区分其产品的许多名称均声称为商标。当这些名称出现在本书中，且出版商知晓商标主张时，这些名称已以首字母大写或全大写形式印刷。

美国国会图书馆出版前编目数据已存档。

10 9 8 7 6 5 4 3 2 1

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_4_0.png)

ISBN 10: 0-13-292372-6
ISBN 13: 978-0-13-292372-9

欢迎阅读第六版《C++ 数据抽象与问题求解：墙与镜子》。自第一版出版以来，我们都积累了使用 C++ 以面向对象方式教授数据抽象的经验。本版反映了这些经验，以及来自教师和学生的众多评论和建议。

我很高兴介绍我的合著者、罗德岛大学同事 Timothy Henry 博士。我们共同对本书进行了急需的修订和全新设计。然而，我们的目标始终是为学生提供数据抽象、面向对象编程及其他现代问题求解技术的卓越基础。所有 C++ 代码均已重写，重点放在安全可靠的编程实践上，并且符合 C++11 标准。

希望您喜欢阅读本书。和您之前的许多人一样，您可以以高效且可持续的方式学习——或教授——数据结构。

## 与我们交流

《墙与镜子》仍在不断发展。我们非常感谢您的评论、建议和更正。以下是联系我们的几种方式：

- 电子邮件：carrano@acm.org
- Facebook：www.facebook.com/makingitreal
- Twitter：twitter.com/Frank_M_Carrano
- 博客：frank-m-carrano.com/makingitreal

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_5_0.png)

## 致学生

本书涵盖的主题涉及组织数据的各种方式，以便特定应用能够高效地访问和操作数据。这些主题对您未来的计算机科学学习至关重要，因为它们为您创建复杂可靠的软件提供了所需的知识基础。无论您对设计电子游戏还是机器人控制手术软件感兴趣，数据结构的学习对您的成功都至关重要。即使您现在不学习本书中的所有主题，以后也可能会遇到它们。希望您喜欢阅读本书，并将其作为未来课程的有用参考工具。

书名中的“墙”和“镜子”代表了贯穿全书的两种基本问题求解技术。数据抽象将模块的实现细节与程序的其余部分隔离并隐藏，就像墙壁可以将您与邻居隔开并隐藏一样。递归是一种重复技术，通过求解完全相同但更小的问题来解决问题，就像面对面的镜子中的图像随着每次反射而变小一样。

请务必浏览本序言的其余部分，了解有助于您学习的特色功能。为了帮助您学习和复习考试，我们提供了视频教程（VideoNotes）、带答案的检查点问题、页边注释、编程提示、章节摘要和术语表等学习辅助工具。在编程过程中，您将在附录和书籍封面内找到 C++ 参考资料。您应该查看本序言后面“增强学习的功能”部分中给出的本书功能列表。

本内容对您的 C++ 知识做了一些基本假设。你们中的一些人可能需要通过查阅本书的附录来复习这门语言，或第一次学习它。本书在若干章节之间通过新的 C++ 插曲（C++ Interludes）介绍了 C++ 类和其他相关语言方面。这些插曲不假设您已经了解其主题。我们假设您没有递归函数的经验，递归函数包含在第 2 章和第 5 章中。

本书中出现的所有 C++ 源代码均可供您使用。本序言后面关于补充材料的描述将告诉您如何获取这些文件，以及 VideoNotes 和其他在线文档。


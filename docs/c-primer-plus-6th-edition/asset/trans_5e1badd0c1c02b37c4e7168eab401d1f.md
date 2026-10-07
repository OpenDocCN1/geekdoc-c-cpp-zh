
- 总结 699
- 章节回顾 700
- 编程练习 702

## 13 类继承 707
- 从简单的基类开始 708
- 继承：一种“是”（Is-a）的关系 720
- 多态公共继承 722
- 静态与动态绑定 737
- 访问控制：protected 745
- 抽象基类 746
- 继承与动态内存分配 757
- 类设计回顾 766
- 总结 778
- 章节回顾 779
- 编程练习780

## 14 在 C++ 中重用代码 785
- 带有对象的成员类 786
- 私有继承 797
- 多重继承 808
- 类模板 830
- 总结 866
- 章节回顾 869
- 编程练习 871

## 15 友元、异常及其他 877
- 友元 877
- 嵌套类 889
- 异常 896
- 运行时类型识别 933
- 类型转换运算符 943
- 总结 947
- 章节回顾 947
- 编程练习 949

## 16 string 类与标准模板库 951
- string 类 952
- 智能指针模板类 968
- 标准模板库 978
- 泛型编程 992
- 函数对象（又称仿函数） 1026
- 算法 1035
- 其他库 1045

# xii 目录
- 总结 1054
- 章节回顾 1056
- 编程练习 1057

## 17 输入、输出与文件 1061
- C++ 输入/输出概述 1062
- 使用 cout 输出 1069
- 使用 cin 输入 1093
- 文件输入/输出 1114
- 核心格式化 1142
- 总结 1145
- 章节回顾 1146
- 编程练习 1148

## 18 使用新 C++ 标准访问 1153
- 回顾 C++11 特性 1153
- 移动语义与右值引用 1164
- 新类特性 1178
- Lambda 函数 1184
- 包装器 1191
- 变长参数模板 1197
- 更多 C++11 特性 1202
- 语言变化 1205
- 现在怎么办？1207
- 总结 1208
- 章节回顾 1209
- 编程练习 1212

## 附录
- A 进制数 1215
- B C++ 留关键字 1221
- C ASCII 字符集 1225
- D 运算符优先级 1231
- E 其他运算符 1235
- F string 模板类 1249
- G 标准模板库方法与函数 1271
- H 精选读物与网络资源 1323
- I 转换为 ISO 标准 C++ 1327
- J 章节回顾答案 1335
- 索引 1367

## 致谢

### 第六版的致谢
感谢 Pearson 的 Mark Taber 和 Samantha Sinkhorn 对本书项目的指导和管理，感谢 David Horvath 提供的技术评审和编辑。

### 第五版的致谢
感谢 Sams Publishing 的 Loretta Yates 和宋林（Songlin Qi）指导并管理本项目。感谢我的同事 Fred Schmidt 提供的许多实用建议。再次感谢 Metroworks 的 Ron Liefty 提供的极大帮助。

### 第四版的致谢
Pearson 的几位编辑自发发起了并维护了该项目；感谢 Linda Sharp、Karen Wach 和 Laurie McGUire。感谢 Michael Maddox、Bill Braun、Chris Maunder 和 Philippe Bruno 提供技术评审和编辑。再次感谢 Michael Maddox 和 Bill Braun 为《实战笔记》提供素材。最后，我要感谢 Metroworks 的 Ron Liefty 和 Comeau Computing 的 Greg Comeau 在 C++ 编译器方面提供的帮助。

### 第三版的致谢
感谢 Macmillan 和 The Wait Group 的编辑们在本书编制中所扮演的角色：Tracy Dunkelberger、Susan Walton 和 Andrew Rosenberg。感谢 Russ Jacobs 提供的内容和技术编辑。来自 Metroworks 的，我要感谢 Dave Mark、Alex Harper 尤其是 Ron Liefty 提供的帮助与合作。

### 第二版的致谢
感谢 Mitchell Waite 和 Scott Calamar 对第二版的支持，感谢 Joel Fagazzotto 和 Joanne Mueller 指导项目完成。感谢 Metroworks 的 Michael Jacoby 回答我关于其 Beta 版本 CodeWarrior 编译器的问题。我还想感谢以下老师花时间对第一版提供反馈：Jeff Buckwater、Earl Brynner、Mike Holland、Andy Yao、Larry Sanders、Sahin Montami 和 Dan Stephens。最后，我要感谢 Heidi Brumbhager 对新内容和修订内容进行的有用编辑工作。

### 第一版的致谢
许多人对本书做出了贡献。特别要感谢 Mitch Waite 在开发、塑造和重塑本书方面所的工作，以及对手稿的评审。我很感激 Harry。

## 关于作者
Stephen Prata 在加州马林学院教授天文学、物理和计算机科学。他从加州理工学院获得学士学位。他编写或合著了十多本关于编程主题的书，包括获得 1990 年计算机协会最佳入门书奖的《C++》，以及获得计算机协会最佳书籍奖的《C++ Primer》。

## 我们想听听你的意见！
作为本书的读者，你是我们最重要的批评者和评论者。我们想知道我们哪里做得好，哪些地方可以改进，你还希望我们出版哪些领域，你可以通过邮件或写信告诉我们对本书的看法。

邮箱：
feedback@developers-library.info

邮件：
Addison-Wesley Developer's Library
800 East 96th Street
Indianapolis, IN 46234 USA

## 读者服务
访问网站并在 www.informit.com/register 本书，以便获取任何可用更新、下载或错误说明。

## 引言
学习 C++ 是一场发现的冒险，特别是该语言支持多种范式，包括面向对象编程、泛型编程和传统的过程化编程。本书第五版描述的 ISO C++ 标准非正式被称为 C++99 和 C++03，有时被称为 C++99/03。（2003 版本很大程度上是对 1999 标准的技术修正，没有添加任何新功能）。此以后，C++ 继续进化。在本书编写期间，国际 C++ 标准委员会刚刚批准了一个新标准。该标准在开发期间的正式称为 C++0x，现在被称为 C++11。大多数现代编译器都能很好地支持 C++99/03，本书中的大多数示例已经出现在某些实现中，本版 C++ Primer 将探索这些新特性。

《C++ Primer》讨论了 C 语言并介绍了 C++ 特性，使本书内容自洽。它介绍了 C++ 基础，并通过简短、易于复制和实验的程序进行说明。你学习了输入/输出（I/O）、如何让执行重复任务并做出选择、处理数据的多种方法以及如何使用函数。你学习了 C++ 为 C 添加了许多功能，包括：

- 类和对象
- 继承
- 多态、虚函数和运行时类型识别 (RTTI)
- 函数重载
- 引用变量
- 通过模板和标准模板库（STL）提供的泛型或类型无关编程
- 处理错误情况的异常机制
- 用于管理函数、类和变量名称的命名空间

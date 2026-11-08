

Addison-Wesley，马萨诸塞州波士顿，1996

- [MeyersCounting] Scott Meyers。*C++ 中的对象计数*。C/C++ 用户杂志，1998 年 4 月。
- [MeyersEffective] Scott Meyers。*Effective C++——改善程序与设计的 50 种具体方法（第 2 版）*。Addison-Wesley，马萨诸塞州波士顿，1998。
- [MeyersMoreEffective] Scott Meyers。*More Effective C++——改善程序与设计的 35 种新方法*。Addison-Wesley，马萨诸塞州波士顿，1996。
- [MoonFlavors] David A. Moon。*使用 Flavors 的面向对象编程*。面向对象编程系统、语言与应用会议论文集，1986。
- [LalondeLMT] Andrew Lalonde 和 Jeremy Siek。*MTL，元模板库*。http://www.cs.illinois.edu/research/mtl/ http://www.oonumerics.org/oon/
- [MusserWangDVA] D. R. Musser 和 W. Wang。*C++ 泛型算法的动态验证*。IEEE 软件工程汇刊，第 23 卷，第 5 期，1997 年 5 月。
- [MeyersTraits] Nathan C. Meyers。*Traits：一种新颖且有用的模板技术*。http://www.cantrip.org/traits.html http://www.cantrip.org/
- [NewMat] Robert Davies。*NewMat0，一个 C++ 矩阵库*。http://www.robertnz.net/index.htm http://www.robertnz.net/nm_intro.htm
- [NewShorterEng] Leslie Brown（编）。*新简明牛津英语词典（第 4 版）*。牛津大学出版社，牛津，1993。
- [POOMA] *POOMA：用于并行科学计算的高性能 C++ 工具包*。http://www.nongnu.org/freepooma/
- [StrokaBatoryMixins] Yannis Smaragdakis 和 Don S. Batory。*C++ 中基于 Mixin 的编程*。第二届生成式与基于组件的软件工程国际研讨会论文集，2000 年 10 月。
- [SpicerSFINAE] John Spicer。*解决表达式的 SFINAE 问题*。http://www-2.cs.cmu.edu/~.../sfin.../sfin.../
- [StepanovLeeSTL] Alexander Stepanov 和 Meng Lee。*标准模板库——HP 实验室技术报告 96-11(R.1)*。1995 年 11 月 14 日。
- Alexander Stepanov。*编程笔记*。http://stepanov.com/notes.pdf http://stepanov...
- [StroustrupC++PL] Bjarne Stroustrup。*C++ 程序设计语言（特别版）*。Addison-Wesley，马萨诸塞州波士顿，2000。
- [StroustrupEvoC++] Bjarne Stroustrup。*C++ 的设计与演化*。Addison-Wesley，马萨诸塞州波士顿，1994。
- [StroustrupC++Glossary] Bjarne Stroustrup。*Stroustrup 的 C++ 术语表*。http://www.stroustrup.com/glossary.html http://www.stroustrup...
- [SutterExceptional] Herb Sutter。*Exceptional C++——47 个工程谜题、编程问题与解决方案*。Addison-Wesley，马萨诸塞州波士顿，2000。
- [SutterMoreExceptional] Herb Sutter。*More Exceptional C++——40 个新的工程谜题、编程问题与解决方案*。Addison-Wesley，马萨诸塞州波士顿，2004。
- [UnruhPrimeOrig] Erwin Unruh。*素数计算的原始元程序*。http://www.erwin-unruh.de/primorig.html http://www.erwin-unruh.de/...
- [VandevoordeJosuttisTemplates] David Vandevoorde 和 Nicolai M. Josuttis。*C++ 模板：完整指南*。Addison-Wesley，马萨诸塞州波士顿，2003。
- [VandevoordeSolutions] David Vandevoorde。*C++ 解决方案*。Addison-Wesley，马萨诸塞州波士顿，1998。
- [VeldhuizenMeta] Todd Veldhuizen。*使用 C++ 模板元编程*。*C++ 报告*，1995 年 5 月。

## 术语表

本术语表汇编了我们在书中使用的最重要的技术术语。关于 C++ 程序员所用术语的全面通用术语表，请参见 [StroustrupGlossary]。

### 抽象类

一种无法创建对象（实例）的类。抽象类用于对类层次中不同类的共同属性进行建模。抽象类的对立面是具体类。抽象类用于基类；缩写 ABC 有时用于表示抽象基类。

### ADL

参数依赖查找的缩写。ADL 是一种过程，它在每个参数所属的命名空间中查找函数名（或运算符名）（或在包含该函数（或运算符名）的函数调用的参数相关联的命名空间中查找）。由于历史原因，它有时被称为 Koenig 查找（后者也用于应用于运算符的 ADL）。

### 别名模板

表示一族类型别名的构造。它指定一种模式，通过用具体实体替换模板参数，可以从该模式生成实际类型别名。别名模板可以是类成员。

### 尖括号 hack

C++ 的一项特性，要求编译器将两个连续的 `>` 字符接受为关闭两个模板参数列表，尽管这两个字符否则会被解释为整数移位运算符（`>>`）。它被称为 hack，是因为它不能很好地适应 C++ 正式规范（尤其是文法）或 C++ 编译器的总体架构。另一个类似的 hack 处理替代双字符记法（见 digraph）。

### 尖括号

字符 `<` 和 `>` 用作分隔符而不是小于和大于运算符时的称呼。

### ANSI

美国国家标准学会的缩写，这是一个私营非营利组织，协调制定美国标准规范的工作。（见 ISO。）注意 ANSI。

### 实参

在广义上，为参数化实体的形参提供具体内容的值。例如，在函数调用 `f(1)` 中，实参是 1。在某些编程社区中，实参被称为实际参数，而形参被称为形式参数。另见默认实参。

### 参数依赖查找

见 ADL。

### 类

对一组对象的描述。类定义了该类型任何对象的一组特征。这包括数据（属性）、数据成员和操作（方法、成员函数）。在 C++ 中，类是成员可以包含函数并受访问限制约束的结构。它们使用关键字 `class` 或 `struct` 声明。

### 类模板

表示一族类的构造。它表示一种模式，通过用具体实体替换模板参数，可以从该模式生成实际类。类模板有时称为参数化类。

### 类类型

使用 `class`、`struct` 或 `union` 声明的 C++ 类型。

### 集合类

用于管理一组对象的类。在 C++ 中，集合……

### 编译器

将翻译单元中的源代码转换为目标代码（带有符号注释的机器码，这些注释允许链接器解析跨翻译单元的引用）的程序或库组件。

### 完整类型

任何不是不完整的类型：已定义的类、元素类型完整且大小已知的数组、具有已定义底层类型的枚举类型，以及除 `void` 之外的任何基本数据类型（可选地带 `const` 和/或 `volatile`）。

### 概念

一组有名称的约束，可应用于一个或多个模板参数。见附录 E。

### 常量表达式

其值可以由编译器在编译时计算的表达式。有时称为真常量，以避免与非常量（不带连字符）混淆。后者包括常量表达式，但不总能由编译器在编译时计算。

### const 成员函数

一种可对常量对象和临时对象调用的成员函数，因为它通常不修改 `this` 对象的成员。

### 集合

见集合类。

### 转换函数

一种特殊成员函数，定义对象如何隐式（或显式）转换为另一类型的对象。它使用 `operator type ()` 形式声明。

### 转换运算符

转换函数的同义词。后者是标准术语，但前者也常用。

### CPP 文件

用于存放变量和非内联函数定义的文件。程序的大部分可执行代码（相对于声明性代码）通常放在 CPP 文件中。它们被称为 CPP 文件，是因为通常以 `.cpp` 为后缀命名。但出于历史原因，后缀也可能是 `.c`、`.cc` 或 `.cxx`。另见头文件和翻译单元。

### CRTP

奇异递归模板模式的缩写。这指的是一种代码模式，其中类 X 派生自一个以 X 作为模板实参的基类。

### 奇异递归模板模式

见 CRTP。

### 退化

数组或函数到指针的隐式转换。例如，字符串字面量 "Hello" 的类型为 `char const [6]`，但在许多上下文中，它被隐式转换为 `char const*` 类型的指针（指向字符串的第一个字符）。

### 声明

将名称引入或重新引入 C++ 作用域的 C++ 构造。另见定义。

### 推导

从使用模板的上下文中隐式确定模板实参的过程。编译器使用模板实参推导。

### 定义

一种声明，它使所声明实体的细节已知；对于变量，它强制为所声明实体保留存储空间。对于类类型和函数定义，这相当于包含花括号包围的主体的声明。对于非虚变量声明，这意味着要么是不带 extern 关键字的声明，要么是带初始化器的声明。

### 依赖基类

依赖于模板参数的基类。访问依赖基类的成员时必须特别小心。另见两阶段查找。

### 依赖名称


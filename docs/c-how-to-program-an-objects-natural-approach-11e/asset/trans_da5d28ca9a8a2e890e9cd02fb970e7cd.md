
## 16.6.1 模块接口单元的模块声明

图16.2定义了我们的第一个模块单元^37^——一个属于模块的翻译单元。当一个模块由一个翻译单元组成时，该模块单元通常简称为模块。图16.2中的模块包含四个函数（第8–10、14–16、21–23和28–30行），用于演示导出声明以供其他翻译单元使用。在以下小节中，我们将讨论第14–16、21–23和28–30行函数周围的导出和命名空间“包装器”。

```cpp
1  // Fig. 16.2: welcome.ixx
2  // Primary module interface for a module named welcome.
3  export module welcome; // introduces the module name
4
5  import <string>; // class string is used in this module
6
7  // exporting a function
8  export std::string welcomeStandalone() {
9      return "welcomeStandalone function called";
10 }
11
12 // exporting all items in the braces that follow export
13 export {
14     std::string welcomeFromExportBlock() {
15         return "welcomeFromExportBlock function called";
16     }
17 }
18
19 // exporting a namespace exports all items in the namespace
20 export namespace TestNamespace1 {
21     std::string welcomeFromTestNamespace1() {
22         return "welcomeFromTestNamespace1 function called";
23     }
24 }
25
26 // exporting an item in a namespace exports the namespace name, too
27 namespace TestNamespace2 {
28     export std::string welcomeFromTestNamespace2() {
29         return "welcomeFromTestNamespace2 function called";
30     }
31 }
```

图16.2 | 名为 welcome 的模块的主模块接口。

### 模块声明与模块命名

第3行的模块声明将模块命名为 welcome。模块名（按惯例）是用点（.）^38^分隔的小写标识符——例如 deitel.time 或 deitel.math，我们将在后续示例中使用它们。这些点没有特殊含义——事实上，有一项提案建议从模块中移除用点分隔的命名。<sup>39</sup> `deitel.time` 和 `deitel.math` 都以“deitel.”开头，但这些模块并不是名为 `deitel` 的更大模块的“子模块”。从模块声明到翻译单元末尾的所有声明都属于模块范围，组成该模块的所有其他单元中的声明也是如此。<sup>40</sup> 我们将在后续小节中展示多文件模块。

当你在**模块声明**前加上 `export` 时，它引入一个模块接口单元，该单元指定客户端代码可以访问的模块成员。每个模块都有一个主模块接口单元，其中包含引入模块名的**导出模块声明**。你将在第16.9节看到，**主模块接口单元**可以由**模块接口分区单元**组成。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1002_0.png)

### 模块接口文件扩展名

Microsoft Visual C++ 对模块接口单元使用 `.ixx` 文件名扩展名。要将模块接口单元添加到 Visual C++ 项目：

- 1. 右键单击项目的 **源文件** 文件夹，选择 **添加 > 模块…**。
- 2. 在 **添加新项** 对话框中，指定文件名（我们使用了名称 `welcome.ixx`），指定文件的保存位置，然后单击 **添加**。
- 3. 用图16.2中的代码替换默认代码。

不要求使用 `.ixx` 文件名扩展名。如果使用不同扩展名命名模块接口单元的文件，请在项目中右键单击该文件，选择 **属性**，并确保该文件的 **项类型** 设置为 **C/C++ 编译器**。

### g++ 和 clang++ 的模块接口文件扩展名

**g++ 和 clang++ 编译器不要求模块接口单元使用特殊文件名扩展名。** 在本节末尾，我们将展示如何使 g++ 和 clang++ 能够编译 `.ixx` 文件，以便你可以为所有三个编译器使用相同的文件名扩展名。

### 其他文件名扩展名

使用 C++20 模块时，你会遇到一些常见的文件名扩展名，包括：

- `.ixx`——Microsoft Visual C++ 用于**主模块接口单元**的文件名扩展名。
- `.ifc`——Microsoft Visual C++ 用于**主模块接口单元**编译版本的文件名扩展名。<sup>41</sup>
- `.cpp`——翻译单元中 C++ 源代码的文件名扩展名，包括模块单元。
- `.cppm`——推荐用于**模块单元**的 clang++ 文件名扩展名。Visual C++ 也识别此扩展名。
- `.pcm`——在 clang++ 中编译**主模块接口单元**时，生成的文件使用此扩展名。

## 16.6.2 导出声明

必须**导出声明**才能使其在模块外部可用。图16.2第8行将 `export` 应用于函数定义，这会导出该函数的声明（即其原型），作为模块接口的一部分。所有导出的声明都必须出现在**翻译单元**中的**模块声明**之后，并且必须出现在**文件作用域**（称为**全局命名空间作用域**）或**具名命名空间的作用域**（第16.6.5节）中。导出语句中的声明不得具有**内部链接**，⁴² 这包括

- **翻译单元**中**全局命名空间作用域**的静态变量和函数，
- **翻译单元**中的 `const` 或 `constexpr` **全局变量**，以及
- 在“**未命名命名空间**”中声明的标识符。⁴³

此外，如果模块定义了任何预处理器宏，它们仅在该模块中使用，不能导出。⁴⁴

### 在模块中定义模板、`constexpr` 函数和 `inline` 函数

与头文件类似，当你在模块中定义模板、**`constexpr` 函数**或**模块中的 `inline` 函数**时，必须导出其完整定义，以便编译器在导入该模块的任何位置都能访问它。

## 16.6.3 导出一组声明

与其将 `export` 应用于各个声明，不如**导出**花括号中的一组声明（第13–17行）。每个**花括号中的声明都会被导出**。花括号不会定义新作用域，因此在此类块中声明的标识符在块结束花括号之后仍然存在。

## 16.6.4 导出命名空间

程序可能包含许多在不同作用域中定义的标识符。有时一个作用域中的变量会与另一个作用域中同名的变量冲突，可能造成命名冲突并导致错误。C++ 使用**命名空间**解决此问题。每个命名空间定义一个作用域，标识符和变量置于其中。如你所知，C++ 标准库的功能定义在 **std 命名空间**中，这有助于确保这些标识符不会与你自己的程序中的标识符冲突。

### 定义和导出命名空间

第20–24行定义命名空间 `TestNamespace1`。命名空间的主体由花括号（`{ }`）界定。命名空间可以包含常量、数据、类和函数。命名空间的定义必须放在**全局命名空间作用域**，或者必须**嵌套**在其他命名空间中。与类不同，命名空间成员可以定义在分开但同名的命名空间块中。例如，每个 C++ 标准库头文件都有一个类似这样的命名空间块

37. “C++ 标准：10 模块——10.1 模块单元与模块范围。”访问于2023年4月18日。https://timsong-cpp.github.io/cppwp/n4861/module.unit。
38. Corwin Joy。“模块命名指南，”2019年6月16日。访问于2023年4月18日。https://wg21.link/P1634R0。
39. Michael Spencer，“P1873R1：从模块名称中移除点分隔命名，”2019年9月17日。`https://wg21.link/p1873r1`。
40. “C++ 标准：10 模块——10.1 模块单元与模块范围。”
41. DaCamara，“实用 C++20 模块与围绕 C++ 模块的工具的未来。”
42. “C++ 标准：10 模块——10.2 导出声明。”
43. “命名空间——未命名命名空间。”访问于2023年4月18日。https://en.cppreference.com/w/cpp/language/namespace#Unnamed_namespaces。
44. Dos Reis，“使用 C++ 模块编程：面向实际软件开发者的指南。”

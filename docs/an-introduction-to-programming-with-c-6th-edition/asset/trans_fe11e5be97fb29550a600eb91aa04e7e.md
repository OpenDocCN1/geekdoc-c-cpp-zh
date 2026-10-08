

# 第 4 章 完成问题解决过程

![](img/d64a28a68f49d61137bf2f3170ac40ad_114_0.png)

**图 4-19** 源代码翻译为可执行代码的过程

许多 C++ 开发工具将编辑器和编译器包含在一个集成环境中，这被称为 **IDE（集成开发环境）**。例如 Microsoft Visual C++、Borland C++、Builder 和 Dev C++。其他 C++ 开发工具称为命令行编译器，它们仅包含编译器，并要求你使用通用编辑器（如记事本、Word 或 vi）将程序指令输入到计算机中。本书的附录 D 包含了使用 Microsoft C++ 2000 IDE 输入和运行程序的的说明。附录 E 包含了在 Dev C++ 中使用 IDE 的说明。然而，请记住，你可以使用大多数 C++ 开发工具输入并运行此书中的程序，只需很少或不需要任何修改。

图 4-20 显示了 Treyson 程序的源代码。接下来的行进行了编号，以便在文中更容易引用；你不需要在图 4-12 中输入行号。未着色的代码行是你的 C++ 指令，在输入 C++ 指令时，你还需要源文件中输入其他指令。某些额外指令是编译器要求的，而另一些是可选的但强烈建议的。可选指令用阴影标出：

```
1/Fig-20.cpp - 显示小费金额
2//Created/revised by <your name> on <current date>
4#include <iostream>
5 using namespace std;
6
7 int main()
{
9 //declare variables
10 double totalBill = 0.0;
```

你不需要像图 4-20 那样对齐声明语句中的值。但是，这样做有助于验证每个内存位置是否已初始化。

**图 4-20** Treyson 移动程序（续）

# 步骤 6—评估并修改程序

（续）

```
11 double liquor = 0.0;
12 double tipPercent = 0.0;
13 double totalNoLiquor = 0.0;
14 double tip = 0.0;
15
16 //enter input items
17 cout << "Enter the total bill: ";
18 cin >> totalBill;
19 cout << "Enter the liquor charge: ";
20 cin >> liquor;
21 cout << "Enter the tip percentage in decimal format: ";
22 cin >> tipPercent;
23
24 //calculate the total without liquor and the tip
25 totalNoLiquor = totalBill - liquor;
26 tip = totalNoLiquor * tipPercent;
27
28 //display the output item
29 cout << "Tip: $$" << tip << endl;
30 system("pause");
31 return 0;
33 } //end of main function
```

![](img/d64a28a68f49d61137bf2f3170ac40ad_115_0.png)

> 取你的 C++ 开发工具，此语句可能不是必要的

图-20 Treyson 模型程序

程序中的第 1、2、9、16、24 和 28 行；第 33 行也有一个注释。你通过在视为注释的文本前输入正斜杠（//）来创建注释。注释简单用于向阅读程序的人传递信息，被称为文档。第 1 行和第 2 行的注释标识了程序的名称和目的，以及程序员的名字和程序创建或修订的日期。其余的注释解释了代码的不同部分。C++ 编译器指示变量声明后面的注释不需要你在程序中包含。但是，这是一个良好的编程习惯，因为它们让你的代码更易读、更容易理解。C++ 编译器在将源代码转换为目标代码时不会处理注释。注释不以分号结束，它们不是 C++ 语句。

图 4-20 中的第 4 行和第 5 行是指令；第 4 行 #include 指令提供了一种将一个文件的源代码与另一个文件合并的方便方法，无需重新输入代码。例如，#include <iostream> 指令告诉编译器包含当前程序的 istream 内容。任何使用 cin 或 cout 对象的程序必须包含 istream。#include 指令不是 C++ 语句；因此它不以分号结束。另一方面，using指令是一个语句；因此它必须以分号结束。using指令告诉编译器（在计算机的内部内存中）查找单词和类的定义。

第 4 章 完成问题解决过程

![](img/d64a28a68f49d61137bf2f3170ac40ad_116_0.png)

例如 double 或 string。using namespace std; 表示标准 C++ 关键字和类位于 std（标准）命名空间。namespace 是计算机内部内存中的一个特殊区域。

在程序的第 7 行，main 是函数的名称，必须用小写字母输入。函数是执行任务的代码块。函数在它们的名称后有括号，如 main()。某些函数要求在括号之间输入信息；像 main 等函数不需要。每个 C++ 程序必须有一个 main 函数，因为那是 C++ 程序执行的地方。一个 C++ 程序可以包含许多函数，其中一个就是 main 函数。某些函数返回完成分配任务的值。如果它返回一个值，值的类型出现在函数名称左侧；否则 void出现在名称左侧。第 7 行的 int 表示 main() 是函数头，因为它标记了函数的开始。在函数头之后，你输入引导函数执行任务的代码。此类代码的示例包括声明变量的语句以及在大括号 {} 内包含代码。大括号标记了代码的开始和结束。你在函数结束时输入右括号 }。在图 4-20 中，左括号出现在第 8 行，紧位于 int main() 函数头下方。右括号出现在第 33 行。左括号和右括号之间的所有内容都在 main 函数中，被称为函数体。注意你可以在 C++ 指令的同一行包含注释（在此情况下为 //end of main function），因为 // 之后的文本被解释为注释。

![](img/d64a28a68f49d61137bf2f3170ac40ad_116_1.png)

图 4-20 的第 31 行和第 32 行包含 system("pause"); 和 return 0; 语句，这取决于你使用的 C++ 开发工具，用于程序执行和显示。在计算机屏幕上的命令行窗口中按任意键继续显示的消息，如图 4-21 所示。return 0 向操作系统返回数字 0，表示程序运行。（如前面提到的，main 是

> 标题栏包含你的 C++ 工具和文件位置

![](img/d64a28a68f49d61137bf2170ad_116_2.png)

图 4-21 命令行窗口

# 赋值运算符

除了 4-7 中列出的标准算术运算符外，C++ 还提供了几种赋值运算符。赋值运算符允许你简写包含算术运算符的赋值语句。然而，赋值语句必须具有以下格式，即 variableName = variableNameArithmeticOperator value。例如，你可以使用乘赋值运算符 *= 来简写 price *= 1.05；这两个语句都将 price 变量的内容乘以 1.05，然后将结果存储在 price 变量中。图 4-22 显示了常用的赋值运算符，并列出了使用赋值运算符简写赋值语句的示例。注意每个赋值运算符由一个算术运算符紧跟赋值运算符 (=）组成。赋值运算符不包含空格；否则，赋值运算符应该是 += 而不是 +=。在赋值运算符中包含空格是一个常见的语法错误。

> 在大多数情况下，value 可能是常量（字面量）或另一个变量的名字。

# 如何使用赋值运算符

语法
variableNameArithmeticAssignmentOperator value;

| 运算符 | 目的 |
| --- | --- |
| += | 加赋值 |
| -= | 减赋值 |
| *= | 乘赋值 |
| /= | 除赋值 |
| %= | 取模（模）赋值 |

> 简写赋值语句很容易。只需移除语句中赋值运算符 (=) 左侧的变量名，然后在算术运算符后紧跟赋值运算符。

示例 1
原始语句：rate = rate + .05;
简写语句：rate += .05;

示例 2
原始语句：price = price - discount;
简写语句：price -= discount;

图 4-22 如何使用赋值运算符

# 小测验 4-3

> 小测验题的答案位于附录 A。

+   输入 cin > age; 而不是 cin >> age; 是错误的示例。


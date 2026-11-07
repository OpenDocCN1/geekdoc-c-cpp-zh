# C++ 编程：入门指南：面向初学者的清晰简洁 C++ 编程学习指南




2022 年由 Internet Archive 数字化，资金由 Kahle/Austin Foundation 提供

## 关于作者

迈克尔·麦克米伦是阿肯色州北小石城普拉斯基技术学院计算机信息系统专业的讲师。他还是阿肯色大学小石城分校信息科学专业的兼职讲师。迈克尔自 1998 年以来一直教授 C++ 及其他编程语言课程，并已从事编程工作近三十年。迈克尔自 1987 年以来一直撰写有关计算机和技术的文章，并且是另外六本计算机编程书籍的作者或合著者。迈克尔与妻子特丽住在阿肯色州北小石城。

欲了解更多关于迈克尔、他的书籍及其计算机编程教学工作的信息，请访问他的网站：www.techbookspress.com。

## C++ 编程简介

C++ 是当今工业界使用的最流行的编程语言之一。根据 TIOBE 编程社区指数（可通过以下网址访问）：

http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html

在撰写本书时，C++ 是第三大最流行的编程语言，仅次于 Java 和 C++ 的小兄弟 C。C++ 是一种通用、多范式编程语言，这仅仅意味着你可以用 C++ 进行许多不同类型的编程。你可以用 C++ 编写过程式程序、面向对象程序和泛型程序，并且可以想象在一个程序中使用所有三种范式。

C++ 也被认为是相对较难使用的计算机编程语言。该语言具有广泛的功能，许多程序员经常只使用其中的一小部分功能。试图一次性学会整个语言几乎是不可能的。

本书的目标是向你介绍 C++ 中大量功能的一小部分，但包括你立即开始编写有用的 C++ 程序所需的主要构造和功能。你将学习如何编写简单的过程式程序来解决算术问题；你将学习一些操作文本数据（字符串）的技术；你将学习如何在程序中使用决策结构（分支）来有选择地执行代码；你将学习如何在程序中使用重复（循环）来一遍又一遍地重复执行代码；你将学习如何组合函数，使你的程序模块化；你将学习如何构建诸如向量和数组之类的数据结构，以便将相关的数据值存储在内存中；你将学习如何处理文本文件，以便处理现实世界中的数据；最后，你将学习如何编写面向对象程序，以便用自己的数据类型扩展 C++ 语言，并学习如何编写使用对象来更准确地建模你试图解决的问题的程序。

本书与所有其他 C++ 编程书籍相比的主要特点之一是，我们不会试图用事实和功能淹没你。每个新的编程构造和概念都被清晰简洁地呈现，只向你展示开始用 C++ 编程所需了解的那些功能。当你完成本书时，你不会成为 C++ 细节方面的专家，但你将能够用 C++ 编写有用的程序，并为学习那些对你最重要的高级功能打下良好的基础。

最后，学习 C++ 编程的唯一方法就是实际编写 C++ 程序。要做到这一点，你需要一个 C++ 编译器。本书中的示例我们选择使用 Microsoft Visual C++ Express 编译器。该编译器可以从 Microsoft 免费下载，包含你学习本书所需的一切，就此而言，也包含更高级的 C++ 编程所需的一切。

如果你选择使用其他 C++ 编译器，你可能需要更改的唯一代码是程序开头的 #include 语句。如果你在进行这些更改时遇到问题，请联系作者寻求帮助。

如果你运行所有程序、对它们进行更改、再次运行它们，并且不怕尝试，你将最大程度地利用本书。完成一章后，在你有时间完成尽可能多的练习之前，不要继续下一章。你只能通过编程来学习编程。

## 第 1 章

## Visual C++ 入门

C++ 是一种编译型编程语言。这意味着什么？这意味着你用 C++ 编写的程序会被编译器翻译成机器语言，然后执行。你不必理解编译过程就可以开始学习 C++ 编程。但是，你确实需要理解程序从构思到执行所必须经历的步骤。这就是我们将在本章中讨论的内容。

### 下载并安装 Visual C++ Express

Microsoft 提供用于非商业用途的免费 C++ 版本，即 Visual C++ Express（Visual C++）。当前版本名为 Visual C++ 2010 Express，但由于该程序更新非常频繁，我们将省略年份。你可以在以下网址找到它：

http://www.microsoft.com/express/Downloads/#2010-Visual-CPP

安装 Visual C++ 是一个自动过程。你下载或安装时应该不会遇到任何问题，特别是如果你在安装过程中选择默认设置。如果你在下载或安装时遇到任何问题，可以观看有关下载和安装 Visual C++ Express 的视频。你可以在以下网址找到它：

http://www.techbookspress.com/cpp

Visual C++ 程序以项目形式组织。从打开窗口中选择“新建项目”以开始新程序。因此，单击“新建项目”。

该窗口列出了你可以创建的不同类型的项目。本书中我们只使用 CLR 控制台应用程序，因此请确保该选择被突出显示。然后向下移动到窗口底部“名称”文本框所在的位置。

Visual C++ Express 将使用你为项目指定的名称来存储项目的文件。例如，如果我们将项目命名为 Example，那么一个具有该名称的文件夹将放置在“名称”文本框下方文本框中显示的“位置”路径中。你可以为项目使用任何名称，但一定要使用有意义的名称，以便你以后可以回到某个项目继续处理它。我们现在要编写一个简单的“Hello, world!”程序，因此输入“HelloWorld”作为项目名称。你输入的名称也会添加到“位置”下方的“解决方案名称”文本框中。我们将在后续文章中进一步讨论这个框。按“确定”，你的项目就会打开。

这是你将用来编写 C++ 程序的主窗口。左侧面板列出构成项目的所有文件。我们将在后续文章中进一步讨论这个窗格。右侧面板是代码编辑器，你将在其中输入 C++ 代码。你会注意到已经编写了一些代码。现在，删除以“Console::WriteLine(…”开头的那一行。然后，在读到“using namespace System;”的那一行下方添加一个空行，并在空行下方写入以下两行：

```cpp
#include <iostream>
using namespace std;
```

然后，在读到“return 0;”的那一行上方，添加以下代码行：

```cpp
cout << "Hello, World!" << endl;
```

最后一个词是“end ell”，不是“end 1”，但许多初学 C++ 的程序员会把“ell”误认为“1”，这会导致下一个要打印的内容从新的一行开始。换句话说，它强制编译器执行换行命令。

现在，代码编辑器窗口中的代码应该如下所示：

```cpp
#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl;
    Console::ReadKey();
    return 0;
}
```

当你的代码看起来像这样时，按工具栏中的绿色箭头运行程序，尽管工具提示显示“开始调试”。这实际上是同一回事。系统会询问你是否要重新生成项目。对此问题回答“是”。然后你应该会看到一个控制台窗口，其中显示短语“Hello, World!”。按任意键关闭窗口。

如果这一切都正确运行，恭喜你编写了第一个 C++ 程序。如果没有正确运行，请回顾上面列出的步骤，看看你哪里做错了。

### “Hello, World!”程序如何工作

让我们逐行检查 Hello, World! 程序，以基本了解发生了什么。第一行是：

```cpp
#include "stdafx.h"
```

这一行称为预处理器指令，用于让编译器知道将指定文件的内容视为包含在程序的其他源代码中。文件 stdafx.h 称为头文件，用于存储任何 C++ 程序都可以使用的可重用源代码。头文件的使用允许我们仅在需要时通过头文件调用额外功能，从而使主语言尽可能简短简洁。我们将讨论头文件

更具体地说，如下所示。

下一行是：

```
using namespace System;
```

命名空间允许你将类似头文件这样的文件归组到一个共同名称下。具有相似用途的文件会存储在同一个命名空间中。第一行指定的头文件 stdafx.h 存储在 System 命名空间中，因此我们必须告诉编译器在 System 命名空间中查找该文件。

接下来的两行是：

```
#include <iostream>
using namespace std;
```

这是另一个预处理指令示例。上面第一条指令的作用是让我们能够访问 Console 类，从而在向其中显示数据时让命令提示符窗口保持打开。iostream 库允许我们使用标准输出流 `cout` 将数据写入控制台窗口。如你所见，iostream 存在于另一个命名空间，即 std 命名空间中，这就是为什么我们必须为该文件单独发出一条指令。

下面这一行：

```
int main(array<System::String ^> ^args)
```

告诉系统我们现在正在定义一个名为 `main` 的函数。每个 C++ 程序都必须有一个名为 `main` 的函数，因为编译器会查找这个函数作为程序的起点。函数名前面的单词 `int` 表示 `main` 函数返回一个整数值。现在，请忽略括号内的所有内容。这称为函数的参数列表，我们暂时不会使用它。

下一行只包含单个字符 `{`，称为花括号。这个字符表示一个代码块的开始。`}` 表示一个代码块的结束。稍后我们会更详细地讨论代码块，但现在只需知道函数必须定义在一个代码块内就足够了。

代码块打开后，下一行是我们程序的第一行：

```
cout << "Hello, World!" << endl;
```

在这一行中，我们表示希望将短语“Hello, World!”显示到标准输出设备，该设备默认是控制台，并被定义为 `cout` 对象。`<<` 运算符称为“放入”运算符，它指定其后的数据将被“放入”标准输出设备。简单来说，这一行会使短语“Hello, World!”显示在命令提示符窗口中。我们已经讨论过 `endl` 的作用。每一段以分号结尾的 C++ 代码称为一个 *语句*。可以把 C++ 中的语句想象成英语中的句子。编译器通过分析你编写的语句来检查 C++ 程序中的语法是否正确。

下一行：

```
Console::ReadKey();
```

使用另一个表示标准输出的对象 `Console`，并调用一个方法或函数 `ReadKey()`，让命令提示符窗口保持打开，直到用户按下任意键。如果我们不使用这一行，命令提示符窗口会在“Hello, World!”写入后立即消失。

接下来我们看到：

```
return 0;
```

这一行在 `main` 函数末尾是必需的，用于表示程序已成功完成。这一行称为 *返回语句*。我们编写的每个程序都会在 `main` 函数末尾包含这一行，尽管 Windows 实际上并不会对这个值做什么。

最后，我们通过写一个右花括号来结束代码块和程序：

```
}
```

如果你没有理解本文讨论的所有内容，不用担心。随着我们深入学习 C++ 编程，我们会反复讲解所有这些内容。下一章将讨论 C++ 语言的两个基本构件——数据类型和变量。

### 练习

1. 确保你能让“Hello, World!”程序在你的计算机上运行。
2. 修改“Hello, World!”程序，让它向你问好。

## 第 2 章：数据类型和变量

你可以把计算机程序想象成很像一份食谱。食谱里有什么？一份食谱包含一份原料清单和一组说明，用于将原料转化为可食用的东西。计算机程序由数据加上指令组成，这些指令告诉计算机如何将数据转换为程序所需的信息。因此，要理解如何编写程序，我们首先需要理解如何处理数据。

在 C++ 中处理数据涉及两件事——确定数据的数据类型，并为数据提供存储空间。本章将讨论 C++ 中一些较常见的数据类型，然后解释如何创建变量，以便在程序运行时将数据存储在内存中。

### C++ 数据类型

在讨论 C++ 中使用的各种数据类型之前，我们需要谈谈为什么拥有数据类型很重要。首先，数据类型定义并限制了可对数据执行的操作范围。例如，将整数相加是合理的，但将布尔值加到整数上就不合理。同样，数据类型还确保针对该类型执行正确类型的操作，因此如果我们想将两个浮点数相加，就会执行浮点加法运算。否则，我们就必须为每种操作单独设置加法运算，而不能对所有数值类型使用共同的运算符 (+)。

现在让我们看看 C++ 的一些常见数据类型。它们是：

1. `int` – 用于大约在 -2,000,000,000 到 2,000,000,000 范围内的整数值
2. `double` – 用于大约在 -3.4e-308 到 3.4e308（或 17 位数字）范围内的双精度浮点数
3. `char` – 用于单个字符值（即字母和符号）。以 -128 到 127 范围内的整数值存储。
4. `bool`（布尔） – 用于真或假的值。范围是真或假。
5. `string` – 用于长度超过一个字符的字符数据。

这些数据类型中的前四种内置于 C++ 中，被视为基本数据类型。`string` 数据类型并非内置于该语言中，但它的使用方式使其可以被当作基本类型来对待。

数据类型的内容远不止这些，随着我们更深入地研究 C++ 编程，我们会继续补充这一讨论。

### 在 C++ 中声明变量

变量是内存中一个具名位置，在程序运行时用于存储数据。在 C++ 中，变量通过声明语句创建。声明至少包含变量的数据类型和变量名。声明还可以使用所谓的初始化器为变量赋初始值。让我们从本文开始讨论创建变量名的规则。

在 C++ 中创建变量的规则很简单——变量名必须以字母字符开头；变量名可以包含其他字母字符、数字和下划线字符；变量名不能是 C++ 保留字。

以下是一些合法 C++ 变量的示例：

- `number`
- `last_name`
- `firstName`
- `hourlyWage`
- `PI`

由多个单词组成的变量名既可以使用下划线分隔单词，也可以将两个单词合并为一个，并将第二个单词的首字母大写。这种变量命名风格称为“驼峰式命名法”，是一种非常流行的变量命名风格，尤其是因为将字母大写比输入下划线字符更容易。不过，驼峰式命名法只是一种风格约定，并不要求你必须使用它。不过，你应该选择一种特定的风格，并在使用中保持一致。

以下是一些非法变量名的示例：

- `first name`
- `1num`
- `while`

第一个非法变量包含空格；第二个示例以数字开头；第三个示例是 C++ 保留字。

变量名应始终有意义，以便名称能够表明其中存储的数据的性质。有意义的变量名是 `hoursWorked`；无意义的变量名是 `hw`。

要声明变量，首先写出变量的数据类型，然后写出变量名。以下是一些示例：

```
int hoursWorked;
bool endOfData;
string lastName;
```

这些行中的每一行都是一条单独的语句，行末的分号表明了这一点。C++ 中的所有语句都以分号结尾。这些特定语句称为声明语句。随着我们学习 C++，还会有更多关于语句的讨论。

第二种声明涉及为变量赋予初始

在声明时赋值。这种声明称为*初始化器*，写法如下：

```cpp
int hoursWorked = 51;
```

这条语句既将 hoursWorked 声明为整型变量，又将该变量赋值为 51。

最后，你可以在单条声明中声明多个相同数据类型的变量。下面的示例声明了多个整型变量：

```cpp
int hours, days, weeks;
```

这等同于写成：

```cpp
int hours;
int days;
int weeks;
```

C++ 会忽略空白字符，因此你也可以像下面这样写上面的几行：

```cpp
int hours; int days; int weeks;
```

### C++ 中的常量

一种特殊类型的变量是*常量*。常量是一种在程序运行期间其值不能改变的变量。常量有助于使程序更易读、更易调试，并应在合适的时候使用。

常量的声明方式如下：

```cpp
const double pi = 3.14159;
```

这个声明看起来与普通变量的声明非常相似。唯一的区别是在数据类型前使用了关键字 const。

每当你有一个会在程序中的多个位置使用的值时，应考虑将该值编码为常量，而不是反复键入字面值。这样一来，如果你必须在程序中的多个位置使用该值，而该值又发生了变化，你只需在声明常量的那一处进行修改，而不必在所有使用该值的地方逐一修改。稍后的示例程序中我们会看到许多常量的例子。

### 练习

- 1. 为以下数据创建变量声明语句：
    - a. 你的姓名
    - b. 你的月收入
    - c. 你的 gpa
- 2. 以下变量名有什么问题？
    - a. `.name`
    - b. `last&name`
    - c. `09Sept`
    - d. `first name`
    - e. `$str`

## 第 3 章：算术运算符与表达式

C++ 程序是执行某些任务的语句集合。当我们在 C++ 中编写执行算术运算的语句时，必须创建表达式，并借助算术运算符来执行算术运算，这些运算符告诉编译器要对数据执行何种算术运算。本章讨论 C++ 中各种算术运算符，以及如何使用它们构成算术表达式。

### 算术运算符

许多人在学习一门新的编程语言时，最先想做的事情之一就是使用该语言执行算术运算。为此，我们需要知道算术表达式是如何构成的。最好的起点是算术运算符。它们如下：

- `+` 加法（加号）
- `-` 减法（减号）
- `*` 乘法
- `/` 除法
- `%` 取余

加号和减号运算符用于区分正数和负数，尽管通常并不用加号来表示正数。

这些运算符随后用于构成算术表达式。以下是一些示例：

```
23 + 2
100 - 17
43.2 * 3.14159
2300 / 12
12 % 2
```

你也可以使用这些运算符构成更复杂的算术表达式：

```
12 + 2 * 3 + 4 / 2
```

当编写这样的表达式时，C++ 会根据运算符的优先级来求值。顺序从高到低为：

- `%`
- `*`、`/`
- `+`、`-`

在上面的表达式中，乘法和除法先于加法和减法执行。你可以使用圆括号来修改运算顺序，强制 C++ 先执行圆括号内的所有运算，再执行其他运算。例如，我们可以将上面的表达式改写为：

```
(12 + 2) * (3 + 4) / 2
```

以改变该表达式的值。

现在让我们看一个在完整 C++ 程序中使用算术表达式的示例。在这个示例中，我们将把 5 个测试成绩赋给 5 个变量，并计算平均成绩。程序如下：

```cpp
// Chapter3.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int grade1, grade2, grade3, grade4, grade5,
        sumOfGrades, numOfGrades;
    double average = 0.0;
    grade1 = 84;
    grade2 = 89;
    grade3 = 77;
    grade4 = 94;
    grade5 = 88;
    numOfGrades = 5;
    sumOfGrades = grade1 + grade2 + grade3 + grade4
                + grade5;
    average = sumOfGrades / numOfGrades;
    cout << "The average is: " << average << endl;
    Console::ReadKey();
    return 0;
}
```

让我们逐行检查这个程序。第一行：

```cpp
int grade1, grade2, grade3, grade4, grade5,
    sumOfGrades, numOfGrades;
```

初始化本程序所需的整型变量：5 个用于成绩的变量、一个用于存储成绩总和的变量，以及一个用于存储成绩数量的变量，计算平均分时需要用到它。

下一行：

```cpp
double average = 0.0;
```

声明并初始化我们用来存储平均分的变量。平均分很可能是浮点值，因此我们需要使用浮点数据类型。

以下几行给成绩变量和存储成绩数量的变量赋值：

```cpp
grade1 = 84;
grade2 = 89;
grade3 = 77;
grade4 = 94;
grade5 = 88;
numOfGrades = 5;
```

下面这一行：

```cpp
sumOfGrades = grade1 + grade2 + grade3 + grade4
             + grade5;
```

将所有成绩变量相加，并把总和存入 sumOfGrades 变量。

接下来，我们通过用成绩总和除以成绩数量来计算平均分：

```cpp
average = sumOfGrades / numOfGrades;
```

最后，我们通过显示所得平均分来结束程序：

```cpp
cout << "The average is: " << average << endl;
```

不过，严格来说，程序真正的结束是这一行：

```cpp
return 0;
```

### 更多关于 C++ 运算符和变量的内容

在 C++ 编程中，给变量赋值这一操作非常频繁，因此有一组运算符专门用于执行该操作。我们将要考察的第一组运算符用于将变量的值递增或递减 1。

### 递增与递减

在所有编程中，最常见的语句之一大致如下：

```cpp
count = count + 1;
```

有无数种情形需要将变量的值增加 1。为便于执行此操作，C++ 提供了一个专门将变量增加 1 的运算符，即 ++ 运算符。

++ 运算符的用法如下：

```cpp
int count = 0;
++count; // the value of count goes from 0 to 1
```

你也可以将运算符放在变量之后，如下所示：

```cpp
count++;
```

一个合乎逻辑的问题是：把 ++ 运算符放在变量之前或之后有什么区别？当变量在语句中单独存在时，没有区别。然而，如果变量用于更复杂的语句中，就可能产生很大差别。下面是一个演示这种差别的示例：

```cpp
int var1, var2;
var1 = 1;
// var1 gets the value 2 and var2 gets the value 2
var2 = ++var1;
```

```cpp
var1 = 1;
var2 = 0;
// var1 gets the value 2 and var2 gets the value 1
var2 = var1++;
```

看到发生了什么吗？当我们将 ++ 运算符放在变量之后，并在赋值语句中使用它时，会先执行赋值操作，然后执行递增操作。这是 ++ 运算符的一个微妙影响，但如果你不理解该运算符的工作方式，它可能会耗费大量额外的调试时间。

递减变量的值使用 -- 运算符。该运算符的用法与 ++ 运算符相同：

```cpp
int var1, var2;
var1 = 2;
--var1; // var1 now has the value 1
var1--; // var1 now has the value 0
var1 = 2;
// var1 and var2 get the value 1
var2 = --var1;
// var2 gets the value 1 and var1 gets the value 0
var2 = var1--;
```

递增和递减运算符在将变量值调整 1 时提供了便捷的快捷方式，但在更复杂的赋值语句中使用它们时要小心。




### 复合赋值运算符

也会有很多情况需要将变量的值调整超过 1，例如以 5 为单位计数：

```cpp
count = count + 5;
```

为了更轻松地编写这类语句，C++ 提供了一组复合赋值运算符。这些运算符是：+=、-=、*=、/= 和 %=。它们的工作方式如下：

```cpp
int var1 = 0;
var1 += 5;  // var1 has the value 5
var1 *= 2;  // var1 now has the value 10;
var1 /= 2;  // var1 has the value 5
var1 %= 5;
// var1 now has the value 0 since 5 / 5 leaves
// remainder of 0
```

使用这些运算符代替更完整的语句，为程序员提供了便捷的快捷方式，应尽可能使用它们，以使程序更易读。

### 练习

- 1. 编写一个 C++ 程序来计算以下表达式。为表达式中的每个数字使用变量，并将结果输出到控制台。
  - a. `3.14159 * 3 * 3`
  - b. `234 * 12 + 32 - 12 / 2`
  - c. `13 % 2`
  - d. `5 * 5 * 5 * 5 * 5`
  - e. `-1 + 3 * -2`
- 2. 编写一个 C++ 程序，使用最合适的复合运算符或自增/自减运算符对变量 number 执行以下操作：
  - a. 声明该变量并将其初始化为值 1。
  - b. 将 number 增加 3。
  - c. 将 number 增加 1。
  - d. 声明变量 num 并赋值为 0。
  - e. 将 number 增加 1，并在同一条语句中将其新值赋给 num。
  - f. 将 number 减 1，并将其旧值赋给 num。
  - g. 将 number 减 2。

## 第 4 章：解决算术问题

让我们运用前几节学到的知识，用 C++ 解决一些算术问题。这将让我们有机会了解如何从问题描述出发，编写出解决问题的完整程序。

### 确定平均成绩

对于第一个问题，我们将求一组测试成绩的平均值。测试成绩为：78、85、92、99 和 81。解决这个问题需要求出测试成绩的总和，并将总和除以测试成绩的数量以得到平均值。要编写程序解决这个问题，我们需要用于测试成绩的变量（这里并非绝对需要为测试成绩创建变量，但我们会创建它们以练习使用变量）、用于测试成绩总和的变量，以及用于保存平均值的变量。

首先，我们需要确定变量的数据类型。测试成绩都是整数，因此测试成绩变量将声明为整数。测试成绩的总数也是整数，因此也是整数，但我们希望将其声明为常量，以演示常量的用法。测试成绩的总和也将声明为整数变量。不过，平均值可以是浮点值，因此我们需要将该变量声明为 double。

以下是声明变量的语句：

```cpp
int grade1, grade2, grade3, grade4, grade5, totalGrades;
double average;
const int numGrades = 5;
```

下一步是为测试成绩变量赋值：

```cpp
grade1 = 78;
grade2 = 85;
grade3 = 92;
grade4 = 99;
grade5 = 81;
```

然后我们可以计算测试成绩的总和：

```cpp
totalGrades = grade1 + grade2 + grade3 + grade4 + grade5;
```

最后，我们可以计算并显示平均值：

```cpp
average = totalGrades / numGrades;
cout << "The average is: " << average << endl;
```

以下是在 Visual C++ Express 中输入的完整程序：

```cpp
// avgGrades.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int grade1, grade2, grade3, grade4, grade5,
        totalGrades;
    double average;
    const int numGrades = 5;
    grade1 = 78;
    grade2 = 85;
    grade3 = 92;
    grade4 = 99;
    grade5 = 81;
    totalGrades = grade1 + grade2 + grade3 + grade4
                        + grade5;
    average = totalGrades / numGrades;
    cout << "The average is: " << average << endl;
    Console::ReadKey();
    return 0;
}
```

以下是程序的输出：

```text
The average is: 87
```

### 数硬币

这是另一个问题，将让你获得设置变量和使用算术表达式的经验。你听到口袋里有很多零钱在哗啦作响，于是把它们拿出来，决定写一个程序来数一数。你发现有 3 枚 25 美分硬币、6 枚 10 美分硬币、5 枚 5 美分硬币和 7 枚 1 美分硬币。你有多少钱？

第一步是确定解决问题所需的变量。我们需要为每种面额创建存储其值的常量，以及一个存储总金额的变量。现在声明它们：

```cpp
double total;
const double penny = .01;
const double nickel = .05;
const double dime = .10;
const double quarter = .25;
```

现在我们需要编写一个表达式，把硬币加起来：

```cpp
total = (3 * quarter) + (6 * dime) + (5 * nickel)
      + (7 * penny);
```

最后，我们需要显示结果：

```cpp
cout << "The total amount of change is: $" << total
     << endl;
```

以下是 Visual C++ 中的完整程序：

```cpp
// countCoins.cpp : main project file.
#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    double total;
    const double penny = .01;
    const double nickel = .05;
    const double dime = .10;
    const double quarter = .25;
    total = (3 * quarter) + (6 * dime) + (5 * nickel)
          + (7 * penny);

    cout << "The total amount of change is: $" << total
         << endl;
    Console::ReadKey();
    return 0;
}
```

以下是输出：

```text
The total amount of change is: $1.67
```

### 投票百分比

这是摘自一本初中数学书的问题：在一次选举中，一名候选人获得了全部有效选票的 60%。15% 的总选票被宣布为无效。如果总票数为 500,000，求投给该候选人的有效选票数。

和往常一样，我们首先需要决定变量是什么。我们确定已知的事实可以作为常量输入，因此有三个常量：

```cpp
const int totalVotes = 500000;
const double candVotePercent = .60;
const double invalidPercent = .15;
```

现在我们需要用于有效选票总数和该候选人获得的有效选票数的变量：

```cpp
double validVotes, candVotes;
```

将这两个变量声明为 double 可能看起来有些奇怪，但由于我们将在用于计算这些变量值的表达式中处理浮点值，将它们声明为 double 可以消除任何关于数据丢失的疑问。（事实上，如果你确实将它们声明为 int，编译器会发出警告，指出在将浮点值赋给整数变量时可能会丢失数据）。

接下来我们需要求出有效选票总数：

```cpp
validVotes = totalVotes - (totalVotes *
             invalidPercent);
```

由于无效选票数等于总选票数的 15%，那么如果我们从总票数中减去这 15%，就会得到有效选票总数。然后我们可以轻松计算该候选人获得的选票数并显示结果：

```cpp
candVotes = validVotes * candVotePercent;
cout << "The candidate received " << candVotes
     << " votes.";
```

以下是完整的 C++ 程序：

```cpp
// votePercent.cpp : main project file.
#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int totalVotes = 500000;
    const double candVotePercent = .60;
    const double invalidPercent = .15;
    double validVotes, candVotes;
    validVotes = totalVotes - (totalVotes *
                 invalidPercent);
    candVotes = validVotes * candVotePercent;
```




```cpp
cout << "The candidate received " << candVotes
     << " votes.";
Console::ReadKey();
}
return 0;
```

以下是输出：

该候选人获得了 255000 票。

### 练习

编写一个完整的 C++ 程序来解决以下文字题。使用直接赋值来输入数据，并将答案显示到控制台。

- 1. 将华氏温度转换为摄氏温度的公式为 c = (5.0/9.0) × (F − 32)，其中 F 是华氏温度。32 华氏度对应的摄氏温度是多少？
- 2. 一辆汽车在 4 小时内行驶了 210 英里，其平均速度是多少？
- 3. 某人投资了 12,000 美元，一部分投入收益为 7% 的共同基金，另一部分投入收益为 4% 的货币市场基金。如果获得的单利总计为 750 美元，那么投入共同基金的钱有多少？
- 4. 两人相距 10 英里，开始相向而行。一人以 5 英里/小时的速度步行，另一人骑自行车以 15 英里/小时的速度行驶。两人相遇需要多长时间？
- 5. 演唱会的门票在售票处售价为 22 美元，但通过 TicketKing 购买的每张门票需收取 2 美元的服务费。包括服务费在内的总收入为 54,400 美元。如果在售票处售出的门票数量是通过 TicketKing 售出的两倍，那么售票处收入了多少美元？

## 第 5 章：程序数据的输入与输出

上一章讨论的三个示例表明，大多数计算机程序都遵循非常标准的开发阶段。首先，程序必须将数据读入变量，我们将此阶段称为输入阶段。该阶段包括声明变量和常量、将数据赋值给变量，以及获取用户输入，我们将在接下来讨论这一点。

第二个阶段是处理阶段。在上述示例中，处理阶段涉及编写一个或多个算术表达式，并将这些表达式的值赋值给变量。在更复杂的程序中，这一阶段可能比我们之前看到的较简单的示例要复杂得多。

最后一个阶段是输出阶段。在此阶段，我们通过将数据写入控制台来向用户显示处理阶段的结果，不过在更复杂的程序中，我们可能会将数据写入文件或数据库，或者将数据发送到打印机。在本书中，我们将主要向控制台显示输出，但至少会涉及如何将数据存储到文件中。

正如我刚才提到的，程序的处理阶段通常比我们目前看过的示例要复杂一些。我们几乎已经准备好讨论如何编写更复杂的程序来解决更复杂的问题，但在那之前，我们需要更多地讨论如何将数据读入程序以及向控制台显示输出。

### 使用 cin 获取输入

将数据读入程序的最常见方式是通过键盘输入。C++ 将键盘视为标准输入设备，并为键盘定义了一个对象——cin。用于从 cin 获取数据的运算符是 >>（“get from”）运算符。从键盘获取输入的一般形式为：

```cpp
cin >> identifier;
```

其中 identifier 通常是一个变量。下面是一个简单示例，展示如何使用 cin 从键盘获取数据：

```cpp
int number;
cout << "Enter a number: ";
cin >> number;
```

在此示例中，提示信息显示后，用户从键盘输入一个整数值，该值被存储在变量 number 中。标识符的数据类型决定了 >> 运算符存储的内容。如果输入的值是整数，则该值将按输入时的形式存储在变量中。但是，如果输入的值是浮点值，则只存储其整数部分。因此，如果在上述示例中输入值 3.14159，则数字 3 会被存储在 number 中。

你可以在一条 cin 语句中通过 >> 运算符分隔变量，从而输入多个值。以下代码片段演示了其工作原理：

```cpp
int number1, number2, sum;
cout << "Enter two numbers: ";
cin >> number1 >> number2;
sum = number1 + number2;
cout << sum << endl;
```

程序的运行结果如下：

```text
Enter two numbers: 2 3
5
```

输入的第一个数字存储在 number1 中，输入的第二个数字存储在 number2 中。显然，两个输入值之间必须有一个空格。

字符串值也可以用同样的方式输入。下面是一个示例：

如果用户输入“Mary”，程序输出：

```text
Hello, Mary
```

但如果用户输入“Mary Smith”，程序输出：

```text
Hello, Mary
```

这是怎么回事？请记住，两个输入值之间的空格会将输入分隔为不同的值。由于没有变量来存放“Smith”，程序就将其忽略了。要读取一整行到变量中，你需要使用 getline() 函数。下面是一个该函数用法的示例：

```cpp
string name;
cout << "Enter your name: ";
getline(cin, name);
cout << "Hello, " << name;
```

现在，当用户输入“Mary Smith”时，程序输出：

你好，Mary Smith

你可以输入任意长度的字符串，变量会自动扩展以容纳该字符串。

### 关于使用 cout 输出的更多内容

我们已经看到了几个如何使用 cout 在控制台上显示数据的示例。我们见过的大多数示例形式都是：cout << expression，但我们还可以用更多方式使用 cout 来显示数据。我们可以像这样组合数据类型：

```cpp
cout << "Pi has the value ";
cout << 3.14159;
```

这两条语句输出在同一行——Pi 的值为 3.14159——因为我们没有指定换行。不过，这里没有理由使用两次 cout，因为我们可以通过将 << 运算符串联起来，把两条语句合并成一条（这里我们还使用了一个变量来存储值 3.14159）：

请注意，即使 \n 是一个字符，也要用双引号将其括起来。我们也可以使用单引号来编写该语句：

```cpp
cout << "Hello, World!" << '\n';
```

### 练习

- 1. 编写一个程序，要求用户输入其全名，然后显示“你好，name！你今天怎么样？”，其中 name 是用户输入的名字。
- 2. 编写一个程序，要求用户输入两个数字，然后以如下形式显示两个数字的和、差、积和商（用户输入 4 和 2）：
    - 4 加 2 等于 6
    - 4 减 2 等于 2
    - 4 乘以 2 等于 8
    - 4 除以 2 等于 2

## 第 6 章：决策

到目前为止，我们讨论的 C++ 程序都是按顺序方式运行的，从程序的第一行开始，逐行执行到程序的最后一行。对于非常简单的问题，顺序解决方案可能就足够了，但对于更复杂的问题，我们需要能够在程序中做出决策，决定程序中的哪些行应该执行，哪些行应该跳过。

例如，公司的工资程序必须决定：如果员工只工作了常规工时，就按正常工资支付；如果员工工作了超过常规工时，就按加班工资支付。另一个例子是提示用户输入用户名和密码的程序。该程序必须判断输入的用户名和密码是否与可接受的用户名和密码列表匹配，从而决定允许用户进入系统还是将其拒之门外。诸如此类的决策都是使用某种形式的 if 语句做出的。但是，在研究如何使用 if 语句之前，我们必须先讨论如何在 C++ 中使用*关系*和*逻辑*表达式来比较值。

### 关系表达式

C++ 程序通过比较两个或多个数据值来做出决策。例如，为了确定员工是否应获得加班工资，程序会将员工工作的小时数与享受加班工资所需的最低小时数（通常为 40 小时）进行比较。这种比较是通过使用一个或多个关系运算符的关系表达式来完成的。




关系运算符有：

- `==` 等于
- `!=` 不等于
- `>` 大于
- `<` 小于
- `>=` 大于或等于
- `<=` 小于或等于

这些运算符是*二元*运算符，因此它们需要在运算符两侧都有操作数。这些操作数可以是任何表达式，包括字面值。关系运算符与两个操作数的组合称为*关系表达式*。

关系表达式总是求值为一个布尔值，要么是 true，要么是 false。以下是一些关系表达式的示例：

```cpp
(2 == 2) // true
(50 >= 50) // true
(34 <= 272) // true
(9 != 9) // false
("Ronald" == "ronald")
// false because "R" is not equal to "r"
("baboon" > "ape")
// true because "b" is greater than "a"
```

当然，变量和字面值一样可以用于关系表达式。注意，在 C++ 中关系表达式必须写在括号内。有些其他语言（例如 Visual Basic）没有这个要求。

### 逻辑运算符

更复杂的比较有时需要程序员组合两个或多个关系表达式。这类比较被称为逻辑表达式，并通过逻辑运算符执行。逻辑运算符有：

- `&&` 与
- `||` 或
- `!` 非

下面是一个示例，说明如何将 `&&` 逻辑运算符与两个关系表达式一起使用（假设我们已经声明了变量 `workerType` 和 `hoursWorked`）：

```cpp
((workerType == "hourly") && (hoursWorked > 40))
```

请注意，两个表达式必须分别用括号括起来，并且整个组合也要用括号括起来。

如果所有关系表达式都为真，`&&` 逻辑表达式返回 true；如果其中任何一个或两个关系表达式为假，则返回 false。我们可以用真值表总结这种行为：

| 关系表达式 1 | 关系表达式 2 | 结果 |
|---|---|---|
| 真 | 真 | 真 |
| 真 | 假 | 假 |
| 假 | 真 | 假 |
| 假 | 假 | 假 |

下面是一个 `||` 逻辑表达式的示例：

```cpp
((hoursWorked < 41) || (workerType == "salary"))
```

在 `||` 逻辑表达式中，如果任一关系表达式为真，则表达式为真；仅当两个关系表达式都为假时，表达式才为假。以下是 `||` 表达式的真值表：

| 关系表达式 1 | 关系表达式 2 | 结果 |
|---|---|---|
| 真 | 真 | 真 |
| 真 | 假 | 真 |
| 假 | 真 | 真 |
| 假 | 假 | 假 |

最后一个逻辑运算符是 `!`（非）运算符。该运算符是单目运算符，对布尔表达式的值取反。例如：

```cpp
! (2 == 2) // false
! (3 < 2) // true
```

在本书中，我们不会经常使用 `!` 运算符。事实上，我们只会在处理文本文件时使用它，你将在本书后面看到。

### 使用 if 语句做出决策

在解决涉及决策的编程问题时，仅使用关系表达式和逻辑表达式是不够的；必须有某种方式根据关系和/或逻辑表达式的结果来控制哪些语句被执行。C++ 中用于做出决策的一个工具是 *if* 语句。

#### if-else 语句

*if* 语句最简单的形式是 *if-else* 语句。该语句用于根据条件（可以是关系表达式或逻辑表达式）的值执行一组语句或另一组语句。

*if-else* 语句的一般形式如下：

```cpp
if (condition)
    statement1
else
    statement2
```

*if-else* 语句的工作方式如下：如果条件为真，则执行 statement₁，否则执行 statement₂。让我们看一个 C++ 示例：

```cpp
int hoursWorked;
cout << "Enter the number of hours worked: ";
cin >> hoursWorked;
```

```cpp
double rate = 25.00;
double pay;
if (hoursWorked > 40)
    pay = (40 * rate) + ((hoursWorked - 40) * (rate
        * 1.5));
else
    pay = (hoursWorked * rate);
```

存储在 `pay` 中的值取决于用户为 `hoursWorked` 变量输入的内容。如果用户输入的数值大于 40，则 `pay` 的值由条件正下方的语句设置。如果用户输入的工作小时数为 40 或更少，则 `pay` 的值由 `else` 下方的语句设置。

你会注意到，在上面的示例中，如果条件为真，只执行一条语句；如果条件为假，也只执行一条语句。如果你使用花括号将多条语句放在一个块中，那么 if-else 语句的每种可能结果并不限于只执行一条语句。此版本 if-else 语句的一般形式如下：

```cpp
if (condition)
{
    statement₁;
    statement₂;
    statementₙ;
}
else
{
    statement₁;
    statement₂;
    statementₙ;
}
```

使用这种 if-else 形式时，当条件为真时执行第一个语句块，当条件为假时执行第二个语句块。让我们看一个示例：

```cpp
int grade, bonus;
bool passFail;
cout << "Enter your grade: ";
cin >> grade;
if (grade >= 70)
{
    passFail = true;
    bonus += 5;
}
else
    passFail = false;
```

在上面的示例中，及格分数（70 分或以上）会将布尔变量设置为 true，并给予 5 分奖励。不及格分数只会将布尔变量设置为 false。

为了节省一点空间，你经常会看到 if-else 语句中的语句块将左花括号与条件写在同一行，例如：

```cpp
if (grade >= 70) {
    passFail = true;
    bonus += 5;
}
```

这样开始一个语句块是一种风格约定，你可以根据需要遵循，但无论选择哪种风格，你都应该保持一致，并始终使用相同的风格。

if 语句可以放在另一个 if 语句内部。这称为嵌套 if 语句。下面是一个示例：

```cpp
int num1, num2, num3;
cout << "Enter three numbers: ";
cin >> num1 >> num2 >> num3;
if (num1 > num2)
    if (num1 > num3)
        cout << "The largest number is " << num1
             << endl;
```

如果第一个条件为真，则执行嵌套在第一个 if 语句内部的第二个 if 语句。

当你想要将 else 语句与嵌套的 if 语句一起使用时，else 语句总是与最近的 if 语句配对。例如：

```cpp
if (guess != number)
    if (guess < number)
        high = guess - 1;
    else
        high = guess + 1;
```

如果你希望 else 与第一个 if 语句结合，可以在嵌套的 if 语句周围使用花括号，如下所示：

```cpp
if (guess != number) {
    if (guess < number)
        low = guess + 1;
    else
        high = guess + 1;
}
else
    if (guess > number)
        high = guess - 1;
```

在编写嵌套 if 语句时，缩进有助于表明你的意图，但使用花括号将确保编译器按照程序员预期的方式执行代码。

#### if-else if 语句

你会如何使用 if 语句为数字考试成绩分配相应的字母等级？一种方法是编写一系列独立的 if 语句，如下所示：

```cpp
int numGrade;

string letterGrade;

cout << "Enter the numerical score: ";

cin >> numGrade;

if (numGrade >= 90)
    letterGrade = "A";

if (numGrade >= 80)
    letterGrade = "B";

if (numGrade >= 70)
    letterGrade = "C";

if (numGrade >= 60)
    letterGrade = "D";

if (numGrade < 60)
    letterGrade = "F";
```

该程序解决了问题，但造成了不必要的计算。如果用户输入数字 86，程序会将 `letterGrade` 赋值为 `"B"`，但随后会继续向下测试每个剩余 if 语句中的 `numGrade`。我们更希望发生的情况是，一旦程序将字母等级赋值给变量，程序就不应该再对 `numGrade` 执行任何测试，而是继续执行下一个任务。

这个问题的解决方案是使用 if 语句的另一种变体——if-else if 语句。if-else if 语句的一般形式如下：

```cpp
if (condition)
    statement;
else if (condition)
```



```cpp
if (condition)
    statement;
else if (condition)
    statement;
else if (condition)
    statement;
...
else
    statement;
```

省略号表示在可选的 else 子句结束该 if 语句之前，还可以编写更多 else if 子句。此外，与 if 语句一样，你可以通过将语句放入块中，在每个 else if 子句内放置多条语句。

现在让我们使用 if-else if 语句来看上面的评分问题：

```cpp
int numGrade;
string letterGrade;
cout << "Enter the numerical score: ";
cin >> numGrade;
if (numGrade >= 90)
    letterGrade = "A";
else if (numGrade >= 80)
    letterGrade = "B";
else if (numGrade >= 70)
    letterGrade = "C";
else if (numGrade >= 60)
    letterGrade = "D";
else if (numGrade < 60)
    letterGrade = "F";
cout << numGrade << " is a " << letterGrade
     << endl;
```

这个新版本的程序在某个条件为真时消除了不必要的测试。如果用户输入分数 74，条件 (numGrade >= 70) 为真，因此 letterGrade 被赋值为“C”，程序跳到最后一个 else if 子句后的第一行，并显示输出：

```
74 is a C
```

我们可以对程序做的一项改进是删除最后一个 else if 子句，因为如果其他条件都不成立，那么该分数的字母等级必定是“F”。因此我们可以按以下方式重写程序：

```cpp
int numGrade;
string letterGrade;
cout << "Enter the numerical score: ";
cin >> numGrade;
if (numGrade >= 90)
    letterGrade = "A";
else if (numGrade >= 80)
    letterGrade = "B";
else if (numGrade >= 70)
    letterGrade = "C";
else if (numGrade >= 60)
    letterGrade = "D";
else
    letterGrade = "F";
cout << numGrade << " is a " << letterGrade << endl;
```

在完全结束 if 语句之前，让我们看一个更复杂的评分问题，它要求我们使用逻辑运算符。

有些学业项目会给标准字母等级加上正负号，例如 A+、B- 等。具体等级由如下数字分数范围决定：

| 数字分数 | 字母等级 |
|---|---|
| 97-100 | A+ |
| 94-96 | A |
| 90-93 | A- |
| 87-89 | B+ |
| 84-86 | B |
| 80-83 | B- |
| 77-79 | C+ |
| 74-76 | C |
| 70-73 | C- |
| 67-69 | D+ |
| 64-66 | D |
| 60-63 | D- |
| 0-59 | F |

具体范围（例如 97 到 100）通过如下方式使用 && 运算符来判定：

```cpp
((numGrade >= 97) && (numGrade <= 100))
```

当我们对每个可能的考试分数范围都这样做时，就可以适当地分配字母等级。下面是程序：

```cpp
// GradeRange.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    int numGrade;
    string letterGrade;
    cout << "Enter a numeric grade: ";
    cin >> numGrade;
    if ((numGrade >= 97) && (numGrade <= 100))
        letterGrade = "A+";
    else if ((numGrade >= 94) && (numGrade <= 96))
        letterGrade = "A";
    else if ((numGrade >= 90) && (numGrade <= 93))
        letterGrade = "A-";
    else if ((numGrade >= 87) && (numGrade <= 89))
        letterGrade = "B+";
    else if ((numGrade >= 84) && (numGrade <= 86))
        letterGrade = "B";
    else if ((numGrade >= 80) && (numGrade <= 83))
        letterGrade = "B-";
    else if ((numGrade >= 77) && (numGrade <= 79))
        letterGrade = "C+";
    else if ((numGrade >= 74) && (numGrade <= 76))
        letterGrade = "C";
    else if ((numGrade >= 70) && (numGrade <= 73))
        letterGrade = "C-";
    else if ((numGrade >= 67) && (numGrade <= 69))
        letterGrade = "D+";
    else if ((numGrade >= 64) && (numGrade <= 66))
        letterGrade = "D";
    else if ((numGrade >= 60) && (numGrade <= 63))
        letterGrade = "D-";
    else
        letterGrade = "F";
    cout << "The letter grade is " << letterGrade
         << "." << endl;
    Console::ReadKey();
    return 0;
}
```

现在让我们看一个需要使用 || 运算符的情形。一种古老的儿童游戏是讲猪拉丁语。在猪拉丁语中，单词的构成取决于它以元音还是辅音开头。如果单词以辅音开头，就把第一个字母移到单词末尾，并加上“ay”。例如，单词“dog”的猪拉丁语形式是“ogday”。如果单词以元音开头，则猪拉丁语单词通过在单词末尾加上“ay”构成。所以“apple”的猪拉丁语形式是“appleay”。

要用 C++ 编写猪拉丁语转换器，我们需要能够查看单词的第一个字母，以决定使用哪种转换方法。有一个 C++ 字符串函数可以从字符串中提取部分字符串，称为 substr。我们可以使用该函数检查单词的第一个字符。然后需要判断该字母是元音还是辅音，这可以通过一个 if 语句完成，其中多个条件用 || 运算符连接。我们必须决定是查找元音还是辅音，由于元音比辅音少，我们将查找元音来决定使用哪种转换方法。

在英语中，我们会说类似这样的话：“如果第一个字母是 'a'，或者第一个字母是 'e'，或者第一个字母是 'i'，或者第一个字母是 'o'，或者第一个字母是 'u'……” 在 C++ 中我们可以这样表达：

```cpp
if ((letter == "a") || (letter == "e") ||
    (letter == "i") || (letter == "o") ||
    (letter == "u"))
```

现在让我们把它放入一个完整程序中，该程序将识别单词开头的字母类型：

```cpp
// pigLatin.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    string word, letter;
    cout << "Enter a word: ";
    cin >> word;
    letter = word.substr(0,1);
    if ((letter == "a") || (letter == "e") ||
        (letter == "i") || (letter == "o") ||
        (letter == "u"))
        cout << letter << " is a vowel";

    else
        cout << letter << " is a consonant";
    Console::ReadKey();
    return 0;
}
```

要让此程序运行，你需要包含对 string 库的引用，它紧接在 iostream 库的引用之下。

### 练习

1. 将以下程序片段改写为单个 if-else 语句：

```cpp
year = 2010;
if ((year % 4) == 0)
    cout << "The year is a leap year.";
if ((year % 4) != 0) {
    year = year + 4 - year % 4;
    cout << year << " is the next leap year.";
}
```

2. 改写以下代码片段，删除任何不必要的比较：

```cpp
if (age > 64)
    cout << "Senior voter";
if (age < 18)
    cout << "Under age";
if ((age >= 18) && (age < 65))
    cout << "Regular voter";
```

3. 编写一个程序，接受用户输入的单个字母，并显示电话上对应的数字。电话上的字母和数字分组如下：

| 数字 | 字母 | 数字 | 字母 | 数字 | 字母 | 数字 | 字母 |
|---|---|---|---|---|---|---|---|
| 2 | ABC | 4 | GHI | 6 | MNO | 8 | TUV |
| 3 | DEF | 5 | JKL | 7 | PRS | 9 | WXY |

Q 或 Z 没有对应数字，因此程序应向用户显示一条消息说明这一点。务必包含提示用户输入字母的提示信息。

4. 编写一个程序，要求用户输入一个算术运算符，然后输入两个数字（int）。程序随后应执行该运算符所表示的算术运算，并按以下形式显示结果（number1 operator number2 = result）。

## 第 7 章：重复

通过 if 语句进行决策是编写有用程序所需的第一个真正强大的编程构造。我们需要的第二个编程构造是重复。人类不擅长一遍又一遍地做事情；我们会感到无聊和疲倦，最终开始犯错。然而，计算机从不疲倦或无聊，可以连续数小时执行同样的任务，甚至不会犯最细微的错误。在本节中，我们将学习如何在 C++ 中使用 while 循环语句执行重复，这也称为循环。

### while 循环

在 C++ 中执行重复的一种方法是使用 while 循环。while 循环会检查一个条件，很像 if 语句所做的那样，在条件为真时重复执行一组语句。多次执行语句的过程称为*迭代*。

while 循环的一般形式如下：

```cpp
while (condition)
{
    statement1;
    statement2;
    statementn;
}
```

块内的语句称为循环体。

while 循环有两个必要的组成部分：1）一个需要测试的条件；2）一个使得条件最终变为 false 的语句。第二个组成部分很重要，因为如果控制循环的条件永远不会变为 false，循环将永远运行（或至少直到计算机资源耗尽）。这种情况被称为*无限循环*。

让我们看两个简单的 while 循环示例。第一个示例将 “Hello, World!” 这个短语显示十次。代码如下：

```cpp
int number = 1;

while (number <= 10)
{
    cout << "Hello, World!" << endl;
    ++number;
}
```

这个示例非常简单，但它指出了成功实现 while 循环所需的重要组件。变量 number 称为循环控制变量。该变量的值控制循环的迭代。通常，循环控制变量在循环外部被赋予一个值。然后，循环控制变量在条件中进行测试。因为我们要显示十次 “Hello, World!”，所以每次循环迭代时 number 的值都必须小于或等于 10。它被初始化为 1，这样条件将为 true，从而进入循环体。

变量初始化后，将测试 while 循环条件。由于 number 当前值为 1，且 1 小于或等于 10，条件为 true，因此进入循环体。短语 “Hello, World!” 被显示到控制台，在最后一行，number 的值增加到 2。

此时，程序回到循环条件，再次进行测试。由于 2 小于或等于 10，条件为 true，并执行另一次迭代。这一过程持续到 number 的值变为 11。当条件被测试时，该值为 false，因为 11 不小于或等于 10，而是大于 10，因此控制权转移到右花括号之后的语句。

下一个示例也没有做什么非常重要的事情，但它再次演示了 while 循环的常见组成部分。我们要编写一个程序，对整数 1 到 10 求和。我们的循环控制变量将再次命名为 number。它被初始化为 1，并在每次迭代时增加 1。我们还需要在循环外部初始化第二个变量（sum），用来在计算过程中保存这些数字的和。

程序如下：

```cpp
// WhileLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number, sum;
    number = 1;
    sum = 0;
    while (number <= 10)
    {
        sum += number;
        ++number;
    }
    cout << "The sum of 1 - 10 is " << sum << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出是：

The sum of 1 - 10 is 55

这个程序还演示了循环控制变量除了控制循环迭代之外，还可以用于其他用途，因为 number 的值被用来计算总和。

### 从文件读取数据

在大多数 C++ 程序中，主要有两种类型的 while 循环——计数器控制循环和哨兵控制循环。上面讨论的示例都是计数器控制循环，因为循环的条件基于达到某个计数，无论是在 “Hello, World!” 示例中循环的迭代次数，还是在计算总和示例中达到某个数字。

另一方面，哨兵控制循环由特定情况控制，例如达到特定值，或者资源耗尽，例如到达文件末尾。该值称为哨兵值，当获得该哨兵值时，哨兵控制循环停止。

哨兵控制循环的一个经典示例是读取文本文件内容的循环。读取数据文件通常由哨兵值控制，因为我们不知道何时到达文件末尾。无法输入特定值，例如要读取的行数，除非我们事先知道文件中有多少行，但这种情况很少见。我们将讨论如何通过读取文本文件的内容来开发哨兵控制循环。

### 处理文本文件

为了从文本文件读取数据，我们需要使用一些特殊函数和对象，它们是外部库 fstream 库的一部分。该库称为“文件流”库，允许我们将文本文件作为流打开，就像我们使用 iostream 库来处理控制台和键盘一样。

第一步是包含 fstream 库的预处理器指令：

```cpp
#include <fstream>
```

该指令被放置在与 iostream 库指令相同的组中。

下一步是创建一个表示我们要读取的文件的文件对象。由于我们正在从文件读取数据，因此文件对象的数据类型是 ifstream。如果我们要将数据写入文件，则会使用 ofstream（输出）数据类型。创建文件对象的代码行是：

```cpp
ifstream myFile;
```

我们还需要一个字符串变量来存储读取的数据：

```cpp
string line;
```

然后我们需要将文件对象与物理文件关联起来。我们使用 open() 函数来完成这一步，将文件的完整路径作为函数的参数传入。该函数直接从文件对象调用，如下所示：

```cpp
myFile.open("c:\\data\\example.txt");
```

open() 函数的参数必须是文件的完整路径，除非文件位于程序所在的同一目录中，在这种情况下，我们可以只使用文件名：

```cpp
myFile.open("example.txt");
```

当文件打开后，我们就可以读取其内容了。这需要一个 while 循环，该循环将一直运行到文件中没有更多数据为止。这是一个哨兵控制循环的示例，我们用于读取数据的哨兵值是由 fstream 函数 eof() 给出的 true/false 值。当文件中还有更多数据要读取时，该函数返回 false，当没有更多数据时返回 true。代码如下：

```cpp
while (!myFile.eof())
{

```

请注意，我们在这里使用了 !（非）运算符，因为 eof() 函数在有数据可读时返回 false，因此我们必须对该 false 值取反，以便循环继续运行。

循环体中的第一行读取一行文本并将其存储在一个变量中：

```cpp
getline(myFile, line);
```

下一行也是最后一行，显示从文件读取的文本：

```cpp
cout << line << endl;
}
```

最后，无论何时打开文件，我们都应该关闭它，并且有一个 close() 函数正是为此目的而设计的：

```cpp
myFile.close();
```

完整的程序如下：

```cpp
// textFile.cpp : main project file.
#include "stdafx.h"
using namespace System;
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream myFile;
    string line;
    myFile.open("example.txt");
    while (!myFile.eof())
    {
        getline(myFile, line);
        cout << line << endl;
    }
    myFile.close();
    Console::ReadKey();
    return 0;
}
```

这个示例演示了如何处理文本文件，但它并没有真正解决一个问题。让我们编写一个程序，从文件中读取一组每日最高温度，并计算平均最高温度。这是一个有趣的问题，因为我们必须跟踪已读取的温度数量，以便计算平均值。首先，创建一个包含温度列表的文本文件。尽量不要注意你在文件中放了多少个温度，但至少包括十五到二十个温度。

下面是计算平均温度的程序：

```cpp
// readTemps.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream temps;
    int temp, totalTemps, numTemps;
    double average;
    totalTemps = numTemps = 0;
    temps.open("C:\\data\\temperatures.txt");
    while (!temps.eof())
    {
        temps >> temp; // read an int
        totalTemps += temp;
        ++numTemps;
    }

    average = totalTemps / numTemps;
    cout << "The average temperature is: " << average
         << endl;
    Console::ReadKey();
    return 0;
}
```

这个程序中有一些你以前没见过的新东西。这一行：

```cpp
totalTemps = numTemps = 0;
```


表示没有更多输入，程序可以继续执行其处理。

下面是一个示例。我们想要一个程序来计算一组测试成绩的平均值，但不知道会输入多少个测试成绩。在这类程序中，必须使用一个数值作为哨兵值，因为程序将从键盘读取数字。对于测试成绩，一个好的哨兵值是 -1，因为可能的最低测试成绩是 0（除非这是一场非常、非常难的考试）。

解决这个问题的程序如下：

```cpp
// AverageGrade.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int testScore, total, count;
    double average;
    total = 0;
    count = 0;
    cout << "Enter a test score (-1 to quit): ";
    cin >> testScore;
    while (testScore != -1)
    {
        total += testScore;
        ++count;
        cout << "Enter a test score (-1 to quit): ";
        cin >> testScore;
    }
    average = total / count;
    cout << endl << "The average test score is: "
         << average << endl;
    Console::ReadKey();
    return 0;
}
```

下面是该程序的一次示例运行：

```text
Enter a test score (-1 to quit): 87
Enter a test score (-1 to quit): 98
Enter a test score (-1 to quit): 76
Enter a test score (-1 to quit): 88
Enter a test score (-1 to quit): 92
Enter a test score (-1 to quit): 83
Enter a test score (-1 to quit): -1
```

平均测试成绩为：87

程序会不断提示用户输入测试成绩，直到输入 -1 为止。输入 -1 会使循环条件为假，从而退出循环。请注意，第一次提示输入测试成绩必须放在循环之外，以便循环体能够正确执行。这有时被称为“预先输入一次（priming the pump）”。如果你不预先输入一次，而是把提示放在循环内部，像这样：

```cpp
while (testScore != -1)
{
        cout << "Enter a test score (-1 to quit): ";
        cin >> testScore;
        total += testScore;
        ++count;
}
```

哨兵值将被计入总和，导致平均值计算错误。

### for 循环

用于重复的第二种结构是 for 循环。for 循环主要用于需要将一组语句迭代固定次数的情况，而 while 循环主要用于需要将一组语句迭代到特定条件发生为止的情况。

#### 使用 for 循环

for 循环的一般形式如下：

```
for(control-var declaration; condition; control-variable modification)
{
    statement1;
    statement2;
    statementn;
}
```

一个具体示例将说明 for 循环如何工作。下面是一个显示数字 1 到 10 的简单程序：

```cpp
// ForLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    for(int i = 1; i <= 10; ++i)
    {
        cout << i << " ";
    }
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```text
1 2 3 4 5 6 7 8 9 10
```

首先发生的是声明循环控制变量 i，并将其初始化为 1。接下来测试条件。这个循环的条件表示，当 i 的值小于或等于 10 时，就迭代执行循环。由于 i 刚刚被初始化为 1，条件为真，因此进入循环体。

与 while 循环一样，for 循环的循环体是一个块。这个特定循环的循环体只有一条语句，因此将 i 的值写入控制台。由于这是循环体中的第一条也是最后一条语句，接下来执行循环控制修改步骤，将 i 的值递增 1。

现在 i 的值是 2，再次测试条件。条件为真，因此将 i 的值 2 写入控制台，并再次将 i 递增 1。for 循环以这种方式继续，直到 i 的值递增到 11。然后测试条件，结果为假，因为 11 不小于或等于 10，于是退出循环体。

#### 更多 for 循环示例

for 循环的一种用途是确定某项投资在某个时间间隔结束时的价值。假设你想以 2% 的年利率投资 10,000 美元，期限为 10 年。到该期限结束时，这项投资的价值会是多少？

解决这个问题的算法包括：将本金乘以利率，并将该值加回本金，重复 10 次。我们可以使用 for 循环来解决这个问题。代码如下：

```cpp
// ForLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    double rate = 1.02;
    double principal = 10000;
    for (int i = 1; i <=10; ++i)
    {
        principal *= rate;
    }
    cout << "After 10 years, $10,000 invested at 2%"
         << " annually will be worth: $"
         << principal << endl;
    Console::ReadKey();
    return 0;
}
```

让我们看一个不涉及数字的示例。如果我们想使用一种简单的加密算法来加密一个句子，我们可能想知道句子中有多少个元音字母。为此，我们必须检查字符串中的每个字符，并将其与元音字母列表进行比较。我们可以使用 for 循环来控制我们在字符串中的移动。

要编写这个程序，我们需要使用几个之前未见过的字符串函数。其中第一个是 substr() 函数。该函数被称为“子串函数”，它从字符串中返回一个子串。该函数的参数是你想要开始子串的字符位置，以及你希望子串包含的字符数。下面是一个示例：

```cpp
string word = "Hello";

cout << word.substr(1,3);  // returns "ell"
```

字符串中的字符从位置 0 开始编号。因此，“Hello”中的字母“H”位于位置 0。“e”位于位置 1。所以，如果我们写 word.substr(1,3)，意思是我们想从位置 1 开始返回该单词中的 3 个字符。

这个示例需要的第二个字符串函数是 compare() 函数。通常的关系运算符在 C++ 中不能用于字符串，因此我们必须使用其他方法来比较字符串。compare() 函数接受一个字符串作为参数，并将其与该函数被调用时所针对的字符串对象进行比较。根据字符串参数的值，该函数返回 0、1 或 -1。例如，如果我们写：

```cpp
string fruit = "banana";

cout << fruit.compare("apple");
```

将返回值 1，因为“banana”大于“apple”。如果将“pear”与变量 fruit 比较，我们会得到值 -1，因为“banana”小于“pear”。如果将“banana”与“banana”比较，我们会得到 0，因为它们相等。

现在我们可以编写元音计数程序的算法了。

该程序的输出为：

句子中的元音字母数量为：23

#### 嵌套 for 循环

有许多编程问题中的数据以表格形式组织。例如，如果教师想计算班上每个学生的平均成绩，数据会组织成类似下面的样子：

|  | 测试 1 | 测试 2 | 测试 3 | 测试 4 |
|---|---:|---:|---:|---:|
| 学生 1 | 84 | 78 | 93 | 98 |
| 学生 2 | 78 | 82 | 84 | 89 |
| 学生 3 | 93 | 89 | 98 | 100 |

程序将从第一个学生开始，横向遍历各列，将每个成绩累加求和，然后除以成绩数量以显示平均值，接着转向下一个学生。这个程序将需要两个 for 循环：一个外层 for 循环用于从一个学生移动到下一个学生，一个内层 for 循环用于横向遍历成绩列。以这种方式协同工作的两个 for 循环称为嵌套 for 循环。

我们还不能用嵌套 for 循环来解决上面的问题，因为我们还没有学习如何将数据存储在数组中（我们很快就会讲到数组）。不过，我们可以用一个更简单的问题来演示如何使用嵌套 for 循环——显示乘法表。

首先，让我们看看 1 x 1 到 5 x 5 的乘法表的布局：


| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

我们可以清楚地看到，行可以由一个 for 循环（内层循环）控制，列由另一个 for 循环（外层循环）控制。现在让我们看看这个程序：

```cpp
// ForLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    int product;
    for(int leftOp = 1; leftOp <= 5; ++leftOp)
    {
        for(int rightOp = 1; rightOp <= 5; ++rightOp)
        {
            product = leftOp * rightOp;
            cout << leftOp << " x " << rightOp << " = "
                 << product << "\t";
        }
        cout << endl;
    }
    Console::ReadKey();
    return 0;
}
```

以下是该程序的输出：

| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

每行中的间距由制表符（`\t`）控制。

在之前所有的 for 循环中，我们都使用单字母变量作为循环控制变量。这是可以接受的，因为阅读代码的人很容易理解该变量的用途。然而，对于这个程序，我们决定为循环控制变量使用更有意义的名称：leftOp 和 rightOp，因为这有助于读者更容易理解程序。

### 练习

- 1. 编写一个程序，要求用户输入一个数字，然后计算从 1 到该数字的平方和。例如，如果用户输入 4，则平方和为 30（1 + 4 + 9 + 16）。输出应包含用户输入的数字和结果。
- 2. 编写一个程序，从文件中读取一组数字，并显示文件中偶数的个数和奇数的个数。提示：使用 % 运算符判断一个数字是偶数还是奇数。
- 3. 编写一个程序，计算 16 到 36 范围内的偶数。在程序中使用 for 循环。
- 4. 使用 while 循环和 for 循环编写一个程序，从文件中读取一组数字，并为每个数字打印一串星号。输出应如下所示：

  ```
  5 -   *****
  10 -  **********
  7 -   *******
  ```

## 第 8 章：向量

到目前为止，我们讨论的数据类型适用于存储单个项。用于存储姓名的变量只能存储一个姓名；用于存储数字的变量只能存储一个数字。我们经常需要能够使用同一个变量名存储多个值。这个问题的一种解决方案是向量。向量允许我们在一个名称下存储多个相同数据类型的项。这种数据结构可以看作一个列表，例如成绩列表或姓名列表。

### 什么是向量？

如上所述，向量可以看作相同数据类型的数据项列表。列表中的每一项由列表中的索引位置指定。添加到向量的第一个项放在索引位置 0，下一项放在索引位置 1，再下一项放在索引位置 2，依此类推。

从图形上看，向量如下所示（第一列是索引，并且该向量被声明为最初有 10 个元素）：

| 索引 | 元素 |
|---:|---|
| 0 | 数据项 |
| 1 | 数据项 |
| 2 | 数据项 |
| 3 | 数据项 |
| 4 | 数据项 |
| 5 | 数据项 |
| 6 | 数据项 |
| 7 | 数据项 |
| 8 | 数据项 |
| 9 | 数据项 |

向量的一个特殊性质是，向量会自动增长以容纳添加到向量中的新项。这种能力将向量与数组区分开来，数组与向量类似，但不具备自动增长的能力。

### 创建向量

向量的声明方式很特殊。以下是向量声明的一般形式：

```cpp
vector<data type> vector-name(number of items, default-value);
```

在 C++ 程序中使用向量之前，必须提供一条预处理器指令，将 vector 类导入程序。将以下行添加到其他预处理器指令中：

```cpp
#include <vector>
```

向量声明以关键字 vector 开头。接下来是存储在向量中的元素的数据类型。数据类型括在小于号和大于号中，这种用法通常称为尖括号。你可以选择在圆括号内提供一个参数，指定最初要存储在向量中的项数。还可以选择为向量元素提供默认值。以下是一些向量声明的示例：

```cpp
// create string vector with 20 elements
vector<string> names(20);
// create integer vector with 100 elements
vector<int> numbers(100);
// create double vector with 0 elements
vector<double> ratios;
// create int vector all 0s
vector<int> numbers(100, 0);
```

### 向向量添加元素

向向量添加元素最常见的方法是使用类方法 push_back()。该方法将其参数放入向量中的下一个可用位置。以下示例演示如何创建一个新向量并向其中填充两个数据项：

```cpp
vector<string> names;
names.push_back("Raymond");
names.push_back("Jennifer");
```

该向量如下所示：

| | |
|---|---|
| 0 | Raymond |
| 1 | Jennifer |

使用 push_back() 添加的每个新数据项都直接放在之前添加的数据项之后。

以下代码片段允许用户通过交互式循环将姓名输入向量：

```cpp
char answer;
string name;
cout << "Do you want to enter names? ";
cin >> answer;
while (answer == 'y')
{
    cout << "Enter a name to store in the vector: ";
    getline(cin, name);
    names.push_back(name);
    cout << "Do you want to enter more names? ";
    cin >> answer;
}
```

### 访问向量元素

通过指定索引位置来访问向量元素。例如，以下行显示上面 names 向量中的第一个姓名：

```cpp
cout << names[0];
```

如果要访问向量的所有元素，请使用从向量的第一个元素开始、到最后一个元素结束的 for 循环。使用这种技术的一个问题是，你可能无法预先知道向量中最后一个元素的位置。你可以使用向量方法 size()，它返回当前向量中的元素个数。

以下程序将数字 1 到 10 存储在一个向量中，然后使用 for 循环对向量元素求和：

```cpp
// Vector.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
using namespace std;

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    for(int i = 1; i <= 10; ++i)
    {
        numbers.push_back(i);
    }
    int sum = 0;
    for(int i = 0; i < numbers.size(); ++i)
    {
        sum += numbers[i];
    }
    cout << "The sum of the integers 1 to 10 is: "
         << sum << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

整数 1 到 10 的和为：55

为 `rand()` 函数设置种子后，就可以生成随机数了。你可能希望为随机数指定一个范围。为此，请使用以下公式：

```
rand() % maxNumber + 1
```

例如，如果你希望随机数范围是 1 到 100，可以使用以下语句生成随机数：

```cpp
// generate random number between 1 and 100
int randomNumber = rand() % 100 + 1;
```

将值加 1 可确保该函数可能生成范围内的最大值。

让我们看一个如何生成随机数的示例。以下程序可以作为儿童猜数字游戏的基础，用户尝试猜一个 1 到 10 之间的数字：

```cpp
// RandomNumber.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    srand(time(NULL));
    int numberToGuess = rand() % 10 + 1;
    int guess;
    cout << "Enter a guess: ";
    cin >> guess;
}
```



```cpp
if (guess == numberToGuess)
    cout << "Right!";
else
    cout << "Wrong. The number was "
         << numberToGuess;
Console::ReadKey();
return 0;
}
```

首先，请注意我们的程序导入了两个新的类库——cstdlib 和 ctime。rand() 和 srand() 位于 cstdlib 库中，而 time() 函数位于 ctime 库中。

程序本身相当简单。我们先为随机数生成器设置种子，然后生成一个 1 到 10 范围内的随机数。接着，我们让用户猜一个数字，并将用户的猜测与先前生成的随机数进行比较。

以下是程序某次运行的输出：

```
Enter a guess: 4
Wrong. The number was 1
```

现在我们来看如何生成随机数并将它们存入一个向量中。方法是一样的，我们只需把 rand() 函数放进循环里。对于这个程序，我们生成 1000 个 1 到 100 范围内的随机数。代码如下：

```cpp
// Vector.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    srand(time(NULL));
    for(int i = 1; i <= 1000; ++i)
    {
        numbers.push_back(rand() % 100 + 1);
    }
    // display the numbers in the vector
    for(int i = 0; i < numbers.size(); ++i)
    {
        cout << numbers[i] << " ";
    }
    unsigned int sum = 0;
    for(int i = 0; i < numbers.size(); ++i)
    {
        sum += numbers[i];
    }
    cout << endl << endl << "The sum is: " << sum
         << endl;
    Console::ReadKey();
    return 0;
}
```

以这种方式使用随机数非常方便。很少有人有耐心把 1000 个值输入到一个向量中。当然，寻找数据来测试程序的另一种解决方案是使用数据文件，并将数据从文件读入向量中。正如过去许多教材作者所说的那样，我们把这留作读者的练习。

### 练习

- 1. 编写一个程序，将 100 个随机数存入一个向量中。然后，程序应遍历该向量，并显示向量中发现的任何重复数字的列表。

- 2. 编写一个程序，将 50 个随机成绩存入一个向量中。然后，程序应遍历该向量，并记录大于或等于 60 的成绩数量以及小于 60 的成绩数量。

- 3. 编写一个程序，将用户输入的 10 个姓名和成绩分别存入两个向量中，然后循环遍历这些向量，每行显示一个姓名和成绩。

## 第 9 章

## 函数

在本文前面的章节中，我们探讨了控制计算机程序控制流的不同方式。到目前为止，我们已经见过以下几种控制流：

- 顺序——程序按顺序逐行运行。
- 选择——if 语句决定运行哪一组语句。
- 迭代——while 循环重复执行一组语句，直到某个条件变为假。

还有另一种控制编程语句执行顺序的方式——子程序。*子程序*是一组有名称的编程语句，编写它们是为了执行某种明确定义的操作。子程序会修改程序的控制流，因为当它们被调用时，组成子程序的语句集合会被执行，然后控制权会转回到调用子程序的位置。

在 C++ 中，子程序被称为*函数*。C++ 中有两种类型的函数：有返回值的函数和不返回值的函数。不返回值的函数称为 void 函数，以区别于有返回值的函数。我们将从讨论如何定义和使用有返回值的函数开始本节。

### 有返回值的函数

有返回值的函数是一组编程语句；当给定特定输入时，它总是返回相同的输出。例如，如果我们定义一个名为 square 的函数，它以数字 *n* 为输入，并返回 *n* * *n*，那么我们知道，当给 square 输入值 2 时，它总是会返回 4。

#### 定义有返回值的函数

我们可以很容易地把 square 函数的这个定义转换成 C++ 代码。函数定义放在 main() 函数之外，可以放在 main() 之前或 main() 之后。如果把函数定义放在 main() 之后，我们就必须采取一些额外步骤，所以现在我们将把函数定义放在预处理指令之后。

以下是 C++ 中 square 函数的定义：

```cpp
int square(int number)
{
    return number * number;
}
```

函数定义的第一行（严格按顺序）包括函数返回值的数据类型、函数名和参数列表，参数列表是该行中位于括号内的部分。

有返回值的函数定义必须始终包含函数返回值的数据类型。函数名应尽可能描述函数的用途。换句话说，命名函数时要像命名变量一样谨慎。

*参数列表*是函数所有输入的列表。一个函数可以没有输入，也可以有很多输入，不过通常一个函数会有一到三个输入。这些输入更正式地称为*参数*。参数类似于变量，因为它保存数据，所以必须在参数名之前指定其数据类型。如果一个函数有多个参数，则列表中每个参数必须用逗号分隔。下面我们将看到带有两个或更多参数的函数示例。

参数列表之后是一个包含*函数体*的块。当然，*函数体*的实际内容取决于函数的用途。不过，在*函数体*的某处必须有一个*return 语句*，它用于将函数计算出的值发送回调用该函数的位置。对于像我们的 square() 函数这样的简单函数，*return 语句*包含了计算返回值所需的全部处理。你在 C++ 中编写的函数中，许多（即使不是大多数）都不会这么简单。

现在我们来看函数在 C++ 程序中实际是如何使用的。下面是一个简单但完整的程序，演示了如何使用 square() 函数：

```cpp
// square.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int square(int number)
{
    return number * number;
}

int main(array<System::String ^> ^args)
{
    int num;
    cout << "Enter a number to square: ";
    cin >> num;
    cout << num << " squared is " << square(num) << endl;
    Console::ReadKey();
    return 0;
}
```

以下是该程序的一次示例运行：

```
Enter a number to square: 12
12 squared is 144
```

要使用一个函数，我们必须执行一次*函数调用*。函数调用可以放在任何期望出现表达式的位置。在上面的程序中，函数调用位于 cout 语句中：

```cpp
cout << num << " squared is " << square(num) << endl;
```

函数调用由函数名和一个作为函数输入的*实参*组成。在函数调用时，系统将程序的控制权转移到函数定义。实参值会替换定义中的参数，然后执行函数体。

通过用实参值替换参数，你可以把 square() 的定义看作如下形式：

```cpp
int square(12)
{
    return 12 * 12;
}
```

函数体执行时适用正常的求值规则，因此 12 * 12 求值为 144，并且这个值会返回给调用程序。




你可以把 `cout` 语句看作如下形式：

```cpp
cout << num << " squared is " << 144 << endl;
```

意思是函数的返回值被替换到函数调用处。现在 `cout` 语句会正常求值，因此以下内容会写入控制台：

```
12 squared is 144
```

### 函数示例——求一个数的幂

我们来开发另一个函数。这个函数将把给定的数提升到给定的幂。虽然有内置函数可以完成这件事，但自己动手构建它很有教学意义，可以让我们在定义函数方面获得更多经验。

定义函数时，有时先使用已知值写下函数应如何工作会很有用。例如，我们知道 2 的二次方是 4。因此，如果我们将函数命名为 `power`，并向它传递参数 2（作为底数）和 2（作为幂），结果将是 4。我们可以这样写：

```
power(2,2) → 4
```

现在再试另一个例子，仍然使用 2：

```
power(2,3) → 8
```

这样做几次将有助于你决定如何编写函数体。在这个例子中，你知道底数需要自乘 3 次才能计算出正确的值。一个简单的方法是使用 `for` 循环进行计算。

现在我们可以通过编写函数头来开始编写函数定义：

```cpp
int power(int base, int exp)
```

这是简单的部分。函数体更难，但我们已经决定使用 `for` 循环将底数自乘 `exp` 参数指定的次数。我们必须从值 1 开始，因为任何数的 1 次幂都是该数本身。代码如下：

```cpp
int power(int base, int exp)
{
    int number = 1;
    for(int i = 1; i <= exp; ++i) {
        number *= base;
    }
    return number;
}
```

现在我们要做的就是在程序中使用它，并用几个值测试它是否有效。首先，我们通过调用 `power(2,3)` 来测试它：

```cpp
int main(array<System::String ^> ^args)
{
    cout << power(2,3) << endl;
    Console::ReadKey();
    return 0;
}
```

这个程序如预期那样显示值 8。现在让我们用 2 的多个幂来试试。以下是完整程序：

```cpp
// Power.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int power(int base, int exp)
{
        int number = 1;
        for(int i = 1; i <= exp; ++i) {
                number *= base;
        }
        return number;
}

int main(array<System::String ^> ^args)
{
        for(int i = 1; i <= 10; ++i) {
                cout << i << "\t" << power(2,i) << endl;
        }
        Console::ReadKey();
        return 0;
}
```

该程序的输出是：

|   |   |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |
| 5 | 32 |
| 6 | 64 |
| 7 | 128 |
| 8 | 256 |
| 9 | 512 |
| 10 | 1024 |

### 函数的优点

创建和使用函数会为程序带来几个明显的优势。以下是其中一些：

- **函数可以简化程序**——一旦函数被创建并测试完成，你就不必再担心程序中的那部分。能够使用函数而不必担心其细节，可以让你更容易管理程序的其余部分。
- **函数可以消除冗余代码**——一旦函数被定义，你就可以在程序中反复使用它。没有函数，你更有可能多次编写相同的代码片段，这可能导致程序中出现更多错误。
- **函数使程序更易于维护**——如果你发现函数中有错误，只需在一个地方（函数定义）修正该错误。如果有多个代码片段存在相同错误，你很可能至少会在某一处漏掉它，或者需要更长时间才能找到该错误的所有实例。
- **函数使你的代码具有可移植性**——一旦编写并测试了一个函数，你就可以在其他程序中使用该函数。本文后面我们将学习如何创建包含用户定义函数的 `.h` 文件。

除了这些之外，函数还有其他优点，但当你开始学习 C++ 编程时，这些应该是对你最有意义的。

### void 函数

一个 *void 函数* 是不返回值的函数。这种类型的函数有时被称为 *子例程* 或 *子过程*。void 函数与有返回值函数相似，因为它们定义在有返回值函数所定义的相同空间中，它们可以有参数，并且有函数体。void 函数只是不返回值。因此你可能会问——如果它们不返回值，那它们有什么用？

这里有一个例子。你正在编写一个程序，它需要在报告的每一页开头打印一个标题，比如只打印准备报告的人的姓名和日期。代码行可能如下所示：

```
cout << "\t" << "Mary Smith" << endl;

cout << "\t" << date << endl;
```

因为这个代码片段必须在多个地方使用，所以它应该放在一个函数中。然而，它不返回任何数据，只是向控制台写出两行内容，因此它必须放在一个 void 函数中。

void 函数的定义方式与有返回值函数类似。以下是上述示例的定义：

```cpp
void printHeading(string date)
{
    cout << "\t" << "Mary Smith" << endl;
    cout << "\t" << date << endl;
}
```

由于 void 函数不返回值，因此它不能像有返回值函数那样在那么多地方被调用。大多数 void 函数都作为完整语句编写（调用），如下所示：

```cpp
string date;
cout << "Enter the date for the heading: ";
cin >> date;
printHeading(date);
```

### 按值传递与按引用传递

void 函数的另一个用途是同时修改两个变量的值。计算机编程中一个常见操作是交换两个变量的值，例如在排序操作中。例如，如果我们需要将两个 `string` 变量按字母顺序排序，可以调用一个 void 函数来执行交换。以下是 `swap` 函数的代码，以及调用该函数的代码：

```cpp
// Swap.cpp : main project file.

#include "stdafx.h"

using namespace System;

#include <iostream>
```

再次运行程序，我们得到以下输出：

```
banana apple
apple banana
banana apple
```

所以这些值在函数内部被交换了，但在函数调用结束后又恢复为原来的值。

我们的值没有被交换的原因在于 C++ 中参数传递的一条规则。这条规则规定，默认情况下，函数的参数是从调用程序按值传递给函数的。“按值”这个说法意味着，当调用函数时，C++ 编译器会复制参数值，并将该副本传递给被调用的函数。当函数完成并且控制权返回程序时，参数值会从内存中移除，即使它们已经被更改，就像上面的 `swap()` 函数示例那样，而程序中的变量仍保留其原始值（它们实际上从未丢失自己的值，因为为函数参数的使用制作了副本）。

如果我们希望被调用的函数能够永久更改函数参数，就必须按引用传递参数。“按引用”传递意味着编译器实际上是将实际参数传递给函数，这样函数就可以访问并更改参数的值，从而在控制权返回调用程序时保留其新值。

要按引用传递参数，请在参数名之前放置一个 & 符号（&）。& 符号称为引用运算符。我们将在本书后面进一步讨论它。

以下是一个函数定义的示例，该函数将 5 加到传递给它的参数上：

```cpp
void addFive(int &num)
{
    num += 5;
}
```

有些程序员建议将与符号放在数据类型旁边，而不是参数旁边，但编译器两种风格都能接受。

只有当没有其他方法可以完成特定任务时，才应该按引用传递参数。例如，上面的 addFive() 函数完全可以用一个值参数来编写，向调用程序返回参数加 5 的结果，这样，作为参数传入的变量就可以被赋值为函数的返回值。或者用更清晰的代码来表示：

```cpp
int addFive(int num)
{
    return num += 5;
}

// in calling program
int number = 0;
number = addFive(number);
```

然而，有些情况下只有按引用传递参数才行，swap() 函数就是其中之一。我们必须使用引用参数来编写该函数的主要原因在于，一个返回值的函数只能返回一个值，而 swap() 函数要处理的是两个值。

话不多说，让我们重写 swap 函数，使其能正确工作：

```cpp
void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}
```

现在 word1 和 word2 是按引用传递的，因此当函数改变这些变量的值时，它实际上是在调用程序中以及函数内真正地改变它们。下面是完整的程序：

```cpp
// Swap.cpp : main project file.

#include "stdafx.h"

using namespace System;

#include <iostream>
#include <string>
using namespace std;

void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}

int main(array<System::String ^> ^args)
{
    string word1, word2;
    word1 = "banana";
    word2 = "apple";
    cout << word1 << " " << word2 << endl;
    swap(word1, word2);
    cout << word1 << " " << word2 << endl;
    Console::ReadKey();
    return 0;
}
```

输出如下：

```
banana apple
apple banana
```

存储在各个内存地址中的值现在已经被交换，因此 word1 存储的是 "apple" 而 word2 存储的是 "banana"。

### 变量作用域

变量的作用域指的是变量的可访问性。变量在何处以及如何可访问，取决于变量在何处声明。最好通过示例来解释变量作用域的工作方式。请看下面这个简单的程序片段：

```cpp
int main()
{
    int number1;
    number1 = 23;
    int number2 = number1 * 13;
    return 0;
}
```

变量 number1 的作用域是 main() 函数。main() 函数块内的任何代码都可以访问 number1 的值。接下来再看一个更长的代码片段：

```cpp
int changeNumber(int number)
{
    return number *= 3;
}

int main()
{
    int number = 3;
    cout << changeNumber(number);
    cout << number;
    return 0;
}
```

参数 number 被称为 changeNumber() 函数的局部变量。这意味着该变量只能被函数定义内的代码访问，并且一旦函数停止执行，它的值就会从内存中完全移除。

为了演示这一点，让我们重写上面的程序来展示局部作用域是如何工作的。完整程序如下：

```cpp
// ScopeExample.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int changeNumber(int number)
{
    number *= 3;
    cout << "The value of number in the changeNumber()"
         << " function is: " << number << endl;
```

#### 作用域级别

上面的示例说明了 C++ 程序中可用的作用域级别之一。这些作用域级别包括：

- *全局*
- *局部*
- *块*

在函数（无论是 main 函数还是用户自定义函数）内声明的变量具有局部作用域。该变量及其值可被定义该函数的块内的任何代码访问。其他函数中的代码无法访问该变量。

##### 全局作用域

如果变量定义在 C++ 程序的全局区域中，则该变量具有全局作用域。这个区域是定义函数的区域，包括 main() 函数上方和下方的区域。在此区域中定义的变量称为*全局变量*，可以被程序中的任何代码访问。

让我们看一个关于全局变量如何工作的简单示例：

```cpp
// GlobalScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int number = 1; // global variable

int changeNumber()
{
    number += 5;
    return number;
}

int main(array<System::String ^> ^args)
{
    cout << "The value of number is: " << number
         << endl;
    number = changeNumber();
    cout << "Now the value of number is: "
         << number << endl;
    Console::ReadKey();
    return 0;
}
```

变量 number 是一个全局变量。即使该变量没有作为参数传递给 changeNumber() 函数，该函数也可以访问 number 的值。同样，尽管 number 没有在 main() 函数中声明，main() 函数也可以访问 number 的值。

如上所述，全局变量可以被程序中定义的任何代码访问。因此你可能会认为，应该将所有变量都声明为全局变量，以便于使用。然而，这是错误的想法。在程序中使用全局变量会带来很多问题。这些问题包括：

- 意外修改 —— 你可能会在某一个函数中意外地修改一个全局变量，却以为它在另一个函数中未发生变化。
- 无法复用代码 —— 大量使用全局变量会让代码变得更加僵化，使代码无法在其他程序中使用。
- 难以管理模块化 —— 大量使用全局变量的代码不如使用更多局部变量的代码具有模块性。

最好的建议是：一开始将变量声明为局部变量，只有在绝对必要时才将它们改为全局变量。在本书后面，我们将讨论使用全局变量更有优势的情况。

##### 局部作用域

我们已经讨论过如何创建具有*局部作用域*的变量，这里只回顾一下这个概念。在函数体内（包括 main() 函数）声明的变量被视为具有局部作用域。局部作用域变量的生命周期与函数的生命周期一致，并且该函数体内定义的任何代码都可以访问该变量。

##### 块作用域

具有*块作用域*的变量只能被该变量所在块内的代码访问。这似乎有些令人困惑，因为局部变量通常定义在一个块中，但很多时候会在另一个代码块内部存在一个代码块。

请看下面这个简单的 for 循环：

```cpp
// BlockScope.cpp : main project file.
#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    for(int i = 1; i <= 10; ++i)
    {
        cout << "The value of i in the loop is: "
             << i << endl;
    }
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```
The value of i in the loop is: 1
The value of i in the loop is: 2
The value of i in the loop is: 3
The value of i in the loop is: 4
The value of i in the loop is: 5
The value of i in the loop is: 6
The value of i in the loop is: 7
The value of i in the loop is: 8
The value of i in the loop is: 9
The value of i in the loop is: 10
```

现在，让我们通过在循环的右花括号之后添加下面这一行，来检查循环外 i 的值：

```cpp
cout << "The value of i outside the loop is: " << i
     << endl;
```

现在编译这个程序。你会发现编译无法通过，因为有一个错误。错误信息指出 i 是未声明的标识符。这是因为 i 是在 for 循环的块内声明的，具有块作用域。换句话说，i 及其值只能在 for 循环的块内被访问，一旦 for 循环结束，变量 i 就会从内存中移除。

你可以将块级作用域用于任何类型的块。虽然我们还没有讨论这一点，但你可以在程序的任何位置放置一个代码块。请看下面的程序：

```cpp
// BlockScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number = 1;
    cout << "The value of number is: " << number
         << endl;
    {
        int number = 100;
        cout << "The value of number in this block"
             << " is: " << number << endl;
    }
    number += 4;
    cout << "The value of number is: " << number << endl;
    Console::ReadKey();
    return 0;
}
```


在 `main()` 函数的代码块内部又创建了一个代码块。这并不常见，但绝对是合法的 C++ 代码。

该程序的输出为：

```
The value of number is: 1
The value of number in this block is: 100
The value of number is: 5
```

这段代码中有两个不同的 `number` 变量，一个在 `main()` 函数中声明，另一个在 `main()` 函数内部的代码块中声明。内层代码块中声明的变量一旦执行离开内层代码块，就会从内存中移除，但在内层代码块执行期间，可见的正是这个变量实例。

块级作用域是一个重要概念，它能防止程序被变量值污染。一个很长的程序可能有许多 `for` 循环和其他块级结构，如果控制这些结构的变量必须在其整个程序生命周期内可见，我们的程序就会浪费大量内存，更不用说跟踪大量变量所涉及的心力了。

### 将向量传递给函数

我们对向量所做的许多操作（显示元素、对数值向量的元素求和等）在程序运行过程中会被多次执行。因此，为其中许多任务创建函数是合理的。在本节中，我们将演示处理向量时常用的几个函数。

我们的第一个示例演示如何编写一个显示向量内容的函数。函数定义必须在参数列表中包含向量及其数据类型。函数体看起来就像我们之前用来显示向量内容的代码。下面的代码片段定义了一个显示 `int` 向量的函数：

```cpp
void DisplayVector(vector<int> n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        cout << n[i] << " ";
    }
    cout << endl;
}
```

要使用这个函数，只需将向量名作为函数的实参提供即可。下面是一个完整程序，它创建并使用 `DisplayVector()` 函数显示一个向量的内容：

```cpp
#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
using namespace std;

void DisplayVector(vector<int> n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        cout << n[i] << " ";
    }
    cout << endl;
}

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    for(int i = 1; i <= 10; ++i)
    {
        numbers.push_back(i);
    }
    DisplayVector(numbers);
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：1 2 3 4 5 6 7 8 9 10。

现在让我们看一个示例，编写一个以向量为参数并返回值的函数。在这种情况下，上面的程序需要一个对 `numbers` 向量的元素求和的函数。其定义看起来与我们之前编写的代码类似。函数定义如下：

```cpp
int SumVector(vector<int> n)
{
    int sum = 0;
    for(int i = 0; i < n.size(); ++i)
    {
        sum += n[i];
    }
    return sum;
}
```

在程序中，我们可以这样调用该函数：

```cpp
cout << "The sum of the elements of numbers is: "
     << SumVector(numbers) << endl;
```

输出为：

numbers 的元素之和为：55

前面的函数最容易使用，因为我们只是把向量作为值参数传递给函数。但是，如果我们想在函数中修改向量的一些或全部元素，该怎么办呢？例如，假设我们有一组成绩，需要按某个百分比或分数进行调分。我们想编写一个函数来完成这项任务，但如果向量是按值传递给函数的，那么函数执行完毕后，实际的向量值将与调用函数之前完全相同。

答案当然是按引用将向量传递给函数，就像我们学习按引用将实参传递给 `swap()` 函数时那样。让我们创建一个名为 `CurveGrades()` 的函数，它给向量中的每个成绩加 5 分：

```cpp
void CurveGrades(vector<int> &n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        n[i] += 5;  // add 5 to each vector element
    }
}
```

我们通过在参数列表中的参数名之前放置引用运算符 `(&)` 来按引用传递向量。现在，当我们在函数中修改向量时，这些更改将在调用程序中保留下来。

下面是一个完整程序，演示如何按引用传递向量：

```cpp
// VectorFunctions.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
using namespace std;

void DisplayVector(vector<int> n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        cout << n[i] << " ";
    }
    cout << endl;
}

int SumVector(vector<int> n)
{
    int sum = 0;
    for(int i = 0; i < n.size(); ++i)
    {
        sum += n[i];
    }
    return sum;
}

void CurveGrades(vector<int> &n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        n[i] += 5; // add 5 to each vector element
    }
}

int main(array<System::String ^> ^args)
{
    vector<int> grades;
    srand(time(NULL));
    for(int i = 1; i <= 10; ++i)
    {
        grades.push_back(rand() % 100 + 1);
    }
    DisplayVector(grades);
    CurveGrades(grades);
    DisplayVector(grades);
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```
67 31 20 76 81 44 96 38 69 84
72 36 25 81 86 49 101 43 74 89
```

### 练习

- 1. 编写一个函数，接收一个温度和一种温标（华氏度或摄氏度），并将该温度转换为指定的温标。例如，如果函数名为 `ftoc()`，则 `ftoc(212, 'c')` 返回 100。在一个程序中使用该函数，由用户输入实参的值。输出应采用如下形式：212 华氏度等于 100 摄氏度。
- 2. 编写一个函数，接收一个整数向量并返回该向量中的最大值。在一个程序中使用该函数。
- 3. 编写一个函数，接收一个圆的半径并返回其周长。你可以在互联网上查找该函数的公式。在一个程序中使用该函数。
- 4. 编写一个函数，使用循环和加法来执行乘法。在一个程序中使用该函数。该函数的实参是乘法的两个操作数，例如 `int product = multiply(4,5);`。
- 5. 编写一个函数，使用循环和减法来执行除法。在一个程序中使用该函数。下面是一个示例函数调用：`double ratio = divide(15,2);`。

## 第 10 章

## 数组

我们已经看过一种用于将数据组织成列表的数据结构——向量。还有另一种数据结构，不仅可以用于将数据组织成列表，还可以将数据组织成表格，甚至三维结构。这种数据结构称为数组。在本章中，我们将学习两种数组——将数据组织成列表的一维数组，以及将数据组织成表格的二维数组。

### 一维数组

向量是将数据一维组织的一种方式。另一种方式是使用数组。数组与向量非常相似。数组是一组相同数据类型的数据项，它们归在一个变量名之下。每个数据项都可以通过其在数组中的*索引*位置访问，从位置 0 开始，就像向量一样。然而，数组是一种固定长度的数据结构，不像向量那样在达到容量后还可以增长。

从图形上看，数组看起来像一个向量：

| 索引 | 元素 |
| --- | --- |
| 0 | 数据项 |
| 1 | 数据项 |
| 2 | 数据项 |
| 3 | 数据项 |
| 4 | 数据项 |
| 5 | 数据项 |





| 索引 | 数据项 |
|---|---|
| 6 | 数据项 |
| 7 | 数据项 |
| 8 | 数据项 |
| 9 | 数据项 |

数组的第一个元素存储在下标 0 处。这个下标被称为索引。在 C++ 代码中，索引使用下标表示法引用，正如我们在 vector 中使用的那样。如果上面的数组名为 `numbers`，那么要访问第一个元素，我们可以这样写：

```cpp
numbers[0]
```

由于数组总是从下标 0 开始，因此数组中的元素数量总是比数组最后一个位置（也称为*上界*）大 1。

#### 声明一维数组

数组必须像变量一样进行声明。数组声明的一般形式为：

```
数据类型 数组名[元素个数];
```

数组声明完成后，编译器会为数组元素预留一块连续的内存空间，因此声明中指定的元素个数必须大于 0。下面是一个示例：

```cpp
string names[10];
```

这条声明告诉编译器在连续内存中为 10 个 string 值预留空间，并将该数组命名为 `names`。你也可以在同一行声明多个相同数据类型的数组，就像变量一样，例如：

```cpp
int grades[20], numbers[100];
```

这行代码创建了两个数组，一个名为 `grades`，包含 20 个元素；另一个名为 `numbers`，包含 100 个元素，二者均为 int 类型。

在指定数组声明中的元素个数时，必须使用整型字面量或整型常量。如果尝试使用变量，编译器会报错，提示它期望一个常量表达式。因此，像这样的声明是合法的：

```cpp
const int size = 10;
int numbers[size];
```

但像这样的声明会导致错误：

```cpp
int size = 10;
int numbers[size];
```

#### 初始化数组元素

声明数组时，你需要将元素初始化为某个值，因为编译器不会自动为你完成这一操作。一种常见的方法是使用 for 循环访问每个元素并将其值设置为默认值。例如，在下面的程序中，声明了一个整型数组，并将每个值初始化为 0。第二个循环显示数组的内容。

代码如下：

```cpp
// Arrays.cpp : main project file.
#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int numbers[10];
    const int sizeNumbers = 10;
    for(int i = 0; i < sizeNumbers; ++i) {
        numbers[i] = i + 1;
    }
    cout << "Element" << "\t" << "Value" << endl << endl;
    for(int i = 0; i < sizeNumbers; ++i) {
        cout << i << "\t" << numbers[i] << endl;
    }
    Console::ReadKey();
    return 0;
}
```

程序的输出如下：

| 元素 | 值 |
|---:|---:|
| 0 | 1 |
| 1 | 2 |
| 2 | 3 |
| 3 | 4 |
| 4 | 5 |
| 5 | 6 |
| 6 | 7 |
| 7 | 8 |
| 8 | 9 |
| 9 | 10 |

不过，有时你想用默认值以外的值来初始化数组。这时可以使用*初始化列表*。下面是一个使用初始化列表声明数组的示例：

```cpp
int grades[5] = {84, 77, 99, 100, 87};
```

该列表是一个用花括号括起来、各值之间用逗号分隔的列表。列表中的数据元素个数必须与数组的声明大小匹配。你也可以省略方括号中的声明大小，编译器会自动确定数组大小，如下所示：

```cpp
int grades[] = {84, 77, 99, 100, 87};
```

第三种选择是将初始化列表留空，这会使编译器将声明数据类型的默认值赋给数组元素。示例如下：

```cpp
int grades[5] = {};
```

使用空初始化列表时，必须在声明中指定数组大小。

你还可以提供一个元素个数少于声明大小的初始化列表，例如：

```cpp
int grades[5] = {84, 77, 99};
```

在这种情况下，剩余的数组元素 `grades[3]` 和 `grades[4]` 会被初始化为该数据类型的默认值 0。

#### 使用一维数组

与 vector 一样，数组提供了一种使用单个名称处理多个数据值的便捷方式。将相关数据收集到数组中，然后对数组元素执行计算，是一种常见的编程技术。尽管数组是数据的集合，我们仍然需要通过访问单个数组元素来向数组中赋值或从数组中读取数据。

通过指定所需数组元素的索引即可访问该元素。如果我们想访问数组的前三个元素以计算它们的和，下面这行 C++ 代码可以实现：

```cpp
total = grades[0] + grades[1] + grades[2];
```

我们可以使用相同的索引技术向数组元素重新赋值：

```cpp
grades[1] = 98;
```

既然我们知道了如何访问数组元素并向其赋值，就可以利用数组执行一些任务了。例如，如果我们想找出家乡过去一周的平均最高气温，可以将每天的最高气温存储在一个数组中，然后使用该数组计算平均值。下面的程序正是这样做的：

```cpp
// avgTemp.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int numTemps = 7;
    int temps[] = {85, 77, 81, 86, 89, 92, 87};
    double average = 0.0;
    int total = 0;
    for(int i = 0; i < numTemps; ++i) {
        total += temps[i];
    }
    average = total / numTemps;
    cout << "The average temperature was: "
         << average

         << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

平均气温为：85

另一个涉及数组的常见任务是在数据集合中查找最小值或最大值。下面是一个在数组中查找最小值和最大值的简单算法：将第一个数组元素赋值给变量 min 和 max；检查数组中的下一个元素并与 min 和 max 比较；如果下一个元素的值小于 min，则将该元素的值赋给 min；如果下一个元素的值大于 max，则将该元素的值赋给 max；继续遍历数组直到到达数组末尾。

下面是一个在数组中查找最小值和最大值的程序：

```cpp
// minMax.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int min, max;
    const int size = 100;
    int numbers[size];

    srand(time(NULL));
    // initialize the array
    for(int i = 0; i < size; ++i) {
        numbers[i] = rand() % 100 + 1;
    }
    min = numbers[0];
    max = numbers[0];
    // search for min and max
    for(int i = 0; i < (size-1); ++i) {
        if (numbers[i+1] < min)
            min = numbers[i+1];
        if (numbers[i+1] > max)
            max = numbers[i+1];
    }
    cout << "The minimum value in the array is "
         << min << endl
         << "The maximum value in the array is "
         << max << endl;
    // display the values
    for(int i = 0; i < size; ++i) {
        cout << numbers[i] << " ";
    }
    Console::ReadKey();
    return 0;
}
```

这个程序对于小型数组来说相当高效，但随着数组规模变大，程序的效率会降低。

### 二维数组

一维数组用于存储列表数据。当你要存储自然以表格形式组织的数据时，需要使用二维数组。二维数组将数据组织为行和列。当我们要指定二维数组中的单个数据项时，必须指定两个位置：该数据项的行和列。

#### 声明二维数组

声明二维数组时需要指定数组要存储的行数和列数。例如，如果我们的数据有两行两列，则数组的声明为：

```c
int numbers[2][2];
```

如果数组有两行三列，声明如下：

```c
int numbers[2][3];
```

在声明中，行数总是先指定，然后才是列数。当然，在程序中你应该使用常量而不是数字字面量（但这里为了节省空间，我们使用了字面量）。

与一维数组一样，你也可以在一条语句中声明并初始化一个二维数组，如下所示：


```cpp
int temps[2][7] = {{87, 85, 89, 92, 94, 88, 90},
                   {79, 86, 85, 88, 93, 91}};
```

#### 初始化二维数组

要初始化二维数组，必须编写一个嵌套 for 循环，遍历行和列。下面是一个示例：

```cpp
const int rows = 2;
const int cols = 3;
int numbers[rows][cols];
    for(int r = 0; r < rows; ++r)
        for(int c = 0; c < cols; ++c)
            numbers[r][c] = 0;
```

在上面的代码片段中，外层 for 循环控制行，内层 for 循环控制列。因此，代码从第 0 行开始，将第 0、1、2 列填充为值 0，然后移到第 1 行，同样将第 0、1、2 列填充为值 0。

#### 显示二维数组元素

我们可以使用与初始化时相同的嵌套 for 循环技术来显示上述二维数组的内容。下面是我们的第一次尝试：

```cpp
for(int r = 0; r < rows; ++r)
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
```

该代码片段的输出为：

```text
0 0 0 0 0 0
```

这是数组的内容，但我们希望按行/列顺序查看它。为此，我们需要在第一行之后写入换行符。我们可以通过在外层 for 循环之后添加一条 cout 语句来修改代码片段，以适应这一需求。下面是新的代码片段：

```cpp
for(int r = 0; r < rows; ++r) {
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
    cout << endl;
}
```

注意，我们必须把内层 for 循环放在一个块中，因为外层 for 循环的主体现在由两条语句组成：for 循环和 cout 语句。

该代码片段的输出为：

```text
0 0 0
0 0 0
```

#### 二维数组示例

下面的程序演示了如何使用二维数组，从存储五名学生成绩的二维数组中计算每名学生的平均分。在讨论其工作原理之前，我们先看一下代码：

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};

    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; ++c) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```text
Student 1: 75 82 84 79 91 Average: 82
Student 2: 85 81 94 96 89 Average: 89
Student 3: 92 91 94 89 90 Average: 91
Student 4: 74 72 81 78 80 Average: 77
Student 5: 84 82 82 83 81 Average: 82
```

两个变量 total 和 average 在嵌套 for 循环之外声明并初始化。然后我们进入外层循环，它把我们置于成绩的第一行（学生 1）。当内层循环逐列移动时，每个成绩都会被访问、显示并加到 total 中。当循环到达最后一列时，控制权转移到外层循环，在那里计算并显示平均分。最后，在开始外层循环的新一轮迭代并移动到下一名学生之前，变量 total 和 average 会被重置为 0。不这样做会导致下一个总分和平均分计算错误。

#### 执行列序计算

并非所有涉及二维数组的任务都需要在外层循环中处理行（这称为*行序*）。有时你可能希望改为按列序处理二维数组。使用上面成绩示例进行列序计算的一个例子是，我们想计算每场考试的平均分。为此，我们想把第一列中所有考试成绩相加，然后计算平均分，接着处理第二列的考试成绩，依此类推。要做到这一点，只需让外层循环处理列，内层循环处理行。程序的其余部分看起来与计算学生考试成绩平均分时完全一样。

下面是修改后的上述程序，它还计算考试平均分：

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};
    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; c++) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    cout << endl << "Test Averages: " << endl;
    total = 0;
    average = 0.0;
    for(int c = 0; c < cols; ++c) {
        cout << "Test " << c+1 << ": ";
        for(int r = 0; r < rows; ++r) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / rows;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

该程序列序部分的输出为：

```text
Test Averages:
Test 1: 75 85 92 74 84 Average: 82
Test 2: 82 81 91 72 82 Average: 81
Test 3: 84 94 94 81 82 Average: 87
Test 4: 79 96 89 78 83 Average: 85
Test 5: 91 89 90 80 81 Average: 86
```

### 练习

- 1. 编写一个程序，从文件中读取 10 个单词，将它们存储到数组中，并显示单词长度的直方图。
- 2. 编写一个程序，将一系列字符存储到数组中。判断这些字符是否构成回文，回文是指正读和反读拼写相同的单词。例如，racecar 和 bob 都是回文。
- 3. 编写一个程序，将 10 个随机成绩存储到数组中。显示所有大于 80 的成绩。
- 4. 编写一个程序，将一年中的月份存储到数组中，提示用户输入月份编号，然后显示与该编号对应的月份。例如，1-一月、2-二月、3-三月，等等。
- 5. 下表列出了不同校区某些课程的注册学生人数。编写一个程序，将这些数据放入二维数组，并显示每个校区各课程注册的学生总数，以及选修每门课程的学生总数。

  |  | 课程 1 | 课程 2 | 课程 3 |
  |---|---|---:|---:|---:|
  | 校区 1 | 23 | 34 | 15 |
  | 校区 2 | 12 | 21 | 19 |
  | 校区 3 | 14 | 19 | 23 |

## 第 11 章

## 类与面向对象编程

我们在 C++ 中编写的程序，是对我们与世界中所存在对象进行交互的模拟。例如，薪资程序模拟公司如何运作，以及如何为员工所做的工作支付报酬。薪资程序的每个组成部分都代表一个对象。例如，员工有一张工时表，或称考勤卡，用来存储他或她在某个薪资周期内工作的小时数。员工还有薪水或时薪，这代表他们的薪酬标准。

在面向对象编程中，我们编写的程序所创建的对象，映射了我们试图模拟的对象。在 C++ 中，对象由类定义。类既包含对象属性或特性的定义，也包含对象行为的描述。例如，在描述一辆汽车时，我们会描述汽车的外观以及它如何运行或表现。在 C++ 中，我们可以通过创建和使用类与对象来做同样的事情。

除了定义对象的属性和行为之外，类还定义对象之间如何交互。通常，对象通过相互发送消息来交互。再次使用汽车的类比，如果一个 Person 对象想让一个 Automobile 对象行驶，Person 会向 Automobile 发送一条“踩油门踏板”消息。发送和接收消息的能力被定义为对象行为的一部分。

类的另一个显著特征是能够显示或隐藏构成类的属性和行为。任何属性或行为都可以暴露给其他对象，也可以隐藏起来，使其他对象无法访问该属性或行为。这一特性称为封装，也是面向对象编程被证明如此成功的原因之一。

在实践中，可以把类视为一种用户定义类型。能够扩展编程语言可处理的类型，是编程语言的一项关键特性。




### 类的定义

当我们在 C++ 中创建类时，会创建两个不同的部分——数据成员（也简称为成员），用于定义类的属性；以及方法（以函数形式实现），用于描述类的行为。

成员和方法在类的两个不同部分中定义，即公有部分或私有部分。在类的公有部分中定义的成员和方法对程序中的所有其他对象可见。在类的私有部分中定义的成员和方法仅对该类自身可见，而与该类交互的其他对象不可见。当我们查看几个示例后，这一切就会更加清楚。

类定义放在全局区域中，也就是定义函数所在的同一位置。类定义以关键字 class 和类名开头，后面跟着一个块，成员和方法的定义就放在这个块中。例如，要创建一个 Name 类，我们像这样开始定义：

```cpp
class Name
{
    // member and method definitions go here
};
```

注意，块的右花括号后面跟有一个分号。在 C++ 中，新类型的定义必须始终以分号结尾。

定义类的下一步是确定该类的成员。继续以 Name 示例为例，姓名的成员可以包括名、中间名和姓。我们也可以包括昵称、后缀（Jr.、Sr. 等）之类的内容，但为简单起见，我们将姓名限制为名、中间名和姓。

确定类的成员后，我们必须决定这些成员要放在公有部分还是私有部分。定义类时的一条常见规则是：将成员设为私有，并使用公有方法来访问和修改它们的值。

关键字 public 和 private 称为*访问修饰符*。它们决定成员或方法的访问级别。声明为 public 的方法或成员可以被程序中的任何代码访问。声明为 private 的方法或成员只能在类定义内部访问，而不能被使用该类的任何代码访问。

让我们通过包含成员声明来扩展 Name 类的定义：

```cpp
class Name
{
    private:
    string first, middle, last;
};
```

如你所见，类的私有部分由关键字 private 和冒号标记。在其下方声明和定义的所有内容都被视为该类的私有内容。

现在我们需要定义一个方法，通过它把数据放入类中。这个方法肯定需要设为公有，以便使用该类的程序能够访问该方法。该方法名为 setName，以下是它在完整类定义中的定义：

```cpp
class Name
{
    private:
    string first, middle, last;

    public:

    void setName(string firstName, string middleName,
                 string lastName)
    {
        first = firstName;
        middle = middleName;
        last = lastName;
    }
};
```

我们几乎可以让这个类进行试用测试了，但首先需要一个能显示姓名的方法。我们将这个方法称为 getName()，并同样把它放在公有部分：

```cpp
class Name
{
    private:
    string first, middle, last;

    public:

    void setName(string firstName, string middleName,
                 string lastName)
    {
        first = firstName;
        middle = middleName;
        last = lastName;
    }

    string getName()
    {
        return first + " " + middle + " " + last;
    }
};
```

现在可以在程序中使用这个类了。首先，我们需要声明一个 Name 对象：

```cpp
Name aName;
```

aName 被声明为一个 Name 对象。理解类与对象之间的区别很重要。类定义一种数据类型，而对象是该类型的一个实例。

创建 Name 类型的对象后，我们需要把数据放入该对象。可以使用 setName() 方法来完成：

```cpp
aName.setName("John", "Quincy", "Adams");
```

然后可以使用 getName() 方法显示姓名。该方法将每个成员作为一个拼接后的字符串返回，并在名和中间名之间留有空格。

这里不再只展示程序的另一个片段，而是给出完整程序，其中包括 Name 类定义：

```cpp
// NameClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Name
{
    private:
    string first, middle, last;

    public:

    void setName(string firstName, string middleName,
                 string lastName)
    {
        first = firstName;
        middle = middleName;
        last = lastName;
    }

    string getName()
    {
        return first + " " + middle + " " + last;
    }
};

int main(array<System::String ^> ^args)
{
    Name aName;
    aName.setName("John", "Quincy", "Adams");
    cout << aName.getName() << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

John Quincy Adams

### 使用构造函数创建类对象

创建类时的设计目标之一是让类尽可能灵活。这意味着为使用该类完成任务提供不同的可选方式。为类提供灵活性的一个例子是，让一个对象可以通过多种方式输入数据。

前面我们讨论了使用 setName() 方法输入数据的一种方式。有时你还希望在声明对象时就为对象输入数据。为此，你需要一种特殊类型的方法，称为构造函数。

Name 类的构造函数方法与 setName() 方法的工作方式完全相同：它将为每个成员提供参数，方法体将把方法的参数赋给对应的成员。标准类方法与构造函数方法的一个主要区别是，构造函数方法与类同名。例如，下面是 Name 类构造函数的一种可能定义：

```cpp
Name(string firstName, string middleName,
      string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}
```

有了这个构造函数定义，我们可以像这样创建一个新对象：

```cpp
Name yourName("Gene", "Ray", "Williams");
```

这使类的使用更加灵活，因为我们允许类的使用者像声明变量时那样，在声明对象时一并提供数据。

不过，有一个问题。C++ 不允许我们使用这个构造函数方法，除非我们再创建一个构造函数方法，称为*默认构造函数*。默认构造函数是没有参数的方法，它为类的成员分配默认值。如果未同时定义默认构造函数方法，Visual C++ 编译器将不允许定义构造函数方法。在我们定义第一个构造函数之前，编译器允许我们运行程序，因为如果没有提供构造函数，编译器会提供自己的默认构造函数。然而，一旦我们定义了构造函数，也就必须为默认构造函数提供定义。

因此，在使用上面的构造函数之前，我们必须定义一个默认构造函数。如下所示：

```cpp
Name()
{
    first = "";
    middle = "";
    last = "";
}
```

你可能已经注意到一件事：我们现在有两个同名构造函数方法。你在本书前面已经了解到，C++ 不允许同一作用域内有两个相同标识符，例如当你试图在 main() 中声明第二个变量，而该变量与已声明的变量同名时。

函数和类方法（实际上只是在类内部定义的函数）的唯一名称规则不同。两个

只要两个方法的参数列表存在具体差异，方法就可以同名。这称为*方法重载*。这种差异必须体现在参数列表中参数的数量和类型上。例如，我们可以在 Name 类中拥有两个名为 Name 的构造函数，因为一个构造函数具有空参数列表（默认构造函数），而另一个构造函数具有 3 个字符串参数。

利用重载规则，我们可以为 Name 类提供以下构造函数（这里只给出方法头）：

```cpp
Name();

Name(string firstName, string middleName, string lastName);

Name(string firstName, string lastName);

Name(string lastName);
```

这些方法在参数列表中的参数数量各不相同，因此当编译器看到对其中一个方法的调用时，就能将其与其他方法定义区分开来。

现在让我们看看所有这些构造函数的完整定义：

```cpp
Name()
{
    first = "";
    middle = "";
    last = "";
}

Name(string firstName, string middleName,
     string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

Name(string firstName, string lastName)
{
    first = firstName;
    middle = "";
    last = lastName;
}

Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}
```

带两个参数的 Name 构造函数将创建一个对象，其中包含名和姓，而中间名仅为空字符串；最后一个构造函数将创建一个对象，其中名和中间名为空字符串，而姓为传入的值。当然，选择最后一个构造函数只是因为假定不会创建只有名或中间名而没有姓的 Name 对象。

### 类的 Get 和 Set 方法

一旦创建了对象，并且数据已存储在成员中，就需要一些方法将数据存入对象和从对象中取出。设计良好的类会提供一组方法，用于从对象返回成员值并向成员赋值。这些方法称为 get 和 set 方法。

我们先从 set 方法开始。前面我们看过一个 set 方法的示例，即 setName() 方法。该方法在一次方法调用中设置所有成员的值。我们还需要为每个单独的成员提供 set 方法。以下是 Name 类所需的 set 方法：

```cpp
void setFirst(string firstName)
{
    first = firstName;
}

void setMiddle(string middleName)
{
    middle = middleName;
}

void setLast(string lastName)
{
    last = lastName;
}
```

现在，如果 Name 对象的名字发生了变化，但不涉及整个姓名，我们可以调用所需的任意一个 set 方法。例如：

```cpp
Name myName("Mary", "Alice", "Smith");
cout << myName.displayName() << endl;
// Mary gets married to Joe Brown
myName.setLast("Brown");
cout << myName.displayName() << endl;
```

输出为：

```
Mary Alice Smith
Mary Alice Brown
```

我们还需要能够单独返回信息的方法，而不只是像 getName() 那样成组返回。Get 方法提供了这种能力。以下是 Name 类的 get 方法：

```cpp
string getFirst()
{
    return first;
}

string getMiddle()
{
    return middle;
}

string getLast()
{
    return last;
}
```

下面这个小程序片段展示了如何使用 get 方法：

```cpp
cout << "The first name in myName is: " <<
     myName.getFirst() << endl;
cout << "The middle name in myName is: " <<
     myName.getMiddle() << endl;
cout << "The last name in myName is: " << myName.getLast()
     << endl;
```

此代码片段的输出为：

```
The first name in myName is: Mary
The middle name in myName is: Alice
The last name in myName is: Brown
```

### 其他类方法

除了所有类都需要的标准类方法（构造函数、get 方法和 set 方法）之外，类可能还需要其他方法来定义类的完整行为。

Name 类中可能需要的一个方法示例是返回 Name 对象姓名首字母的方法。我们不需要为这项数据创建成员，因为可以从已有的成员中获取它。我们只需从名、中间名和姓中提取第一个字符。以下是 getInitials() 方法的定义：

```cpp
string getInitials()
{
    return first.substr(0,1) + middle.substr(0,1)
        + last.substr(0,1);
}
```

对该方法的调用：

```cpp
cout << myName.getInitials() << endl;
```

将返回：

```
MAB
```

你可以将此定义放在类定义的 public 区域中的任何位置，但这类方法通常放在 get 和 set 方法之后。

```cpp
}
Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}

void setFirst(string firstName)
{
    first = firstName;
}

void setMiddle(string middleName)
{
    middle = middleName;
}

void setLast(string lastName)
{
    last = lastName;
}

void setName(string firstName, string middleName,
             string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

string getFirst()
{
    return first;
}

string getMiddle()
{
    return middle;
}

string getLast()
{
    return last;
}

string getName()
{
    return first + " " + middle + " " + last;
}

string getInitials()
{
    return first.substr(0,1) +
           middle.substr(0,1) +
           last.substr(0,1);
}
};

int main(array<System::String ^> ^args)
{
    Name myName("Mary", "Alice", "Smith");
    cout << myName.getName() << endl;
    // Mary gets married to Joe Brown
    myName.setLast("Brown");
    cout << myName.getName() << endl;
    cout << "The first name in myName is: "
         << myName.getFirst()
         << endl;
    cout << "The middle name in myName is: "
         << myName.getMiddle() << endl;
    cout << "The last name in myName is: "
         << myName.getLast() << endl;
    cout << "myName's initials are: "
         << myName.getInitials() << endl;
    Console::ReadKey();
    return 0;
}
```

```cpp
void setName(string, string, string);
```

编译类时，源文件中的方法定义必须与头文件中的原型完全匹配，否则编译器将报错。

要使用 Visual C++ Express 为 Name 类创建头文件，请在“解决方案资源管理器”窗口中右键单击“头文件”，选择“添加”，然后选择“新建项”。为项类型选择“头文件”，并将其命名为“Name.h”。将出现一个空的代码编辑器窗口，你可以在其中放入头文件代码。

以下是 Name 类的头文件：

```cpp
#include <string>
using namespace std;

class Name
{
private:
    string first, last, middle;

public:
    Name();
    Name(string, string, string);
    Name(string, string);
    Name(string);
    void setFirst(string);
    void setMiddle(string);
    void setLast(string);
    void setName(string, string, string);
    string getFirst();
    string getMiddle();
    string getLast();
    string getName();
    string getInitials();
};
```

尽管头文件中没有可执行代码，但我们仍然需要包含 string 库，因为 string 数据类型在多个地方被提及。

重要的是，源文件中使用的每个成员和方法都必须在头文件中定义，否则编译器在编译该类时将报错。

### 为 Name 类创建源文件

构建头文件后，下一步是构建一个源文件，其中包含类方法的可执行代码定义。要在 Visual C++ Express 中创建源文件，请在“解决方案资源管理器”中右键单击“源文件”，选择“添加”，然后选择“新建项”，并选择“C++ 文件”作为项类型。将文件命名为“Name.cpp”。事实上，源文件的名称必须与头文件的名称完全匹配。

Name 类的源文件看起来几乎与我们上面为类定义构建的内容完全相同。下面列出了 Name 类的源文件，随后解释了这里的代码与上面为 Name 类使用的代码有何不同：

```cpp
#include "stdafx.h"
using namespace System;

#include "Name.h"

Name::Name()
{
    first = "";
    middle = "";
    last = "";
}

Name::Name(string firstName, string middleName,
            string lastName)
{
    first = firstName;
    middle = middleName;
```


```cpp
last = lastName;
}

Name::Name(string firstName, string lastName)
{
    first = firstName;
    middle = "";
    last = lastName;
}

Name::Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}

void Name::setFirst(string firstName)
{
    first = firstName;
}

void Name::setMiddle(string middleName)
{
    middle = middleName;
}

void Name::setLast(string lastName)
{
    last = lastName;
}

void Name::setName(string firstName,
                  string middleName,
                  string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

string Name::getFirst()
{
    return first;
}

string Name::getMiddle()
{
    return middle;
}

string Name::getLast()
{
    return last;
}

string Name::getName()
{
    return first + " " + middle + " " + last;
}

string Name::getInitials()
{
    return first.substr(0,1) + middle.substr(0,1) +
           last.substr(0,1);
}
```

首先要注意的是，我们必须在程序顶部包含头文件。必须告诉编译器在哪里找到后续方法定义的原型。

这个源文件与前面 Name 类的代码之间的主要区别在于，每个方法名前面都有 `Name::`。例如，`getName()` 方法的定义是：

```cpp
string Name::getName()
{
    return first + " " + middle + " " + last;
}
```

在方法名前加上 `Name::` 可以确保编译器正确识别该方法属于 Name 类，而不只是一个未附加到任何特定类的“普通”函数。

`::` 运算符称为作用域解析运算符，在这里它要求运算符左侧是类名，右侧是方法名。像这样定义作用域是必要的，因为我们是在类定义之外定义该类的方法，编译器必须知道这些方法定义属于哪个类。

### 编译 Name 类

尽管我们还没有编写任何实际使用 Name 类的代码，但仍然可以编译该类，以确保一切在语法上正常工作。在 Visual C++ Express 中，单击菜单区域中的 Debug，然后选择 Build Solution。这会编译你的头文件和源文件，并让你知道这两个文件中是否有任何错误。

假设没有任何错误，你就可以进入最后一步——编写一些代码来测试该类。

### 测试 Name 类

我们已经编写了测试 Name 类的代码，但需要演示如何在将 Name 类代码与使用该代码的程序分离的背景下进行测试。我们已经有用于编写测试代码的文件。它是一个源文件，名称与项目名称相同；如果你一直按照上面的讨论操作，项目名称就是“NameTest”。

现在只需添加我们之前用来测试 Name 类第一个实现的代码。代码如下：

```cpp
// NameClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

#include "Name.h"

int main(array<System::String ^> ^args)
{
        Name myName("Mary", "Alice", "Smith");
        cout << myName.getName() << endl;
        // Mary gets married to Joe Brown
        myName.setLast("Brown");
        cout << myName.getName() << endl;
        cout << "The first name in myName is: "
             << myName.getFirst()
             << endl;
        cout << "The middle name in myName is: "
             << myName.getMiddle()
             << endl;
        cout << "The last name in myName is: "
             << myName.getLast()
             << endl;
        cout << "myName's initials are: "
             << myName.getInitials()
             << endl;
        Console::ReadKey();
        return 0;
}
```

### 开发 List 类

Name 类是一个有用的第一个示例，但它并没有展示用类可以做的所有事情。我们需要开发的许多类都要求每个对象存储不止一条数据（比如一个姓名）。一个存储列表的类将展示如何把数据结构纳入类设计中。

#### 创建抽象数据类型

开发类时，在编写任何代码之前，你需要做的第一件事就是仔细思考类的设计。你可以通过问自己几个问题来做到这一点——类中要存储什么数据？需要对数据执行哪些操作？在开始编程之前把这些信息写下来是个不错的主意。

在编程开始之前勾勒出的类称为*抽象数据类型*，简称*ADT*。ADT 会包含诸如类名、类成员列表及它们存储的数据、类方法列表及它们执行的操作等信息。

如果要为 List 类设计 ADT，首先必须决定希望这个类做什么。当然，我们希望该类存储一组项（即列表）。我们希望能够向列表中添加项、显示列表中的项、清空列表并重新开始，以及显示列表中项的数量。对列表还可以做更多事情，但这些操作对于本示例已经足够。（例如，从列表中移除项以及按字母顺序对列表排序涉及高级 C++ 技术，本书没有篇幅讨论。）

我们还需要决定在类中存储什么数据。由于我们正在构建 List 类，因此需要某种能存储数据集合的东西，比如 vector。另一项可能有用的数据是列表中项的数量，即计数。

List 类的 ADT 会列出该 ADT 的每个成员和方法，并描述成员中存储什么数据，或者方法应执行什么操作。下面是 List 类的 ADT：

ADT 名称：List  
ADT 目的：存储相关项

#### ADT 成员

| # | 成员 | 描述 |
|---|---|---|
| 1 | Datastore | 字符串向量 |
| 2 | numItems | 整数 |

#### ADT 方法

| # | 方法 | 描述 |
|---|---|---|
| 1 | Add | 向列表中添加新的字符串项 |
| 2 | Clear | 从列表中移除所有项 |
| 3 | Display | 将列表写成字符串 |
| 4 | Count | 列表中项的数量 |

ADT 描述中可能仍会遗漏一些细节，例如我们究竟如何实现排序方法，但把这些信息写下来的过程会通过将注意力集中在我们知道希望类完成的事情上，帮助我们实际编写类。你会注意到，当需要数据类型时，就提供了一种数据类型。例如，vector 将存储字符串，而 numItems 成员将存储整数。

#### 为 List 类开发代码

现在我们可以直接从 List 类的 ADT 转到编写该类的头文件。如下所示：

```cpp
#include <iostream>
using namespace std;

class List
{
private:
    vector<string> datastore;
    int numItems;
public:
    List();
    void add(string);
    void clear();
    void display();
    int count();
};
```

下一步是编写 List 类源文件的代码。这个类的许多方法几乎与完成该任务所需的 vector 方法相同。例如，`remove()` 方法将调用 vector 的 `erase()` 方法，因此我们真正做的只是把 vector 方法重命名为对列表操作来说更常见的名称。甚至类的一个成员 `numItems`，实际上也只是 vector 的 `size()` 方法的另一个名称。事实上，当我们需要使用 `numItems` 时，我们会通过调用 datastore 向量上的 `size()` 方法来给它的值赋值。否则，我们就必须持续记录添加和移除项的数量，而在代码中这样做容易出错。

下面是 List 类的源文件代码：

```cpp
#include "stdafx.h"
using namespace System;
#include "List.h"

List::List()
{
    vector<string> datastore;
    int numItems = 0;
}

void List::add(string item)
{
    datastore.push_back(item);
}

void List::clear()
{
    datastore.clear();
}
```



```cpp
string List::display()
{
    string items = "";
    for(int i = 0; i < datastore.size(); ++i) {
        items += datastore[i];
        items += " ";
    }
    return items;
}

int List::count()
{
    return datastore.size();
}
```

唯一稍微有点难写的方法是 display() 方法，但这只是遍历 vector、用 vector 的每个元素构建一个字符串而已。主要需要决定的是是否将每个 vector 项放在单独一行。你会注意到，该方法返回一个字符串，而不是直接将各项输出到控制台。对于大多数类似情况，更灵活的决定是将类的内容写入字符串，并让使用该类的程序决定如何最好地呈现信息。如果将数据写入控制台，调用程序也别无选择，只能这样做。将数据作为字符串返回，使调用程序有机会将数据存储在变量中、写入控制台，也许写入文件，或完全用它做其他事情。

在编写测试此实现的代码之前，我们可以通过从“调试”菜单中选择“生成解决方案”来编译该类，以确保语法正确。创建类时，你应该经常生成解决方案，以确保过程中不会犯任何错误。

现在我们需要一个测试程序，以确保 List 类正常工作。我们想通过创建一个项目列表、显示它们、清空该列表、创建新列表，然后显示新列表来测试该类的所有方法。请记住，这段代码应放在与项目同名的源文件中，在本例中是 ListClass.cpp 文件。代码如下：

```cpp
// ListClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

#include "List.h"

int main(array<System::String ^> ^args)
{
    List groceries;
    groceries.add("milk");
    groceries.add("bread");
    groceries.add("eggs");
    cout << "First list: " << endl;
    cout << groceries.display() << endl;
    cout << "Number of items in list: "
         << groceries.count() 
         << endl;
    groceries.clear();
    groceries.add("cereal");
    groceries.add("coffee");
    groceries.add("apples");
    groceries.add("ice cream");
    cout << endl << "Second list: " << endl;
    cout << groceries.display() << endl;
    cout << "Number of items in list: "
         << groceries.count() << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```text
First list:
milk bread eggs
Number of items in list: 3

Second list:
cereal coffee apples ice cream
Number of items in list: 4
```

### 练习

- 1. 创建一个地址簿类，用于存储一个人的姓名、家庭住址和电话号码。确保为该类包含一整套构造函数以及 get 和 set 方法。编写一个程序来测试该类。
- 2. 创建一个 Time 类，以 hh/mm/ss 格式存储时间。至少包含两个构造函数，并为每个数据成员包含 get 和 set 方法。编写一个 increment 方法，将时间推进 1 分钟。如果新的分钟超过 59，则将分钟重置为 0，并将小时加 1。编写一个程序来测试该类，包括 increment 方法。

## 第 12 章：文件输入与输出

到目前为止，我们处理的数据都存储在内存中的变量、vector 或数组中。然而，一旦程序停止运行，这些数据就会从内存中移除。如果希望程序中的数据被永久保存，就必须将数据存储到文件中。本章讨论如何创建文件来保存数据，以及如何使用 C++ 从文件中读取数据。

### 使用文件和流

对 C++ 来说，文件是一个字符（字节）序列，文件末尾由一个特殊的文件结束标记来标识。与控制台输入和输出类似，C++ 将文件与一个流关联起来，该流用于与文件通信。想要读写文件的源文件必须包含头文件 fstream。

通常，在 C++ 中可以处理两种类型的文件：**二进制**文件和**文本**文件。二进制文件也称为*随机存取文件*，在存储空间上比文本文件更高效，但编程难度稍大。文本文件也称为*顺序访问文件*，或简称*顺序文件*，效率较低，但更易于编程，并且可以用标准文本编辑器编辑。本章我们将只处理文本文件。

### 创建文本文件

大多数读者已经知道文本文件是什么样子。你可能已经用记事本或其他文本编辑器创建过文本文件。我们不是从键盘输入文件文本，而是要编写一个 C++ 程序来创建一个存储成绩列表的简单文本文件。

程序的第一步是像前面提到的那样，在程序中包含 fstream 头文件。下一步是创建一个文件对象，表示我们要创建的文件。当我们向控制台写入数据时，使用的是与控制台关联的内置对象 cout。我们可以通过声明一个 ofstream 类型的标识符来为文件创建自己的对象，ofstream 代表“输出流”。我们要创建的文件被视为输出文件。

创建文件对象不仅仅涉及声明该对象。我们还必须指定文件名。为此，我们要给出文件的完整路径，除非文件与程序位于同一目录中。不过这种情况并不常见，因此通常将完整路径作为参数给出。例如，如果我们想把成绩文件存储在根目录下的 data 子目录中，可以用以下语句创建文件对象：

```cpp
ofstream outFile("c:\\data\\grades.txt");
```

注意，路径字符串中每个目录名前面都有两个反斜杠。如果不这样做，C++ 会尝试将单个反斜杠解释为特殊字符，例如表示制表符的“\t”。使用两个反斜杠可确保编译器不会将文件路径字符串的某些部分解释为特殊字符。

这条语句不仅创建文本文件并将该文件与我们的文件对象关联起来，还会打开该文件。因此，文件现在已准备好接收程序写入的数据。要向文件写入数据，请像向 cout 对象发送数据一样，将数据发送到文件对象。下面是一个示例：

```cpp
outFile << 85;
```

字符 8 和 5 会写入文件的前两个位置，因为它们是首先写入文件的字符。如果我们再写一条类似的语句：

```cpp
outFile << 77;
```

字符 77 将紧挨着 85 写入，因此文件看起来像这样：

```text
8577
```

如果希望两个成绩之间有一个空格，或者希望将第二个成绩 77 放在下一行，就必须将空格字符或换行字符写入文件。该语句将是

完成向文件写入数据后，必须关闭文件，以确保数据确实已存储到文件中。执行此操作的语句是：

```cpp
outFile.close();
```

下面是完整的程序，用于将成绩 85 和 77 写入文件，并且每个成绩占一行：

```cpp
// CreateFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ofstream outFile("C:\\data\\grades.txt");
    outFile << 85;
    outFile << endl;
    outFile << 77;
    outFile.close();
    Console::ReadKey();
    return 0;
}
```

更实际的程序会允许用户使用循环将数据输入文件。下面是一个示例：

```cpp
// CreateFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ofstream outFile("C:\\data\\grades.txt");
    int grade;
    cout << "Enter a grade (-1 to quit): ";
    cin >> grade;
    while (grade > -1)
    {
        outFile << grade << endl;
        cout << "Enter a grade (-1 to quit): ";
        cin >> grade;
    }
    outFile.close();
    Console::ReadKey();
}
```


```cpp
return 0;
}
```

要查看文件内容，请打开命令提示符窗口并输入以下命令（同样假设你使用的文件系统结构与我使用的一致）：

```text
type c:\data\grades.txt
```

你应该会看到运行上面的程序时输入到文件中的成绩列表。如果没有看到，请再次运行该程序，并再次输入 type 命令。

### 从文本文件读取数据

我们在第 8 章讨论过从文件读取文本，但既然你现在对 C++ 中文件和流的工作方式有了更多了解，我们将再讲一遍这部分内容。

从文件读取数据的技术类似于我们从控制台读取数据以及之前创建文本文件的方式。我们需要一个文件对象；必须将该对象与一个输入流关联起来，然后把文件中的数据读入一个变量。

为了从文本文件读取数据，我们创建的是用于输入的文件对象，而不是用于输出的文件对象。这意味着我们必须使用 `ifstream` 数据类型，而不是 `ofstream` 数据类型。打开文件用于输入所需的语句如下所示：

```cpp
ifstream inFile("c:\\data\\grades.txt");
```

接下来，你需要创建一个变量来存储所读取的数据。然后可以使用类似下面的语句将文件中的数据读入该变量（这里也包含了变量声明）：

```cpp
int grade;
inFile >> grade;
```

然后，你可以对刚刚读入变量的数据做任何需要做的事情。由于文件中的数据是每行一个成绩，要获取下一个成绩，只需再次使用上面的语句：

```cpp
inFile >> grade;
```

每次从 grades.txt 文件读取一个值时，一个内部指针会自动移动到下一个值，因此当你再次发出输入语句时，新的数据值将被读入变量。如果数据是存储在一行中，而不是分别存储在多行中，我们就必须在每个值之间放置一个空格，以便编译器知道将指针放在哪里以读取下一个值。

你可以继续以这种方式从文件读取数据并将其存储到变量中，直到没有数据可读为止。在程序结束之前，你应该关闭文件，以确保文件不会损坏。我们之前已经见过如何关闭文件：

```cpp
inFile.close();
```

下面是一个从 grades.txt 文件读取并显示前两个成绩的程序：

```cpp
// ReadFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream inFile("c:\\data\\grades.txt");
    int grade;
    inFile >> grade;
    cout << grade << endl;
    inFile >> grade;
    cout << grade << endl;
    inFile.close();
    Console::ReadKey();
    return 0;
}
```

这个程序并不是我们真正需要的、用于正确读取文本文件的程序，因为它假设程序员确切知道文件中有多少数据。请记住，在执行输入语句后，指针会自动放在下一个要读取的数据项处。如果程序试图读取超过文件中最后一个值的内容，就会发出错误，程序将崩溃。为避免这种情况发生，你应该编写使用循环读取数据的程序，并使用一个特殊条件来判断何时到达文件末尾。

从文本文件读取数据时，我们要检查的条件称为 *eof*，它代表文件末尾（end-of-file）。C++ 文件对象有一个名为 eof() 的方法，你可以调用它来判断是否已到达文件末尾。如果已经没有更多数据可读，该方法返回 true；如果还有更多数据可读，则返回 false。

下面是一个程序清单，该程序将读取整个 grades.txt 文件，并使用 eof() 方法显示文件中的每个成绩：

```cpp
// ReadFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream inFile("c:\\data\\grades.txt");
    int grade;
    while (!inFile.eof())
    {
        inFile >> grade;
        cout << grade << endl;
    }
    inFile.close();
    Console::ReadKey();
    return 0;
}
```

请注意，我们使用了 !（非）运算符，因为如果文件中没有更多数据，eof() 方法会返回 true。只要还有更多数据可读，该方法就返回 false，因此我们必须用 ! 运算符对它取反，直到确实没有更多数据可读为止。

现在让我们对这些数据做一些有用的事情，比如计算成绩总和并求出平均值。做法如下：

```cpp
// ReadFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream inFile("c:\\data\\grades.txt");
    int grade, total, numGrades;
    double average;
    total = numGrades = 0;
    while (!inFile.eof())
    {
        inFile >> grade;
        cout << grade << " ";
        total += grade;
        ++numGrades;
    }
    inFile.close();
    average = total / numGrades;
    cout << endl << "The average grade is: "
         << average << endl;
    Console::ReadKey();
    return 0;
}
```

这个程序中你之前没见过的唯一代码是这一行：

```cpp
total = numGrades = 0;
```

与所有其他语句一样，要对其求值，请从右向左进行，因此值 0 被赋给 numGrades，而 numGrades 的值（现在为 0）被赋给 total。像这样的快捷语句如果使程序难以阅读，并不总是一个好主意。不过，这个特定语句足够简单，任何有一点编程知识的人都能理解它在做什么。

### 向文本文件追加数据

假设你有一个包含成绩的数据文件，内容如下：

```text
85
77
75
71
89
91
84
```

后来，你又参加了几次考试，想把这些成绩添加到文件中，以便更新平均分。最简单的方法是打开数据文件并将数据追加到文件中。

C++ 提供了一种通过指定希望处理文件的模式来打开文件以实现该目的的方法。向文件追加数据的模式用常量 `ios::app` 指定。该模式是 open() 方法的一个可选参数。因此，如果我们想打开 grades.txt 文件以向其追加数据，就编写以下语句：

```cpp
ofstream outFile("c:\\data\\grades.txt", ios::app);
```

现在，任何写入文件的新数据都将写在已写入文件的最后一个数据值之后。

下面是一个让我们向 grades.txt 文件添加更多数据的程序：

```cpp
// AppendFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ofstream outFile("c:\\data\\grades.txt",
        ios::app);
    outFile << endl; // next grade on new line
    int grade = 0;
    cout << "Enter a grade (-1 to quit): ";
    cin >> grade;
    while (grade > -1)
    {
        outFile << grade << endl;
        cout << "Enter a grade (-1 to quit): ";
        cin >> grade;
    }
    outFile.close();
    Console::ReadKey();
    return 0;
}
```

你会注意到，在提示用户输入新成绩之前，我们向文件写入了一个换行符。这是因为当文件以追加方式打开时，内部文件指针指向文件中已写入的最后一个成绩之后的位置，并且仍在同一行。换句话说，如果文件中的最后一个成绩是

```text
84
```

那么在追加第一个成绩之后，文件最后一行的内容将如下所示（假设 92 是追加到文件中的第一个成绩）：

```text
8492
```

我们的文件结构设置为每行一个成绩，因此我们需要在添加任何新成绩之前向文件写入一个换行符，这样当 92 写入文件时，它会写在 84 之后的下一行。

### 关于文件模式的简要说明

在上一节中，我们使用了文件模式 `ios::app`，以指定要打开的文件应以追加方式打开。如果我们没有使用该文件模式，open() 方法就会认为我们想要开始一个新文件，编译器会在向文件写入任何新数据之前清空 grades.txt 文件的内容。显然，你必须非常小心文件的打开方式，尤其是在为输出而打开文件时。




### 练习

1. 编写一个程序，允许用户将一组单词输入到文件中。用户完成单词输入后，计算每个单词的长度，并显示文件中单词的平均长度。

2. 编写一个程序，允许用户向练习 1 创建的文件中追加数据，然后在向文件添加新单词后显示单词的平均长度。

## 第 13 章：其他 C++ 控制流结构

C++ 的主要控制流结构包括用于决策的 if 语句、用于重复的 while 和 for 循环，以及用于将代码块视为一个单元的函数。在本章中，我们将考察一些也会修改程序控制流的结构——用于以另一种方式做出决策的 switch 语句，以及用于以另一种方式执行重复的 do-while 循环。

### switch 语句

*switch* 语句提供了一种替代 if 语句的方式，用于根据条件决定执行哪一组语句。对于许多决策而言，switch 语句通常被认为不如 if 语句灵活，因为 switch 语句中测试的条件必须是一个求值为整数值的表达式。在实践中，这意味着要使用 switch 语句，程序必须要求决策基于 int 或 char 类型的表达式。然而，在合适的情况下，switch 语句可能比 if 语句更容易创建、修改和阅读。

#### 编写 switch 语句

switch 语句的一般形式为：

```cpp
switch (expression)
{
    case const-expr:
        set of statements;
        break;
    case const-expr:
        set of statements;
        break;
    ...
    default:
        set of statements;
}
```

如上所述，被测试的表达式必须是整型，通常是整数或字符。分支到一组语句发生在 switch 语句的 case 子句部分。case 子句中的常量表达式（const-expr）会与开头的表达式进行比较。如果比较为真，则执行该子句内的一组语句，然后由于 break 语句，控制权会转移到 switch 语句之外。如果比较为假，控制会落到下一个 case 子句。如果没有执行任何 case 子句，并且存在 default 子句，则执行 default 子句内的语句。

一些示例可能会消除你对 switch 语句工作方式的任何误解。在第一个示例中，输入一个字母等级，并显示该字母等级可能的数值范围：

```cpp
// Switch.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    char letterGrade;
    cout << "Enter your letter grade: ";
    cin >> letterGrade;
    switch (letterGrade)
    {
        case 'A':
            cout << "A grade is in the range of 90-100."
                 << endl;
            break;
        case 'B':
            cout << "B grade is in the range of 80-89."
                 << endl;
            break;
        case 'C':
            cout << "C grade is in the range of 70-79."
                 << endl;
            break;
        case 'D':
            cout << "D grade is in the range of 60-69."
                 << endl;
            break;
        case 'F':
            cout << "An F grade is in the range of 0-59."
                 << endl;
            break;
        default:
            cout << "The letter grade must be A-D,"
                 << " or F." << endl;
    }
    Console::ReadKey();
    return 0;
}
```

现在让我们看一个示例，其中我们让一些 case 子句“贯穿”（fall through）。如果你希望在两个或多个 case 子句为真时执行同一组语句，就可以这样做。继续使用字母等级，下面这个程序根据字母等级判断学生是通过还是未通过测试（A、B、C 和 D 等级都算通过；只有 F 是不及格的等级）：

```cpp
// Switch.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    char letterGrade;
    cout << "Enter your letter grade: ";
    cin >> letterGrade;
    switch (letterGrade)
    {
        case 'A':
        case 'B':
        case 'C':
        case 'D':
            cout << "You passed the test!" << endl;
            break;
        case 'F':
            cout << "Sorry, you failed the test."
                 << endl;
            break;
        default:
            cout << "Enter a valid letter grade."
                 << endl;
    }
    Console::ReadKey();
    return 0;
}
```

当用户输入 A、B、C 或 D 时，编译器会让控制贯穿这些 case 子句，直到遇到可执行语句。该语句被执行，然后由于 break 语句，控制会跳出 switch 语句。如果用户输入 F，只有最后一个 case 子句为真，因此执行其语句，控制会跳出 switch 语句。如果等级不是 A、B、C、D 或 F 中的任何一个，则执行 default 子句。

这里还有一个不涉及测试成绩的示例。这个程序分析一个句子，以确定句子中有多少个元音。它通过循环遍历句子并检查每个字母来实现这一点。我们编写了一个名为 isVowel 的函数，它使用 switch 语句来判断传给该函数的字母是否为元音。在程序末尾，会显示元音的数量。代码如下：

```cpp
// isVowel.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

bool isVowel(char letter)
{
    switch (letter)
    {
        case 'a': case 'A': case 'e': case 'E': case 'i':
        case 'I': case 'o': case 'O': case 'u':
        case 'U':
            return true;
            break;
        default:
            return false;
    }
}

int main(array<System::String ^> ^args)
{
    string sentence;
    char ltr;
    int numVowels = 0;
    cout << "Enter a sentence: ";
    getline(cin, sentence);
    for(int i = 0; i < sentence.size(); ++i)
    {
        ltr = sentence[i];
        if (isVowel(ltr))
            ++numVowels;
    }
    cout << "There are " << numVowels
         << " vowels in the sentence.";
    Console::ReadKey();
    return 0;
}
```

如果我们输入以下句子：

Now is the time for all good people to come to the aid of their party

输出为：

There are 23 vowels in the sentence.

我们在这个程序中运用了一个非常有趣的技巧。我们像遍历数组一样遍历 sentence 变量。我们之所以能这样做，是因为对 C++ 而言，字符串就是数组。在内部，C++ 将字符串存储为 char 值的数组。了解这一点使我们能够轻松地遍历字符串，通过字母在“字符串”数组中的索引位置取出每个字符，并判断该字母是元音还是辅音。在本书后面讨论指针时，我们将进一步探讨如何将字符串视为数组。

由于要求被测试的条件必须是整型表达式，switch 语句不能普遍替代 if 语句。然而，在适用的情况下，switch 语句提供了一种易读、易修改的替代方案。

### do-while 循环

对于 C++ 中的许多重复问题，要测试的条件位于循环的开头，在任何语句执行之前。这在许多情况下是正常的，但有些情况下你可能希望在测试条件之前执行循环体。对于这些情况，C++ 提供了一种替代的重复语句——do-while 循环。

#### 使用 do-while 循环

do-while 循环的一般形式为：

```cpp
do
{
    set of statements;
} while (condition);
```

控制循环的条件位于要执行的语句之后，这保证循环体至少执行一次。while 循环则不是这样：如果在第一次进入循环之前条件不为真，循环根本不会执行。

下面的示例演示了 do-while 循环的实用性。这里有一个简单的加法练习程序，它要求用户解决一个问题，然后询问用户是否想再做一道题：


```cpp
// DoWhile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int op1, op2, result, answer;
    char quit;
    srand(time(NULL));
    op1 = rand() % 100 + 1;
    op2 = rand() % 100 + 1;
    result = op1 + op2;
    cout << "What is " << op1 << " + " << op2 << "? ";
    cin >> answer;
    if (result == answer)
        cout << endl << "Right!";

    else
        cout << "Sorry. That is wrong.";

    cout << "Another problem (y or n)?";
    cin >> quit;
    while (quit != 'n')
    {
        op1 = rand() % 100 + 1;
        op2 = rand() % 100 + 1;
        result = op1 + op2;
        cout << "What is " << op1 << " + " << op2
             << "? ";
        cin >> answer;
        if (result == answer)
            cout << endl << "Right! ";
        else
            cout << "Sorry. That is wrong.";
        cout << " Another problem (y or n)?";
        cin >> quit;
    }
```

```cpp
cout << "Sorry. That is wrong.";
cout << "Another problem (y or n)?";
cin >> quit;
} while (quit != 'n');
cout << endl
     << "Thanks for practicing your addition."
     << endl;
Console::ReadKey();
return 0;
}
```

看看这个程序的第二个版本比第一个版本短了多少。一般来说，大多数提示用户继续或退出的 while 循环都可以用 do-while 循环重写，使程序更短、更容易理解。

事实上，许多使用 while 循环的程序都可以用 do-while 循环重写，尤其是当测试条件可以在进入循环之前设为真时。例如，一个用来确定余额为 5,000 美元的储蓄账户在给定利率下需要多长时间才能累积到 10,000 美元的程序，如果用 while 循环编写，也可以很容易地用 do-while 循环重写。下面是 while 循环版本：

```cpp
// DoWhile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    double balance, rate;
    int years = 0;
    balance = 5000;
    // Enter 1.02 for 2%
    cout << "What is the interest rate? ";
    cin >> rate;
    while (balance < 10000)
    {
        balance *= rate;
        ++years;
    }
    cout << "It will take " << years
         << " to reach $10,000.00." << endl;
    Console::ReadKey();
    return 0;
}
```

下面是使用 do-while 循环重写后的程序：

```cpp
// DoWhile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    double balance, rate;
    int years = 0;
    balance = 5000;
    // Enter 1.02 for 2%
    cout << "What is the interest rate? ";
    cin >> rate;
    do
    {
        balance *= rate;
        ++years;
    } while (balance < 10000);
    cout << "It will take " << years
         << " to reach $10,000.00." << endl;
    Console::ReadKey();
    return 0;
}
```

这两个程序差别很小，尽管两个程序执行结果完全相同，但使用 while 循环版本比使用 do-while 循环版本更可取。

不过，有些情况下你不应该选择 do-while 循环而不选择 while 循环。最常见的情况是处理文本文件中的数据。处理文本文件的循环，其测试条件需要在执行循环中任何读取数据的语句之前，检查文件中是否有数据。试图从空文件中读取数据可能会导致程序崩溃。处理文本文件时始终使用 while 循环。

### 练习

- 1. 使用 switch 语句编写一个程序，允许用户输入月份编号并显示该月份。例如，如果用户输入 5，程序显示 May。

- 2. 下表列出了电话上的字母及其对应的数字。使用 switch 语句编写一个程序，允许用户输入一个字母并显示相应的数字。

| 字母 | 数字 | 字母 | 数字 | 字母 | 数字 | 字母 | 数字 |
| --- | ---: | --- | ---: | --- | ---: | --- | ---: |
| ABC | 2 | DEF | 3 | GHI | 4 | JKL | 5 |
| MNO | 6 | PRS | 7 | TUV | 8 | WXY | 9 |

- 3. 使用 do-while 循环编写一个程序，显示 -40°F 到 40°F 范围内的华氏温度及其对应摄氏温度值的表格。

- 4. 使用 do-while 循环编写一个程序，提示用户输入一个单词，并让程序倒序显示该单词。只使用一个 cin 语句获取用户输入。务必提供一种让程序停止的方法。

## 第 14 章

## 指针

指针是 C++ 语言中一个常被误解的特性。Java 编程语言至少部分是为了解决指针所引发的问题而创造的。不过，有些情况下指针很有用。指针可以像引用一样，用于将变量按引用传递给函数。某些高级数据结构必须用指针实现，尽管也存在基于指针的数据结构的替代方案。本章将介绍指针如何工作，以及为什么有时需要它们。

### 指针的定义

我们可以非常简单地对指针下定义。指针是一个包含另一个变量地址的变量。当我们访问指针的值时，返回的是一个内存地址。声明指针时，在指针变量名前放置一个星号，如下所示：

```
int *pointerVariable;
```

当我们想给指针变量赋一个地址时，要在其地址要赋给指针变量的那个变量前使用引用运算符（&）。例如：

```
int num = 100;
int *ptrNum;
ptrNum = &num;
```

在这个代码片段中，我们将 num 声明为 int 变量并赋值为 100。然后我们将 ptrNum 声明为指针变量，并在最后一条语句中把 num 的地址赋给它。提到 ptrNum 时，程序员通常说 ptrNum 指向 num。

现在，如果我们通过编写以下代码来显示 ptrNum 的值：

```
cout << ptrNum;
```

我们会得到这样的数据：

```
0018ECF8
```

这是一个内存地址。每次执行该语句时，这个值都会变化。

如果我们想查看存储在这个内存地址上的值，也就是我们存储在 num 变量中的值，就必须解引用该指针变量，如下所示：

```
cout << *ptrNum;
```

下面这个完整程序说明了我们到目前为止讨论的内容：

```cpp
// pointerExample1.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
        int num = 100;
        int *ptrNum;
        ptrNum = &num;
        cout << "The memory address of num: "
             << ptrNum << endl;
        cout << "The value stored in num: "
             << *ptrNum << endl;
        Console::ReadKey();
        return 0;
}
```

该程序的输出是：

num 的内存地址是：001CEF98  
num 中存储的值是：100

### 指针与按引用传递

由于指针指向变量的内存地址，因此可以用指针将参数按引用传递给函数。

本书前面已经看到，如何使用引用来创建一个 swap 函数，该函数交换作为参数传给函数的两个变量的值。下面是那个程序：

```cpp
// Swap.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}
```

```cpp
int main(array<System::String ^> ^args)
{
    string word1, word2;
    word1 = "banana";
    word2 = "apple";
    cout << word1 << " " << word2 << endl;
    swap(word1, word2);
    cout << word1 << " " << word2 << endl;
    Console::ReadKey();
    return 0;
}
```

要用指针代替引用，我们只需在 swap 函数的参数列表中将引用运算符（&）换成指针运算符（*），并在函数体代码中使用指针引用，如下所示：

```cpp
void swap(string *word1, string *word2)
{
    string temp;
    temp = *word1;
    *word1 = *word2;
    *word2 = temp;
}
```

运行该程序会得到输出：

```text
banana apple
apple banana
```

下面是使用指针而不是引用重写 swap 函数后的完整程序：


```cpp
// Swap.cpp : main project file.

#include "stdafx.h"

using namespace System;

#include <iostream>
#include <string>
using namespace std;

void swap(string *word1, string *word2)
{
        string temp;
        temp = *word1;
        *word1 = *word2;
        *word2 = temp;
}

int main(array<System::String ^> ^args)
{
        string word1, word2;
        word1 = "banana";
        word2 = "apple";
        cout << word1 << " " << word2 << endl;
        swap(&word1, &word2);
        cout << word1 << " " << word2 << endl;
        Console::ReadKey();
        return 0;
}
```

使用指针进行交换与使用引用进行交换的工作方式相同，因为我们向 swap 函数传递的是内存地址，而不仅仅是变量值的副本。

### 指针和数组

在 C++ 中，指针和数组有着非常紧密的关系。事实上，这种关系如此紧密，以至于数组名可以作为指向数组第一个元素的指针。

首先，让我们看看如何使用标准指针技术创建一个指向数组的指针。下面的程序创建一个包含 100 个随机数的数组，显示数组的第一个元素，初始化一个指向该数组的指针变量，并通过该指针打印数组的第一个元素：

```cpp
// PointersAndArrays.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^>^args)
{
        int nums[100];
        srand(time(NULL));
        const int size = 100;
        for(int i = 0; i < size; ++i)
            nums[i] = rand() % 100 + 1;
        cout << nums[0] << endl;
        int *ptrNums;
        ptrNums = &nums[0];
        cout << *ptrNums;
        Console::ReadKey();
        return 0;
}
```

然而，由于数组名可以作为指向数组的指针，我们不必费心创建指向数组的指针变量。我们可以直接使用数组名作为指针：

```cpp
// PointersAndArrays.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int nums[100];
    srand(time(NULL));
    const int size = 100;
    for (int i = 0; i < size; ++i)
        nums[i] = rand() % 100 + 1;
    cout << nums[0] << endl;
    cout << *nums << endl;
    Console::ReadKey();
    return 0;
}
```

数组名是指向数组第一个元素的指针。我们只需对数组名进行解引用，就可以访问第一个元素。

如果我们想使用指针表示法访问数组的第二个元素，可以这样做：

```cpp
cout << *(nums+1);
```

这里使用括号非常重要。数组名本身是对数组第一个元素的引用。如果我们想要下一个元素（位于位置 1），需要通过写作 `(nums+1)` 来引用该位置。然而，如果没有括号，我们表达的意思是“给我数组中第 0 个位置的元素，并给它加 1。”下面是一个演示这一点的程序：

```cpp
// PointersAndArrays.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int nums[100];
    const int size = 100;
    srand(time(NULL));
    for(int i = 0; i < size; ++i)
        nums[i] = rand() % 100 + 1;
    cout << "The first element: " << *(nums+0) << endl;
    cout << "The second element: " << *(nums+1) << endl;
    cout << "Accessing the second element ";
    cout << " without parentheses: " << *nums+1 << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```text
The first element: 95
The second element: 83
Accessing the second element without parentheses: 96
```

每当需要访问数组元素时，我们都可以使用指针表示法代替下标。下面的程序在前面的示例所使用的数组上演示了这种技术：

```cpp
// PointersAndArrays.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int nums[100];
    const int size = 100;
    srand(time(NULL));
    for(int i = 0; i < size; ++i)
        nums[i] = rand() % 100 + 1;
    for(int i = 0; i < size; ++i)
        cout << nums[i] << " ";
    Console::ReadKey();
    return 0;
}
```

使用指针表示法而不是下标来访问数组通常更高效。然而，指针表示法有时更难阅读，除了特别需要效率的情况外，大多避免使用。

有时使用指针表示法的另一种情况是，将大型数据结构（如向量）用作函数参数。将大型数据结构作为指针或引用传递比按值传递更高效，原因很明显：按值传递时编译器必须复制该数据结构，而按指针或引用传递时，编译器只是将一个内存地址传递给函数。

### 练习

- 1. 使用指针编写一个函数，接受一个字符串作为输入，并判断该字符串是否为回文。编写一个程序测试该函数。
- 2. 使用指针表示法编写一个程序，显示数组中大致位于第一个元素和最后一个元素中间的元素。
- 3. 使用指针表示法，将 10 个随机成绩存储到数组中，并显示这些成绩的平均值。
- 4. 使用指针编写一个函数，接受两个字符串作为输入，并判断这两个字符串是否相等。例如，equal("hello", "hello") 返回 true，但 equal("hello", "Hello") 返回 false。

## 第 15 章：继承与组合

我们在 C++ 中使用面向对象编程的原因之一，是我们想要创建自己的数据类型。在上一章中，我们讨论了如何通过创建一个展现类属性和行为的类来构建 List 数据类型。使用面向对象编程的另一个原因，是能够构建相互依托的数据类型层次结构。这称为*继承*。

使用面向对象编程的另一种方式是创建包含其他类的类。这称为*组合*。例如，一个 College 类可以由 Faculty 类、Student 类和 Staff 类组成。本章讨论如何使用继承和组合构建更有用的类。

### 继承

一个类可以继承另一个类的成员和方法。继承成员和方法的类称为派生类。被继承的类称为基类。

继承用于描述对象之间的*是一种*关系。换句话说，熊是一种哺乳动物；鳟鱼是一种鱼；小说是一种书。这些关系往往以层次结构的方式描述。一个具体示例将有助于解释继承在抽象层面如何工作。

#### 继承示例——车辆

Vehicle 类包含有关车辆的信息。我们将把对车辆的讨论限制在有轮子的车辆上。那么，有轮子的车辆有哪些属性和行为呢？首先，它们有轮子。大多数（但并非所有）有轮子的车辆都有转向机构。大多数都有发动机和制动系统，尽管同样并非全部如此，而且大多数都有某种座位安排。车辆能够移动，也能够停止和转向。

现在我们可以开始考虑从基类 Vehicle 派生出的类。汽车派生自 Vehicle 类，卡车、公交车和火车也是如此，这里仅举几例。它们中的每一个都具有与所有车辆共同的特征，但每一个也有自己独特的特征。

继承的工作方式是：首先定义用于描述基类所有实例的属性和行为，然后从基类派生出在某些方面与基类不同的类。你也可以说，派生类可以展现基类更具体的特征。有轮子的车辆只是有轮子；汽车有四个轮子，摩托车有两个轮子（那些有三个轮子的除外）。

使用继承的优点是，当我们从基类构建派生类时，我们可以选择在派生类中原样使用基类的特性，也可以以某种方式修改它们。我们不必仅仅因为派生类在某种程度上不同于基类就完全从头开始定义。这可以节省大量编程和调试时间，因为一旦某个方法在基类中编写并调试完成，我们就可以在派生类中原样使用它，并确信该方法能按预期工作。




#### 代码中的继承示例

为了演示 C++ 中继承的工作原理，我们将开发一组类，模拟公司中不同类型员工之间的关系。

出于演示目的，我们将定义公司中的三种员工类型——普通员工、主管和经理。我们将让 Employee 类作为基类，Supervisor 类和 Manager 类将作为派生类。

首先，让我们定义 Employee 类。为了避免事情变得过于复杂，我们将所有类定义在同一个程序中。我们不提倡在“真实世界”的程序中这样做，但如果所有类定义都在同一个地方，会让我们的讨论更容易理解。

以下是对 Employee 类进行定义以及测试该实现的测试程序的初步尝试：

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
private:
        string empName;
        double pay;

public:
        Employee(string name, double payRate)
        {
                empName = name;
                pay = payRate;
        }

        string getName()
        {
            return empName;
        }

        double getPay()
        {
            return pay;
        }

        double grossPay(int hours)
        {
            return pay * hours;
        }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName() << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40) << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出是：

```
Employee name: Mary Smith
Pay rate: 15
Gross pay: 600
```

现在我们可以从 Employee 类派生 Manager 类了。当我们从基类派生一个类时，我们只想实现派生类中出现的不同成员和方法，并复用基类中与派生类共享的成员和方法。这意味着我们希望继续在 Manager 类中使用 Employee 类的数据成员，并添加任何不同的属性，例如经理通常是领薪员工而不是计时员工这一事实。我们可以通过包含一个布尔变量 isSalaried 将此事实添加到 Manager 类中，然后调整 grossPay() 方法：如果对象是经理，则返回薪金；如果对象是普通员工，则返回薪金乘以工作小时数。

我们几乎准备好实现 Manager 类了，但有一个主要问题。Employee 类的数据成员是私有成员，这意味着它们的值只能在类定义内部访问。我们可以为基类使用一种访问修饰符，使类的成员和方法可被派生类访问：protected。这种访问修饰符允许派生类访问基类的成员和方法，但不允许任何其他代码（例如测试程序）访问。

一旦我们将基类的成员和方法设为受保护，就必须告诉编译器派生类正在从基类继承成员和方法。为此，在派生类定义的第一行同一行中，写一个冒号，后跟关键字 public 和基类名称，以包含对基类的引用，如下所示：

```cpp
class Manager : public Employee
```

现在我们可以重新定义 Employee 类并定义 Manager 类了。以下是完整程序：

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
protected:
    string empName;
    double pay;

public:
    Employee(string name, double payRate)
    {
        empName = name;
        pay = payRate;
    }

    string getName()
    {
        return empName;
    }

    double getPay()
    {
        return pay;
    }

    double grossPay(int hours)
    {
        return pay * hours;
    }
};

class Manager : public Employee
{
protected:
    bool salaried;

public:
    Manager(string name, double payRate,
            bool isSalaried)
        : Employee(name, payRate)
    {
        salaried = isSalaried;
    }

    bool getSalaried()
    {
        return salaried;
    }

    double grossPay(double hours)
    {
        if (salaried)
            return pay;
        else
            return Employee::grossPay(hours);
    }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName()
         << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40)
         << endl;
    Manager emp2("Liz Warren", 1500, true);
    cout << "Employee name: " << emp2.getName()
         << endl;
    cout << "Pay rate: " << emp2.getPay() << endl;
    cout << "Gross pay: " << emp2.grossPay(40)
         << endl;
    Console::ReadKey();
    return 0;
}
```

我们做的第一个更改是将 Employee 类数据成员的访问修饰符从 private 改为 protected。以下是该部分代码：

```cpp
class Employee
{
protected:
    string empName;
    double pay;
```

必须进行此更改，以便 Manager 类可以访问 Employee 类的数据成员。因此，我们不必在 Manager 类中重新声明 Employee 类的数据成员。

Manager 类的构造函数也利用了继承，它使用 Employee 类定义中的成员赋值来设置员工姓名和员工薪金。让我们只关注构造函数，看看它是如何工作的：

```cpp
Manager(string name, double payRate,
        bool isSalaried)
    : Employee(name, payRate)
{
    salaried = isSalaried;
}
```

构造函数的参数列表包括所有数据成员的参数。然而，在列表之后，有一个冒号，后跟对 Employee 类基类构造函数的调用。可以把它看作函数调用。在代码中的这一点，编译器将控制权转移到为 Employee 类构造函数定义的代码。这是代码复用的经典示例，也是继承最重要的特性之一。没有理由包含以下语句：

```
empName = name;
pay = payRate;
```

因为我们已经在基类中编写了它们。

构造函数体的其余部分将最后一个参数赋给 Manager 类的新数据成员，即布尔数据成员 salaried。

另一段需要解释的代码是 grossPay() 方法。以下是其定义：

```cpp
double grossPay(double hours)
{
    if (salaried)
        return pay;
    else
        return Employee::grossPay(hours);
}
```

此方法首先通过测试 salaried 变量来检查员工是否领取薪金。如果是，该方法只返回 pay 中的值。如果员工不领薪金，则该方法计算总工资。由于我们已经在 Employee 类中执行了此计算，因此没有理由在 Manager 类中重复它。相反，我们只需像这样调用 Employee 类中的该方法：

`Employee::grossPay(hours)`

如果我们只写：

`grossPay(hours)`

编译器会感到困惑并再次调用同一个方法，导致永无止境的递归调用，最终使程序崩溃。此示例演示了在 C++ 中使用继承如何帮助减少必须编写的代码量，从而使代码更易于使用和调试。

### 组合

继承是在派生类中复用基类的代码。*组合* 是在一个类的定义中使用其他类。组合用于描述 *“有一个”* 关系。一条线有一个点（准确地说，是两个点）；一个圆有一个半径；一辆汽车有一个发动机。这些都是一个对象由其他对象组成的例子。

许多看似适合用继承解决的编程问题，实际上用组合解决更好。继承，尤其是涉及长链派生类时，众所周知很难正确实现。



#### 组合示例：Employee 类

定义一名员工有许多属性，例如他或她的姓名、年龄、性别、受雇日期等。其中一些属性可以单独作为类存在，例如姓名和受雇日期。在本节中，我们将构建一个 Employee 类，它由 Name 类和 Date 类的对象组合而成。

我们已经定义了一个 Name 类，因此这里可以直接使用该类的简化版本。在展示 Employee 类的全部代码时，我们会再次列出它。不过，我们还没有 Date 类，所以现在就来定义它。

Date 类的成员肯定包括日、月和年。还有许多其他可能的成员，但我们将定义限制为这三个成员。

这里我们将定义的 Date 类方法仅包括一个构造函数和一个以 mm/dd/yyyy 格式显示日期的方法。我们还可以包含许多其他方法，但这两个方法足以演示如何在类组合示例中使用该类。

以下是 Date 类的代码：

```cpp
class Date
{
private:
    int month, day, year;

public:
    Date()
    {
        month = 0;
        day = 0;
        year = 0;
    }

    Date(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    void setDate(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    string getDate()
    {
        stringstream dt;
        dt << month << "/" << day << "/" << year;
        return dt.str();
    }
};
```

上面的 getDate() 方法需要一些解释。C++ 语言在组合字符串和整数方面做得并不好。编写 getDate() 函数的简单方式是：

```cpp
return month + "/" + day + "/" + year;
```

但这种方法无法编译。最简单的解决方案是使用一种特殊的数据类型 stringstream，它允许你将数据流赋给一个变量，就像将数据流写到控制台一样。然后，你可以将包含月、日和年并用斜杠分隔的数据流写入该变量，再以字符串形式显示 stringstream 变量的值。

现在，我们准备好使用 Date 类和 Name 类来构建 Employee 类了。以下是代码：

```cpp
class Employee
{
private:
    Name empName;
    Date hireDate;

public:
    Employee(string first, string middle,
             string last, int m, int d, int y)
    {
        empName.setName(first, middle, last);
        hireDate.setDate(m, d, y);
    }

    string getEmployee()
    {
        return empName.getName() + "\n" +
               hireDate.getDate() + "\n";
    }
};
```

数据成员由两个对象组成——一个 Name 对象和一个 Date 对象。构造函数必须分别调用 setName 和 setDate 方法，将数据放入这两个数据成员，因为此时无法调用构造函数。getEmployee() 方法只是分别调用 Name 和 Date 对象的相应 get 方法，并加入换行符，使输出更易读。

在面向对象编程中，你会遇到的许多问题，使用组合而不是继承可以更轻松、更高效地解决。组合以与继承大致相同的方式利用代码复用，但不会像继承那样导致令人困惑、低效且可能不正确的代码。还有许多问题也更适合采用组合方案，而不是使用继承的解决方案。

### 练习

- 1. 设计一个 DateBook 类，它由 Name 类和 Date 类组成。编写一个程序来测试该类。确保创建一整套构造函数以及 get 和 set 方法。
- 2. 创建一个 DateTime 类，它组合 Date 类和 Time 类，使得当时间从 23:59 变为 00:00 时，对应的日期增加 1。确保包含构造函数以及 get 和 set 方法。

## 附录 A

### 错误与错误消息

程序中出现错误是不可避免的。初学 C++ 的程序员尤其会在程序中遇到许多错误，但同样真实的是，专家级 C++ 程序员每天也会经历代码中的错误。编程太复杂了，程序员不可能期望不必处理错误。在本附录中，我们讨论你开始学习 C++ 时会遇到的一些常见错误。更重要的是，我们讨论如何解释编译器在代码中发现错误时你将收到的错误消息。

#### 语法错误

你刚开始学习 C++ 编程时最常犯的错误是*语法错误*。语法错误意味着你没有正确地构成 C++ 语句。一种常见语法错误的例子是在语句末尾漏掉分号。下面是一个 C++ 程序，其中一条语句漏掉了分号：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl
    Console::ReadKey();
    return 0;
}
```

运行此程序时，首先会弹出一个消息框，内容为：“存在生成错误。是否要继续并运行上一次成功生成？” 对这个问题你应该回答“否”。

现在查看 Visual C++ Express 底部的“输出”窗口。你将看到以下消息：

```text
1>------ Build started: Project: ErrorHandling.cpp, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(12): error C2143: Syntax error: missing ';' before System::Console::ReadKey
====== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ======
```

输出消息非常清楚地告诉你漏掉了分号，并且给出了编译器最终判定发生错误的行号。它无法告诉你错误在第 11 行，因为它必须等到发现第 12 行的后续代码，才能确定确实需要在第 11 行末尾放置分号。然而，Console::ReadKey() 不能跟在 cout << "Hello, World!" << endl 之后而没有在 endl 后加分号，所以报告了该错误。

另一种常见语法错误是拼错变量名。下面的程序演示了当你错误输入变量名时会发生什么：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2, number3;
    number1 = 12;
    number2 = 23;
    numbre3 = number1 + number2;
    cout << "The sum is: " << number3 << endl;
    Console::ReadKey();
    return 0;
}
```

你可以看到变量 number3 在第 14 行被拼错了。产生的错误消息是：

```text
1>------ Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(14): error C2065: 'numbre3': undeclared identifier
1>------ Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ------
```

这条错误消息更加用户友好，因为它准确报告了拼写错误发生在哪一行以及拼写错误是什么。你只需回到程序并修正错误。

另一种常见语法错误是遗漏——在预处理指令中漏掉一个库。下面的程序忘记包含 <iostream> 库：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl;
    Console::ReadKey();
    return 0;
}
```

编译此程序时得到的错误消息是：

```text
1>----- Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(8): error C2065: 'cout' : undeclared identifier
1>ErrorHandling.cpp(8): error C2065: 'endl' : undeclared identifier
=========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ===========
```

这条错误消息比上一条用处稍小，因为它没有告诉你你做了什么，只是让你知道它无法识别 cout 和 endl。不过，每当你看到这条错误消息，并且错误消息中提到的标识符是系统对象（例如 cout 和 endl）时，你就可以确定自己忘记包含那些对象所在的库了。

当你尝试在程序中使用一个尚未声明的变量时，会出现类似的错误消息：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2;
    number1 = 12;
    number2 = 23;
```



```cpp
number3 = number1 + number2;
cout << "The sum is " << number3 << endl;
Console::ReadKey();
return 0;
}
```

该程序会导致显示一条类似的错误消息：

```text
1>------ Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>  ErrorHandling.cpp
1>ErrorHandling.cpp(14): error C2065: 'number3': undeclared identifier
1>ErrorHandling.cpp(15): error C2065: 'number3': undeclared identifier
========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ==========
```

不过，这次错误消息并不是因为漏掉了某个库，而是因为程序忘记声明变量 number3。注意，错误消息中变量被使用的两处都被列为错误，而不仅仅是第一次出现的位置。

当然，你可能还会犯其他语法错误，但我们刚才讨论的错误是你可能遇到的三种较为常见的错误。通过讨论错误消息的样子以及如何解读它们，你现在至少应该不会像以前那样被未来可能遇到的新错误消息吓到了。

#### 逻辑错误

一旦程序能够编译并运行，出现的任何错误都可以称为*逻辑错误*，即程序逻辑中的错误。逻辑错误比语法错误难找得多，因为计算机程序只会执行程序员告诉它做的事情，而不会多做任何事。程序无法理解程序员在编写代码时想要做什么，它只能依次执行遇到的语句。

逻辑错误形形色色，我们只能举几个例子来说明逻辑错误与语法错误有何不同。下面的程序显示了数字数组中最后一个元素：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int size = 10;
    int numbers[size];
    for(int i = 0; i < size; ++i)
        numbers[i] = i + 1;
    cout << "The last item in the array is: "
         << numbers[size] << endl;
    Console::ReadKey();
    return 0;
}
```

你能找出错误吗？如果找不到，你觉得输出应该是什么？现在，运行程序看看实际输出是什么：

The last item in the array is -1231954775

但你可能认为最后一项应该是 10。

如果仔细查看代码，会发现 cout 语句中使用了常量 size，而 size 的值为 10。然而，数组的上界是 9，因此用于显示最后一个数组元素的下标应该是 size - 1。

这就是逻辑错误的一个例子。程序运行正确，但输出不符合预期。通常，找到逻辑错误的唯一方法是审查代码，仔细查找编程中可能出错的地方。

再举一个例子：你需要编写一个程序来查找文件中存储的一组数字的最大值。在声明用于存储最大值的变量的那一行，你将其初始化为 0。运行程序后，它报告最大值为 0。嗯？你挠了一会儿头，然后去查看数据文件，发现文件中的所有数字都是负数。显然，当 max 等于 0 时，没有任何值能通过测试 (currentValue > max)，因此按照程序的逻辑，0 就是最大值。

查找这类错误既是一门科学，也是一门艺术。你必须仔细地逐行检查程序，并且必须透彻理解程序所处理的数据。经验是查找错误的最佳老师。你拥有的经验越多，你就能做得越好。只要你继续编写程序，你就会从错误中积累经验。

## 索引

- `-` 运算符，24
- `--` 运算符，29
- `-=` 运算符，30
- `!` 运算符，48, 49, 69, 174
- `!=` 运算符，47
- `*` 运算符，24
- `*=` 运算符，30
- `/` 运算符，24
- `/=` 运算符，30
- `\n`（换行），44
- `\t` 字符，82, 168
- `&` 运算符，105, 119, 192
- `&&` 运算符，48, 58-60
- `%`（取模）运算符，24
- `%=` 运算符，30
- `+` 运算符，24
- `++` 运算符，28-29
- `+=` 运算符，30
- `<` 运算符，47
- `<<` 运算符，16, 43-45
- `<=` 运算符，47
- `==` 运算符，47
- `>` 运算符，47
- `>=` 运算符，47
- `>>` 运算符，41-43
- `||` 运算符，48-49, 60-61
- 抽象数据类型，161-162
- 访问修饰符，140
- 与真值表，48
- 尖括号 (<>)，85
- 追加模式，176
- 算术运算符，24-27
- 数组声明，123-124
- 数组元素访问，127
- 数组索引，122-123
- 数组初始化，124-127
- 数组初始化器，126
- 数组上界，123
- 基类，202
- 二进制文件，167
- 二元运算符，47
- 块作用域，113-116
- 块，15
- 布尔数据类型，19
- 字符数据类型，19
- cin，41-43
- 类编译，159
- 类构造函数，144-147
- 类数据成员，139-140
- 类 get 方法，148-149
- 类头文件，154-156
- 类对象，138-139
- 类 set 方法，147-148
- 类源文件，158-159
- 类测试，159-160
- 类，138-166
- close()，70
- compare()，78
- 复合赋值运算符，30
- 组合，202, 210-213
- Console 类，15
- Console::ReadKey()，16
- 常量，22
- cout，15, 43-45
- cstdlib 库，91
- ctime 库，91
- 花括号 ({ })，15
- 数据成员，定义，139
- 声明语句，19
- 递减运算符，29-30
- 默认构造函数，145-146
- 派生类，202
- do-while 循环，185-190
- 双精度数据类型，19
- endl，13
- eof()，69, 173
- 错误，215-221
- 函数求值，97
- 文件追加，175-177
- 文件输入和输出，167-177
- 文件模式，177
- for 循环，75-82
- fstream，167
- 函数实参，97
- 函数体，96
- 函数调用，97
- 函数形参，96
- 函数，优点，101
- 函数，94-121
- getline()，42
- 全局作用域，111-113
- has-a 关系，210
- 头文件，14
- if 语句，46
- if-else if 语句，54-60
- if-else 语句，50-54
- ifstream，68, 171
- 递增运算符，28-29
- 索引位置，84, 122
- 继承，202-210
- 内层循环，81
- 实例（对象），142
- 整型数据类型，19
- iostream 库，15
- is-a 关系，202
- 局部作用域，111, 113
- 逻辑错误，219-221
- 逻辑运算符，48-49
- 循环控制变量，76
- main 函数，15
- 方法重载，146
- 方法原型，154-155
- 命名空间，15
- 嵌套 for 循环，80-82
- 面向对象编程，138
- ofstream，68, 168
- 一维数组，122-130
- open()，68
- 运算符优先级，25
- 或真值表，49
- 外层循环，81
- 参数列表，95
- 参数传递，105
- 按引用传递，105-108
- 按值传递，103-105
- 指针定义，192
- 指针解引用，193
- 按引用传递指针，194-196
- 指针与数组，197-200
- 指针与数据结构，192
- 指针，192-200
- 预处理器指令，14
- 预读，74
- 私有访问修饰符，139-140
- 受保护访问修饰符，206
- 公有访问修饰符，139-140
- push_back()，86
- RAND_MAX，89
- rand()，89
- 随机数生成，89-92
- 关系表达式，46-47
- 关系运算符，47
- return 语句，16, 96
- 作用域解析运算符 (::)，159
- 设置 rand() 函数种子，89
- 哨兵控制循环，67, 72-74
- 顺序文件，167
- sizeof()，87
- srand()，89
- 语句，16
- std 命名空间，15
- stdafx.h，15
- 字符串数据类型，19
- 子程序，94, 102
- substr()，60, 78
- switch case 子句，180
- switch 语句，179-185
- 语法错误，215-219
- System 命名空间，15
- 文本文件，从中读取数据，67-72
- 文本文件，167
- time()，91
- 二维数组
  - 声明，130-131
- 二维数组
  - 初始化，131
- 二维数组，130-136
- 类型转换，72
- 返回值函数，95-101
- 变量初始化器，21
- 变量作用域，108-116
- 变量，19-21
- vector 类预处理器
  - 指令，85
- vector，84-92
- vector 作为函数实参，116-121
- Visual C++ 2010 Express，12
- void 函数，102-103
- while 循环，64-74




![](img/674eb91f423b4ce95fc29b249543e101_230_0.png)

# C++ 编程：入门指南

## 面向初学者的清晰简洁 C++ 编程学习指南

本书网站：www.techbookspress.com 提供更多学习 C++ 的资源，包括视频、本书源代码以及更多编程示例。


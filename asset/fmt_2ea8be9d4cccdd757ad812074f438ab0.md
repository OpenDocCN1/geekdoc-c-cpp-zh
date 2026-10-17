
关键字 `void` 用于指定不返回任何值的函数的返回类型。此类函数使用形式为 `function_Name(argument_list);` 的语句调用。

能够定义函数是编程中的一种强大工具。如果某个问题需要对该问题中的某个项目应用 C++ 中未提供的操作，我们只需

1. 定义一个函数来执行该操作，并且

2. 将该函数应用于该项目

就像我们对温度转换操作 `celsiusToFahrenheit()` 所做的那样。此外，正如我们在下一节中将看到的那样，此类函数随后可以存储在库中，在需要时从中检索。

## 6.4 库简介

我们已经看到，如果某个问题需要某种新操作，我们可以定义一个函数来执行它，然后像它在 C++ 中提供一样调用它。从本质上讲，我们正在扩展 C++ 的操作集合。然而，尽管这种程序员定义的函数比仅使用表达式提供了显著的改进，但它们本身并不能使重用我们的工作变得容易。例如，要在另一个程序中使用示例 6.2 中的 `celsiusToFahrenheit()` 函数，我们必须从该程序中复制其原型和定义，并将其插入到新程序的适当位置。我们可能会使用文本编辑器或文字处理器的复制和粘贴功能来执行此操作，或者我们可能只需复制示例 6.2 中的程序，删除 `celsiusToFahrenheit()` 的原型和定义之间的所有内容，然后在该原型和定义之间编写新程序。

为了促进可重用性，C++ 的父语言 C 提供了几个标准库，它们只是包含可以由不同程序和其他库共享的项目的文件。例如，我们已经使用 C 的标准库 `cmath` 中的函数 `pow()` 来计算幂，并且在前一章中我们使用了 C 的 `cassert` 库中的 `assert()` 函数来检查某些条件是否为真。要使用其中一个函数，例如 `pow()`，我们只需将库包含在程序中：

```
#include <cmath>
```

C 的库以及 C++ 中添加的库，其中一些在附录 D 中描述，是使这些编程语言如此强大的功能之一，因为它们使在不同程序之间共享常用函数成为可能。本节简要描述了如何构建此类库以及如何构建我们自己的库。

### 6.4.1 构建库

如果我们检查标准库，我们会发现每个库的内容在某种程度上是相关的。因此，具有组织原则是构建库的第一步，这样我们就知道它应该包含什么样的内容。例如，`cmath` 库包含有用的数学函数，而 `iostream` 库包含与输入和输出流相关的项目。因此，如果我们打算将温度转换函数 `celsiusToFahrenheit()` 存储在库中，我们可能会决定它应该包含以某种方式与热量和温度相关的项目，并将库命名为 Heat。

一旦我们有了组织原则，我们必须决定将什么项目放入我们的库中。例如，如果我们的 Heat 库要包含我们的 `celsiusToFahrenheit()` 函数，那么它还应包括用于华氏度到摄氏度转换的逆操作。我们还可能包括将温度从每个刻度转换为开尔文并返回的函数。通过仔细规划并预测哪些项目可能最有用，我们希望开发一个长期有用而不是短期的库。

尽管我们的示例仅为函数，但库还可能包含其他项目。例如，我们可能还想在库中包含重要的与热量相关的常量，例如绝对零（开尔文刻度上的 0K）、水的熔解热（79.71 卡路里/克）和水的汽化热（539.55 卡路里/克）。需要记住的重要一点是，项目应与库的组织原则一致，并且对用户有用（从而避免不得不“重新发明轮子”）。

一旦确定了库的内容，我们就可以开始构建它。库是一组文件：

- 一个 `头文件`，其中包含库中项目的 `声明` 和 `原型`，并使用 `#include` 指令插入到程序（或另一个库）中。它充当库与使用它的程序之间的 `接口`，因此有时也称为库的 `接口文件`。

- 一个 `实现文件`，其中包含未在头文件中定义项目的 `定义`。它必须单独编译，然后链接到需要访问其内容的程序（将在本节后面描述）。

- 一个 `文档文件`，其中包含库中项目的 `文档`。

7 一种替代方法是记录头文件中的每个项目。然而，这确实会使头文件变得杂乱并降低其整体可读性，因此我们将把此文档放在单独的文件中。

## 示例 6.8 库 Heat 的实现文件

```
/* Heat.cpp provides the function implementations for Heat, a
library of heat-related constants and functions.

Created by: Jane Doe, January, 2012, at Dooflingy Engineering.
Modification History: Kelvin items added February, 2012 -- JD.
---------------------------------------------------------------*/

#include "Heat.h"

double celsiusToFahrenheit(double tempCels)
{
    return 1.8 * tempCels + 32;
}

double fahrenheitToCelsius(double tempFahr)
{
    return (tempFahr - 32) / 1.8;
}

// . . . Definitions of other functions omitted to save space . . .
```

需要注意的是，与头文件不同，库的实现文件必须被编译，因此其名称 `Heat.cpp` 具有与我们在前几章中考虑的源文件相同的扩展名 `.cpp`。还请注意，此实现文件包含行

```
#include "Heat.h"
```

除了各种温度相关函数的定义之外。在编译实现文件中的代码之前，编译器将在实现文件的开头插入头文件中的函数原型。这使它能够检查函数原型和定义是否一致。如果检测到不一致，将显示错误消息以提醒我们该问题。

需要注意的是：

- 实现文件中定义了头文件中声明的项目的项目，可以在任何使用 `(i)` `#include` 指令插入头文件，并且 `(ii)` 链接到实现文件的程序中访问。

- 除了头文件中声明的函数的定义之外，实现文件还可以使用未在头文件中声明的其他项目——常量、变量、函数——。此类项目甚至不能被包含头文件的程序在实现文件之外访问。

简单来说，头文件中声明的项可以看作是 `公共` 信息，而实现文件中声明的项在库内部是 `私有` 的。

### 6.4.1.3 构建文档文件

顾名思义，文档文件向库的用户提供关于库中各项的信息。在本文中，我们将其构建为头文件的一个副本，但附加文档注释，描述每个对象并提供每个函数原型的规范。示例 6.9 展示了库 Heat 的文档文件的一部分。我们将其命名为 `Heat.txt`，因为它是文本文档，但其他扩展名如 `.doc` 也同样合适。

### 示例 6.9 库 Heat 的文档文件

```
/* Heat.txt provides the documentation for Heat, a library of
heat-related constants and functions.

Created by: Jane Doe, January, 2012, at Dooflingy Engineering.
Modification History: Kelvin items added February, 2012 -- JD.
-------------------------------------------------------------------*/

// Absolute zero on the Kelvin scale
const double KELVIN_ABSOLUTE_ZERO = 0;          // absolute 0 Kelvin

// The amount of heat needed to change water from liquid to solid
const double HEAT_OF_FUSION = 79.71;            // calories per gram

// The amount of heat needed to change water from liquid to gas
const double HEAT_OF_VAPORIZATION = 539.55;     // calories per gram

/* celsiusToFahrenheit converts a temperature from Celsius
to Fahrenheit.

Receive: A Celsius temperature
Return: The equivalent Fahrenheit temperature
-------------------------------------------------------------------*/
double celsiusToFahrenheit(double tempCels);

/* fahrenheitToCelsius converts a temperature from Fahrenheit
to Celsius.

Receive: A Fahrenheit temperature
Return: The equivalent Celsius temperature
-------------------------------------------------------------------*/
double fahrenheitToCelsius(double tempFahr);

// . . . Other functions omitted to save space . . .
```

这样的文档文件还有一个次要目的：作为头文件的带注释副本，充当头文件的 `备份`。

## 6.4.2 在程序中使用库

一旦我们构建了库 Heat，就可以在类似示例 6.10 的程序中使用它来解决温度转换问题。

### 示例 6.10 使用库进行温度转换

```cpp
/* This program converts temperatures from Celsius to Fahrenheit, using
   function fahrenheitToCelsius() that is stored in library Heat.

   Input:  tempFahrenheit
   Output: tempCelsius
---------------------------------------------------------------*/

#include <iostream>              //cin, cout, <<, >>
using namespace std;
#include "Heat.h"                 // our library's header file

int main()
{
   cout << "Program to convert Celsius temperatures to Fahrenheit.\n";

   double tempCelsius,        // Celsius temperature
          tempFahrenheit;      // Fahrenheit temperature

   cout << "\nEnter a Celsius temperature (< -273.15 to stop): ";
   cin >> tempCelsius;
   while (tempCelsius >= -273.15)
   {
      tempFahrenheit = 1.8 * tempCelsius + 32;

      cout << tempCelsius << " degrees Celsius is equivalent to "
           << tempFahrenheit << " degrees Fahrenheit\n";
      cout << "\nEnter a Celsius temperature (< -273.15 to stop): ";
      cin >> tempCelsius;
   }
}
```

该程序的执行方式与示例 6.2 中的相同。然而，在这个程序中，主函数之前的 `celsiusToFahrenheit()` 原型已被以下行替换：

```
#include "Heat.h"
```

并且 `celsiusToFahrenheit()` 的定义不再存在。该文件中没有给出 `celsiusToFahrenheit()` 的原型和定义，因为原型位于库 Heat 的头文件中，定义位于库的实现文件中。

重要的是注意并理解 C++ 标准库之一的 `#include` 指令与用于包含程序员自定义库的 `#include` 指令之间的区别，例如

```
#include <iostream>
```

以及用于包含程序员自定义库的指令，例如

```
#include "Heat.h"
```

在第一种情况下，库名被尖括号（`<` 和 `>`）包围，C++ 编译器将在特殊的系统包含目录中搜索它。相比之下，如果库的头文件名用双引号括起来，C++ 编译器将在包含正在编译的源文件的目录中搜索它。⁹

## 6.4.3 转换库

程序的转换由两个独立步骤组成：

- 1. `编译`：将源程序转换为等效的机器语言程序，称为 `目标程序`，存储在 `目标文件` 中。如果程序使用程序员自定义库，该库也必须被编译并存储在单独的目标文件中。

- 2. `链接`：将程序中对库函数的调用与库中的函数定义进行链接，生成 `可执行程序`。

下图说明了这一过程：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_189_0.png)

⁹ C++ 还允许程序员将库存储在不同的目录中（例如，库目录），然后指示编译器在查找由 `#include` 指令指定的文件时搜索该目录。具体做法因系统而异。

单独编译库可以显著减少包含库的源程序的转换时间，因为库不需要重新编译，只需与程序的目标文件链接。此外，在转换中检测到的任何错误很可能位于源程序中（因为库已经编译过）。

转换的具体执行方式因系统而异，但有两种基本方法。在诸如 Visual C++ 的集成开发环境中，转换通过创建项目并向其中添加源文件和库文件来协调。然后可以使用菜单选择来执行编译和链接，生成二进制可执行文件并执行它。在命令行环境中，用户通过键入命令与计算机交互。例如，在 Unix/Linux 系统上使用 GNU C++ 时，编译和链接示例 6.10 中的源代码和 `Heat.cpp` 需要几条命令。我们首先输入命令来分别编译源文件和库的实现文件：

```
g++ -c example6-10.cpp
g++ -c Heat.cpp
```

生成目标文件 `example6-10.o` 和 `Heat.o`。然后我们使用以下命令将这两个目标文件链接在一起，生成名为 `example6-10.exe` 的二进制可执行文件：

```
g++ example6-10.o Heat.o -o example6-10.exe
```

要执行生成的文件，我们只需将其名称作为命令键入：

```
example6-10.exe
```

## 6.4.4 以对象为中心的设计：整合函数和库

到目前为止，我们一直在使用以对象为中心的设计（OCD）来设计问题的软件解决方案，其步骤如下：（1）描述程序的行为；（2）识别问题的对象；（3）识别所需操作；（4）以解决问题的方式安排它们。现在我们来考虑如何将函数和库整合到 OCD 中。

由于函数可以被视为添加到 C++ 所提供操作中的操作，它们自然地契合了 OCD 的这一部分：

识别解决问题所需的操作。

如果某个操作不是 C++ 提供的，则编写一个函数来实现它；如果它看起来可能在其它问题中可复用，则将其存储在库中。

## 6.4.5 使用库的好处

我们以描述库的一些主要特性和好处来结束对库的讨论，这些特性和好处使它们在面向对象的编程方法中如此重要。

### 6.4.5.1 库隐藏实现细节

在我们的程序中，我们可以使用库中的项，而无需关心它们在实现文件中是如何定义的。我们所需要的只是头文件中的信息。

`header` 和文档文件，以及由编译实现文件生成的对象文件的访问权限，以便将其内容链接到我们的程序中。实现文件中的细节可以保持“隐藏”，使我们能够使用库而无需关心这些细节。例如，我们在每个程序中都使用了 `iostream` 库提供的输入/输出操作，而无需关心其实现细节。

### 6.4.5.2 库促进程序维护

程序和库的单独编译使得可以更改库的实现文件并仅重新编译它，而无需更改或重新编译使用该库的程序或其他库。例如，如果库 Heat 的实现文件中的函数 `celsiusToFahrenheit()` 被更改，则只需重新编译实现文件即可。使用此函数的程序无需重新编译，因为 `celsiusToFahrenheit()` 的原型未发生变化，只有其定义发生了变化。只需将程序重新链接到库 Heat 的新对象文件即可。

相比之下，如果头文件中的接口被更改，则库的实现文件以及所有在 `#include` 指令中命名该头文件的程序和其他库都必须重新编译并重新链接。

### 6.4.5.3 库支持独立编码

库通过允许将相关项分组到独立单元中来促进软件设计的模块化，这在大型软件项目中尤其有用。一旦在项目中识别并对所需的对象和操作进行分类，就可以设计库来容纳各种对象类型的项，并为这些库构建头文件。

在此之后，项目的工作可以分给不同的程序员组，分别负责构建各种库的实现文件，以及负责在软件项目中使用库的程序的其他组。将工作划分为可管理的“块”并可并行编码，可以加快整个项目的完成速度。此外，由于一个部分的工作独立于另一部分的工作进行，因此出错的可能性更小。

### 6.4.5.4 库简化测试

单独的库可以由不同的程序员团队独立开发和测试（使用驱动程序）。这意味着每个库可以比单个非常大的程序更彻底（并且更快速）地进行测试。

### 6.4.5.5 库扩展编程语言

库提供可供任何程序（或其他库）使用的项——函数、常量等。程序员不必每次需要这些项时都“重新发明轮子”。

## 6.5 数值方法简介

科学和工程中的问题和数学模型，以及许多其他领域，都涉及求解常微分代数方程、微分方程、方程组等。在许多情况下，使用可由计算机程序实现的数值方法来寻找解。以下是数值方法常规使用的一些主要问题类型：

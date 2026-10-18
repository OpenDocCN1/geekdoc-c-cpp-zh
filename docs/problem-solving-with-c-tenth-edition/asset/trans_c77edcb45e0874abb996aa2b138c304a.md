

- 5. 编写一个程序，从键盘输入一个字符，然后输出由该字符组成的大写字母“C”。例如，如果用户输入字符“X”，则输出应如下所示：

```text
    X X X
  X     X
X
X
X
X
X
  X     X
    X X X
```

> 不要想象你知道什么是计算机终端。计算机终端并不是某种笨重的老式电视机前面放着一台打字机。它是一个接口，在那里思想和身体可以与宇宙连接并移动其中的比特。
> 
> DOUGLAS ADAMS, Mostly Harmless (the fifth volume in The Hitchhiker's Trilogy)

## INTRODUCTION

在本章中，我们解释了一些额外的 C++ 示例程序，并提供了足够详细的 C++ 语言介绍，以便你能够编写简单的 C++ 程序。

## PREREQUISITES

在第 1 章中，我们给出了一个示例 C++ 程序的简要描述。 （如果你尚未阅读该程序的描述，在阅读本章之前阅读它可能会有所帮助。）

## 2.1 VARIABLES AND ASSIGNMENTS

> 一旦一个人理解了编程中使用变量的方式，他就理解了编程的精髓。
> 
> E. W. DIJKSTRA, Notes on Structured Programming

程序操作诸如数字和字母这样的数据。C++ 和大多数其他常见编程语言使用称为变量的编程构造来命名和存储数据。变量是像 C++ 这样编程语言的核心所在，因此我们从对 C++ 的描述开始于此。我们将使用第 2.1 节显示的程序进行讨论，并解释该程序中的所有项目。虽然该程序的总体思路应该很清楚，但其中一些细节是新的，需要一些解释。

### Variables

C++ 变量可以保存数字或其他类型的数据。就目前而言，我们将注意力限制在只保存数字的变量上。这些变量就像小黑板，数字可以写在上面。就像写在黑板上的数字可以改变一样，C++ 变量保存的数字也可以改变。与可能完全不包含数字的黑板不同，C++ 变量保证其中有某个值，即使是一些先前运行的程序留在计算机内存中的垃圾数字。

**Display 2.1 A C++ Program (part 2 of 2)**

```text
23  cout << "Then press return.\n";
24  cin >> numberOfBars;
25  cin >> oneWeight;
26
27  totalWeight = oneWeight * numberOfBars;
28
29  cout << numberOfBars << " candy bars\n";
30  cout << oneWeight << " ounces each\n";
31  cout << "Total weight is " << totalWeight << " ounces.\n";
32
33  cout << "Perhaps an apple would be healthier.\n";
34
35  return 0;
36  }
```

**Sample Dialogue**

```text
Enter the number of candy bars in a package and the weight in ounces of one candy bar.
Then press return.
11 2.1
11 candy bars
2.1 ounces each
Total weight is 23.1 ounces.
Try another brand.
Enter the number of candy bars in a package and the weight in ounces of one candy bar.
Then press return.
12 1.8
12 candy bars
1.8 ounces each
Total weight is 21.6 ounces.
Perhaps an apple would be healthier.
```

### Names: Identifiers

你可能会注意到，我们示例程序中变量的名称比数学课上通常使用的变量名称要长。为了使你的程序易于理解，你应该始终为变量使用有意义的名称。变量（或程序中可能定义的其它项目）的名称称为标识符。

### Cannot Get Programs to Run?

如果你无法让你的 C++ 程序编译和运行，请阅读第 1 章中题为“Getting Your Program to Run”的编程提示。该部分提供了处理 C++ 编译器和 C++ 环境差异的提示。

标识符必须以字母或下划线符号开头，其余所有字符必须是字母、数字或下划线符号。例如，以下都是有效的标识符：

```text
x x1 x_1 _abc ABC123z7 sum RATE count data2 Big_Bonus
```

所有上述名称都是合法的，编译器会接受它们，但前五个是标识符的糟糕选择，因为它们不能描述标识符的用途。以下都不是合法标识符，编译器会拒绝它们：

```text
12 3X %change data-1 myfirst.c PROG.CPP
```

前三个不允许，因为它们不是以字母或下划线开头。后三个不是标识符，因为它们包含除字母、数字和下划线符号以外的符号。

C++ 是区分大小写的语言；也就是说，它在标识符的拼写中区分大写和小写字母。因此，以下是三个不同的标识符，可以用来命名三个不同的变量：

```text
rate RATE Rate
```

然而，在同一个程序中使用两种这样的变体并不是一个好主意，因为这可能会令人困惑。虽然 C++ 并未强制要求，但变量通常使用全小写字母拼写。预定义的标识符，如 `main`、`cin`、`cout` 等，必须使用全小写字母拼写。我们将在本章后面看到使用大写字母拼写的标识符的用途。

C++ 标识符可以是任意长度，尽管某些编译器会忽略指定且通常较大的初始字符数之后的所有字符。

### Identifiers

标识符用作 C++ 程序中变量和其他项目的名称。标识符必须以字母或下划线符号开头，其余字符必须全部是字母、数字或下划线符号。

### Variable Declarations

所有变量必须在使用前声明。变量声明的语法如下：

**SYNTAX**

```cpp
Type_Name variableName1, variableName2, ...;
```

**EXAMPLES**

```cpp
int count, numberOfDragons, numberOfTrolls;
double distance;
```

### Naming Conventions

命名约定是用于命名变量等标识符的规则集。在本书中，我们使用变量以小写字母开头的约定。复合词或短语被挤在一起，下一个词的首字母大写。这种约定称为驼峰式或驼峰命名法。其他命名约定，例如 C 风格约定，使用下划线分隔单词，而其他命名约定则在变量名中标识变量类型。

变量声明提供了编译器实现变量所需的信息。回想一下，编译器将变量实现为内存位置，变量的值存储在分配给该变量的内存位置中。值被编码为 0 和 1 的字符串。不同类型的变量需要不同大小的内存位置，以及将它们的值编码为 0 和 1 字符串的不同方法。计算机使用一种代码将整数编码为 0 和 1 的字符串。它使用不同的代码对具有小数部分的数字进行编码。它使用另一种代码将字母编码为 0 和 1 的字符串。变量声明告诉编译器——最终告诉计算机——为变量使用多大的内存位置，以及在将变量的值表示为 0 和 1 的字符串时使用哪种代码。

在赋值语句中，等号右侧的表达式可以仅仅是另一个变量。语句

```cpp
totalWeight = oneWeight;
```

会更改变量 totalWeight 的值，使其与变量 oneWeight 相同。如果你将此语句用于第 2.1 节显示的程序中，它会给出包裹的总重量过低的错误值（假设包裹中有不止一块糖果棒），但在某些其他程序中它可能有意义。

另一个例子，以下赋值语句将 numberOfBars 的值更改为 37：

```cpp
numberOfBars = 37;
```

像此示例中的 37 这样的数字称为常量，因为与变量不同，其值不能更改。

由于变量的值会随时间变化，并且赋值运算符是更改其值的一种方式，因此赋值语句的含义中包含时间因素。首先，评估等号右侧的表达式。之后，等号左侧变量的值被更改为从该表达式获得的值。这意味着变量可以在赋值运算符的两侧有意义地出现。例如，考虑赋值语句

```cpp
numberOfBars = numberOfBars + 3;
```

这个赋值语句乍一看可能很奇怪。如果你把它读成英语句子，它似乎在说“numberOfBars 等于 numberOfBars 加三。”它似乎是这样说的，但它真正的意思是“使 numberOfBars 的新值等于 numberOfBars 的旧值加三。”C++ 中的等号使用方式与英语或简单数学中的使用方式不同。

### Assignment Statements

在赋值语句中，首先评估等号右侧的表达式，然后将等号左侧的变量设置为此值。

**SYNTAX**

```cpp
Variable = Expression;
```

**EXAMPLES**

```cpp
distance = rate * time;
count = count + 2;
```


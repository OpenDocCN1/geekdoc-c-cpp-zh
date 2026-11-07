
```cpp
int main ()
{
    bool truth = true;
    bool lie = false;
    bool result = truth + lie;
    cout << result;
    return 0;
}
```

**PR-15.** 列出下列程序中的所有关键字。

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int x = 0;
    int y = 1;
    cout << x << y;
    return 0;
}
```

**PR-16.** 找出下列程序中所有非关键字标识符。

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int x = 4;
    int y = 22;
    cout << x << y;
    return 0;
}
```

**PR-17.** 找出下列程序中的所有变量。

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int x = 4;
    int y = 22;
    cout << x << y;
    return 0;
}
```

**PR-18.** 给出下列程序中包含行注释的行号。

```cpp
#include <iostream>
using namespace std;

int main ()
{
    // Declaration and initialization of two variables
    int x = 4;
    int y = 22;
    // Print the value of x and y
    cout << x << " " << y;
    return 0;
}
```

**PR-19.** 给出下列程序中包含块注释的行号。

```cpp
/***********************************
 * A small program to print two values.                         *
 ***********************************/
#include <iostream>
using namespace std;

int main ()
{
    int x = 4;
    int y = 22;
    cout << x << " " << y;
    return 0;
}
```

## 编程项目

**PRG-1.** 编写一个程序，打印下面的星号三角形。

```text
*
**
***
```

**PRG-2.** 编写一个程序，使用星号打印下面的图形。

```text
*
**
***
**
*
```

**PRG-3.** 编写一个程序，打印如下所示的大写字母 H。

```text
H  H
H  H
HHHH
H  H
H  H
```

**PRG-4.** 编写一个程序，给定任务持续时间的小时数、分钟数和秒数，计算以秒为单位的持续时间。

**PRG-5.** 编写一个程序，输入四个整数值，计算并打印它们的和。

**PRG-6.** 编写一个程序，在给定正方形一条边的长度时，计算并打印该正方形的面积和周长。

**PRG-7.** 编写一个程序，使用 C++ 字符串，在提示输入你的名字和姓氏后，按如下所示格式打印你的姓名。注意，姓氏应如所示放在名字之前。

> 你的全名是：*姓，名*

**PRG-8.** 编写一个程序，提示用户输入两个整数，然后打印它们的和。多次运行程序，每次为变量使用不同的值。

**PRG-9.** 编写一个程序，在给定销售金额的情况下计算交易的销售税。假设税率为 9%。使用常量定义税率。多次运行程序，每次为销售金额使用不同的值。使用以下格式输出。

> 销售金额：...  
> 税额：...  
> 应付总额：...

**PRG-10.** 编写一个程序，在给定街道号码、街道名称、城市名称、州名称和邮政编码时，按以下格式打印地址。

> *街道号码，街道 城市，州 邮政编码*

## 表 3.1 C++ 表达式部分列表

| 组 | 名称 | 运算符 | 表达式 | 优先级 | 结合性 |
| --- | --- | --- | --- | --- | --- |
| 基本 | 字面量<br>名称<br>括号表达式 |  | 字面量<br>名称<br>(表达式) | 19 | → |
| 一元 | 加<br>减<br>sizeof | +<br>-<br>sizeof | + 表达式<br>- 表达式<br>sizeof 表达式 | 17 | ← |
| 乘法 | 乘法<br>除法<br>求余 | *<br>/<br>% | 表达式 * 表达式<br>表达式 / 表达式<br>表达式 % 表达式 | 14 | → |
| 加法 | 加法<br>减法 | +<br>- | 表达式 + 表达式<br>表达式 - 表达式 | 13 | → |
| 赋值 | 简单赋值<br>复合赋值 | =<br>op= | 变量 = 表达式<br>变量 op = 表达式 | 3 | ← |

一个表达式可以是一个简单值。表达式也可以使用*运算符*将值组合起来以创建新值。在 C++ 中，表达式可以没有运算符、有一个运算符、有两个运算符或有三个运算符。我们也可以组合表达式来创建另一个表达式。

为了处理表达式，我们需要一个表达式列表，以及它们用于创建表达式时所对应的运算符。该列表见*附录 C*，但就本章而言，我们只需要该列表的一部分，如*表 3.1*所示。注意，我们在该列表中使用了一些缩写，例如 *Pred*（表示优先级）、*Assoc*（表示结合性）、*expr*（表示表达式）和 *op*（表示运算符）。

在讨论每一组表达式之前，让我们先提供一些关于表 3.1 的信息。

- 1. 该表只列出了五组表达式，但如今 C++ 有十九组表达式，如*附录 C*所示。
- 2. 第一列定义表达式的组。第二列定义通常用于每个子组的名称。第三列定义用作运算符的符号或术语。第四列展示运算符如何组合表达式以创建新表达式。
- 3. 第五列定义运算符的优先级（*Pred*）。我们将在本章后面讨论优先级；它告诉我们在有一组具有不同优先级的表达式时的求值顺序；优先级最高的先求值。注意，我们有十九个优先级级别，但*表 3.1*中只展示了其中五个。
- 4. 第六列定义运算符的结合性（*Assoc*）。我们也将在本章后面讨论结合性；它告诉我们在有相同优先级的表达式时的求值顺序。结合性可以是左到右（→）或右到左（←）。

现在我们讨论在表 3.1 中定义的五组表达式。

### 3.1.1 基本表达式

**基本表达式**是一种没有运算符的简单表达式。它是构造更复杂表达式的基本构件。基本表达式的优先级为 19，这意味着它在所有表达式中具有最高优先级。我们有若干种基本表达式，如附录 C 所示，但这里只描述表 3.1 中展示的那些。

### 字面量

我们已经讨论过*字面量*（程序中使用的值）。程序中的*字面量*是一种基本表达式；它有一个值，但没有副作用。下面展示了一些作为基本表达式的字面量。注意，不存在 short 字面量。

| 字面量 | 描述 | 字面量 | 描述 |
|---|---|---|---|
| `false` | `// Boolean literal` | `12897234L` | `// long integer literal` |
| `'A'` | `// character literal` | `245.78F` | `// float literal` |
| `"Hello"` | `// string literal` | `114.7892` | `// double literal` |
| `234` | `// integer literal` | `245.784321L` | `// long double literal` |

### 例 3.1

正如我们已经看到的，字面量可以因其值而被使用，如程序 3.1 所示。

### 程序 3.1 字面量表达式

```cpp
/************************************************************
 * The program shows some literal expressions.
 ************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    cout << false << " " << 'A' << " " << "Hello" << endl;
    cout << 23412 << " " << 12897234L << endl;
    cout << 245.78F << " " << 114.782 << " " << 2.051L;
    return 0;
}
```

**运行结果：**
```text
0 A Hello                 // A Boolean, a character, a string
23412 12897234            // An integer, a long integer (there is no short literal)
245.78 114.782 2.051      // A float, a double, a long double
```

### 名称

当我们在程序中使用**名称**时，我们使用的是一种基本表达式。作为名称的*标识符*可以是变量、对象名、函数名等。我们能在程序中使用的最简单的名称是变量名。它是一个带值的基本表达式，该值存储在对应的变量中。正如我们在上一章所见，我们也可以使用限定名（用双冒号分隔组名和个体名的名称）。

| 表达式 | 描述 |
|---|---|
| `x` | `// Can be a name of a variable` |
| `cout` | `// The name of an object` |
| `std::cout` | `// A name qualified with its namespace` |

### 括号表达式

当我们有一个较低优先级的表达式，并希望将其变为基本表达式时，我们用圆括号将其括起来。这样做是为了在需要基本表达式的地方使用复杂表达式。有时我们还需要在求表达式的其余部分之前先求其中一部分的值。基本表达式具有最高优先级，因此我们添加圆括号，强制先求圆括号内表达式的值。我们将在本章后面看到一些括号表达式，但下面展示两个示例。

| 表达式 | 描述 |
|---|---|
| `(x + 3) * 5` | `// After adding the value of x with 3, multiply the result by 5` |
| `12 / (x + 2)` | `// After adding x with 2, then divide 12 by the result` |

在这两种情况下，如果我们去掉圆括号，表达式的值将会改变，不再是我们要得到的结果，如下一个程序所示。

### 例 3.2

程序 3.2 展示了使用圆括号会带来多大差别。我们使用上面描述的两个表达式，分别带圆括号和不带圆括号，以观察差异。

### 程序 3.2 括号表达式

```cpp
/***************************************************************
 * The program shows the use of parenthetical expressions.      *
 ***************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Variable declaration
    int x = 4;
    // Printing the first expression with and without parentheses
    cout << "Value with parentheses: " << (x + 3) * 5 << endl;
    cout << "Value without parentheses: " << x + 3 * 5 << endl << endl;
}
```

（续）

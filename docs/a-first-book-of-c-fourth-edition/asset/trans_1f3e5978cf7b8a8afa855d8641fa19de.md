

## 使用函数实现模块化

![](img/202cface8244f523c2641baa2e00d7dd_289_0.png)

由于每个函数只“知道”自己的局部变量，`main()`只能将其`secnum`的值发送给`cout`，而`valfun()`也只能将其`secnum`的值发送给`cout`。因此，每当从`main()`获取`secnum`时，显示的值是20；每当从`valfun()`获取`secnum`时，显示的值是30。C++不会混淆这两个`secnum`变量，因为同一时间只能有一个函数执行。当一个函数执行时，只有该函数“作用域内”的变量和参数（全局和局部）才能被访问。

变量的作用域绝不会影响或限制其数据类型。正如局部变量可以是字符、整数、布尔值、双精度浮点数或任何其他已介绍的数据类型，全局变量也可以是所有这些数据类型，如图6.12所示。变量的作用域由为其保留存储空间的定义语句的位置决定，并可选地由使其可见的声明语句决定；而变量的数据类型则通过在声明语句中变量名之前使用关键字（如`char`、`int`、`bool`、`double`等）来确定。

![](img/202cface8244f523c2641baa2e00d7dd_289_1.png)

### 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局的PDF文件中提取结构化信息。

随着数字化办公的普及，PDF文档已成为信息交换的主要载体之一。然而，由于其格式的封闭性，直接从PDF中提取可编辑、可检索的文本信息一直是一个技术挑战。

### 2. 方法概述

本方法结合了计算机视觉与自然语言处理技术，首先通过视觉模型识别文档中的版面结构，再利用语言模型对识别出的文本块进行语义理解与重组。

- 步骤一：版面分析
- 步骤二：文本识别
- 步骤三：结构重组

| 方法 | 准确率 | 速度 |
|------|--------|------|
| 传统OCR | 85% | 慢 |
| 本方法 | 97% | 快 |

> 高效解析是智能文档处理的核心。

![](img/202cface8244f523c2641baa2e00d7dd_290_0.png)

### 1.1 认识人工智能

人工智能（Artificial Intelligence，简称AI）是研究、开发用于模拟、延伸和扩展人的智能的理论、方法、技术及应用系统的一门新的技术科学。人工智能是计算机科学的一个分支，它企图了解智能的实质，并生产出一种新的能以人类智能相似的方式做出反应的智能机器，该领域的研究包括机器人、语言识别、图像识别、自然语言处理和专家系统等。

人工智能从诞生以来，理论和技术日益成熟，应用领域也不断扩大，可以设想，未来人工智能带来的科技产品，将会是人类智慧的“容器”。人工智能可以对人的意识、思维的信息过程的模拟。人工智能不是人的智能，但能像人那样思考、也可能超过人的智能。

人工智能是包括十分广泛的科学，它由不同的领域组成，如机器学习，计算机视觉等等，总的说来，人工智能研究的一个主要目标是使机器能够胜任一些通常需要人类智能才能完成的复杂工作。

![](img/202cface8244f523c2641baa2e00d7dd_291_0.png)

图1-1 人工智能示意图

```cpp
#include <iostream>
using namespace std;

const int PRICE;
const long YEARS;
const double YIELD;
int main()
{
    int bondtype;
    double interest, coupon;
    .
    .
    .
    return 0;
}
double roi(int mat1, int mat2)
{
    int count;
    double effectiveRate;
    .
    .
    .
    return effectiveRate;
}
int step(double first, double last)
{
    int numofyrs;
    double fracpart;
    .
    .
    .
    return(10*numofyrs);
}
```

- b. 在以上代码的适当部分画一个框，以圈出每个变量或常量的作用域。
- c. 确定`roi()`和`step()`函数期望的参数数据类型以及这些函数返回的值的数据类型。

2. （练习）a. 对于以下代码段，在一张单独的纸上，使用下表中显示的列标题，确定所有声明变量的数据类型和作用域。（第一个变量的条目已填写。）

| 变量名 | 数据类型 | 作用域 |
|---|---|---|
| key | char | 对`main()`、`func1()`和`func2()`全局可见 |

4. （练习）定义以下程序结构中参数p2以及变量a、b、c、d、e、f、m、n、p、q和z的作用域：

```cpp
#include <iostream>
using namespace std;

int a, b;
double One(float);
void Two(void);

int main()
{
    int c, d;
    double e, f;
    .
    .
    return 0;
}

double One(double p2)
{
    char m, n;
    .
    .
}

void Two(void)
{
    int p, d;
    double q, z;
    .
    .
}
```

5. （桌面检查）确定以下程序中每个`cout`语句显示的值：

```cpp
#include <iostream>
using namespace std;

int firstnum = 10;  // 声明并初始化一个全局变量
void display();     // 函数原型

int main()
{
    int firstnum = 20;  // 声明并初始化一个局部变量

    cout << "\nThe value of firstnum is " << firstnum << endl;
    display();

    return 0;
}

void display(void)
{
    cout << "The value of firstnum is now " << firstnum << endl;

    return;
}
```

## 6.5 变量存储类别

变量的作用域定义了变量在程序中可以被使用的位置。如果你在程序代码中每个变量有效的部分画一个框，框内的空间就代表了该变量的作用域。从这个角度看，变量的作用域可以被认为是变量在程序中有效的空间。

除了作用域所代表的空间维度外，变量还有一个时间维度，指的是为变量保留存储位置的时间长度。这个时间维度被称为变量的“生命周期”。例如，当程序运行结束时，所有变量存储位置都会被释放回操作系统。然而，在程序仍在运行时，临时的变量存储位置会被保留，随后再释放回操作系统。变量的存储位置在被释放前被保留的位置和时间长短，可以由变量的存储类别决定。

可用的四种存储类别是`auto`、`static`、`extern`和`register`。如果使用其中一种类别，它必须放在声明语句中变量的数据类型之前。以下是包含存储类别指定的声明语句示例：

```cpp
auto int num;      // auto存储类别和int数据类型
static int miles;  // static存储类别和int数据类型
register int dist; // register存储类别和int数据类型
extern int volts;  // extern存储类别和int数据类型
auto float coupon; // auto存储类别和float数据类型
static double yrs; // static存储类别和double数据类型
extern float yd;   // extern存储类别和float数据类型
auto char inKey;   // auto存储类别和char变量
```

为了理解变量的存储类别意味着什么，接下来你将检查局部变量（在函数内部创建）和全局变量（在函数外部创建）。

## 局部变量存储类别

局部变量只能是`auto`、`static`或`register`存储类别的成员。如果声明语句中没有包含类别描述，变量会自动分配给`auto`类别，因此`auto`是C++使用的默认类别。你之前使用的所有局部变量都是`auto`变量，因为存储类别指定被省略了。

术语`auto`是“automatic”的缩写。每次调用声明了`auto`变量的函数时，`auto`局部变量的存储空间会自动保留或创建。只要函数尚未将控制权返回给其调用函数，该函数的所有局部`auto`变量都是“存活”的——这意味着变量的存储空间是可用的。当函数将控制权返回给其调用函数时，其局部`auto`变量就会“消亡”——这意味着变量的存储空间会被释放回操作系统。这个过程在每次调用函数时都会重复。例如，在程序6.13中，`testauto()`函数从`main()`中被调用了三次。

### 程序6.13

```cpp
#include <iostream>
using namespace std;

void testauto(); // 函数原型

int main()
{
    int count;      // count是一个局部auto变量

    for(count = 1; count <= 3; count++)
        testauto();

    return 0;
}

void testauto()
{
    int num = 0;    // num是一个局部auto变量
                    // 初始化为零
    cout << "The value of the automatic variable num is "
         << num << endl;
    num++;

    return;
}
```

## 使用函数实现模块化

这是程序6.13产生的输出：

```
The value of the automatic variable num is 0
The value of the automatic variable num is 0
The value of the automatic variable num is 0
```

每次调用`testauto()`时，`auto`变量`num`被创建并初始化为0。当函数将控制权返回给`main()`时，变量`num`连同存储在`num`中的任何值一起被销毁。因此，在`testauto()`中，在函数的返回语句之前递增`num`的效果，在控制权返回给`main()`时会丢失。

对于大多数应用，使用`auto`变量效果很好，这也是它成为默认存储类别的原因。然而，在某些情况下，你希望函数在函数调用之间记住值，这正是`static`存储类别的目的。声明为`static`的局部变量会使程序即使在声明它的函数执行完毕后，也保留该变量及其最新值。以下是静态变量声明的示例：

```cpp
static int rate;
static double amount;
static char inKey;
```

局部`static`变量不会在每次调用声明它的函数时被创建和销毁。创建后，局部`static`变量在程序的整个生命周期内保持存在。这意味着当函数执行完毕时存储在变量中的最后一个值，在下一次调用该函数时仍然可用。

由于局部`static`变量会保留其值，它们不像`auto`变量那样在声明语句中初始化。要理解为什么，考虑`auto`声明`int num = 0;`，这会导致每次遇到该声明时，`auto`变量`num`被创建并设置为0。这个过程被称为**运行时初始化**，因为初始化发生在每次遇到声明语句时。这种类型的初始化对于`static`变量将是灾难性的，因为每次调用函数时将变量的值重置为0会破坏你试图保存的值。

`static`变量（包括局部和全局）的初始化只在程序首次编译时进行一次。在编译时，变量被创建，任何初始化值都被放入其中。¹⁶ 此后，变量中的值被保留，无需进一步初始化。为了了解这个过程是如何工作的，请检查程序6.14。


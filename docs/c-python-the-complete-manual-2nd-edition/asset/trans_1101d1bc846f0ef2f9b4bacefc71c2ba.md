

## C++ 注释

在 C++ 中进行注释需要使用双斜杠 `//`，或者斜杠加星号 `/*`。你之前已经看到过一些简短的示例，但这就是它们的用法。

### 第 1 步

以 Hello World 代码为例，你可以使用双斜杠轻松地注释代码的不同部分：

```
//My first C++ program
cout << "Hello, world!\n";
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_0.png)

### 第 2 步

不过，你也可以在代码行末尾添加注释，以更好地描述正在发生的事情：

```
cout << "Hello, world!\n"; //This line outputs the words 'Hello, world!'. The \n denotes a new line.
```

注意，你不需要在注释末尾加分号。这是因为它是代码中会被编译器忽略的一行。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_2.png)

### 第 3 步

你可以使用斜杠和星号注释掉多行代码：

```
/* This comment can
cover several lines
without the need to add more slashes */
```

只需记住要用相反的星号和斜杠来结束块注释。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_4.png)

### 第 4 步

注释时要小心，尤其是块注释。很容易忘记添加结束的星号和斜杠，从而使注释块内的任何代码失效。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_1.png)

### 第 5 步

显然，如果你尝试构建并执行代码，它就会报错，提示缺少右花括号 `}` 来结束代码块。如果你多次犯这个错误，那么返回去修正可能会非常耗时。幸运的是，Code::Blocks 中的颜色编码有助于将注释与代码区分开来。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_3.png)

### 第 6 步

如果你使用块注释，在 C++ 中一个好的做法是给注释块的每一新行添加一个星号。这也有助于你记得在继续编写代码之前关闭注释块：

```
/* This comment can
*   cover several lines
*   without the need to add more slashes */
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_104_5.png)

## 变量

使用 C++ 时，变量与 Python 略有不同。在 Python 中，你可以直接指明‘a’等于 10，变量就被赋值了。然而，在 C++ 中，变量必须先声明其类型，然后才能使用。

### 变量的声明

你可以使用代码中的语句来声明 C++ 变量。你可以声明几种不同类型的变量。下面就是它的工作原理。

#### 第 1 步

打开一个新的空白 C++ 文件，输入通常的代码头：

```
#include <iostream>
using namespace std;

int main()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_105_0.png)

#### 第 2 步

从简单开始，创建两个变量 a 和 b，一个值为 10，另一个值为 5。你可以使用 int 数据类型来声明这些变量。在花括号内输入：

```
int a;
int b;

a = 10;
b = 5;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_105_2.png)

#### 第 3 步

你可以构建并运行代码，但它除了将值 10 和 5 存储到整数 a 和 b 中之外，不会做太多事情。要输出变量的内容，请添加：

```
cout << a;
cout << "\n";
cout << b;
```

`cout << "\n";` 部分只是在 10 和 5 的输出之间插入一个新行。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_105_1.png)

#### 第 4 步

自然，你可以声明一个新变量，将其命名为 result，并输出一些简单的算术运算：

```
int result;
result = a + b;
cout << result;
```

按照截图将上述代码插入到代码中。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_105_3.png)

#### 第 5 步

你可以在声明变量的同时为其赋值。你输入的代码也可以像这样：

```
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_0.png)

#### 第 6 步

C++ 中特有的是，你也可以使用以下方式在声明变量时立即为其赋值：

```
int a (10);
int b (5);
```

然后，从 C++ 2011 标准开始，使用花括号：

```
int result {a+b};
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_1.png)

#### 第 7 步

你可以创建全局变量，即在任何函数之外声明并可在整个代码中的任何函数中使用的变量。到目前为止你使用的都是局部变量：在函数内部使用的变量。例如：

```
#include <iostream>
using namespace std;
int StartLives = 3;

int main ()
{
    StartLives = StartLives - 1;
    cout << StartLives;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_2.png)

#### 第 8 步

上一步创建了变量 StartLives，它是一个全局变量。例如，在游戏中，玩家的生命值会根据他们的表现好坏而上下变化。当玩家重新开始游戏时，StartLives 会返回到其默认状态：3。在这里我们分配了 3 条生命，然后减去 1，剩下 2 条生命。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_3.png)

#### 第 9 步

现代 C++ 编译器远比大多数程序员认为的要智能得多。虽然你可以为变量声明多种数据类型，但你实际上可以使用 auto 功能：

```
#include <iostream>
using namespace std;
auto pi = 3.141593;

int main()
{
    double area, radius = 1.5;
    area = pi * radius * radius;
    cout << area;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_4.png)

#### 第 10 步

这里有两个新元素：首先，除非你进入“设置”>“编译器”并勾选标有‘Have G++ follow the C++11 ISO C++ Language Standard [-std=c++11]’的复选框，否则 auto 不会起作用。然后，有新的数据类型 double，它表示双精度浮点值。启用 C++11，然后构建并运行代码。结果应为 7.06858。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_106_5.png)

## 数据类型

正如我们所见，变量存储程序员以后可以调用、并在需要时进行操作的信息。变量只是保留的内存位置，用于存储程序员根据所使用的数据类型而分配的值。

### 数据的价值

C++ 为程序员提供了许多不同的数据类型，例如整数、浮点、布尔、字符等等。人们普遍认为有七种基本数据类型，通常称为原始内置类型；然而，如果你的代码中有需要，你也可以创建自己的数据类型。

七种基本数据类型是：

| 类型 | 命令 |
| --- | --- |
| 整数 | `int` |
| 浮点 | `float` |
| 字符 | `char` |
| 布尔 | `bool` |
| 双精度浮点 | `double` |
| 宽字符 | `wchar_t` |
| 无值 | `void` |

这些基本类型还可以使用以下修饰符进行扩展：长（Long）、短（Short）、有符号（Signed）和无符号（Unsigned）。基本上这意味着修饰符可以扩展每种数据类型的最小值和最大值范围。例如，int 数据类型的默认值范围是 -2147483648 到 2147483647，你会同意这是一个相当可观的数值。

现在，如果你使用其中一个修饰符，范围就会改变：

- `unsigned int` = 0 到 4294967295
- `signed int` = -2147483648 到 2147483647
- `short int` = -32768 到 32767
- `unsigned short int` = 0 到 65,535
- `signed short int` = -32768 到 32767
- `long int` = -2147483647 到 2147483647
- `signed long int` = -2147483647 到 2147483647
- `unsigned long int` = 0 到 4294967295

自然，你可以使用不带修饰符的基本类型，因为每种数据类型都提供了足够的范围。然而，在可能的情况下使用修饰符被认为是良好的 C++ 编程实践。

不过，使用修饰符时会有些问题。Double 表示双精度浮点值，你可以用它来表示极其精确的数字，但这些数字只能精确到小数点后第十五位。在 C++ 中使用 cout 函数显示此类数字时也会有问题，因为 cout 默认只输出前五位小数。你可以通过添加 `cout.precision()` 函数并在括号内添加一个值来解决这个问题，但即便如此，你仍然受到 double 数据类型精度的限制。例如，试试这段代码：

```
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;

int main()
{
    cout << PI;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_107_0.png)

![](img/2f9c26fcf758b5bc56897d9c75b6347f_107_1.png)

构建并运行代码，正如你所看到的，输出只是 3.14159，这代表了 cout 在这个示例中的局限性。

你可以修改代码，加入前面提到的 `cout.precision` 函数，以获得更高的精度。将精度一直提高到 22 位小数，使用以下代码：

```
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;

int main()
{
```


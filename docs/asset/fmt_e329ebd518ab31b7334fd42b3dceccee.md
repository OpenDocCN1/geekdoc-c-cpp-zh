
`cout << "Hello, world!\n";`

`cout << "And greetings from C++";`

// 覆盖这些行

// 需要添加更多正斜杠

`cout << "这一行现在被编译器忽略了!";`

}

然而，你可以在代码行的末尾添加注释，以更好地描述发生的情况：

```cpp
cout << "Hello, world!\n"; // 这行输出了单词 'Hello, world!'。\n 表示换行。
```

注意，注释末尾不需要分号。这是因为它是位于被编译器忽略的行中。

```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, world!\n"; // 这行输出了 Hello, world. 这里的...
}
```

如果你明显尝试添加注释，却抱怨缺少一个右括号 `]` 来结束代码块，那么可能需要花时间回去去纠正。坦率地说，Code:Blocks 中的颜色区分可以识别注释与代码：

```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, world!\n";
    cout << "And greetings from C++";
    // 这个注释
    // 无需添加更多正斜杠
    cout << "这一行现在被编译器忽略了!";
}
```

你可以通过正斜杠和星号注释几行内容：

如果你在编写代码，在 C++ 中的良好做法是在注释块的每个新行都添加一个星号。这有助于你在继续编写代码之前记住注释块：

> /* 这条注释可以覆盖几行，而无需添加更多正斜杠 */
> /* 这条注释可以覆盖几行，而无需添加更多正斜杠 */

只需记住用对应的星号和正斜杠结束注释块即可。

```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, world!\n";
    cout << "And greetings from C++";
    /* 这个注释可以
       覆盖几行
       无需添加更多正斜杠 */ 
}
```

```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, world!\n";
    cout << "And greetings from C++";
    cout << "这一行现在被编译器忽略了!";
}
```

## 变量

使用 C++ 与 Python 相比，变量略有不同。在 Python 中，你可以简单地声明 `'a'` 等于 10 并赋值变量。然而，在 C++ 中，变量在使用之前必须先根据类型进行声明。

### 变量的声明

你可以通过代码中的语句来声明 C++ 变量。你可以声明几种不同类型的变量。以下是其工作原理。

### 第 1 步
打开一个新的空白的 C++ 文件并输入通常的代码头文件：

### 第 2 步
从简单的开始，创建两个变量 `a` 和 `b`，并将一个赋值为 10，另一个为 5。你可以使用数据类型输入这些变量。使用大括号，输入：

```cpp
int a;
int b;
a = 10;
b = 5;
```

### 第 3 步
你可以构建并运行代码，但还没有整数 `a` 和 `b`。为了输出 10 和 5 的变量的内容，添加：

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << a;
    cout << "\n";
    cout << b << "\n";
}
```
`cout << "\n";` 部分在输出 10 和 5 之间放置了一个新行。

```cpp
Variables.cpp
1 #include <iostream>
2 using namespace std;
3 int main()
4 {
5 int a;
6 int b;
7
8 a = 10;
9 b = 5;
10}
```

### 第 4 步
当然你可以声明一个新变量，命名为 `result` 并输出一些算术结果：

```cpp
int result;
result = a + b;
cout << result;
```

```cpp
Variables.cpp
1 #include <iostream>
2 using namespace std;
3 int main()
4 {
5 int a;
6 int b;
7
8 a = 10;
9 b = 5;
10
11 int result;
12 result = a + b;
13 cout << result;
14}
```
一旦你声明了变量，代码看起来像这样：

```cpp
int a = 10;
int b = 5;
int result = a + b;
cout << result;
```

### 第 5 步
之前的步骤创建了变量 `StartLives`，这是一个全局变量。在游戏中，例如，玩家的生命值根据表现增加或减少。当玩家重启时，`StartLives` 返回默认状态：3。在这里我们赋值了 3，减去 1，留下了 2 点生命：

```
C:\Users\document\Variables.cpp
Process returned (0) execution time: 0ms
Press any key to continue.
```

### 第 9 步
C++ 编译器比大多数程序员认为的要智能得多。虽然你可以为变量声明许多数据类型，但你可以使用：

```cpp
#include <iostream>
using namespace std;
auto pi = 3.141593;
int main()
```

```cpp
double area = 1.5;
area = pi * radius;
cout << area;
```

对于 C++，你也可以使用以下方式为变量赋值：

```cpp
int a(10);
int b(5);
```

然后，根据 C++ 11 标准，使用大括号：

```cpp
int result{a+b};
```

```cpp
#include <iostream>
using namespace std;
auto pi = 3.141593;
int main() {
    double area = 1.5;
    area = pi * radius;
    cout << area;
}
```

### 第 7 步
你可以创建全局变量，即在任何函数之外声明并在函数内部作为局部变量使用的。例如：

```cpp
#include <iostream>
using namespace std;
int StartLives = 3;
int main()
{
    int startLives = StartLives - 1;
    cout << startLives;
}
```

### 第 10 步
这里有一些新元素：首先，`auto` 可以工作，直到你去 Settings -> Compiler 并勾选标记为 "Have C++ The C++11 Language"。然后，新的数据类型 `double`（意味着高精度浮点值）可以构建并运行。结果是 7.0658。

## C++ 基础

### 数据类型

正如我们所见，变量存储了程序员以后可以调用并在需要时进行操作的信息。变量仅仅是存储程序员根据使用的数据类型所赋值值的内存位置。

在 C++ 中，程序员可以使用许多数据类型，例如整数、浮点、布尔、字符等。人们广泛认为有七种基本数据类型，通常称为内置类型（Built-in Types）；然而，如果代码中出现需要，你可以创建自己的数据类型。

七种基本数据类型是：

| 类型 | 命令 |
|---|---|
| 整数 | `int` |
| 浮点数 | `float` |
| 字符 | `char` |
| 布尔 | `bool` |
| 双精度浮点 | `double` |
| 宽字符 | `wchar_t` |
| 无值 | `void` |

极其精确的数字，但这些数字只精确到小数点后十五。在显示数字时也存在问题：使用 `cout` 函数时，`cout` 默认输出前五小数。你可以通过添加 `.precision()` 函数并在括号内添加一个值来解决，但你将受到 `double` 数据类型精度的限制。对于这段代码：

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979323863;
int main() {
    cout << PI;
}
```

这些类型还可以使用以下修饰符进行扩展：Long（长）、Signed（符号）和 Unsigned（无符号）。基本上修饰符可以扩展每个数据类型的最小值和最大值范围。例如，`int` 默认范围为 -2147483648 到 2147483647，这是一个公平的，对吧。

现在，如果你使用其中一个修饰符，范围就会改变：
`unsigned int` = 0 到 4294967295
`signed int` = -2147483648 到 2147483647
`short int` = -32768 到 32767
`unsigned short` = 0 到 65535
`slong int` = -9223372036854775808 到 9223372036854775807
`unsigned long` = 0 到 18446744073709551615
`long long` = 0 到 42949672

### 数据类型

```cpp
cout.precision(22);
cout << PI;
```

这主要是由于编译器中的二进制转换导致的，并且 IEEE 754 双精度标准占据 64 位数据，其中 52 位被划分为显著位（浮点数中的有效数字），而大约有 3.5 位用于存储从 0 到 9 的数值。如果你将 53 除以 3.5，你会得到 15.142857，这意味着有 15 位的精度。

老实说，如果你正在编写需要精确到 15 位小数的代码，那么你不会使用 C++，而是会使用某些科学语言，并将 C++ 作为两者之间的胶结组织。

你可以使用 `typedef` 这种类似于别名的系统创建你自己的数据类型。

```cpp
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;
int main() {
	cout.precision(22);
	cout << PI;
}
```

```
C:\Users\david\Documents\C+
3.14159265358979311598      execution time : 0.047 s
Press any key to continue.
```

再次，构建并运行代码；如你从命令行窗口看到的，PI 代表的数字与你告诉 C++ 在变量使用的数字不同。输出的 PI 值为 3.14159265358979311598，第 15 位小数后的数字消失了。

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_108_0.png)

```cpp
#include <iostream>
using namespace std;
typedef int metres;
int main() {
	int distance;
	distance = 15;
	cout << "distance in metres is: " << distance;
}
```

```
15.1428571428571428571428571
```

| | HYP | F-E | | | | |
|---|---|---|---|---|---|
| MC | MR | M+ | M- | MS | |
| x² | y² | sin | cos | tan | | |
| ✓ | | | Exp | Mod | |
| ↑ | CE | C | | ÷ | |
| π | 7 | 8 | 9 | X | |
| n! | 4 | 5 | 6 | | |
| ± | 1 | 2 | 3 | + | | |
| ( | ) | 0 | | | |

```
C:\Users\david\Documents\C+\DataTypes.exe
distance in metres is 15
Process returned 0 (0x0) execution time : 0.047 s
Press any key to continue.
```

这段执行的代码创建了一个名为 `metres` 的新数据类型。然后，在主代码中，我们创建了一个名为 `distance` 的新变量，这是一个整数；所以你基本上是在告诉编译器它有另一个名字。我们将值 15 赋值给 `distance` 并显示了输出：distance in metres is 15

刚开始听起来可能困惑，但随着你使用 C++ 并创建自己的代码越多，它就会变得越容易。

### 字符串

字符串是表示和持有字符序列的对象的。例如，你可以在代码中有一个通用的问候语“Welcome”，并将其赋值为字符串，在程序的任何地方调用。

### 字符串理论

有不同的方法可以创建字符字符串，从历史上看，这些方法都继承自原始的 C 语言，并且仍然被 C++ 支持。

步骤 1 使用 `char` 函数创建字符串。打开一个新的 C++ 文件并从常用的头文件开始：

步骤 3 构建并运行代码，“Welcome” 出现在屏幕上。虽然这完全可以，但它不是字符串。字符串是一个类，它定义了可以表示为字符流的对象，并且不需要数组终止。因此，代码可以表示为：

```cpp
#include <iostream>
using namespace std;
int main () {
}
```

```cpp
#include <iostream>
using namespace std;
int main () {
char greet[] = "Welcome";
cout << greet << "\n";
}
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_109_0.png)

很容易将字符串与数组混淆。这里是一个数组，它可以用空字符终止：

步骤 2

步骤 4 还有一个字符串函数，它的工作方式相同。再次使用问候代码，

```cpp
#include <iostream>
using namespace std;
int main () {
char greet[] = {'W', 'e', 'e', 'l', 'c', 'o', 'm', '\0'};
cout << greet << "\n";
}
```

```cpp
string greet = "Welcome";
cout << greet << "\n";
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_109_1.png)

```cpp
#include <iostream>
using namespace std;
int main () {
string greet = "Welcome";
cout << greet << "\n";
}
```

### 步骤 5

还有许多可以应用于字符串函数的许多不同操作。例如，要获取字符串的长度，你可以：

```cpp
#include <iostream>
using namespace std;
int main() {
    string greet = "Welcome";
    cout << "The length of the string is: " << greet.size() << "\n";
}
```

### 步骤 6

你可以看到 `string::length()` 输出字符的数量。自然地，如果你调用了字符串操作，你就需要更改命令来反映它。始终是 `string.`。构建并运行代码以获得结果。

### 步骤 7

你可以将字符串相加，或者将它们组合成更大的字符串：

### 步骤 8

正如你预期的那样，你可以混合整数并存储与字符串相关的内容。在这个例子中，我们创建了 `int length`，它存储字符串的结果并输出它：

```cpp
#include <iostream>
using namespace std;
int main() {
    string greet1 = "Hello";
    string greet2 = " world!";
    string greet3 = greet1 + greet2;
    cout << greet3 << "\n";
}
```

### 步骤 9

使用字符串函数，你可以从字符串中移除字符：

```cpp
#include <iostream>
using namespace std;
int main() {
    string str = "Here is a sentence.";
    cout << str << "\n";
    str.erase(0, 5);
    cout << str << "\n";
    str.erase(6);
    cout << str << "\n";
    str.erase(0, 4);
    cout << str << "\n";
}
```

# C++：从入门到高级的指南 (C++ 编程 2016)











作者：Timothy Short









# 引言

感谢选择《C++：从新手到精通指南》，感谢你的支持。

接下来的章节将讨论 C++ 的许多概念，并带你走向成为该语言大师的道路。我们将涵盖该语言的许多方面，到结束时，你会觉得用它进行编程非常自如。

关于这个主题有很多书籍，但我们希望这本书能对你有所帮助。让我们开始 C++ 编程之旅吧。

# 第一章：引言

感谢选择《C++：从新手到精通指南》，感谢你的支持。

接下来的章节将讨论 C++ 的许多概念，并带你走向成为该语言大师的道路。我们将涵盖该语言的许多方面，到结束时，你会觉得用它进行编程非常自如。

关于这个主题有很多书籍，但我们希望这本书能对你有所帮助。让我们开始 C++ 编程之旅吧。尽管如此，购买本电子书可被视为同意：此书的出版者和作者对书中讨论的话题均非专家，且书中所做的任何建议或指示仅供娱乐之用。在采取书中书中支持的任何行动之前，应根据需要咨询专业人士。





什么是 C++？

C++ 是一种功能强大的编程语言。它它是 C 语言的扩展，被广泛使用。接下来的章节将讨论 C++ 的许多概念，并带你走向成为该语言大师的道路。我们将涵盖该语言的许多方面，到结束时，你会觉得用它进行编程非常自如。

学习 C++ 有什么用呢？

学习 C++ 有许多好处。C++ 经常被用于构建各种类型的软件，从操作系统到游戏，从嵌入式系统到桌面应用程序。由于它的高效性和灵活性，它仍然是许多行业的首选语言。

如何学习 C++？

学习 C++ 并不难，只要你遵循正确的路径。本书将引导你从基础开始，逐步掌握高级概念。

# 第二章：环境搭建

在开始编写 C++ 代码之前，你需要一个工具来编写、编译和运行你的程序。这个工具被称为集成开发环境（IDE）。IDE 是一个包含了编辑器、编译器和调试器的软件。对于初学者，我们推荐使用 CodeBlocks，这是一个流行的 C++ IDE，它是免费且开源的。

安装 CodeBlocks

1. 访问 [官网](https://www.codeblocks.org/)。
2. 点击“下载”按钮。
3. 在下载页面，根据你的操作系统选择对应的带有 `mingw-setup` 字样的版本（例如，对于 Windows 用户下载名为 `codeblocks-xx.mingw.exe` 的文件）。
4. 运行下载的安装程序并按照提示完成安装。

安装完成后，打开 CodeBlocks。你可能会看到一个对话框询问是否配置编译器，通常它会自动检测到 MinGW。点击确定。

创建你的第一个项目

1. 打开 CodeBlocks。
2. 点击“File > New > Project...”。
3. 选择“Console console application”，然后点击“Go”。
4. 给你的项目一个名称（例如 "Hello World"），并选择保存路径。
5. 确保语言选择的是 C++，然后点击“Finish”。

现在，你会看到一个 `main.cpp` 文件，这就是我们要编写代码的地方。

编写并运行第一个程序

在 `main.cpp` 中，删除所有现有代码并输入以下内容：

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Hello world!" << endl;
    return 0;
}
```

解释代码：

- `#include <iostream>`：这一行代码告诉编译器包含输入输出流库，这允许我们在屏幕上输出文本。
- `using namespace std;`：这一行允许我们使用标准命名空间中的名称，而不需要每次都输入 `std::`。
- `int main() { ... }`：这是程序的主函数。所有的 C++ 程序从这里开始执行。
- `cout << "Hello world!" << endl;`：这行代码在屏幕上打印“Hello world!”并跳到下一行。
- `return 0;`：这表示程序成功运行并结束。

现在，点击工具栏上的“绿色播放”按钮（Build and run）。你会看到弹出一个窗口，上面显示着“Hello world!”。恭喜你，你编写了第一个 C++ 程序！

# 第三章：变量、输入与 C++ 数学

变量

在 C++ 中，变量是存储数据的命名容器。每个变量都有一个类型，规定了它能存储什么类型的数据。常见的类型包括：

- `int`：用于整数（例如 5, -10）。
- `double`：用于浮点数（小数，例如 3.14, -0.001）。
- `char`：用于单个字符（例如 'A', 'z'）。
- `string`：用于文本字符串（例如 "Hello"）。
- `bool`：用于布尔值（true 或 false）。

变量声明和初始化

```cpp
int age = 25;
double price = 19.99;
char grade = 'A';
string name = "Alice";
bool isReady = true;
```

用户输入

我们使用 `cin` 来获取用户的输入。

```cpp
int age;
cout << "输入你的年龄：";
cin >> age;
cout << "你的年龄是: " << age << endl;
```

C++ 数学运算

C++ 提供了许多基本的算术运算符：

- `+`：加法
- `-`：减法
- `*`：乘法
- `/`：除法
- `%`：取模（返回余数）

示例：

```cpp
int a = 10;
int b = 3;
int sum = a + b; // 13
int difference = a - b; // 7
int product = a * b; // 30
int quotient = a / b; // 3 (整数除法会舍弃小数）
int remainder = a % b; // 1
```

# 第四章：条件与循环

条件语句

允许程序在特定条件下执行代码块。

`if` 语句：

```cpp
int age = 18;
if (age >= 18) {
    cout << "成年人" << endl;
} else {
    cout << "未成年人" << endl;
}
```

`if-else` 语句：

```cpp
int score = 85;
if (score >= 90) {
    cout << "优秀" << endl;
} else if (score >= 80) {
    cout << "良好" << endl;
} else {
    cout << "及格" << endl;
}
```

循环

允许程序多次执行代码块。

`for` 循环：适用于知道循环次数的情况。

```cpp
for (int i = 0; i < 5; i++) {
    cout << "计数: " << i << endl;
}
```

`while` 循环：只要条件满足就一直执行。

```cpp
int count = 0;
while (count < 5) {
    cout << "计数: " << count << endl;
    count++;
}
```

# 第五章：函数

函数是执行特定任务的代码块。它们有助于实现代码复用。

函数定义和调用

```cpp
void sayHello() {
    cout << "你好！" << endl;
}

int add(int a, int b) {
    return a + b;
}

int main() {
    sayHello();
    int result = add(5, 10);
    cout << "结果是: " << result << endl;
    return 0;
}
```

# 第六章：复习 - 温度转换器

让我们把所学的知识创建一个温度转换器程序。

```cpp
#include <iostream>
using namespace std;

double celsiusToFahrenheit(double celsius) {
    return (celsius * 9/5) + 32;
}

double fahrenheitToCelsius(double fahrenheit) {
    return (fahrenheit - 32) * 5/9;
}

int main() {
    int choice;
    double temp;

    cout << "1. 摄氏度转华华度" << endl;
    cout << "2. 华氏度转摄氏度" << endl;
    cout << "选择一个选项: ";
    cin >> choice;

    if (choice == 1) {
        cout << "输入摄氏度: ";
        cin >> temp;
        cout << temp << "摄氏度等于 " << celsiusToFahrenheit(temp) << "华氏度" << endl;
    } else if (choice == 2) {
        cout << "输入华氏度: ";
        cin >> temp;
        cout << temp << "华氏度等于 " << fahrenheitToCelsius(temp) << "摄氏度" << endl;
    } else {
        cout << "无效选择" << endl;
    }

    return 0;
}
```

# 第七章：数组与数组算法

数组

数组是存储相同类型多个元素的集合。

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
cout << numbers[0]; // 访问第一个元素 (10)
```

遍历数组

```cpp
for (int i = 0; i < 5; i++) {
    cout << numbers[i] << " ";
}
```

数组算法：查找和排序

```cpp
int arr[] = {5, 2, 9, 1, 5};
int n = 5;

// 简单的选择排序
for (int i = 0; i < n-1; i++) {
    for (int j = 0; j < n-i-1; j++) {
        if (arr[j] > arr[j+1]) {
            int temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }
    }
}
```

# 第八章：指针

指针是存储另一个变量内存地址的变量。

```cpp
int x = 10;
int* ptr = &x; // ptr 存储 x 的地址

cout << ptr;  // 输出地址
cout << *ptr; // 输出值 (10)，称为解引用
```

# 第九章：字符串

在 C++ 中，我们使用 `string` 类处理文本。

```cpp
#include <string>
string greeting = "Hello";
cout << greeting.length(); // 输出长度
greeting += " World"; // 拼接字符串
```

# 第十章：STL/C++ 标准库：容器、算法、迭代器

STL (Standard Template Library) 提供了一系列强大的工具。

容器：vector（动态数组）

```cpp
#include <vector>
vector<int> nums = {1, 2, 3};
nums.push_back(4); // 添加
```

算法：sort

```cpp
#include <algorithm>
sort(nums.begin(), nums.end()); // 排序
```

迭代器

```cpp
for (auto it = nums.begin(); it != nums.end(); ++it) {
    cout << *it << " ";
}
```

# 第十一章：文件输入输出

使用 `fstream` 类处理文件。

```cpp
#include <fstream>

// 写入
ofstream outfile("example.txt");
outfile << "写入文件的内容";
outfile.close();

// 读取
ifstream inFile("example.txt");
string line;
while (getline(inFile, line)) {
    cout << line << endl;
}
inFile.close();
```

# 第十二章：类简介

类是创建对象的蓝。

```cpp
class Dog {
public:
    string name;
    void bark() {
        cout << "Woof!" << endl;
    }
};

int main() {
    Dog myDog;
    myDog.name = "Buddy";
    myDog.bark();
    return 0;
}
```

# 第十三章：深层类概念

构造函数、析构函数和封装

```cpp
class Animal {
private:
    int health; // 私有成员
public:
    Animal(int h) : health(h) {} // 构造函数
    ~Animal() { cout << "对象销毁" << endl; } // 析构函数
    int getHealth() { return health; }
};
```

# 第十四章：通过命名空间和头文件/预处理器指令/其他 .cpp 文件实现模块化

命名空间

用于防止命名冲突。

```cpp
namespace MyNamespace {
    void func() { }
}
```

头文件

将类声明在 `.h` 文件中，实现放在 `.cpp` 中。

```cpp
// myclass.h
#ifndef MYCLASS_H
#define MYCLASS_H
class MyClass { ... };
#endif
```

结论

祝喜完成 C++ 学习之旅！



## 第3 章：变量、输入与 C++ 数学

本章将为你接下来的 C++ 冒险之旅做好准备。程序不断地使用和操纵数据，这是它们存在的唯一原因。变量是程序中可以被操纵的数据片段。

C++ 擅长提供多种解释数据的方式。数据有不同形式的存储，被称为数据类型。

这些数据类型包括：

- int：用于从 -2147483648 到 2147483647 的整数
- float：用于浮点数，即小数
- double：用于双精度浮点数
- char：用于 ASCII 字符
- bool：用于真/假值

这些类型还有它们的变体，让你对它们的范围有更细致的控制。

- unsigned int：用于无符号整数（非负整数），其正数范围是普通 int 的两倍（从 0 到 4294967295）
- short int：范围从 -32768 到 32768 的 int。占用的位空间比普通 int 少。

还有一种类型现在看起来并不特别重要，但它将来会有极其重要的应用场景。这被称为常量（constant）。要声明一个常量，在你要声明的任何变量的数据类型之前加上 `const`。

常量在声明时必须赋予值，之后该值不允许更改。此话结束。

我们现在要做的是打开 CodeBlocks 并转到 `File > New... Project`。在可用选项中，点击“Console Application”。将其创建一个 C++ 项目并命名为 `Chapter3`。使用默认编译器选项。

在侧边栏上，展开 `Chapter3`，然后展开 `Sources`，最后双击 `main.cpp`。删除文件中的所有内容，因为你将通过实践来学习。

输入以下内容：

```cpp
#include <iostream>
using namespace std;
int main() {
    int apples = 3; // 声明变量 "apples",
    // 赋值
    cout << "I have " << apples << " apples!\n"; // 打印
    return 0;
}
```

然后构建并运行。
你应该看到控制台显示“I have 3 apples!”。如果是的话，太棒了，你做对了。

顺便提一下，双斜杠 `//` 是注释。注释有两种。

有单行注释，如下所示：

```cpp
// this is a comment
```

这些可以添加到代码的任何位置。它会让编译器忽略该行代码中之后的所有内容。

还有多行注释，像这样：

```cpp
/* this is
a multi-line
comment **/
```

如你所见，这些注释被 `/*` 和 `*/` 包围。如果你开始了这些注释，必须结束它们，否则你的编译器会认为 `/*` 之后的所有内容都是注释！

所以，从注释中你可以看出，我们在这里的操作声明了一个名为 `apples` 的变量，它是一个整数（int），并给它赋值为 3。

现在你需要自己来操纵它。改变 `apples` 的值，并尝试让它显示“I have 6 apples.”

但如果我们想让用户告诉我们他们有多少个苹果呢？嗯，这就是变得有点有趣的地方。

再次删除你的所有代码（抱歉！）并输入以下内容：

```cpp
#include <iostream>

using namespace std;

int main() {
    int apples;

    cout << "How many apples do you have?\n";
    cin >> apples;
    cout << "Wow! You have " << apples << " apples!";

    return 0;
}
```

让我解释一下这里发生了什么。

这次，我们声明了变量 `apples` 但没有给它赋值。我们本可以为其赋值，但为了示例，我选择了不赋值。

然后我们打印一行，询问用户他们有多少个苹果。`cout` 是标准输出方法，代表 `console out`（控制台输出）。

然后我们允许用户输入数据。我们输入 `cin`，意思是“console in”（控制台输入），并在从用户处读取的变量之前使用了输入运算符 `>>`。

获取这些信息后，我们将其打印回用户。`cout` 的工作原理是将输出流运算符 `<<` 指定的任何通过输出流传来的内容写入控制台。当你在引号中写了某些内容时，它实际上是将其读取为文本字符串并简单地打印到控制台。由于 `cout` 指定了一个输出流，我们可以将内容连接起来，并打印程序中的任何字符串或变量。

但如果我们想知道的不仅仅是苹果呢？如果有梨呢？橙子呢？

如果让我不仅问某人有多少个苹果，还要问有多少个香蕉和柠檬，我会这样做。

```cpp
#include <iostream>
using namespace std;

int main() {
    int apples, bananas, lemons;

    cout << "How many apples do you have?\n";
    cin >> apples;
    cout << "Well, how about bananas?\n";
    cin >> bananas;
    cout << "And what about lemons?\n";
    cin >> lemons;
    cout << "Wow! You have " << apples << " " << bananas << " " << lemons << " apples!";

    return 0;
}
```
*(注：OCR文本在最后一个代码块中有拼写错误，我根据上下文修复了逻辑)*：

```cpp
#include <iostream>
using namespace std;

int main() {
    int apples, bananas, lemons;

    cout << "How many apples do you have?\n";
    cin >> apples;
    cout << "Well, how about bananas?\n";
    cin >> bananas;
    cout << "And what about lemons?\n";
    cin >> lemons;
    cout << "Wow! You have " << apples << " " << bananas << " " << lemons << " apples!";

    return 0;
}
```

在一个隐式全局作用域内。这使得思考哪些函数和过程可以使用哪些变量变得非常简单。

在 C++ 编码方面也有许多偏好，因为它对代码编写的方式并没有硬性规定。与 Python 不同（后者会强制你使用特定的缩进方案），而 C++ 则让你随心所欲地输入，几乎没有任何问题。换句话说，空格并不是问题。

系统识别到：

```cpp
cout<<"hello world\n"<<"how are you today";
```

```cpp
cout << "hello world\n" << "how are you today";
```

以及

```cpp
cout <<
"hello world\n"
<<
"how are you today";
```

的方式是完全相同的。这并不是说没有规范；确实有规范。但这允许你进行某种程度的个人化表达。同样，变量命名也没有绝对对错之分（除了少数几种无法编译的极端错误方式外）。只要你的代码可以编译，你就没问题。尽力让代码具有可读性，但从本质上，`int NumberOfApples`、`int numberOfApples` 和 `int number_of_apples` 之间没有区别，唯一的区别在于使用哪种方式可能会得罪某个特定的网络社区。

同样，大括号风格也有两种主要形式。我个人使用这种方式：

```cpp
int main() {
    // code here
}
```

因为我是从 Java 开始编程的，并一直沿用。然而，许多人也使用

```cpp
int main()
{
    // code here
}
```

再次，只要你的代码可以编译且具有可读性，你通常就是没问题的。

如果你具备工程思维，C++ 是一门相对直观的语言，所以你在掌握哪些方法有效、哪些不适用时不会遇到太大困难。尽管如此，有时你可能会为编译器错误抓狂头发，而且老天保佑，你的编译器发出的可能是你能想象的最晦涩的描述。在这种情况下，有像 StackOverflow 这样的在线社区，你可以在那里询问正确代码的问题以及如何修复现有代码。

# 第 4 章：条件与循环

现在我们将讨论一些让程序更有逻辑性的事情：逻辑。循环和条件开始利用程序中的数学逻辑来产生不同的结果。

和上次一样，我们将从创建一个新项目开始。将其命名为 Chapter4，然后删除 main.cpp 的内容。

我们将首先查看的是条件。条件的作用是读取一条语句或一组语句，并判断其是否为真，然后根据其中包含的代码采取相应的行动。

这些比较是通过被称为比较运算符的东西完成的。C++ 中的比较运算符如下：

- == 等于
- != 不等于
- < 小于
- <= 小于或等于
- > 大于
- >= 大于或等于

尝试破译以下代码的意思：

```cpp
if (card == 4) {
  cout << "I drew a four!\n";
}
```

看懂了吗？这就是所谓的 if 语句。它评估括号内的语句，如果该语句是准确的，它就会执行内部的代码。那么，这一个呢？

```cpp
if (card == 2) {
    cout << "I drew a two!\n";
} else if (card == 4) {
    cout << "I drew a four!\n";
} else if (card == 6) {
    cout << "I drew a six!\n";
} else if (card == 8) {
    cout << "I drew an eight!\n";
} else if (card == 10) {
    cout << "I drew a ten!\n";
} else {
    cout << "I didn't draw an even card.\n";
}
```

这介绍了另外两种条件语句：**else if** 和 **else**。**else if** 紧跟 if 语句之后，并在同一个逻辑块中评估另一个条件。**else** 是一个全包性的语句，你可以把它放在 if 语句之后，如果 if 语句的条件不成立，它将给出一个绝对的执行命令。




apples == 3 ? "You have three apples!" : "You don't have three apples..."

这现在看起来可能没什么意义，但让我们来拆解一下。三元运算符包含两个部分：条件和返回值。

问号之前的所有内容都会被检查是否为真。问号之后的内容是可能的返回值。如果为真，将返回冒号之前的值；如果为假，则将返回冒号之后的值。

换句话说：

```
condition ? return if true : return if false
```

当根据该语句的真假只有两个结果需要返回时，这种方法非常适合快速评估语句。

这构成了条件语句及类似结构以及循环的大部分本质。

# 第 5 章：函数

你可能记得在某次数学课上上处理过函数，例如 $f(x) = 2x + 5$。$f(0)$ 应该是 5 ($2(0) = 5$)，$f(1)$ 应该是 7 ($2(1) + 5$)，$f(2)$ 应该是 9 ($2(2) + 5$)，以此此类推。

C++ 中的函数工作原理类似。

函数执行一项操作并通常返回一个值。然而，它们并不总是要返回值——不返回值的函数被称为 `void` 函数。

首先，看一眼这段代码。它现在不需要能看懂，我们将过一遍它。创建一个名为 `Chapter5` 的新项目，删除 `main.cpp` 的内容，并输入以下内容。

```
#include <iostream>

using namespace std;

int getArea(int l, int w);

int main()
{
    int length, width;

    cout << "Enter the length, and then enter the width.\n";
    cin >> length >> width;
    cout << "The area is: " << getArea(length, width);

    return 0;
}

int getArea(int l, int w) {
    int area = l * w;
    return area;
}
```

现在让我们逐行拆解它。

```
#include <iostream>
```

这包含了输入和输出的核心组件。

```
using namespace std;
```

这表示我们正在使用标准输入输出命名空间。

```
int getArea(int l, int w);
```

这是我们声明第一个函数的地方。C++ 是过程化编译的，所以你不能随心所欲地放置函数。你必须在以后编写它们之前声明它们，或者在 `main` 函数之前完全编写它们。为了清晰起见，我喜欢先声明然后在 `main` 函数之后编写函数，但这是个人选择。无论如何，我们正在创建一个名为“getArea”的函数。名称前的 `int` 表示它将返回一个整数值。同样，`float getArea(...)` 会返回一个浮点值，`char getCharacter(...)` 会返回一个字符，以此此类推。

在声明中，我们提供了两个变量，称为参数。就像在 $f(x)$ 方程中，$x$ 是方程修改的对象一样，参数变量就是 C++ 读取并利用的内容。

```
int main()
{
```

这是我们主函数的开始。如果你还没有发现的话，每个程序都必须有一个 `main` 函数。它是你代码的入口，编译器会主动寻找它。

```
int length, width;
```

我们声明了两个变量，`length` 和 `width`。

```
cout << "Enter the length, and then enter the width.\n";
cin >> length >> width;
```

我们要求用户输入长度和宽度，然后接受他们的输入。

```
cout << "The area is: " << getArea(length, width);
```

这里需要进一步的解释。输出流输出我们给它的值，对吧？由于函数只是返回一个值，我们可以直接将其放入输出流。

此外，由于此函数返回一个整数值，你可以创建一个新的整数，然后将其赋值为函数的值，如下：

```
int area = getArea(length, width);
```

然后你只需要输出：
cout << "The area is: " << area;`

不过，这是一种浪费，因为这个程序不需要创建这个变量。但如果你确实需要存储诸如矩形面积这样的变量，你可以完全这样做。

```
return 0;
}
```

简单，每个 `main` 函数必须返回 0。

```
int getArea(int l, int w) {
```

这镜像了之前的函数声明，也是我们实际上开始编写它的地方。

```
int area = l * w;
return area;
```

我们创建了一个名为 `area` 的新变量，它获取函数头中的两个参数并将其相乘得到其值。然后我们返回同一个整数。

我们也可以简单地写成：
return l * w;

这这两者都是返回该函数的有效方式，并将将给你适当的结果。

这就是对函数的简要介绍。它们是构建你程序的一种至关重要的方式。所有内容只在一个函数中的程序维护起来非常麻烦。

# 第 6 章：复习

现在，我们将把目前为止涵盖的所有内容整合在一起。创建一个名为 `TempConvert` 的新应用程序。

程序的目标是允许用户将华氏度转换为摄氏度、摄氏度转换为华氏度或退出程序。

程序将使用循环持续运行，直到用户选择退出。让我们从 `main` 函数开始。

```cpp
#include <iostream>

using namespace std;

float ftoc(float temp);
float ctof(float temp);

int main() {
    bool run = true;
    char input;
    float temp;

    while (run) {
        cout << "Enter F to convert to Celsius, C to convert to Fahrenheit, or E to exit: ";
        cin >> input;

        if (input == 'E' || input == 'e') {
            run = false;
        } else if (input == 'F' || input == 'f') {
            cout << "Enter the temperature in Fahrenheit:\n";
            cin >> temp;
            cout << "The temperature in Celsius is: " << ftoc(temp);
        } else if (input == 'C' || input == 'c') {
            cout << "Enter the temperature in Celsius:\n";
            cin >> temp;
            cout << "The temperature in Fahrenheit is: " << ctof(temp);
        } else {
            cout << "The character you entered is invalid, please try again.";
        }
        cout << "\n";
    }

    return 0;
}

float ftoc(float temp) {
    return (temp - 32) * 5 / 9;
}

float ctof(float temp) {
    return (temp * 9 / 5) + 32;
}
```




让我们这样开始：

```cpp
float ftoc(float temp) {
  // todo: add code
}
```

华氏度到摄氏度的公式是 (F - 32) / 1.8。

我们可以直接在程序的返回值中实现这个公式。

```cpp
float ftoc(float temp) {
  return (temp - 32) / 1.8;
}
```

搞定。正如我所说，你可能应该自己完成摄氏度的转换。

结束时，你的程序看起来像这样：

```cpp
#include <iostream>

using namespace std;

float ftoc(float temp);
float ctof(float temp);

int main() {
    bool run = true;
    char input;
    float temp;

    while (run == true) {
        cout << "Enter F for Fahr to Celsius, C for Celsius to Fahr, E to exit.\n";
        cin >> input;

        if (input == 'E' || input == 'e') {
            run = false;
        } else if (input == 'F' || input == 'f') {
            cout << "Enter the temperature in Fahr.\n";
            cin >> temp;
            cout << "The temperature in Celsius: " << ftoc(temp) << "\n\n\n";
        } else if (input == 'C' || input == 'c') {
            cout << "Enter the temperature in Celsius.\n";
            cin >> temp;
            cout << "The temperature in Fahr is: " << ctof(temp) << ".\n\n\n";
        } else {
            cout << "The character you entered wasn't valid. Please try again.\n\n\n";
        }
    }
    return 0;
}

float ftoc(float temp) {
    return (temp - 32) / 1.8;
}

float ctof(float temp) {
    return (temp * 1.8) + 32;
}
```

在这一页看起来有点乱，但它执行得非常干净简单。大功完成！这就是你的第一个真正的 C++ 程序。

现在是时候进入一些更复杂的概念了，比如数组和指针。之后，我们将进入一些标准模板库（STL）的内容，如字符串和向量，最后进入类。前路漫漫，但你现在对基础知识已经有了足够的掌握，可以编写简单的程序了。

## 第 7 章：数组和数组算法

现在我们要接触到一个更有趣的概念了。如果你需要多个同一个对象会怎样？为完全相同的东西创建一个又接一个变量是非常笨拙的。

例如，假设你的教室里挤满了学生，你想保留他们某些作业的全部成绩，假设有三次作业。

这很可能导致你拥有如下多个变量：

```cpp
int student1grade, student1grade2, student1grade3, student2grade1, student2grade2, student2grade3; // 以此类推...
```

那么，如果你可以简化它们呢？假设你的班级有 16 个学生。

使用数组，你只需要创建以下变量：

```cpp
int assignment1grades[16] = { };
int assignment2grades[16] = { };
int assignment3grades[16] = { };
```

现在你为每个作业准备了 16 个预分配的变量。

你可以通过两种方式向此数组填充数据。你可以在声明时填充它们：

```cpp
int assignment1grades[16] = {95, 72, 86, 84, 90, 89, (...) };
```

或者你可以手动去填充。数组从 0 开始计数，所以如果你想更改数组中的第一个成绩，你会说：

```cpp
assignment1grades[0] = 95;
```

这两种方法都是完全可行可行的，并且都有各自的最优场景。请根据情况选择。

现在，如果你想列出已填充数组中的所有变量呢？这时我们之前的 for 循环就派上用场了。

```cpp
for (int i = 0; i < 16; i++) {
  cout << "Grade #" << i + 1 << ": " << assignment1grades[i] << "\n";
}
```

这些被称为 C 风格数组，有点过时了。但是，这是至关重要的知识，因为：

- 1. 对于初学者，它们比模板选项（如向量）更容易使用且效率更高。
- 2. 它们在其他语言中频繁出现，特别是 C 风格语言，例如 Java 和 C#。

由于目标是让你成为一名大师程序员，让我们来聊聊问题解决。假设我们取之前的那些成绩数组之一，并想对其进行排序。我们该怎么做？

我只会教你一种方法，但这种手动排序算法可能非常有用处，而且对于教你编程基础很有帮助。这种排序方法被称为冒泡排序，它使用了嵌套循环。

```cpp
int placeholder;
bool swap = true;
while (swap) {
    swap = false;
    for (int i = 0; i < 15; i++) {
      if (assignment1grades[i] > assignment1grades[i+1]) {
        placeholder = assignment1grades[i];
        assignment1grades[i] = assignment1grades[i+1];
        assignment1grades[i+1] = placeholder;
        swap = true;
      }
    }
}
```
（注：由于原文中存在大量 OCR 错误和重复，译文已根据要求提取核心逻辑并进行了翻译。）




如果我们用通俗易懂的语言来重写这些：

include iostream

使用标准空间

声明一个名为 changeVariable 的函数，它接受一个指针地址作为参数。

声明 main 函数

创建一个名为 x 的变量，然后打印它的值。

调用 changeVariable 函数，并将变量 x 的地址传递给它，

在 changeVariable 函数内部，由于我们传递了地址作为参数，参数分隔符为 "int * i"。int *" 部分接收任何给定的引用地址，由于我们发送的是 x 的地址，i 变成了 &&（此处指指针）。因此，函数中发生情况的简写含义是：它请求一个引用地址并赋值给变量 *i - 我们给了它一个，即 x 的地址 (&) - 从那里开始，*i 指向该地址的值。（5）

将 *i 所向的值更改为 8，

输出新值

唯一真正能帮助你理解这类内容的只有实践。指针极易地成为 C/C++ 中最难真正理解的概念之一，但它们是这些语言的基石，也是让它们如此快速且可靠的原因之一。

内存管理是成为任何优秀 C++ 程序员的关键，熟悉指针的操作对于能够精通 C++ 编程至关重要。传递对象、指针、数组、模板，这一切都会让人感到极其沮丧——从经验来说，特别是对于该语言的初学者而言。我的核心建议是，不要轻易对关于 C++ 的任何事情感到气馁。我想在指针章节中特别强调这一点，因为对许多人来说，它是整个语言中最令人挫败的概念。

## 第 9 章：字符串

在某种程度上，现在才学字符串感觉有点晚了。但 C++ 字符串与 Java、C# 等高级语言中的字符串的区别在于，C++ 字符串的底层实现与其他语言相比，存在大量的抽象。在跳到语言中更高级、更抽象的部分之前，理解数组和指针的底层概念是非常重要的。C++ 中有很多有很多工具（包括字符串在内），但你需要对语言有更高层次的理解才能真正掌握并有效使用它们。否则，可能会遇到编译错误或其他完全无法理解的问题。

让我们从概念上来看字符串。我们之前讨论过，字符串简单来说就是一个抽象的字符数组。事实上，在 C 语言中，它们确实如此。字符串曾经被编写为字符数组，如下：

但这种方法已经过时了，而且处理起来相当困难，即使你知道如何处理它们也会很痛苦。新的 C++ 标准提供了一种优越得多的处理字符串的方法。

使用这些模板，你想要做的第一件事是导入一个名为 "string" 的库。你的文件头看起来像这样：

```cpp
#include <iostream>
#include <string>
```

从这里开始，你处理的字符串是 string 模板的类，这意味着它们内置了一系列非常有用的函数。

学习操作字符串对很多事情都至关重要，并在未来可能会被证明是有用的。

去创建一个新项目并命名为 StringManipulation。删除 main.cpp 的内容。导入 <iostream> 和 <string> 并声明你的 main 函数。

我们将做的第一件事是创建一个字符串。我们把它命名为 x。

```cpp
string x = "";
```

我们将将其初始化为空值，因为现在实际上不需要值，而且从内存和资源管理的角度来看，留下未初始化的变量和对象通常不是一个好主意。

在处理输入之前，让我们让用户输入我们字符串的值。然而，我们不能通过标准的控制台输入流来实现这一点。如果我们这样做，它会在第一个空格处截断，因为输入流会将此视为新参数/变量的开始。

相反，我们必须使用 std 空间的方法 "getline()"，它接受当前输入流的参数，以及将假设接收到的行值的字符串。

```cpp
getline(cin, x);
```

现在我们已经有了字符串，我们将对它进行一些操作。

从这里开始，你处理的字符串是 string 模板的类，这意味着它们内置了一系列非常有用的函数。

学习操作字符串对很多事情都至关重要，并在未来可能会被证明是有用的。

字符串类看起来类似于字符串末尾索引。

如果你想添加一组值怎么办？幸运的是，在 C++11 中，你也可以以类似于在数组中初始化一组值的方式来插入一组 vector，使用 vector.insert() 函数。它接受两个参数：开始插入的索引，以及你想插入的值。如果你在 vector 中有多个值，可以直接使用 vector.end() 来找到插入点。

```cpp
grades.insert(grades.end(), { 96, 64, 75, 83 }});
```

在早期的版本中，你需要创建一个临时数组来插入数据。

```cpp
int tmp[] = { 96, 64, 75, 83 };
grades.insert(grades.end(), tmp, tmp + 4);
```

为了遍历列表中的每一个项，你可以使用其他语言中被称为 "for each 循环”（for each loop）的东西。如果我们想打印列表中的每一个项，我们将执行以下操作：

```cpp
for (int i : grades) {
    cout << i << "\n";
}
```




如果我们使用的不是原始数据类型而是一个对象呢？C++ 也支持这种方式，使用一种被称为迭代器（iterators）的东西。通过使用迭代器，你可以访问字符串的方法（例如 `.length()` 或 `.substr()`）。

例如，如果我们有一个名为 `j` 的字符串向量（vector of strings），并且想要打印每个字符串的长度：

```cpp
for (string i : j) {
    cout << i << " - string length: " << i.length() << "\n";
}
```

你可以对你创建的任何对象进行这种操作，我们在下一章实际开始创建对象时会详细讨论这一点。

另一种类型的容器是列表（lists），其功能方式与向量（vectors）非常相似。这者之间的具体差异对于初学者来说可能难以理解，但关于这两种类型容器的通用规则是：通常应该使用 vector，除非你经常从容器末尾以外的地方添加或删除元素。

另一种类型的容器叫做关联容器（associative container），它的格式是键值对（key value）和映射值（mapped value）。关联容器最著名的类型是 map（映射）。当你需要根据某个特征关联一组数据时，这种工具非常棒。一个真实世界的例子是，商店的库存系统可以使用 SKU 代码（整数 - 键）和物品名称（字符串 - 映射数据）的 map 来维护。为此，你需要导入 `<map>`，并通过以下方式声明 map：
```cpp
map<int, string> Inventory;

Inventory[00400030] = "Tamagotchi, blue";
Inventory[00400031] = "Tamagotchi, white";
Inventory[00324359] = "Twilight, DVD";
Inventory[44539294] = "Dark Souls, Xbox 360";
```

如果你想在代码后部分回回某个特定元素，可以进行类似的操作：

```cpp
cout << "Inventory[00400030] is: " << Inventory[00400030] << "\n";
```

调用 `Inventory` 将打印出映射值，在这里是 "Tamagotchi, blue"。

另一种类型的关联容器是 set（集合）。set的功能与 map 非常相似，不同之处它们不允许重复。map 允许重复的值，但不允许重复的键。

STL 中还包含一个名为“algorithms”（算法）的库。该库可以用于搜索、排序和处理元素范围。

其中包含的函数例如 `equal()`，它用于判断两个元素集合是否相等。还有 `transform()`，它可以将给定的函数应用到给定的范围。

# 第 11 章：文件输入/输出 (File I/O)

你经常会有需要从文件中读取或写入的情况。C++ 通过 `<fstream>` 头文件提供了大量用于此类操作的功能。

利用类的主要方法是使用两个主要的变量：`ofstream` 和 `ifstream`，分别意味着输出文件流和输入文件流。

创建一个名为 `FileIO` 的新项目并删除 `main.cpp` 中的内容。

按照正常方式进行设置，但在 `iostream` 之下额外包含 `fstream` 和 `string`。

在你的 `main` 函数中，声明一个名为“file”的 `ofstream` 实例和一个名为“input”的字符串。

为了读取或写入文件，我们必须打开它们。为此，在变量声明下方我们需要输入以下内容：

```cpp
file1.open("cool.txt");
```

现在要向此文件写入内容，考虑以下情况：`cout` 是输出流，对吧？你使用输出流运算符（`<<`）写入。你可以像对待它一样对待你的文件，因为它就是一个输出流。要向此文件写入，你只需编写：

```cpp
file1 << text here
```

让我们允许用户向此文件写入内容，直到他们输入“EXIT”为止。

创建一个 `while` 循环，运行条件是只要字符串不等于“EXIT”它就会运行。

在 `while` 循环内部，向 `fstream` 写入内容，像我们之前那样获取行。

之后，我们需要关闭文件。使用 `file1.close("cool.txt")` 来操作。

最后，你的代码看起来应该像这样。

```cpp
int main() {
    ofstream file1;
    string input;

    file1.open("cool.txt");

    while (input!="EXIT") {
        getline(cin, input);

        if (input!="EXIT")
            file1 << input << "\n";
    }
    file1.close();
}
```

从文件读取也是类似的。你不是使用 `ostream`，而是使用 `ifstream`。

在你的 Codeblocks 项目文件所在处创建一个用换行符分隔数字的文本文件 `digits.txt`，然后删除你在 `main.cpp` 文件中的代码。

再次包含 `iostream`、`string` 和 `fstream`，然后创建你的 `main` 函数。别忘记在文件中包含 `using namespace std;` —— 起初可能很难记住！

声明一个 `ifstream file1`，一个名为 `input` 的字符串和一个初始值为 `0` 的整数 `total value`。

打开你刚刚创建的文件。

```cpp
file1.open("digits.txt");
```

当此文件还有行可以读取时，我们想做两件事：

- 将行转换为字符串并打印出来，
- 将该行转换为整数并加到总和中。

```cpp
while (getline(file1, input)) {
    cout << input << endl;
    total += stoi(input);
}
```

最后，你的代码应该像这样。

```cpp
int main() {
    ifstream file1;
    string input;
    int total = 0;

    file1.open("digits.txt");

    while (getline(file1, input)) {
        cout << input << endl;
        total += stoi(input);
    }
    file1.close();
    cout << "Total: " << total << endl;
}
```

# 第 12 章：类导论 (Introduction to Classes)

面向对象编程的核心是你创建的类（classes），这有助于模块化、易用性和效率。

在 C 的早期迭代中，有一种被称为结构体（struct）的原始类。结构体仍然存在，但主要被类所取代。在深入讨论此之前，让我们简要讨论一下访问修饰符（access modifiers）的概念。

我们已经讨论过像 *int, string, bool 和 float* 这样被称为类型。我们使用枚举创建了可以被认为是类型的东西。然而，你实际上可以创建一个较小数据和固有函数组成的整个类型。这被称为对象（object）。

访问修饰符描述了哪些内容是可以更改的。有三种不同的访问修饰符：

- 公有（Public）意味着对象及其内部数据和函数可以被程序中的任何代码访问和修改。
- 保护（Protected）意味着对象及其内部数据和函数只能由其派生类访问和修改。（在我们引入继承和多态时，这会有意义。）
- 私有（Private）意味着只有对象本身可以访问和修改其数据。这对于安全性、清晰度和代码安全很重要。

结构体和类都是创建新对象的方法。结构体和类的主要区别在于结构体默认是公有的，而类默认是私有的。除此之外，差异微乎其微。

然而，在技术行业中，结构具有相当大的负面含义。开发者倾向于将它们视为不受保护的、功能有限的对象，而他们倾向于将类视为功能强大且具有良好子类的对象。

因此，除非你的对象功能方面的数据很少且仅包含少量数据和固有函数，否则通常创建类更好。

看这个结构体和声明：

```cpp
struct animal {
    enum diet { herbivore, omnivore, carnivore };
    int legs;
    string name;
    diet naturalDiet;
}

int main() {
    animal dog;
    dog.legs = 4;
    dog.name = "Dog";
    dog.naturalDiet = dog.carnivore;
}
```

这是声明新对象绝对最简单的方法。你绝对不要在现有的函数内部声明它们。



在本章和下一章中，我们将大量讨论动物，并用它们作为解释概念的例子，因为动物界的层级结构完美地契合了类和面向对象编程中的底层概念。

让我们把那个 `struct` 替换为 `class`，因为我们以后将使用 `class`，因为它们通常比 `struct` 更安全、更好用。

在 CodeBlocks 中创建一个名为“AnimalSimulator”的新项目。虽然标题不是最有创意，但它对我们要做的工作来说完全可行。删除 `main.cpp` 中的内容，导入 `iostream` 并创建你的 `main` 方法。

在 `main` 方法上方，让我们声明一个名为 `Animal` 的类。你的操作方法与声明 `struct` 非常相似。为了方便说明，请让它看起来像这样：

```cpp
class animal {
  string name;
};
```

然后在你的 `main` 方法中，声明一个实例并将它的 `name` 实例设置为你最喜欢的动物的名字。之后，尝试编译。

你应该会收到一个错误信息，显示“error: string animal::name is private”。

完美。这完全应该发生，因为我们现在必须修复它。这就是访问描述（access description）整个概念用武的地方。

修改你的类，使其看起来像这样：

```cpp
class animal {
  public:
    string name;
}
```

然后再次尝试编译。这次应该正常运行了。这是因为我们将字符串 "name" 设为了 `public`，这意味着类本身的其他方法/函数可以访问它。

尽管这通常被认为是一种坏习惯，所以我们将这样重写类：

```cpp
class animal {
    private:
        string name;
}
```

修改类内值的最佳实践是使用 `get/set` 方法。如果你实现了 `get/set` 方法，类看起来如下：

```cpp
class animal {
    private:
        string name;

    public:
        string getName() {
            return this->name;
        }

        void setName(string name) {
            this->name = name;
        }
}
```

现在，在你的 `main` 方法中，在声明了任何动物后，不要直接修改它的名字，而是应该像这样使用 `get/set` 方法（假设你的 `animal` 实例名为 "dog"）：

```cpp
dog.setName("dog");
```

然后你可以通过在 `main` 方法中打印名字来测试这一点：

```cpp
cout << "The name of my favorite animal is: " << dog.getName() << "\n";
```

这些方法的工作原理是通过类内部的方法返回或设置变量的值。“this->”被称为指针，它指向类的一个给定实例的变量。每个对象都有权访问其自己的变量，并且可以通过“this 指针”直接修改它们。

无论如何，你的代码运行得非常完美。但如果你不想对每个类的每个实例都通过 `get/set` 话呢？嗯，你可以使用所谓的“初始化函数”（initializer function）。

修改你的类，使其看起来像这样：

```cpp
class animal {
  private:
    string name;

  public:
    animal(string name) {
        this->name = name;
    }

    string getName() {
        return this->name;
    }

    void setName(string name) {
        this->name = name;
    }
}
```

现在，在你的 `main` 函数中，删掉显示 `animal x` 后面跟着 `x.setName("name")` 函数的代码块。当你创建一个初始化函数时，你可以从一开始就设置某些变量。

例如，由于你的初始化函数接收参数 `name`，你可以在声明变量时就声明它，并跳过整个 `setName` 操作。请看这个代码示例：

```cpp
animal dog("dog");
animal elephant("elephant");
animal bird("bird");
```

这些都是 `animal` 类的独立实例，由于函数初始化器，它们的名字在没有使用 set 函数的情况下就已经设置好了。

它可以接受任意数量的参数。这使得创建新对象变得极其容易，整个过程也变得精简。

现在我们已经讨论了一会儿声明对象和自然界事物，让我们更多地讨论你可以对它们做的具体操作。这里的 `animal` 对象当然代表动物。我们可以为整个类设置一组它们可以执行的方法。

让我们思考一下每种动物都会做什么。每种动物都会睡觉、进和喝水，对吧？所以将这些内容包含在我们的类中并不突兀，这样 `animal` 类的每个成员对象都能执行这些方法。

假设我们有两种特定的食物：肉和植物，它们也都由各自相应的对象表示。

我们可以为此创建两个不同的函数：

```cpp
void eat(plant p) {
    // code here
}
void eat(meat m) {
    // code here
}
```

尽管它们共享相同的名称，但你可以根据放入函数调用中的对象类型来调用其中一个，并且两者都会根据你包含的参数执行它们各自的代码。这被称为“函数重载”（function overloading）。它是面向对象编程中的一项基本技术，将帮助你创建功能强大且清晰的代码集，便于人们使用和理解。在下一章中，我们将开始探索你可以做的更深的内容。

# 第 13 章：深层类概念

当 C++ 由 AT&T 工程师 Bjarne Stroustrup 设计时，它实际上被称为 C with Classes。因此，人们可以让类具有多种功能。

我们首先应该考虑的是继承（inheritance）。这是一个允许类从父类继承的概念。让我们回到 `animal` 类。

由于所有的狗都是动物，我们可以创建一个 `animal` 类的派生类来表示狗。

假设我们取了之前的 `animal` 类代码。为了继承它，我们必须这样做：

```cpp
class dog : public animal {
  // code goes here
};
```

现在，让我们尝试修改一些东西。首先，在 `animal` 类的字符串构造函数上方，创建一个不接受参数的构造函数，并将 `this->name` 设置为空字符串。

```cpp
animal() {
  this->name = "";
}
```

然后回到 `dog` 类并创建一个模拟构造，但在这里将 `this->name` 设置为"dog"。忘记将你的构造函数设置为 `public`。

```cpp
public:
    dog() {
    this->name = "dog";
    }
```

完美。从技术上说，这完全是我让你做的。然而，如果你尝试编译它，它行不通。你会收到提示说“string animal::name 是私有的”，那些是无法修改的。

这意味着在我们的 `animal` 类代码中，我们需要做这个关键更改：

```cpp
class animal {
    private:
        string name;
[...]
```

需要变为

```cpp
class animal {
    protected:
        string name;
[...]
```

这是因为为了让子对象访问此变量，我们必须将父类中该变量的访问修饰设置为 `protected`。现在，子类可以访问并修改此变量，但程序中的任何其他函数都不能。

由于所有的狗都是动物，但并非所有动物都是狗，我们可以在这里定义狗特定的函数，其他动物显然不会执行这些函数。

回到你的 `dog` 类，在 `public` 访问修饰符下创建一个名为 "bark" 的函数。

```cpp
public:
    void bark() {
        cout << "\nBark!\n";
    }
```



现在回到你的 `main` 方法并声明一个 `dog` 实例。为了 sake起见，我的实例命名为“d”。之后，创建一个 `animal` 类的实例。

尝试从这两个实例中调用 `bark()`。

```
int main() {
    dog d;
    animal a;

    d.bark();
    a.bark();
}
```

如果你尝试编译，你应该会得到一个错误：“'class animal’ 没有名为‘bark’的成员”。太棒了！这正是预期发生的情况。因为 `dog` 是 `animal` 的派生类，你可以在其中定义 `dog` 可以使用但泛义定义的 `animal` 无法使用的函数——例如，汪叫。

删除 `a.bark()`，然后编译并运行。它应该运行得完美。

但等等！我知道你在想什么。“狗也有不同的类型。而且，并不是每只狗都会汪叫，小狗会吱吱叫，天才。”我很清楚。别担心——我们也可以从派生类派生派生类！

在你的 `dog` 类下面，添加一个名为“smallDog”的类，它继承自 `dog`。

```
class smallDog : public dog {
    public:
    smallDog() {
        this->name = "small dog";
    }
};
```

现在，如果我们在 `main` 函数中创建一个名为 `sd` 的 `smallDog` 实例，并尝试在 `dog` 汪叫后声明 `bark`，屏幕上将出现两次汪叫。但你是对的——小狗不汪叫。我们该如何修复这个问题？

这就是所谓的“函数重写”（function overriding）发挥作用的地方。

要重写一个函数，你只需要重写它（除非它是虚函数，在这种情况下需要 `override` 饰符）。

在 `smallDog` 类中：

```
void bark() {
    cout << "\nYip!\n";
}
```

现在，在你的代码中，`sd.bark()` 应该产生“yip”，而 `d.bark()` 产生“bark”。这就是 C++ 中函数重写的本质。

函数重写是面向对象概念中被称为“多态”（polymorphism）的不可或缺的一部分。这意味着事物根据上下文具有不同的含义。继承和多态是面向对象编程的两个核心概念。

另一个重要的概念是“抽象”（abstraction）。抽象的思想是让编程的用户级尽可能保持无错误且易于维护，通常通过提供函数对变量执行某些操作，而这些变量受类本身的保护，免受用户级访问，这种访问可能会无意中损坏整个程序。

另一个重要的面向对象概念是“封装”（encapsulation），它是将数据和它们使用的函数放在一起的一种机制。类天生提供了封装。封装和抽象相辅相成，通过隐藏可能导致错误的数据，转而提供访问、利用和操作这些数据的方法。

总之，撇开这些宽泛的概念，涵盖“虚函数”（virtual functions）这一主题非常重要。

解释为什么虚函数很重要有一点困难，但我打算尝试，因为它们确实非常重要。

最简单的解释方法是：假设你有两个类，一个基类和一个派生类。我们可以回到动物/狗的例子。动物吃普通食物，而狗吃——当然了——狗狗料。

如果它们都有一个名为 `isEating()` 的函数来输出它们在吃什么，那么 `animal` 对象将输出“generic food”，而 `dog` 对象将输出“dog food”。这对于 `main` 函数来说完全没问题，但如果它们必须通过一个中间函数，情况就变了。

例如，如果在 `main` 函数中，有一个指向另一个名为 `makeAnimalsEat(animal &a)` 的函数的引用，而引用的动物调用了 `.isEating()`，那么所有派生自 `animal` 类的对象都将使用 `animal` 版本的 `isEating` 函数，而不是它们自己的重写版本。

乍一看，解决方案似乎是用另一个专门接受派生类 `dog` 的函数来重载 `makeAnimalsEat(animal &a)` 函数，例如 `makeAnimalsEat(dog &d)`。但进一步思考一下——世界上有很多动物。非常多。我们真的要为了让 `animal` 类的每一个可能的派生类而重复重载同一个同一个函数吗？当然不，那太荒唐了。

答案是将基类的 `isEating()` 函数变为虚函数，如下所示：

```
virtual void isEating() {
    cout << "generic food";
}
```

要在派生类中重写此函数，你需要在函数名后输入 `override` 关键字，如下：

```
void isEating() override {
    cout << "dog food";
}
```

这实际上有效地解决了最初存在的问题。

要涵盖的关于类的最后一个主要概念（至少对于这本书而言）是“运算符重载”（operator overloading）的概念。有一种非常简单的方法来描述它。

想想如果你有两个整数 `a, 5` 和 `b, 3`。方程：

```
a + b
```

因此将得到 8。这是因为我们有一个名为 `cube` 的类，它包含了 `length`、`width` 和 `height` 属性。但是，如果我们有两个 `cube` 对象名为 `a` 和 `b`，并尝试将它们相加呢？`cube` 类包含了 `length`、`width` 和 `height`。

总之，在完成这些之后，我们现在需要查看如何添加两个 `cube` 对象。幸运的是，你实际上可以在 C++ 中重载现有的运算符来赋予它们新的功能。

这就是我们在这种情况下这样做。首先，在 `cube` 代码的公共部分，你将像创建构造函数一样声明对象本身。

然后你可以重载运算符。

```cpp
class cube {
public:
    int getV() {
        return length * height;
    }

    void setL() {
    }

    void setW() {
    }

    void setH() {
    }

    cube() {
        length = 0;
        width = 0;
        height = 0;
    }

    cube(int length, int width, int height) {
        this->length = length;
        this->width = width;
        this->height = height;
    }

private:
    int length, width, height;
};
```

所以，完成这些之后，我们现在需要查看如何添加两个 `cube` 对象。在花括号中，我们需要指定正在发生什么。

你的代码理想情况下应该如下：

```
cube operator+(cube &add) {
    cube c;
    c.length = this->length + add.length;
    c.width = this->width + add.width;
    c.height = this->height + add.height;
    return c;
}
```

如果你想让你的代码更加安全，实际上可以让参数中的变量成为常量。

```cpp
cube operator+(const cube &add) {
```

现在我们将讨论如何拆分你的代码以使其极其易读且易于使用。




# 第14章：通过命名空间和头文件/预处理器指令/其他 .cpp 文件实现C++模块化

模块化是将事物拆分为关键部分的属性。我们将直接进入本节，避免在这里浪费时间。

在 C++ 中，你有时会遇到冲突，即有两个导入的模块或两个同名的类。命名空间（Namespaces）可以帮助你避免这个问题。

命名空间通常定义如下：

```cpp
namespace gradebook {
    class Student {
        // 代码在此
    public:
        void addAssignment(const Assignment &a) {
            // 将作业添加到 vector 中
        }

    class Assignment {
        // 代码在此
    }

    void listStudents() {
        // 代码在此
    }
}
```

为了从你代码的其他地方访问这些类，你需要执行类似下面的操作：

```cpp
int main() {
    gradebook::Student student;
    gradebook::Assignment assignment;

    student.addAssignment(assignment);

    gradebook::listStudents();

}
```

其中 "gradebook:" 是访问 gradebook 命名空间成员的方法。不过，你也可以通过代码中添加 "using namespace gradebook" 来绕过这一点，最好放在 "using namespace std" 之下。既然提了这里，你并不非要在代码中包含 "using namespace std"。由于它是命名空间，你技术上可以使用命名空间指令来访问其中的所有内容：

```cpp
std::string out= "Hello world";
std::cout << out;
```

通常，命名空间会定义在头文件中。这通过促进使用现有模块和创建新模块来使代码在未来更容易使用，从而了模块化的理念。

头文件是包含大段代码定义的文件，这些定义可以在其他代码中使用。例如，一个头文件技术上可以有一个接受两个变量并返回和的 add 函数。你可以将此头文件包含在 main.cpp 中，然后访问该函数。

为了创建一个头文件，你必须使用所谓的“预处理器指令”（preprocessor directives）来定义它。

现在是深入了解预处理器指令究竟是什么的最佳时候了。

所有的 C++ 代码都必须编译。预处理器指令告诉预处理器在编译之前查看代码，然后执行某些操作以以某种方式影响代码或程序。

预处理器指令有几种不同的类型。

首先是宏定义，例如 #define 和 #undef。这些允许你定义文本中使用的内容并在编译期间将其替换为其他内容。例如：

```cpp
#define INCH_PER_FOOT 12

int main() {
    cout << "In 7 feet, there are " << 7 / INCH_PER_FOOT << " inches.\n";
}
```

它也可以与三元表达式一起使用来描述函数宏。

其他的是条件运算符。#ifdef、#elif 等。

为了向你展示头文件和额外 CPP 文件的用途，我们实际上将开始一个新项目，我们将这个项目命名为 Gradebook。信不信由！

这次我们将保留 main.cpp，你已经有足够的练习了。只需删掉 hello world 部分即可。

由于这是我们第一次在一个项目中使用多个文件，我将尽量让它看起来自明易懂。这将把我们目前为止使用的许多概念结合起来，在我们的主文件中产生一些非常漂亮且易于使用的代码，同时教你关于模块化的知识。

C++ 项目通常分为两个部分：接口（头文件）和它们的实现（C++ 文件）。接口旨在是可重用和扩展的。为了这个项目，我们将创建一个成绩单，在头文件的命名空间内存储我们的类数据，将重要函数存储在其他 C++ 文件中，并使用

无论如何，现在你去“文件 -> 新建 -> 空文件”。创建一个名为“gradebook.h”的文件。我们需要向预处理器抛出一些指令，所以这是我们要做的：

```cpp
#ifndef GRADEBOOK_H
#define GRADEBOOK_H

#endif
```

在 #define 和 #endif 指令之间，我们将创建主命名空间“gradebook”。在其中，我们将创建两个类：Assignment 和 Student。

- assignment 类应该有一个公共字段，包含：
    - 一个构造函数，接收一个用于作业名称的字符串和一个用于分数的浮点数
- 它应该有一个私有字段，包含：
    - 一个字符串：assignmentName
    - 一个浮点数：grade

- Student 类应该有一个公共字段，包含：
    - 一个接收学生名称字符串的构造函数
    - 一个将作业添加到作业 vector 中的中的函数，该函数接受该作业作为参数
    - 一个返回学生名称的函数
- 以及一个私有字段，包含：
    - 一个名为 grades 的 vector<Assignment>
    - 一个学生名称的字符串

## 你的代码看起来应该是这样的：

```cpp
#include <vector>
#include <string>

#ifndef GRADEBOOK_H
#define GRADEBOOK_H

using std::vector;
using std::string;

namespace gradebook {
    class Assignment {
    public:
        Assignment(std::string name, float grade) {
            this->assignmentName = name;
            this->grade = grade;
        }
    private:
        std::string assignmentName;
        float grade;
    };

    class Student {
    public:
        Student(std::string name) {
            this->name = name;
        }
        void addGrade(Assignment &assignment) {
            this->grades.push_back(assignment);
        }
        string getName() {
            return this->name;
        }
    private:
        std::vector<Assignment> grades;
        std::string name;
    };
}
#endif
```

头文件现在写完成了。

去“文件 -> 新建 -> 空文件”并将其命名为 load.cpp。

在此文件中，包含 iostream, vector 和你的头文件 "gradebook.h"。

你将使用 std::vector 和我们创建的命名空间中的 Student 类。通过输入 using gradebook::student 告诉编译器你正在使用。

在这里，我们想创建一个返回空内容的函数。将其命名为 loadStudents，让它接受一个学生 vector 作为参数。这里的想法是我们将从 main 发送一个 vector 并用学生填充它。

使用 vector<student>.push_back(Student()) 来填充它。

然而，如果我们想从文件读取学生而不是硬编码呢？

这就是我们的重载课程派上用场的地方。让我们创建一个名为 loadStudents 的第二个函数，它接收学生 vector 以及名为 filename 的字符串。在文件顶部包含 fstream，并在你的 load 文件中两个变量：一个 std::ifstream 变量和一个 std::string 变量。

打开文件，并将 filename 作为文件名。当还有行需要读取时，使用 vector<student>.push_back(Student()) 将学生读入 vector 中。它看起来应该是这样的：

```cpp
void loadStudents(vector<Student> &vec, std::string &filename) {
    std::ifstream file;
    std::string input;
    file.open(filename);
    while(getline(file, input))
        vec.push_back(Student(input));
    file.close();
}
```

搞定！我们现在有两个适用的 loadStudents 函数。

但等一下，我们还没有在主函数中使用它们。

你看，问题在于当你使用来自源文件的函数时，必须执行某种所谓的“前向声明”。

有两种方法可以实现：

1. 在 main.cpp 文件的开头声明，在 using 语句之后，主函数之前。
2. 在你的头文件中声明它。

我们将采用后者，因为它整洁得多。

所以我们进入头文件，在我们 gradebook 命名空间之后就是声明这些函数的地方。

```cpp
void loadStudent(vector<gradebook::Student> &vec);
loadStudent(vector<gradebook::Student> &vec, std::string &filename);
```

现在我们可以回到主文件，确保一切都按预期工作。

首先，创建一个名为 studentList 的新学生 vector。

调用 loadStudents 函数，将你创建的 vector 作为参数传递给它。



```cpp
for (Student s : studentList) {
  cout << s.getName() << "\n";
}
```

这是未来许多其他功能的跳板。

让我们现在尝试给学生布置一些作业吧，他们缺少这些。我们已经有了一个内置函数来处理这些，所以我们只需要找一个学生……等一下。在 `vector` 中查找学生有点困难。我们可以通过两种方式来修正这个问题，让那些必须在控制台周围操作的可怜老师们轻松一些。

第一种方案在用户端效率更高，所以我们用这个。让我们重新利用我们的循环，或者说是我们的 `cout` 语句。它现在会在学生名称旁边打印当前索引，这将告诉我们每个学生在 `vector` 中的位置。我们知道它们从 0 开始。所以我们可以定义一个从 0 开始的整数 `i`，它在每次循环循环时递增。我们的 `cout` 函数看起来应该是这样：

```cpp
cout << i << " : " << s.getName() << "\n";
```

之后，我们将测试这个功能。创建一个名为 `input` 的 `int`，然后通过 `cin` 运行它。输出 `studentList.at(input).getName()` 的值。编译并测试。它应该运行得很好，并且看起来像这样：

```cpp
#include <iostream>
#include <vector>
#include "gradebook.h"

using namespace std;
using gradebook::Student;

int main() {
    int i = 0, input;
    vector<Student> studentList;

    loadStudents(studentList);

    for (Student s : studentList) {
        cout << i << " : " << s.getName() << "\n";
        i++;
    }

    cin >> input;

    cout << studentList.at(input).getName();

    return 0;
}
```

如果一切顺利，那就太棒了。我们知道代码运行良好。现在我们需要做的是修改我们刚才的操作，以便以足够简单的方式输入分数？我们将修改那个 `cout` 语句，显示“Enter assignment name”。然后我们将接受一行输入并存储在名为 "assignmentName" 的 `string` 中，并通过 `cin` 过滤一个 `float` 变量 `grade`。为了简单起见，我们将使用标准输入 `cin`。听起来有点吓人，但它是有道理的且运行良好。到结束时，你的代码看起来大致如下：

```cpp
cin >> assignmentName >> grade;

Assignment a = Assignment(assignmentName, grade);

studentList.at(input).addGrade(a);
```

现在我们需要测试它。让我们进入 `assignment` 类并添加一种同时返回名称和分数的的方法。我们还需要进入 `student` 类并添加一种返回其作业 `vector`的方法。你的 `Assignment` 和 `Student` 类理想情况下应该是这样的：

```cpp
class Assignment {
public:
    Assignment(std::string name, float grade)
    {
        this->assignmentName = name;
        this->grade = grade;
    }
    string getName() {
        return assignmentName;
    }
    float getGrade() {
        return grade;
    }
private:
    std::string assignmentName;
    float grade;
};
```

```cpp
class Student {
public:
    Student(std::string name) {
        this->name = name;
    }
    void addGrade(Assignment &assignment) {
        this->grades.push_back(assignment);
    }
    std::vector<assignment> getGrades() {
        return this->grades;
    }
    string getName() {
        return this->name;
    }
private:
    std::vector<Assignment> grades;
    std::string name;
};
```

现在让我们好好利用它。编写一个 `cout` 函数，显示学生的名称，然后是作业名称，最后是该作业的分数。我的代码最后看起来像这样，你的也应该相似。它非常重，有很多方法可以让它看起来更舒服一些，但对于我们的目的来说，它是有效的。

```cpp
cout << "The student's name is: " <<
studentList.at(input) << ".\n"
<< "Their grade on assignment " <<
studentList.at(input).at(0).getName()
 << " was " <<
studentList.at(input).getGrades().at(0).getGrade();
```

有很多方法可以改进本指南，但这主要是为了向你展示 C++ 中模块化的多种用途以及命名空间（namespaces）等内容的巨大用处。你可以在几个循环内实现所有这些代码，如果你愿意，甚至可以为程序实现类似菜单的东西。这有很多可能性。整个章节的核心理由是向你展示 C++ 将大项目拆分为小块的巨大强大能力。

想象一下如果我们必须把所有这些都实在一个小程序的一个函数中会怎样？对于大约 3 行输入和极少的计算，代码将会有近 150 行。尽管如此，为程序拥有一个坚实的基础设施与任何事情一样重要。事实上，这正是面向对象编程的核心思想：为底层概念提供更好的基础设施和利用代码的更好方法。我本人是这一理念非常严格的遵循者——可以说是过头了！如果某物可以做成一个类或一个函数，我将总是这样做。

模块化的完美之处在于重用的潜力。你可以定义跨程序重用的函数或算法。这种模块化的绝佳例子就是游戏引擎。游戏引擎提供了许多重要功能，如图形、音频、接收键盘和控制器输入、运行循环以及

随着本节的完成，本书基本结束了。

# 结语

感谢你阅读《C++：从初学者到专家指南》，希望它具有启发性，并为你提供了实现目标所需的所有工具。下一步是在编程中应用你的知识。与任何事情一样，进步的终极方法是练习、练习再练习。我建议寻找开源项目并看看你可以从源码中分解出什么。思考一些有趣的项目——学习编程 GUI、制作基础网页浏览器、制作音乐播放器、编写游戏引擎——然后一步步地，首先将其拆解为你你熟悉的内容，然后在此基础上构建。例如，如果你想构建网页浏览器，你需要处理连接互联网以发送和接收数据，这超出了本书的范围。如果你想构建点对点聊天客户端，你需要处理建立到另一台计算机的直接隧道，以便你们可以在对方的控制台或聊天框直接对话。一旦你有了想做什么的想法，搜索关于如何做的教程——或者如果你想自己探索，寻找可以帮助你的 API，然后查看它们的文档以弄清楚如何使用它们。无论你最终做什么，提高任何事情的方法都是推自己一把并尽可能地练习，以成为该领域最好的自己。这本书只是开始。你现在已经掌握了 C++ 编程的基础知识，但未来的道路很漫长，每个项目都会有自己的问题和


需求。我只希望我已经为你做好了充分准备，以应对可能出现的任何问题。

最后，如果你觉得这本书很有帮助，欢迎在 Amazon 上给出评价，我们将不胜感激！

# Timothy Short 的其他书籍

- SQL：从入门到专家指南
- Linux：新手快速上手指南
- PowerShell：从入门到专家指南
- 区块链：掌握隐藏经济的全面指南
- 树莓派 3：从入门到专家指南
- WordPress：从入门到专家指南
- Shopify：从入门到专家指南
- 被动收入：财务自由终极指南
- 项目管理：从入门到专业经理及受人尊敬的领导者
- Evernote：简单化：精通时间管理与生产力

所有书籍可通过 amazon.com 获取

# C++

编程是当今经济中的一项基本技能。不要满足于平庸：《C++：从入门到专家指南》将教你所需的所有知识，让你在 C++ 领域打下良好基础，并开始创建精彩、响应迅速且可靠的程序。

在本书，我们将从最基础的内容开始——你的第一个 hello world 程序、变量等内容——一直到到高级的概念，如多态、继承和模块化。

如果你想成为最优秀的 C++ 程序员并对自己的领域了如指掌，这本书将是你极佳的起点。如果你下载了《C++：从入门到专家指南》，你绝对不会失望。相反，你将发现许多以前所未接触的知识。

学习 C++ 将对你的职业生涯大益，让你开启一系列全新的爱好，并使你能够进行批判性和逻辑性的思考——特别是在计算方面。

![](img/bde7f8c00e4b9a8e19781b9fbd51576a_107_0.png)

![](img/bde7f8c00e4b9a8e19781b9fbd51576a_107_1.png)

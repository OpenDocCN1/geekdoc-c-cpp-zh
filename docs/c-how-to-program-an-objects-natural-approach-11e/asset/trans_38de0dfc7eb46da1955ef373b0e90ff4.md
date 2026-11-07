
### std 命名空间

当我们使用从标准库头文件（如 <iostream>）引入程序的名称时，cout 前面的 std:: 是必需的。记号 std::cout 表明我们使用的是名称 cout，它属于命名空间 std。^1 我们将在第 16 章讨论命名空间。目前，在每次提到 cout 时都要在前面加上 std::。我们很快会介绍 using 声明和 using 指令，它们使你能够在每次使用 std 命名空间中的名称时省略 std::。

1\. 我们把“std::”读作“standard”，而不是读作单个字母 s、t 和 d。

### 流插入运算符与转义序列

与 cout 一起使用时，<< 运算符是流插入运算符。运算符右侧的值（右操作数）被插入到输出流中。注意，<< 指向数据要去的位置。字符串的字符通常完全按照引号内键入的内容显示。然而，在图 2.1 的输出中不会显示字符 `\n`。反斜杠（`\`）是转义字符。当 C++ 在字符串中遇到反斜杠时，会将下一个字符与反斜杠组合成转义序列。转义序列 `\n` 表示换行。它使光标——即当前屏幕位置指示器——移动到屏幕上下一行的开头。下表列出了一些常见的转义序列：

| 转义序列 | 说明 |
| --- | --- |
| `\n` | 换行。将屏幕光标定位到下一行的开头。 |
| `\t` | 水平制表。将屏幕光标向右移动到下一个制表位。 |
| `\r` | 回车。将屏幕光标定位到当前行的开头；不前进到下一行。 |
| `\a` | 警报。发出系统响铃声。 |
| `\\` | 反斜杠。在字符串中包含一个反斜杠字符。 |
| `\'` | 单引号。在字符串中包含一个单引号字符。 |
| `\"` | 双引号。在字符串中包含一个双引号字符。 |

### return 语句

第 9 行

```cpp
return 0; // indicate that program ended successfully
```

是我们将用来退出函数的几种方式之一。在 main 末尾的这个 return 语句中，值 0 表示程序成功终止。如果程序执行到达右花括号时没有遇到 **return 语句**，则 main 函数会隐式返回 0。因此，在后续成功终止的程序中，我们省略 main 的 return 语句。

### 检查点

- 1. *（填空）* 空行、空格和制表符统称为 ______，并且通常会被编译器忽略。  
  **答案：** 空白字符。
- 2. *（代码）* 编写一条语句，输出字符串“Hello world”，然后将光标移到下一行的开头。

  ```cpp
  std::cout << "Hello World\n";  // display message
  ```
- 3. *（对/错）* 下面的语句在 `main` 末尾执行时，表示程序没有正确执行：

  ```cpp
  return 0;
  ```

  **答案：** 错。该语句表示程序成功执行。

## 2.3 修改我们的第一个 C++ 程序

接下来的两个示例修改图 2.1 的程序。第一个使用多条语句在一行上显示文本。第二个使用一条语句在多行上显示文本。

### 用多条语句显示一行文本

图 2.2 在多条语句（第 7—8 行）中执行流插入，却产生与图 2.1 相同的输出。每次流插入都从上一个流插入停止的位置继续显示。第 7 行显示 Welcome，后跟一个空格。该字符串没有以 `\n` 结尾，因此第 8 行紧跟在空格之后在同一行开始显示。

```cpp
// fig02_02.cpp
// Displaying a line of text with multiple statements.
#include <iostream> // enables program to output data to the screen

// function main begins program execution
int main() {
    std::cout << "Welcome ";
    std::cout << "to C++!\n";
} // end function main
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_128_0.png)

**图 2.2** | 用多条语句显示一行文本。

### 用一条语句显示多行文本

一条语句可以通过使用额外的换行符来显示多行，如图 2.3 的第 7 行所示。每当在输出流中遇到 `\n`（换行）转义序列时，光标就定位到下一行的开头。要在输出中得到一个空行，请将两个换行符背靠背放置，如第 7 行所示。

```cpp
// fig02_03.cpp
// Displaying multiple lines of text with a single statement.
#include <iostream> // enables program to output data to the screen

// function main begins program execution
int main() {
    std::cout << "Welcome to C++!\n\n";
} // end function main
```

**图 2.3** | 用一条语句显示多行文本。（第 1 部分，共 2 部分。）

![](img/7b5e2088e71c7f78681d4ddbcf104c06_129_0.png)

**图 2.3** | 用一条语句显示多行文本。（第 2 部分，共 2 部分。）

### 检查点

- 1. *（对/错）* 下面的语句显示字符串 `"Hello"`，然后将输出光标定位到下一行。

  `std::cout << "Hello";`

  **答案：** 错。该语句显示字符串 `"Hello"`，并将输出光标留在 `"Hello"` 中的 `o` 之后。
- 2. *（对/错）* 一条语句可以通过使用额外的换行符显示多行。

  **答案：** 对。
- 3. *（代码）* 编写一条输出单个字符串的语句，显示以下内容，并将输出光标定位在新的一行：

  ```text
  Hello

  World
  ```

  **答案：** `std::cout << "Hello\n\nWorld\n";`

## 2.4 另一个 C++ 程序：整数相加

我们的下一个程序获取用户在键盘上输入的两个整数，计算它们的和，并使用 `std::cout` 输出结果。图 2.4 显示了该程序以及示例输入和输出。在示例执行中，我们的约定是用**粗体**显示用户的输入。

```cpp
// fig02_04.cpp
// Addition program that displays the sum of two integers.
#include <iostream> // enables program to perform input and output

// function main begins program execution
int main() {
    // declaring and initializing variables
    int number1{0}; // first integer to add (initialized to 0)
    int number2{0}; // second integer to add (initialized to 0)
    int sum{0}; // sum of number1 and number2 (initialized to 0)

    std::cout << "Enter first integer: "; // prompt user for data
    std::cin >> number1; // read first integer from user into number1

    std::cout << "Enter second integer: "; // prompt user for more data
    std::cin >> number2; // read second integer from user into number2
```

**图 2.4** | 显示两个整数之和的加法程序。（第 1 部分，共 2 部分。）

C++ 基本类型名称通常由一个或多个关键字组成，并且必须全部使用小写字母。有关 C++ 基本类型及其取值范围的完整列表，请参见 https://en.cppreference.com/w/cpp/language/types

### 标识符与驼峰式命名

变量名（例如 number1）可以是任何有效的标识符。标识符是由字母、数字和下划线（_）组成的一系列字符，不能以数字开头，也不能是关键字。C++ 区分大小写——大写字母和小写字母不同。因此，a1 和 A1 是不同的标识符。

C++ 允许任意长度的标识符。不要用下划线加大写字母或两个下划线作为标识符的开头。C++ 编译器会在内部将这些名称用于自身目的。

按照惯例，变量名标识符以小写字母开头，名称中第一个单词之后的每个单词都以大写字母开头。例如，firstNumber 的第二个单词 Number 以大写 N 开头。这种命名约定称为驼峰式命名法，因为大写字母像骆驼的驼峰一样突出。选择有意义的标识符有助于使程序自我说明——人们只需阅读程序就能理解它，而不必参考程序注释或外部文档。避免在标识符中使用缩写。虽然这可能需要你多敲一些键，但它提高了程序的可读性。

### 变量声明的位置

变量声明几乎可以放在程序中的任何位置，但必须出现在变量使用之前。例如，第 8 行中的声明

```cpp
int number1{0}; // first integer to add (initialized to 0)
```

本可以紧挨着第 13 行之前放置：

```cpp
std::cin >> number1; // read first integer from user into number1
```

第 9 行中的声明：

```cpp
int number2{0}; // second integer to add (initialized to 0)
```

本可以紧挨着第 16 行之前放置：

```cpp
std::cin >> number2; // read second integer from user into number2
```

以及第 10 行中的声明：

```cpp
int sum{0}; // sum of number1 and number2 (initialized to 0)
```

本可以紧挨着第 18 行之前放置：

```cpp
sum = number1 + number2; // add the numbers, store result in sum
```

事实上，第 10 行和第 18 行可以合并为下面的声明，并放在第 20 行之前：

```cpp
int sum{number1 + number2}; // initialize sum with number1 + number2
```

### 从用户处获取第一个值

第 12 行

```cpp
std::cout << "Enter first integer: "; // prompt user for data
```

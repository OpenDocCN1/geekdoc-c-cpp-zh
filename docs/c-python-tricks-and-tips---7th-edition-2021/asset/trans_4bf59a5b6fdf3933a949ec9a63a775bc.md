
## 计数循环

请记住，在 Python 中，循环不会计入你在 range 中指定的最后一个数字。因此，如果你希望循环从 1 计数到 10，就需要使用：

```python
n = list(range(1, 11))
```

这将返回 1 到 10。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_70_0.png)

## 区分大小写

Python 是一种区分大小写的编程语言，因此你需要检查你分配的任何变量。例如，`Lives=10` 与 `lives=10` 是不同的变量；在代码中调用错误的变量可能会导致意外结果。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_70_1.png)

## 括号

每个人都会忘记在语句末尾补上本应添加的那个额外括号。Python 依赖例程中右括号与左括号数量相等，因此代码中的任何错误都可能是因为你忘记数括号，包括方括号。

```python
def print_game_status(self):
    print (board[len(self.missed_letters)])
    print ('Word: ' + self.hide_word())
    print ('Letters Missed: ',)
    for letter in self.missed_letters:
        print (letter,)
    print ()
    print ('Letters Guessed: ',)
    for letter in self.guessed_letters:
        print (letter,)
    print ()
```

## 冒号

初学者常常忘记在结构语句末尾添加冒号，例如：

```
class Hangman:
def guess(self, letter):
```

等等。冒号用于分隔代码，并创建后续代码所属的缩进。

```python
class Hangman:
    def __init__(self,word):
        self.word = word
        self.missed_letters = []
        self.guessed_letters = []

    def guess(self,letter):
        if letter in self.word and letter not in self.guessed_letters:
            self.guessed_letters.append(letter)
        elif letter not in self.word and letter not in self.missed_letters:
            self.missed_letters.append(letter)
        else:
            return False
        return True

    def hangman_over(self):
        return self.hangman_won() or (len(self.missed_letters) == 6)

    def hangman_won(self):
        if '_' not in self.hide_word():
            return True
        return False

    def hide_word(self):
        rtn = ''
        for letter in self.word:
            if letter not in self.guessed_letters:
                rtn += '_'
            else:
                rtn += letter
        return rtn
```

## 运算符

使用错误的运算符也是常见的错误。例如，当你在两个值之间进行比较时，需要使用相等运算符（双等号，`==`）。使用单个等号（`=`）是赋值运算符，用于将值赋给变量（例如，`lives=10`）。

```python
b = 5
c = 10
d = 10
b == c #false because 5 is not equal to 10
c == d #true because 10 is equal to 10
```

## 操作系统

为多个平台编写代码很困难，尤其是当你开始使用操作系统的外部命令时。例如，如果你的代码要求清屏，那么在 Windows 中你会使用 `cls`。而在 Linux 中，你需要使用 `clear`。你需要通过捕获错误并用替代命令来处理它，从而解决这个问题。

```python
# Code to detect error for using a different OS
run=1
while(run==1):
    try:
        os.system('clear')
    except OSError:
        os.system('cls')
    print('\n>>>>>>>>>>Python 3 File Manager<<<<<<<<<<\n')
```

## C++ 初学者的错误

C++ 开发者可能会遇到许多陷阱，尤其是因为这是一门更复杂、且往往不留情面的语言，掌握起来并不容易。初学者需要一步一步地学习 C++，并在继续之前消化所学内容。

### 常见的 C++ 错误

诚然，犯下我们这些页面中概述的这类错误的并不只有 C++ 初学者；即使是经验丰富的程序员也偶尔会出些差错。以下是一些需要尝试避免的常见问题。

### 未声明的标识符

一个常见的 C++ 错误——老实说，也是大多数编程语言中的常见错误——是你试图输出一个不存在的变量。在屏幕上显示 x 的值没问题，但前提是你已经告诉编译器 x 的值最初是什么。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_0.png)

### std 命名空间

初学者在整个代码中引用标准库很常见，但如果你漏掉语句中的 std:: 部分，代码在编译时就会报错。你可以通过添加以下内容来解决：

```cpp
using namespace std;
```

在 #include 部分下方添加，然后从此以后直接使用 cout、cin 等即可。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_1.png)

### 分号

请记住，C++ 程序的每一行都必须以分号结尾。如果没有，编译器会把缺少分号的那一行与下一个分号所在行视为同一行。这会在编译时造成各种各样的问题，所以不要忘记这些分号。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_2.png)

### GCC 或 G++

如果你在 Linux 中编译，那么无疑会遇到 gcc 和 g++。简而言之，gcc 是 GNU 编译器集合（过去称为 GNU C 编译器），而 g++ 是该编译器的 GNU C++（C++ 版本）。如果你要编译 C++，就需要使用 g++，否则会使用错误的编译器驱动程序。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_71_3.png)

### 注释（再次）

确实，从不对代码做任何注释这一错误又回来了。正如我们之前所抱怨的那样，代码中缺少可读的标识符会让你和其他人都很难回顾它当初是如何工作的。请多使用注释。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<double> v;
    double d;
    while (cin >> d) v.push_back(d);    // read elements
    if (cin.eof()) {                    // check if input failed
        cerr << "format error\n";       // error return
        return 1;
    }

    cout << "read " << v.size() << " elements\n";
    reverse(v.begin(), v.end());
    cout << "elements in reverse order:\n";
    for (int i = 0; i < v.size(); ++i) cout << v[i] << '\n';

    return 0;                           // success return
}
```

### 引号

缺少引号是各个水平用户都会犯的常见错误。请记住，引号需要括住字符串，以及例如要输出到屏幕或文件中的任何内容。大多数编译器错误都是由于代码中缺少引号造成的。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_72_0.png)

### 多余的分号

虽然 C++ 的每一行末尾都需要有分号，但这条规则也有一些例外。分号需要位于每个完整语句的末尾，但有些代码行并不是完整语句。例如：

```text
#include
if lines
switch lines
```

如果听起来令人困惑，不用担心，编译器会让你知道哪里出错了。

```cpp
// Program to print positive number entered by the user
// If user enters negative number, it is skipped

#include <iostream>
using namespace std;

int main()
{
    int number;
    cout << "Enter an integer: ";
    cin >> number;

    // checks if the number is positive
    if (number > 0)
    {
        cout << "You entered a positive integer: " << number << endl;
    }

    cout << "This statement is always executed.";
    return 0;
}
```

### 花括号过多

花括号（或称大括号）是代码块的开头和结尾标记。因此，每一个 `{` 都必须有一个对应的 `}`。在编写代码时，很容易多包含或漏掉其中一个配对的括号；这通常发生在使用文本编辑器编写代码时，因为 IDE 会自动为你添加它们。

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    string mystring = "This is a string!\n";
    cout << "What's the value of x? ";
    cin >> x;
    cout << x;
    {
        cout << "\n\n";
        cout << mystring;
    }
}
```

### 初始化变量

在 C++ 中，变量默认不会初始化为零。这意味着如果你创建一个名为 x 的变量，那么它可能被赋予一个从 0 到 18,446,744,073,709,551,616 的随机数，这会很难纳入方程中。创建变量时，请先给它赋值为零：x=0。

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x;
    x=0;

    cout << x;
}
```

### a.out

在 Linux 中编译时的一个常见错误是，编译后忘记给 C++ 代码命名。当你从终端编译时，会输入：

```bash
g++ code.cpp
```

这会编译文件 code.cpp 中的代码，并创建一个可通过 ./a.out 执行的 a.out 文件。但是，如果 a.out 中已经有代码，那么它会被覆盖。请使用：

```bash
g++ code.cpp -o nameofprogram
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_72_1.png)


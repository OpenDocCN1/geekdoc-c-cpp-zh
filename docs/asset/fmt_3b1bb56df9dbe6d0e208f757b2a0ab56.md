
## 字符函数

`int isalpha(int x);` 参数为字母？

`int iscntrl(int x);` 参数为控制字符？

`int isdigit(int x);` 参数为十进制数字（0 到 9）？

`int isgraph(int x);` 参数为空格以外的可打印字符？

`int islower(int x);` 参数为小写字母（a 到 z）？

`int isprint(int x);` 参数为可打印字符（包括空格）？

`int ispunct(int x);` 参数为标点符号？

`int isspace(int x);` 参数为空白字符（空格、返回或制表符）？

`int isupper(int x);` 参数为大写字母（A 到 Z）？

`int isxdigit(int x);` 参数为十六进制字符（0–9, a–f, A–F）？

### 程序 6.5 使用字符函数

```cpp
// 一个将每个小写字母转换为大写字母并统计字母字符的程序。
#include <iostream>
#include <ctype>
using namespace std;

int main() {
    // 声明
    char ch;
    int count = 0;
    // 输入字符并处理
    while (cin >> noskipws) {
        if (isalpha(ch)) {
            count++;
        }
        ch = toupper(ch);
        cout << ch;
    }
    // 打印字符计数
    cout << "The count of alphabetic characters is: " << count;
    return 0;
}
```

运行：

这是一行超过10个字符的文本。

THIS IS A LINE MADE OF MORE THAN 10 CHARACTERS.

^Z
The count of alphabetic characters is: 35

## 6.2.3 处理时间

我们在 C++ 编程中遇到的库函数之一是定义在 `<ctime>` 头文件中的 `time` 函数。我们将在将在附录 I 中详细讨论该函数，但目前，只需要知道，当传递给函数的参数为 0 时，该函数返回从 Unix 纪元（1970 年 1 月 1 日午夜）以来经过的秒数。换句话说，`time(0)` 给出了从纪元到调用该函数时的秒数计数，如图 6.5 所示。

要找到当前时间的日期、月份和年份，我们需要更复杂的函数，我们将在后续章节中进行讨论（必须考虑闰年）。然而，找到当前的小时、分钟和秒是很的，如下一个示例所示。

## 6.2 库函数 221

**图 6.5** 由 `time(0)` 函数定义的秒数

### 示例 6.8

程序 6.6 显示了如何使用 `time(0)` 函数打印当前时间。我们需要知道计算的时间是格林威治标准时间 `GMT`，而不是本地时间。

注意程序 6.6 中 `/` 和 `%` 运算符的使用。第一个结束当前单位；第二个结束当前单位。请注意，如果你想找到你所在位置当前时间，必须加减本地时间与 `GMT` 时间之间的差异。

## 6.2.4 随机数生成

C++ 11 引入了标准类，用于根据概率论中定义的任何分布创建随机数。我们将在书的后部分讨论这些。在本章中，我们

### 程序 6.6 查找当前时间

```cpp
/******************************************************
 * 一个使用 time(0) 函数查找当前时间的程序 *
****************************************************************/
#include <iostream>
#include <ctime>
using namespace std;
int main() {

    // 查找经过的秒和当前秒
    long elapsedSeconds = time(0);
    int currentSecond = elapsedSeconds % 60;
    // 查找经过的分钟和当前分钟
    long elapsedMinutes = elapsedSeconds / 60;
    int currentMinute = elapsedMinutes % 60;
    // 查找经过的小时和当前小时
    long elapsedHours = elapsedMinutes / 60;
    int currentHour = elapsedHours % 24;
    // 打印当前时间
    cout << "Current time: " << endl;
    cout << currentHour << ":" << currentMinute << ":" << currentSecond << endl;
    return 0;
}
```

运行：

Current time: 20 : 57 : 52

运行：

Current time: 20 : 58 : 22

## 第 6 章 函数

缩放

```cpp
temp = rand() % (b - a + 1)
```

偏移

```cpp
result = temp + a
```

**图 6.6** 随机数的缩放和偏移

我们引入继承自 C 语言并定义在 `<stdlib>` 中的随机数生成器，它生成一个 0 到 `RAND_MAX` 之间的随机整数，该值取决于系统，但通常设置为 32,767 `$2^{15}-1$`，这意味着如果包含 0，就有 32,768 个值。

该函数是伪随机的：它在程序的每次运行中都会生成相同的随机数集合，因为它使用相同的*种子* `seed` 来启动随机序列。种子被设置为 1，为了在每次运行中获得不同的序列，我们每次运行程序时必须给函数一个不同的种子。最好的选择是使用自纪元以来的秒数，这是我们讨论过的。每次我们运行程序，`time(0)` 的值都会变化，这意味着 `time(0)` 传递给 `srand` 函数可以得到不同的随机数。

### 示例 6.9

通过生成随机数来模拟猜数字游戏，我们在两个限制 `low` 和 `high` 之间生成一个随机数，让用户给出数字。正如程序 6.7 所示，如果数字不正确，我们会给用户提示。

### 程序 6.7 使用随机数的猜数字游戏

```cpp
#include <stdlib>
#include <ctime>
using namespace std;
int main() {
    // 声明和初始化
    int low = 5;
    int guess = 15;
    int tryLimit = 5;
    int guess;
    // 随机数的生成
    srand(time(0));
    int temp = rand();
    int num = temp % (high - low) + low;
    // 猜数字循环
    int counter = 1;
    bool found = false;
    while (counter <= tryLimit) {
        do {
            cout << "Enter your guess between 5 to 15 (inclusive): ";
            cin >> guess;
        } while (guess < 5 || guess > 15);
        {
            if (guess == num) {
                found = true;
            } else if (guess > num) {
                cout << "Your guess was high!" << endl;
            } else {
                cout << "Your guess was low!" << endl;
            }
            counter++;
        }
    }
    // 成功响应
    if (found) {
        cout << "Congratulation. You found it. ";
        cout << "The number was: " << num;
    } else {
        cout << "Sorry, you did not find it! ";
        cout << "The number was: " << num;
    }
    return 0;
}
```

运行：

输入 5 到 15 之间的数字：7

你猜的太小了！

输入 5 到 15 之间的数字：8

恭喜。你找到了。数字是：8

运行：

输入 5 到 15 之间的数字：15

你猜的太大了！

输入 5 到 15 之间的数字：14

你猜的太大了！

输入 5 到 15 之间的数字：13

你猜的太大了！

输入 5 到 15 之间的数字：12

你猜的太大了！

输入 5 到 15 之间的数字：10

你猜的太大了！

抱歉，你没有找到！数字是：10

## 无参数的 void 函数

最简单的情况可能是无参数的 **void 函数**。该函数不接受任何参数且不返回任何内容。这种函数的定义仅是为了它的副作用 `side effect`，副作用发生在函数内部；否则，该函数是毫无用处的。由于函数没有返回值，我们无法在需要值的地方使用它。我们只能将此函数作为前缀表达式使用，其中利用它的副作用。

### 示例 6.10

让我们创建一个无参数的 void 函数，它在屏幕上打印一条消息（例如问候语）（副作用），如程序 6.8 所示。注意，我们为函数定义使用了不同的背景颜色。同样请注意，函数定义（第 13 到 19 行）在 *main* 函数中位于函数调用（第 23 行）之之前。事实上，我们有两个函数定义，一个是 *greeting* 函数，另一个是 *main* 函数。*greeting* 函数是在 *main* 函数内部被调用的；*main* 函数则由 C++ 运行器调用。

### 程序 6.8 使用无参数的 void 函数

```cpp
/****************************************************/
* 一个程序使用 void 函数打印带框的问候语
*****************************************************/
#include <iostream>
using namespace std;
/*
* greeting 函数的函数定义。这是一个无参数的 void
* 函数，它创建了一个三行的消息。
* 该函数不向其调用者返回任何内容。它只有副作用
* 副（显示三行内容）
*************************************************/
void greeting () {
    cout <<"********************" << endl;
    cout <<"* Hello Friends **" << endl;
    cout <<"********************";
    return;
}
int main () {
    greeting(); // 调用 greeting 函数（表达式语句）
    return 0;
}
```

运行:

*********************************

* Hello Friends *

*********************************

```cpp
int main () {
    greeting();
    return 0;
}

void greeting () {
    cout << "side effect";
    return;
}
```

**图 6.8** `main` 函数与 `greeting` 函数之间的通信

图 6.8 显示了 *main* 函数与 *greeting* 函数之间的通信。尽管在 *main* 和 *greeting* 函数之间没有数据交换，但存在副作用。`main` 函数首先调用 *greeting* 函数。*greeting* 函数在屏幕上打印问候语（副作用）。随后控制权返回到 `main` 函数（void 返回）。

## 带参数的 void 函数

下一个选择是创建一个带参数的函数。该函数接收传递的值（参数），这些值占据参数的位置。该函数有副作用，但不向其调用者返回数据。当我们只需要函数的副作用，但又需要传递某些信息（例如每次调用函数时要输出什么）时，就会使用这种函数。正如我们稍后将看到的，带参数的 void 函数是输入输出设计模块的良好选择。

### 示例 6.11

程序 6.9 显示了一个示例，参数告知如何格式化执行时的模式。第 14 到 25 行是函数定义；38 行是函数调用。

### 程序 6.9 带参数的 void 函数

```cpp
/************************************************************************
* 此程序展示了我们如何使用带参数的 void
* 函数创建不同的模式。
*********************************************************************/
#include <iostream>
using namespace std;
/************************************************************************
* pattern 函数的函数定义。这是一个带有一个参数的 void
* 函数，在每次调用程序时从用户处接收其大小。
* 参数被用于为模式创建
*不同的的大小。
*********************************************************************/
void pattern (int size) {
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++)
```

运行

输入模式的大小: 3

***

***

***

***

运行

输入模式的大小: 4

****

****

****

****

图 6.9 显示了 `main` 和 `pattern` 函数之间的通信。每当我们运行程序，都会得到一个 `patternSize` 的值，并将该值传递给函数调用，以控制打印模式的大小。

## 无参数的返回值函数

这种类型的函数是为了副作用设计的，并向调用函数返回值。正如我们稍后将看到的，它是输入输出设计模块的良好选择。程序 6.10 展示了这一点。

```cpp
int main () {
    greeting();
    return 0;
}

void greeting () {
    cout << "side effect";
    return;
}
```

**图 6.8** `main` 函数与 `greeting` 函数之间的通信

图 6.8 显示了 *main* 函数与 *greeting* 函数之间的通信。尽管 *main* 和 *greeting* 函数之间没有数据交换，但存在副作用。`main` 函数首先调用 *greeting* 函数。*greeting* 函数在屏幕上打印问候语（副作用）。

## 无参数的返回值函数

这种类型的函数是为了副作用设计的，并向调用函数返回值。正如我们稍后将看到的，它是输入输出设计模块的良好选择。程序 6.10 展示了它。

### 程序 6.10 无参数的返回值函数

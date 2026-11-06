

### 第一位数字 = 6

最后剩下的数字，恰好是第一位数字，是

```cpp
digit1 = (int)(67 / 10);
```

该算法的 C++ 程序如下所示。

### project_13_1_2c

```cpp
#include <iostream>
using namespace std;

int main() {
    int digit1, digit2, digit3, digit4, number, r, sum;

    cout << "Enter a four-digit integer: ";
    cin >> number;

    digit4 = number % 10;
    r = (int)(number / 10);

    digit3 = r % 10;
    r = (int)(r / 10);

    digit2 = r % 10;
    digit1 = (int)(r / 10);

    sum = digit1 + digit2 + digit3 + digit4;
    cout << sum;
    return 0;
}
```

为了进一步帮助你，还有一个通用 C++ 程序，可用于拆分任何给定的整数。该程序使用第二种方法。再一次说明，由于程序的长度取决于数字的位数 N，你只需编写 N-1 对语句。

```cpp
cout << "Enter a N-digit integer: ";
cin >> number;
```

![](img/7b41666e32fdead550ef74cdd9f6ead0_146_0.png)

```cpp
digit2 = r % 10;
digit1 = (int)(r / 10);
```

![](img/7b41666e32fdead550ef74cdd9f6ead0_147_0.png)

例如，如果要拆分一个五位数整数，必须使用四对语句。

### project_13_1_2d

```cpp
#include <iostream>
using namespace std;

int main() {
    int digit1, digit2, digit3, digit4, digit5, number, r;

    cout << "Enter a five-digit integer: ";
    cin >> number;

    digit5 = number % 10;
    r = (int)(number / 10);

    digit4 = r % 10;
    r = (int)(r / 10);

    digit3 = r % 10;
    r = (int)(r / 10);

    digit2 = r % 10;
    digit1 = (int)(r / 10);

    cout << digit1 << ", " << digit2 << ", " << digit3 << endl;
    cout << digit4 << ", " << digit5 << endl;
    return 0;
}
```

![](img/7b41666e32fdead550ef74cdd9f6ead0_147_1.png)

### 练习 13.1-3 *显示经过的时间*

*编写一个 C++ 程序，提示用户输入一个表示经过时间（以秒为单位）的整数，然后按“DD 天 HH 小时 MM 分钟和 SS 秒”的格式显示。例如，如果用户输入 700005，则必须显示消息“8 天 2 小时 26 分钟和 45 秒”。*

### 解法

你可能已经知道，一分钟有 60 秒，一小时有 3600 秒，一天有 86400 秒。

让我们尝试用第一种方法分析数字 700005。

| 结果 | 解释 |
|---|---|
| **天数 = 8** | 如果将给定整数除以 86400 得到整数商，就可以分离出天数<br>`days = (int)(700005 / 86400);` |
| **剩余秒数 = 8805** | 如果将给定整数除以 86400 得到整数余数，就可以分离出剩余秒数<br>`r = 700005 % 86400;` |
| **小时 = 2** | 如果将剩余秒数除以 3600 得到整数商，就可以分离出小时数<br>`hours = (int)(8805 / 3600);` |
| **剩余秒数 = 1605** | 现在的剩余秒数为<br>`r = 8805 % 3600;` |
| **分钟 = 26** | 如果将剩余秒数除以 60 得到整数商，就可以分离出分钟数<br>`minutes = (int)(1605 / 60);` |
| **秒 = 45** | 最后一个余数，也就是剩余的秒数，为<br>`seconds = 1605 % 60;` |

该算法的 C++ 程序如下。

```cpp
// project_13_1_3
#include <iostream>
using namespace std;

int main() {
    int days, hours, minutes, number, r, seconds;

    cout << "Enter a period of time in seconds: ";
    cin >> number;

    days = (int)(number / 86400);   // 60 * 60 * 24 = 86400
    r = number % 86400;

    hours = (int)(r / 3600);        // 60 * 60 = 3600
    r = r % 3600;

    minutes = (int)(r / 60);
    seconds = r % 60;

    cout << days << " days " << hours << " hours " << endl;
    cout << minutes << " minutes and " << seconds << " seconds";
    return 0;
}
```

### 练习 13.1-4 — 反转一个数

编写一个 C++ 程序，提示用户输入一个三位数整数，然后将其反转。例如，如果用户输入数字 375，则应显示数字 573。

### 解法

要分离出给定数字的三位数字，可以使用第一种或第二种方法。之后，本练习唯一的难点是构造反转后的数字。以数字 375 为例。分离后的三个数字是

```cpp
digit1 = 3;
digit2 = 7;
digit3 = 5;
```

你可以通过简单地计算乘积之和来构造反转后的数字：

digit3 × 100 + digit2 × 10 + digit1 × 1

换个方式，你可以使用第二种方法拆分给定的数字。该 C++ 程序如下所示。

### project_13_1_4

```cpp
#include <iostream>
using namespace std;

int main() {
    int digit1, digit2, digit3, number, r, reversed;

    cout << "Enter a three-digit integer: " << endl;
    cin >> number;

    digit3 = number % 10;        // This is the rightmost digit
    r = (int)(number / 10);

    digit2 = r % 10;             // This is the digit in the middle
    digit1 = (int)(r / 10);      // This is the leftmost digit

    reversed = digit3 * 100 + digit2 * 10 + digit1;
    cout << reversed;
    return 0;
}
```

## 13.2 复习练习

完成以下练习。

- 1. 编写一个 C++ 程序，提示用户输入任意整数，然后将其最后一位数字乘以 8 并显示结果。
  提示：可以使用对 10 取模运算分离出任意整数的最后一位数字。
- 2. 编写一个 C++ 程序，提示用户输入一个五位数整数，然后将其反转。例如，如果用户输入数字 32675，则必须显示数字 57623。
- 3. 编写一个 C++ 程序，提示用户输入一个整数，然后当该数为奇数时显示 1；否则显示 0。尽量不要使用任何决策控制结构，因为你还没有学过它们！
- 4. 编写一个 C++ 程序，提示用户输入一个整数，然后当该数为偶数时显示 1；否则显示 0。尽量不要使用任何决策控制结构，因为你还没有学过它们！
- 5. 编写一个 C++ 程序，提示用户输入一个表示经过时间（以秒为单位）的整数，然后按“WW 周 DD 天 HH 小时 MM 分钟和 SS 秒”的格式显示。例如，如果用户输入数字 2000000，则应显示消息“3 周 23 天 3 小时 33 分钟和 20 秒”。
- 6. 一台 ATM 银行机内有 $20、$10、$5 和 $1 的纸币。编写一个 C++ 程序，提示用户输入其想要取出的金额（使用整数值），然后显示 ATM 应给出的最少纸币张数。例如，如果用户输入金额 $76，程序应显示消息“3 张 $20、1 张 $10、1 张 $5 和 1 张 $1”。
- 7. 一个机器人抵达月球以执行一些实验。机器人每一步长 25 英寸。编写一个 C++ 程序，提示用户输入机器人行走的步数，然后计算并显示以英里、英尺、码和英寸表示的行进距离。例如，如果行进距离为 100000 英寸，程序应显示消息“1 英里、1017 码、2 英尺和 4 英寸”。

已知：

- 1 英里 = 63360 英寸
- 1 码 = 36 英寸
- 1 英尺 = 12 英寸

## 第 14 章：操作字符串

### 14.1 引言

一般来说，字符串是你可以使用键盘输入的任何内容，包括字母、符号（例如 &、* 和 @）以及数字。有时程序会处理以字符串（文本）形式出现的数据。在 C++ 中，字符串总是像这样用双引号括起来：“ ”。

下一个示例中的每条语句都会输出一个字符串。

```cpp
#include <iostream>
using namespace std;

int main() {
  cout << "Everything enclosed in double quotes is a ";
  cout << "string, even the numbers below" << endl;
  cout << "3, 4, 7" << endl;
  cout << "You can even mix letters, symbols and ";
  cout << "numbers like this:" << endl;
  cout << "The result of 3 + 4 equals to 7";
  return 0;
}
```

字符串无处不在——从文字处理软件到网页浏览器，再到短信程序。本书中的许多练习实际上大量使用了字符串。尽管 C++ 支持许多用于操作字符串的有用函数，但本章只涵盖对本书目的绝对必要的那些函数。不过，如果你需要更多信息，可以访问

http://www.cplusplus.com/reference/string/string/

> **注意：** 当有需要时，可以使用 C++ 字符串函数，例如从字符串中分离出若干字符、删除字符串开头可能存在的空格，或将字符串中的所有字符转换为大写。
>
> **记住！** 函数只不过是解决小问题的小型子程序。子程序可以定义为一个语句块，它被打包为一个单元，具有名称并执行特定任务。

此外，尽管 C++ 支持许多有用的字符串函数，但本书使用的一些函数并不属于标准 C++；相反，它们定义在 Boost C++ 库中。在这种情况下，每个使用这些函数中任意一个的 C++ 项目都必须包含这些库。如果从主菜单中选择“文件→项目属性”，并在“C++ 编译器”类别中包含 Boost C++ 库的目录（文件夹），如 **图 14-1** 所示，即可完成此操作。


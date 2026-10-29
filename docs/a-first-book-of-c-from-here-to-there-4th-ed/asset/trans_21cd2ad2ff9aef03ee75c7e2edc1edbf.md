

# 表 14.7 C 字符串转换函数

| 函数 | 描述 | 示例 |
|---|---|---|
| int atol(stringExp) | 将 stringExp 转换为整数。转换在第一个非整数字符处停止。 | atoi("1234") |
| double atof(stringExp) | 将 stringExp 转换为双精度数。转换在第一个无法解释为双精度的字符处停止。 | atof("12.34") |
| char[] itoa(integerExp) | 将 integerExp 转换为字符数组。分配给返回字符的空间必须足够容纳转换后的值。 | itoa(1234) |

下面的函数 isvalidInt() 可用于检查输入的字符串是否符合这些条件。该函数如果条件满足则返回布尔值 true；否则返回布尔值 false。

```
bool isvalidInt(string str)
{
    int start = 0;
    int i;
    bool valid = true;  // assume a valid
    bool sign = false;  // assume no sign

    // check for an empty string
    if (int(str.length()) == 0) valid = false;

    // check for a leading sign
    if (str.at(0) == '-' || str.at(0) == '+')
    {
        sign = true;
        start = 1;  // start checking for digits after the sign
    }

    // check that there is at least one character after the sign
    if (sign && int(str.length()) == 1) valid = false;

    // now check the string, which you know has at least one non-sign char
    i = start;
    while(valid && i < int(str.length()))
    {
        if(!isdigit(str.at(i))) valid = false; //found a non-digit character
        i++; // move to next character
    }
    return valid;
}
```

在该函数的代码中，请注意正在检查的条件。它们在代码中已注释，内容如下：

- 字符串不为空。
- 存在有效的符号（+ 或 -）。
- 如果存在符号，其后至少有一个数字。
- 字符串中剩余的所有字符都是数字。

只有在满足所有这些条件时，函数才会返回布尔值 true。返回该值后，字符串就可以安全地转换为整数，并且可以保证不会产生意外值从而妨碍进一步的数据处理。程序 14.18 在完整程序的上下文中使用了此函数。

## 程序 14.18

```
#include <iostream>
#include <string>
using namespace std;

bool isvalidInt(string); // function prototype (declaration)
int main()
{
    string value;
    int number;

    cout << "Enter an integer: ";
    getline(cin, value);

    if (!isvalidInt(value))
        cout << "The number you entered is not a valid integer.";
    else
    {
        number = atoi(value.c_str());
        cout << "The integer you entered is " << number;
    }

    return 0;
}
```

```
bool isvalidInt(string str)
{
    int start = 0;
    int i;
    bool valid = true;  // assume a valid
    bool sign = false;  // assume no sign

    // check for an empty string
    if (int(str.length()) == 0) valid = false;

    // check for a leading sign
    if (str.at(0) == '-' || str.at(0) == '+')
    {
        sign = true;
        start = 1;  // start checking for digits after the sign
    }

    // check that there is at least one character after the sign
    if (sign && int(str.length()) == 1) valid = false;

    // now check the string, which you know has at least one non-sign char
    i = start;
    while(valid && i < int(str.length()))
    {
        if(!isdigit(str.at(i))) valid = false; //found a non-digit character
        i++;  // move to next character
    }
    return valid;
}
```

程序 14.18 的两次示例运行产生了以下输出：

Enter an integer: 12e45
The number you entered is not a valid integer.

以及

Enter an integer: -12345
The integer you entered is -12345

正如该输出所示，程序确定在第一次运行中输入了无效字符。
第二道防线是使用异常处理代码，通常允许用户通过重新输入新数据来纠正问题，例如无效的数据输入，直到提供有效值或输入结束程序为止。使用异常处理和程序 14.18 中的 isvalidInt() 函数，您可以开发一个更全面的名为 `getAnInt()` 的函数，该函数会持续接受用户输入，直到检测到对应有效整数的字符串为止。输入字符串后，`getAnInt()` 将其转换为整数并返回整数值。这种技术可确保请求整数的程序确实接收到整数，并防止任何不良影响，例如因输入无效数据类型而导致程序崩溃。执行此任务所使用的算法如下：

- 1. **将布尔变量 `notanint` 设置为 true while (notanint 为 true)**
- 2. **try**
  - 接受字符串值
  - 如果字符串值不对应整数，则抛出异常
- 3. **catch 异常**
  - 显示错误信息“Invalid integer - Please reenter: ”
  - 将控制权发送回 while 语句
  - 将 `notanint` 设置为 false（导致循环终止）
- 4. **End while**
- 5. **返回输入字符串对应的整数**

对应于该算法的代码在程序 14.19 中以阴影显示。

```
#include <iostream>
#include <string>
using namespace std;

int getAnInt();  // function prototype
int main()
{
    int value;

    cout << "Enter an integer value: ";
    value = getAnInt();
    cout << "The integer entered is: " << value << endl;

    return 0;
}

int getAnInt()
{
    bool isValidInt(string);  // function prototype
    bool notanint = true;
    string svalue;
```

## `string` 类和异常处理

```
while (notanint)
{
    try
    {
        cin >> svalue;  // accept a string input
        if (!isvalidint(svalue)) throw svalue;
    }
    catch (string e)
    {
        cout << "Invalid integer - Please reenter: ";
        continue; // send control to the while statement
    }
    notanint = false;
}
return atoi(svalue.c_str());  // convert to an integer
}

bool isvalidInt(string str)
{
    int start = 0;
    int i;
    bool valid = true;  // assume a valid
    bool sign = false;  // assume no sign

    // check for an empty string
    if (int(str.length()) == 0) valid = false;

    // check for a leading sign
    if (str.at(0) == '-' || str.at(0) == '+')
    {
        sign = true;
        start = 1;  // start checking for digits after the sign
    }

    // check that there is at least one character after the sign
    if (sign && int(str.length()) == 1) valid = false;

    // now check the string, which you know has at least one non-sign char
    i = start;
    while (valid && i < int(str.length()))
    {
        if (!isdigit(str.at(i))) valid = false;  // found a non-digit character
        i++;  // move to next character
    }
    return valid;
}
```

以下是程序 14.19 产生的一个示例输出：

```
Enter an integer value: abc
Invalid integer - Please reenter: 12.
Invalid integer - Please reenter: 12e
Invalid integer - Please reenter: 120
The integer entered is: 120
```

正如该输出所示，getanInt() 函数工作正确。它会持续请求输入，直到输入有效整数为止。

## 练习 14.5

- 1. **（练习）** 编写一个 C++ 程序，提示用户输入一个整数。让程序使用 cin 以整数形式接受该数字，并使用 cout 显示程序从输入数据中实际接受的值。运行程序四次。第一次运行时输入一个有效整数；第二次运行时输入一个双精度数；第三次运行时输入一个字符；第四次运行时输入值 1234。

- 2. **（修改）** 修改你在练习 1 中编写的程序，以提示并接受双精度数。运行程序四次：首先输入一个整数；其次输入一个十进制数；第三次输入一个以“f”为最后一个字符输入的十进制数；第四次输入一个字符。使用输出显示，跟踪程序从你输入的数据中实际接受的数字。发生了什么，如果有的话，为什么？

- 3. **（思考）**
  - a. 你认为成功的应用程序程序为何包含广泛的数据输入有效性检查？*（提示：回顾练习 1 和 2。）*
  - b. 你认为数据类型检查和数据合理性检查之间的区别是什么？
  - c. 程序要求用户输入月份、日期和年份。对输入的数据可以做哪些合理的检查？

- 4. **（练习）**
  - a. 输入并运行程序 14.18。
  - b. 运行程序 14.18 四次，使用练习 1 中列出的数据进行每次运行。

- 5. **（修改）** 修改程序 14.18 以显示输入的任何无效字符。

- 6. **（修改）** 修改程序 14.18 以持续请求整数，直到输入有效数字为止。

- 7. **（修改）** 修改程序 14.18 以在检查有效性之前从输入的字符串中删除所有前导和尾随空格。

- 8. **（有用工具）** 编写一个函数，在输入时逐个检查每个数字，而不是像程序 14.18 中那样检查完成的字符串。

- 9. **（练习）** 输入并运行程序 14.19。


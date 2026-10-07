
它导致键盘输入的下一个字符被存储在变量 `nextChar` 中。该函数对于在将字符赋值给完整的字符串或 C++ 数据类型之前对字符进行输入和检查非常有用。

与 `get` 对应的输出是 `put()`。该函数期望一个单字符参数并显示该字符。例如，语句 `cout.put('A')` 会导致字母 A 显示在屏幕上。

表 9.6 中的最后三行，`ignore()` 是最有用的。它跳过直到遇到指定的字符（如 `'\n'`）为止。例如，`cin.ignore(80,'\n')`。

`peek()` 函数返回输入流中的下一个字符但不从流中移除它。

最后，`putback()` 将字符放回输入流。

**幻影换行符** 正如你在节中所示

### 信息点

### 不一致性

### 命名不一致
在 9.6 中列出的所有类函数都使用在函数名前加对象的命名法，如 `cin.get()`。然而，字符串类的 `getline()` 函数使用了 `getline(cin, strVar)`。在这种命名法中，对象 `(cin)` 作为参数出现，这是基于过程的。为了一致性，你会期望 `getline()` 被调用为 `cin.getline()`。不幸的是，这种命名已经用于字符串（正如 7.2 节中讨论的一维字符数组），因此产生了命名不一致。对于存储为一维数组的字符串，正确的函数调用是 `cin.getline(strVar, MAXCHARS)`，其中 `MAXCHARS` 是数组的最大字符数。

#### 程序 9.15

```cpp
#include <iostream>

using namespace std;

int main() {

    char fkey;

    cout << "Type in a character: ";

    cin.get(fkey);

    cout << "The key just accepted is " << int(fkey) << endl;

    return 0;

}
```

程序 9.15 运行，响应提示 "Type in a character:" 的输入的字符被存储在字符变量 `fkey` 中，通过显式将字符转换为整数来强制其作为整数值显示，从而显示进制。示例运行说明了这一点：

Type in a character: m
The just accepted is 109

在此时，一切看起来都是正确的，尽管你可能奇怪为什么显示的是 m 的进制值而不是字符。

## 完成基础部分

### 程序 9.16

```cpp
#include <iostream>

using namespace std;

int main()
{
    char fkey, skey;
    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;
    cout << "Type in another character: ";
    cin.get(skey);
    cout << "The key just accepted is " << int(skey) << endl;
    return 0;
}
```

以下是程序 9.16 的示例运行。
输入一个字符: m
刚刚接受的键是 109
输入另一个字符: 
刚刚接受的键是 10

在响应第一个提示并输入 m 之后，按了 Enter 键。从字符的角度来看，这次输入代表了两个不同字符的输入。第一个字符是 m，它被编码并存储为整数 109。第二个字符是 l，它被存储在缓冲区中的 Enter 键中。第二次调用 `get()` 立即获取了该字符，等待另一个键被按下。`endl` 流显示了该键的代码，显示的是数值而不是字符，因为 Enter 键没有与之关联的可显示平台字符。

记住，每个键都有一个数值，包括 Enter、空格（space）、Escape 和 Ctrl。在输入数字时，这些键通常没有影响，因为函数会将它们视为带有数值数据的前导或尾输入而被忽略。这些键也会影响作为第一个输入数据请求的单个字符的输入，如程序 9.15 所示。只有当用户已经输入了其他数据后，才请求字符时（如程序 9.16 所示），通常不可见的 Enter 键才会变得明显起来。

在第 9.1 节中，你学习了如何使用 `getline()` 函数防止 Enter 键被接受为合法的输入。当程序中使用 `getline()` 函数时，你可以使用以下方法：

- 在 `cin.get()` 输入后调用 `cin.ignore()`。
- 将 Enter 作为一个字符接受，然后不使用它。

![](img/d5a225ca53b347501e86d72212077531_573_0.png)

## 第 9 章

程序 9.17 将第一种解决方案应用于程序 9.16。在读取并显示第一个字符后忽略 Enter 键，可以清除缓冲区中的 Enter 键，它准备准备好将下一个有效输入字符作为它的第一个字符。

![](img/d5a225ca53b347501e86d72212077531_574_0.png)

### 程序 9.17

```cpp
#include <iostream>

using namespace std;

int main()
{
    char fkey, skey;
    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;
    cin.ignore();
    cout << "Type in another character: ";
    cin.get(skey);
    cout << "The key just accepted is " << int(skey) << endl;
    cin.ignore();
    return 0;
}
```

在程序 9.17 中，观察到当用户输入字母 m 并按下 Enter 键时，m 被赋值给 `fkey` 且该键被忽略了。下一次调用 `get()` 将按下的下一个键的代码存储在 `skey` 变量中。从用户的角度来看，Enter 键没有影响，除了指示每个字符输入的结束。以下是程序 9.17 的示例运行：

- 输入一个字符: m
刚刚接受的键是 109
- 输入另一个字符: b
刚刚接受的键是 98

## 用户输入验证的第二次查看

正如第 3.4 节提到的，有效响应意外输入的程序正式被称为健壮型程序（robust programs），非正式被称为“防弹”程序。验证确保程序不会因为意外输入而产生意外结果。

## 完成基础部分

为了看到意外的结果，请检查以下代码。首先，假设程序由于以下输入而导致无限循环或崩溃：

```cpp
cout << "Enter an integer:
cin >> value;
```

在错误的情况下，用户输入非数字。在早期的 C++ 版本中，这种输入会导致程序终止。在当前的 ANSI/ISO 标准中，不会发生这种情况，但会导致意外结果。

```cpp
double value;
{
cout << "Enter a number (0 to exit): ";
cin >> value;
cout << "The square root of this number is: " << sqrt(value) << endl;
while (value != 0);
```

处理无效数据的基本技术是验证。在输入期间或之后验证数据，如果正确，它可以防止程序崩溃、创建无限循环或产生意外结果。

验证字符有效性的两种技术将在 9.5 节中讨论。

![](img/d5a225ca53b347501e86d72212077531_575_0.png)

### 9.4 练习

- 1. 练习并运行程序 9.13。
- 2. 练习并运行程序 9.14。
- 3. 练习编写一个 C++ 程序，统计字符串中的单词数。每当从空格遇到非空格字符时，遇到一个单词。字符串由空格分隔。
- 4. 练习生成 0-9 之间的随机数。如果数字代表可打印字符，打印该字符并带有相应的消息，指示：
    - 字符是小写字母。
    - 字符是大写字母。
    - 字符是数字。
    - 字符是空格。
  如果字符不是这些之一，显示其整数格式。
- 5. 练习编写一个名为 `length()` 的函数，使用字符串类确定并返回字符串的长度。
    - b. 写一个简单的 `main()` 函数来测试练习中的 `length()` 函数。
- 6. 练习编写一个 `countlets()` 函数，返回作为参数的字符串中的字母数量。数字、空格、标点符号、制表符和换行符不计入返回计数。
    - 将 `countlets()` 函数包含在一个可执行的 C++ 程序中，并使用该程序测试该函数。
- 7. 练习编写一个程序，从控制台接收字符串并显示字符串每个字符的十六进制值。
- 8. 练习编写一个 C++ 程序，从控制台接收字符串并每行显示一个单词。
- 9. 调试以下代码，用户输入数据 12e4：
  `cout << "Enter an integer:";`
  `cin >> value;`
  变量 `value` 中存储了什么？

### 9.5 输入数据验证

程序中字符串的一个主要用途是用户输入验证。验证输入是非常关重要的：当程序提示用户输入特定类型的数据（如整数）时，提示并不确保输入符合要求。事实上，用户输入什么完全不在程序员的控制范围内。你所控制的是如何处理输入的输入。
告诉一个沮丧的用户“程序接受了无效数据并防止其被接受”是没有任何好处的。通常，这是通过验证数据是否正确来实现。如果是，则接受数据；否则，要求用户重新输入，并解释数据无效的原因。

## 完成基础工作

验证数值输入数据的一种常用方法是将所有数字都视为字符串。然后，可以检查字符串中的每个字符，以确保它符合要求的数据类型。在完成此检查并验证数据为正确类型后，可以使用表 9.7 列出的转换函数将字符串转换为整数或双精度值。（对于使用 `string` 对象的数据接收，在调用转换函数之前，必须对字符串应用 `c_str()` 函数）

例如，考虑输入一个整数。为了使其有效，输入的数据必须符合以下条件：

- 数据必须至少包含一个字符。
- 如果第一个字符是 `+` 或 `-` 号，则数据必须包含一个数字。
- 在第一个字符之后，所有从 0 到 9 的数字都是可接受的。

表 9.7 C 字符串转换函数
| 函数 | 描述 | 示例 |
|---|---|---|
| `int atoi(stringExp)` | 将 `stringExp` 转换为整数。在遇到第一个非整数字符时停止转换。 | `atoi("1234")` |
| `double atof(stringExp)` | 将 `stringExp` 转换为双精度数字。在遇到第一个无法解释为双精度数的字符时停止转换。 | `atof("12.34")` |
| `char[] itoa(integerExp)` | 将 `integerExp` 转换为字符数组。为返回字符分配的空间必须足够容纳转换后的值。 | `itoa(1234)` |

以下函数 `isValidInt()` 可检查输入的字符串是否符合这些条件。如果满足条件，该函数返回布尔值 `true`；否则，它返回 `false` 值。

```cpp
bool isValidInt(string str) {
    int start = 0;
    int i;
    bool valid = true; // 假设是有效的
    bool sign = false; // 假设没有符号
// 检查空字符串
    if (int(str.length()) == 0) valid = false;
// 检查前导符号
if (str.at(0) == '-' || str.at(0) == '+')
{
    sign = true;
    start = 1; // 从符号后开始检查数字
}
// 检查符号后是否至少有一个字符
if (sign && int(str.length()) == 1) valid = false;
}
// 现在检查你已知的索引
// 是否至少有一个非数字字符
i = start;
while (valid && i < int(str.length()))
{
    if (!isdigit(str.at(i))) valid = false; // 找到了非数字字符
    i++;
    // 移动到下一个字符
}
return valid;
}
```

在 `isValidInt()` 函数的代码中，请注意所检查的条件。它们在代码中都有注释，并包含以下内容：

- 字符串不空。
- 存在有效的符号（+ 或 -）。
- 如果存在符号，后面至少跟着一个数字。
- 字符串中所有剩余字符都是数字。

只有当满足所有条件时，函数才会返回布尔值 `true`。在返回此值后，可以将字符串转换为整数，并且可以确保不会有意外的值干扰进一步的数据处理。程序 9.18 在一个完整程序的上下文中使用了此函数。该程序的两次示例运行产生了：

Enter an integer: 12e45
The number you entered is not a valid integer.

以及

Enter an integer: -12345
The integer you entered is -12345

作为输出，该程序成功地确定在第一次运行中输入了无效字符。

### 程序 9.18

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
    bool isValidInt(string); // 函数原型（声明）
    string value;
    int number;
    cout << "Enter an integer: ";
    getline(cin, value);
    if (!isValidInt(value))
        cout << "The number you entered is not a valid integer.";
    else
    {
        number = atoi(value.c_str());
        cout << "The integer you entered is " << number;
    }
    return 0;
}
bool isValidInt(string str)
{
    int start = 0;
    int i;
    bool valid = true; // 假设是有效的
    bool sign = false; // 假设没有符号
    // 检查空字符串
    if (str.length() == 0) valid = false;
    // 检查前导符号
    if (str.at(0) == '-' || str.at(0) == '+')
    {
        sign = true;
        start = 1; // 从符号后开始检查数字
    }
    // 检查符号后至少有一个字符
    if (sign && int(str.length()) == 1) valid = false;
    // 现在检查字符串，你已知它
    // 至少有一个非符号字符
    i = start;
    while (valid && i < int(str.length()))
    {
        if (!isdigit(str.at(i))) valid = false; // 找到了非数字字符
        i++; // 移动到下一个字符
    }
    return valid;
}
```

一种坚实的防御措施是在异常处理代码的上下文中提供错误处理代码。这类代码通常用于允许用户通过重新输入值来修正问题（例如无效数据）。在 C++ 中提供这种机制被称为异常处理。使用异常，你可以构建一种方法确保用户输入有效数字，防止输入无效数据导致程序崩溃。执行此任务的算法如下：

- 将名为 `notant` 的布尔变量置为 `true`
当 `notant` 为 `true` 时

- 尝试
接收一个字符串值
如果字符串值不对应整数，则抛出异常
捕获异常
显示错误信息 "Invalid integer - reenter:"
将控制权传回循环语句
将 `notant` 置为 `false`（导致循环终止）

- 结束循环
返回算法任务返回的整数

与该算法对应的代码如程序 9.19。

```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    int getInt(); // 函数原型（声明）
    int value;
    cout << "Enter an integer value: ";
    value = getInt();
    cout << "The integer entered is: " << value << endl;
    return 0;
}
```

```cpp
int getInt() {
    bool isValid(string); // 函数原型（声明）
    bool notanint = true;
    string value;
    while (notanint) {
        try {
            cin >> value; // 接受字符串输入
            if (!isValid(value)) throw value;
        } catch (string e) {
```

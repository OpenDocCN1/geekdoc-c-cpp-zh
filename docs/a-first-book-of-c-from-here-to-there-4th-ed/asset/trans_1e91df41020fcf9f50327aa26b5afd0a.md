

这个输出很直观：`str1` 是一个不包含任何字符的空字符串，而其他字符串则显示它们初始化时所用的字符。由于字符串中的第一个字符被指定为位置 0，而不是 1，因此例如在字符串 `Hot Dog` 中，`D` 的字符位置是 4，如图 14.2 所示。

![](img/e9bf940282dfb289356f077151cc69dd_628_0.png)

**图 14.2** 字符串 `Hot Dog` 的字符位置

## 字符串的输入与输出

除了使用表 14.1 中列出的构造函数来初始化字符串外，字符串还可以从键盘输入并在屏幕上显示。表 14.2 列出了用于字符串值输入和输出的基本方法和对象。

**表 14.2** *string* 类的输入与输出

| C++ 对象或方法 | 描述 |
|---|---|
| `cout` | 通用屏幕输出对象 |
| `cin` | 通用键盘输入对象，遇到空白字符时停止读取字符串输入 |
| `getline(cin, strObj)` | 通用键盘输入方法，输入所有输入的字符，将其存储在字符串 `strObj` 中，并在收到换行符（`\n`）时停止接受字符 |

除了本书中一直使用的标准 `cout` 和 `cin` 流之外，string 类还提供了用于字符串输入的 `getline()` 方法。例如，表达式 `getline(cin, message)` 会持续接受并存储键盘输入的字符，直到按下回车键。按下回车键会产生一个换行符 `\n`，`getline()` 将其解释为行输入的结束。`getline()` 遇到的所有字符（换行符除外）都会存储在字符串 `message` 中，如图 14.3 所示。

![](img/e9bf940282dfb289356f077151cc69dd_628_1.png)

**图 14.3** 使用 `getline()` 输入字符串

程序 14.2 演示了如何使用 `getline()` 方法和 `cout` 流来输入和输出用户在键盘上输入的字符串数据。虽然该程序使用 `cout` 进行字符串输出，但通常不能使用 `cin` 代替 `getline()` 进行字符串输入，因为 `cin` 读取的是一组字符，直到遇到空格或换行符为止。因此，如果尝试使用语句 `cin >> message;` 输入字符 This is a string，则只有单词 This 会被赋值给 `message`。由于空格会终止 `cin` 的提取操作，`cin` 在输入字符串数据方面的用途受到限制；因此，需要使用 `getline()`。

### 程序 14.2

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string message;    // 声明一个字符串对象

    cout << "Enter a string:\n";

    getline(cin, message);

    cout << "The string just entered is:\n"
         << message << endl;

    return 0;
}
```

以下是程序 14.2 的示例运行结果：

```
Enter a string:
This is a test input of a string of characters.
The string just entered is:
This is a test input of a string of characters.
```

在其最通用的形式中，`getline()` 方法具有以下语法：

```
getline(cin, strObj, terminatingChar)
```

在此语法中，`strObj` 是字符串对象名，`terminatingChar` 是可选字符常量或变量，用于指定终止字符。例如，表达式 `getline(cin, message, '!')` 会接受键盘输入的所有字符（包括换行符），直到输入感叹号为止。感叹号不会作为字符串的一部分存储。

如果在调用 `getline()` 时省略了可选的第三个参数 `terminatingChar`，则默认的终止字符是换行符（`'\n'`）。因此，语句 `getline(cin, message, '\n');` 可以代替语句 `getline(cin, message);` 使用。这两个语句都会在按下回车键时停止读取字符。从此时起，在本书所有程序中，输入均通过按下回车键终止，该操作会生成一个换行符。因此，传递给 `getline()` 的可选第三个参数（即终止字符）会被省略。

**注意：幻影换行符** 当 `cin` 输入流和 `getline()` 方法一起用于接受数据，或者单独使用 `cin` 接受字符时，可能会出现看似奇怪的结果。为了了解这种结果是如何产生的，请看程序 14.3，该程序使用 `cin` 接受键盘输入的整数。该整数随后存储在变量 `value` 中，然后调用 `getline()` 方法。

### 程序 14.3

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int value;
    string message;

    cout << "Enter a number: ";
    cin >> value;
    cout << "The number entered is:\n"
         << value << endl;

    cout << "Enter text:\n";
    getline(cin, message);
    cout << "The text entered is:\n"
         << message << endl;
    cout << int(message.length());

    return 0;
}
```

当程序 14.3 运行时，响应提示 `Enter a number:` 而输入的数字会存储在变量 `value` 中。此时，一切似乎都运行正常。但请注意，在输入数字时，您会键入数字并按下回车键。在几乎所有计算机系统上，输入的这些数据在字符输入后会立即存储在称为缓冲区的临时存储区域中，如图 14.4 所示。

## 信息点

### string 和 char 数据类型

字符串可以由零个、一个或多个字符组成。当字符串没有字符时，它被称为空字符串，长度为 0。包含单个字符的字符串（例如 "a"）是长度为 1 的字符串，其存储方式与 char 数据类型（例如 'a'）不同。然而，在许多实际用途中，长度为 1 的字符串和 char 的响应方式相同；例如，`cout << "\n"` 和 `cout << '\n'` 都会在屏幕上产生一个新行。重要的是要理解它们是不同的数据类型。例如，以下两个声明

```
string s1 = 'a';  // 无效的初始化
char key = "\n"; // 无效的初始化
```

都会产生编译错误，因为它们试图用另一种类型的字面值来初始化一种数据类型。

![](img/e9bf940282dfb289356f077151cc69dd_631_0.png)

# 图 14.4 键入的字符首先存储在缓冲区中

程序 14.3 中的 `cin` 输入流接受了输入的数字，但将 `'\n'` 留在了缓冲区中。下一个输入语句（即对 `getline()` 的调用）会将回车键的代码作为下一个字符拾取，并终止任何进一步的输入。以下是程序 14.3 的示例运行结果：

```
Enter a number: 26
The number entered is 26
Enter text:
The text entered is
```

在此输出中，响应提示 `Enter text:` 时没有接受任何文本。没有接受文本的原因是，在程序接受数字 26 之后，回车键的代码（即换行转义序列）仍留在缓冲区中，并被 `getline()` 拾取并解释为其输入的结束。无论 `cin` 接受的是整数（如程序 14.3 所示）、字符串还是任何其他输入，只要随后调用 `getline()` 方法，都会出现此结果。针对这个“幻影”回车键问题，有三种解决方案：

- 不要在同一程序中将 `cin` 与 `getline()` 输入混用。
- 在 `cin` 输入后调用 `cin.ignore()`。
- 在字符变量中接受回车键，然后忽略它。

第一种解决方案是首选。然而，所有解决方案都围绕着一个事实：回车键是合法的字符输入，必须被识别为如此。当您在 14.2 节中学习接受 char 数据类型时，会再次遇到此问题。

## 字符串处理

可以使用 string 类函数或 14.2 节中描述的逐字符函数来操作字符串。表 14.3 列出了最常用的 string 类方法，以及也可用于字符串的标准算术和比较运算符。在示例中，类方法的调用方式是先给出对象名，后跟句点，然后是方法名。除少数显著例外外，所有类方法都以这种方式调用。

表 14.3 string 类的处理方法（需要 #include <string>）

| 方法/操作 | 描述 | 示例 |
|---|---|---|
| int length() | 返回字符串的长度 | string.length() |
| int size() | 与上一项相同 | string.size() |
| at(index) | 返回指定索引处的字符，如果索引不存在则抛出异常 | string.at(4) |
| int compare(str) | 将给定字符串与 str 进行比较；如果给定字符串小于 str，则返回负值；如果相等，则返回 0；如果给定字符串大于 str，则返回正值 | string1.compare(string2) |
| c_str() | 将字符串作为以 NULL 结尾的 C 字符串返回 | string1.c_str() |
| bool empty | 如果字符串为空，则返回 true；否则返回 false | string1.empty() |
| erase(ind,n); | 从索引 ind 开始，从字符串中移除 n 个字符 | string1.erase(2,3) |
| erase(ind) | 从索引 ind 开始移除字符串中的所有字符，直到字符串末尾，剩余字符串的长度变为 ind | string1.erase(4) |




## I/O 章节

尽管你已经在某种程度上以“菜谱式”的方式使用 `cin` 和 `getline()` 来接受从键盘输入的数据，但了解数据被发送到程序的内容以及程序必须如何处理这些数据仍然很有用。从根本上说，所有输入（以及输出）都是逐字符进行的，如图 14.10 所示。

![](img/e9bf940282dfb289356f077151cc69dd_646_0.png)

**图 14.10** 接受键盘输入的字符

如图所示，每项数据的输入（无论是字符串还是数字）都是由键入字符组成的。例如，输入字符串 Hello 需要按下并松开 H、e、l、l、o 这五个字符键，以及回车键。类似地，输出数字 26.95 需要显示 2、6、.、9、5 这五个字符。尽管程序员通常不会以这种方式看待数据，但程序受到这种逐字符 I/O 的限制，而 C++ 的所有高级 I/O 方法和流对象都基于更底层的字符 I/O 方法。程序员可以使用的这些更基本的字符方法列于表 14.5 中。

### 表 14.5 基本字符 I/O 方法（需要头文件 iostream）

| 方法 | 描述 | 示例 |
|---|---|---|
| cout.put(charExp) | 将 charExp 的字符值放入输出流 | cout.put('A'); |
| cin.get(charVar) | 从输入流中提取下一个字符并将其赋值给变量 charVar | cin.get(key); |
| cin.peek(charVar) | 将输入流中的下一个字符赋值给变量 charVar，但不将该字符从流中提取出来 | cin.peek(nextKey); |
| cin.putback(charExp) | 将 charExp 的字符值推回到输入流中 | cin.putback(cKey); |
| cin.ignore(n, char) | 最多忽略接下来的 n 个输入字符，直到检测到 char（含 char）为止；如果未指定参数，则忽略输入流中的下一个字符 | cin.ignore(80, '\n');<br>cin.ignore(); |

`get()` 方法读取输入流中的下一个字符，并将其赋值给该方法的字符变量。例如，请看以下语句：

```
cin.get(nextChar);
```

它使键盘输入的下一个字符存储到字符变量 nextChar 中。此方法可用于在字符被赋值给完整的字符串、字符或数值变量之前，对它们进行输入和检查。

与 `get()` 对应的字符输出方法是 `put()`。此方法需要一个单字符参数，并在屏幕上显示传递给它的字符。例如，语句 `cout.put('A')` 会在屏幕上显示字母 A。

在表 14.5 列出的后三个方法中，`cin.ignore()` 最有用。此方法允许跳过输入，直到遇到指定字符（如 `'\n'`）为止。例如，语句 `cin.ignore(80, '\n')` 最多跳过后面的 80 个字符，或者在遇到换行符时停止跳过。此语句可用于跳过一行上的所有后续输入，最多 80 个字符，或直到当前行结束。输入将从下一行开始。

表 14.5 中的 `peek()` 方法返回流中的下一个字符，但不会将其从流缓冲区中移除。例如，表达式 `cin.peek(nextChar)` 返回键盘输入的下一个字符，但将其保留在缓冲区中。此操作有时可用于预先查看下一个字符是什么，同时将其保留在原处供下一次输入使用。

### 补充说明

### 记法不一致

表 14.5 中的所有字符类方法都使用标准的面向对象表示法，即在方法名前面加上对象名和句点，如 `cin.get()`。然而，string 类的 `getline()` 方法使用 `getline(cin, strVar)` 这种表示法。在这种表示法中，对象（cin）作为参数出现在括号内，这正是基于过程的函数传递变量的方式。为了保持一致性，你可能会期望 `getline()` 以 `cin.getline()` 的形式被调用。遗憾的是，在表 14.5 中的类方法被包含到 C++ 库中之前，这种表示法已经被用于为 C 风格字符串（即一维字符数组，如 7.2 节所述）创建的 `getline()` 函数。保留原始调用语法意味着产生了一种记法上的不一致。

最后，`putback()` 方法将一个字符放回流中，使其成为下一个被读取的字符。传递给 `putback()` 的参数可以是任何计算结果为合法字符值的字符表达式；它不必是最后输入的字符。

### 再谈幽灵换行符

正如你在 14.1 节中所见，当 cin 输入流后面跟着 `getline()` 方法调用时，有时会得到看似奇怪的结果。当使用 `get()` 字符方法输入字符时，也会出现同样的结果。要了解它是如何发生的，请看程序 14.10，它使用 `get()` 方法接受键盘输入的下一个字符，然后将该字符存储在变量 fkey 中。

![](img/e9bf940282dfb289356f077151cc69dd_648_0.png)

# 程序 14.10

```
#include <iostream>
using namespace std;

int main()
{
    char fkey;

    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;

    return 0;
}
```

当运行程序 14.10 时，响应提示 Type in a character: 所输入的字符被存储在字符变量 fkey 中，并通过显式地将该字符强制转换为整数，以强制其以整数值显示，从而显示该字符的十进制代码。下面的示例运行说明了这一技术：

Type in a character: m
The key just accepted is 109

此时，一切似乎都在正常工作，尽管你可能想知道为什么显示的是 m 的十进制值而不是字符。正如你将在程序 14.11 中看到的，在输入 m 时，通常需要按下两个键：m 键和回车键。如 14.1 节所述，这两个字符在按下后会存储在一个缓冲区中（请参考前面的图 14.2）。第一个按下的键——本例中为 m——会从缓冲区中取出并存储在 fkey 中，但回车键的代码仍留在缓冲区中。因此，随后调用 `get()` 进行字符输入时，会自动将回车键的代码作为下一个字符获取。要查看示例，请看程序 14.11。

# 程序 14.11

![](img/e9bf940282dfb289356f077151cc69dd_649_0.png)

```
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

以下是程序 14.11 的示例运行：

Type in a character: m
The key just accepted is 109
Type in another character: The key just accepted is 10

回顾该程序中发生的情况：在响应第一个提示输入字母 m 后，回车键也被按下。从字符的角度来看，这个输入代表了两个不同字符的输入。第一个字符是 m，它被编码并存储为整数 109。第二个字符也以回车键的数值代码存储在缓冲区中。第二次调用 `get()` 会立即获取这个代码，而不会等待按下另一个键。最后一个 cout 流显示了这个键的代码。之所以显示数值代码而不是字符，是因为回车键没有与之关联的、可以显示的可打印字符。

请记住，每个键都有一个数值代码，包括回车键、空格键、Escape 键和 Ctrl 键。这些键在输入数字时通常不会产生效果，因为输入方法会将它们视为数值数据的前导或尾随输入而忽略。这些键也不会影响作为用户首先输入的数据而被请求的单个字符的输入，如程序 14.10 所示。只有当用户在已经输入其他数据之后才被请求输入一个字符时（如程序 14.11），通常不可见的回车键才会变得引人注意。

在 14.5 节中，你将学习在使用 `getline()` 方法时，防止回车键被当作有效字符输入接受的其他方法。然而，当在程序中使用 `get()` 方法时，可以使用以下方法：

- 在 `cin.get()` 输入之后调用 `cin.ignore()`。
- 将回车键接收到一个字符变量中，然后不再使用它。

程序 14.12 将第一种解决方案应用于程序 14.11。在读取并显示第一个字符后忽略回车键，可以清除缓冲区中的回车键，使其准备好将下一个有效输入字符存储为第一个字符。

# 程序 14.12

```
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

    return 0;
}
```


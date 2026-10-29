

在此示例中，如果 ch 包含数字字符，则执行第一条 cout 语句；如果字符是字母，则执行第二条 cout 语句。然而，在这两种情况下，要检查的字符都会作为参数传递给该方法。程序 14.8 演示了这种在程序中统计字符串中字母、数字和其他字符数量的代码。要检查的字符通过使用 string 类的 at() 方法获得。在该程序中，此方法在 for 循环中使用，该循环从第一个字符到最后一个字符遍历字符串。

## 程序 14.8

```
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main()
{
    string str = "This -123/ is 567 A ?<6245> Test!";
    char nextChar;
    int i;
    int numLetters = 0, numDigits = 0, numOthers = 0;
    cout << "The original string is: " << str
         << "\nThis string contains " << int(str.length())
         << " characters," << " which consist of" << endl;

    // check each character in the string
    for (i = 0; i < int(str.length()); i++)
    {
        nextChar = str.at(i);  // get a character
        if (isalpha(nextChar))
            numLetters++;
        else if (isdigit(nextChar))
            numDigits++;
        else
            numOthers++;
    }

    cout << "      " << numLetters << " letters" << endl;
    cout << "      " << numDigits << " digits" << endl;
    cout << "      " << numOthers << " other characters." << endl;

    cin.ignore();
    return 0;
}
```

## 信息点

### 为什么 char 数据类型使用整数值

在 C++ 中，字符以整数值形式存储，这有时会让初学者感到困惑。原因在于，除了标准的英文字母和字符外，程序还需要存储一些没有可打印等价物的特殊字符。其中之一是文件结束（EOF）哨兵，所有计算机系统都用它来标识数据文件的结束。EOF 哨兵可以通过键盘输入。例如，在基于 UNIX 的系统中，可以通过按住 Ctrl 键并同时按下 D 来生成；在基于 Windows 的系统中，通过按住 Ctrl 并按下 Z 来生成。在这两个系统中，EOF 哨兵都存储为整数值 -1，它没有对应的字符值。你可以通过显示每个输入字符的整数值（参见程序 14.10）并按下 Ctrl+D 或 Ctrl+Z（取决于你使用的系统）来验证这一点。

通过使用 16 位整数值，可以表示超过 64,000 个不同字符。这个字符数量为多种字符集提供了足够的存储空间，包括阿拉伯文、中文、希伯来文、日文和俄文，以及几乎所有已知的语言符号。因此，将字符存储为整数值具有实际价值。

使用整数编码来表示字符串字符的一个重要结果是，字符可以很容易地按字母顺序进行比较。例如，只要字母表中每个后续字母的值都大于其前一个字母的值，字符值的比较就简化为数值比较。由于字符按顺序数值存储，因此将某个字母加 1 就会得到字母表中的下一个字母。

程序 14.9 的一次示例运行产生了以下输出：

```
Type in any sequence of characters: this is a test of 12345.
The characters just entered, in uppercase, are: THIS IS A TEST OF 12345.
```

在这个程序中，请特别注意用于遍历字符串中每个字符的语句：for (i = 0; i < int(str.length()); i++)。通常，逐个字符地遍历字符串是访问字符串中每个元素的方式，使用 length() 方法来确定何时到达字符串末尾。（回顾程序 14.8，可以看到它以相同的方式使用。）唯一真正的区别在于，程序 14.9 使用数组下标表示法 str[i] 访问每个元素；而程序 14.8 使用 at() 方法。虽然这两种表示法可以互换——使用哪种由你自行选择——但为了保持一致，不应在同一个程序中混用这两种表示法。

## 字符 I/O

虽然你已通过类似于“菜谱”的方式使用 cin 和 getline() 来接受从键盘输入的数据，但了解发送到程序的数据以及程序如何处理这些数据仍然是有用的。在基本层面上，所有输入（以及输出）都是逐字符进行的，如图 14.10 所示。

![](img/202cface8244f523c2641baa2e00d7dd_646_0.png)

### 图 14.10 接受键盘输入的字符

如图所示，每项数据的输入，无论是字符串还是数字，都是由键入字符组成的。例如，输入字符串 Hello 需要按下并释放 H、e、l、l、o 这五个字符键以及 Enter 键。类似地，输出数字 26.95 需要显示 2、6、.、9、5 这五个字符。虽然程序员通常不这样看待数据，但程序受限于这种逐字符的 I/O，并且 C++ 所有更高级的 I/O 方法和流对象都基于更低级的字符 I/O 方法。这些程序员可以使用的更基本的字符方法列于表 14.5 中。

### 表 14.5 基本字符 I/O 方法（需要头文件 iostream）

| 方法 | 描述 | 示例 |
|---|---|---|
| cout.put(charExp) | 将 charExp 的字符值放入输出流 | cout.put('A'); |
| cin.get(charVar) | 从输入流中提取下一个字符，并将其赋给变量 charVar | cin.get(key); |
| cin.peek(charVar) | 将输入流中的下一个字符赋给变量 charVar，但不从流中提取该字符 | cin.peek(nextKey); |
| cin.putback(charExp) | 将 charExp 的字符值推回输入流 | cin.putback(cKey); |
| cin.ignore(n, char) | 最多忽略接下来的 n 个输入字符，直到检测到 char（包括 char）；如果未指定参数，则忽略输入流中的下一个字符 | cin.ignore(80,'\n');<br>cin.ignore(); |

get() 方法读取输入流中的下一个字符，并将其赋给该方法的字符变量。例如，看看以下语句：

```
cin.get(nextChar);
```

该语句使在键盘上输入的下一个字符被存储在字符变量 nextChar 中。此方法对于在字符被赋给完整字符串、字符或数值变量之前输入并检查字符很有用。

与 get() 对应的字符输出方法是 put()。该方法需要一个单字符参数，并在屏幕上显示传递给它的字符。例如，语句 cout.put('A') 会使字母 A 显示在屏幕上。

在表 14.5 列出的最后三个方法中，cin.ignore() 最有用。此方法允许跳过输入，直到遇到指定字符（如 '\n'）。例如，语句 cin.ignore(80, '\n') 最多跳过接下来的 80 个字符，或者在新行字符出现时停止跳过。该语句可用于跳过一行中的所有后续输入，最多 80 个字符，或直到当前行结束。输入将从下一行开始。

表 14.5 中的 peek() 方法返回流中的下一个字符，但不会将其从流的缓冲区中移除。例如，表达式 cin.peek(nextChar) 返回在键盘上输入的下一个字符，但将其留在缓冲区中。此操作有时对于提前查看下一个字符是什么很有用，但会将其留在原处供下一次输入使用。

## 信息点

### 记法不一致

表 14.5 中的所有字符类方法都使用标准的面向对象记法，即方法名前加上对象名和句点，如 `cin.get()`。然而，string 类的 `getline()` 方法使用 `getline(cin, strVar)` 记法。在这种记法中，对象（cin）作为括号内的参数出现，这正是基于过程的函数传递变量的方式。为了保持一致，你可能会期望 `getline()` 被调用为 `cin.getline()`。不幸的是，在表 14.5 中的类方法被纳入 C++ 库之前，这种记法已经用于为 C 风格字符串（即简单的一维字符数组，如第 7.2 节所述）创建的 `getline()` 函数。保留原始调用语法意味着产生了记法上的不一致。

最后，`putback()` 方法将一个字符放回流中，使其成为下一个读取的字符。传递给 `putback()` 的参数可以是任何求值为合法字符值的字符表达式；它不一定是最后一个输入字符。

### 再谈幽灵换行符

如你在第 14.1 节中所见，当 cin 输入流后跟 getline() 方法调用时，有时会得到看似奇怪的结果。当使用 get() 字符方法输入字符时，也会出现同样的结果。要了解它是如何发生的，请看程序 14.10，它使用 get() 方法接受在键盘上输入的下一个字符，然后将该字符存储在变量 fkey 中。

## 程序 14.10

```
```cpp
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
```


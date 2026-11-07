
这会将整行读入 name 数组，前提是该行由 19 个或更少字符组成。（`getline()` 成员函数还有一个可选的第三个参数，第 17 章会讨论它。）

程序清单 4.4 修改了程序清单 4.3，使用 `cin.getline()` 代替简单的 `cin`。除此之外，程序没有变化。

### 程序清单 4.4 `instr2.cpp`

```cpp
// instr2.cpp -- reading more than one word with getline
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.getline(name, ArSize);  // reads through newline
    cout << "Enter your favorite dessert:\n";
    cin.getline(dessert, ArSize);
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    return 0;
}
```

下面是程序清单 4.4 的一些示例输出：

```text
Enter your name:
Dirk Hammernose
Enter your favorite dessert:
Radish Torte
I have some delicious Radish Torte for you, Dirk Hammernose.
```

现在程序可以读取完整姓名，并为用户端上他应得的甜点！`getline()` 函数方便地每次读取一行。它读取输入直到标记行尾的换行符，但并不保存该换行符。相反，在存储字符串时，它用空字符替换换行符（见图 4.5）。

## 使用 `get()` 的面向行输入

让我们尝试另一种方法。`istream` 类还有另一个成员函数 `get()`，它有几种变体。其中一种变体的工作方式与 `getline()` 非常相似。它接受相同的参数，以相同的方式解释这些参数，并读取到行尾。但是，`get()` 不会读取并丢弃换行符，而是将该字符留在输入队列中。假设连续调用两次 `get()`：

```cpp
cin.get(name, ArSize);
cin.get(dessert, ArSize);  // a problem
```

![](img/9afc44517b591d64e2e19f623c9308ef_142_0.png)

图 4.5 `getline()` 读取并替换换行符。

因为第一次调用将换行符留在输入队列中，所以该换行符就是第二次调用看到的第一个字符。因此，`get()` 会认为它已到达行尾，却没有找到任何可读取的内容。如果没有辅助手段，`get()` 就无法越过那个换行符。

幸运的是，`get()` 的一种变体可以提供帮助。调用 `cin.get()`（不带参数）会读取下一个单字符，即使它是换行符，因此你可以用它来处理掉换行符，并为下一行输入做好准备。也就是说，下面的调用序列可以正常工作：

```cpp
cin.get(name, ArSize);      // read first line
cin.get();                  // read newline
cin.get(dessert, ArSize);   // read second line
```

使用 `get()` 的另一种方式是将两个类成员函数连接（或串接）起来，如下所示：

```cpp
cin.get(name, ArSize).get(); // concatenate member functions
```

之所以可以这样做，是因为 `cin.get(name, ArSize)` 返回 cin 对象，随后该对象被用作调用 `get()` 函数的对象。类似地，下面的语句将连续两行输入读入数组 `name1` 和 `name2`；它等价于分别调用两次 `cin.getline()`：

`cin.getline(name1, ArSize).getline(name2, ArSize);`

程序清单 4.5 使用了连接调用。在第 11 章“使用类”中，你将学习如何将此特性融入类定义中。

### 程序清单 4.5 `instr3.cpp`

```cpp
// instr3.cpp -- reading more than one word with get() & get()
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.get(name, ArSize).get();    // read string, newline
    cout << "Enter your favorite dessert:\n";
    cin.get(dessert, ArSize).get();
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    return 0;
}
```

下面是程序清单 4.5 中程序的一次示例运行：

```text
Enter your name:
Mai Parfait
Enter your favorite dessert:
Chocolate Mousse
I have some delicious Chocolate Mousse for you, Mai Parfait.
```

需要注意的一点是，C++ 如何允许函数有多个版本，前提是它们具有不同的参数列表。例如，如果你使用 `cin.get(name, ArSize)`，编译器会注意到你使用的是将字符串放入数组的形式，并调用适当的成员函数。相反，如果你使用 `cin.get()`，编译器会意识到你想要的是读取一个字符的形式。第 8 章“函数探秘”将探讨这一特性，它称为*函数重载*。

究竟为什么要使用 `get()` 而不是 `getline()`？首先，较旧的实现可能没有 `getline()`。其次，`get()` 让你可以更谨慎一些。例如，假设你使用 `get()` 将一行读入数组。你如何判断它读取了整行，而不是因为数组已满而停止？查看下一个输入字符。如果它是换行符，那么整行已被读取。如果它不是换行符，那么该行还有更多输入。第 17 章将探讨这一技术。简而言之，`getline()` 使用起来稍简单一些，但 `get()` 使错误检查更简单。你可以用其中任何一个来读取一行输入；只需记住它们略有不同的行为。

## 空行及其他问题

`getline()` 或 `get()` 读取空行后会发生什么？最初的做法是，下一条输入语句从上一个 `getline()` 或 `get()` 停止的地方继续。然而，当前的做法是，在 `get()`（而不是 `getline()`）读取空行后，它会设置一个称为*失败位*（failbit）的东西。这样做的后果是后续输入被阻塞，但你可以用以下命令恢复输入：

```cpp
cin.clear();
```

另一个潜在问题是输入字符串可能长于分配的空间。如果输入行长于指定的字符数，`getline()` 和 `get()` 都会将剩余字符留在输入队列中。然而，`getline()` 还会设置 failbit 并关闭后续输入。

第 5、6 和 17 章将探讨这些特性以及如何围绕它们进行编程。

## 混合字符串和数字输入

将数字输入与面向行的字符串输入混合可能导致问题。考虑程序清单 4.6 中的简单程序。

### 程序清单 4.6 `numstr.cpp`

```cpp
// numstr.cpp -- following number input with line input
#include <iostream>
int main()
{
    using namespace std;
    cout << "What year was your house built?\n";
    int year;
    cin >> year;
    cout << "What is its street address?\n";
    char address[80];
    cin.getline(address, 80);
    cout << "Year built: " << year << endl;
    cout << "Address: " << address << endl;
    cout << "Done!\n";
    return 0;
}
```

运行程序清单 4.6 中的程序，结果大致如下：

```text
What year was your house built?
1966
What is its street address?
Year built: 1966
Address:
Done!
```

你根本没有机会输入地址。问题在于，当 cin 读取年份时，它会把按 Enter 键生成的换行符留在输入队列中。然后 cin.getline() 将该换行符作为空行读取，并把空字符串赋给 address 数组。修复方法是在读取地址之前读取并丢弃换行符。这可以通过几种方式完成，包括使用带 char 参数或不带参数的 get()，如前面的示例所述。你可以分别进行这些调用：

```cpp
cin >> year;
cin.get();    // or cin.get(ch);
```

或者可以连接这些调用，利用表达式

```cpp
cin >> year
```

返回 `cin` 对象这一事实：

```cpp
(cin >> year).get();  // or (cin >> year).get(ch);
```

如果对程序清单 4.6 做上述某一更改，它就能正常工作：

```text
What year was your house built?
1966
What is its street address?
43821 Unsigned Short Street
Year built: 1966
Address: 43821 Unsigned Short Street
Done!
```

C++ 程序经常使用指针而不是数组来处理字符串。在稍微讨论指针之后，我们将讨论字符串的这一方面。与此同时，让我们看看一种更新的处理字符串的方式：C++ string 类。

## 引入 `string` 类

ISO/ANSI C++98 标准通过添加 string 类扩展了 C++ 库。因此现在，你可以使用 string 类型变量（用 C++ 术语来说就是对象），而不是使用字符数组来保存字符串。正如你将看到的，string 类比数组更易于使用，并且还提供了一种将字符串作为类型的术语表示。

要使用 string 类，程序必须包含 string 头文件。string 类属于 std 命名空间，因此你必须提供 using 指令或声明，否则就要将该类称为 std::string。类定义隐藏了字符串的数组本质，让你可以像对待普通变量一样对待字符串。程序清单 4.7 说明了 string 对象与字符数组之间的一些相似之处和不同之处。

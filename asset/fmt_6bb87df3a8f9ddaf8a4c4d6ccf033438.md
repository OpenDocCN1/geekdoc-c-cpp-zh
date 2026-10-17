
如果你按下 `Q` 或 `q` 退出，程序运行正常。如果你按下其他任何可打印字符继续（例如除 `Q` 或 `q` 外的字母、数字或标点符号），程序也运行正常。

然而，如果你按下 `ENTER` 键会怎样？答案是：什么都没有发生；`cin` 仍在等待你输入。你必须输入一个可打印字符才能继续。这是因为流提取运算符 (`>>`) 会忽略所有的空白字符，例如按下 `ENTER` 键产生的换行符。

# `cin.get` 函数

在第 10 章中，我们讨论了 `cin` 对象的 `getline` 函数。`getline` 函数是一个成员函数。成员函数不是独立调用的，就像我们在第 4 章中用于计算数字幂的 `pow` 函数一样。相反，成员函数是从对象调用的。这里，`getline` 是 `cin` 的成员函数。它通过 `cin` 调用并用点号分隔，如 `cin.get(name, 80)`。

这里我们使用了 `cin` 的另一个成员函数，在第 10 章简要介绍了 `get` 函数。`get` 函数同样可以有两个或三个参数，第一个参数是字符数组。

除了两个和三个参数外，`get` 成员函数还可以无参数或单参数的形式调用。与三个版本不同，`get` 的零和单参数版本用于读取单个字符而不是字符数组。单参数版本将在本节讨论。无参数版本将在下一节（标题“`cin.ignore` 函数”）中讨论。

单参数的数据类型是字符，该参数的值将变为用户按下的任何键盘键。即使按下的是 `ENTER` 键也是如此。然后可以使用 `cin` 对象配合流插入运算符 (`<<`) 将按下 `ENTER` 键产生的换行符赋值给字符变量。

我们将对之前的程序进行修改。我们将语句 `cin >> ch` 改为 `cin.get(ch)`，因此程序现在读取为：

```cpp
#include <iostream>

using namespace std;

int main()
{
    char ch;
    do {
        cout << "Press Q or q to quit, any other key to continue:";
        cin.get(ch);
        if (ch == 'Q' && ch != 'q')
            cout << "You want to continue?\n";
        else
            cout << "You quit\n";
    } while (ch != 'Q' && ch != 'q');
    return 0;
}
```

现在，正如下面的输入和输出，如果你按下 `ENTER` 键继续，程序是可以正常工作的：

Press Q or q to quit, any other key to continue:
You want to continue?
Press Q or q to quit, any other key to continue: q
You quit

然而，如下输入所示，如果你按下一个可打印字符来继续，你将无法在下一个提示处输入内容，因为该提示似乎被跳过了：

```
Press Q or q to quit, any other key to continue: x

You want to continue?

Press Q or q to quit, any other key to continue: You want to

continue?

Press Q or q to quit, any other key to continue:
```

正如这反映的，通过解决空白字符未被识别的问题，我们在输入可打印字符时引入了一个新问题。

描述这个新问题之前，首先需要对输入缓冲区进行简要解释。输入缓冲区是存储输入（例如来自键盘）的内存区域，直到这些输入被赋值（例如通过 `cin` 和流提取运算符 (`>>`)，或者通过对象的 `get` 或 `getline` 成员函数）。

当循环开始时，输入缓冲区是空的。因此，循环的执行停止在 `cin.get(ch)` 语句，直到你输入某些内容。

如图 12-1 所示，如果你按下回车键，缓冲区中唯一的字符就是换行符。该字符作为输入缓冲区中的第一个（也是唯一的）字符，被从输入缓冲区移除并赋值给变量 `ch`。因此，在循环的下一次迭代中，输入缓冲区再次为空。

![](img/59a3417a6d5906fae6d8000d4c2cff76_232_0.png)

**图 12-1：**仅按下回车键时的输入缓冲区

相比之下，如果你输入字母 `x` 然后按下回车键输入，如图 12-2 所示，输入缓冲区包含的不是一个而是两个字符：`x` 和由换行符表示的回车键。

## 读取一个字符

![](img/59a3417a6d5906fae6d8000d4c2cff76_233_0.png)

**图 12-2：在输入字母 x 并按下回车键后的输入缓冲区**

`cin` 对象的 `get` 成员函数从输入缓冲区中移除第一个字符 `x`，并将该值赋值给变量 `ch`。如图 12-2 所示，换行符仍然留在输入缓冲区中。

由于换行符仍然留在输入缓冲区中，在循环的下一次迭代中，你没有机会输入。`get` 成员函数将空白字符视为可打印字符，它会将换行符从输入缓冲区移除并将换行符赋值给变量 `ch`。现在输入缓冲区为空了，因此在下一次循环迭代中，你将有机会输入内容。

## `cin.ignore` 函数

解决方案是在调用 `get` 函数之前清除输入缓冲区中的换行符。你可以使用 `cin` 对象的 `ignore` 成员函数来实现这一点。

`ignore` 成员函数像 `get` 和 `getline` 成员函数一样也是重载的。它可以在不带参数、一个参数或两个参数的情况下调用。

不带参数调用 `ignore` 函数将读取输入缓冲区中的下一个字符并将其丢弃——也就是说，它不会被赋值给任何变量。这正是我们想要的。我们不需要将输入缓冲区中留下的换行符赋值给某个变量，只需要除掉它。

`ignore` 成员函数的一个参数和两个参数版本用于字符数组而不是单个字符。在 `ignore` 成员函数的一个参数版本中，该参数是从输入缓冲区中移除的最大字符数。例如，`cin.ignore(80)` 语句从输入缓冲区中移除多多 80 个字符。在两个参数的版本中，第二个参数是一个字符，如果在遇到第一个参数指定的字符数之前遇到了该字符，则取消从输入缓冲区中的移除。因此，`cin.ignore(80, '\n')` 语句将跳过后续 80 个字符或遇到换行符，以先者为准。

注意

```
*** `cin.ignore();`
*** `cin.get();`
```

本节将使用不带参数的 `ignore` 成员函数，但也可以用不带参数的 `get` 函数来实现相同效果。

因此，程序通过在调用 `get` 成员函数之后调用 `ignore` 成员函数，对之前的程序进行了修改：

```cpp
#include <iostream>

using namespace std;

int main(void)
{
    char ch;
    do {
        cout << "Press Q or q to quit, any other key to continue:";
        cin.get(ch);
        cin.ignore();
        if (ch != 'Q' && ch != 'q')
            cout << "You want to continue\n";
        else
            cout << "You quit\n";
    } while (ch != 'Q' && ch != 'q');
    return 0;
}
```

现在，如下输入和输出所示，如果你按下一个可打印字符来继续：

Press Q or q to quit, any other key to continue: x
You want to continue?
Press Q or q to quit, any other key to continue: q
You quit

这种之所以有效是因为不带参数的 `ignore` 成员函数移除了输入缓冲区中的下一个字符。如图 12-3 所示，这移除了输入缓冲区中剩余的换行符。

```cpp
cin.get(ch);
```

| Value: ? | 'x' | '\n' | 赋值前的输入缓冲区 |
| :--- | :--- | :--- | :--- |
| ch | | | |
| | 'x' | '\n' | 换行符留在 |
| | | | |

```
cin.ignore();
```

**图 12-3：** `cin.ignore()` 之后的输入缓冲区

然而，如下输入和输出所示，如果你按下回车键继续，你必须这样做两次，因为第一次尝试似乎被跳过了：

Press Q or q to quit, any other key to continue:

You want to continue?
Press Q or q to quit, any other key to continue:

这太让人沮丧了！我们可以让可打印字符输入或空白输入正常工作，但无法同时兼顾。

在编程中感到沮丧是正常的。在编程中，坚持无论是比喻意义还是字面上都有回报的。几乎总是有。但首先，你应该理解你试图解决的问题。在我们添加对 `ignore` 成员函数的调用后，你必须按下两次回车键的原因是 `ignore` 函数移除了输入缓冲区中的下一个字符。然而，如图 12-4 所示，当调用不带参数的 `ignore` 函数时，输入缓冲区是空的。

## 读取一个字符

![](img/59a3417a6d5906fae6d8000d4c2cff76_236_0.png)

**图 12-4：** 为什么需要按下两次回车键

如之前的程序和示例输入输出所示，当且仅当输入缓冲区中剩余换行符时，才需要在 `get` 成员函数之后调用 `ignore` 成员函数。因此，建议的解决方案是使用 `if` 语句，仅当用户输入的字符不是换行符时调用 `ignore` 成员函数。如果是换行符，那么在换行符赋值给变量 `ch` 后，输入缓冲区将为空，因此不应调用 `ignore` 函数。然而，如果输入了可打印字符，在可打印字符赋值给变量 `ch` 后，换行符将留在输入缓冲区中，因此应该调用 `ignore` 函数。以下代码段说明了这一点：

```cpp
if (ch == '\n')
    cin.ignore();
```

# 读取字符

```cpp
else cout << "You quit";
while (ch != 'Q' && ch != 'q');
return 0;
```

无论使用可打印字符还是 `ENTER` 键来继续，该程序都能完美运行。

# 注意

`if` 语句和 `while` 语句的条件都是 `ch != 'Q' && ch != 'q'`。新手常见的错误是在应该使用 `&&` 运算符的地方使用了 `||` 运算符，反之亦然，例如 `ch == 'Q' && ch == 'q'`，该条件将为真。一个变量一次只能有一个值，因此 `ch` 的值永远不会等于 `Q` 或 `q`，因为它不可能同时是两者其中之一。当然，该表达式可以使用 `||` 运算符重写为 `!(ch == 'Q' || ch == 'q')`。

# 结合使用 `cin`、`cin.get` 和 `cin.getline()`

换行符残留在输入缓冲区中的问题并不限于在响应“按任意键继续”的提示时按下 `ENTER` 键的情况。当在一个程序中同时使用 `get` 或 `getline` 成员函数时，这个问题也会出现，因为 `ENTER` 键被用于结束输入。

以下程序在一个程序中结合使用 `cin` 和 `getline` 成员函数的示例：

```cpp
#include <iostream>

using namespace std;

int main()
{
    char name[80];
    int courseNum;
    cout << "Enter course number: ";
    cin >> courseNum;
    cout << "Enter your name: ";
    cin.getline(name, 80);
    cout << "Course number is: " << courseNum << endl;
    cout << "Your name is: " << name << endl;
    return 0;
}
```

这里是示例输入和输出：

Enter course number: 802
Enter your: Course is: 802
Your name is: 

你没有机会输入名字。原因与上一节中的情况类似，即用户没有机会进行输入。

如图 12-5 所示，当你输入 802 并按下 `ENTER` 键进行输入时，输入缓冲区不仅包含了 802，还包含了按下 `ENTER` 键产生的换行符。`cin` 配合流提取运算符（`>>`）被移除并赋值给变量 `courseNum`，但*不包括*换行符，该换行符留在输入缓冲区中。

# 读取字符

![](img/59a3417a6d5906fae6d8000d4c2cff76_238_0.png)

图 12-5：`cin >> courseNum` 后接 `cin.getline(name,80)` 的输入缓冲区

由于换行符残留在输入缓冲区中，你没有机会在下一个语句（`getline` 成员函数的调用）中输入。相反，图 12-5 所示，`getline` 成员函数从输入缓冲区中移除空白和换行符，并将换行符赋值给字符数组 `name`。虽然字符数组 `name` 被赋予了值，但它不是一个可打印字符，因此输出显示 `name` 没有值。

上一节指出的解决方案是在使用 `cin` 对象和流提取运算符（`>>`）后，紧跟使用无参数的 `ignore`（或 `get`）成员函数。然而，与流提取运算符（`>>`）不同，它总是会在输入缓冲区中留下一个换行符。以下是对之前程序的修改，通过在使用 `cin` 对象配合流提取运算符（`>>`）之后添加无参数版本的 `ignore` 成员函数的调用，实现了这一解决方案：

```cpp
#include <iostream>

using namespace std;

int main(void)
{
    char name[80];
    int courseNum;
    cout << "Enter course number: ";
    cin >> courseNum;
    cin.ignore();
    cout << "Enter your name: ";
    cin.getline(name, 80);
    cout << "Course: " << courseNum << endl;
cout << "Your name is: " << name << endl;
    return 0;
}
```

如下面的示例输入输出所示，程序现在可以正常工作：

Enter course number: 802
Enter your name: Jeff Kent
Course number is: 802
Your name is: Jeff Kent

# 遵循准则

这里有三个简单的规则，可以避免输入缓冲区中换行符引起的问题（当然，前提是你没有编程需求需要在输入缓冲区中保留换行符）。

- 规则 #1：始终在 `cin` 和流提取运算符（`>>`）之后紧跟 `ignore` 成员函数。

解释：带有流提取运算符（`>>`）的 `cin` 对象始终会在输入缓冲区中留下换行符。使用 `ignore` 成员函数将其清除。

```cpp
char ch;
cin >> ch;
cin.ignore();
```

- 规则 #2：不要在 `getline` 函数之后紧跟无参数的 `ignore` 成员函数。

解释：`getline` 函数会从输入缓冲区中移除结束输入的换行符。因此，后面不应该紧跟 `ignore` 成员函数。

- 规则 #3：在使用带有一个参数的 `get` 函数（如 `cin.get(ch)`）后，检查输入缓冲区是否有换行符。如果有，使用 `ignore` 成员函数将其清除。

解释：带单个字符参数的 `get` 函数在输入字符并按下 `ENTER` 后，会在输入缓冲区中留下换行符。

```cpp
char ch;
cin >> ch;
cin.ignore();
```

# 有用的字符函数

`cctype` 库中的许多函数允许你判断字符的值——即字母、字符或空白符号。这些函数接受一个参数（字符），并返回布尔值（真或假）。表 12-1 总结了这些函数。

# 大小写转换

`toupper` 和 `tolower` 各有一个参数。如果参数是字母，`toupper` 返回大写形式；相反，`tolower` 返回小写。

```cpp
#include <iostream>
#include <cctype>

using namespace std;

int main(void)
{
    char ch;
    do {
        cout << "Enter a character: ";
        cin.get(ch);
        if (ch != '\n'){
            cout << "Uppercase: " << toupper(ch) << endl;
            cout << "Lowercase: " << tolower(ch) << endl;
        }
    } while (ch != 'Q' && ch != 'q');
    return 0;
}
```

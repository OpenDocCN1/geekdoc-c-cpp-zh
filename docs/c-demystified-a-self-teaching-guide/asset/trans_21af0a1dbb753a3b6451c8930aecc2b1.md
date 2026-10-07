

# 读取字符

```cpp
else cout << "You quit";
while (ch != 'Q' && ch != 'q');
return 0;
```

无论使用可打印字符还是 ENTER 键来继续，该程序都能完美运行。

# 注意

`if` 语句和 `while` 语句的条件都是 `ch != 'Q' && ch != 'q'`。新手常见的错误是在应该使用 `&&` 运算符的地方使用了 `||` 运算符，反之亦然，例如 `ch == 'Q' && ch == 'q'`，该条件将为真。一个变量一次只能有一个值，因此 `ch` 的值永远不会等于 `Q` 或 `q`，因为它不可能同时是两者其中之一。当然，该表达式可以使用 `||` 运算符重写为 `!(ch == 'Q' || ch == 'q')`。

# 结合使用 cin、cin.get 和 cin.getline()

换行符残留在输入缓冲区中的问题并不限于在响应“按任意键继续”的提示时按下 ENTER 键的情况。当在一个程序中同时使用 `get` 或 `getline` 成员函数时，这个问题也会出现，因为 ENTER 键被用于结束输入。

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

如图 12-5 所示，当你输入 802 并按下 ENTER 键进行输入时，输入缓冲区不仅包含了 802，还包含了按下 ENTER 键产生的换行符。`cin` 配合流提取运算符（>>）被移除并赋值给变量 `courseNum`，但*不包括*换行符，该换行符留在输入缓冲区中。

# 读取字符

![](img/59a3417a6d5906fae6d8000d4c2cff76_238_0.png)

图 12-5：`cin >> courseNum` 后接 `cin.getline(name,80)` 的输入缓冲区

由于换行符残留在输入缓冲区中，你没有机会在下一个语句（`getline` 成员函数的调用）中输入。相反，图 12-5 所示，`getline` 成员函数从输入缓冲区中移除空白和换行符，并将换行符赋值给字符数组 `name`。虽然字符数组 `name` 被赋予了值，但它不是一个可打印字符，因此输出显示 `name` 没有值。

上一节指出的解决方案是在使用 `cin` 对象和流提取运算符（>>）后，紧跟使用无参数的 `ignore`（或 `get`）成员函数。然而，与流提取运算符（>>）不同，它总是会在输入缓冲区中留下一个换行符。以下是对之前程序的修改，通过在使用 `cin` 对象配合流提取运算符（>>）之后添加无参数版本的 `ignore` 成员函数的调用，实现了这一解决方案：

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

- 规则 #1：始终在 `cin` 和流提取运算符（>>）之后紧跟 `ignore` 成员函数。

解释：带有流提取运算符（>>）的 `cin` 对象始终会在输入缓冲区中留下换行符。使用 `ignore` 成员函数将其清除。

```cpp
char ch;
cin >> ch;
cin.ignore();
```

- 规则 #2：不要在 `getline` 函数之后紧跟无参数的 `ignore` 成员函数。

解释：`getline` 函数会从输入缓冲区中移除结束输入的换行符。因此，后面不应该紧跟 `ignore` 成员函数。

- 规则 #3：在使用带有一个参数的 `get` 函数（如 `cin.get(ch)`）后，检查输入缓冲区是否有换行符。如果有，使用 `ignore` 成员函数将其清除。

解释：带单个字符参数的 `get` 函数在输入字符并按下 ENTER 后，会在输入缓冲区中留下换行符。

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

# 检查字符值的函数

`cctype` 库中的许多函数允许你判断字符的值——即字母、字符或空白符号。这些函数接受一个参数（字符），并返回布尔值（真或假）。表 12-1 总结了这些函数。

表 12-1：检查字符值的函数

| 函数 | 说明 |
| :--- | :--- |
| isalpha | 如果参数是字母，返回真；否则返回假。 |
| isnum | 如果参数是字母或数字，返回真；否则返回假。 |
| isdigit | 如果参数是数字，返回真；否则返回假。 |
| islower | 如果参数是字母中的小字母，返回真；否则返回假。 |
| isprint | 如果参数是可打印字符（包括按下空格键产生的空格），返回真；否则返回假。 |


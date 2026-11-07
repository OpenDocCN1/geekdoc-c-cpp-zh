
**表6.4 cctype字符函数**

| 函数名 | 返回值 |
| --- | --- |
| `isxdigit()` | 如果参数是十六进制数字字符（即0–9、a–f或A–F），则该函数返回`true`。 |
| `tolower()` | 如果参数是大写字符，`tolower()`返回该字符的小写版本；否则，返回未更改的参数。 |
| `toupper()` | 如果参数是小写字符，`toupper()`返回该字符的大写版本；否则，返回未更改的参数。 |

## ?: 运算符

C++有一种运算符可以经常用来代替`if else`语句。这个运算符称为*条件运算符*，写作`?:`，而且，对冷知识爱好者来说，它是唯一需要三个操作数的C++运算符。一般形式如下：

`expression1 ? expression2 : expression3`

如果`expression1`为真，那么整个条件表达式的值就是`expression2`的值。否则，整个表达式的值就是`expression3`的值。下面两个例子展示了该运算符的工作方式：

`5 > 3 ? 10 : 12  // 5 > 3 is true, so expression value is 10`
`3 == 9 ? 25 : 18  // 3 == 9 is false, so expression value is 18`

我们可以这样转述第一个例子：如果5大于3，表达式的求值结果为10；否则，求值结果为12。当然，在实际编程情境中，表达式会涉及变量。

程序清单6.9 `condit.cpp`

```cpp
// condit.cpp -- using the conditional operator
#include <iostream>
int main()
{
    using namespace std;
    int a, b;
    cout << "Enter two integers: ";
    cin >> a >> b;
    cout << "The larger of " << a << " and " << b;
    int c = a > b ? a : b;  // c = a if a > b, else c = b
    cout << " is " << c << endl;
    return 0;
}
```

下面是程序清单6.9中程序的示例运行：

```text
Enter two integers: 25 28
The larger of 25 and 28 is 28
```

该程序的关键部分是下面这条语句：

```cpp
int c = a > b ? a : b;
```

它产生的结果与以下语句相同：

```cpp
int c;
if (a > b)
    c = a;
else
    c = b;
```

与if else序列相比，条件运算符更简洁，但乍看之下不那么直观。两种方法的一个区别是，条件运算符产生一个表达式，因而产生一个单一值，该值可以被赋值，也可以并入更大的表达式中，正如程序清单6.9中把条件表达式的值赋给变量c那样。条件运算符的简洁形式、不寻常的语法以及整体怪异的外观，使它成为欣赏这些特性的程序员的最爱。一个颇受欢迎的伎俩——其目的令人不齿，即隐藏代码用途——是把条件表达式相互嵌套，下面这个温和的例子展示了这一点：

```cpp
const char x[2][20] = {"Jason ", "at your service\n"};
const char * y = "Quillstone ";

for (int i = 0; i < 3; i++)
    cout << ((i < 2) ? i ? x[i] : y : x[1]);
```

这不过是一种晦涩（但绝不是最晦涩）的方式，用来按以下顺序打印三个字符串：

```text
Jason Quillstone at your service
```

就可读性而言，条件运算符最适合简单的关系和简单的表达式值：

```cpp
x = (x > y) ? x : y;
```

如果代码变得更复杂，那么用if else语句来表达可能更清晰。

## switch语句

假设你创建一个屏幕菜单，要求用户从五个选项中选择一个——例如，Cheap、Moderate、Expensive、Extravagant和Excessive。你可以扩展if else if else序列来处理五个备选项，但C++的switch语句能更轻松地从扩展列表中选择一个选项。下面是switch语句的一般形式：

```cpp
switch (integer-expression)
{
        case label1 : statement(s)
        case label2 : statement(s)
        ...
        default     : statement(s)
}
```

C++的switch语句就像一种路由设备，告诉计算机接下来执行哪一行代码。程序到达switch语句时，会跳转到标签值与`integer-expression`的值相对应的那一行。例如，如果`integer-expression`的值为4，程序就转到带有`case 4:`标签的那一行。顾名思义，`integer-expression`的值必须是一个归约为整数值的表达式。此外，每个标签都必须是整数常量表达式。最常见的情况是，标签是简单的int或char常量，例如1或'q'，或者是枚举量。如果`integer-expression`与任何标签都不匹配，程序就跳转到标有`default`的那一行。default标签是可选的。如果省略它且没有匹配项，程序就跳转到switch后面的下一条语句（见图6.3）。

switch语句与Pascal等语言中的类似语句有一个非常重要的不同之处。每个C++ case标签只起行标签的作用，而不是选项之间的边界。也就是说，程序跳转到switch中的某一行后，本质上会执行该switch中该行之后的所有语句，除非你明确指示它不这样做。执行不会在下一个case处自动停止。要让执行在特定语句组末尾停止，必须使用`break`语句。这会使执行跳转到switch后面的语句。

程序清单6.10展示了如何结合使用switch和break，为高管们实现一个简单的菜单。该程序使用`showmenu()`函数显示一组选项。然后，switch语句根据用户的响应选择一个操作。

![](img/9afc44517b591d64e2e19f623c9308ef_289_0.png)

图6.3 switch语句的结构。

### 注意

某些硬件/操作系统组合会将`\a`转义序列（在程序清单6.10的case 1中使用）视为静音。

程序清单6.10 `switch.cpp`

```cpp
// switch.cpp -- using the switch statement
#include <iostream>
using namespace std;
void showmenu();  // function prototypes
void report();
void comfort();
int main()
{
    showmenu();
    int choice;
    cin >> choice;
    while (choice != 5)
    {
        switch(choice)
        {
            case 1  :  cout << "\a\n";
                       break;
            case 2  :  report();
                       break;
            case 3  :  cout << "The boss was in all day.\n";
                       break;
            case 4  :  comfort();
                       break;
            default :  cout << "That's not a choice.\n";
        }
        showmenu();
        cin >> choice;
    }
    cout << "Bye!\n";
    return 0;
}

void showmenu()
{
    cout << "Please enter 1, 2, 3, 4, or 5:\n"
         "1) alarm             2) report\n"
         "3) alibi              4) comfort\n"
         "5) quit\n";
}
void report()
{
    cout << "It's been an excellent week for business.\n"
         "Sales are up 120%. Expenses are down 35%.\n";
}
void comfort()
{
    cout << "Your employees think you are the finest CEO\n"
         "in the industry. The board of directors think\n"
         "you are the finest CEO in the industry.\n";
}
```

下面是程序清单6.10中高管菜单程序的示例运行：

```text
Please enter 1, 2, 3, 4, or 5:
1) alarm             2) report
3) alibi              4) comfort
5) quit
4
Your employees think you are the finest CEO
in the industry. The board of directors think
you are the finest CEO in the industry.
Please enter 1, 2, 3, 4, or 5:
1) alarm             2) report
3) alibi              4) comfort
5) quit
2
It's been an excellent week for business.
Sales are up 120%. Expenses are down 35%.
Please enter 1, 2, 3, 4, or 5:
1) alarm             2) report
3) alibi              4) comfort
5) quit
6
That's not a choice.
Please enter 1, 2, 3, 4, or 5:
1) alarm             2) report
3) alibi              4) comfort
5) quit
5
Bye!
```

当用户输入5时，while循环终止。输入1到4会激活switch列表中的相应选项，输入6会触发default语句。

请注意，输入必须是整数，该程序才能正确工作。例如，如果输入一个字母，输入语句就会失败，循环将无休止地运行，直到你终止程序。为了应对那些不遵守说明的人，最好使用字符输入。


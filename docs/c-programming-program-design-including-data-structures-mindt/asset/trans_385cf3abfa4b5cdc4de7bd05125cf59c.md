
提取运算符读取包含空格的字符串。例如，假设变量 name 的定义如上所述。如果输入是：

```text
Alice Wonderland
```

那么在执行以下语句之后：

```cpp
cin >> name;
```

执行后，变量 name 的值为 "Alice"。

要读取包含空格的字符串，可以使用函数 getline。

使用函数 getline 的语法是

```cpp
getline(istreamVar, strVar);
```

其中 istreamVar 是输入流变量，strVar 是字符串变量。读取以换行符 '\n' 为分隔。

getline 函数读取直到当前行的末尾。换行符也会被读取，但不会存储在字符串变量中。

考虑以下语句：

```cpp
string myString;
```

如果输入是 29 个字符：

```text
bbbbHello there. How are you?
```

其中 b 表示一个空格，在执行以下语句之后：

```cpp
getline(cin, myString);
```

myString 的值为：

```cpp
myString = "    Hello there. How are you?"
```

全部 29 个字符（包括前四个空格）都会存储到 myString 中。

类似地，你可以使用输出流变量（例如 cout）和插入运算符 << 来输出 string 数据类型变量的内容。

## 调试：理解逻辑错误并使用 `cout` 语句进行调试

在第 2 章的调试部分，我们说明了如何理解和纠正语法错误。正如我们所见，语法错误由编译器报告，编译器不仅报告语法错误，还会对错误给出一些解释。另一方面，逻辑错误通常不会被编译器捕获，除非是诸如使用未正确初始化的变量之类的简单错误。在本节中，我们说明如何使用 cout 语句发现并纠正逻辑错误。

![](img/b217c421655b51e7494cf3b89bb5432d_206_0.png)

假设我们要编写一个程序，输入华氏温度，输出等效的摄氏温度。温度转换公式为 *摄氏温度 = 5 / 9 * (华氏温度 − 32)。* 因此，考虑以下程序：

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
    int fahrenheit;                                      //Line 5
    int celsius;                                         //Line 6

    cout << "Enter temperature in Fahrenheit: ";        //Line 7
    cin >> fahrenheit;                                   //Line 8
    cout << endl;                                        //Line 9

    celsius = 5 / 9 * (fahrenheit - 32);                 //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C." << endl;             //Line 11

    return 0;                                            //Line 12
}                                                        //Line 13
```

**示例运行 1：** 在此示例运行中，用户输入以阴影显示。

```text
Enter temperature in Fahrenheit: 32
32 degree F = 0 degree C.
```

**示例运行 2：** 在此示例运行中，用户输入以阴影显示。

```text
Enter temperature in Fahrenheit: 110
110 degree F = 0 degree C.
```

第一次计算显示的结果看起来正确。然而，第二次计算的结果显然不正确，尽管使用的是同一个公式，因为 110 华氏度 = 43 摄氏度。这意味着第 10 行计算出的 celsius 值不正确。现在，celsius 的值由表达式 5 / 9 * (fahrenheit − 32) 给出。因此，我们应该仔细查看这个表达式。为了查看该表达式的效果，我们可以分别打印两个表达式 5/9 和 fahrenheit − 32 的值。这可以通过临时插入一条输出语句来实现，如下面的程序所示：

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
    int fahrenheit;                                      //Line 5
    int celsius;                                         //Line 6

    cout << "Enter temperature in Fahrenheit: ";        //Line 7
    cin >> fahrenheit;                                   //Line 8
    cout << endl;                                        //Line 9

    cout << "5 / 9 = " << 5 / 9
         << "; fahrenheit - 32 = "
         << fahrenheit - 32 << endl;                     //Line 9a

    celsius = 5 / 9 * (fahrenheit - 32);                 //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C." << endl;             //Line 11

    return 0;                                            //Line 12
}                                                        //Line 13
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Enter temperature in Fahrenheit: 110
5 / 9 = 0; fahrenheit - 32 = 78
110 degree F = 0 degree C.
```

让我们看看示例运行。我们看到 5 / 9 = 0，且 fahrenheit - 32 = 78。因为 fahrenheit = 110，所以表达式 fahrenheit - 32 的值是正确的。现在让我们看看表达式 5 / 9。该表达式的值为 0。由于运算符 / 的两个操作数 5 和 9 都是整数，使用整数除法，该表达式的值为 0。也就是说，表达式 5 / 9 = 0 的值也是正确计算出来的。因此，根据运算符的优先级，无论 fahrenheit 的值是多少，表达式 5 / 9 * (fahrenheit - 32) 的值将始终为 0。所以问题出在整数除法上。我们可以将表达式 5 / 9 替换为 5.0 / 9。在这种情况下，表达式 5.0 / 9 * (fahrenheit - 32) 的值将是小数。因为 fahrenheit 和 celsius 是 int 变量，我们可以使用强制转换运算符将此值转换为整数，也就是说，我们使用以下表达式：

```cpp
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```

（注意，在前面的表达式中，我们加上了 0.5，以将该数字四舍五入到最接近的整数。）

修改后的程序是：

```cpp
#include <iostream>                         //Line 1

using namespace std;                         //Line 2

int main()                                    //Line 3
{
    int fahrenheit;                           //Line 5
    int celsius;                              //Line 6

    cout << "Enter temperature in Fahrenheit: ";    //Line 7
    cin >> fahrenheit;                               //Line 8
    cout << endl;                                    //Line 9

    celsius = static_cast<int>
              (5.0 / 9 * (fahrenheit - 32) + 0.5);   //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;        //Line 11
    return 0;                                        //Line 12
}                                                    //Line 13
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Enter temperature in Fahrenheit: 110
110 degree F = 43 degree C.
```

正如我们所见，使用临时的 cout 语句，我们能够找到问题。纠正问题后，临时 cout 语句会被移除。

温度转换程序包含逻辑错误，而不是语法错误。使用 cout 语句打印表达式和/或变量的值以查看计算结果，是发现并纠正逻辑错误的一种有效方法。

## 文件输入/输出

前面的章节较为详细地讨论了如何从键盘（标准输入设备）获取输入，以及如何将输出发送到屏幕（标准输出设备）。然而，从键盘获取输入和将输出发送到屏幕存在一些限制。只要输入量非常小，在程序中从键盘输入数据就很方便。如果数据量很小（不超过屏幕大小），并且你不希望以打印格式将输出分发给他人，那么将输出发送到屏幕效果很好。

然而，如果输入数据量很大，每次运行程序时都在键盘上键入数据是低效的。除了键入大量数据的不便之外，键入还可能产生错误，而无意的拼写错误会导致错误结果。你必须通过某种方式从其他来源将数据送入程序。通过使用替代数据源，你可以在运行程序之前准备好数据，并且程序每次运行时都可以访问这些数据。

假设你想在会议上展示程序的输出。分发程序输出的打印副本比在屏幕上显示输出更好。例如，你可以在重要会议之前向委员会的每位成员提供一份打印报告。此外，有时必须保存输出，以便一个程序产生的输出可以作为其他程序的输入。

本节讨论如何从其他输入设备（例如闪存盘，即辅助存储器）获取数据，以及如何将输出保存到闪存盘。C++ 允许

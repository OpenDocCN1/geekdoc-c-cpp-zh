
回忆一下，提取运算符会跳过任何前导空白字符，并且读取会在空白字符处停止。因此，不能使用提取运算符读取包含空格的字符串。例如，假设变量 `name` 如上定义。如果输入是：

```
Alice Wonderland
```

那么在语句：

```
cin >> name;
```

执行后，变量 `name` 的值是 "Alice"。

要读取包含空格的字符串，可以使用函数 `getline`。

使用函数 `getline` 的语法是：

```
getline(istreamVar, strVar);
```

其中 `istreamVar` 是输入流变量，`strVar` 是字符串变量。读取以换行字符 '\n' 为界。

函数 `getline` 会一直读取，直到到达当前行的末尾。换行字符也会被读取，但不会存储在字符串变量中。

考虑以下语句：

```
string myString;
```

如果输入是 29 个字符：

```
bbbbHello there. How are you?
```

其中 b 表示一个空格，在语句：

```
getline(cin, myString);
```

之后，`myString` 的值是：

```
myString = "    Hello there. How are you?"
```

所有 29 个字符，包括前四个空格，都存储到 `myString` 中。

类似地，可以使用输出流变量（例如 `cout`）和插入运算符 `<<` 来输出数据类型为 `string` 的变量的内容。

## 调试：理解逻辑错误并使用 `cout` 语句进行调试

在第 2 章的调试部分，我们说明了如何理解和纠正语法错误。正如我们所见，语法错误由编译器报告，编译器不仅报告语法错误，还会对错误给出一些解释。另一方面，逻辑错误通常不会被编译器捕获，除非是诸如使用未正确初始化的变量之类的琐碎错误。在本节中，我们说明如何使用 cout 语句发现并纠正逻辑错误。假设我们想编写一个程序，输入华氏温度并输出等效的摄氏温度。转换温度的公式是：*摄氏度* = 5 / 9 * (*华氏度* − 32)。因此考虑以下程序：

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                      //Line 2

int main()                                                //Line 3
{                                                         //Line 4
    int fahrenheit;                                       //Line 5
    int celsius;                                           //Line 6

    cout << "Enter temperature in Fahrenheit: ";         //Line 7
    cin >> fahrenheit;                                    //Line 8
    cout << endl;                                         //Line 9

    celsius = 5 / 9 * (fahrenheit - 32);                 //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;            //Line 11

    return 0;                                             //Line 12
}                                                         //Line 13
```

**示例运行 1：** 在本示例运行中，用户输入以阴影显示。

输入华氏温度：`32`

32 华氏度 = 0 摄氏度。

**示例运行 2：** 在本示例运行中，用户输入以阴影显示。

输入华氏温度：`110`

110 华氏度 = 0 摄氏度。

第一次计算中显示的结果看起来是正确的。然而，第二次计算中的结果显然不正确，尽管使用的是同一个公式，因为 110 华氏度 = 43 摄氏度。这意味着第 10 行计算出的 celsius 值不正确。现在，celsius 的值由表达式 5 / 9 * (fahrenheit − 32) 给出。因此我们应该仔细查看这个表达式。为了查看这个表达式的效果，我们可以分别打印两个表达式 5 / 9 和 fahrenheit − 32 的值。这可以通过临时插入一条输出语句来完成，如下面的程序所示：

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                      //Line 2

int main()                                                //Line 3
{                                                         //Line 4
    int fahrenheit;                                       //Line 5
    int celsius;                                           //Line 6

    cout << "Enter temperature in Fahrenheit: ";    //Line 7
    cin >> fahrenheit;                              //Line 8
    cout << endl;                                   //Line 9

    cout << "5 / 9 = " << 5 / 9
         << ";  fahrenheit - 32 = "
         << fahrenheit - 32 << endl;                //Line 9a

    celsius = 5 / 9 * (fahrenheit - 32);            //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;       //Line 11

    return 0;                                       //Line 12
}                                                   //Line 13
```

**示例运行：** 在本示例运行中，用户输入以阴影显示。

```
Enter temperature in Fahrenheit: 110

5 / 9 = 0;  fahrenheit - 32 = 78
110 degree F = 0 degree C.
```

让我们看一下这个示例运行。我们看到 5 / 9 = 0，fahrenheit − 32 = 78。因为 fahrenheit = 110，所以表达式的值是正确的。现在让我们看一下表达式 5 / 9。这个表达式的值是 0。因为运算符 / 的两个操作数 5 和 9 都是整数，使用整数除法，表达式的值为 0。也就是说，表达式 5 / 9 = 0 的值也是正确计算出来的。因此，根据运算符的优先级，无论 fahrenheit 的值是多少，表达式 5 / 9 * (fahrenheit − 32) 的值将始终为 0。所以问题出在整数除法上。我们可以将 5 / 9 的值替换为 5.0 / 9。在这种情况下，表达式 5.0 / 9 * (fahrenheit − 32) 的值将是一个小数。因为 fahrenheit 和 celsius 是 int 变量，我们可以使用强制类型转换运算符将这个值转换为整数，也就是说，我们使用以下表达式：

```
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```

（注意，在前面的表达式中，我们加上了 0.5，以便将数字四舍五入到最接近的整数。）

修订后的程序是：

```cpp
#include <iostream>                            //Line 1

using namespace std;                            //Line 2

int main()                                      //Line 3
{
    int fahrenheit;                             //Line 4
    int celsius;                                //Line 5

    cout << "Enter temperature in Fahrenheit: ";              //Line 7
    cin >> fahrenheit;                                         //Line 8
    cout << endl;                                              //Line 9

    celsius = static_cast<int>
              (5.0 / 9 * (fahrenheit - 32) + 0.5);             //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;                 //Line 11

    return 0;                                                  //Line 12
}                                                          //Line 13
```

**示例运行：** 在本示例运行中，用户输入以阴影显示。

```
Enter temperature in Fahrenheit: 110

110 degree F = 43 degree C.
```

正如我们所见，使用临时的 cout 语句，我们能够找到问题。纠正问题后，临时 cout 语句被移除。

温度转换程序包含的是逻辑错误，而不是语法错误。使用 cout 语句打印表达式和/或变量的值来查看计算结果，是发现并纠正逻辑错误的一种有效方法。

## 文件输入/输出

前面几节较为详细地讨论了如何从键盘（标准输入设备）获取输入，以及如何将输出发送到屏幕（标准输出设备）。然而，从键盘获取输入和将输出发送到屏幕存在一些局限性。只要输入量非常小，在程序中从键盘输入数据就很方便。如果数据量很小（不超过屏幕大小），并且你不希望以打印格式将输出分发给其他人，那么将输出发送到屏幕效果很好。

但是，如果输入数据量很大，那么每次运行程序时都从键盘输入数据是低效的。除了输入大量数据的不便之外，打字还可能产生错误，无意的拼写错误会导致错误的结果。你必须有一些方法从其他来源将数据传入程序。通过使用替代数据源，你可以在运行程序之前准备好数据，而程序每次运行时都可以访问这些数据。

假设你想在会议上展示程序的输出。分发程序输出的打印副本比在屏幕上显示输出更好。例如，你可以在重要会议之前给委员会的每位成员一份打印报告。此外，有时必须保存输出，以便一个程序产生的输出可以作为其他程序的输入使用。

本节讨论如何从其他输入设备（例如磁盘，即二级存储）获取数据，以及如何将输出保存到磁盘。C++ 允许程序获取


在打印`radius`的值之后，第25行的语句将浮点数的输出设置为两位小数，然后以两位小数输出`height`的值。接着，它将浮点数的输出设置为五位小数，然后以五位小数输出`PI`的值。

如果省略第9行的语句并重新编译运行程序，你将看到十进制数的默认输出。更具体地说，计算体积的表达式的值可能会以科学计数法打印。

## C++14 数字分隔符

读写长数字容易出错。例如，假设你正在处理数字`87523872918`。通常，这个数字写作`87,523,872,918`。然而，在C++中，逗号不能用来分隔数字的各位。为了使长数字的读写更容易，C++14引入了数字分隔符`'`（单引号字符）。因此，在C++14中，数字`87523872918`可以表示为`87'523'872'918`。下面示例中的程序进一步说明了这一点。

### 示例 3-12

下面的程序演示了如何在程序中使用数字分隔符。

```cpp
//C++ 14 Digit Separator

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int x = 7'087'625;
    long long y = 28'087'523'872'918;
    double z = 47'034'612'982.688'741;

    cout << fixed << showpoint << setprecision(5);

    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    cout << "z = " << z << endl;
    cout << "1'2'3'4'5'6'7'8'9'0" << endl;
    cout << "8'403 * 3'600 = " << 8'403 * 3'600 << endl;

    return 0;
}
```

示例运行：

```text
x = 7087625
y = 28087523872918
z = 47034612982.68874
1'2'3'4'5'6'7'8'9'0
8'403 * 3'600 = 30250800
```

上述输出不言自明。我们将细节留作练习。

## setw

操纵符`setw`用于在指定列数内输出表达式的值。表达式的值既可以是字符串也可以是数字。表达式`setw(n)`在n列中输出下一个表达式的值。输出是右对齐的。因此，例如，如果你指定列数为8，而输出只需要4列，则前4列将留空。此外，如果指定的列数少于输出所需的列数，输出会自动扩展到所需的列数；输出不会被截断。例如，如果x是一个int变量，下面的语句会在标准输出设备上以5列输出x的值：

```cpp
cout << setw(5) << x << endl;
```

要使用操纵符`setw`，程序必须包含头文件`iomanip`。因此，需要以下include语句：

```cpp
#include <iomanip>
```

与`setprecision`（它控制所有浮点数的输出，直到被重置）不同，`setw`只控制下一个表达式的输出。

### 示例 3-13

```cpp
//Example: This example illustrates how the function setw works

#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{                                                        //Line 5
    int miles = 245;                                     //Line 6
    int speed = 55;                                      //Line 7
    double hours = 35.45;                                //Line 8
    double error = 3.7564;                               //Line 9

    cout << fixed << showpoint;                          //Line 10
    cout << "123456789012345678901234567890" << endl;   //Line 11

    cout << setw(5) << miles << endl;                    //Line 12

    cout << setprecision(2);                             //Line 13
    cout << setw(5) << miles << setw(5) << speed
         << setw(6) << hours
         << setw(7) << error << endl << endl;            //Line 14

    cout << setw(5) << speed << setw(5) << miles
         << setw(4) << hours
         << setw(7) << error << endl << endl;            //Line 15

    cout << setw(2) << miles << setw(6) << hours
         << setw(7) << error << endl << endl;            //Line 16

    cout << setw(2) << miles
         << setw(7) << "error"
         << error << endl;                              //Line 17
    return 0;                                           //Line 18
}                                                       //Line 19
```

示例运行：

```text
123456789012345678901234567890
  245
  245   55 35.45   3.76

   55  24535.45   3.76

245 35.45   3.76

245  error3.76
```

第6、7、8和9行的语句声明了变量miles、speed、hours和error，并将这些变量分别初始化为245、55、35.45和3.7564。第10行的语句将浮点数的输出设置为固定小数格式，带小数点和尾随零。第11行语句的输出显示了打印特定值时的列位置；它是输出的第一行。

第12行的语句以5列输出miles的值。因为miles只有3位数字，所以只需3列即可输出其值。因此，在输出的第二行中，前两列留空。

第13行的语句将浮点数的输出设置为两位小数。第14行的语句在前5列输出miles的值，在接下来的5列输出speed的值，在接下来的6列输出hours的值，在接下来的7列输出error的值。由于hours包含4位数字和一个小数点，输出hours的值需要5列。另外，因为setw函数将hours的输出设置为6列，所以第一列留空。类似地，error的值以7列输出，前3列留空。输出的第四行是空白的，因为操纵符endl在第14行的语句中出现了两次。

第15行的语句在前5列输出speed的值，在接下来的5列输出miles的值，在接下来的4列输出hours的值，在接下来的7列输出error的值，从而形成第五行输出。注意，输出hours的值至少需要5列，但程序只指定了4列，因此hours的输出会扩展为所需的列数。还要注意，在打印miles的值之后，hours的值会在当前光标位置打印（见输出的第五行）。

第16行的语句将miles的输出设置为2列。但是，miles的值包含3位数字，因此miles的值会扩展为正确的列数。在打印miles的值之后，hours的值在接下来的6列中打印，随后error的值在接下来的7列中打印。

第17行的语句将miles的输出设置为2列。但是，miles的值包含3位数字，因此miles的值会扩展为正确的列数。在打印miles的值之后，字符串“error”的值在接下来的7列中打印，随后是error的值。由于没有指定输出error值的列数，因此在打印字符串“error”后，error的值会被打印（见输出的最后一行）。

## 附加输出格式工具

在上一节中，你学习了如何使用操纵符`setprecision`、`fixed`和`showpoint`来控制浮点数的输出，以及如何使用操纵符`setw`在指定列中显示输出。尽管这些操纵符足以生成一份漂亮的报表，但在某些情况下，你可能还想做更多事情。在本节中，你将学习能够让你更好地控制输出的附加格式化工具。

### setfill 操纵符

回顾一下，在操纵符`setw`中，如果指定的列数超过表达式所需的列数，表达式的输出是右对齐的，左侧未使用的列会填充空格。输出流变量可以使用操纵符`setfill`来用空格以外的字符填充未使用的列。

使用操纵符`setfill`的语法是：

```cpp
ostreamVar << setfill(ch);
```

其中`ostreamVar`是一个输出流变量，`ch`是一个字符。例如，语句：

```cpp
cout << setfill('#');
```

将标准输出设备上的填充字符设置为'#'。

要使用操纵符`setfill`，程序必须包含头文件`iomanip`。

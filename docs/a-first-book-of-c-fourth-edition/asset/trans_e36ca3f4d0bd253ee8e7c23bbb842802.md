

## 16. (程序) a. 下列是一个用于将实数四舍五入到 n 位小数的有用编程算法：

- 第 1 步：将该数乘以 10ⁿ。
- 第 2 步：加上 0.5。
- 第 3 步：删除结果的小数部分。
- 第 4 步：除以 10ⁿ。

例如，使用此算法将数字 78.374625 四舍五入到三位小数得到：

- 第 1 步：78.374625 × 10³ = 78374.625
- 第 2 步：78374.625 + 0.5 = 78375.125
- 第 3 步：保留整数部分 = 78375
- 第 4 步：78375 除以 10³ = 78.375

使用此算法，编写一个 C++ 函数，该函数接受用户输入的值并返回四舍五入到两位小数的结果。

### b. 将练习 16a 中编写的函数包含在一个可工作的程序中。确保你的函数从 main() 中被调用并正确地向 main() 返回值。让 main() 使用 cout 语句显示返回的值。通过向其传递各种数据来测试该函数并验证返回的值。

## 6.3 返回多个值

在典型的函数调用中，被调用的函数从其调用函数接收值，存储和操作传递的值，并直接返回最多一个值。当以这种方式传递数据时，它被称为按值传递。

按值调用函数并传递参数是 C++ 的一个显著优势。它允许函数作为独立的实体编写，可以使用任何变量或参数名，而不必担心其他函数可能使用相同的名称。它还消除了在一個函数中更改参数或变量可能会无意中更改另一个函数中参数或变量值的任何担忧。在这种方法中，参数可以被视为已初始化的变量，或在函数执行时被赋值的变量。然而，被调用的函数在任何时候都无法直接访问在调用函数中定义的任何变量，即使该变量在函数调用中用作参数。

然而，有时你需要通过让被调用函数直接访问其调用函数的变量来修改这种方法。这种方法允许一个函数——被调用的函数——使用和更改在调用函数中定义变量的值。这样做需要将变量的地址传递给被调用函数。在被调用函数获得变量的地址后，它“知道变量存储在哪里”，因此可以访问并更改存储在那里的值。

## 使用函数的模块化

传递地址被称为函数的 **按引用传递**，因为被调用的函数可以引用或访问已传递地址的变量。C++ 提供了两种类型的地址参数：引用和指针。下一节描述使用引用参数的方法。

### 传递和使用引用参数

与往常一样，在两个函数之间交换数据时，你必须同时关注发送方和接收方。从发送方来看，调用函数并将地址作为参数传递，该参数在接收方被接受为引用参数，与调用函数并传递值相同；通过给出其名称和参数列表，被调用函数被召唤执行。例如，语句 `newal(firstnum, secnum);` 调用名为 `newal()` 的函数并向其传递两个参数。实际传递的是值还是地址取决于为 `newal()` 声明的参数类型。现在来看一下编写 `newal()` 函数和原型，使其接收变量 `firstnum` 和 `secnum` 的地址而不是值，假设它们是双精度变量。

编写 `newal()` 的第一个要求之一是声明两个引用参数以接受传递的地址。在 C++ 中，引用参数的声明语法如下：

```
dataType& referenceName
```

例如，引用声明

```
double& num1;
```

声明 num1 是一个引用参数，用于存储一个 double 的地址。类似地，`int& secnum;` 声明 secnum 是对一个整数的引用，而 `char& key;` 声明 key 是对一个字符的引用。

在 C++ 中，& 表示“地址”。此外，当 & 用于声明时，它指的是“前一个数据类型”的“地址”。利用这些信息，像 `double& num1` 和 `int& secnum` 这样的声明如果倒过来读会更清晰。按这种方式读取声明 `double& num1` 得到的信息是“num1 是双精度值的地址”。（该主题在第 8.1 节中有更详细的讨论。）

因为你需要在 `newal()` 的参数列表中接受两个地址，所以可以使用声明 `double& num1` 和 `double& num2`。将这些声明包含在 `newal()` 的参数列表中，并假设函数不返回值（void），`newal()` 的函数头如下：

```
void newal(double& num1, double& num2)
```

对于此函数头，以下是一个合适的函数原型：

```
void newal(double&, double&);
```

该原型和函数头包含在程序 6.8 中，该程序使用 newval() 函数体在被调用函数内部显示和更改这些引用变量存储的值。

### 程序 6.8

```
#include <iostream>
using namespace std;

void newval(double&, double&); // prototype with two reference parameters

int main()
{
    double firstnum, secnum;

    cout << "Enter two numbers: ";
    cin >> firstnum >> secnum;
    cout << "\nThe value in firstnum is: " << firstnum << endl;
    cout << "The value in secnum is: " << secnum << "\n\n";

    newval(firstnum, secnum);    // call the function

    cout << "The value in firstnum is now: " << firstnum << endl;
    cout << "The value in secnum is now: " << secnum << endl;

    return 0;
}

void newval(double& xnum, double& ynum)
{
    cout << "The value in xnum is: " << xnum << endl;
    cout << "The value in ynum is: " << ynum << "\n\n";
    xnum = 89.5;
    ynum = 99.5;

    return;
}
```

在程序 6.8 中调用 newval() 函数时，你需要理解函数调用中使用的参数 firstnum 和 secnum 与函数头中使用的参数 xnum 和 ynum 之间的联系。两者都引用相同的数据项。其意义在于，参数 firstnum 和 secnum 中的值现在可以从 newval() 内部通过使用参数名 xnum 和 ynum 来更改。因此，参数 xnum 和 ynum 并不是存储 firstnum 和 secnum 值副本；相反，它们访问为这两个参数保留的内存位置。

图 6.7 显示了程序 6.8 中参数名与参数名的等价性，这是按引用传递的本质。参数名及其匹配的参数名只是引用相同内存存储区域的不同名称。在 main() 中，这些内存位置由参数名 firstnum 和 secnum 引用，而在 newval() 中，相同的内存位置由参数名 xnum 和 ynum 引用。

![](img/202cface8244f523c2641baa2e00d7dd_279_0.png)

**图 6.7** 程序 6.8 中参数与参数的等价性

以下是程序 6.8 的一个示例运行：

```
Enter two numbers: 22.5 33.0

The value in firstnum is: 22.5
The value in secnum is: 33

The value in xnum is: 22.5
The value in ynum is: 33
The value in firstnum is now: 89.5
The value in secnum is now: 99.5
```

在回顾此输出时，注意参数 xnum 和 ynum 最初显示的值与参数 firstnum 和 secnum 显示的值相同。然而，因为 xnum 和 ynum 是引用参数，newval() 现在可以直接访问参数 firstnum 和 secnum。因此，对 newval() 中 xnum 的任何更改都会更改 main() 中 firstnum 的值，而对 ynum 的任何更改都会更改 secnum 的值。正如最终显示的值所示，对 newval() 中 xnum 和 ynum 的赋值在 main() 中反映为 firstnum 和 secnum 值的更改。

程序 6.8 中所示的实际调用参数与函数参数之间的等价性为从函数内部返回多个值提供了基础。例如，假设你想编写一个函数来接受三个值，计算这些值的和


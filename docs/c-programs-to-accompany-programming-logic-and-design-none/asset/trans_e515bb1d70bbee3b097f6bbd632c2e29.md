
> **注意**
>
> 在C++中，当你编写需要多个参数的函数时，必须分别列出这些参数，即使它们具有相同的数据类型。

它被突出显示，并包含两个形参，即 double amount 和 double rate，这些形参列在圆括号内并用逗号分隔。名为 `balance` 的变量的值作为实参按值传递给 `computeTax` 函数，并存储在名为 amount 的形参中。名为 rate 的变量的值作为实参按值传递给 `computeTax` 函数，并存储在名为 rate 的形参中。如图7-3所示，被传递的其中一个参数 rate 与接收的参数 rate 同名并不重要，因为它们占用不同的内存位置。

> **注意** 传递给函数的实参数量没有限制，但是当向函数传递多个实参时，函数调用和函数头必须匹配。这意味着实参/形参的数量必须相同，它们的数据类型必须相同，并且它们的列出顺序必须相同。

> **注意**
>
> 注意第8行的函数声明指定了两个参数（实参），它们的数据类型都是 `double`。这与第21行传递给 `computeTax` 的两个 double 值以及第26行函数头中接收的两个 double 值一致。

接下来，你将学习如何编写一个向调用它的函数返回值的函数。

### 练习7-3：编写需要多个参数的函数

在本练习中，你将运用所学的关于编写需要多个参数的C++函数的知识。

- 1. 给定以下函数调用和变量声明，编写函数的函数头和函数声明：

  - a.
    ```cpp
    string name, date;
    printBirthdayInvitation(name, date);
    ```

  - b.
    ```cpp
    double one_length, two_length;
    calculateRectangleArea(one_length, two_length);
    ```

  - c.
    ```cpp
    int day, month, year;
    printNotice(day, month, year);
    ```

- 2. 给定以下函数头和变量声明，编写一个函数调用：

  - a.
    ```cpp
    string custName = "Smith";
    double balance = 54000;
    void custInfo(string name, double bal)
    ```

  - b.
    ```cpp
    int val1 = 10, val2 = 20;
    void printSum(int num1, int num2)
    ```

  - c.
    ```cpp
    double salary = 37500, percent = .10;
    void increase(double sal, double pcnt)
    ```

### 实验7-3：编写需要多个参数的函数

在本实验中，你将完成一个部分编写的C++程序，该程序包含一个需要多个参数（实参）的函数。程序提示用户输入商品价格和订购数量。如果商品价格低于 $5.00，程序应应用5%的折扣；如果商品价格在 $5.00 到 $9.99 之间，程序应应用10%的折扣；如果商品价格为 $10.00 或更高，程序应应用15%的折扣。应用折扣后，程序应计算所购买商品数量的总价，然后显示原价、折扣百分比、折后价格、订购数量以及所订购商品的总价。本实验提供的源代码文件包含变量声明和输入语句。文件中包含注释，可帮助你编写程序的其余部分。

- 1. 使用记事本或你选择的文本编辑器打开名为 `DiscountPrices.cpp` 的源代码文件。
- 2. 按照注释指示编写C++语句。
- 3. 将此源代码文件保存到你选择的目录中，然后使该目录成为你的工作目录。
- 4. 编译源代码文件 `DiscountPrices.cpp`。
- 5. 执行该程序。

## 编写返回值函数

到目前为止，在本书中，你编写的函数（除了 `main` 函数）都没有返回值。这些函数的函数头都包含关键字 `void`，如下所示：

```cpp
void nameAndAddress()
```

表示该函数不返回值。然而，作为程序员，你经常会发现需要编写确实会返回值的函数。在C++中，一个函数只能返回一个值；当你编写函数的代码时，必须指明要返回的值的数据类型。这通常称为函数的**返回类型**。返回类型可以是C++的任何内置数据类型，也可以是类类型，例如 `string`。你将在本书第10章学习更多关于类的知识。现在，我们将重点讨论返回内置类型和 `strings` 的值。

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_134_0.png)

在*《编程逻辑与设计（第五版）》*第7章中，你研究了一个程序的设计，该程序包含一个名为 `getHoursWorked` 的函数。该函数旨在提示用户输入员工工作的小时数，获取该值，然后将该值返回到程序中调用该函数的位置。实现该设计的C++代码如图7-4所示。

```cpp
1    // GrossPay.cpp - This program computes an employee's gross pay.
2    // Input:  Interactive
3    // Output: The employee's hours worked and their gross pay
4
5    #include <iostream>
6    #include <string>
7    using namespace std;
8    double getHoursWorked();
9
10   int main()
11   {
12       double hours;
13       const double PAY_RATE = 12.00;
14       double gross;
15
16       hours = getHoursWorked();
17       gross = hours * PAY_RATE;
18
19       cout << "Hours worked: " << hours << endl;
20       cout << "Gross pay is: " << gross << endl;
21
22       return 0;
23   } // End of main function
24
25   double getHoursWorked()
26   {
27       double workHours;
28
29       cout << "Please enter hours worked: ";
30       cin >> workHours;
31
32       return workHours;
33   } // End of getHoursWorked function
```

**图7-4** 包含 `getHoursWorked` 函数的程序的C++代码

图7-4所示的C++程序在 `main` 函数的第12、13和14行声明了局部常量以及变量 `hours`、`PAY_RATE` 和 `gross`。下一条语句（第16行）如下所示，是一条赋值语句：

```cpp
hours = getHoursWorked();
```

该赋值语句包含对名为 `getHoursWorked` 的函数的调用。与所有赋值语句一样，先计算赋值运算符（`=`）右侧的表达式，然后将结果赋给赋值运算符（`=`）左侧命名的变量。在此示例中，右侧的表达式是对 `getHoursWorked` 函数的调用。

当调用 `getHoursWorked` 函数时，程序控制权转移到该函数。注意，该函数的函数头（第25行）编写如下：

```cpp
double getHoursWorked()
```

函数头中使用关键字 `double`，以指定该函数返回一个 `double` 数据类型的值。另外，请注意程序第8行，函数声明与函数头一致。也就是说，函数声明指定该函数返回一个 `double`。

然后，在第27行声明一个名为 `workHours` 的局部 `double` 变量。第29行要求用户输入工作小时数，第30行获取该值并将其存储在名为 `workHours` 的局部变量中。随后第32行的return语句将 `workHours` 中存储的值（数据类型为 `double`）的副本返回到调用函数中调用 `getHoursWorked` 的位置，即第16行赋值语句的右侧。

返回到赋值语句右侧的值随后被赋给 `main` 函数中名为 `hours` 的变量（数据类型为 `double`）。接下来，在第17行计算总工资，然后第19行和第20行的 `cout` 语句显示局部变量 `hours` 和 `gross` 的值，这些变量包含工作小时数和计算出的总工资。

你也可以直接使用函数的返回值，而不是将其存储在变量中。接下来的两条C++语句调用图7-4中所示的同一个 `getHoursWorked` 函数，但在这些语句中，返回值直接用于计算总工资的语句和打印返回值的语句：

```cpp
gross = getHoursWorked() * PAY_RATE;
cout << "Hours worked are " << getHoursWorked() << endl;
```

接下来，你将学习如何将整个数组传递给函数，以及如何将数组的各个元素传递给函数。

### 练习7-4：编写返回值的函数

在本练习中，你将运用所学的关于在C++中编写返回值函数的知识。


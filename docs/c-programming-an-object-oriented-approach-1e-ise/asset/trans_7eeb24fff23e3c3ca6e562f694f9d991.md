
## 6.5 关于参数的更多内容

还有两个与参数相关的问题必须讨论：默认参数和重载函数。

### 6.5.1 默认参数

程序可能会多次调用一个函数。如果函数设计为按值传递参数，那么可能出现某个参数的值在大多数情况下都相同的情况。在这种情况下，我们可以为一个或多个参数值（包括所有参数）使用**默认参数**值。如果只有部分参数具有默认参数，那么它们必须是*最右边的参数*。

**示例 6.18**

假设我们设计了一个名为 *calcEarnings* 的函数，用于计算一组员工的每周总收入。该函数使用两个参数：*rate* 和 *hours*。大多数员工工作 40 小时；但有些员工工作更少。我们假设没有员工可以工作超过 40 小时（公司规定）。我们可以在这个函数中为参数 *hours* 使用默认值 40，只需在参数列表中为该参数指定默认值即可。下面的声明语句展示了名为 *calcEarnings*、默认工作时间为 40 小时的函数的声明。

```cpp
double calcEarnings (double rate, double hours = 40.0);
```

请注意，如果没有函数声明（当函数定义出现在函数调用之前时），那么正如我们之前讨论的，函数定义就充当函数声明。这意味着默认参数必须定义在函数定义的头部中。

当员工工作 40 小时时，我们可以只传递 *rate* 参数的实参来调用 *calcEarnings*。当员工工作少于 40 小时时，我们同时传递 *rate* 和 *hours*。下面的示例演示了默认参数的概念。

```cpp
calcEarnings (payRate);
calcEarnings (payRate, hoursWorked);
```

在第一次调用中，程序会为员工的工作小时数插入默认值 40。请注意，默认参数必须是函数参数列表中最右边（最后）的参数。程序 6.18 展示了这一概念。

**程序 6.18 使用默认值**

```cpp
/****************************************************
 * This program shows how we use the default parameter value.  *
 ****************************************************/
#include <iostream>
using namespace std;

// Declaration: the second parameter uses a default value of 40
double calcEarnings (double rate, double hours = 40);

int main()
{
    // The first function call uses the default value
    cout << "Employee 1 pay: " << calcEarnings (22.0) << endl;
    cout << "Employee 2 pay: " << calcEarnings (12.50, 18);
    return 0;
}
/************************************************************
 * The function definition has two parameters, but we do not *
 * have to show the default parameter in the function because *
 * it is the declaration that contains the default value.    *
 ************************************************************/
double calcEarnings (double rate, double hours)
{
    double pay;
    pay = hours * rate;
    return pay;
} // End of calcEarnings
```

运行结果：
```text
Employee 1 pay: 880
Employee 2 pay: 225
```

### 6.5.2 函数重载

我们可以有两个同名函数吗？如果它们的参数列表不同（类型、数量或顺序不同），答案就是肯定的。在 C++ 中，这种做法称为**函数重载**。编译器用来允许程序中存在两个同名函数的标准称为**函数签名**。函数的签名是函数名与参数列表中类型的组合。如果两个函数定义具有不同的签名，编译器就能区分它们。请注意，函数的返回类型不包含在签名中，因为 C++ 在调用函数时必须从重载函数中进行选择；返回类型不包含在函数调用的语法中。

> **函数的返回值不包含在其签名中。**

**示例 6.19**

下面展示了如何定义不同的函数，以分别求两个整数之间以及两个浮点值之间的最大值。

```cpp
int max (int a, int b)
{
    ...
}

double max (double a, double b)
{
    ...
}
```

上述两个函数被视为两个不同（重载）的函数，因为它们的签名不同。第一个函数（左边的那个）的签名是 *max (int, int)*；第二个函数的签名是 *max (double, double)*。

**示例 6.20**

下面两个函数不会被识别为两个重载函数，因为它们的签名相同。

```cpp
int get ()
{
  ...
}

double get ()
{
  ...
}
```

第一个函数的签名是 *get ( )*；第二个函数的签名也是 *get ( )*。如果我们编写一个包含上述两个定义的程序，它无法编译。

> **编译器不会编译包含两个具有相同签名的函数定义的程序。**

**示例 6.21**

重载可以帮助我们在一个函数内部调用另一个函数。例如，我们可以编写三个重载函数，分别求两个整数中的最大值、三个整数中的最大值和四个整数中的最大值。第二个函数在其定义中调用第一个函数；第三个函数调用第二个函数。程序 6.19 演示了这一概念。

**程序 6.19 创建三个重载函数**

```cpp
/**************************************************************
 * This program shows how we can use different signatures to  *
 * create three overloaded functions.                         *
 **************************************************************/
#include <iostream>
using namespace std;

// Function Declaration
int max (int num1, int num2);
int max (int num1, int num2, int num3);
int max (int num1, int num2, int num3, int num4);

int main ()
{
  // Three calls to overloaded max functions
  cout << "maximum (5, 7):" << max (5, 7) << endl;
  cout << "maximum (7, 9, 8):" << max (7, 9, 8) << endl;
  cout << "maximum (14, 3, 12, 11):" << max (14, 3, 12, 11);
  return 0;
} // End main
/**************************************************************
 * The following is the definition for the max function with    *
 * two arguments num1 and num2. It returns the maximum of the   *
 * parameters.                                                  *
 **************************************************************/
int max (int num1, int num2)
{
    int larger; // Local variable
    if (num1 >= num2)
    {
        larger = num1;
    }
    else
    {
        larger = num2;
    }
    return larger;
}
/**************************************************************
 * The following is the definition for the max function with    *
 * three arguments num1, num2, and num3. It uses a call to      *
 * the function with two arguments to first find the maximum    *
 * of the first two. It then makes another call to the first    *
 * function to find the maximum of the result and the num3.     *
 **************************************************************/
int max (int num1, int num2, int num3)
{
    return max(max(num1, num2), num3);
}
/**************************************************************
 * The following is the definition for the max function with    *
 * four arguments num1, num2, num3, and num4. It uses a         *
 * call to the function with three arguments first to find      *
 * the maximum of the first three, and then calls the function  *
 * with two arguments to find the max of the previous result    *
 * and the fourth number.                                       *
 **************************************************************/
int max (int num1, int num2, int num3, int num4)
{
    return max(max(num1, num2, num3), num4);
} // End max function with four parameters
```

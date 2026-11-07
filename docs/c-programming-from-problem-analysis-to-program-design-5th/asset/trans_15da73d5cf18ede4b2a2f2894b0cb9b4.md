
在C++中，*return* 是一个保留字。

当 *return* 语句在函数中执行时，函数立即终止，控制权返回给调用者。此外，函数调用语句会被 *return* 语句返回的值替换。当 *return* 语句在 main 函数中执行时，程序终止。

为了将上述讨论中的思想付诸实践，让我们编写一个函数来确定两个数中的较大者。因为该函数比较两个数，所以它有两个参数，且两个参数都是数字。假设这些数字的数据类型是浮点数（十进制）——例如 double。因为较大的数是 double 类型，所以函数的类型也是 double。让我们将这个函数命名为 larger。完成这个函数所需的唯一东西就是函数体。因此，按照函数的语法，你可以将这个函数写成如下形式：

```cpp
    double larger(double x, double y)
    {
        double max;

        if (x >= y)
            max = x;
        else
            max = y;

        return max;
    }
```

注意，函数 **larger** 要求你使用一个额外的变量 **max**（称为**局部声明**，其中 **max** 是函数 **larger** 的局部变量）。图6-1描述了函数 **larger** 的各个部分。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_368_0.png)

假设 num、num1 和 num2 是 double 变量。还假设 num1 = 45.75，num2 = 35.50。图6-2展示了对函数 larger 的各种调用。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_369_0.png)

图6-2 函数调用

你还可以将函数 `larger` 的定义写成如下形式：

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

因为函数中 return 语句的执行会终止函数，所以前面的函数 larger 也可以（不包含 else）写成：

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;

    return y;
}
```

注意，这些形式的函数 `larger` 不要求你声明任何局部变量。

- 1. 在函数 `larger` 的定义中，x 和 y 是形式参数。
- 2. `return` 语句可以出现在函数的任何位置。回想一下，一旦 `return` 语句执行，所有后续语句都会被跳过。因此，最好在计算出值后立即返回它。

## 示例6-2

现在函数 larger 已经编写好了，下面的 C++ 代码说明了如何使用它。

```cpp
double one = 13.00;
double two = 36.53;
double maxNum;
```

考虑以下语句：

```cpp
cout << "The larger of 5 and 6 is " << larger(5, 6)
     << endl;                                      //Line 1

cout << "The larger of " << one << " and " << two
     << " is " << larger(one, two) << endl;        //Line 2

cout << "The larger of " << one << " and 29 is "
     << larger(one, 29) << endl;                   //Line 3

maxNum = larger(38.45, 56.78);                     //Line 4
```

- 第1行中的表达式 `larger(5, 6)` 是一个函数调用，5 和 6 是实际参数。当表达式 `larger(5, 6)` 执行时，5 被复制到 x，6 被复制到 y。因此，第1行中的语句输出 5 和 6 中的较大者。
- 第2行中的表达式 `larger(one, two)` 是一个函数调用。这里，one 和 two 是实际参数。当表达式 `larger(one, two)` 执行时，one 的值被复制到 x，two 的值被复制到 y。因此，第2行中的语句输出 one 和 two 中的较大者。
- 第3行中的表达式 `larger(one, 29)` 也是一个函数调用。当表达式 `larger(one, 29)` 执行时，one 的值被复制到 x，29 被复制到 y。因此，第3行中的语句输出 one 和 29 中的较大者。
- 第4行中的表达式 `larger(38.45, 56.78)` 是一个函数调用。在这个调用中，实际参数是 38.45 和 56.78。在这个语句中，函数 larger 返回的值被赋给变量 maxNum。

> **注意**
>
> 在函数调用中，你只指定实际参数，而不指定其数据类型。例如，在示例6-2中，第1、2、3行中的语句展示了如何使用实际参数调用函数 larger。但是，以下语句包含对函数 larger 的错误调用，会导致语法错误。（假设所有变量都已正确声明。）
>
> ```
> x = larger(int one, 29);        //illegal
> y = larger(int one, int 29);    //illegal
> cout << larger(int one, int two); //illegal
> ```

一旦编写了一个函数，你就可以在程序中的任何地方使用它。函数 `larger` 比较两个数并返回两者中的较大者。现在让我们编写另一个函数，使用这个函数来确定三个数中的最大者。我们称这个函数为 `compareThree`。

```cpp
double compareThree(double x, double y, double z)
{
    return larger(x, larger(y, z));
}
```

在函数头中，x、y 和 z 是形式参数。

让我们看一下这个表达式：

```cpp
larger(x, larger(y, z))
```

在函数 `compareThree` 的定义中，这个表达式包含两次对函数 `larger` 的调用。外层调用的实际参数是 x 和 `larger(y, z)`；内层调用的实际参数是 y 和 z。因此，首先计算表达式 `larger(y, z)`；也就是说，内层调用先执行，得到 y 和 z 中的较大者。假设 `larger(y, z)` 计算得到 t（注意 t 是 y 或 z）。接下来，外层调用确定 x 和 t 中的较大者。最后，`return` 语句返回最大的数。因此，要执行函数调用，需要先对参数进行求值。例如，外层调用的实际参数 `larger(y, z)` 会先被求值。

注意，函数 `larger` 比函数 `compareThree` 更具通用性。这里，我们仅仅是在说明，一旦你编写了一个函数，你就可以用它来编写其他函数。本章后面将演示如何使用函数 `larger` 从一组数中确定最大的数。

## 函数原型

现在你大致了解了如何在程序中编写和使用函数，接下来的问题涉及用户自定义函数在程序中应出现的顺序。例如，你是将函数 `larger` 放在函数 `main` 之前还是之后？`larger` 应该放在 `compareThree` 之前还是之后呢？根据“必须在使用标识符之前声明它”的规则，并且知道函数 `main` 使用了标识符 `larger`，从逻辑上讲，你必须将 `larger` 放在 `main` 之前。

实际上，C++ 程序员习惯上将函数 `main` 放在所有其他用户自定义函数之前。然而，这种组织方式可能会产生编译错误，因为函数是按照它们在程序中出现的顺序编译的。例如，如果函数 `main` 放在函数 `larger` 之前，那么在编译函数 `main` 时，标识符 `larger` 是未定义的。为了绕过这种未声明标识符的问题，我们将**函数原型**放在任何函数定义（包括 `main` 的定义）之前。

**函数原型：** 没有函数体的函数头。

### 语法：函数原型

返回值函数的函数原型的一般语法是：

```cpp
functionType functionName(parameter list);
```

（请注意，函数原型以分号结尾。）

对于函数 larger，其原型是：

```cpp
double larger(double x, double y);
```

> **注意**
>
> 编写函数原型时，你不必在参数列表中指定变量名。但是，你必须指定每个参数的数据类型。
>
> 你可以将函数 larger 的函数原型改写如下：
>
> ```cpp
> double larger(double, double);
> ```

## 最终程序

现在你已经有足够的知识来编写整个程序、编译并运行它了。下面的程序使用函数 larger、compareThree 和 main 来确定两个或三个数中的较大者/最大者。

```cpp
//Program: Largest of three numbers

#include <iostream>

using namespace std;

double larger(double x, double y);
double compareThree(double x, double y, double z);

int main()
{
    double one, two;                              //Line 1

    cout << "Line 2: The larger of 5 and 10 is "
         << larger(5, 10) << endl;                //Line 2

    cout << "Line 3: Enter two numbers: ";        //Line 3
    cin >> one >> two;                             //Line 4
    cout << endl;                                  //Line 5

    cout << "Line 6: The larger of " << one
         << " and " << two << " is "
         << larger(one, two) << endl;              //Line 6
```

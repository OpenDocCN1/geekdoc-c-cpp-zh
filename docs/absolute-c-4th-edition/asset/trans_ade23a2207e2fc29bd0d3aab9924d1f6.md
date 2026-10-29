

# 显示 13.2 显示 13.1 中函数的迭代版本

```cpp
//Uses iostream:
void writeVertical(int n)
{
    int nsTens = 1;
    int leftEndPiece = n;
    while (leftEndPiece > 9)
    {
        leftEndPiece = leftEndPiece/10;
        nsTens = nsTens*10;
    }
    //nsTens is a power of ten that has the same number
    //of digits as n. For example, if n is 2345, then
    //nsTens is 1000.

    for (int powerOf10 = nsTens;
             powerOf10 > 0; powerOf10 = powerOf10/10)
    {
        cout << (n/powerOf10) << endl;
        n = n%powerOf10;
    }
}
```

显示 13.1 中给出的函数的版本。非递归函数的版本通常使用某种循环（或循环）来代替递归。因此，非递归版本通常被称为**迭代版本**。如果用显示 13.2 中给出的版本替换显示 13.1 中给出的函数 `writeVertical` 的定义，输出将是相同的。正如本例所示，函数的递归版本有时可能比迭代版本简单得多。

递归编写的函数通常运行速度较慢并且使用比等效的迭代版本更多的存储空间。计算机必须做大量的工作来操作栈以跟踪递归。然而，由于系统会自动为你完成所有这些工作，使用递归有时可以使你作为程序员的工作更轻松，有时可以产生更易于理解的代码。

## 自测练习

- 6. 如果你的程序产生错误信息说“stack overflow”，错误的可能来源是什么？
- 7. 编写函数 `cheers` 的迭代版本，该函数定义在自测练习 1 中。
- 8. 编写自测练习 2 中定义的函数的迭代版本。
- 9. 编写自测练习 3 中定义的函数的迭代版本。

## 13.2 返回值的递归函数

> _迭代是人类的，递归是神圣的。_
> 
> —匿名

### 返回值递归函数的通用形式

到目前为止你看到的递归函数都是 void 函数，但递归并不限于 void 函数。递归函数可以返回任何类型的值。设计返回值的递归函数的技术基本上与 void 函数相同。成功返回值的递归函数定义的概要如下：

- 一个或多个情况下，返回的值是通过对同一函数的调用计算得出的（即使用递归调用）。与 void 函数的情况一样，递归调用的参数最终应该是“更小”的。
- 一个或多个情况下，返回的值是在不使用任何递归调用的情况下计算得出的。这些没有递归调用的情况称为 _基本情况_ 或 _停止情况_（与 void 函数的情况一样）。

下一编程示例说明了这种技术。

## 示例 另一个幂函数

第 3 章介绍了预定义函数 pow，它计算幂。例如，pow(2.0, 3.0) 返回 2.0³，或以下将变量 result 设置为 8.0：

```
double result = pow(2.0, 3.0);
```

函数 pow 接受两个 double 类型的参数并返回 double 类型的值。显示 13.3 包含一个递归定义，用于定义一个类似但使用类型 int 而不是 double 的函数。这个新函数称为 power。例如，以下将使 result2 的值等于 8，因为 2³ 是 8：

```
int result2 = power(2, 3);
```

我们定义函数 power 的主要原因是有一个简单的递归函数示例，但在某些情况下，函数 power 会比函数

# 显示 13.3 递归函数 power

```
//Program to demonstrate the recursive function power.
#include <iostream>
#include <cstdlib>
using std::cout;
using std::endl;

int power(int x, int n);
//Precondition: n >= 0.
//Returns x to the power n.

int main()
{
    for (int n = 0; n < 4; n++)
        cout << "3 to the power " << n
            << " is " << power(3, n) << endl;

    return 0;
}

//uses iostream and cstdlib:
int power(int x, int n)
{
    if (n < 0)
    {
        cout << "Illegal argument to power.\n";
        exit(1);
    }

    if (n > 0)
        return ( power(x, n - 1)*x );
    else // n == 0
        return (1);
}
```

## 示例对话

3 to the power 0 is 1
3 to the power 1 is 3
3 to the power 2 is 9
3 to the power 3 is 27

pow 更可取。函数 pow 返回 double 类型的值，这只是一个近似量。函数 power 返回 int 类型的值，这是一个精确量。在某些情况下，你可能需要函数 power 提供的额外精度。

函数 power 的定义基于以下公式：

x^n 等于 x^(n-1) * x

将其翻译成 C++ 表示 power(x, n) 返回的值应与表达式的值相同

```
power(x, n - 1)*x
```

显示 13.3 中给出的函数 power 的定义确实为 power(x, n) 返回此值，前提是 n > 0。

n 等于 0 的情况是停止情况。如果 n 为 0，则 power(x, n) 仅返回 1（因为 x^0 为 1）。

让我们看看当函数 power 用一些示例值调用时会发生什么。首先考虑以下简单表达式：

```
power(2, 0)
```

当函数被调用时，x 的值被设置为 2，n 的值被设置为 0，并且函数定义体中的代码被执行。由于 n 的值是合法值，因此 if-else 语句被执行。由于此 n 值不大于 0，因此使用 else 之后的 return 语句，因此函数调用返回 1。因此，以下将使 result3 的值等于 1：

```
int result3 = power(2, 0);
```

现在让我们看一个涉及递归调用的例子。考虑表达式

```
power(2, 1)
```

当函数被调用时，x 的值被设置为 2，n 的值被设置为 1，并且函数定义体中的代码被执行。由于此 n 值大于 0，因此使用以下 return 语句来确定返回的值：

```
return ( power(x, n - 1)*x );
```

在这种情况下等价于

```
return ( power(2, 0)*2 );
```

此时 power(2, 1) 的计算被挂起，此挂起计算的副本被放在栈上，然后计算机开始新的函数调用以计算 power(2, 0) 的值。正如你已经看到的，power(2, 0) 的值是 1。在确定 power(2, 0) 的值后，计算机用其值 1 替换表达式 power(2, 0) 并

恢复挂起的计算。恢复的计算根据上述 return 语句确定 `power(2, 1)` 的最终值如下：

`power(2, 0) * 2 是 1*2，即 2。`

因此，`power(2, 1)` 返回的最终值是 2。所以，以下将使 `result4` 的值等于 2：

```
int result4 = power(2, 1);
```

第二个参数的较大数值会产生更长的递归调用链。例如，考虑语句

```
cout << power(2, 3);
```

`power(2, 3)` 的值计算如下：

```
power(2, 3) 是 power(2, 2)*2
    power(2, 2) 是 power(2, 1)*2
        power(2, 1) 是 power(2, 0)*2
            power(2, 0) 是 1（停止情况）
```

当计算机到达停止情况 `power(2, 0)` 时，有三个挂起的计算。在计算停止情况的返回值后，它恢复最近挂起的计算以确定 `power(2, 1)` 的值。之后，计算机完成其他每个挂起的计算，使用每个计算出的值作为插入到另一个挂起计算中的值，直到它到达并完成原始调用 `power(2, 3)` 的计算为止。整个计算的细节在显示 3.4 中说明。

## 自测练习

- 12. 以下程序的输出是什么？

```
#include <iostream>
using std::cout;
using std::endl;

int mystery(int n);
//Precondition: n >= 1.

int main()
{
    cout << mystery(3) << endl;
    return 0;
}

int mystery(int n)
{
```


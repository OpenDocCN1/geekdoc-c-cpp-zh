
关于这个运算符，还有一点我们必须提及。如果我们没有为类定义赋值运算符，系统会提供一个（合成赋值运算符）。然而，合成的运算符可能并不是我们需要的。此外，以下警告适用于重载运算符：

-   我们应验证宿主对象和参数对象不是同一个对象（不具有相同地址）。如果对象是在堆内存中创建的，这一点尤其重要。因为我们必须在复制参数对象的内容之前删除宿主对象，所以如果两个对象相同，那么与宿主对象在物理上相同的参数对象会被删除，也就没有任何内容可供复制了。
-   我们知道赋值运算符是从右到左结合的。换句话说，如果有 `y = x`，那么我们可以把该运算的结果赋给另一个对象，即 `z = y = x`，它被解释为 `z = (y = x)`。然而，C++ 要求将 `z` 视为对 `y` 的引用。这就是为什么返回的对象必须按引用返回。

## 示例 13.5

表 13.11 展示了 `Fraction` 类的赋值运算符的声明和定义。

## 复合赋值运算符

我们还可以重载另一组运算符，即复合赋值运算符（`+=`、`-=`、`*=`、`/=` 和 `%=`）。我们知道复合赋值的含义。

| 表达式 | 表示 | 等价表达式 |
|---|---|---|
| `fract1 += fract2` | 表示 | `fract1 = fract1 + fract2` |
| `fract1 -= fract2` | 表示 | `fract1 = fract1 - fract2` |
| `fract1 *= fract2` | 表示 | `fract1 = fract1 * fract2` |
| `fract1 /= fract2` | 表示 | `fract1 = fract1 / fract2` |
| `fract1 %= fract2` | 表示 | `fract1 = fract1 % fract2` |

### 表 13.11 赋值运算符

![](img/d68f6199646ca63591a6d8419e0ed4ba_629_0.png)

```cpp
// Declaration of assignment operator
Fraction& operator=(const Fraction& right)

// Definition of assignment operator
Fraction& Fraction::operator=(const Fraction& right)
{
    if (*this != right) // or check inequality in another way
    {
        number = right.number;
        denom = right.denom;
    }
    return *this;
}
```

在这个运算中，*fract1* 是宿主对象，*fract2* 是参数对象。该过程与赋值运算符相同，只是我们必须仔细定义宿主对象的分子和分母。返回的对象是更改后的宿主对象。

## 示例 13.6

表 13.12 展示了 *Fraction* 类的复合赋值运算符的声明和定义。

### 表 13.12 重载复合赋值运算符

| 运算 | 等价运算 | 结果 |
|---|---|---|
| `a/b += c/d` | `a/b = a/b + c/d` | `(a*d + b*c)/(b*d)` |
| `a/b -= c/d` | `a/b = a/b - c/d` | `(a*d - b*c)/(b*d)` |
| `a/b *= c/d` | `a/b = a/b * c/d` | `(a*c)/(b*d)` |
| `a/b /= c/d` | `a/b = a/b / c/d` | `(a*d)/(b*c)` |

```cpp
// Declaration of += operator
Fraction& operator+=(const Fraction& right)

// Definition of += operator
Fraction& Fraction::operator+=(const Fraction& right)
{
    numer = numer * right.denom + denom * right.numer;
    denom = denom * right.denom;
    normalize();
    return *this;
}

// Declaration of -= operator
Fraction& operator-=(const Fraction& right)

// Definition of -= operator
Fraction& Fraction::operator-=(const Fraction& right)
{
    numer = numer * right.denom - denom * right.numer;
    denom = denom * right.denom;
    normalize();
    return *this;
}

// Declaration of *= operator
Fraction& operator*=(const Fraction& right)

// Definition of *= operator
Fraction& Fraction::operator*=(const Fraction& right)
{
    numer = numer * right.numer;
    denom = denom * right.denom;
    normalize();
    return *this;
}

// Declaration of /= operator
Fraction& operator/=(const Fraction& right)

// Definition of /= operator
Fraction& Fraction::operator/=(const Fraction& right)
{
    numer = numer * right.denom;
    denom = denom * right.numer;
    normalize();
    return *this;
}
```

在表 13.12 中，只要运算定义良好，右操作数不必与左操作数属于相同的对象类型。例如，我们可以使用赋值运算符将一个分数与一个整数相加、相减、相乘或相除。该运算定义良好。重载规则不要求宿主对象和参数对象具有相同的类型。

## 13.3.3 其他运算符

还有其他运算符可以实现为成员函数。接下来我们讨论其中一些。

## 间接运算符和成员选择运算符

在 C++ 中，我们经常使用间接运算符（`*`）或成员选择运算符（`->`）来访问存储在栈内存或堆内存中的对象或对象的成员。在重载这两个运算符之前，我们必须提及关于它们的一些要点。

-   这两个运算符都是一元运算符，这意味着它们都只有一个操作数，且该操作数必须是指向相应对象的指针。间接运算符返回该操作数所指向的对象；成员选择运算符将指针操作数变为一个可指向相应对象任意成员的指针，并返回该成员。在第一种情况下，运算符位于操作数之前（前缀）；在第二种情况下，运算符位于操作数之后（后缀），如下所示：

```cpp
// Returns object                 // Returns member
*ptr                              ptr->
```

-   如果我们想重载这两个运算符，就需要一个充当指针的类，因为操作数（宿主对象）必须是指针。

![](img/d68f6199646ca63591a6d8419e0ed4ba_632_0.png)

## 智能指针

当我们使用指针指向栈中的对象时，不需要重载间接运算符和成员选择运算符（`*` 和 `->`）。我们可以使用指针作为一种复合数据类型来指向我们的对象。当对象超出作用域时，它会自动从栈中弹出，不会发生内存泄漏。然而，当我们在堆中创建对象时，必须记得删除它以避免内存泄漏，正如我们在第 9 章所讨论的那样。为此，我们创建一个智能指针，如图 13.8 所示。

智能指针对象是一个只含有一个数据成员的对象：一个指向所需类型（如 `Fraction`）的指针。当调用该对象的构造函数时，它会创建一个指向所需类型的指针。运算符 `*` 和 `->` 已为 `SmartPtr` 类重载，该类可以指向所需对象以及所需对象的成员。

## 示例 13.7

我们创建一个名为 *SmartPtr* 的智能指针类，其接口如程序 13.1 所示。

### 程序 13.1——文件 smartptr.h

```cpp
/*******************************************************
 * The interface file for the SmartPtr class           *
 *******************************************************/
#ifndef SMARTPTR_H
#define SMARTPTR_H
#include <iostream>
using namespace std;

class Fraction;    // Forward declaration
class SmartPtr
{
    private:
        Fraction* ptr;
    public:
        SmartPtr(Fraction* ptr);
        ~SmartPtr();
        Fraction& operator*() const;
        Fraction* operator->() const;
};
#endif
```

注意，我们在第 9 行添加了一个前向声明，以告知头文件：*SmartPtr* 声明中的名称 *Fraction* 是一个类型。*Fraction* 类的声明和定义位于其他文件中，正如我们在第 7 章讨论分离编译原则时所述。

现在我们为 *SmartPtr* 类创建实现（程序 13.2）。注意，析构函数会删除由 *ptr* 成员分配的内存（第 15 行）。

现在我们创建应用程序来测试 *SmartPtr* 类（程序 13.3）。

### 程序 13.2——文件 smartptr.cpp

```cpp
/**************************************************************
 * The implementation file for the SmartPtr class            *
 **************************************************************/
#include "smartptr.h"

// Constructor
SmartPtr::SmartPtr(Fraction* p)
    : ptr(p)
{
}

// Destructor
SmartPtr::~SmartPtr()
{
    delete ptr;
}

// Overloading of indirection operator
Fraction& SmartPtr::operator*() const
{
    return *ptr;
}

// Overloading of the arrow operator
Fraction* SmartPtr::operator->() const
{
    return ptr;
}
```

### 程序 13.3——文件 app.cpp

```cpp
/**************************************************************
 * The application file to test the SmartPtr class           *
 **************************************************************/
#include "smartptr.h"
#include "fraction.h"
```

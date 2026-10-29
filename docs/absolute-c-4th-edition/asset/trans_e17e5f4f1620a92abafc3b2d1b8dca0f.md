

# Display 8.3  作为友元重载运算符（第 1 部分，共 2 部分）

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

//Class for amounts of money in U.S. currency
class Money
{
public:
    Money( );
    Money(double amount);
    Money(int dollars, int cents);
    Money(int dollars);
    double getAmount( ) const;
    int getDollars( ) const;
    int getCents( ) const;
    void input( ); //Reads the dollar sign as well as the amount number.
    void output( ) const;
    friend const Money operator +(const Money& amount1, const Money& amount2);
    friend const Money operator +(const Money& amount1, const Money& amount2);
    friend bool operator ==(const Money& amount1, const Money& amount2);
    friend const Money operator -(const Money& amount);
private:
    int dollars; //A negative amount is represented as negative dollars and
    int cents; //negative cents. Negative $4.50 is represented as -4 and -50.

    int dollarsPart(double amount) const;
    int centsPart(double amount) const;
    int round(double number) const;
};

int main( )
{
    /*If the main function is the same as in Display 8.1, then the screen dialogue
      will be the same as shown in Display 8.1.*/
}

const Money operator +(const Money& amount1, const Money& amount2)
{
    int allCents1 = amount1.cents + amount1.dollars*100;
    int allCents2 = amount2.cents + amount2.dollars*100;
    int sumAllCents = allCents1 + allCents2;
    int absAllCents = abs(sumAllCents); //Money can be negative.
    int finalDollars = absAllCents/100;
```

# Display 8.3  作为友元重载运算符（第 2 部分，共 2 部分）

```cpp
41    int finalCents = absAllCents%100;
42
43    if (sumAllCents < 0)
44    {
45        finalDollars = -finalDollars;
46        finalCents = -finalCents;
47    }
48
49    return Money(finalDollars, finalCents);
50 }

51 const Money operator -(const Money& amount1, const Money& amount2)
52 {
53     bool operator ==(const Money& amount1, const Money& amount2)
54     {
55         return ((amount1.dollars == amount2.dollars)
56                 && (amount1.cents == amount2.cents));
57     }

58 const Money operator -(const Money& amount)
59 {
60     return Money(-amount.dollars, -amount.cents);
61 }
```

*注意友元可以直接访问成员变量。*

*完整定义见自测练习题 7。*

*除 Display 8.1 中所述外，其他所有成员函数的定义均相同。*

# FRIEND FUNCTIONS

类的友元函数是一个普通的函数，只是它可以访问该类对象的私有成员。要使一个函数成为类的友元，必须在类定义中列出该友元函数的函数声明。函数声明前面加上关键字 `friend`。函数声明可以放在私有部分或公有部分，但无论如何它都是一个公有函数，因此更清晰的做法是将其列在公有部分。

# 包含友元函数的类定义的语法

```cpp
class Class_Name
{
public:
    friend Declaration_for_Friend_Function_1
    friend Declaration_for_Friend_Function_2
        .
        .
        .
};
```

*你不必先列出友元函数。你可以交错这些声明的顺序。*

## 1.2 函数

函数是数学中的一个基本概念，它描述了一种从一个集合（定义域）到另一个集合（值域）的对应关系。

在初中阶段，我们主要学习一次函数、二次函数和反比例函数。这些函数在解决实际问题中有着广泛的应用。

- 一次函数：形如 y = kx + b (k ≠ 0) 的函数。
- 二次函数：形如 y = ax² + bx + c (a ≠ 0) 的函数。
- 反比例函数：形如 y = k/x (k ≠ 0) 的函数。

函数的图像是理解函数性质的重要工具。通过图像，我们可以直观地看出函数的增减性、最值等特征。

![](img/9505fd46e120aa9c1406715936ff6251_319_0.png)

> > 数学是打开科学大门的钥匙。

在解决函数问题时，我们常常需要用到数形结合的思想，将代数问题转化为几何问题，或者将几何问题转化为代数问题。

```python
def linear_function(x, k, b):
    return k * x + b
```

当一个类是另一个类的友元时，通常这些类会在其类定义中相互引用。这要求你对第二个定义的类包含一个**前向声明**，如下文概述所示。请注意，前向声明只是类定义的首部后面跟一个分号。

如果你想让类 F 成为类 C 的友元，设置的方式大致如下：

```
class F; //forward declaration

class C
{
public:
    ...
    friend class F;
    ...
};

class F
{
    ...
};
```

使用友元类的完整示例在第 17 章给出。我们到那时才开始使用友元类。

- **Self-Test Exercises**
- 6. 类的友元函数与该类的成员函数有什么区别？
- 7. 完成 Display 8.3 中友元减法运算符 − 的定义。
- 8. 假设你希望重载运算符 < 使其适用于 Display 8.3 中定义的 Money 类型。你需要在 Display 8.3 中给出的 Money 定义中添加什么？

# 8.3 References and More Overloaded Operators

> Do not mistake the pointing finger for the moon.
> 
> — Zen Saying

本节介绍一些专门的但重要的重载主题，包括重载赋值运算符和 <<、>>、[]、++、-- 运算符。因为

# RULES ON OVERLOADING OPERATORS

- 重载运算符时，结果重载运算符的至少一个参数（一个操作数）必须是类类型。
- 大多数运算符可以作为类的成员、类的友元或非成员非友元来重载。
- 以下运算符只能作为类的（非静态）成员来重载：[]、->、->* 和（）。
- 你不能创建新的运算符。你只能重载已有的运算符，如 +、-、*、/、% 等。
- 你不能改变运算符所取参数的个数。例如，你不能在重载时将 % 从二元改为一元；你不能在重载时将 ++ 从一元改为二元。
- 你不能改变运算符的优先级。重载的运算符具有与普通版本运算符相同的优先级。例如，x*y + z 总是表示 (x*y) + z，即使 x、y、z 是对象且运算符 + 和 * 已为适当类重载。
- 以下运算符不能被重载：点运算符（.）、作用域解析运算符（::）、sizeof、?:，以及本书未讨论的运算符 ^。
- 重载的运算符不能有默认参数。

你需要理解返回引用才能以更自然的方式重载某些运算符，因此我们也讨论这个主题。

# REFERENCES

引用是存储位置的名称。² 你可以有独立的引用，如下所示：

```
int robert;
int& bob = robert;
```

这使得 bob 成为变量 robert 的存储位置的引用，这使得 bob 成为变量 robert 的别名。对 bob 所做的任何更改也会对 robert 产生影响。如此表述，独立引用听起来只是使代码变得混乱并惹麻烦的一种方式。在大多数情况下，独立引用只是

² 如果你了解指针，你会注意到引用听起来像指针。引用本质上是，但不完全是，一个常量指针。指针和引用之间存在差异，它们并非完全可以互换。

麻烦，尽管在少数情况下它可能很有用。我们将不再讨论独立引用，也不会使用它们。

正如你可能猜到的，引用用于实现传引用参数机制。因此，这个概念对本章来说并不完全新颖，尽管“引用”这个词是新的。

我们在这里关心引用是因为返回引用将允许你以更自然的方式重载某些运算符。返回引用可以被视为类似于返回一个变量，或更准确地说，返回一个变量的别名。语法细节很简单。你在返回类型中加上一个 &。例如：

```
double& sampleFunction(double& variable);
```

由于像 double& 这样的类型与 double 不同，因此你必须在函数声明和函数定义中都使用 &。返回表达式必须是具有引用的东西，例如适当类型的变量。它不能是表达式，如 X + 5。尽管许多编译器会让你这样做（结果不幸），你也不应返回局部变量，因为你会生成一个别名指向一个变量并立即销毁该变量。函数定义的简单示例是

```
double& sampleFunction(double& variable)
{
    return variable;
}
```

当然，这是一个相当无用、甚至麻烦的函数，但它说明了概念。例如，以下代码将输出 99 然后输出 42：

```
double m = 99;
cout << sampleFunction(m) << endl;
sampleFunction(m) = 42;
cout << m << endl;
```

我们只会在定义某些种类的重载运算符时返回引用。

# L-VALUES AND R-VALUES

术语 l-value 用于可以出现在赋值运算符左侧的东西。术语 r-value 用于可以出现在赋值运算符右侧的东西。

如果你希望函数返回的对象是一个 l-value，它必须通过引用返回。


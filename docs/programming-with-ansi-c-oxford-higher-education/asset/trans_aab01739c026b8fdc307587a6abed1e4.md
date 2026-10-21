

## 6.2 操作符重载的限制

尽管操作符重载是可能的，但它有一套自己的限制，如下所述：

操作符重载为操作符提供额外的含义。

- 1. 操作符不会失去其原始含义；相反，当被重载时，它们具有额外的含义。不能改变操作符的原始含义。
- 2. 不能发明新的操作符。只有具有给定限制的现有操作符才能被重载。
- 3. 操作符将具有额外的含义，但不会具有额外的优先级。优先级保持不变。
- 4. 操作符不能改变原始形式下可用的参数数量。因此，二元形式的‘+’只能有两个参数。它不能用三个参数重载。
- 5. 操作符只能为用户定义的类型重载。所有重载的操作符必须至少有一个参数是用户定义的类型。
- 6. 除 () 外，其他操作符不能有默认参数。
- 7. 有些操作符永远不能被重载。

### 6.2.1 不能被重载的操作符

以下操作符不能被重载：

- 1. 成员访问点操作符 (.)
- 2. 解引用成员到类操作符 (.*)
- 3. 作用域解析操作符 (::)
- 4. sizeof 操作符 (sizeof)
- 5. 条件三元操作符 (?:)
- 6. 强制转换操作符 (static_cast<>, dynamic_cast<>, reinterpret_cast<>, 和 const_cast<>)
- 7. 宏预处理器的 # 和 ## 标记

> 注意 可能有人会问为什么这些操作符不能被重载。考虑重载点操作符。如果它被重载，类成员操作将获得新的含义，这可能导致严重的错误。编译器开发者必须处理由此类错误产生可能的复杂性，并通过提供错误可能的原因来帮助程序员。如果 C++ 允许此类代码，它很容易让编译器因不可预见的副作用而感到困惑。C++ 不允许添加新操作符也是出于同样的原因。C++ 也不允许对某些操作符进行全局定义（例如，= 操作符）。包括 Java 在内的许多语言都不提供操作符重载，因为这是一个非常难以管理的问题。

### 6.2.2 不能作为友元被重载的操作符

如前所述，操作符是作为函数重载的。为了使一个函数对一个类起作用，它应该是成员或友元。其结果是，操作符可以以两种不同的方式重载，即作为成员或作为友元。以下操作符不能作为友元被重载：

- 1. 赋值操作符 =
- 2. 函数调用操作符 ()
- 3. 数组下标操作符 []
- 4. 使用指向对象的指针访问类成员操作符 ->

当操作符被重载时，应遵循原始含义的语法规则。以下是一些示例：

- 1. 所有算术操作符必须返回一个值。然而，它可以与原始操作符返回的类型不同。
- 2. 一元操作符没有显式参数。如果作为友元重载，它们接受一个引用参数。
- 3. 二元操作符如果作为成员重载则接受一个显式参数，如果作为友元重载则接受两个显式参数。

## 6.3 通过成员函数进行操作符重载

操作符函数作为成员的语法与普通成员函数的语法相似，具有特定的命名约定。让我们看一下程序 6.1，它处理复数。

## 程序 6.1 使用重载操作符添加两个复数

```
//00+.cpp
#include <iostream>
#include <string>
using namespace std;

class Complex
{
    float Real;
    float Imag;
public:
    Complex(float TempReal = 0, float TempImag = 0)
    {
        Real = TempReal;
        Imag = TempImag;
    }

    Complex Add(Complex Comp2)
    {
        float TempReal;
        float TempImag;
        TempReal = Real + Comp2.Real;
        TempImag = Imag + Comp2.Imag;
        return Complex(TempReal, TempImag);
    }

    Complex operator +(Complex Comp2)
    {
        float TempReal;
        float TempImag;
        TempReal = Real + Comp2.Real;
        TempImag = Imag + Comp2.Imag;
        return Complex(TempReal, TempImag);
    }

    void Display()
    {
        cout << Real << "+" << Imag << "i \n";
    }
};
```

```
void main()
{
Complex Comp1(10, 20);
Complex Comp2(20, 30);
Complex CompResult1, CompResult2;
CompResult1 = Comp1.Add(Comp2);
CompResult1.Display();
CompResult2 = Comp1 + Comp2;
CompResult2.Display();
}
```

## 程序如何工作

定义复数作为类 在此示例中，复数被视为一个类。复数始终表示为两个部分的集合。第一部分称为实值，第二部分称为虚值。它表示为 <实值> + <虚值>i，即在复数 20 + 30i 中，20 是实部，30 是虚部。这里，i 被认为是 -1 的平方根。

使用复数类的操作符重载 我们在这里的目的是了解如何使用这个特定类在 C++ 中提供操作符重载。我们在此将复数表示为两个值，实部和虚部，并附带一些函数。

- 1. 第一个函数是构造函数。Complex Comp1(1, 2) 将创建一个复数 Comp1，其实值为 1，虚值为 2。
- 2. 第二个函数是显示。Comp1.Display()，它应显示 1 + 2i 。
- 3. 第三个是 Add() 函数。它是类的成员函数，并有一个复数作为参数。这意味着它已经有一个隐式参数，即指向调用对象的 this 指针。它将传递给它的两个 Complex 对象的实部和虚部相加，并将两个对象的和作为另一个 Complex 对象返回。

## Add 函数和重载的 '+'

让我们考虑一个有趣的例子，其中函数的体与 Add() 函数的体相同。它以与 Add() 函数相同的方式工作，但调用方式不同。对操作符函数的调用与对普通函数的调用不同。在查看差异之前，应注意函数的命名。

> 所有操作符函数的名称都以关键字 operator 开头，其后是实际的操作符。在这种情况下，+ 操作符已被重载，因此函数名应为 operator + 。每当 + 操作符被重载时，函数名都将命名为 operator + 。当 – 操作符被重载时，它将被命名为 operator – 等等。

当 + 操作符与两个操作数都为复数参数一起使用时，操作符函数被调用。如前所述，它看起来不像函数调用。

```
CompResult2 = Comp1 + Comp2;
```

它实际上是

```
CompResult2 = Comp1.operator + (Comp2)
```

> 如果操作符被正确重载，它会提高程序的可读性。

查看调用 CompResult2 = Comp1 + Comp2; 它实际上是 CompResult2 = Comp1.operator + (Comp2)

## 注意

尽管操作符是以与函数相同的方式定义的，但它们不是以相同的方式调用的。

函数之所以这样调用，是因为我们希望复数的加法看起来与任何其他数值变量的加法相似。操作符重载的一个优点是，两个函数（Add() 和 operator +()）都在执行相同的活动。操作符重载是 C++ 设计者期望用户定义对象的工作方式与内置对象相似的一个很好的例子。然而，从可读性的角度来看，第二个函数看起来好得多，即 CompResult2 = Comp1 + Comp2 比 CompResult1 = Comp1.add(Comp2) 更具可读性。

## 选择复数来重载 '+'

选择复数示例来说明重载 + 的原因是，尽管 + 可以为任何其他操作重载，但重要的是为与原始含义相似的操作重载它。如果选择其他操作由 + 表示，则可读性会成为问题。例如，如果 + 用于获取参数的乘积作为复数，那么它会让读者感到困惑和误导。

同样，为非数值项重载 + 也会在读者的脑海中造成歧义。有时，尽管 + 表示某种类型的加法，但也可以将其用于非数值操作数。

> 重要的是为与原始操作相似或几乎相似的操作重载操作符。

## 为用户定义类重载 '+'

考虑程序 6.2，它是向集合添加员工的示例。此程序与第 4 章中讨论的 FriendClass.cpp 相同。我们已重载 + 以表示添加到集合中。

## 程序 6.2 向员工集合添加员工

```
#include <iostream>
#include <string>
using namespace std;

class CollectionEmp; // Forward definition
class employee
{
    int EmpNo;
    string Name;
    string DeptName;
    string Designation;
public:
    void Init(int TempNo, string TempName, string TempDept, string TempDesi)
    {
        EmpNo = TempNo;
        Name = TempName;
        DeptName = TempDept;
        Designation = TempDesi;
    }

    void DisplayDetails()
    {
        cout << "Details of employee number" << EmpNo << "\n";
        cout << "Name is" << Name << "\n";
        cout << "Department is " << DeptName << "\n";
```




### 表 A.1 访问权限和继承

| 基类元素的访问权限 | Private | Public | Protected |
|---|---|---|---|
| Private | 不可访问 | 不可访问 | 不可访问 |
| Protected | Private | Protected | Protected |
| Public | Private | Public | Protected |

在表 A.1 中，最左侧一列列出了类元素可能的访问权限。它还包含第三种类型，即 protected。protected 访问权限用于在子类中可直接使用但从外部不可访问的元素。换句话说，我们可以说 protected 元素的访问权限介于 private 和 public 元素之间，因此它们可以在以相应类为根的类层次结构中使用。

第一、第二和第三列分别显示了当子类使用 private、public 和 protected 访问继承时，基类元素的结果访问权限。

## A.10.2 多重继承

如前所述，C++ 允许一个类从多个基类派生。可以通过在逗号分隔的列表中指定基类，轻松地从多个类派生，如下所示。

```
class Son:public Mother, public Father
{
    public:
        Father(...);
        Mother(...);
        Father(...)
        {
            ...
        }
    ~Son()(...)
};
```

## A.11 抽象类

抽象类是指无法创建对象的类。它仅被设计和用作基类。抽象类的定义方式与普通类相似。然而，其中一些成员函数被指定为必须由子类定义。我们只需提及其签名（包括返回类型、名称和参数），但在函数体中不做任何说明。这通过在方法签名后附加 ‘= 0’ 来表示。

```
class Baseclass
{
    ...
    public:
    ...
    virtual void MemberFunction() = 0; // Pure virtual function
};
```

此类定义将强制每个需要创建对象的派生类定义方法 MemberFunction()。这些方法声明也称为纯方法。

### A.11.1.1 纯虚函数

纯虚函数是在基类中没有定义的虚函数。程序代码 A.22 对此进行了说明。

![](img/a99ec79093c067f0bed8f1086197950e_803_0.png)

```
void main()
{
    BaseClass *p, b;
    DerivedClass1 d1;
    DerivedClass2 d2;
    p = &b;
    b->VirFunc();
    // access Base class's virtual function
    p = &d1;
    p->VirFunc();
    // access derived class1's virtual function
    p = &d2;
    p->VirFunc();
    // As derived class2 does not have VirFunc()
    // It will therefore access the derived class1's
    //VirFunc()
}
Output:
From Base class virtual function named VirFunc()
From Derived class1's virtual function named VirFunc()
From Derived class1's virtual function named VirFunc()
```

如程序代码 A.22 所示，当虚函数未被派生类重新定义时，将使用基类中定义的版本。在许多情况下，基类中可能没有虚函数的有意义定义，或者所有派生类都会重写虚函数。

为处理这两种情况，C++ 支持纯虚函数。纯虚函数是在基类中没有定义的函数。

```
virtual type func_name(parameter_list) = 0;
```

当虚函数被设为纯虚函数时，任何派生类都必须提供其自身定义；否则会导致编译时错误。程序代码 A.23 说明了纯虚函数。

```
PROGRAM CODE A.23
// To draw different shapes
class shape
{
    public:
    virtual void Draw() = 0;
};
class line:public shape
{
 int x1, y1, x2, y2;
 public:
 void Draw()
 {
 x1 = 10;
 y1 = 10;
 x2 = 100;
 y2 = 100;
 line (x1, y1, x2, y2);
 }
 };

class circle:public shape
{
 int x1, y1, r;
 public:
 void Draw()
 {
 x1 = 100;
 y1 = 100;
 r = 50;
 circle(x1, y1, r);
 }
 };

class rectangle:public shape
{
 int x1, y1, x2, y2;
 public:
 void Draw()
 {
 x1 = 100;
 y1 = 100;
 x2 = 200;
 y2 = 200;
 rectangle(x1, y1, x2, y2);
 }
 };

void main()
{
 shape *p;
 line L;
 circle C;
 rectangle R;
 int gd = detect, gm;
 initgraph(&gd, &gm, " ");
 p = &L;
 p->Draw(); // draws a line
 p = &C;
 p->Draw(); // draws a circle
 p = &R;
 p->Draw(); // draws a rectangle
}
```

在程序代码 A.23 中，由于每个派生类都应实现其自身的 Draw()，因此它应为纯虚函数。纯方法也必须声明为虚函数，因为我们只希望使用派生类的对象。定义纯方法的类称为抽象类。

## A.12 运算符重载

为数据类型的运算符赋予特殊含义的机制称为运算符重载。它有助于为运算符分配额外任务，并指定其在应用该运算符的类中的含义。运算符重载的一般语法如下：

```
return type class name::operator op(arguments list)
{
...
};
```

这里，op 是被重载的运算符，前面带有关键字 operator，而 operator op 是函数名。

让我们考虑复数的抽象数据类型 Complex，如下所示：

```
class Complex
{
double Real, Imag;
public:
Complex()
{
Real = 0.0;
Imag = 0.0;
}
Complex(const double real, const double imag)
{
Real = real;
Imag = imag;
}
Complex Add(const Complex op);
Complex Mul(const Complex op);
...
};
```

现在可以通过调用函数 Add() 来添加两个复数，如下所示：

```
Complex A(1.0, 2.0), B(3.5, 1.2), C;
C= A.Add(B);
```

这里，我们添加两个复数 A 和 B 并将和赋给 C。此表达式也可以写得类似于整数或实数加法，即 C = A + B。C++ 也允许此表达式。在 C++ 中，我们可以为新创建的类型重载几乎所有运算符。例如，我们可以为类 Complex 定义 ‘+’ 运算符，如下所示：

```
class Complex
{
...
public:
...
Complex operator + (const Complex &op) // member of a class
{
    double real = Real + op.Real;
    double imag = Imag + op.Imag;
    return(Complex(real, imag));
}
...
};
```

在这种情况下，我们将运算符 ‘+’ 作为类 Complex 的成员。现在允许形式为 C = A + B 的表达式。这里，此语句被翻译为

```
C = A.operator + (B);
```

因此，二元运算符 ‘+’ 只需要一个参数。第一个参数由调用对象（在此例中为 A）隐式提供。但是，运算符调用也可以解释为常规函数调用，如下所示：

```
C = operator + (A, B);
```

在这种情况下，重载的运算符不是类的成员。相反，它在类外部定义为普通重载函数。例如，我们可以如下定义 ‘+’ 运算符：

```
class Complex
{
...
public:
...
double real() {return Real;}
double imag() { return Imag; }
};
Complex operator + (Complex &op1, Complex &op2)
{
    double real = op1.Real() + op2.Real();
    double imag = op1.Imag() + op2.Imag();
    return(Complex(real, imag));
}
```

在这种情况下，我们必须为实部和虚部定义访问方法，因为运算符在类作用域之外定义。但是，运算符与类关系密切，允许运算符访问私有成员是合理的。这可以通过将其声明为类 Complex 的友元来实现。

### A.12.1 比较函数重写和重载

让我们比较函数重写与重载。在函数重写中，重新定义的虚函数的原型必须与基类中指定的原型完全匹配，而在函数重载中，原型必须在参数数量或类型上有所不同。

在函数重写中，如果在重新定义虚函数时更改原型，则 C++ 编译器会将该函数视为重载，其虚函数特性将丢失。

- 虚函数必须是其所属类的非静态成员。
- 虚函数不能是友元。构造函数不能是虚函数，但析构函数可以是虚函数。

## A.13 友元函数

友元函数可用于重载二元运算符，而非成员函数。我们可以将函数或类定义为类的友元，以允许它们直接访问其私有数据成员。例如，在 A.12 节中，我们希望 '+' 运算符的非成员函数能够访问类 Complex 的私有数据成员 Real 和 Imag。因此，我们将运算符 '+' 声明为类 Complex 的友元。

```
class Complex
{
    ...
    public:
    ...
    friend Complex operator +
    {
    const Complex &,
```


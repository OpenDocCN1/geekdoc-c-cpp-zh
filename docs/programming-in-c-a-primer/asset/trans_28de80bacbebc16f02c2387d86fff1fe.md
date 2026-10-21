

```
}

public class Fraction
{
    private int numerator;
    private int denominator;

    // create a fraction by passing in the numerator and denominator
    public Fraction(int numerator, int denominator)
    {
        this.numerator = numerator;
        this.denominator = denominator;
    }

    // overloaded operator + takes two fractions
    // and returns their sum
    public static Fraction operator +(Fraction frac1, Fraction frac2)
    {
        // like fractions (shared denominator) can be added by adding their numerators
        if (frac1.denominator == frac2.denominator)
        {
            return new Fraction(frac1.numerator + frac2.numerator, frac1.denominator);
        }

        int product1 = frac1.numerator * frac2.denominator;
        int product2 = frac2.numerator * frac1.denominator;
        return new Fraction(product1 + product2, frac1.denominator * frac2.denominator);
    }

    // return a string representation of the fraction
    public override string ToString()
    {
        String show = numerator.ToString() + " / " +
        denominator.ToString();
        return show;
    }
}
}
```

## 运算符重载

```
The fraction 1 is : 388/6677
The fraction 2 is : 205/47
The output of fraction 1 + fraction 2 is : 1387021/313819
Press any key to continue . . . -
```

## 案例研究

### 问题陈述

Ulinfo Private Limited 为 AeroFly 和 FlyHigh 等公司开发新型飞机。在开发新飞机设计时，Ulinfo 的设计人员需要进行大量复杂计算。手动执行这些复杂计算已成为 Ulinfo 设计人员的一项繁琐任务。Ulinfo 如何才能自动化执行复杂计算的任务？

### 解决方案

ULInfo 的管理层经过多次讨论后得出结论：必须开发一个应用程序来自动化执行复杂计算的任务。为此，他们联系了一家名为 ABC Software Solutions Private Limited 的软件开发公司。这家软件开发公司首先进行需求分析，以了解 UlInfo 的需求。然后决定在 C# 应用程序中使用 C# 的运算符重载特性来重载诸如 + 和 - 之类的运算符，以便可以使用同一运算符执行不同功能。10 天后，ABC Software Solutions Private Limited 提出了以下 C# 应用程序，该应用程序有助于执行诸如两个数字相加和相乘之类的数学运算。

//Operator Overloading using inheritance
using System;
using System.Collections.Generic;
using System.Text;
namespace OperatorOverloading
{
class StoreValue
{
private int num1;
private int num2;
}

```
public StoreValue()
{
}
public StoreValue(int m, int n)
{
    num1 = m+m;
    num2 = n+n;
}
public void DisplayWindow()
{
    Console.WriteLine("The sum of numbers is {0} {1}", num1, num2);
}
}
```

class InheritValue : StoreValue
{
    private double num1 ;
    private double num2 ;
    public InheritValue(double a, double b)
    {
        num1 = a*a;
        num2 = b*b;
    }
    public InheritValue()
    {
    }
    public new void DisplayWindow()
    {
    Console.WriteLine("Now the square of the numbers 355 and 455 are {0} and {1}",num1,num2);
    }
}

class InheritMoreValue : InheritValue
{
    private double num1;
    private double num2;
    public InheritMoreValue(double a, double b)
    {
        num1 = (a * b) / (a+b);
        num2 = (a * b) / (b-a);
    }
    public InheritMoreValue()
    {
    }
    public new void DisplayWindow()
    {
        Console.WriteLine("The value of the numbers 48 and 62 are {0} and {1}", num1, num2);
    }
}
class Program

```
{
static void Main(string[] args)
{
    Console.WriteLine("Operator Overloading with Inheritance.");
    StoreValue Obj1 = new StoreValue(119,280);
    Obj1.DisplayWindow();
    InheritValue Obj2 = new InheritValue(355,455);
    Obj2.DisplayWindow();
    InheritMoreValue Obj3 = new InheritMoreValue(150,250);
    Obj3.DisplayWindow();
}
}
```

备注：通过在 C# 应用程序中使用运算符重载，可以为 +、− 和 ++ 等运算符提供新的定义。运算符重载允许你使用 C# 支持的运算符来处理类和结构体，就像这些运算符处理内置数据类型一样。

## 常见编程错误

-   忘记将运算符方法声明为 public。
-   忘记将运算符方法声明为 static。
-   重载关系运算符时，忘记重载其配对运算符。
-   重载关系运算符时，忘记返回 bool 类型值。
-   重载比较运算符时，尝试比较两个 float 值。
-   关系运算符使用不当。例如，将“大于或等于”符号写成 => 而不是 >=。

## 复习题

15.1 判断下列说法是否正确。
(a) 所有条件运算符都可以重载。
(b) 逻辑运算符必须成对重载。
(c) 我们可以通过重载改变运算符的优先级。
(d) 用于定义运算符重载的运算符方法必须是 public。
(e) 运算符方法从不返回值。
(f) 比较运算符方法必须返回 bool 类型值。

15.2 一元运算符和二元运算符有什么区别？

15.3 如果重载 == 运算符，还应该做什么？

15.4 什么是运算符重载？

15.5 为什么有必要重载运算符？

15.6 什么是运算符方法？描述其语法。

15.7 一元运算符方法的定义中使用多少个参数？

15.8 讨论重载比较运算符和重载算术运算符之间的区别。

15.9 列出可以重载的运算符。

15.10 列出不可重载的运算符。

15.11 举一些可能应用运算符重载的例子。

15.12 找出以下运算符方法头部行中的错误（如果有）：

-   (a) public Matrix operator + (Matrix x, Matrix y)
{}
-   (b) static Vector operator -(Vector a, Vector b)
{}
-   (c) public static Vector operator *(Vector a)
{}
-   (d) public static Vector operator *=(Vector a, Vector b)
{}
-   (e) public static Vector operator *(double x, Vector a)
{}

## 调试练习

15.1. 下面的程序有什么问题？

```
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp1_chap15
{
class OvrLoadingBinary
{
    int x;
    int y;
    OvrLoadingBinary() {}
    OvrLoadingBinary(int i, int j)
    {
        x = i;
        y = j;
    }
    public void DisplayWindow()
    {
        Console.WriteLine("{0} {1}",+x,+y);
    }
    public static OvrLoadingBinary operator +(OvrLoadingBinary olb1, OvrLoadingBinary olb2)
    {
        OvrLoadingBinary pos = new OvrLoadingBinary();
        pos.x = x + olb2.x;
        pos.y = y + olb2.y;
        return pos;
    }
}
class Program
```

```
{
public static void Main()
{
    OvrLoadingBinary olb1 = new OvrLoadingBinary(46, 200);
    Console.Write("First Window Position at : ");
    olb1.DisplayWindow(); // displays 10 & 20
    Console.Write("Then the Window is moved to position : ");
    OvrLoadingBinary olb2 = new OvrLoadingBinary(125, 310);
    olb2.DisplayWindow(); // displays 125 & 310
    OvrLoadingBinary olb3 = new OvrLoadingBinary();
    olb3 = olb1 + olb2;
    Console.Write("Displaying Window at : ");
    olb3.DisplayWindow();
}
}
```

15.2. 找出以下用于一元运算符重载的程序中的错误。

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp2_chap15
{
    class UnaryOperatorOverload
    {
        private int val1;
        private int val2;
        public UnaryOperatorOverload()
        {
        }
        public UnaryOperatorOverload(int i, int j)
        {
            i = val1;
            j = val2;
        }
        public void ShowCommandWindowPosition()
        {
            Console.WriteLine("The values keep changing due to operator overloading");
            Console.WriteLine("The values are {0} {1}", val1, val2);
        }
        public static UnaryOperatorOverload operator -(UnaryOperatorOverload uoo)
        {
            UnaryOperatorOverload pos = new UnaryOperatorOverload();
            pos.val1 = -uoo.val1;
            pos.val2 = -uoo.val2;
            return pos;
        }
    }
}
```


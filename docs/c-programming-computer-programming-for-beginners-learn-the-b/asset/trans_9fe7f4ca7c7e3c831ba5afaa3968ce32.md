

}
set
{
    if (value == "Red")
        color = value;
    else
        Console.WriteLine("This car can only be red!");
}
正如你所见，这是一段更复杂的代码，包含更高级的属性。现在，你会发现 color 变量在返回时只会以大写字符形式出现。这是因为在返回之前对变量添加了 ToUpper() 方法。代码的下一部分将设置 color 变量。然而，唯一会被接受的值是“Red”。

## A Short Guide to Visibility

在阅读本指南的过程中，你会遇到 public 和 private 这两个术语。你可能在想它们代表什么。嗯，它们是表示所讨论项可见性的关键字。

protected internal 项的类即使继承类存在于另一个项目中也可以访问该项。

你现在应该能够自行创建简单的类，甚至创建它们的属性。当然，这只是基础水平。通过练习和进一步的知识，你可以创建功能强大且令人惊叹的程序，其中包含多个类和属性。

## Getting a Grip on Member Functions and Encapsulation

在类中，成员函数是一个其原型或定义在类定义内、方式与其它变量类似的函数。成员函数可以操作其类的任何对象。它还可以访问该对象类的每个成员。

另一方面，成员变量是对象的属性。因此，它们将被保持为私有以实现封装。它们只能通过使用公共成员函数来访问。

以下示例说明了类成员的使用。在这里，正在查找不同类成员的值。

```
using System;
```
```
namespace BoxApplication
```
```
{
```
```
class Box
{
    private double length; // Length of a box
    private double breadth; // Breadth of a box
    private double height; // Height of a box
    public void setLength( double len )
    {
        length = len;
    }
    public void setBreadth( double bre )
    {
        breadth = bre;
    }
    public void setHeight( double hei )
    {
        height = hei;
    }
    public double getVolume()
```
```
Box2.setBreadth(13.0);
Box2.setHeight(10.0);
// volume of box 1
volume = Box1.getVolume();
Console.WriteLine("Volume of Box1 :{0}",volume);
// volume of box 2
volume = Box2.getVolume();
Console.WriteLine("Volume of Box2 :{0}",volume);
Console.ReadKey();
}
}
}
```

执行上面给出的代码后，将会产生以下结果。

Volume of Box1 :210

Volume of Box2 :1560

## Static Members of a Class in C#

类成员可以用 static 关键字定义为静态。在将类的特定成员声明为静态时，

无论为该类创建了多少个对象，该静态成员都只有一个副本。

换句话说，static 关键字表示对于一个类，该成员只有一个实例存在。静态变量倾向于用于定义常量。这是因为可以通过调用类而无需创建实例来检索它们的值。静态变量的初始化可以在类定义或成员函数之外进行。同时，静态变量也可以在类定义内部初始化。

看下面的例子。

```
using System;

namespace StaticVarApplication
{
    class StaticVar
    {
        public static int num;
        public void count()
        {
            num++;
```
```
}

public int getNum()
{
    return num;
}

}

class StaticTester
{
    static void Main(string[] args)
    {
        StaticVar s1 = new StaticVar();
        StaticVar s2 = new StaticVar();

        s1.count();
        s1.count();
        s1.count();

        s2.count();
        s2.count();
        s2.count();
    }
}
```
```
```
```
Console.WriteLine("Variable num for s1: {0}",
s1.getNum());
Console.WriteLine("Variable num for s2: {0}",
s2.getNum());
Console.ReadKey();
}
}
}
```
```

执行上面所示的代码时，会产生以下结果。

Variable num for s1: 6

Variable num for s2: 6

成员函数也可以声明为静态。这些函数将只访问静态变量。此外，静态函数甚至可以在创建对象之前存在。

看下面的例子以更好地理解这些静态函数。

```
```csharp
using System;
namespace StaticVarApplication
{
```
```
class StaticVar
{
public static int num;
public void count()
{
num++;
}
public static int getNum()
{
return num;
}
}

class StaticTester
{
static void Main(String[] args)
{
StaticVar s = new StaticVar();
s.count();
}
}
```
```
s.count();

s.count();

Console.WriteLine("Variable    num:    {0}", StaticVar.getNum());

Console.ReadKey();
}
}
}
```

编译并执行上面的代码后，你会发现产生以下结果。

Variable num: 3

## Chapter 8

## A Brief on Methods

在阅读本书时，你会多次遇到方法。如果你想知道它们是什么，那么这里就是你了解它们的地方。方法是关于编程的基础知识之一，你应该知道。

## What is a Method?

方法可以说是一组可以一起执行任务的语句。所有 C# 程序至少会有一个类，其中包含一个名为 Main 的方法。你已经遇到过它们。

为了使用方法，必须先定义该方法。然后，调用该方法。让我们逐一看看这个过程。

## Defining a Method

当方法被定义时，方法结构的各个元素会被声明。在 C# 语言中定义方法的语法如下所示。

```
<Access Specifier> <Return Type> <Method Name>(Parameter List)
```
```
{
```
```
Method Body
```
```
}
```

方法可以有各种元素。它们如下所述。

Access Specifier: 正如你所知，访问说明符将决定方法或变量从另一个类中的可见性。

Return Type: 方法可能返回值。返回类型说明了方法将返回的值的数据类型。如果方法没有返回值，则返回类型为 void。

Method name: 这是方法的唯一标识符。名称区分大小写。此外，标识符不能与类中已声明的任何其他标识符相同。

Parameter list: 参数用于在方法之间传递和接收数据。它们用括号括起来。参数列表将指明方法的参数的顺序、数量和类型。重要的是，方法可能没有任何参数。

Method Body: 主体将包含完成活动所需的指令集。

看下面给出的示例。在这段代码片段中，你会注意到一个函数 FindMax。它接受两个整数值并比较它们。较大的值将被返回。该函数具有 public 访问说明符。因此，它可以通过使用其实例从类外部访问。

```
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if (num1 > num2)
            result = num1;
        else
```
```
result = num2;

return result;
}
...
}
```

## Calling a Method

在 C# 中，调用方法非常容易，只需使用其名称即可。看下面给出的示例。它展示了如何调用方法。

```
using System;

namespace CalculatorApplication
{

class NumberManipulator
{

public int FindMax(int num1, int num2)
{

/* local variable declaration */

int result;

if (num1 > num2)
```


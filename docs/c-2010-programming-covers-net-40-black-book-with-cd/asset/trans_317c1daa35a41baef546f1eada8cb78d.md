

当你调用重载方法时，编译器会根据方法调用中指定的签名自动确定应使用哪个方法。以下代码片段展示了方法重载的示例：

```
public class Shape
{
    public void Area(int Side)
    {
        //Calculate Square Area
    }
    public void Area(int Length, int Breadth)
    {
        //Calculate Rectangle Area
    }
    public void Area(double Radius)
    {
        //Calculate Circle Area
    }
    public double Area(double Base, double Height)
    {
        //Calculate Triangle Area
    }
}
class MainClass
{
    ...
    shape.Area(15);
    shape.Area(10, 20);
    shape.Area(10.5);
    shape.Area(15.5, 20.4);
}
```

在前面的代码片段中，你可以看到 Area() 方法是一个重载方法，因为它以不同的签名和返回类型被多次定义。

## 运算符重载

所有运算符都有指定的含义和功能，例如 +（加号）运算符将两个数值相加，而 -（减号）运算符从一个数值中减去另一个数值。然而，在 C# 中，你可以通过重载它们来改变运算符的功能。例如，你可以使用 + 运算符连接两个字符串。将特殊含义分配给运算符以适应用户定义的数据类型（如类或结构体）的机制称为运算符重载。并非所有运算符都可以被重载。表 5.1 显示了运算符及其重载状态的列表，显示了运算符是否可以被重载：

| Table 5.1: Operators and their Overloading Status |
|---|---|---|
| Operators | Type | Overloading Status |
| +, -, !, ~, ++, --, true, false | Unary | Can be overloaded |
| +, -, *, /, %, &, |, ^, <<, >> | Binary | Can be overloaded |
| ==, !=, <, >, <=, >= | Comparison | Can be overloaded |
| &&, || | Conditional logic | Cannot be overloaded but can be evaluated using & and | |
| [] | Array Indexing | Cannot be overloaded but can help in defining indexes |
| () | Cast | Cannot be overloaded but can help in defining new conversion operators |
| +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>= | Assignment | Cannot be overloaded |
| =, ., ?:, new, is, sizeof, typeof | Other | Cannot be overloaded |

### NOTE

> 如果你重载比较运算符，它们必须成对重载，例如如果重载了 == 则也必须重载 !=。反之亦然，同样规则适用于 < 和 >，以及 <= 和 >=。

## 索引器重载

在 C# 中，索引器用于将对象视为数组。它用于为对象提供索引以从对象中获取值。实现索引器需要你使用方括号 ([ ]) 与对象一起获取和设置对象的值。索引器被声明为属性，不同之处在于对于索引器，你不需要为其提供名称。你需要使用 this 关键字来定义索引器。

以下代码片段展示了如何定义索引器：

```
public string this[int Position]
{
    get
    {
        return MyData[Position];
    }
    set
    {
        MyData[Position] = value;
    }
}
```

在前面的代码片段中，get 属性用于检索 MyData 成员的索引，而 set 属性用于为成员分配索引。你也可以看到索引器没有被赋予名称。

与任何其他数据成员类似，索引器也可以被重载。以下代码片段展示了如何重载索引器：

```
public string this[int position]
{
    get
    {
        return myVar[position];
    }
    set
    {
        myVar [position] = value;
    }
}
public string this[string strdata]
{
    get
    {
        int count = 0;
        for (int i=0; i < arrSize; i++)
        {
            if (myvar [i] == strdata)
            {
                count++;
            }
        }
        return count.ToString();
    }
    set
    {
        for (int i=0; i < arrSize; i++)
        {
            if (myVar[i] == strdata)
            {
                myVar[i] = value;
            }
        }
    }
}
```

在前面的代码片段中，我们通过传递不同类型的参数重载了索引器。在索引器的第一个声明中，我们传递了 int 数据类型；而在另一个中，我们传递了 string 数据类型。

## 运行时多态/重写

重写是一个特性，允许派生类为基类中已定义的方法提供特定的实现。派生类中方法的实现会覆盖或替换其基类中方法的实现。该特性也称为运行时多态，因为编译器在程序执行期间（运行时）而不是在程序编译期间将方法绑定到对象。当你调用方法时，派生类中定义的方法会被调用和执行，而不是基类中的方法。要调用派生类中已在基类中定义的方法，你需要执行以下步骤：

- 将基类方法声明为 virtual
- 使用 override 关键字实现派生类方法

以下代码片段展示了如何在派生类中重写基类的方法：

```
class BaseClass
{
    public virtual void ShowData()
    {
        //Method Body
    }
}
class DerivedClass:BaseClass
{
    public override void ShowData()
    {
        //Method Body
    }
}
```

在前面的代码片段中，你可以看到在 BaseClass 类中，ShowData() 方法被标记为 virtual 关键字，而在 DerivedClass 类中，ShowData() 方法被标记为 override 关键字。

让我们现在学习关于抽象。

## 抽象

抽象是从用户隐藏特定概念或对象的细节并仅公开其基本特征的过程。抽象和封装的概念是互补的。你可以通过封装部分讨论的示例很好地理解抽象的概念。正如你在冰箱的例子中看到的，当顾客去购买冰箱时，店主会给出冰箱功能的简要描述，例如颜色和存储容量，但不会描述冰箱的内部工作系统。展示与冰箱相关的一般信息的过程是抽象，而将复杂信息从用户隐藏起来称为封装。

就 OOP 而言，抽象是指在不包含背景细节或解释的情况下表示基本特征。抽象是根据其功能而不是其实现细节来开发类、对象和类型。抽象简单地表示一个模型、一个视图或一个实际项目（类、对象或类型）的表示。抽象的主要特征如下：

- 管理代码的复杂性
- 将复杂系统分解为更小的组件

让我们现在讨论抽象类。

## 抽象类

在 C# 中，你可以有一个基类和多个派生类。如果你不希望任何类创建基类的对象，你可以将基类设为抽象。类中的 abstract 关键字表示该类不能被实例化。你可以创建其派生类的实例（前提是它未被标记为 abstract）。以下代码片段展示了如何创建抽象类：

```
abstract class BaseClass
{
    //Data Members and Member Functions
}
class DerivedClass: BaseClass
{
    // Data Members and Member Functions
}
class MainClass()
{
    ...
    ...
    BaseClass bc;        //Can't be instantiated
    DerivedClass dc;     //Can be instantiated
}
```

在前面的代码片段中，我们不能实例化 BaseClass 类，因为我们已将其声明为抽象。

抽象类的一些特征如下：

- 限制实例化，意味着你不能创建抽象类的对象
- 允许你在其中定义抽象和非抽象成员
- 要求其中至少有一个抽象方法
- 限制其中使用 sealed 关键字
- 具有 public 访问说明符；因此，它可以在程序的任何位置使用

让我们现在讨论抽象方法。

## 抽象方法

抽象方法类似于虚拟方法，它不提供任何实现；因此，抽象方法没有方法体。它可以使用 abstract 关键字声明。以下代码片段展示了如何创建抽象方法：

```
public abstract void Area(int Length, int Breadth);
```

抽象方法的一些特征如下：

- 限制在抽象类中实现
- 允许在非抽象派生类中实现
- 要求仅在抽象类中声明
- 限制与 static 和 virtual 关键字一起声明
- 允许你重写虚拟方法

以下代码片段展示了抽象方法的实现：

```
public abstract class Shape
{
    ...
    public abstract void Area( int Length, int Breadth)
    {
        //Method Area() can't be implemented at this place.
    }
}
public abstract class BasicShape: Shape
{
    //Method Area() can't be implemented at this place also
}
public class Rectangle: BasicShape
{
    public override void Area(int Length, int Breadth)

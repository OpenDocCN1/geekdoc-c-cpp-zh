
## 继承

继承是面向对象编程中的基本概念之一。继承促进代码重用，并允许你扩展已编写代码的功能。本章介绍以下内容：

-   继承的工作原理
-   在 C# 中实现继承
-   定义抽象方法和类
-   密封类和方法
-   定义重载方法
-   在继承中可使用的不同类型的访问修饰符
-   在接口中使用继承

## 在 C# 中理解继承

以下 Employee 类包含公司员工的信息：

```
public class Employee
{
    public string Name { get; set; }
    public DateTime DateOfBirth { get; set; }
    public ushort Age()
    {
        return (ushort)(DateTime.Now.Year - this.DateOfBirth.Year);
    }
}
```

## 第一部分：C# 基础

Manager 类包含有关管理者的信息：

```
public class Manager
{
    public string Name { get; set; }
    public DateTime DateOfBirth { get; set; }
    public ushort Age()
    {
        return (ushort)(DateTime.Now.Year - this.DateOfBirth.Year);
    }
    public Employee[] subordinates { get; set; }
}
```

Manager 类与 Employee 类之间的关键区别在于，Manager 具有一个额外的属性 subordinates，其中包含受某位经理监督的员工数组。实际上，经理实际上是一名员工，只是他承担了一些额外的角色。在此示例中，Manager 类可以继承自 Employee 类，然后添加其所需的额外 subordinates 属性，如下所示：

```
public class Manager: Employee
{
    public Employee[] subordinates { get; set; }
}
```

通过继承 Employee 类，Manager 类可以使用 Employee 类中定义的所有成员。Employee 类与 Manager 类之间的关系可以用类图表示，如图 6-1 所示。

![](img/a977a875c7c627b45d939729705a252e_207_0.png)

Employee 被称为基类，而 Manager 是派生类。在面向对象编程中，继承分为两种类型：实现和接口。本章将探讨这两种类型。

## 实现继承

实现继承是指一个类从另一个基类派生，继承基类的所有成员。若要向类添加新成员，可以定义另一个从现有基类派生的类。使用实现继承，新派生类继承基类提供的所有实现。

为了理解 C# 中继承的工作原理，按如下方式定义一个简单的类：

```
public class Shape
{
    //---properties---
    public double length { get; set; }
    public double width { get; set; }
    //---method---
    public double Perimeter()
    {
        return 2 * (this.length + this.width);
    }
}
```

这里，Shape 类包含两个属性和一个方法。单独来看，该类并未指定特定形状，但它假设基本形状包含长度和宽度。它还假设形状的周长只是其长度和宽度之和的两倍。

使用此基类，可以定义其他形状，例如正方形、矩形和圆形。让我们从矩形形状开始。使用 Shape 作为基类，可以通过继承 Shape 类来定义 Rectangle 类（派生类，因为它派生自 Shape 类），如下所示：

```
public class Rectangle : Shape
{
}
```

在 C# 中，使用冒号 (:) 运算符表示一个类继承自另一个类（称为基类）。此示例的含义是：“Rectangle 类继承自 Shape 类。”这意味着 Shape 类拥有的任何成员都将被 Rectangle 类继承。（在此示例中，Rectangle 类没有实现；将在接下来的几节中添加。）

C# 仅支持单类继承，这意味着一个类只能直接从一个基类继承。如果未指定基类，C# 编译器假定它继承自 System.Object 类。因为 Shape 类未指定它继承自谁，所以等效于：

```
public class Shape : Object
{
    //---properties---
    public double length { get; set; }
    public double width { get; set; }
    //---method---
    public double Perimeter()
    {
        return 2 * (this.length + this.width);
    }
}
```

要使用 Rectangle 类，可以像使用其他类一样实例化它：

```
Rectangle r = new Rectangle();
```

## 第一部分：C# 基础

因为 Rectangle 类继承了 Shape 类的所有成员，所以可以像在 Rectangle 类本身中定义一样访问其成员：

```
r.length = 4;
r.width = 5;
Console.WriteLine(r.Perimeter()); //---18---
```

## 抽象类

Shape 类未指定特定形状，因此直接实例化它（如下面所示）真的没有意义：

```
Shape someShape = new Shape();
```

相反，所有其他形状都应继承自此基类。为了确保无法直接实例化 Shape 类，可以使用 abstract 关键字将其设为抽象类：

```
public abstract class Shape
{
    //---properties---
    public double length { get; set; }
    public double width { get; set; }

    //---method---
    public double Perimeter()
    {
        return 2 * (this.length + this.width);
    }
}
```

一旦将类定义为抽象类，就不能再直接实例化它；以下内容现在不被允许：

```
//---cannot instantiate directly---
Shape someShape = new Shape();
```

abstract 关键字表示该类仅为继承目的而定义；其他类需要继承它才能拥有此基类型的对象。

## 抽象方法

除了使用 abstract 关键字使类抽象外，还可以创建抽象方法。抽象方法没有实现，其实现留给继承定义它的类的类。以 Shape 类为例，现在可以定义一个名为 Area() 的抽象方法来计算形状的面积：

```
public abstract class Shape
{
    //---properties---
    public double length { get; set; }
    public double width { get; set; }

    //---method---
    public double Perimeter()
    {
        return 2 * (this.length + this.width);
    }

    //---abstract method---
    public abstract double Area();
}
```

将 Area() 方法设为抽象是有道理的，因为此时你并不知道正在处理的形状是什么（例如圆形、正方形或三角形），因此不知道如何计算其面积。

抽象方法与普通方法一样定义，只是没有普通的方法块 ({})。继承包含抽象方法的类的类必须为这些方法提供实现。

先前定义的 Rectangle 类现在必须使用 override 关键字实现 Area() 抽象方法：

```
public class Rectangle : Shape
{
    //---provide the implementation for the abstract method---
    public override double Area()
    {
        return this.length * this.width;
    }
}
```

而不是使用 this 关键字访问 length 和 width 属性，也可以使用 base 关键字：

```
public class Rectangle : Shape
{
    public override double Area()
    {
        return base.length * base.width;
    }
}
```

base 关键字用于从派生类内部访问基类的成员（例如属性和变量）。你也可以使用 base 关键字访问基类的方法；下面是一个示例：

```
public class Rectangle : Shape
{
    public override sealed double Area()
    {
        return this.length * this.width;
    }
}
```

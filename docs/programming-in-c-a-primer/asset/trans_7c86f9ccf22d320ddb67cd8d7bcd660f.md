

一个 C# 类可以具有两种可见性修饰符之一：**public** 或 **internal**。如果我们没有显式标记类的可见性修饰符，则隐式设置为‘internal’；也就是说，默认情况下所有类都是 **internal**。Internal 类在同一个程序程序集中可访问，且无法从程序集外部访问。

标记为 **public** 的类在程序集内部和外部都可以访问。 .NET 类框架中包含的所有类都标记为 **public**，以便所有开发人员都可以访问它们并用于配置应用程序和服务。

尽管类通常标记为 **public** 或 **internal**，但当它作为另一个类的成员声明时，类也可以标记为 **private**。在这种情况下，该类像封闭类的成员一样表现，因此适用于类成员的修饰符也适用于它。

## 13.5.2 类成员可见性

如上一章所述，类成员可以具有五种可见性修饰符中的任意一种：

- public
- private
- protected internal
- protected
- internal

除 **protected internal** 组合外，同时指定多个访问修饰符是错误的。当未指定修饰符时，默认为 **private** 可访问性。表 13.1 显示了可见性修饰符如何控制程序中成员的可见性。

### 表 13.1 类成员的可见性

| 关键字 | 包含类 | 派生类 | 包含程序 | 包含程序外部的任何位置 |
|---|---|---|---|---|
| private | ✓ |  |  |  |
| protected | ✓ | ✓ |  |  |
| internal | ✓ |  | ✓ |  |
| protected internal | ✓ | ✓ | ✓ |  |
| public | ✓ | ✓ | ✓ | ✓ |

必须记住，成员的可访问性域绝不会大于包含它的类的可访问性域。表 13.2 给出了在不同类访问说明符组合下成员的可见性域。

### 表 13.2 类成员的可访问性域

| 成员修饰符 | Public | Internal | Private |
|---|---|---|---|
| public | 到处 | 仅程序 | 仅类 |
| internal | 仅程序 | 仅程序 | 仅类 |
| private | 仅类 | 仅类 | 仅类 |

## 13.5.3 基类成员的可访问性

当一个类从基类继承时，基类的所有成员，除构造函数和析构函数外，都会被继承并成为派生类的成员。基类成员声明的可访问性对其可继承性没有控制作用。然而，一个继承的成员可能在派生类中不可访问，要么是因为其声明的可访问性，要么是因为它被类本身中的声明隐藏了。

```csharp
class A
{
    private int x;
    protected int y;
    public int z;
}
```

```csharp
class B : A
{
    public void SetXYZ()
    {
        x = 10; // Error; x is not accessible
        y = 20; // ok
        z = 30; // ok
    }
}
```

请注意，尽管 B 从 A 继承了私有成员 x，但它在 B 中不可访问。然而，A 的 protected 和 public 成员在子类 B 中是可访问的。但就类的使用者而言，protected 是 private。因此，以下是非法操作：

```csharp
A a = new A(); // object of A
a.y = 5; // error! an object cannot access protected data
a.z = 10; // ok
```

## 13.5.4 可访问性约束

C# 在继承过程中对成员和类的可访问性施加了某些约束。

- 派生类的直接基类必须至少与派生类本身一样可访问。
- 成员的可访问性域绝不会大于包含它的类的可访问性域。
- 方法的返回类型必须至少与方法本身一样可访问。

```csharp
class A
{
    ....
}
public class B : A
{
    ....
}
```

是非法的，因为 A 默认是 'internal' 而 B 是 public。A 应该至少与 B 一样可访问。

再考虑另一个例子：

```csharp
class A
{
    private class B
    {
        public int x;
    }
}
```

这里，公共数据 x 在类 B 外部不可访问。这是由于类 B 的可访问性所施加的约束。因为 B 是 private，x 上的 public 被降为 private。

在许多情况下，我们使用方法来处理类对象，因此它们将类作为返回类型。在这种情况下，方法的返回类型必须至少与方法本身一样可访问。例如，考虑以下代码：

```csharp
class A
{
    ...
}
public class B
{
    A Method1() {}        // OK
    internal A Method2() {}  // OK
    public A Method3() {}   // Error!
}
```

类 B 中声明的这三个方法都指定 A 作为其返回类型。由于类 A 默认假设可访问性级别为 internal，方法

```csharp
public A Method3() // public is higher than internal
{
    ...
}
```

是错误的。该方法不能具有高于其返回类型的可访问性级别。

## 13.6 定义子类构造函数

我们已经看到，当调用构造函数时对象会被创建。相同的原理也可应用于构造派生类对象。我们可以为派生类定义适当的构造函数，当创建派生类对象时可以调用它。记住，构造函数的目的是为类的字段提供值。如果基类构造函数需要参数来构造基类对象，我们如何将值传递给基类构造函数？程序 13.2 通过实现单级继承回答了这些问题。

### 程序 13.2 单继承的应用

```csharp
using System;
class Room        // base class
{
    public int length;
    public int breadth;
    public Room(int x, int y)   // base constructor
    {
        length = x;
        breadth = y;
    }
    public int Area()
    {
        return (length * breadth);
    }
}
class BedRoom : Room  // Inheriting Room
{
    int height;
    // subclass constructor
    public BedRoom(int x, int y, int z) : base(x, y)
    {
        height = z;
    }
    public int Volume()
    {
        return (length * breadth * height);
    }
}
class InherTest
{
    public static void Main()
    {
        BedRoom room1 = new BedRoom(14, 12, 10);
        int area1 = room1.Area();    // superclass method
        int volume1 = room1.Volume(); // subclass method
        Console.WriteLine("Area1 = " + area1);
        Console.WriteLine("Volume1 = " + volume1);
    }
}
```

程序 13.2 的输出为：

```text
Area1 = 168
Volume1 = 1680
```

该程序定义了一个类 Room 并将其扩展为另一个类 BedRoom。请注意，类 BedRoom 定义了自己的数据成员和方法。子类 BedRoom 现在包含三个实例变量，即 length、breadth 和 height 以及两个方法 Area 和 Volume。

派生类中的构造函数使用 base 关键字将基类构造函数所需的值传递给它。语句

```csharp
BedRoom room1 = new BedRoom(14, 12, 10);
```

首先调用 BedRoom 构造函数方法，该方法又使用 base 关键字调用 Room 构造函数方法。

最后，子类 BedRoom 的对象 room1 调用在超类中定义的方法 Area 以及在子类本身中定义的方法 Volume。

### 13.6.1 子类构造函数

子类构造函数用于构造子类和超类的实例变量。子类构造函数使用关键字 base 调用超类的构造函数方法。

```csharp
public BedRoom(int x, int y, int z) : base(x, y)
{
    height = z;
}
```

这里，派生构造函数接受三个参数，前两个提供给基类构造函数，第三个提供给它自己的类成员的值。请注意 base(x, y) 像方法调用一样行为，因此参数指定时不带类型。这些参数的类型和顺序必须与基类构造函数参数的类型和顺序匹配。

当编译器遇到 base(x, y) 时，它将值 x 和 y 传递给接受两个 int 参数的基类构造函数。基类构造函数在派生类构造函数执行之前被调用。也就是说，数据成员 length 和 breadth 在成员 height 被赋值的之前被赋予值。

请注意，关键字 base 的使用不仅限于构造函数逻辑本身。我们可以在任何子类中使用 base 来访问父类中定义的 public 或 protected 成员。例如，语句：

```csharp
base.length = 100;
int area = base.Area();
```

在派生类 BedRoom 内部是有效的。

## 13.7 多级继承

面向对象编程中的一个常见需求是使用派生类作为超类。C# 支持这一概念，并在构建其类库时广泛使用它。这一概念允许我们构建如 Fig. 13.5 所示的类链。

类 A 作为派生类 B 的基类，而 B 又作为派生类 C 的基类。链 ABC 被称为继承路径。

具有多级基类的派生类声明如下：

```csharp
class A
{
    ....
    ....
}
class B : A // First level derivation
{
    ....
    ....
}
class C : B // Second level derivation
{
    ....
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_253_0.png)

图 13.5 多级继承


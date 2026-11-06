
```csharp
}
}
```

代码输出如下：

```text
The Length of the figure is: 5.4
The Width of the figure is: 3.2
The Area of the figure is: 17.28
```

类成员变量 *width* 和 *length* 已被声明为 *public*，这意味着在创建类的实例后，我们能够从 *Main()* 函数访问它们。我们创建了 *Figure* 类的一个实例，并将其命名为 *f*。

*CalculateArea()* 和 *Show()* 成员函数也能够在不必使用类实例的情况下访问这些成员变量。*Show()* 成员函数也被声明为 public，这意味着我们能够使用类的实例从 *Main()* 函数访问它。

## 受保护访问修饰符

这种访问修饰符使子类能够访问基类中已定义的成员函数和成员变量。这样，实现继承就更容易。这将在继承部分讨论。

## 内部访问修饰符

这种访问修饰符允许类将其成员函数和成员变量公开给当前程序集中的其他对象和函数。这意味着，使用内部访问修饰符创建的任何成员，都可以从定义该成员的应用程序内已定义的任何类或方法中访问。以下示例演示了这一点：

```csharp
using System;

namespace AccesserApplication {

  class Figure {

    // The member variables
    internal double width;
    internal double length;
    double CalculateArea() {
return length * width;
}
public void Show() {
    Console.WriteLine("The Length of the figure is: {0}", length);
    Console.WriteLine("The Width of the figure is: {0}", width);
    Console.WriteLine("The Area of the figure is: {0}", CalculateArea());
}
}//end the class Figure

class RunFigure {
    static void Main(string[] args) {
        Figure f = new Figure();
        f.length = 6.5;
        f.width = 4.8;
        f.Show();
        Console.ReadLine();
    }
}
}
```

代码应返回以下结果：

```text
The Length of the figure is: 6.5
The Width of the figure is: 4.8
The Area of the figure is: 31.2
```

## 第 14 章：继承

借助继承，程序员可以根据另一个类来定义一个类。这也使我们能够重用代码并缩短实现应用程序所需的时间。

在创建类时，程序员不必创建全新的成员函数和数据成员，而是可以指定新类继承已有类的成员。*基类*是现有类的名称，而新类称为*派生类*。

继承只是 IS-A 关系<sup>[36]</sup>的一种实现。例如，奶牛是哺乳动物。

一个类可以从多个类或接口继承，这意味着它可以从多个基接口或基类继承数据和函数。以下示例演示基类和派生类的概念：

```csharp
using System;

namespace InheritanceApp {
    class Figure {
        public void setWidth(int wid) {
            width = wid;
        }
        public void setHeight(int heig) {
            height = heig;
        }
        protected int width;
        protected int height;
    }
    // A Derived class
    class Rectangle: Figure {
        public int calculateArea() {
return (width * height);
}
}
class TestInheritance {
    static void Main(string[] args) {
        Rectangle R = new Rectangle();
        R.setWidth(6);
        R.setHeight(8);
        // Print the rectangle's area.
        Console.WriteLine("The area is: {0}", R.calculateArea());
        Console.ReadKey();
    }
}
}
```

代码应返回以下输出：

```text
The area is: 48
```

我们定义了 *Figure* 类，它有两个属性，即 *width* 和 *height*。此类还有两个方法：*setWidth()* 和 *setHeight()*。然后我们定义了一个名为 *Rectangle* 的类。注意我们用于创建此类的语法：

```csharp
class Rectangle: Figure {
```

使用完整冒号表明 Rectangle 类正在继承 Figure 类。Rectangle 类只有一个方法，即 *calculateArea()* 方法。但是，由于它继承了 Figure 类，这意味着它具有 Figure 类的所有属性，例如 width 和 height。

然后我们创建了 *TestInheritance* 类。在 Main() 方法中，创建了 Rectangle 类的一个实例，并将其命名为 R。我们使用此实例访问了在 Rectangle 类和 Figure 类中定义的属性。这就是继承的强大之处！

### 基类初始化

派生类继承在以下代码中定义的成员方法和成员变量：

```csharp
cost = CalculateArea() * 120;
return cost;
}

public void Show() {
    base.Show();
    Console.WriteLine("The total cost for the carpet is: {0}",
CalculateCost());
}
}
}
class RunObject {
    static void Main(string[] args) {
        Carpet c = new Carpet(7.5, 9.5);
        c.Show();
        Console.ReadLine();
    }
}
}
}
```

代码将返回以下输出：

```text
The Width of the figure is: 9.5
The Length of the figure is: 7.5
The Area of the figure is: 71.25
The total cost for the carpet is: 8550
```

### 多重继承

C# 不支持多重继承。但是，借助接口，我们可以实现多重继承。考虑以下示例：

```csharp
using System;
namespace InheritanceApp {
    class Object {
        public void setWidth(int wid) {
            width = wid;
}
public void setHeight(int heig) {
    height = heig;
}
protected int width;
protected int height;
}

// PaintCost for the Base class
public interface PaintCost {
    int calculateCost(int area);
}
// The derived class
class Board : Object, PaintCost {
    public int calculateArea() {
        return (width * height);
    }
    public int calculateCost(int area) {
        return area * 120;
    }
}
class InheritanceTester {
    static void Main(string[] args) {
        Board B = new Board();
        int area;
        B.setWidth(5);
        B.setHeight(7);

    area = B.calculateArea();
    // Show the area of the object
    Console.WriteLine("The area of the object is: {0}", B.calculateArea());
            Console.WriteLine("The total printing cost is: ${0}" ,
    B.calculateCost(area));
    Console.ReadKey();
    }
    }
}
```

代码给出以下输出：

```text
The area of the object is: 35
The total printing cost is: $4200
```

## 第 15 章：多态

多态[37]一词意为呈现多种形式。在编程中，它表示为**“一个接口，多个函数”**。多态可以采取两种形式：静态或动态。

对于静态多态的情况，对函数的响应在编译时确定。在动态多态中，对函数的响应在运行时确定。

### 静态多态

如上所述，在此类多态中，对函数的响应在编译时确定。在编译时将函数链接到对象的过程称为*早期绑定*。它也称为*静态绑定*。在 C# 中，静态多态可以通过两种方式实现：

- 函数重载
- 运算符重载

### 函数重载

我们可以在同一作用域内为同一函数名提供多个定义。这些函数之间的差异通过函数所接受的参数类型或参数数量来体现。不能仅通过改变返回类型来重载函数声明。

**以下示例演示如何在 C# 中重载函数：**

```csharp
using System;

namespace PolymorphismApp {
    class DisplayData {
        void display(int x) {
            Console.WriteLine("Printing an int value: {0}", x );
        }

        void display(double y) {
```

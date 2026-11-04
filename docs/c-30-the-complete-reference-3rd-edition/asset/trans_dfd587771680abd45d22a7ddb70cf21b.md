
```csharp
// Construct a copy of a TwoDShape object.
public TwoDShape(TwoDShape ob) {
    Width = ob.Width;
    Height = ob.Height;
}

// Properties for Width and Height.
public double Width {
    get { return pri_width; }
    set { pri_width = value < 0 ? -value : value; }
}

public double Height {
    get { return pri_height; }
    set { pri_height = value < 0 ? -value : value; }
}

public void ShowDim() {
    Console.WriteLine("Width and height are " +
        Width + " and " + Height);
}

// A derived class of TwoDShape for triangles.
class Triangle : TwoDShape {
    string Style;

    // A default constructor.
    public Triangle() {
        Style = "null";
    }

    // Constructor for Triangle.
    public Triangle(string s, double w, double h) : base(w, h) {
        Style = s;
    }

    // Construct an isosceles triangle.
    public Triangle(double x) : base(x) {
        Style = "isosceles";
    }

    // Construct a copy of a Triangle object.
    public Triangle(Triangle ob) : base(ob) {
        Style = ob.Style;
    }

    // Return area of triangle.
    public double Area() {
        return Width * Height / 2;
    }

    // Display a triangle's style.
    public void ShowStyle() {
        Console.WriteLine("Triangle is " + Style);
    }
}

class Shapes7 {
    static void Main() {
        Triangle t1 = new Triangle("right", 8.0, 12.0);
        // Make a copy of t1.
        Triangle t2 = new Triangle(t1);

        Console.WriteLine("Info for t1: ");
        t1.ShowStyle();
        t1.ShowDim();
        Console.WriteLine("Area is " + t1.Area());

        Console.WriteLine();

        Console.WriteLine("Info for t2: ");
        t2.ShowStyle();
        t2.ShowDim();
        Console.WriteLine("Area is " + t2.Area());
    }
}
```

在这个程序中，t2 由 t1 构造而来，因此二者完全相同。输出如下：

```text
Info for t1:
Triangle is right
Width and height are 8 and 12
Area is 48

Info for t2:
Triangle is right
Width and height are 8 and 12
Area is 48
```

请特别注意这个 Triangle 构造函数：

```csharp
public Triangle(Triangle ob) : base(ob) {
    Style = ob.Style;
}
```

它接收一个 Triangle 类型的对象，并将该对象（通过 base）传递给这个 TwoDShape 构造函数：

```csharp
public TwoDShape(TwoDShape ob) {
    Width = ob.Width;
    Height = ob.Height;
}
```

```csharp
class Derived2 : Base {
    // Override Who() again in another derived class.
    public override void Who() {
        Console.WriteLine("Who() in Derived2");
    }
}

class OverrideDemo {
    static void Main() {
        Base baseOb = new Base();
        Derived1 dOb1 = new Derived1();
        Derived2 dOb2 = new Derived2();

        Base baseRef;  // a base class reference

        baseRef = baseOb;
        baseRef.Who();

        baseRef = dOb1;
        baseRef.Who();

        baseRef = dOb2;
        baseRef.Who();
    }
}
```

该程序的输出如下：

```text
Who() in Base
Who() in Derived1
Who() in Derived2
```

这个程序创建了一个名为 **Base** 的基类和两个名为 **Derived1** 和 **Derived2** 的派生类。**Base** 声明了一个名为 **Who()** 的方法，派生类重写了它。在 **Main()** 方法中，声明了 **Base**、**Derived1** 和 **Derived2** 类型的对象。此外，还声明了一个 **Base** 类型的引用，名为 **baseRef**。然后，程序将每种类型对象的引用赋给 **baseRef**，并使用该引用调用 **Who()**。正如输出所示，执行的是哪个版本的 **Who()** 取决于调用时所引用对象的类型，而不是 **baseRef** 的类类型。

不必重写虚方法。如果派生类不提供自己的虚方法版本，则使用基类中的版本。例如：

```csharp
/* When a virtual method is not overridden,
   the base class method is used. */

using System;

class Base {
    // Create virtual method in the base class.
    public virtual void Who() {
        Console.WriteLine("Who() in Base");
    }
}

class Derived1 : Base {
    // Override Who() in a derived class.
    public override void Who() {
        Console.WriteLine("Who() in Derived1");
    }
}

class Derived2 : Base {
    // This class does not override Who().
}

class NoOverrideDemo {
    static void Main() {
        Base baseOb = new Base();
        Derived1 dOb1 = new Derived1();
        Derived2 dOb2 = new Derived2();

        Base baseRef; // a base class reference

        baseRef = baseOb;
        baseRef.Who();

        baseRef = dOb1;
        baseRef.Who();

        baseRef = dOb2;
        baseRef.Who(); // calls Base's Who()
    }
}
```

该程序的输出如下：

```text
Who() in Base
Who() in Derived1
Who() in Base
```

这里，Derived2 没有重写 Who()。因此，当对 Derived2 对象调用 Who() 时，执行的是 Base 中的 Who()。

在多级层次结构中，如果派生类没有重写某个虚方法，那么在沿层次结构向上移动时，遇到的该方法的第一个重写版本就是被执行的那个版本。例如：

```csharp
/* In a multilevel hierarchy, the first override of a virtual method that is found while moving up the hierarchy is the one executed. */

using System;

class Base {
    // Create virtual method in the base class.
    public virtual void Who() {
        Console.WriteLine("Who() in Base");
    }
}

class Derived1 : Base {
    // Override Who() in a derived class.
    public override void Who() {
        Console.WriteLine("Who() in Derived1");
    }
}

class Derived2 : Derived1 {
    // This class also does not override Who().
}

class Derived3 : Derived2 {
    // This class does not override Who().
}

class NoOverrideDemo2 {
    static void Main() {
        Derived3 dOb = new Derived3();
        Base baseRef; // a base class reference

        baseRef = dOb;
        baseRef.Who(); // calls Derived1's Who()
    }
}
```

输出如下：

```text
Who() in Derived1
```

这里，**Derived3** 继承 **Derived2**，**Derived2** 继承 **Derived1**，**Derived1** 继承 **Base**。正如输出所验证的，由于 `Who()` 既没有被 `Derived3` 重写，也没有被 `Derived2` 重写，因此执行的是 `Derived1` 中对 `Who()` 的重写，因为它是找到的第一个 `Who()` 版本。

另一点：属性也可以用 virtual 关键字修饰，并使用 override 重写。索引器也是如此。

## 为什么要重写方法？

重写方法使 C# 能够支持运行时多态。多态对面向对象编程至关重要，原因之一是：它允许一个通用类指定将为其所有派生类共有的方法，同时允许派生类定义其中部分或全部方法的具体实现。重写方法是 C# 实现多态中“一个接口，多种方法”方面的另一种方式。

成功应用多态的关键之一，是理解基类和派生类构成了一个从较不专门化到较专门化的层次结构。如果使用正确，基类会提供派生类可以直接使用的所有元素。通过虚方法，基类还定义了派生类可以自行实现的方法。这既赋予派生类灵活性，又仍然强制实施一致的接口。因此，通过将继承与重写方法结合，基类可以定义其所有派生类将使用的方法的一般形式。

```csharp
// Construct a square.
public Rectangle(double x) :
    base(x, "rectangle") { }

// Construct a copy of a Rectangle object.
public Rectangle(Rectangle ob) : base(ob) { }

// Return true if the rectangle is square.
public bool IsSquare() {
    if(Width == Height) return true;
    return false;
}

// Override Area() for Rectangle.
public override double Area() {
    return Width * Height;
}

class DynShapes {
    static void Main() {
        TwoDShape[] shapes = new TwoDShape[5];

        shapes[0] = new Triangle("right", 8.0, 12.0);
        shapes[1] = new Rectangle(10);
        shapes[2] = new Rectangle(10, 4);
        shapes[3] = new Triangle(7.0);
        shapes[4] = new TwoDShape(10, 20, "generic");

        for(int i=0; i < shapes.Length; i++) {
            Console.WriteLine("object is " + shapes[i].name);
            Console.WriteLine("Area is " + shapes[i].Area());
            Console.WriteLine();
        }
    }
}
```

该程序的输出如下：

```text
object is triangle
Area is 48

object is rectangle
Area is 100

object is rectangle
Area is 40

object is triangle
Area is 24.5

object is generic
Area() must be overridden
Area is 0
```

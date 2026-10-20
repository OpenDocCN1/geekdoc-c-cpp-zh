
GetArea() 和 Display() 也可以直接访问这些变量，而无需使用类的任何实例。成员函数 Display() 也被声明为 public。这样，它也可以从 Main() 中通过 Rectangle 类的实例 r 进行访问。

## 私有访问修饰符

使用此修饰符，类可以对其对象和函数隐藏成员函数和成员变量。只有属于同一类的函数才能访问私有成员。甚至类的实例也无法访问私有成员。

下面的示例说明了私有访问修饰符的概念。

```
using System;

namespace RectangleApplication
{

class Rectangle
{

//member variables

private double length;

private double width;
```

```
Length: 4.4
Width: 3.3
Area: 14.52
```

在上面的示例中，您会注意到成员变量 width 和 length 已被声明为 private。因此，无法从 Main() 函数访问它们。只有成员函数 Display() 和 AcceptDetails() 可以访问这些变量。由于这些成员函数已声明为 public，因此可以从 Main() 中使用 Rectangle 类的实例 r 访问它们。

## 受保护访问修饰符

此修饰符将使子类能够访问基类的成员函数和成员变量。因此，该修饰符在实现继承时非常有用。

## 内部访问修饰符

此修饰符将允许类在当前程序集中向其他对象和函数公开其成员函数和成员变量。也就是说，带有内部访问修饰符的成员可以从该成员所在应用程序中定义的任何方法或类访问。

查看以下示例以更好地理解此修饰符。

```
using System;

namespace RectangleApplication
{
    class Rectangle
    {
        //member variables
        internal double length;
        internal double width;
        double GetArea()
        {
            return length * width;
        }
        public void Display()
        {
            Console.WriteLine("Length: {0}", length);
            Console.WriteLine("Width: {0}", width);
            Console.WriteLine("Area: {0}", GetArea());
        }
    }//end class Rectangle

    class ExecuteRectangle
    {
        static void Main(string[] args)
        {
            Rectangle r = new Rectangle();
            r.length = 4.5;
            r.width = 3.5;
            r.Display();
            Console.ReadLine();
        }
    }
}
```

执行上述代码后，会得到以下结果。

```
Length: 4.5
Width: 3.5
Area: 15.75
```

您会注意到在示例中，GetArea() 未使用任何访问修饰符声明。如果未指定访问修饰符，类成员将获得默认的私有访问修饰符。

## 受保护内部访问修饰符

此访问修饰符允许类将其成员函数和成员变量对其他类函数和对象隐藏。只有同一应用程序中的子类（如果有）才能访问这些成员。此访问修饰符通常用于实现继承。

## 第7章：认识 C# 中的类及其属性

您还记得，C# 是一种面向对象的编程语言。如果您对计算机编程有所了解，那么您一定听说过类。类在面向对象编程中至关重要。

可以说，类是一种构造，通过将不同类型的变量、事件和方法组合在一起，您可以构建自定义类型。换句话说，类是一个包含相互关联的变量和方法的集合。类将描述这些内容。在大多数情况下，您将创建类的实例，该实例被称为对象。您可以在此对象上使用已定义的变量和方法。当然，您可以根据代码的需求创建类的多个实例。

### 理解类

在之前的示例中，您已经接触过类的使用。毕竟，您在 C# 中构建的任何内容都必须以类为基础。通过以下示例可以获得更好的理解。

```
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Car car;
            car = new Car("Red");
            Console.WriteLine(car.Describe());
            car = new Car("Green");
            Console.WriteLine(car.Describe());
            Console.ReadLine();
        }
    }
}

class Car
{
    private string color;
    public Car(string color)
    {
        this.color = color;
    }
    public string Describe()
    {
        return "This car is " + Color;
    }
    public string Color
    {
        get { return color; }
        set { color = value; }
    }
}
```

正如您所见，首先定义了一个新类，并将其命名为 Car。为了简便起见，该类与主应用程序一起在同一个文件中声明。通常，新类倾向于定义在它们自己的文件中，但是，

还定义了一个变量，名为 color。此外，它被声明为私有变量。这是您应该记住的一点。通常应使用属性从外部访问变量。在 Car 类的末尾，定义了 Color 属性。这允许访问 color 变量。

Car 类还定义了一个构造函数，该构造函数接收一个参数。这允许我们使用颜色来初始化 Car 对象。由于此应用程序中只有一个构造函数，因此只能使用颜色来实例化 Car 对象。

还使用了 Describe() 方法。其目的是让用户在获取已记录信息的同时获得一些额外文本。它只会返回一个字符串以及已提供的数据。

在主应用程序中，声明了一个类型为 Car 的变量。随后创建了一个新实例，参数为“Red”。根据类的编码方式，红色将被分配为汽车的颜色。

为了验证这一点，再次使用了 Describe() 方法。

再次执行相同的步骤，以向您展示创建同一个类的多个实例实际上非常容易。当然，这一次使用了另一种颜色。

### 理解类的属性

属性的作用是让您能够控制类变量的可访问性。在任何面向对象的编程语言中，属性始终是从外部访问变量的推荐方式。在之前的示例中，您已经接触过属性的使用。

可以说，属性是方法和变量的组合。因此，它不能接受任何参数。另一方面，值可以在返回之前进行处理。属性将由两个部分组成。会有 get 方法和 set 方法。两者将一起包含在属性中。您可以在以下代码中看到这样的示例。

```
private string color;
public string Color
{
    get { return color; }
    set { color = value; }
}
```

get 方法必须用于返回变量。另一方面，set 方法必须用于为该变量赋值。当然，上面的示例是一个涉及属性的非常简单的代码示例。因此，完全有可能进一步扩展它。

关于属性，还有一点您应该了解。一个属性至少需要一个方法才能工作。换句话说，您可以使用 get 方法或 set 方法。在这种情况下，另一个方法变为可选。这种技术允许您根据需求定义只读属性或只写属性。

这里是另一个示例，进一步说明了属性的潜力。

```
public string Color
{
    get
    {
        return color.ToUpper();
    }
}
```


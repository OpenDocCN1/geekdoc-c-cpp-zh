

```csharp
int MyMethod(int x)
float MyMethod(float x)
double MyMethod(double x, double y)
```

考虑下面的示例，其中有两个方法用于添加不同类型的数字：

### 示例

```csharp
static int PlusMethodInt(int x, int y)
{
    return x + y;
}
```

```csharp
static double PlusMethodDouble(double x, double y)
{
    return x + y;
}
```

```csharp
static void Main(string[] args)
{
    int myNum1 = PlusMethodInt(8, 5);
    double myNum2 = PlusMethodDouble(4.3, 6.26);
    Console.WriteLine("Int: " + myNum1);
    Console.WriteLine("Double: " + myNum2);
}
```

## 2.22 C# - 什么是 OOP？

OOP 代表面向对象编程。过程式编程是编写对数据执行操作的过程或方法，而面向对象编程则是创建包含数据和方法的对象。

- OOP 执行更快且更容易。
- OOP 为程序提供了清晰的结构。
- OOP 有助于保持 C# 代码 DRY（“不要重复自己”），并使代码更易于维护、修改和调试。
- OOP 使得用更少的代码和更短的开发时间创建可复用的完整应用程序成为可能。

## C# - 什么是类与对象？

类与对象是面向对象编程的两个主要方面。

查看下图以了解类与对象的区别：

## 类与对象

你在上一章中了解到，C# 是一种面向对象的编程语言。C# 中的一切都与类、对象及其属性和方法相关联。例如：在现实生活中，汽车是一个对象。汽车具有重量和颜色等属性，以及驾驶和刹车等方法。

类就像对象构造函数，或创建对象的“蓝图”。

## 创建类

要创建类，请使用 class 关键字：

创建一个名为“Car”的类，其中包含一个变量 color：

```csharp
class Car
{
    string color = "red";
}
```

## 创建对象

对象由类创建。我们已经创建了名为 Car 的类，现在可以用它来创建对象。要创建 Car 的对象，请指定类名，后跟对象名，并使用 new 关键字：

### 示例

创建一个名为“myObj”的对象，并使用它打印 color 的值：

```csharp
class Car
{
    string color = "red";

    static void Main(string[] args)
    {
        Car myObj = new Car();
        Console.WriteLine(myObj.color);
    }
}
```

## 多个对象

你可以创建同一个类的多个对象：

### 示例

创建两个 Car 对象：

```csharp
class Car
{
    public string color = "red";
}
```

## 类成员

类中的字段和方法通常被称为“类成员”：

### 示例

创建一个包含三个类成员的 Car 类：两个字段和一个方法。

```csharp
// The class

class Car
{
    // Class members
    string color = "red";    // field
    int maxSpeed = 200;      // field
    public void fullThrottle() // method
    {
        Console.WriteLine("The car is going as fast as it can!");
    }
}
```

```csharp
class Car
{
    string color;
    int maxSpeed;

    static void Main(string[] args)
    {
        Car myObj = new Car();
        myObj.color = "red";
        myObj.maxSpeed = 200;
        Console.WriteLine(myObj.color);
        Console.WriteLine(myObj.maxSpeed);
    }
}
```

## 对象方法

你在 C# 方法章节中了解到，方法用于执行某些操作。方法通常属于类，并定义类的对象如何表现。就像字段一样，你可以使用点语法访问方法。但是请注意，方法必须是 public。请记住，我们使用方法名称，后跟两个括号 `()` 和一个分号 `;` 来调用（执行）方法：

### 示例

```csharp
class Car
{
    string color;      // field
    int maxSpeed;      // field
    public void fullThrottle()  // method
    {
        Console.WriteLine("The car is going as fast as it can!");
    }

    static void Main(string[] args)
    {
        Car myObj = new Car();
        myObj.fullThrottle(); // Call the method
    }
}
```

## 构造函数

构造函数是一种用于初始化对象的特殊方法。构造函数的优点是，在创建类的对象时自动调用。它可以用于为字段设置初始值：

### 示例

创建一个构造函数：

```csharp
// Create a Car class
class Car
{
    public string model; // Create a field

    // Create a class constructor for the Car class
    public Car()
    {
        model = "Mustang"; // Set the initial value for model
    }

    static void Main(string[] args)
    {
        Car Ford = new Car(); // Create an object of the Car Class (this will call the constructor)
        Console.WriteLine(Ford.model);  // Print the value of model
    }
}
```

// 输出 "Mustang"

## 构造函数参数

构造函数也可以接受参数，用于初始化字段。

下面的示例向构造函数添加了一个 `string modelName` 参数。在构造函数中，我们将 `model` 设置为 `modelName`（`model = modelName`）。当我们调用构造函数时，我们会向构造函数传递一个参数（`"Mustang"`），这将把 `model` 的值设置为 `"Mustang"`：

### 示例

```csharp
class Car
{
    public string model;

    // Create a class constructor with a parameter
    public Car(string modelName)
    {
        model = modelName;
    }

    static void Main(string[] args)
    {
        Car Ford = new Car("Mustang");
        Console.WriteLine(Ford.model);
    }
}
```

// 输出 "Mustang"

## 2.22 访问修饰符

到目前为止，你已经非常熟悉我们许多示例中出现的 `public` 关键字：

### `public string color`

`public` 关键字是一种访问修饰符，用于设置类、字段、方法和属性的访问级别/可见性。

### 私有修饰符

如果你使用私有访问修饰符声明字段，则该字段只能在同一个类内访问：

示例：

```csharp
class Car
{
    private string model = "Mustang";

    static void Main(string[] args)
    {
        Car myObj = new Car();
        Console.WriteLine(myObj.model);
    }
}
```

输出将是：

Mustang

### 公共修饰符

如果你使用公共访问修饰符声明字段，则所有类都可以访问它：

示例：

```csharp
class Car
{
    public string model = "Mustang";
}

class Program
{
    static void Main(string[] args)
    {
        Car myObj = new Car();
        Console.WriteLine(myObj.model);
    }
}
```

输出将是：

Mustang

## 2.23 属性和封装

在我们开始解释属性之前，你应该对“封装”有一个基本的了解。

封装的含义是确保“敏感”数据对用户隐藏。要实现这一点，你必须：

- 将字段/变量声明为 `private`
- 通过属性提供公共的 `get` 和 `set` 方法，以访问和更新私有字段的值

### 属性

你在上一章中了解到，私有变量只能在同一个类内访问（外部类无法访问）。然而，有时我们需要访问它们——这可以通过属性来实现。

属性类似于变量和方法的组合，它有两个方法：`get` 和 `set` 方法：

示例：

```csharp
class Person
{
    private string name; // field

    public string Name // property
    {
        get { return name; } // get method
        set { name = value; } // set method
    }
}
```

## 2.24 继承（派生类和基类）

在 C# 中，可以将一个类的字段和方法继承到另一个类。我们将“继承概念”分为两类：

- **派生类（子类）** - 继承另一个类的类
- **基类（父类）** - 被继承的类

要继承一个类，请使用 `:` 符号。

在下面的示例中，Car 类（子类）继承 Vehicle 类（父类）的字段和方法：

## 多态和方法重写

多态意味着“多种形式”，当我们有许多通过继承相互关联的类时，就会出现多态。

正如我们在上一章中指定的，继承让我们从另一个类继承字段和方法。多态使用这些方法来执行不同的任务。这允许我们以不同的方式执行同一个操作。

例如，考虑一个名为 Animal 的基类，它有一个名为 `animalSound()` 的方法。Animal 的派生类可能是猪、猫、狗、鸟——而且它们还


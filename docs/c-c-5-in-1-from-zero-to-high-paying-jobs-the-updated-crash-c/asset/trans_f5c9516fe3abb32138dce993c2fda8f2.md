

```csharp
abstract class Shape
{
    public abstract double CalculateArea();
}
```

### 第 2 步：实现子类

创建子类 `Circle` 和 `Rectangle`，二者都继承自 `Shape` 基类。在每个子类中重写 `CalculateArea()` 方法。

```csharp
class Circle : Shape
{
    public double Radius { get; set; }
    public Circle(double radius)
    {
        Radius = radius;
    }
    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}
class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }
    public Rectangle(double width, double height)
    {
        Width = width;
        Height = height;
    }
    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```

### 第 3 步：使用多态

创建一个使用多态来操作形状的程序。我们将创建一个包含不同形状的数组，并调用它们的 `CalculateArea()` 方法，而不必担心它们的具体类型。

```csharp
class Program
{
    static void Main(string[] args)
    {
        Shape[] shapes = new Shape[]
        {
            new Circle(5),
            new Rectangle(3, 4),
            new Circle(7)
        };

        foreach (Shape shape in shapes)
        {
            double area = shape.CalculateArea();
            Console.WriteLine($"Area of the shape: {area}");
        }
    }
}
```

### 输出：

```
Area of the shape: 78.53981633974483
Area of the shape: 12
Area of the shape: 153.93804002589985
```

## 第4章：第3部分总结

在这个示例中，多态使我们能够创建可处理不同形状的通用代码，而不论其具体类型如何。通过利用公共基类并在子类中重写方法，我们能够操作形状集合，而无需知道它们的确切类型。这展示了多态如何增强代码的灵活性和可复用性，使你能够编写更通用、更泛化的代码来处理各种对象。

通过掌握 C# 的面向对象编程（OOP）原则，并理解如何创建类、对象和接口，你将稳步迈向构建模块化且可维护的应用程序。驾驭继承和多态的能力将使你能够设计出适应不断变化需求的健壮软件。

## 第4部分：中级 C# 编程

## 第1章：中级 C# 特性

在本章中，我们将深入探讨一些提升你编程技能的中级 C# 特性。我们将探索委托与事件、用于数据查询的语言集成查询（LINQ），以及异常处理的最佳实践。这些主题将使你能够编写更通用、更健壮的代码。

- 1. 委托与事件

### 委托

委托是一种表示方法引用的类型。它允许你将方法视为一等公民，使方法更加灵活，并支持回调函数等场景。

以声明式风格编写，并可用于集合、数据库、XML 等。

```csharp
var evenNumbers = from num in numbers
where num % 2 == 0
select num;
```

### LINQ to Objects

LINQ to Objects 支持查询内存中的集合、数组和列表。

### LINQ to SQL

LINQ to SQL 支持使用 C# 语法查询和修改 SQL 数据库中的数据。

### 3. 异常处理最佳实践

### Try-Catch 块

使用 try-catch 块来优雅地捕获和处理异常，防止程序崩溃。

```csharp
try
{
    // Code that might throw exceptions
}
catch (Exception ex)
{
    // Handle the exception
}
```

### 异常类型

C# 提供了多种异常类型，例如 `ArgumentException`、`InvalidOperationException` 等。请选择合适的异常类型来传达错误的性质。

### 自定义异常

当内置异常无法完整描述你应用程序特有的错误时，创建自定义异常类。

```csharp
public class MyCustomException : Exception
{
    public MyCustomException(string message) : base(message)
    {
    }
}
```

### 异常处理最佳实践

- **处理特定异常：** 在捕获更宽泛的异常之前先捕获特定异常，以便妥善处理。
- **记录异常：** 记录异常以帮助调试和故障排除。
- **清理资源：** 使用 `finally` 块确保资源得到正确释放，即使发生异常也是如此。

在本章中，你探索了将编程技能提升到更高水平的中级 C# 特性。委托与事件使你能够处理动态行为和通知，LINQ 提供强大的查询能力，而异常处理最佳实践可确保代码保持可靠和健壮。这些概念将为你提供工具，以编写更具表现力、更高效且更可维护的 C# 代码。

## 第2章：C# 应用程序与项目

在本章中，我们将探索 C# 在各领域的实际应用，并提出项目想法，让你的技能付诸实践。无论你对 Web 开发、创建 Windows 应用程序，还是深入游戏开发感兴趣，C# 都能满足你的需求。让我们开始吧！

### 1. C# 的实际应用

### Web 开发

C# 与 ASP.NET 框架一起广泛用于 Web 开发。你可以使用 ASP.NET Core 和 Blazor 等技术构建动态且功能丰富的 Web 应用程序。

### Windows 应用程序

C# 是使用 Windows Forms、WPF（Windows Presentation Foundation）和 UWP（Universal Windows Platform）开发 Windows 应用程序的首选语言。这些技术允许你创建具有丰富用户界面的桌面应用程序。

### 游戏开发

C# 在游戏开发行业中越来越受欢迎，尤其是在 Unity 游戏引擎中。你可以利用 Unity 内 C# 脚本的强大能力，为各种平台创建 2D 和 3D 游戏。

### 2. 项目想法

### Web 应用程序

想法：使用 ASP.NET Core MVC 开发一个任务管理 Web 应用程序。用户可以创建、编辑和组织任务，应用程序可以提供用户身份验证和实时更新。

优势：该项目让你练习 Web 开发基础知识，包括处理 HTTP 请求、使用数据库以及创建交互式用户界面。

### 桌面实用工具

想法：使用 Windows Forms 创建一个密码管理器桌面应用程序。该应用程序应安全地存储密码、生成强密码并提供密码提醒。

**优势：** 该项目增强你的 Windows 应用程序开发技能，并教你数据加密、文件 I/O 和用户界面设计。

### 3. 强调持续学习与更多资源

当你着手 C# 项目和应用时，请记住学习是一个持续的过程。请及时了解 C# 的最新进展，并探索异步编程、设计模式和依赖注入等高级主题。

### 更多资源

- **在线教程：** Microsoft Docs、Codecademy 和 Pluralsight 等网站提供关于 C# 及相关技术的全面教程。
- **书籍：** 由 Jon Skeet 编写的《C# in Depth》和由 Andrew Troelsen 编写的《Pro C# 9 with .NET 5》等知名书籍深入剖析了 C# 概念。
- **社区论坛：** 在 Stack Overflow 和 Reddit 等平台上与 C# 社区互动，提出问题、分享知识，并从他人的经验中学习。
- **编码挑战：** LeetCode 和 HackerRank 等平台提供编码挑战，以磨练你的问题解决能力。

## 第3章：第4部分总结

在本章中，我们探索了 C# 在 Web 开发、Windows 应用程序和游戏开发中的实际应用。我们还提供了项目想法，帮助你将技能应用于现实场景。请记住，C# 提供了多样化的机会；当你开展项目时，请不断寻找新资源来扩展你的知识和专长。通过将学习与实践经验相结合，你将成为一名熟练的 C# 开发者，能够构建有影响力的应用程序和项目。

## 第5部分：高级 C# 概念

## 第1章：高级 C# 主题

在本章中，我们将深入探讨将你的编程技能提升到更高水平的高级 C# 主题。我们将探索用于高效并行执行的多线程与异步编程、用于动态行为的反射与特性，并深入研究用于有效组织应用程序的依赖注入与设计模式。让我们深入这些主题，它们将扩展你的 C# 熟练度。

### 1. 多线程与异步编程

### 多线程

多线程使你的应用程序能够同时执行多个任务，从而提高性能和响应能力。请注意线程同步，以避免竞态条件。


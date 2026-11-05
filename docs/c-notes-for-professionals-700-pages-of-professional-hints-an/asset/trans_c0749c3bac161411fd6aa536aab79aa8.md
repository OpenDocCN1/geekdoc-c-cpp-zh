
警告：由于其工作原理，默认值在某些情况下可能存在问题。如果更改方法参数的默认值且未重新编译该方法的所有调用方，这些调用方仍将使用编译时存在的默认值，可能导致不一致。

## 第 47.7 节：方法重载

### 定义

当声明多个具有相同名称但参数不同的 方法 时，称为方法重载。方法重载通常表示在目的上相同的函数，但编写时接受不同数据类型作为其参数。

### 影响因素

- 参数数量
- 参数类型
- 返回类型

考虑一个名为 Area 的方法，它将执行计算功能，接受各种参数并返回结果。

### 示例

```csharp
public string Area(int value1)
{
    return String.Format("Area of Square is {0}", value1 * value1);
}
```

该方法将接受一个参数并返回一个字符串，如果我们使用整数（例如 5）调用该方法，输出将为 "Area of Square is 25"。

```csharp
public double Area(double value1, double value2)
{
    return value1 * value2;
}
```

类似地，如果我们向此方法传递两个 double 值，输出将是这两个值的乘积，类型为 double。这可用于乘法以及查找矩形的面积

```csharp
public double Area(double value1)
{
    return 3.14 * Math.Pow(value1,2);
}
```

这可专门用于查找圆的面积，它将接受一个 double 值（半径）并返回另一个 double 值作为其面积。

这些方法中的每一个都可以正常调用而不会冲突——编译器将检查每次方法调用的参数以确定需要使用哪个版本的 Area。

```csharp
string squareArea = Area(2);
double rectangleArea = Area(32.0, 17.5);
double circleArea = Area(5.0); // all of these are valid and will compile.
```

**请注意，返回类型单独无法区分两个方法。例如，如果我们有两个 Area 的定义，它们具有相同的参数，如下所示：**

```csharp
public string Area(double width, double height) { ... }
public double Area(double width, double height) { ... }
// This will NOT compile.
```

如果我们需要让类使用返回不同值的相同方法名称，我们可以通过实现接口并显式定义其用法来消除歧义问题。

```csharp
public interface IAreaCalculatorString {
    public string Area(double width, double height);
}

public class AreaCalculator : IAreaCalculatorString {
    public string IAreaCalculatorString.Area(double width, double height) { ... }
    // Note that the method call now explicitly says it will be used when called through
    // the IAreaCalculatorString interface, allowing us to resolve the ambiguity.
    public double Area(double width, double height) { ... }
}
```

## 第 47.8 节：访问权限

```csharp
// static: is callable on a class even when no instance of the class has been created
public static void MyMethod()

// virtual: can be called or overridden in an inherited class
public virtual void MyMethod()

// internal: access is limited within the current assembly
internal void MyMethod()

//private: access is limited only within the same class
private void MyMethod()

//public: access right from every class / assembly
public void MyMethod()

//protected: access is limited to the containing class or types derived from it
protected void MyMethod()

//protected internal: access is limited to the current assembly or types derived from the containing class.
protected internal void MyMethod()
```

## 第 48 章：扩展方法

| 参数 | 详情 |
|---|---|
| this | 扩展方法的第一个参数始终应以 `this` 关键字开头，后跟用于引用要扩展的对象的“当前”实例的标识符 |

### 第 48.1 节：扩展方法 - 概述

扩展方法在 C# 3.0 中引入。扩展方法在不创建新的派生类型、重新编译或以其他方式修改原始类型的情况下扩展并为现有类型添加行为。*当您无法修改要增强的类型源时，它们尤其有帮助。* 扩展方法可以为系统类型、第三方定义的类型以及您自己定义的类型创建。扩展方法可以像原始类型的成员方法一样被调用。这允许使用 **方法链** 来实现 **流畅接口**。

扩展方法是通过向与被扩展的原始类型不同的 `static class` 添加 `static method` 来创建的。保存扩展方法的静态类通常仅为保存扩展方法而创建。

扩展方法采用一个特殊的第一个参数来指定被扩展的原始类型。此第一个参数用关键字 `this` 装饰（这在 C# 中构成了 `this` 的一种特殊且不同的用法——应将其理解为不同于允许引用当前对象实例成员的 `this` 的用法）。

在下面的示例中，被扩展的原始类型是类 `string`。`string` 已通过方法 `Shorten()` 进行了扩展，该方法提供了缩短的额外功能。静态类 `StringExtensions` 已被创建以保存扩展方法。扩展方法 `Shorten()` 通过特别标记的第一个参数表明它是 `string` 的扩展。为了表明 `Shorten()` 方法扩展了 `string`，第一个参数被标记为 `this`。因此，第一个参数的完整签名是 `this string text`，其中 `string` 是被扩展的原始类型，text 是所选的参数名称。

```csharp
static class StringExtensions
{
    public static string Shorten(this string text, int length)
    {
        return text.Substring(0, length);
    }
}

class Program
{
    static void Main()
    {
        // This calls method String.ToUpper()
        var myString = "Hello World!".ToUpper();

        // This calls the extension method StringExtensions.Shorten()
        var newString = myString.Shorten(5);

        // It is worth noting that the above call is purely syntactic sugar
        // and the assignment below is functionally equivalent
        var newString2 = StringExtensions.Shorten(myString, 5);
    }
}
```

.NET Fiddle 上的实时演示

作为扩展方法的第一个参数传递的对象（附带 `this` 关键字）是调用扩展方法的实例。

例如，当执行以下代码时：

```csharp
"some string".Shorten(5);
```

参数的值如下：

```
text: "some string"
length: 5
```

*请注意，扩展方法只有在与定义在同一命名空间中、使用扩展方法的代码显式导入命名空间，或扩展类没有命名空间时才可用。.NET 框架指南建议将扩展类放在自己的命名空间中。然而，这可能导致发现问题。*

这不会导致扩展方法与所使用的库之间出现冲突，除非可能冲突的命名空间被显式引入。例如 LINQ 扩展：

```csharp
using System.Linq; // Allows use of extension methods from the System.Linq namespace

class Program
{
    static void Main()
    {
        var ints = new int[] {1, 2, 3, 4};

        // Call Where() extension method from the System.Linq namespace
        var even = ints.Where(x => x % 2 == 0);
    }
}
```

.NET Fiddle 上的实时演示

自 C# 6.0 起，还可以将 `using static` 指令放在包含扩展方法的 `class` 上。例如，`using static System.Linq.Enumerable;`。这使得该特定类中的扩展方法可用，而不会将同一命名空间中的其他类型引入作用域。

当具有相同签名的类方法可用时，编译器会优先于扩展方法调用。例如：

```csharp
class Test
{
    public void Hello()
    {
        Console.WriteLine("From Test");
    }
}
```

```csharp
static class TestExtensions
{
    public static void Hello(this Test test)
    {
        Console.WriteLine("From extension method");
    }
}
```

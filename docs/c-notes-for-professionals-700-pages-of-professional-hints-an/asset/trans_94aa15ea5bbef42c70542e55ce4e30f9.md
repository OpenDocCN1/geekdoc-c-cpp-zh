

## 第33章：内置类型的别名

### 33.1节：内置类型表

下表列出了内置 C# 类型的关键字，这些关键字是 System 命名空间中预定义类型的别名。

| C# 类型 | .NET Framework 类型 |
|---|---|
| bool | System.Boolean |
| byte | System.Byte |
| sbyte | System.SByte |
| char | System.Char |
| decimal | System.Decimal |
| double | System.Double |
| float | System.Single |
| int | System.Int32 |
| uint | System.UInt32 |
| long | System.Int64 |
| ulong | System.UInt64 |
| object | System.Object |
| short | System.Int16 |
| ushort | System.UInt16 |
| string | System.String |

C# 类型关键字及其别名可以互换。例如，可以使用以下任一声明来声明一个整数变量：

```csharp
int number = 123;
System.Int32 number = 123;
```

## 第34章：匿名类型

### 34.1节：匿名类型与动态类型

匿名类型允许创建对象，而无需事先显式定义其类型，同时保持静态类型检查。

```csharp
var anon = new { Value = 1 };
Console.WriteLine(anon.Id); // compile time error
```

相反，dynamic 具有动态类型检查，宁可选择运行时错误，而不是编译时错误。

```csharp
dynamic val = "foo";
Console.WriteLine(val.Id); // compiles, but throws runtime error
```

### 34.2节：创建匿名类型

由于匿名类型没有名称，因此这些类型的变量必须隐式类型化（var）。

```csharp
var anon = new { Foo = 1, Bar = 2 };
// anon.Foo == 1
// anon.Bar == 2
```

如果未指定成员名称，则成员名称将设置为用于初始化对象的属性/变量的名称。

```csharp
int foo = 1;
int bar = 2;
var anon2 = new { foo, bar };
// anon2.foo == 1
// anon2.bar == 2
```

请注意，仅当匿名类型声明中的表达式是简单的属性访问时，才能省略名称；对于方法调用或更复杂的表达式，必须指定属性名称。

```csharp
string foo = "some string";
var anon3 = new { foo.Length };
// anon3.Length == 11
var anon4 = new { foo.Length <= 10 ? "short string" : "long string" };
// compiler error - Invalid anonymous type member declarator.
var anon5 = new { Description = foo.Length <= 10 ? "short string" : "long string" };
// OK
```

### 34.3节：匿名类型相等性

匿名类型的相等性由 Equals 实例方法确定。如果两个对象具有相同的类型，并且每个属性都具有相等的值（通过 Prop.Equals(b.Prop) 比较），则这两个对象相等。

```csharp
var anon = new { Foo = 1, Bar = 2 };
var anon2 = new { Foo = 1, Bar = 2 };
var anon3 = new { Foo = 5, Bar = 10 };
var anon4 = new { Foo = 5, Bar = 10 };
var anon4 = new { Bar = 2, Foo = 1 };
// anon.Equals(anon2) == true
// anon.Equals(anon3) == false
```
```
// anon.Equals(anon4) == false (anon and anon4 have different types, see below)
```

当且仅当两个匿名类型的属性具有相同的名称和类型，并且以相同的顺序出现时，才认为这两个匿名类型相同。

```csharp
var anon = new { Foo = 1, Bar = 2 };
var anon2 = new { Foo = 7, Bar = 1 };
var anon3 = new { Bar = 1, Foo = 3 };
var anon4 = new { Fa = 1, Bar = 2 };
// anon and anon2 have the same type
// anon and anon3 have different types (Bar and Foo appear in different orders)
// anon and anon4 have different types (property names are different)
```

### 34.4节：使用匿名类型的泛型方法

泛型方法允许通过类型推断来使用匿名类型。

```csharp
void Log<T>(T obj) {
    // ...
}
Log(new { Value = 10 });
```

这意味着 LINQ 表达式可以与匿名类型一起使用：

```csharp
var products = new[] {
    new { Amount = 10, Id = 0 },
    new { Amount = 20, Id = 1 },
    new { Amount = 15, Id = 2 }
};
var idsByAmount = products.OrderBy(x => x.Amount).Select(x => x.Id);
// idsByAmount: 0, 2, 1
```

### 34.5节：使用匿名类型实例化泛型类型

使用泛型构造函数将要求匿名类型具有名称，而这是不可能的。另一种方式是使用泛型方法来允许类型推断发生。

```csharp
var anon = new { Foo = 1, Bar = 2 };
var anon2 = new { Foo = 5, Bar = 10 };
List<T> CreateList<T>(params T[] items) {
    return new List<T>(items);
}
var list1 = CreateList(anon, anon2);
```

对于 List<T>，可以通过 ToList LINQ 方法将隐式类型化数组转换为 List<T>：

```csharp
var list2 = new[] {anon, anon2}.ToList();
```

### 34.6节：隐式类型化数组

可以使用隐式类型化创建匿名类型数组。

```csharp
var arr = new[] {
    new { Id = 0 },
new { Id = 1 }
};
```

## 第35章：动态类型

### 35.1节：创建带属性的动态对象

```csharp
using System;
using System.Dynamic;

dynamic info = new ExpandoObject();
info.Id = 123;
info.Another = 456;

Console.WriteLine(info.Another);
// 456

Console.WriteLine(info.DoesntExist);
// Throws RuntimeBinderException
```

### 35.2节：创建动态变量

```csharp
dynamic foo = 123;
Console.WriteLine(foo + 234);
// 357
Console.WriteLine(foo.ToUpper())
// RuntimeBinderException, since int doesn't have a ToUpper method

foo = "123";
Console.WriteLine(foo + 234);
// 123234
Console.WriteLine(foo.ToUpper());
// NOW A STRING
```

### 35.3节：返回 dynamic

```csharp
using System;

public static void Main()
{
    var value = GetValue();
    Console.WriteLine(value);
    // dynamics are useful!
}

private static dynamic GetValue()
{
    return "dynamics are useful!";
}
```

### 35.4节：处理编译时未知的特定类型

以下代码产生等效结果：

```csharp
class IfElseExample
{
    public string DebugToString(object a)
    {
        if (a is StringBuilder)
{
    return DebugToStringInternal(a as StringBuilder);
}
else if (a is List<string>)
{
    return DebugToStringInternal(a as List<string>);
}
else
{
    return a.ToString();
}
}

private string DebugToStringInternal(object a)
{
    // Fall Back
    return a.ToString();
}

private string DebugToStringInternal(StringBuilder sb)
{
    return $"StringBuilder - Capacity: {sb.Capacity}, MaxCapacity: {sb.MaxCapacity}, Value: {sb.ToString()}";
}

private string DebugToStringInternal(List<string> list)
{
    return $"List<string> - Count: {list.Count}, Value: {Environment.NewLine + "\t" + string.Join(Environment.NewLine + "\t", list.ToArray())}";
}

class DynamicExample
{
    public string DebugToString(object a)
    {
        return DebugToStringInternal((dynamic)a);
    }

    private string DebugToStringInternal(object a)
    {
        // Fall Back
        return a.ToString();
    }

    private string DebugToStringInternal(StringBuilder sb)
    {
        return $"StringBuilder - Capacity: {sb.Capacity}, MaxCapacity: {sb.MaxCapacity}, Value: {sb.ToString()}";
    }

    private string DebugToStringInternal(List<string> list)
    {
        return $"List<string> - Count: {list.Count}, Value: {Environment.NewLine + "\t" + string.Join(Environment.NewLine + "\t", list.ToArray())}";
    }
}
```

dynamic 的优势在于，添加要处理的新类型只需添加该新类型的 DebugToStringInternal 重载。同时也不再需要手动将其强制转换为该类型。

## 第36章：类型转换

### 36.1节：显式类型转换

```csharp
using System;
namespace TypeConversionApplication
{
    class ExplicitConversion
    {
        static void Main(string[] args)
        {
            double d = 5673.74;
            int i;

            // cast double to int
            i = (int)d;
            Console.WriteLine(i);
            Console.ReadKey();
        }
    }
}
```

### 36.2节：MSDN 隐式运算符示例

```csharp
class Digit
{
    public Digit(double d) { val = d; }
    public double val;

    // User-defined conversion from Digit to double
    public static implicit operator double(Digit d)
    {
        Console.WriteLine("Digit to double implicit conversion called");
        return d.val;
    }
    // User-defined conversion from double to Digit
    public static implicit operator Digit(double d)
    {
        Console.WriteLine("double to Digit implicit conversion called");
        return new Digit(d);
    }
}

class Program
{
    static void Main(string[] args)
    {
        Digit dig = new Digit(7);
        //This call invokes the implicit "double" operator
        double num = dig;
        //This call invokes the implicit "Digit" operator
        Digit dig2 = 12;
        Console.WriteLine("num = {0} dig2 = {1}", num, dig2.val);
        Console.ReadLine();
    }
}
```

输出：


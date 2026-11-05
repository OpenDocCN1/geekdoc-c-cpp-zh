
//Adds all the parts found in the same assembly as the PluginManager class
catalog.Catalogs.Add(new AssemblyCatalog(typeof(Program).Assembly));
catalog.Catalogs.Add(new DirectoryCatalog(loggersDllDirectory));

//Create the CompositionContainer with the parts in the catalog
_container = new CompositionContainer(catalog);

//Fill the imports of this object
try
{
    this._container.ComposeParts(this);
}
catch (CompositionException compositionException)
{
    throw new CompositionException(compositionException.Message);
}
}

## 第45章：部分类和方法

部分类为我们提供了一个选项，可将类拆分为多个部分并分布在多个源文件中。所有部分在编译时会被合并为一个单一类。所有部分都应包含关键字 partial，应具有相同的可访问性。所有部分都应存在于同一程序集中，以便在编译时包含。

### 第45.1节：部分类

部分类提供了一种将类声明拆分（通常拆分为单独的文件）的能力。使用部分类可以解决的一个常见问题是允许用户修改自动生成的代码，而不必担心如果代码被重新生成，其更改会被覆盖。此外，多名开发人员可以同时处理同一个类或方法。

```csharp
using System;

namespace PartialClassAndMethods
{
    public partial class PartialClass
    {
        public void ExampleMethod() {
            Console.WriteLine("Method call from the first declaration.");
        }
    }

    public partial class PartialClass
    {
        public void AnotherExampleMethod()
        {
            Console.WriteLine("Method call from the second declaration.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            PartialClass partial = new PartialClass();
            partial.ExampleMethod(); // outputs "Method call from the first declaration."
            partial.AnotherExampleMethod(); // outputs "Method call from the second declaration."
        }
    }
}
```

### 第45.2节：继承自基类的部分类

当继承自任何基类时，只需要一个部分类指定基类即可。

```csharp
// PartialClass1.cs
public partial class PartialClass : BaseClass {}
// PartialClass2.cs
public partial class PartialClass {}
```

你可以在多个部分类中指定相同的基类。某些 IDE 工具会将其标记为冗余，但它仍然可以正确编译。

```csharp
// PartialClass1.cs
public partial class PartialClass : BaseClass {}
```

```
// PartialClass2.cs
public partial class PartialClass : BaseClass {} // base class here is redundant
```

你不能在多个部分类中指定不同的基类，这会导致编译器错误。

```
// PartialClass1.cs
public partial class PartialClass : BaseClass {} // compiler error
// PartialClass2.cs
public partial class PartialClass : OtherBaseClass {} // compiler error
```

### 第45.3节：部分方法

部分方法由一个部分类声明中的定义（常见场景为自动生成的）以及另一个部分类声明中的实现组成。

```csharp
using System;

namespace PartialClassAndMethods
{
    public partial class PartialClass // Auto-generated
    {
        partial void PartialMethod();
    }

    public partial class PartialClass // Human-written
    {
        public void PartialMethod()
        {
            Console.WriteLine("Partial method called.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            PartialClass partial = new PartialClass();
            partial.PartialMethod(); // outputs "Partial method called."
        }
    }
}
```

## 第46章：对象初始化器

### 第46.1节：简单用法

对象初始化器在你需要创建对象并立即设置几个属性，但现有构造函数不足时非常方便。假设你有一个类

```csharp
public class Book
{
    public string Title { get; set; }
    public string Author { get; set; }

    // the rest of class definition
}
```

使用初始化器初始化类的新实例：

```csharp
Book theBook = new Book { Title = "Don Quixote", Author = "Miguel de Cervantes" };
```

这等价于

```csharp
Book theBook = new Book();
theBook.Title = "Don Quixote";
theBook.Author = "Miguel de Cervantes";
```

### 第46.2节：与非默认构造函数一起使用

你可以在必要时将对象初始化器与构造函数结合以初始化类型。例如，假设有一个如下定义的类：

```csharp
public class Book {
    public string Title { get; set; }
    public string Author { get; set; }

    public Book(int id) {
        //do things
    }

    // the rest of class definition
}
```
var someBook = new Book(16) { Title = "Don Quixote", Author = "Miguel de Cervantes" }

这将首先使用 Book(int) 构造函数实例化一个 Book，然后在初始化器中设置每个属性。这等价于：

```csharp
var someBook = new Book(16);
someBook.Title = "Don Quixote";
someBook.Author = "Miguel de Cervantes";
```

### 第46.3节：与匿名类型一起使用

对象初始化器是初始化匿名类型的唯一方式，而匿名类型是由编译器生成的类型。

```csharp
var album = new { Band = "Beatles", Title = "Abbey Road" };
```

因此，对象初始化器在 LINQ select 查询中被广泛使用，因为它们提供了一种便捷的方式来指定你对查询对象的哪些部分感兴趣。

```csharp
var albumTitles = from a in albums
    select new
    {
        Title = a.Title,
        Artist = a.Band
    };
```

## 第47章：方法

### 第47.1节：调用方法

调用静态方法：

// Single argument
System.Console.WriteLine("Hello World");

// Multiple arguments
string name = "User";
System.Console.WriteLine("Hello, {0}!", name);

调用静态方法并存储其返回值：

```
string input = System.Console.ReadLine();
```

调用实例方法：

```
int x = 42;
// The instance method called here is Int32.ToString()
string xAsString = x.ToString();
```

调用泛型方法

```
// Assuming a method 'T[] CreateArray<T>(int size)'
DateTime[] dates = CreateArray<DateTime>(8);
```

### 第47.2节：匿名方法

匿名方法提供了一种将代码块作为委托参数传递的技术。它们是有方法体但没有名称的方法。

```csharp
delegate int IntOp(int lhs, int rhs);

class Program
{
    static void Main(string[] args)
    {
        // C# 2.0 definition
        IntOp add = delegate(int lhs, int rhs)
        {
            return lhs + rhs;
        };

        // C# 3.0 definition
        IntOp mul = (lhs, rhs) =>
        {
            return lhs * rhs;
        };

        // C# 3.0 definition - shorthand
        IntOp sub = (lhs, rhs) => lhs - rhs;

        // Calling each method
        Console.WriteLine("2 + 3 = " + add(2, 3));
        Console.WriteLine("2 * 3 = " + mul(2, 3));
    }
}
```

```
Console.WriteLine("2 - 3 = " + sub(2, 3));
}
```

### 第47.3节：声明方法

每个方法都有一个唯一的签名，由访问修饰符（public、private、...）、可选的修饰符（abstract）、名称以及如果需要的方法参数组成。注意，返回类型不是签名的一部分。方法原型如下所示：

```
AccessModifier OptionalModifier ReturnType MethodName(InputParameters)
{
    //Method body
}
```

AccessModifier 可以是 public、protected、private 或默认的 internal。

OptionalModifier 可以是 static、abstract、virtual、override、new 或 sealed。

ReturnType 可以是 void 表示无返回，也可以是基本类型如 int 到复杂类的任意类型。

方法可能有或没有输入参数。要为方法设置参数，你应该像声明普通变量一样声明每个参数（如 int a），对于多个参数，你应该用逗号分隔它们（如 int a, int b）。

参数可以有默认值。为此，你应该为参数设置一个值（如 int a = 0）。如果参数有默认值，则设置输入值是可选的。

以下方法示例返回两个整数的和：

```
private int Sum(int a, int b)
{
    return a + b;
}
```

### 第47.4节：参数和参数

方法可以声明任意数量的参数（在此示例中，i、s 和 o 是参数）：

```
static void DoSomething(int i, string s, object o) {
    Console.WriteLine(String.Format("i={0}, s={1}, o={2}", i, s, o));
}
```

参数可用于将值传递给方法，以便方法可以处理它们。这可以是各种工作，例如打印值、修改参数引用的对象，或存储值。

当你调用方法时，你需要为每个参数传递一个实际值。此时，你实际传递给方法调用的值称为参数（Arguments）：

```
DoSomething(x, "hello", new object());
```

### 第47.5节：返回类型

方法可以返回 nothing（void），或指定类型的值：

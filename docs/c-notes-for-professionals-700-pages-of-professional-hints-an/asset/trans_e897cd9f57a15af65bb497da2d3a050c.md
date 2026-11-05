
```
~~~csharp
{
    _price = price;
}

private decimal _price;
public decimal Price { get { return _price * (1 + vat); } }
}
~~~
```

## 第 52.53 节：委托

委托是表示对方法的引用的类型。它们用于将方法作为参数传递给其他方法。

委托可以保存静态方法、实例方法、匿名方法或 lambda 表达式。

```
~~~csharp
class DelegateExample
{
    public void Run()
    {
        //using class method
        InvokeDelegate( WriteToConsole );

        //using anonymous method
        DelegateInvoker di = delegate ( string input )
        {
            Console.WriteLine( string.Format( "di: {0} ", input ) );
            return true;
        };
        InvokeDelegate( di );

        //using lambda expression
        InvokeDelegate( input => false );
    }

    public delegate bool DelegateInvoker( string input );

    public void InvokeDelegate(DelegateInvoker func)
    {
        var ret = func( "hello world" );
        Console.WriteLine( string.Format( " > delegate returned {0}", ret ) );
    }

    public bool WriteToConsole( string input )
    {
        Console.WriteLine( string.Format( "WriteToConsole: '{0}'", input ) );
        return true;
    }
}
~~~
```

将方法分配给委托时需要注意，方法必须具有相同的返回类型以及参数。这与“普通”方法重载不同，在普通方法重载中，只有参数定义了方法的签名。

事件是基于委托构建的。

## 第 52.54 节：unchecked

`unchecked` 关键字可防止编译器检查溢出/下溢。

例如：

```
const int ConstantMax = int.MaxValue;
unchecked
{
    int i1 = 2147483647 + 10;
}
int i1 = unchecked(ConstantMax + 10);
```

如果没有 unchecked 关键字，这两个加法运算都无法编译。

### 这在什么时候有用？

这很有用，因为它可能有助于加快肯定不会溢出的计算的速度，因为溢出检查需要时间，或者当溢出/下溢是期望的行为时（例如，在生成哈希码时）。

## 第 52.55 节：ushort

用于存储 16 位正整数的数值类型。ushort 是 System.UInt16 的别名，占 2 字节内存。

有效范围是 0 到 65535。

```
ushort a = 50; // 50
ushort b = 65536; // Error, cannot be converted
ushort c = unchecked((ushort)65536); // Overflows (wraps around to 0)
```

## 第 52.56 节：sizeof

用于获取非托管类型的字节大小

```
int byteSize = sizeof(byte); // 1
int sbyteSize = sizeof(sbyte); // 1
int shortSize = sizeof(short); // 2
int ushortSize = sizeof(ushort); // 2
int intSize = sizeof(int); // 4
int uintSize = sizeof(uint); // 4
int longSize = sizeof(long); // 8
int ulongSize = sizeof(ulong); // 8
int charSize = sizeof(char); // 2(Unicode)
int floatSize = sizeof(float); // 4
int doubleSize = sizeof(double); // 8
int decimalSize = sizeof(decimal); // 16
int boolSize = sizeof(bool); // 1
```

## 第 52.57 节：in

in 关键字有三种用法：

- a) 作为 foreach 语句语法的一部分或作为 LINQ 查询语法的一部分

```
foreach (var member in sequence)
{
    // ...
}
```

- b) 在泛型接口和泛型委托类型的上下文中，表示所讨论的类型参数的 *contravariance*：

```csharp
public interface IComparer<in T>
{
    // ...
}
```

- c) 在 LINQ 查询的上下文中，指正在被查询的集合

```csharp
var query = from x in source select new { x.Name, x.ID, };
```

## 第 52.58 节：implicit

`implicit` 关键字用于重载转换运算符。例如，您可以声明一个 `Fraction` 类，该类在需要时应自动转换为 `double`，并且可以从 `int` 自动转换：

```csharp
class Fraction(int numerator, int denominator)
{
    public int Numerator { get; } = numerator;
    public int Denominator { get; } = denominator;
    // ...
    public static implicit operator double(Fraction f)
    {
        return f.Numerator / (double) f.Denominator;
    }
    public static implicit operator Fraction(int i)
    {
        return new Fraction(i, 1);
    }
}
```

## 第 52.59 节：do

`do` 运算符会重复执行一段代码块，直到条件查询等于 false。do-while 循环也可以通过 `goto`、`return`、`break` 或 `throw` 语句中断。

`do` 关键字的语法是：

> `do { code block; } while( condition );`

示例：

```csharp
int i = 0;

do
{
    Console.WriteLine("Do is on loop number {0}.", i);
} while (i++ < 5);
```

输出：

> "Do is on loop number 1."
> "Do is on loop number 2."
> "Do is on loop number 3."
> "Do is on loop number 4."
> "Do is on loop number 5."

与 while 循环不同，do-while 循环是出口控制的。这意味着 do-while 循环即使条件第一次判断失败，也至少会执行一次其语句。

```
bool a = false;
do
{
    Console.WriteLine("This will be printed once, even if a is false.");
} while (a == true);
```

## 第 52.60 节：long

long 关键字用于表示有符号 64 位整数。它是存在于 mscorlib.dll 中的 System.Int64 数据类型的别名，每当您创建 C# 项目时，每个项目都会隐式引用它。

任何 long 变量都可以显式和隐式声明：

```
long long1 = 9223372036854775806; // explicit declaration, long keyword used
var long2 = -9223372036854775806L; // implicit declaration, 'L' suffix used
```

long 变量可以保存从 −9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 的任何值，并且在变量必须保存超出其他变量（如 int 变量）范围的值的情况下很有用。

## 第 52.61 节：enum

enum 关键字告诉编译器此类继承自抽象类 Enum，而无需程序员显式继承。Enum 是 ValueType 的后代，ValueType 用于与一组不同的命名常量一起使用。

```
public enum DaysOfWeek
{
    Monday,
    Tuesday,
}
```

您可以选择为每个（或其中一些）指定特定值：

```
public enum NotableYear
{
    EndOfWWI = 1918,
    EndOfWWII = 1945,
}
```

在此示例中我省略了 0 的值，这通常是不良做法。枚举始终会有一个通过显式转换产生的默认值（YourEnumType）0，其中 YourEnumType 是您声明的枚举类型。如果未定义 0 的值，枚举在初始化时将没有定义的值。

enum 的默认基础类型是 int，您可以将基础类型更改为任何整型，包括 byte、sbyte、short、ushort、int、uint、long 和 ulong。下面是一个基础类型为 byte 的枚举：

```csharp
enum Days : byte
{
    Sunday = 0,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
};
```

还请注意，您可以通过强制转换简单地在基础类型之间进行转换：

```csharp
int value = (int)NotableYear.EndOfWWI;
```

因此，在公开库函数时，最好始终检查枚举是否有效：

```csharp
void PrintNotes(NotableYear year)
{
    if (!Enum.IsDefined(typeof(NotableYear), year))
        throw new InvalidEnumArgumentException("year", (int)year, typeof(NotableYear));
    // ...
}
```

## 第 52.62 节：partial

partial 关键字可在类、结构或接口的类型定义期间使用，以允许将类型定义拆分为多个文件。这对于在自动生成的代码中合并新功能很有用。

### File1.cs

```csharp
namespace A
{
    public partial class Test
    {
        public string Var1 {get;set;}
    }
}
```

### File2.cs

```csharp
namespace A
{
    public partial class Test
    {
        public string Var2 {get;set;}
    }
}
```

注意：一个类可以拆分为任意数量的文件。但是，所有声明必须在同一命名空间和同一程序集中。

方法也可以使用 partial 关键字声明为 partial。在这种情况下，一个文件只包含方法定义，另一个文件包含实现。

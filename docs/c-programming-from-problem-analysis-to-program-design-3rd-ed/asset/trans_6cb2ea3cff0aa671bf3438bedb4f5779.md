
这里展示的基于对象的方法不是类型安全的。`string` 类型的数据可能会被压入同一个也保存整数的栈中。检索数据时，如果尝试对 `string` 项进行算术运算，程序将异常终止。为避免此问题，可以定义三个独立的栈类：一个用于整数，另一个用于双精度浮点数，第三个用于字符串。这可以通过复制粘贴代码来实现。但是，如果需要进行简单的修改，则必须对这三个类都进行更正。这正是泛型发挥作用的地方。它们允许你定义类型安全、由编译器生成的代码，这些代码可以用任意类型来定义和使用。内部算法保持不变，但 `class` 可以定义一次并重复使用。示例 11-27 演示了如何定义一个简单的泛型 `class`。

### 示例 11-27

```csharp
public class GenericClass<T>
{
    public T dataMember;
}
```

请注意，泛型 `class` 的定义方式是在类定义行的左右尖括号之间插入一个标识符。在示例 11-27 中，使用 T 作为标识符。T 是 Microsoft 大多数文档中用于定义泛型类型的标准标识符；不过，只要遵守创建标识符的规则，你可以使用任何有效标识符。在方法体中，标识符被放在应插入数据类型的位置。它可以作为方法中的返回类型、方法的参数列表中的类型，或如示例 11-27 所示，作为实例数据成员的数据类型。

创建该类的实例时，需要指定用于替换类型参数的实际类型。如果 dataMember 被定义为 `public`（或者 dataMember 有可用的 `public` 属性），则可以如示例 11-28 所示使用该 `class`。

### 示例 11-28

```csharp
GenericClass<string> anIdentifier = new GenericClass<string>();
anIdentifier.dataMember = "A string";
```

你可以利用这一新特性，将 Stack `class` 重新定义为泛型 `class`。示例 11-29 对此进行了说明。

### 示例 11-29

```csharp
public class Stack<T>
{
    private T[] items;
    private int stackPointer = 0;

public Stack(int size)
{
    items = new T[size];
}

public T Pop( )
{
    return items[--stackPointer];
}

public void Push(T anItem)
{
    items[stackPointer] = anItem;
    stackPointer++;
}
```

示例 11-30 说明了实现该类所需的更改。请注意，这里实例化了三个独立的对象。可以放入 int Stack 的值只能是整数。因此，创建了一个类型安全的数据结构。

### 示例 11-30

```csharp
public class TestOfGenericStack
{
    static void Main(string[ ] args)
    {
        Stack<int> intStack = new Stack<int>( 5 );
        Stack<double> doubleStack = new Stack<double>( 5 );
        Stack<string> stringStack = new Stack<string>( 5 );
        stringStack.Push("test");

        intStack.Push(100);
        intStack.Push(200);

        doubleStack.Push(3.6);

        Console.WriteLine("Values in the 3 Stacks are: " +
            doubleStack.Pop( ) + ", " +
            intStack.Pop( ) + ", " +
            intStack.Pop( ) + ", " +
            stringStack.Pop( ) );
    }
}
```

请注意，在示例 11-30 中不需要进行强制转换。示例 11-29 和 11-30 产生的输出与图 11-17 所示相同。

## 泛型方法

你可以定义不属于泛型类的泛型方法。这样，方法会推迟指定一个或多个类型，直到客户端代码声明并实例化该方法。定义泛型方法与定义泛型类类似。在方法定义行的左右尖括号之间插入一个标识符，以表明它是泛型方法。然后将该标识符放在参数列表中、作为返回类型，或同时放在这两处。示例 11-31 对此进行了说明。

### 示例 11-31

```csharp
public static void SwapData<T> (ref T first, ref T second)
{
        T temp;
        temp = first;
        first = second;
        second = temp;
}
```

示例 11-32 展示了对 SwapData( ) 方法的调用。

### 示例 11-32

```csharp
public static void TestSwap( )
{
        string firstValue = "Programming";
        string secondValue = "C#";
        SwapData<string>(ref firstValue, ref secondValue);
        System.Console.WriteLine(firstValue + " " + secondValue);
}
```

如示例 11-32 所示，调用泛型方法时，需要在方法名和参数列表之间指定实际类型。在此示例中，使用了 string 类型。

![](img/e33ae760e23d89eac66541252ad65de8_724_0.png)

回想一下，将 ref 关键字添加到实参和参数列表中，以便按引用传递实参。其效果是，当控制权返回到调用方法时，在 SwapData( ) 方法中对参数所做的更改将反映在该变量中。在 C# 中，必须既在方法的参数列表中添加 ref 关键字，也在调用方的实参列表中添加 ref 关键字。

## 动态类型

C# 最初被描述为一种强类型语言，要求在编译时将存储的所有数据位都与已定义的类型关联起来。这使编译器能够检查并确保只尝试存储兼容的值。潜在错误可以在程序实际运行之前尽早捕获。它还使编译器能够使用静态数据类型来优化存储需求，以及针对该值的运算选择算法。使用静态类型，可以执行显式强制转换。变量仍然可以定义为对象，然后在运行时强制转换为不同的数据类型。但这需要额外的数据装箱/拆箱。在 C# 4.0 中，关键字列表新增了一种 **dynamic** 数据类型。

### 动态数据类型

你第一次读到 **dynamic** 数据类型是在第 2 章。使用 **dynamic** 关键字定义的对象可以存储任何内容。在大多数情况下，它的行为类似于 **object**。在编译时，类型为 **dynamic** 的元素被假定支持任何操作。示例 11-33 声明了几个 **dynamic** 类型的变量。在使用它们之前不需要拆箱或强制转换。如示例 11-33 所示，四个变量被定义为 dynamic。每个变量都用差异很大的数据进行初始化。打印内容时不需要进行特殊强制转换。

### 示例 11-33

```csharp
dynamic intValue = 1000;
dynamic stringValue = "C#";
dynamic decimalValue = 23.45m;
dynamic aDate = System.DateTime.Today;
Console.WriteLine("{0}    {1}    {2}    {3}",
    intValue, stringValue, decimalValue, aDate);
```

使用动态数据类型时，类型检查在运行时进行。上述程序语句产生的输出为

```text
1000    C#    23.45    8/16/2010 12:00:00 AM
```

更有意思的是，一旦定义为 **dynamic**，该内存位置可以保存任何值。请注意，在示例 11-34 中定义了一个 dynamic 内存位置，但随后将四种不同数据类型的值赋给了该内存位置。

### 示例 11-34

```csharp
dynamic aValue;
aValue = 1001;
aValue++;
Console.WriteLine("aValue = int: " + aValue);
aValue = "C#";
Console.WriteLine("aValue = string: " + aValue);
aValue = 23.45m;
Console.WriteLine("aValue = decimal: " + aValue);
aValue = System.DateTime.Today;
Console.WriteLine("aValue = Date: " + aValue);
```

上述程序语句产生的输出为

aValue = int: 1001
aValue = string: C#
aValue = decimal: 23.45
aValue = Date: 8/16/2010 12:00:00 AM

查看示例 11-34 时，请注意能够使用该 dynamic 内存位置执行算术运算。aValue 被递增。该内存位置既存储整数值，也存储浮点值，并且能够引用 string 和 object 类型。所有这一切都在没有任何强制转换或装箱/拆箱的情况下完成。动态类型可用于方法参数或方法返回类型。它们提供了编码的自由和速度，但仍应谨慎使用。强类型语言相对于动态语言的主要优势之一是会在编译时进行广泛的错误检查，从而可以尽早发现缺陷。使用动态类型时，这会延迟到运行时。

### var 数据类型

另一个关键字 **var** 可能会被误认为是 **dynamic** 类型。乍一看，它似乎在执行 dynamic 所做的相同事情。它使开发人员能够将特定的数据类型与一组位关联起来。但 **var** 不同。它用于隐式类型化变量。在方法内部声明的变量可以使用 **var** 关键字声明。以下声明在功能上等效。

```
int someValue = 1000;
var someValue = 1000;
```

第一个声明 `int someValue = 1000;` 由程序员显式指定类型。第二个声明 `var someValue = 1000;` 由编译器隐式指定类型。它被称为隐式类型的局部变量，因为编译器会确定类型。该关键字指示编译器从初始化语句右侧的表达式推断变量的类型。你不需要编写 `dynamic aValue = System.DateTime.Today`，而应编写

`var aValue = System.DateTime.Today;`

**dynamic** 与 **var** 的主要区别之一是，var 数据项必须在声明时初始化。编译器根据初始化值确定内存位置的类型。如果尝试声明没有初始化值的 **var** 类型，将收到编译器错误：“隐式类型的局部变量必须初始化。” **dynamic** 则不是这样。如示例 11-34 所示，使用 **dynamic**，你可以声明一个 dynamic 内存位置，并在稍后将值与它关联。

![](img/e33ae760e23d89eac66541252ad65de8_726_0.png)

动态类型和 **dynamic** 关键字与 Microsoft 新的动态语言运行时（DLR）环境紧密相关——这是 .NET Framework 的一项新功能。DLR 构建在公共语言运行时（CLR）之上。DLR 为平台增加了一组专为动态语言需求设计的服务，包括支持轻松生成快速的动态代码。

你将在第 14 章再次看到 **var** 的使用。它常与 LINQ 查询操作一起使用。

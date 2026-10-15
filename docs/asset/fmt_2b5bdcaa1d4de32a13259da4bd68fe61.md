
由于匿名类型在定义上没有名称，因此不可能将局部变量显式声明为匿名类型。相反，局部变量的类型被替换为 `var`。但这绝不意味着隐式类型变量是未类型的。恰恰相反，它们被完全类型化为所赋值的值的类型。如果隐式类型变量被赋值为匿名类型，那么该局部变量声明底层的 CIL 代码将是编译器生成的类型。类似地，如果隐式类型变量被赋值为字符串，其在底层 CIL 中的数据类型也将是字符串。实际上，对于赋值不是匿名类型（如字符串）的隐式类型变量，与显式声明为 `string` 类型的情况相比，生成的 CIL 代码没有差异。如果声明语句是 `string text = "This is a test of the…"`，其生成的 CIL 代码将与隐式类型声明 `var text = "This is a test of the…"` 完全相同。编译器根据所赋的表达式来确定隐式类型变量的数据类型。在带初始化器的显式类型局部变量（`string s = "hello";`）中，编译器首先根据左侧的声明类型确定 `s` 的类型，然后分析右侧表达式，并验证右侧表达式可赋值给该类型。在隐式类型局部变量中，这个过程在某种意义上反转了。首先分析右侧表达式以确定其类型，然后逻辑上用该类型替换 `var`。

尽管 C# 没有为匿名类型提供名称，但它仍然是强类型的。例如，该类型的属性是完全可访问的。在清单14.1中，`patent1.Title` 和 `patent2.YearOfPublication` 在 `Console.WriteLine` 语句中被调用。任何尝试调用不存在的成员都会导致编译器错误。即使 Visual Studio 等 IDE 中的 IntelliSense 也能与匿名类型配合工作。

你应该谨慎使用隐式类型变量声明。显然，对于匿名类型，不可能指定数据类型，必须使用 `var`。然而，在数据类型不是匿名类型的情况下，通常更倾向于使用显式数据类型 `type`。一般情况下，你应专注于使代码的语义更具可读性，同时利用编译器验证生成的变量是否为你期望的类型。要使用隐式类型的局部变量实现这一点，仅在分配给隐式类型变量的类型完全显而易见时才使用它们。例如，在 `var items = new Dictionary<string, List<Account>>();` 中，结果代码更简洁且可读。相比之下，当类型不明显时，例如方法返回值被赋值时，开发人员应优先使用显式的变量类型声明，如下所示：

```
Dictionary<string, List<Account>> dictionary = GetAccounts();
```

## NOTE

隐式类型变量通常应保留用于匿名类型声明，而不是在编译时已知数据类型时随意使用，除非分配给变量的类型完全显而易见。

## Language Contrast: C++/Visual Basic/JavaScript—void*, Variant, and var

隐式类型变量不等同于 C++ 中的 `void*`、Visual Basic 中的 `Variant` 或 JavaScript 中的 `var`。在每种情况下，变量声明都不是很严格，因为变量可以被赋予任意类型，就像你在 C# 中使用类型为 `object` 的变量声明时所能做的那样。相比之下，`var` 是由编译器明确类型的；一旦在声明时确定，类型就不能更改，并且类型检查和成员调用在编译时得到验证。

## More about Anonymous Types and Implicit Local Variables

在 Listing 14.1 中，匿名类型的成员名称通过将值赋给 `patent1` 和 `patent2` 的名称来显式标识（例如，`Title = "Phonograph"`）。然而，如果分配的值是属性或字段调用，则名称可能会默认为字段或属性的名称，而不是显式指定值。例如，`patent3` 是使用名为“Title”的属性定义的，而不是分配给显式名称。如 Output 14.1 所示，结果属性名称由编译器确定，以匹配从中检索值的属性。

`patent1` 和 `patent2` 具有相同的属性名称和相同的数据类型。因此，C# 编译器为这两个匿名声明生成一个数据类型。然而，`patent3` 迫使编译器创建第二个匿名类型，因为专利年份的属性名称与 `patent1` 和 `patent2` 中的不同。此外，如果 `patent1` 和 `patent2` 之间交换属性的顺序，这两个匿名类型也不会类型兼容。换句话说，在同一程序集中使两个匿名类型类型兼容的要求是属性名称、数据类型和属性顺序的匹配。如果满足这些标准，即使它们出现在不同的方法或类中，类型也是兼容的。Listing 14.2 演示了类型不兼容的情况。

### LISTING 14.2: Type Safety and Immutability of Anonymous Types

```
class Program
{
    static void Main()
    {
        var patent1 =
            new
            {
                Title = "Bifocals",
                YearOfPublication = "1784"
            };

        var patent2 =
            new
            {
                YearOfPublication = "1877",
                Title = "Phonograph"
            };

        var patent3 =
            new
            {
                patent1.Title,
                Year = patent1.YearOfPublication
            };

        // ERROR: Cannot implicitly convert type
        //        'AnonymousType#1' to 'AnonymousType#2'
        patent1 = patent2;
        // ERROR: Cannot implicitly convert type
        //        'AnonymousType#3' to 'AnonymousType#2'
        patent1 = patent3;

        // ERROR: Property or indexer 'AnonymousType#1.Title'
        //        cannot be assigned to -- it is read-only
        patent1.Title = "Swiss Cheese";
    }
}
```

前两个编译器错误的结果断言这些类型不兼容，因此它们不会成功相互转换。

第三个编译器错误是由 `Title` 属性的重新赋值引起的。匿名类型是不可变的，因此在实例化后更改匿名类型的属性是编译器错误。

尽管 Listing 14.2 中未显示，但不可能声明具有隐式数据类型参数（`var`）的方法。因此，匿名类型的实例只能以两种方式在创建它们的范围外传递。首先，如果方法参数的类型为 `object`，则匿名类型实例可以传递到方法之外，因为匿名类型会隐式转换。第二种方法是使用方法类型推断，即匿名类型实例作为编译器可以成功推断的方法类型参数传递。因此，使用 `Function(patent1)` 调用 `void Method<T>(T parameter)` 将会成功，尽管 `Function()` 中对 `parameter` 的可用操作仅限于 `object` 支持的操作。

尽管 C# 允许像 Listing 14.1 中所示的匿名类型，但通常不建议你以这种方式定义它们。匿名类型为 C# 3.0 对投影的支持提供了关键功能，例如连接/关联集合，我们将在本章后面讨论。然而，通常你应将匿名类型定义保留在需要它们的情况下，例如从多个类型聚合数据。

## ADVANCED TOPIC

## Anonymous Type Generation

即使 `Console.WriteLine()` 的实现是调用 `ToString()`，请注意在 Listing 14.1 中，`Console.WriteLine()` 的输出不是默认的 `ToString()`，后者会输出完全限定数据类型名称。相反，输出是每个匿名类型属性的 `PropertyName = value` 对列表。这是因为编译器在匿名类型代码生成中重写了 `ToString()`，从而将 `ToString()` 输出格式化为所示形式。同样，生成的类型包括对 `Equals()` 和 `GetHashCode()` 的重写实现。

`ToString()` 的实现本身就是一个重要原因，即属性顺序的变化会导致生成新的数据类型。如果两个单独的匿名类型，可能在完全不同的类型甚至命名空间中被统一，然后更改属性顺序，一个实现上属性顺序的变化会对另一个的 `ToString()` 结果产生明显且可能不可接受的影响。此外，在执行时，可以通过反射查看类型并检查类型上的成员——甚至可以动态调用其中一个成员（在运行时确定要调用哪个成员）。两个看似相同的类型上成员顺序的变化可能会触发意外的结果。为了避免这个问题，C# 设计者决定生成两种不同的类型。

## Collection Initializers

添加到 C# 3.0 中的另一个功能是集合初始化器。集合初始化器允许程序员在实例化时以类似于数组声明的方式构造具有初始成员集的集合。在集合初始化可用之前，元素必须在集合实例化后显式添加到集合中——使用类似 `System.Collections.Generic.ICollection<T>` 的 `Add()` 方法。通过集合初始化，`Add()` 调用由 C# 编译器生成，而不是由开发人员显式编码。Listing 14.3 显示了如何使用集合初始化器初始化集合。

### LISTING 14.3: Collection Initialization

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<string> sevenWorldBlunders;
        sevenWorldBlunders = new List<string>()
        {
            // Quotes from Ghandi
            "Wealth without work",
            "Pleasure without conscience",
            "Knowledge without character",
            "Commerce without morality",
            "Science without humanity",
            "Worship without sacrifice",
            "Politics without principle"
        };

        Print(sevenWorldBlunders);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

语法不仅类似于数组初始化，也类似于对象初始化器，后者在构造函数后使用大括号。如果构造函数中未传递参数，则数据类型后的括号是可选的（与对象初始化器相同）。

集合初始化器要成功编译，需要满足一些基本要求。理想情况下，集合初始化器所应用的集合类型应为实现 `System.Collections.Generic.ICollection<T>` 的类型。这确保集合包含编译器生成的代码可以调用的 `Add()`。然而，也存在一种宽松的版本要求，只需在实现 `IEnumerable<T>` 的类型上存在一个或多个 `Add()` 方法即可，这些方法可以作为扩展方法（C# 6.0）或实例方法存在——即使集合未实现 `ICollection<T>`。`Add()` 方法需要采用与集合初始化器中指定的值兼容的参数。

对于字典，集合初始化器语法稍微复杂一些，因为字典中的每个元素都需要键和值。该语法如清单14.4所示。

### LISTING 14.4: 初始化字典

```csharp
using System;
using System.Collections.Generic;
#if !PRECSHARP6
    // C# 6.0 or Later
    Dictionary<string, ConsoleColor> colorMap =
        new Dictionary<string, ConsoleColor>
        {
            ["Error"] = ConsoleColor.Red,
            ["Warning"] = ConsoleColor.Yellow,
            ["Information"] = ConsoleColor.Green,
            ["Verbose"] = ConsoleColor.White
        };
#else
    // Before C# 6.0
    Dictionary<string, ConsoleColor> colorMap =
        new Dictionary<string, ConsoleColor>
        {
            { "Error", ConsoleColor.Red },
            { "Warning", ConsoleColor.Yellow },
            { "Information", ConsoleColor.Green },
            { "Verbose", ConsoleColor.White}
        };
#endif
```

此清单实际包含两个不同版本的初始化。第一个演示了C# 6.0引入的新语法，它通过允许赋值运算符来表达哪个值与哪个键关联，从而说明名称/值对的意图。第二种语法（在C# 6.0或更高版本中仍然有效）使用花括号将名称和值配对在一起。

允许在不支持 `ICollection<T>` 的集合上使用初始化器之所以重要，有两个原因。首先，大多数集合（实现 `IEnumerable<T>` 的类型）并不实现 `ICollection<T>`，这大大降低了集合初始化器的实用性。其次，根据方法名和签名与集合初始化器项的兼容性进行匹配，使得初始化到集合中的项更具多样性。例如，只要有一个 `Add()` 方法的签名与参数 `a` 兼容，并且有第二个 `Add()` 方法的签名与 `b`、`c` 兼容，初始化器现在就可以支持 `new DataStore(){ a, {b, c}}`。

请注意，不能为匿名类型提供集合初始化器，因为集合初始化器需要构造函数调用，而无法命名构造函数。解决办法是定义一个方法，例如 `static List<T> CreateList<T>(T t) { return new List<T>(); }`。方法类型推断允许隐式推断类型参数，而不是显式指定，因此这种方法可以成功创建匿名类型的集合。

初始化匿名类型集合的另一种方法是使用数组初始化器。由于无法在构造函数中指定数据类型，数组初始化语法允许使用 `new[]` 进行匿名数组初始化（见清单14.5）。

### LISTING 14.5: 初始化匿名类型数组

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        var worldCup2006Finalists = new[]
        {
            new
            {
                TeamName = "France",
                Players = new string[]
                {
                    "Fabien Barthez", "Gregory Coupet",
                    "Mickael Landreau", "Eric Abidal",
                    // ...
                }
            },
            new
            {
                TeamName = "Italy",
                Players = new string[]
                {
                    "Gianluigi Buffon", "Angelo Peruzzi",
                    "Marco Amelia", "Cristian Zaccardo",
                    // ...
                }
            }
        };

        Print(worldCup2006Finalists);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

结果变量是匿名类型项的数组，由于是数组，该项的类型必须是同类型的。

## 类成为集合的条件：`IEnumerable<T>`

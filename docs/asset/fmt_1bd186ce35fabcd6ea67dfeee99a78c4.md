
```
int? x = GetNullableType();
if (x == null)
{
    WriteLine("x is null");
}
else if (x < 0)
{
    WriteLine("x is smaller than 0");
}
```

既然你已经了解了 `Nullable<T>` 是如何定义的，让我们来讨论使用可空类型。可空类型也可以与算术运算符一起使用。变量 `x3` 是变量 `x1` 和 `x2` 的总和。如果任何可空类型的值为 null，则结果也为 null：

```
int? x1 = GetNullableType();
int? x2 = GetNullableType();
int? x3 = x1 + x2;
```

> **注意** 这里调用的 `GetNullableType` 方法只是任何返回可空 int 的方法的占位符。为了测试，你可以实现它，让它简单地返回 null 或返回任何整数值。

非可空类型可以转换为可空类型。从非可空类型转换为可空类型时，可以进行隐式转换，不需要强制转换。这种转换总是成功：

```
int y1 = 4;
int? x1 = y1;
```

在相反的情况下，从可空类型转换为非可空类型可能会失败。如果可空类型的值为 null，并且将该 null 值赋给非可空类型，则会抛出 `InvalidOperationException` 类型的异常。这就是为什么需要强制转换运算符来执行显式转换：

```
int? x1 = GetNullableType();
int y1 = (int)x1;
```

除了进行显式转换之外，还可以使用合并运算符将可空类型转换为非可空类型。合并运算符使用 `??` 语法，在可空类型的值为 null 的情况下为转换定义默认值。这里，如果 `x1` 为 null，`y1` 将获得值 0：

```
int? x1 = GetNullableType();
int y1 = x1 ?? 0;
```

### 泛型方法

除了定义泛型类之外，还可以定义泛型方法。对于泛型方法，泛型类型是在方法声明时定义的。泛型方法可以定义在非泛型类中。

方法 `Swap<T>` 将 `T` 定义为泛型类型，用于两个参数和一个变量 `temp`：

```
void Swap<T>(ref T x, ref T y)
{
    T temp;
    temp = x;
    x = y;
    y = temp;
}
```

可以通过在方法调用时指定泛型类型来调用泛型方法：

```
int i = 4;
int j = 5;
Swap<int>(ref i, ref j);
```

然而，由于 C# 编译器可以通过调用 `Swap` 方法获取参数的类型，因此在方法调用时不需要指定泛型类型。泛型方法可以像非泛型方法一样简单地调用：

```
int i = 4;
int j = 5;
Swap(ref i, ref j);
```

#### 泛型方法示例

此示例使用泛型方法来累加集合的所有元素。为了展示泛型方法的特性，使用了以下包含 `Name` 和 `Balance` 属性的 `Account` 类（代码文件 `GenericMethods/Account.cs`）：

> **注意** 使用 .NET Core 时，此示例需要引用 NuGet 包 `System.Collections`。

```
public class Account
{
    public string Name { get; }
    public decimal Balance { get; private set; }
    public Account(string name, Decimal balance)
    {
        Name = name;
        Balance = balance;
    }
}
```

需要累加余额的所有账户都被添加到一个类型为 `List<Account>` 的账户列表中（代码文件 `GenericMethods/Program.cs`）：

```
var accounts = new List<Account>
{
    new Account("Christian", 1500),
    new Account("Stephanie", 2200),
    new Account("Angela", 1800),
    new Account("Matthias", 2400)
};
```

累加所有 `Account` 对象的传统方式是使用 `foreach` 语句循环遍历它们，如下所示。由于 `foreach` 语句使用 `IEnumerable` 接口来迭代集合的元素，`AccumulateSimple` 方法的参数类型为 `IEnumerable`。`foreach` 语句适用于任何实现 `IEnumerable` 的对象。这样，`AccumulateSimple` 方法可以用于所有实现了 `IEnumerable<Account>` 接口的集合类。在这个方法的实现中，直接访问 `Account` 对象的 `Balance` 属性（代码文件 `GenericMethods/Algorithms.cs`）：

```
public static class Algorithms
{
    public static decimal AccumulateSimple(IEnumerable<Account> source)
    {
        decimal sum = 0;
        foreach (Account a in source)
        {
            sum += a.Balance;
        }
        return sum;
    }
}
```

`AccumulateSimple` 方法这样调用：

```
decimal amount = Algorithms.AccumulateSimple(accounts);
```

#### 带约束的泛型方法

第一个实现的问题在于它只适用于 `Account` 对象。使用泛型方法可以避免这个问题。

`Accumulate` 方法的第二个版本接受任何实现了 `IAccount` 接口的类型。正如你之前看到的泛型类，你可以使用 `where` 子句限制泛型类型。你可以将用于泛型类的相同子句用于泛型方法。`Accumulate` 方法的参数被改为 `IEnumerable<T>`，这是一个由泛型集合类实现的泛型接口（代码文件 `GenericMethods/Algorithms.cs`）：

```
public static decimal Accumulate<TAccount>(IEnumerable<TAccount> source)
        where TAccount : IAccount
{
    decimal sum = 0;

    foreach (TAccount a in source)
    {
        sum += a.Balance;
    }
    return sum;
}
```

`Account` 类现在被重构为实现 `IAccount` 接口（代码文件 `GenericMethods/Account.cs`）：

```
public class Account : IAccount
{
    //...
}
```

`IAccount` 接口定义了只读属性 `Balance` 和 `Name`（代码文件 `GenericMethods/IAccount.cs`）：

```
public interface IAccount
{
    decimal Balance { get; }
    string Name { get; }
}
```

新的 `Accumulate` 方法可以通过定义 `Account` 来调用

你可以重载泛型方法，以便为特定类型定义专用版本。对于带有泛型参数的方法也是如此。`Foo` 方法定义了四个版本。第一个版本接受一个泛型参数；第二个是针对 `int` 参数的专用版本。第三个 `Foo` 方法接受两个泛型参数，第四个是第三个的专用版本，其第一个参数类型为 `int`。在编译期间，会选择最佳匹配。如果传入的是 `int`，则会选择带有 `int` 参数的方法。对于任何其他参数类型，编译器会选择该方法的泛型版本（代码文件 `Specialization/Program.cs`）：

```
public class MethodOverloads
{
    public void Foo<T>(T obj)
    {
        WriteLine($"Foo<T>(T obj), obj type: {obj.GetType().Name}");
    }

    public void Foo(int x)
    {
        WriteLine("Foo(int x)");
    }

    public void Foo<T1, T2>(T1 obj1, T2 obj2)
    {
        WriteLine($"Foo<T1, T2>(T1 obj1, T2 obj2); {obj1.GetType().Name}" +
            $"{obj2.GetType().Name}");
    }

    public void Foo<T>(int obj1, T obj2)
    {
        WriteLine($"Foo<T>(int obj1, T obj2); {obj2.GetType().Name}");
    }

    public void Bar<T>(T obj)
    {
        Foo(obj);
    }
}
```

现在可以使用任何参数类型调用 `Foo` 方法。示例代码传递 `int` 和 `string` 值来调用全部四个 `Foo` 方法：

```
static void Main()
{
    var test = new MethodOverloads();
    test.Foo(33);
    test.Foo("abc");
    test.Foo("abc", 42);
    test.Foo(33,"abc");
}
```

运行该程序，你可以通过输出看到选择的是最佳匹配的方法：

```
Foo(int x)
Foo<T>(T obj), obj type: String
```

### 7 数组和元组

#### 本章内容

- 简单数组

- 多维数组

- 交错数组

- `Array` 类

- 数组作为参数

- 枚举

- 元组

- 结构比较

#### Wrox.com 本章代码下载

本章的 wrox.com 代码下载位于 [`www.wrox.com/go/professionalcsharp6`](www.wrox.com/go/professionalcsharp6) 的 Download Code 选项卡。本章代码分为以下主要示例：

- SimpleArrays

- SortingSample

- ArraySegment

- YieldsSample

- TuplesSample

- StructuralComparison

#### 多个相同类型和不同类型的对象

如果你需要处理多个相同类型的对象，可以使用集合（见第 11 章“集合”）和数组。C# 有特殊的表示法来声明、初始化和使用数组。在幕后，`Array` 类会发挥作用，它提供了多种方法来排序和过滤数组中的元素。使用枚举器，你可以遍历数组中的所有元素。

要使用多个不同类型的对象，可以使用 `Tuple` 类型。有关该类型的详细信息，请参阅本章后面的“元组”一节。

#### 简单数组

如果你需要处理多个相同类型的对象，可以使用数组。数组是一种数据结构，包含若干个相同类型的元素。

#### 数组声明

声明数组时，先定义数组内元素的类型，后跟空方括号和变量名。例如，包含整数元素的数组声明如下：

```
int[] myArray;
```

#### 数组初始化

声明数组后，必须分配内存来容纳数组的所有元素。数组是引用类型，因此必须在堆上分配内存。你可以使用 `new` 运算符，并指定类型和数组中的元素数量来初始化数组变量。这里，你需要指定数组的大小：

```
myArray = new int[4];
```

> 注意 值类型和引用类型在第 3 章“对象和类型”中介绍。

通过这种声明和初始化，变量 `myArray` 引用了托管堆上分配的四个整数值（见图 7.1）。

![](img/3d365b72b289213a91ade7eb366b8f35_271_0.png)

> 注意 数组的大小指定后，如果不复制所有元素，就无法调整其大小。如果你事先不知道数组中应包含多少个元素，可以使用集合（见第 11 章）。

除了使用单独的行来声明和初始化数组外，你也可以在一行中完成：

```
int[] myArray = new int[4];
```

你还可以使用数组初始化器为每个数组元素赋值。数组初始化器只能在声明数组变量时使用，不能在数组声明之后使用：

```
int[] myArray = new int[4] {4, 7, 11, 2};
```

如果使用花括号初始化数组，你也可以省略数组的大小，因为编译器可以统计元素的数量：

```
int[] myArray = new int[] {4, 7, 11, 2};
```

利用 C# 编译器，还有一种更简短的写法。使用花括号，你可以编写数组的声明和初始化。编译器生成的代码与之前的结果相同：

```
int[] myArray = {4, 7, 11, 2};
```

#### 访问数组元素

数组声明并初始化后，你可以使用索引器访问数组元素。数组仅支持具有整数参数的索引器。

使用索引器时，传入元素编号以访问数组。索引器始终从 0 开始表示第一个元素。因此，你可以传给索引器的最大数字是元素数量减一，因为索引从零开始。在下面的示例中，数组 `myArray` 被声明并初始化为四个整数值。可以使用索引器值 0、1、2 和 3 访问这些元素。

```
int[] myArray = new int[] {4, 7, 11, 2};
int v1 = myArray[0];    // 读取第一个元素
int v2 = myArray[1];    // 读取第二个元素
myArray[3] = 44;        // 更改第四个元素
```

> 注意 如果使用了超出数组长度的错误索引器值，会抛出 `IndexOutOfRangeException` 类型的异常。

如果你不知道数组中的元素数量，可以使用 `Length` 属性，如下面的 `for` 语句所示：

```
for (int i = 0; i < myArray.Length; i++)
{
    WriteLine(myArray[i]);
}
```

除了使用 `for` 语句遍历数组的所有元素外，你也可以使用 `foreach` 语句：

```
foreach (var val in myArray)
{
    WriteLine(val);
}
```

> 注意 `foreach` 语句使用 `IEnumerable` 和 `IEnumerator` 接口，并从第一个索引遍历到最后一个索引。本章后面会详细讨论这一点。

#### 使用引用类型

除了能够声明预定义类型的数组外，你还可以声明自定义类型的数组。让我们从下面的 `Person` 类开始，它使用自动实现的属性 `FirstName` 和 `LastName`，并重写了 `Object` 类的 `ToString` 方法（代码文件 `SimpleArrays/Person.cs`）：

```csharp
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public override string ToString() => $"{FirstName} {LastName}";
}
```

声明包含两个 `Person` 元素的数组与声明 `int` 数组类似：

```csharp
Person[] myPersons = new Person[2];
```

但是，请注意，如果数组中的元素是引用类型，则必须为每个数组元素分配内存。如果你使用数组中尚未分配内存的项，则会抛出 `NullReferenceException`。

> 注意 有关错误和异常的信息，请参阅第 14 章“错误和异常”。

你可以通过从 0 开始的索引器为数组的每个元素分配内存：

```csharp
myPersons[0] = new Person { FirstName="Ayrton", LastName="Senna" };
myPersons[1] = new Person { FirstName="Michael", LastName="Schumacher" };
```

图 7.2 显示了托管堆中带有 `Person` 数组的对象。`myPersons` 是存储在栈上的一个变量。该变量引用了一个存储在托管堆上的 `Person` 元素数组。该数组有足够的空间容纳两个引用。数组中的每一项都引用一个也存储在托管堆上的 `Person` 对象。

![](img/3d365b72b289213a91ade7eb366b8f35_274_0.png)

**图 7.2**

与 `int` 类型类似，你也可以在自定义类型上使用数组初始化器：

```
Person[] myPersons2 =
{
    new Person { FirstName="Ayrton", LastName="Senna" },
    new Person { FirstName="Michael", LastName="Schumacher" }
};
```

### 多维数组

普通数组（也称为一维数组）通过单个整数进行索引。多维数组通过两个或多个整数进行索引。

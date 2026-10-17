
```csharp
abstract class Element { }

class Element<T> : Element { }

class BasicElement<T> : Element<T> { }

class Int32Element : BasicElement<int> { }
```

在此示例中，`Element<T>` 从 `Element` 派生，它是一个开放类型。`BasicElement<T>` 从 `Element<T>` 派生，它也是一个开放类型。`Int32Element` 是一个构造类型，因为它从构造类型 `BasicElement<int>` 派生。

然而，派生类可以为其基类的部分类型参数提供类型实参，在这种情况下，它是一个开放构造类型。可以将开放构造类型视为介于开放类型和封闭类型之间；也就是说，它已经为至少一个类型参数提供了实参，但同时也仍有至少一个类型参数需要提供实参才能成为构造类型。

将清单 11.9 中的示例扩展，创建一个具有两个类型参数 `T` 和 `K` 的开放类型 `Element`，清单 11.10 展示了创建开放构造类型的不同可能性。

### 继承自开放构造类

```csharp
class Element<T, K> { }

class Element<T> : Element<T, int> { }

class Element2<K> : Element<string, K> { }
```

如果开放构造类型指定了约束，则派生类型必须提供符合这些约束的类型实参。这可以通过自身指定约束来实现。子类上的约束可以与基类应用的约束相同，也可以是这些约束的超集。清单 11.11 展示了从一个带约束的开放构造类继承的示例。

### 继承自带约束的开放构造类

```csharp
class ConstrainedElement<T>
    where T : IComparable<T>, new()

class ConstrainedElement1<T> : ConstrainedElement<T>
    where T : IComparable<T>, new()
```

最后，如果泛型类实现了一个接口，则该类的所有实例都可以转换为该接口。

## 结合泛型与数组

在第 9 课时中，你了解到所有下界为零的一维数组都自动实现 `IList<T>`。因此，你可以创建一个泛型方法来遍历 `IList<T>` 的内容，该方法适用于任何集合类型（因为它们都实现 `IList<T>`）以及任何一维数组。

清单 11.12 展示了此类泛型方法的一个示例。

### 使用泛型方法打印集合项

```csharp
public static class Program
{
    public static void PrintCollection<T>(IList<T> collection)
    {
        StringBuilder builder = new StringBuilder();
        foreach(var item in collection)
        {
            builder.AppendFormat("{0} ", item);
        }
        Console.WriteLine(builder.ToString());
    }
}
```

```csharp
public static void Main()
{
    int[] array = {0, 2, 4, 6, 8};
    List<int> list = new List<int>() { 1, 3, 5, 7, 9};
    PrintCollection(array);
    PrintCollection(list);

    string[] array2 = { "hello", "world" };
    List<string> list2 = new List<string>() { "now", "is", "the", "time" };
    PrintCollection(array2);
    PrintCollection(list2);
}
```

## 泛型接口中的方差

类型方差指的是使用不同于最初指定类型的类型的能力。**协变**允许你使用比指定类型更派生的类型，而**逆变**允许你使用比指定类型更基础（派生程度更低）的类型。C# 支持返回类型的协变和参数的逆变。

C# 中的泛型集合是**不变**的，这意味着你必须使用与指定形式类型完全匹配的类型。因此，不可能在预期是基础类型的位置替换为包含更派生类型的集合。例如，如果你有一个汽车集合，你不能将其视为警车集合，因为它可能包含一辆不是警车的汽车。同样，你也不能将其视为车辆集合，因为你可以将一辆卡车（显然不是汽车）放入车辆集合中，但不能放入汽车集合中。

> **实现泛型方变接口的类**
>
> 实现泛型方变接口的类始终是不变的。

这里真正的实际问题在于集合是可变的。如果你能将集合限制在只读行为子集内，就可以使其具备协变性，从而可以毫无问题地将汽车序列视为车辆序列。

在 C# 中，如果其类型参数被声明为协变或逆变，则该接口是*方变*的。协变和逆变仅当两种类型之间存在引用转换时才适用。这意味着你不能对值类型使用方差。你也不能对 `ref` 或 `out` 参数使用方差。

表 11.2 中列出的几个泛型集合接口支持方差。

| 接口 | 方差 |
| --- | --- |
| IEnumerable<T> | T 是协变的。 |
| IEnumerator<T> | T 是协变的。 |
| IQueryable<T> | T 是协变的。 |
| IGrouping<TKey, TElement> | TKey 和 TElement 是协变的。 |
| IComparer<T> | T 是逆变的。 |
| IEqualityComparer<T> | T 是逆变的。 |
| IComparable<T> | T 是逆变的。 |

## 自己动手试一试

### 探索方差

通过按照以下步骤操作，你可以通过修改清单 11.12 中显示的代码来探索方差是如何工作的。

- 1. 创建一个新的控制台应用程序，并将 `Program.cs` 的内容修改为清单 11.12 所示的样子。
- 2. 使用 Ctrl+F5 运行应用程序，观察输出是否与图 11.3 中显示的内容一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_279_0.png)

**图 11.3**

打印数组的内容

- 3. 修改 `PrintCollection<T>`，使其不再是一个泛型方法，并且集合的类型为 `IEnumerable<object>`。
- 4. 你应该会立即看到图 11.4 中显示的编译器错误。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_279_1.png)

**图 11.4**

编译器错误

- 5. 通过注释掉无效的代码行来修正这两个错误。请记住，方差不适用于值类型，这就是产生编译器错误的原因。
- 6. 再次运行应用程序，观察输出是否与图 11.5 中显示的内容一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_280_0.png)

### 扩展方变泛型接口

编译器不会从继承的接口中推断方差，这要求你显式指定派生接口是否支持方差，如清单 11.13 所示。

#### 清单 11.13 扩展泛型方变接口

```csharp
interface ICovariant<out T>
{
}

interface IInvariant<T> : ICovariant<T>
{
}

interface IExtendedCovariant<out T> : ICovariant<T>
{
}
```

尽管 `IInvariant<T>` 接口和 `IExtendedCovariant<out T>` 接口都扩展了同一个协变接口，但只有 `IExtendedCovariant<out T>` 也是协变的。你可以以相同的方式扩展逆变接口。

如果派生接口是不变的，你也可以在同一个派生接口中扩展协变和逆变接口，如清单 11.14 所示。

#### 清单 11.14 同时扩展协变和逆变接口

```csharp
interface ICovariant<out T>
{
}

interface IContravariant<in T>
{
}

interface IInvariant<T> : IContravariant<T>, ICovariant<T>
{
}
```

但是，如果基接口是开放接口，则不能使用协变接口扩展不变接口，反之亦然，如清单 11.15 所示。

## 创建您自己的变体泛型接口

正如您可以定义自己的泛型接口一样，您也可以使用 `in` 和 `out` 关键字与泛型类型参数来定义您自己的变体泛型接口。

`out` 关键字将泛型类型参数声明为协变的，而 `in` 关键字将泛型类型参数声明为逆变的。接口还可以针对不同类型参数同时支持协变和逆变。与既出现在声明处也出现在调用处的 `ref` 和 `out` 关键字不同，这些关键字仅出现在接口声明中。

**顺便说一下**

**清单 11.15** 以逆变方式扩展不变接口

```csharp
// Generates a compiler error.
interface IInvalidVariance<in T> : ICovariant<T>
{
}
```

## 处理元组

元组是一种具有特定数量和序列值的数据结构。元组通常用于

- 表示一组数据
- 提供对数据集合的简单访问
- 从方法中轻松返回多个值

尽管元组最常见于函数式编程语言（如 F#、Ruby 或 Python），但 .NET 框架提供了几个表示包含从一到七个值的元组的 `Tuple` 类。还有一个 n 元组类，其中 n 是任何大于或等于 8 的值。这个 n 元组类与 1 到 7 元组类略有不同，区别在于元组的第八个组件是另一个 `Tuple` 对象，它定义了剩余的组件。

**试一试**

**处理元组**

要创建一个新的 Tuple<T1, T2> 实例并访问该元组的值，请遵循以下步骤。

1. 创建一个新的控制台应用程序。
2. 在 Program.cs 文件中创建一个返回 Tuple<int, string> 的新方法：

```csharp
public static Tuple<int, string> GenerateTuple()
{
    return Tuple.Create(1, "hello, world");
}
```

3. 在 **Main** 方法中，输入以下代码：

```csharp
var t = GenerateTuple();
Console.WriteLine(t.GetType());
Console.WriteLine("{0}:{1}", t.Item1, t.Item2);
```

4. 按 Ctrl+F5 运行应用程序；您应该看到图 11.6 中显示的内容。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_282_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_282_1.png)

## 总结

在本小时的学习中，您了解了为什么泛型编程很重要，以及它如何使您能够以一种可重用的方式解决问题，无论使用什么数据类型。您学习了类型参数的工作方式，以及如何约束这些类型参数以提供对允许类型的限制。

您学习了如何创建自己的泛型类、接口和方法，包括在非泛型类中创建泛型方法的能力。最后，您学习了如何显式指定泛型接口的类型参数的变异性。

通过创建自己的泛型类型和使用现有的泛型集合进行泛型编程，是一个灵活且强大的概念，它使您只需编写单一实现就能保持类型安全性。

# 问答

问：泛型最常见的用途是什么？

答：泛型最常见于集合类和接口中，尽管您也可以将它们用于自己的类。

问：使用泛型可以防止哪些问题？

答：使用泛型使您可以编写一个类型安全的单一实现，并且不需要装箱或拆箱操作。

问：C# 泛型像 Java 泛型还是 C++ 模板？

答：虽然语法与两者都相似，但实现是不同的。Java 泛型是仅语言层面的构造，泛型类型信息在运行时未知。C++ 模板在编译时展开，为每个模板类型生成额外的代码。

问：什么是类型约束？

答：约束使您能够在编译时对可用于类型参数的类型施加限制，并向编译器保证在任何类型参数上调用的任何运算符或方法都受支持。

问：非泛型类可以包含泛型方法吗？

答：可以，泛型方法可以定义在泛型类或非泛型类中。

问：泛型接口的协变和逆变是什么？

答：变异性被定义为两种泛型类型仅基于其类型参数的已知赋值兼容性而具有赋值兼容性的能力。协变使接口方法能够拥有比类型参数最初指定的更派生的返回类型。逆变使接口方法能够拥有比类型参数最初指定的较少派生的参数类型。

# 练习场

## 测验

1. 使用泛型测试值相等性的正确方法是什么？
2. 什么是类型参数约束？
3. 什么是封闭类型和开放类型？

## 答案

1. 使用泛型测试值相等性的正确方法是应用 where T : IComparable<T> 并使用 CompareTo 方法来执行值相等性测试。
2. 类型参数约束是指当一个泛型参数被用作另一个泛型参数的约束时。
3. 开放类型是一个未为其类型参数提供任何类型参数的泛型类型。封闭类型是一个非开放的泛型类型（即，已为其所有类型参数提供了类型参数）。

## 练习

1. 向 ExifMetadata 结构添加以下方法：

```csharp
private static Nullable<T> QueryMetadata<T>(BitmapMetadata metadata, string query)
where T : struct
{
    Nullable<T> result = new Nullable<T>();

    if (metadata.ContainsQuery(query))
    {
        try
        {
            object queryResult = metadata.GetQuery(query);
            if (queryResult.GetType() == typeof(T))
            {
                result = (T)queryResult;
            }
            else
            {
                try
                {
                    result = (T)Convert.ChangeType(queryResult, typeof(T));
                }
                catch (InvalidCastException)
                {
                    result = null;
                }
                catch (FormatException)
                {
                    result = null;
                }
                catch (OverflowException)
                {
                    result = null;
                }
            }
            catch
            {
                result = null;
            }
        }
    }

    return result;
}
```

用以下代码替换构造函数的内容：

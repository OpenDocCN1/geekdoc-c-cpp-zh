

以及 `System.Enum`——也可能不被用作约束。例如，当编译器遇到列表 12.31 中的类声明时，会生成一个错误。

## 列表 12.31：继承约束不能为 `System.Delegate` 类型

```csharp
// 错误：约束不能是特殊类 'System.Delegate'
public class Publisher<T>
       where T : System.Delegate
{
    public event T Event;
    public void Publish()
    {
        if (Event != null)
        {
            Event(this, new EventArgs());
        }
    }
}
```

所有委托类型都被视为不能指定为类型参数的特殊类。这样做会阻止对 `Event()` 调用的编译时验证，因为在使用 `System.Delegate` 和 `System.MulticastDelegate` 数据类型时，事件触发的签名是未知的。同样的限制也适用于任何枚举类型。

## 构造器约束仅允许用于默认构造器

列表 12.26 包含一个构造器约束，该约束强制为 `TValue` 提供的类型参数必须提供一个公共的无参构造器。没有约束可以强制类型参数提供一个接受其他形式参数的构造器。例如，你可能希望约束 `TValue`，使得为其提供的类型参数必须提供一个接受 `TKey` 类型参数的构造器，但这是不可能的。列表 12.32 展示了无效的代码。

## 列表 12.32：构造器约束只能为默认构造器指定

```csharp
public TValue New(TKey key)
{
// 错误：'TValue'：创建变量类型实例时
// 不能提供参数
TValue newEntity = null;
// newEntity = new TValue(key);
Add(newEntity.Key, newEntity);
return newEntity;
}
```

规避此限制的一种方法是提供一个工厂接口，其中包含一个用于实例化该类型的方法。实现该接口的工厂负责实例化实体，而不是 `EntityDictionary` 本身（参见列表 12.33）。

## 列表 12.33：使用工厂接口替代构造器约束

```csharp
public class EntityBase<TKey>
{
    public EntityBase(TKey key)
    {
        Key = key;
    }
    public TKey Key { get; set; }
}

public class EntityDictionary<TKey, TValue, TFactory> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>
    where TFactory : IEntityFactory<TKey, TValue>, new()
{
    ...
    public TValue New(TKey key)
    {
        TFactory factory = new TFactory();
        TValue newEntity = factory.CreateNew(key);
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    ...
}

public interface IEntityFactory<TKey, TValue>
{
    TValue CreateNew(TKey key);
}
```

像这样的声明允许你将新键传递给接受参数的 `TValue` 工厂方法，而不是被迫依赖默认构造器。它不再对 `TValue` 使用构造器约束，因为 `TFactory` 负责实例化值。（对列表 12.33 中代码的一种修改是缓存工厂方法的引用——如果需要多线程支持，可能利用 `Lazy<T>`。这将使你能够重用工厂方法，而不是每次重新实例化它。）

声明一个类型为 `EntityDictionary<TKey, TValue, TFactory>` 的变量将产生一个类似于列表 12.34 中 `Order` 实体的实体声明。

## 列表 12.34：声明要在 `EntityDictionary<...>` 中使用的实体

```csharp
public class Order : EntityBase<Guid>
{
    public Order(Guid key) :
        base(key)
    {
        // ...
    }
}

public class OrderFactory : IEntityFactory<Guid, Order>
{
    public Order CreateNew(Guid key)
    {
        return new Order(key);
    }
}
```

## 泛型方法

前面，你看到当类型是泛型时，向该类型添加方法是一个相对简单的事情；这样的方法可以使用由该类型声明的泛型类型参数。例如，我们在迄今为止见过的泛型类示例中做了这件事。

泛型方法使用泛型类型参数，这与泛型类型非常相似。它们可以声明在泛型或非泛型类型中。如果声明在泛型类型中，它们的类型参数与其包含的泛型类型的类型参数是不同的。要声明一个泛型方法，你指定泛型类型参数的方式与泛型类型相同：在方法名后立即添加类型参数声明语法，如列表 12.35 中的 `MathEx.Max<T>` 和 `MathEx.Min<T>` 示例所示。

## 列表 12.35：定义泛型方法

```csharp
public static class MathEx
{
    public static T Max<T>(T first, params T[] values)
        where T : IComparable<T>
    {
        T maximum = first;

        foreach (T item in values)
        {
            if (item.CompareTo(maximum) > 0)
            {
                maximum = item;
            }
        }
        return maximum;
    }

    public static T Min<T>(T first, params T[] values)
        where T : IComparable<T>
    {
        T minimum = first;

        foreach (T item in values)
        {
            if (item.CompareTo(minimum) < 0)
            {
                minimum = item;
            }
        }

        return minimum;
    }
}
```

在这个例子中，方法是静态的，尽管 C# 并不要求必须如此。

与泛型类型一样，泛型方法可以包含多个类型参数。元数（类型参数的数量）是方法签名的另一个区分特征。也就是说，只要它们在方法类型参数元数上不同，具有相同名称和相同形式参数类型的两个方法是合法的。

## 泛型方法类型推断

就像在使用泛型类型时，类型参数在类型名称之后提供一样，方法类型参数也在方法类型名称之后提供。用于调用 `Min<T>` 和 `Max<T>` 方法的代码看起来像列表 12.36 中所示的那样。

## 列表 12.36：显式指定类型参数

```csharp
Console.WriteLine(
    MathEx.Max<int>(7, 490));
Console.WriteLine(
    MathEx.Min<string>("R.O.U.S.", "FireSwamp"));
```

列表 12.36 的输出显示在输出 12.4 中。

## 输出 12.4

490
Fireswamp

不出所料，类型参数 `int` 和 `string` 对应于在泛型方法调用中使用的实际类型。然而，指定类型参数是多余的，因为编译器可以根据传递给方法的形式参数推断类型参数。显然，列表 12.36 中 `Max` 的调用者打算类型参数为 `int`，因为两个方法参数都是 `int` 类型。为了避免冗余，在所有编译器能够逻辑推断出你 intended 的类型参数的情况下，你可以从调用中排除类型参数。这种实践的一个例子，即**方法类型推断**，出现在列表 12.37 中。输出显示在输出 12.5 中。

## 列表 12.37：从参数中推断类型参数

```csharp
Console.WriteLine(
    MathEx.Max(7, 490)); // 没有类型参数！
Console.WriteLine(
    MathEx.Min("R.O.U.S", "Fireswamp"));
```

## 输出 12.5

490
Fireswamp

为了使方法类型推断成功，参数的类型必须以这样一种方式与泛型方法的形式参数“匹配”，使得可以推断出所需的类型参数。一个有趣的问题是，当做出矛盾的推断时会发生什么。例如，当你使用 `MathEx.Max(7.0, 490)` 调用 `Max<T>` 方法时，编译器可以从第一个参数推断出类型参数应该是 `double`，并可以从第二个参数推断出类型参数是 `int`，这是一个矛盾。在 C# 2.0 中，这会生成一个错误。更复杂的分析会注意到，由于每个 `int` 都可以转换为 double，因此这个矛盾可以解决，所以 double 是类型参数的最佳选择。C# 3.0 和 C# 4.0 都包含了对方法类型推断算法的改进，允许编译器进行这些更复杂的分析。

在方法类型推断仍然不够复杂以推断出类型参数的情况下，你可以通过在参数上插入类型转换来澄清编译器应使用哪种参数类型进行推断，或者通过放弃类型推断并显式包含类型参数来解决错误。

请注意，方法类型推断算法在进行推断时，只考虑参数、参数的类型以及泛型方法的形式参数类型。在实践中可用于分析的其他因素——例如泛型方法的返回类型、方法返回值被赋值给变量的类型，或方法泛型类型参数的约束——完全不被方法类型推断算法考虑。

## 指定约束

泛型方法的类型参数可以像泛型类型的类型参数一样被约束。例如，你可以限制方法类型参数实现某个接口或可转换为某个类类型。约束在参数列表和方法体之间指定，如列表 12.38 所示。

## 列表 12.38：在泛型方法上指定约束

```csharp
public class ConsoleTreeControl
{
    // 泛型方法 Show<T>
    public static void Show<T>(BinaryTree<T> tree, int indent)
    where T : IComparable<T>
    {
        Console.WriteLine("\n{0}{1}",
            "+ --".PadLeft(5 * indent, ' '),
            tree.Item.ToString());
        if (tree.SubItems.First != null)
            Show(tree.SubItems.First, indent + 1);
        if (tree.SubItems.Second != null)
            Show(tree.SubItems.Second, indent + 1);
    }
}
```

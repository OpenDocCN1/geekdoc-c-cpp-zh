

## OR 条件不受支持

如果为类型参数提供多个接口或类约束，编译器始终假设约束之间为 AND 关系。例如，where T : IComparable<T>, IFormattable 要求同时支持 IComparable<T> 和 IFormattable。无法在约束之间指定 OR 关系。因此，不支持清单 11.30 的等效写法。

### 清单 11.30：不允许使用 OR 关系组合约束

```
public class BinaryTree<T>
    // Error: OR is not supported.
    where T : System.IComparable<T> | System.IFormattable
{
    ...
}
```

支持此功能将阻止编译器在编译时解析调用哪个方法。

## 类型委托和枚举约束无效

已熟悉 C# 1.0 并阅读本章以了解新特性的读者，对委托的概念不会陌生，委托在第 12 章中介绍。另一项不允许的约束是将任何委托类型用作类约束。例如，编译器会对清单 11.31 中的类声明输出错误。

### 清单 11.31：继承约束不能为 System.Delegate 类型

```
// Error: Constraint cannot be special class 'System.Delegate'
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

所有委托类型都被视为特殊类，不能指定为类型参数。这样做将阻止对 Event() 调用的编译时验证，因为使用 System.Delegate 和 System.MulticastDelegate 数据类型时，事件触发的签名未知。任何枚举类型都存在相同的限制。

## 构造函数约束仅允许用于默认构造函数

清单 11.26 包含一个构造函数约束，强制 TValue 支持默认构造函数。没有约束可以强制 TValue 支持除默认构造函数以外的构造函数。例如，仅使用约束无法将 EntityBase 键设为 protected，并且仅在接受 TKey 参数的 TValue 构造函数中设置它。清单 11.32 演示了无效代码。

### 清单 11.32：构造函数约束只能针对默认构造函数指定

```
public TValue New(TKey key)
{
    // Error: 'TValue': Cannot provide arguments
    // when creating an instance of a variable type.
    TValue newEntity = null;
    // newEntity = new TValue(key);
    Add(newEntity.Key, newEntity);
    return newEntity;
}
```

绕过此限制的一种方法是提供一个包含用于实例化类型的方法的工厂接口。实现该接口的工厂负责实例化实体，而不是 EntityDictionary 本身（请参阅清单 11.33）。

### 清单 11.33：使用工厂接口代替构造函数约束

```
public class EntityBase<TKey>
{
    public EntityBase(TKey key)
    {
        Key = key;
    }

    public TKey Key
    {
        get { return _key; }
        set { _key = value; }
    }

    private TKey _key;
}

public class EntityDictionary<TKey, TValue, TFactory> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<T>, IFormattable
where TValue : EntityBase<TKey>
where TFactory : IEntityFactory<TKey, TValue>, new()
{
    ...
    public TValue New(TKey key)
    {
        TValue newEntity = new TFactory().CreateNew(key);
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    ...
}

public interface IEntityFactory<TKey, TValue>
{
    TValue CreateNew(TKey key);
}
...
```

这样的声明允许将新键传递到接受参数的 TValue 构造函数，而不是默认构造函数。它不再对 TValue 使用构造函数约束，因为 TFactory 负责实例化订单，而不是 EntityDictionary<...>。（对清单 11.33 中代码的一种修改是保存工厂的副本。这样您就可以重复使用工厂，而不是每次都重新实例化它。）

为 EntityDictionary<TKey, TValue, TFactory> 类型的变量声明会生成类似于清单 11.34 中 Order 实体的实体声明。

### 清单 11.34：声明要在 EntityDictionary<...> 中使用的实体

```
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

您已经了解，当类是泛型类时，向类添加泛型方法相对简单。您在迄今的泛型类示例中已经这样做过，并且这对静态方法也同样适用。此外，您可以在泛型类中使用泛型类，就像您在之前的 BinaryTree 清单中使用以下代码行所做的那样：

```
public Pair<BinaryTree<T>> SubItems;
```

泛型方法是指即使包含类不是泛型类，或者方法包含不在泛型类类型参数列表中的类型参数时，仍使用泛型的方法。要定义泛型方法，请在方法名称后立即添加类型参数语法，如清单 11.35 中的 MathEx.Max<T> 和 MathEx.Min<T> 示例所示。

### 清单 11.35：定义泛型方法

```
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

当方法需要包含类类型参数列表中未包含的其他类型参数时，您在泛型类上使用相同的语法。在此示例中，方法是静态的，但 C# 不要求这样做。

请注意，泛型方法（如同类一样）可以包含多个类型参数。arity（类型参数的数量）是方法签名的另一个区分特征。

## 类型推断

用于调用 Min<T> 和 Max<T> 方法的代码如清单 11.36 所示。

### 清单 11.36：显式指定类型参数

```
Console.WriteLine(
MathEx.Max<int>(7, 490));
Console.WriteLine(
MathEx.Min<string>("R.O.U.S.", "Fireswamp"));
```

清单 11.36 的输出显示在输出 11.4 中。

### 输出 11.4：

```
490
Fireswamp
```

毫不奇怪，类型参数 int 和 string 对应于泛型方法调用中使用的实际类型。但是，指定类型是多余的，因为编译器可以从传递给方法的参数推断类型。为避免冗余，您可以从调用中排除类型参数。这称为类型推断，示例出现在清单 11.37 中。输出显示在输出 11.5 中。

### 清单 11.37：推断类型参数

```
Console.WriteLine(
MathEx.Max(7, 490));
Console.WriteLine(
MathEx.Min("R.O.U.S.", "Fireswamp"));
```

### 输出 11.5：

```
490
Fireswamp
```

要使类型推断成功，类型必须与方法签名匹配。但是，从 C# 3.0 开始，编译器添加了一项增强功能，只要类型隐式兼容，就可以推断类型参数。例如，使用 MathEx.Max(7.0, 490) 调用 Max<T>() 方法将成功编译。尽管参数不全是相同类型（int 和 double），但它们都将隐式转换为 double，因此方法调用可以编译。您可以通过显式转换或包含类型参数来解决错误。还要注意，您不能仅根据返回类型执行类型推断。允许类型推断需要参数。

## 指定约束

泛型方法还允许指定约束。例如，您可以限制类型参数实现 IComparable<T>。约束在方法标题后立即指定，位于方法块的花括号之前，如清单 11.38 所示。

### 清单 11.38：在泛型方法上指定约束

```
public class ConsoleTreeControl
{
    // Generic method Show<T>
    public static void Show<T>(BinaryTree<T> tree, int indent)
        where T : IComparable<T>
    {
        Console.WriteLine(new string(' ',
            "* -- ".PadLeft(5*indent) + " ",
            tree.Item.ToString()));
        if (tree.SubItems.First != null)
            Show(tree.SubItems.First, indent+1);
        if (tree.SubItems.Second != null)
            Show(tree.SubItems.Second, indent+1);
    }
}
```


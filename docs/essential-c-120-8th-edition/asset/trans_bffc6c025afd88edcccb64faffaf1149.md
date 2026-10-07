
# 第 12 章：泛型

## 约束继承

泛型类型参数及其约束都不会被派生类继承，因为泛型类型参数不是成员。（记住，类继承是派生类拥有基类所有成员的属性。）创建继承自其他泛型的新泛型类型是一种常见做法。在这种情况下，由于派生泛型的类型参数变成了泛型基类的类型数参数，因此这些类型参数必须具有与基类中相同（或更强于）基类约束的约束。感到困惑吗？请参考列表 12.31。

列表 12.31：显式指定的已继承的约束

```sharp
public class EntityBase<T> where T : IComparable<T>
{
    // ...
}

ERROR:
// 类型 'U' 必须转换为 'System.IComparable<U>' 
// 才能作为泛型类型或
// 方法中的参数 'T' 使用
class Entity<U> : EntityBase<U>
{
    //...
}
```

在列表 12.31 中，`EntityBase<T>` 要求由基类指定符 `EntityBase<U>` 为 `T` 提供的参数 `U` 实现 `IComparable<U>`。因此，`Entity<U>` 类需要对 `U` 相同的约束。未这样做会导致编译错误。这种模式增加了程序员对基类类型约束的意识，避免了程序员在类派生类并发现约束但不理解其来源时可能可能的困惑。

我们还没有介绍泛型方法；我们将在本章的晚些部分讨论它们。现在，请先意识到方法可以是泛型的，并且也可以为为其类型参数所提供的类型数参数施加约束。那么，当一个虚泛型方法被继承和重写时，约束是如何处理的？与在泛型类上声明类型参数的情况不同，重写虚泛型方法（或显式接口方法）的约束是隐式继承的，不能再次重述（参见列表 12.32）。

列表 12.32：禁止在虚成员上重复已继承的约束

```sharp
public class EntityBase {
    public virtual void Method<T>(T t)
    where T : IComparable<T>
    {
        // ...
    }
}
public class Order : EntityBase {
    public override void Method<T>(T t)
    // 重写成员上不能重复
    // 约束
    where T : IComparable<T>
    {
        // ...
    }
}
```

在泛型继承的情况下，派生类上的类型参数可以通过不仅添加基类上的约束（必须的），还可以添加其他约束来进一步约束。然而，重写虚泛型方法必须完全符合基类方法定义的约束。额外的约束可能会破坏多态性，因此是不被允许的，重写方法上的类型参数约束是隐含的。

## 高级主题

### 约束的局限性

约束被恰当限制限制以避免无意义的代码。例如，你不能将类类型约束与结构体或类约束结合，或者将 `notnull` 与任一类型的约束结合。此外，你不能指定将继承限制为特殊类型（如 `object`、数组或 `System.ValueType`）的约束。¹¹ 你不能为特定的委托类型（如 `Action`、`Func<T>` 或相关类型）设置约束。

在某些情况下，约束的局限性可能是理想的，但它们仍然不受支持。仅具有要求默认构造函数的能力可能是此类限制之一。以下子节提供了一些不允许的约束的额外示例。

### 不允许运算符约束

所有的泛型都隐式地允许 `==` 和 `!=` 比较，以及到 `object` 的隐式转换，因为一切都是对象。你不能将类型参数约束为实现特定方法或运算符的类型（上述情况除外），除非通过接口类型约束（针对方法）或类类型约束（针对方法和运算符）。由于此原因，泛型 `Add()` 无法正常工作。

列表 12.33：约束表达式无法要求运算符

```sharp
public abstract class Math<T>
{
    public static T Add(T first, T second)
    {
        // 错误：运算符 '+' 无法应用于
        // 类型为 'T' 和 'T' 的操作数
        // return first + second;
    }
}
```

在这种情况下，该方法假设所有可能作为 `T` 类型数参数提供的类型上都存在 `+` 运算符。但没有约束可以阻止你提供一个没有关联加法运算符的类型数参数，否则发生错误。遗憾的是，没有办法在约束内部指定需要加法运算符，除非通过使用实现了加法运算符的类类型约束来实现。

更通用地说，没有方法可以将类型约束为静态方法。

¹¹ `System.Enum` (enum)、`System.Delegate` 和 `System.MulticastDelegate` 从 C# 7.3 开始支持。

### 不支持 OR 逻辑

如果你为类型参数提供多个接口或类约束，编译器始终假设约束之间是 AND 逻辑关系。例如，在 `T : IComparable<T>` 处，支持同时要求 `T` 满足 `IComparable<T>` 和 `IFormattable`。没有方法可以指定约束之间的 OR 关系。因此，等同于列表 12.34 的代码是不支持。

列表 12.34：不支持使用 OR 关系组合约束

```sharp
public class BinaryTree<T>
    // 错误：不支持 OR
    // where T: System.IComparable<T> // System.IFormattable
{
    //...
}
```

支持此功能将防止编译器在编译时解析应调用哪个方法。

## 泛型方法

之前，你看到当类型是泛型时，为类型添加方法是一件相对简单的事；此类方法可以使用该类型声明的类型参数。你已经这样做了，例如在我们目前为止看到的泛型类示例中。

泛型方法使用泛型类型参数，就像泛型类型一样。它们可以在泛型类型或非泛型类型中声明。如果在泛型类型中声明，则它们的类型参数与包含它们的泛型类型的类型参数是不同的。要声明泛型方法，你以以处理泛型类型的方式指定类型参数：在方法名后立即添加类型参数声明语法，如列表 12.35 中的 `MathEx.Max<T>` 和 `MathEx.Min<T>` 示例所示。

在这个示例中，方法是静态的，尽管这不是强制要求的。

列表 12.35：定义泛型方法

```sharp
public static class MathEx {
    public static T Max<T>(T first, params T[] values)
    where T : IComparable<T> {
        T maximum = first;
        foreach(T item in values) {
            if(item.compareTo(maximum) > 0) {
                maximum = item;
            }
        }
        return maximum;
    }

    public static T Min<T>(T first, params T[] values)
    where T : IComparable<T> {
        T minimum = first;
        foreach(T item in values) {
            if(item.compareTo(minimum) < 0) {
                minimum = item;
            }
        }
        return minimum;
    }
}
```

泛型方法和泛型类型一样，可以包含多个类型参数。类型参数的数量（arity）是方法签名的一个额外区分特征。也就是说，只要类型参数的数量不同，两个具有相同名称和形式参数类型的方法是合法的。

## 泛型方法推断

正如在使用泛型类型时类型数提供在类型名之后一样，方法类型数提供在方法名之后。调用 `Min<T>` 和 `Max<T>` 方法的代码如列表 12.36 所示，输出为 12.4。

列表 12.36：显式指定类型参数

```sharp
Console.WriteLine(
  MathEx.Max<int>(7, 490));
Console.WriteLine(
  MathEx.Min<string>("R.O.U.S", "Fireswamp"));
```

# 输出 12.4

```
490
ireswamp
```

并不意外，类型参数 `int` 和 `string` 与泛型方法调用的实际类型。然而，指定类型参数是冗余的，因为编译器可以从传递给方法的形式参数推断出类型参数。为了避免冗余，在编译器能够逻辑推断你预期的类型参数的情况下，可以在调用时排除类型参数。这种被称为**方法类型推断**的做法示例出现在列表 12.37 中，输出为 12.5。

列表 12.37：从参数推断类型参数

```sharp
Console.WriteLine(
  MathEx.Max(7, 490)); // 无类型参数！
Console.WriteLine(
  MathEx.Min("R.O.U.S", "Fireswamp"));
```

# 输出 12.5

```
490
fireswamp
```


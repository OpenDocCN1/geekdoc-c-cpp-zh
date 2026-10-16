
```
foreach (var title in titles.Reverse())
{
    WriteLine(title);
}
WriteLine();
WriteLine("subset");
foreach (var title in titles.Subset(2, 2))
{
    WriteLine(title);
}
```

## 使用 Yield Return 返回枚举器

使用 `yield` 语句，你还可以做更复杂的事情，例如通过 `yield return` 返回枚举器。以下面的井字棋游戏为例，玩家轮流在九个方格中的一个中放入叉号或圆圈。这些移动由 `GameMoves` 类模拟。`Cross` 和 `Circle` 方法是用于创建迭代器类型的迭代器块。变量 `cross` 和 `circle` 在 `GameMoves` 类的构造函数中被设置为 `Cross` 和 `Circle`。通过设置这些字段，方法并未被调用，而是被设置为迭代器块定义的迭代器类型。在 `Cross` 迭代器块中，移动信息被写入控制台，并且移动编号递增。如果移动编号大于 8，迭代以 `yield break` 结束；否则，每次迭代都返回圆形迭代器类型的枚举器对象。`Circle` 迭代器块与 `Cross` 迭代器块非常相似；它只是每次迭代返回叉形迭代器类型（代码文件 `YieldSample/GameMoves.cs`）：

```csharp
public class GameMoves
{
    private IEnumerator _cross;
    private IEnumerator _circle;

    public GameMoves()
    {
        _cross = Cross();
        _circle = Circle();
    }

    private int _move = 0;
    const int MaxMoves = 9;

    public IEnumerator Cross()
    {
        while (true)
        {
            WriteLine($"Cross, move {_move}");
            if (++_move >= MaxMoves)
            {
                yield break;
            }
            yield return _circle;
        }
    }

    public IEnumerator Circle()
    {
        while (true)
        {
            WriteLine($"Circle, move {_move}");
            if (++_move >= MaxMoves)
            {
                yield break;
            }
            yield return _cross;
        }
    }
}
```

在客户端程序中，你可以按如下方式使用 `GameMoves` 类。第一步是通过将枚举器设置为 `game.Cross` 返回的枚举器类型来完成的。在 `while` 循环中，调用 `enumerator.MoveNext`。第一次调用时，会调用 `Cross` 方法，该方法通过 `yield` 语句返回另一个枚举器。返回值可以通过 `Current` 属性访问，并设置为下一个循环的枚举器变量：

```csharp
var game = new GameMoves();
IEnumerator enumerator = game.Cross();
while (enumerator.MoveNext())
{
    enumerator = enumerator.Current as IEnumerator;
}
```

该程序的输出显示了交替移动，直到最后一次移动：

```
Cross, move 0
Circle, move 1
Cross, move 2
Circle, move 3
Cross, move 4
Circle, move 5
Cross, move 6
Circle, move 7
Cross, move 8
```

## 元组

数组组合的是相同类型的对象，而元组可以组合不同类型的对象。元组起源于 F# 等函数式编程语言，在这些语言中经常使用。借助 .NET Framework，所有 .NET 语言都可以使用元组。

.NET Framework 定义了八个泛型 `Tuple` 类和一个充当元组工厂的静态 `Tuple` 类。不同的泛型 `Tuple` 类支持不同数量的元素——例如，`Tuple<T1>` 包含一个元素，`Tuple<T1, T2>` 包含两个元素，依此类推。

`Divide` 方法演示了返回包含两个成员的元组：`Tuple<int, int>`。泛型类的参数定义了成员的类型，这里两个成员都是整数。该元组使用静态 `Tuple` 类的静态 `Create` 方法创建。同样，`Create` 方法的泛型参数定义了所实例化的元组类型。新创建的元组使用 `result` 和 `remainder` 变量初始化，以返回除法结果（代码文件 `TupleSample/Program.cs`）：

```csharp
public static Tuple<int, int> Divide(int dividend, int divisor)
{
    int result = dividend / divisor;
    int remainder = dividend % divisor;

    return Tuple.Create(result, remainder);
}
```

下面的示例演示了如何调用 `Divide` 方法。可以使用 `Item1` 和 `Item2` 属性访问元组的各项：

```csharp
var result = Divide(5, 2);
WriteLine($"result of division: {result.Item1}, remainder: {result.Item2}");
```

如果你需要在一个元组中包含超过八个项，可以使用包含八个参数的 `Tuple` 类定义。最后一个模板参数名为 `TRest`，表示你必须传递一个元组本身。这样，你就可以创建包含任意数量参数的元组。

下面的示例演示了这一功能：

```csharp
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest>
```

这里，最后一个模板参数本身就是一个元组类型，因此你可以创建包含任意数量项的元组：

```csharp
var tuple = Tuple.Create<string, string, string, int, int, int, double,
    Tuple<int, int>>("Stephanie", "Alina", "Nagel", 2009, 6, 2, 1.37,
    Tuple.Create<int, int>(52, 3490));
```

## 结构化比较

数组和元组都实现了 `IStructuralEquatable` 和 `IStructuralComparable` 接口。这些接口不仅比较引用，还比较内容。这些接口是显式实现的，因此在使用时必须将数组和元组强制转换为这些接口。`IStructuralEquatable` 用于比较两个元组或数组是否具有相同的内容；`IStructuralComparable` 用于对元组或数组进行排序。

在演示 `IStructuralEquatable` 的示例中，使用了实现 `IEquatable` 接口的 `Person` 类。`IEquatable` 定义了一个强类型的 `Equals` 方法，该方法比较 `FirstName` 和 `LastName` 属性的值（代码文件 `StructuralComparison/Person.cs`）：

```csharp
public class Person : IEquatable<Person>
{
    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public override string ToString() => $"{Id}, {FirstName} {LastName}";

    public override bool Equals(object obj)
    {
        if (obj == null)
        {
            return base.Equals(obj);
        }
        return Equals(obj as Person);
    }

    public override int GetHashCode() => Id.GetHashCode();

    public bool Equals(Person other)
    {
        if (other == null)
            return base.Equals(other);

        return Id == other.Id && FirstName == other.FirstName &&
            LastName == other.LastName;
    }
}
```

现在创建了两个包含 `Person` 项的数组。两个数组都包含变量名为 `janet` 的同一个 `Person` 对象，以及两个内容相同但不同的 `Person` 对象。比较运算符 `!=` 返回 `true`，因为确实存在两个不同的数组，分别由 `persons1` 和 `persons2` 两个变量名引用。由于 `Array` 类没有重写带一个参数的 `Equals` 方法，因此与使用 `==` 运算符比较引用时的情况相同，它们并不相同（代码文件 `StructuralComparison/Program.cs`）：

```csharp
var janet = new Person { FirstName = "Janet", LastName = "Jackson" };
Person[] persons1 = {
    new Person
    {
        FirstName = "Michael",
        LastName = "Jackson"
    },
    janet
};

Person[] persons2 = {
    new Person
    {
        FirstName = "Michael",
        LastName = "Jackson"
    },
    janet
};

if (persons1 != persons2)
{
    WriteLine("not the same reference");
}
```

调用 `IStructuralEquatable` 接口定义的 `Equals` 方法——即第一个参数类型为 `object`、第二个参数类型为 `IEqualityComparer` 的方法——可以通过传递一个实现 `IEqualityComparer<T>` 的对象来定义比较方式。`IEqualityComparer` 的默认实现由 `EqualityComparer<T>` 类完成。该实现会检查类型是否实现了 `IEquatable` 接口，并调用 `IEquatable.Equals` 方法。如果类型没有实现 `IEquatable`，则会调用基类 `Object` 的 `Equals` 方法进行比较。

`Person` 实现了 `IEquatable<Person>`，其中会比较对象的内容，而这两个数组确实包含相同的内容：

```csharp
if ((persons1 as IStructuralEquatable).Equals(persons2,
    EqualityComparer<Person>.Default))
{
    WriteLine("the same content");
}
```

接下来，你将看到如何使用元组完成同样的事情。这里创建了两个内容相同的元组实例。当然，由于引用 `t1` 和 `t2` 引用的是两个不同的对象，比较运算符 `!=` 返回 `true`：

```csharp
var t1 = Tuple.Create(1, "Stephanie");
var t2 = Tuple.Create(1, "Stephanie");
if (t1 != t2)
{
    WriteLine("not the same reference to the tuple");
}
```

`Tuple<>` 类提供了两个 `Equals` 方法：一个是从 `Object` 基类重写而来的，以对象作为参数；另一个是由 `IStructuralEquatable` 接口定义的，以对象和 `IEqualityComparer` 作为参数。如所示，可以将另一个元组传递给第一个方法。该方法使用 `EqualityComparer<object>.Default` 获取一个 `ObjectEqualityComparer<object>` 来进行比较。这样，元组中的每一项都会通过调用 `Object.Equals` 方法进行比较。如果每一项都返回 `true`，则 `Equals` 方法的结果为 `true`，这里在 `int` 和 `string` 值相同的情况下正是如此：

```csharp
if (t1.Equals(t2))
{
    WriteLine("the same content");
}
```

你还可以创建自定义的 `IEqualityComparer`，如下面的示例所示，使用 `TupleComparer` 类。该类实现了 `IEqualityComparer` 接口的 `Equals` 和 `GetHashCode` 两个方法：

```csharp
class TupleComparer : IEqualityComparer
{
    public new bool Equals(object x, object y) => x.Equals(y);
```


```
IWrapper<object> storedObjectWrapper =
(IWrapper<object>)stringWrapper;
Circle myCircle = new Circle();
storedObjectWrapper.SetData(myCircle);
```

`IWrapper<T>` 接口被称为不变的。即使类型 A 派生自类型 B，也不能将 `IWrapper<A>` 对象分配给 `IWrapper<B>` 类型的引用。默认情况下，C# 实现此限制以确保代码的类型安全。

## 协变接口

假设你用以下示例中所示的 `IStoreWrapper<T>` 和 `IRetrieveWrapper<T>` 接口代替 `IWrapper<T>`，并像这样在 `Wrapper<T>` 类中实现这些接口：

```
interface IStoreWrapper<T>
{
    void SetData(T data);
}

interface IRetrieveWrapper<T>
{
    T GetData();
}

class Wrapper<T> : IStoreWrapper<T>, IRetrieveWrapper<T>
{
    private T storedData;

    void IStoreWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }

    T IRetrieveWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
```

在功能上，`Wrapper<T>` 类与之前相同，只是你通过不同的接口访问 `SetData` 和 `GetData` 方法。

```
Wrapper<string> stringWrapper = new Wrapper<string>();
IStoreWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
```

```
IRetrieveWrapper<string> retrievedStringWrapper = stringWrapper;
Console.WriteLine($"Stored value is
{retrievedStringWrapper.GetData()}");
```

那么，以下代码合法吗？

```
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

简短的答案是否定的，它无法编译并出现与之前相同的错误。但如果你仔细想想，虽然 C# 编译器认为此语句不是类型安全的，但假设此原因的原因不再有效。`IRetrieveWrapper<T>` 接口仅允许你使用 `GetData` 方法读取 `Wrapper<T>` 对象中保存的数据，并且它不提供任何更改数据的方式。在此类情况下，其中类型参数仅作为泛型接口中方法的返回值出现，你可以通知编译器某些隐式转换是合法的，并且它不必强制严格的类型安全。你通过在声明类型参数时指定 `out` 关键字来实现这一点，如下所示：

```
interface IRetrieveWrapper<out T>
{
    T GetData();
}
```

此功能称为协变。你可以将 `IRetrieveWrapper<A>` 对象分配给 `IRetrieveWrapper<B>` 引用，只要从类型 A 到类型 B 存在有效的转换，或者类型 A 派生自类型 B。以下代码现在可以编译并按预期运行：

```
// string derives from object, so this is now legal
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

你只能在类型参数作为方法的返回类型出现时使用 `out` 修饰符指定类型参数。如果使用类型参数指定任何方法参数的类型，则 `out` 修饰符是非法的，你的代码将无法编译。此外，协变仅适用于引用类型。这是因为值类型不能形成继承层次结构。因此，以下代码将无法编译，因为 `int` 是值类型：

```
Wrapper<int> intWrapper = new Wrapper<int>();
IStoreWrapper<int> storedIntWrapper = intWrapper; // this is legal
...
// the following statement is not legal - ints are not objects
IRetrieveWrapper<object> retrievedObjectWrapper = intWrapper;
```

`.NET Framework` 中定义的多个接口表现出协变，其中包括 `IEnumerable<T>` 接口，该接口在第 19 章“枚举集合”中进行了详细介绍。

## 注意

只有接口和委托类型（在第 18 章中介绍）可以声明为协变。你不会对泛型类指定 `out` 修饰符。

## 反变接口

反变遵循与协变相似的原则，只是它在相反的方向工作；它使你能够通过对类型 A 的引用来引用类型 B 的对象，只要类型 B 派生自类型 A。这听起来很复杂，因此值得查看 `.NET Framework` 类库中的一个示例。

`.NET Framework` 中的 `System.Collections.Generic` 命名空间提供了一个名为 `IComparer` 的接口，其如下所示：

```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

实现此接口的类必须定义 `Compare` 方法，该方法用于比较由 T 类型参数指定的类型的两个对象。`Compare` 方法预期返回一个整数值：如果参数 x 和 y 具有相同的值则为零，如果 x 小于 y 则为负，如果 x 大于 y 则为正。以下代码显示了一个根据哈希码对对象进行排序的示例。（`GetHashCode` 方法由 `Object` 类实现。它只是返回一个标识对象的整数值。所有引用类型都继承此方法并且可以用自己的实现重写它。）

```
class ObjectComparer : IComparer<Object>
{
    int IComparer<Object>.Compare(Object x, Object y)
    {
        int xHash = x.GetHashCode();
        int yHash = y.GetHashCode();

        if (xHash == yHash)
            return 0;

        if (xHash < yHash)
            return -1;
        return 1;
    }
}
```

你可以创建 `ObjectComparer` 对象并通过 `IComparer<Object>` 接口调用 `Compare` 方法来比较两个对象，如下所示：

```
Object x = ...;
Object y = ...;
ObjectComparer objectComparer = new ObjectComparer();
IComparer<Object> objectComparator = objectComparer;
int result = objectComparator.Compare(x, y);
```

这就是枯燥的部分。更有趣的是，你可以通过比较字符串的 `IComparer` 接口版本来引用同一个对象，如下所示：

```
IComparer<String> stringComparator = objectComparer;
```

乍一看，此语句似乎违反了你能想象到的所有类型安全规则。然而，如果你思考 `IComparer<T>` 接口的作用，这种方法是有意义的。`Compare` 方法的目的是基于传入的参数之间的比较返回一个值。如果你可以比较 `Objects`，你当然也应该能够比较 `Strings`，因为它们只是 `Objects` 的特化类型。毕竟，`String` 应该能够做 `Object` 能够做的任何事情——这就是继承的目的。

然而，这仍然听起来有点武断。C# 编译器如何知道你在 `Compare` 方法的代码中不会执行任何可能在通过基于不同类型的接口调用方法时失败的类型特定操作？如果你重新查看 `IComparer` 接口的定义，你可以看到在类型参数之前的 `in` 限定符：

```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

`in` 关键字告诉 C# 编译器你可以将类型 T 作为参数类型传递给方法，或者传递派生自 T 的任何类型。你不能将 T 用作任何方法的返回类型。从本质上讲，这使得你可以通过基于对象类型的泛型接口引用对象，或者通过基于派生自对象类型的类型的泛型接口引用对象。基本上，如果类型 A 暴露了一些操作、属性或字段，那么如果

类型 B 派生自类型 A，它也必须暴露相同的操作（如果已被重写，则可能行为不同）、属性和字段。因此，用类型 B 的对象替换类型 A 的对象应该是安全的。

协变和反变可能看起来是泛型世界中的边缘话题，但它们是有用的。例如，`List<T>` 泛型集合类（在 `System.Collections.Generic` 命名空间中）使用 `IComparer<T>` 对象来实现 `Sort` 和 `BinarySearch` 方法。`List<Object>` 对象可以包含任何类型的对象的集合，因此 `Sort` 和 `BinarySearch` 方法需要能够对任何类型的对象进行排序。没有使用反变，`Sort` 和 `BinarySearch` 方法需要包含确定正在排序或搜索的项目的实际类型的逻辑，然后实现类型特定的排序或搜索机制。然而，除非你是一名数学家，否则很难回忆起协变和反变实际上做了什么。我根据本节中的示例记住的方式如下：

- **协变示例** 如果泛型接口中的方法可以返回字符串，它们也可以返回对象。（所有字符串都是对象。）

- **反变示例** 如果泛型接口中的方法可以接受对象参数，它们也可以接受字符串参数。（如果你可以使用对象执行操作，你也可以使用字符串执行相同的操作，因为所有字符串都是对象。）

> **注意**
>
> 与协变一样，只有接口和委托类型可以声明为反变。你不会对泛型类指定 `in` 修饰符。

### 摘要

在本章中，你学习了如何使用泛型创建类型安全的类。你看到了如何通过指定类型参数来实例化泛型类型。你还看到了如何实现泛型接口和定义泛型方法。最后，你学习了如何定义协变和反变泛型接口，使其能够与类型层次结构一起操作。

- 如果你想继续下一章，请保持 `Visual Studio 2015` 运行并转到第 18 章。
- 如果你现在想退出 `Visual Studio 2015`，请在文件菜单上单击退出。如果出现保存对话框，请单击是并保存项目。

### 快速参考

| 要 | 执行此操作 |
|---|---|
| 使用泛型类型实例化对象 | 指定适当的泛型类型参数。例如：`Queue<int> myQueue = new Queue<int>();` |
| 创建新的泛型类型 | 使用类型参数定义类。例如：``` public class Tree<TItem> { ... } ``` |
| 限制可替换为泛型类型参数的类型 | 在定义类时使用 `where` 子句指定约束。例如：``` public class Tree<TItem> where TItem : IComparable<TItem> { ... } ``` |
| 定义泛型方法 | 使用类型参数定义方法。例如：``` static void InsertIntoTree<TItem> (Tree<TItem> tree, params TItem[] data) { ... } ``` |
| 调用泛型方法 | 为每个类型参数提供类型。例如：`InsertIntoTree<char>(charTree, 'Z', 'X');` |
| 定义协变接口 | 为协变类型参数指定 `out` 限定符。仅将协变类型参数作为方法的返回类型引用，而不是作为方法参数的类型：``` interface IRetrieveWrapper<out T> { T GetData(); } ``` |

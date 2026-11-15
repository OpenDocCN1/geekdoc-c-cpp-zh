

```
}
ICollection<Phone> IContainer<Phone>.Items
{
    get { ... }
    set { ... }
}
ICollection<Email> IContainer<Email>.Items
{
    get { ... }
    set { ... }
}
}
```

在此示例中，Items 属性通过具有不同类型参数的显式接口实现多次出现。如果没有泛型，这是不可能的，编译器反而只允许一个显式的 IContainer.Items 属性。

对 Person 的一个可能改进是也实现 IContainer<object>，并让 items 返回所有三个容器（地址、电话和电子邮件）的组合。

## 定义构造函数和终结器

也许出人意料的是，泛型上的构造函数和析构函数不需要类型参数来匹配类声明（换句话说，不是 Pair<T>({...})。在清单 11.11 中的对示例中，构造函数使用 public Pair(T first, T second) 声明。

## 清单 11.11：声明泛型类型的构造函数

```
public struct Pair<T>: IPair<T>
{
    public Pair(T first, T second)
    {
        _Second = second;
        _Second = second;
    }

    public T First
    {
        get { return _First; }
        set { _First = value; }
    }
    private T _First;

    public T Second
    {
        get { return _Second; }
        set { _Second = value; }
    }
    private T _Second;
}
```

## 指定默认值

清单 11.1 包含一个构造函数，用于获取 First 和 Second 的初始值，并将它们分配给 _First 和 _Second。由于 Pair<T> 是结构体，你提供的任何构造函数都必须初始化所有字段。然而，这带来了一个问题。考虑一个在实例化时仅初始化一半对的 Pair<T> 构造函数。

定义这样的构造函数（如清单 11.12 所示）会导致编译错误，因为字段 _Second 在构造函数结束时未初始化。为 _Second 提供初始化会带来问题，因为你不知道 T 的数据类型。如果它是引用类型，则 null 可行，但如果 T 是值类型（除非可为 null），则这不够。

## 清单 11.12：未初始化所有字段，导致编译错误

```
public struct Pair<T>: IPair<T>
{
// ERROR: Field 'Pair<T>._Second' must be fully assigned
// before control leaves the constructor
// public Pair(T first)
// {
// _First = first;
// }
// ...
}
```

为处理此场景，C# 2.0 允许使用 default 运算符以动态方式对任何数据类型编码默认值，这在第 8 章中首次讨论过。在第 8 章中，我展示了如何使用 default(int) 指定 int 的默认值，而字符串的默认值使用 default(string)（对所有引用类型返回 null）。对于 _Second 所需的 T，你使用 default(T)（参见清单 11.13）。

## 清单 11.13：使用 default 运算符初始化字段

```
public struct Pair<T>: IPair<T>
{
    public Pair(T first)
    {
        _First = first;
        _Second = default(T);
    }

    // ...
}
```

default 运算符在泛型上下文之外也是允许的；任何语句都可以使用它。

## 多个类型参数

泛型类型可以使用任意数量的类型参数。最初的 Pair<T> 示例仅包含一个类型参数。要支持存储二元对象对（例如名称/值对），需要扩展 Pair<T> 以支持两个类型参数，如清单 11.14 所示。

## 清单 11.14：声明带有多个类型参数的泛型

```
interface IPair<TFirst, TSecond>
{
    TFirst First { get; set; }
    TSecond Second { get; set; }
}

public struct Pair<TFirst, TSecond>: IPair<TFirst, TSecond>
{
    public Pair(TFirst first, TSecond second)
    {
        _First = first;
        _Second = second;
    }

    public TFirst First
    {
        get { return _First; }
        set { _First = value; }
    }
    private TFirst _First;

    public TSecond Second
    {
        get { return _Second; }
        set { _Second = value; }
    }
    private TSecond _Second;
}
```

使用 Pair<TFirst, TSecond> 类时，需在声明和实例化语句的尖括号中提供多个类型参数，然后在调用方法时为方法参数提供匹配的类型，如清单 11.15 所示。

## 清单 11.15：使用带有多个类型参数的类型

```
Pair<int, string> historicalEvent =
    new Pair<int, string>(1914,
    "Shackleton leaves for South Pole on ship Endurance");
Console.WriteLine("({0}: {1}",
    historicalEvent.First, historicalEvent.Second);
```

类型参数的数量（即 arity）唯一区分了类。因此，可以在同一命名空间中定义 Pair<T> 和 Pair<TFirst, TSecond>，因为 arity 有所不同。

## Arity 丰富

在 C# 4.0 中，CLR 团队定义了九个名为 Tuple 的新泛型类。与 Pair<...> 一样，可以重用相同的名称，因为 arity 有所不同（每个类具有不同数量的类型参数），如清单 11.16 所示。

## 清单 11.16：使用 out 类型参数修饰符的协变

```
public class Tuple { ... }
public class Tuple<T1> : IStructuralComparable, IComparable { ... }
public class Tuple<T1, T2> : ... { ... }
public class Tuple<T1, T2, T3> : ... { ... }
public class Tuple<T1, T2, T3, T4> : ... { ... }
public class Tuple<T1, T2, T3, T4, T5> : ... { ... }
public class Tuple<T1, T2, T3, T4, T5, T6> : ... { ... }
public class Tuple<T1, T2, T3, T4, T5, T6, T7> : ... { ... }
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest> : ... { ... }
```

Tuple... 类集的设计目的与 Pair<T> 和 Pair<TFirst, TSecond> 类相同，但它们共同可以处理七个类型参数。事实上，使用清单 11.16 中显示的最后一个 Tuple，TRest 可用于存储另一个 Tuple，从而使元组大小的潜在限制实际上是无限的。

元组类集的另一个有趣特性是 Tuple（无类型参数）。该类有八个静态 create 方法用于实例化各种泛型类型。虽然每个泛型类型都可以直接使用其构造函数进行实例化，但 Tuple 类型的 create 方法允许隐式类型参数。清单 11.17 显示了区别。

## 清单 11.17：使用 out 类型参数修饰符的协变

```
Tuple<string, Contact<KeyValuePair,
    KeyValuePair =
    Tuple.Create(
    "555-55-5555", new Contact("Inigo Montoya"));
KeyValuePair =
    new Tuple<string, Contact<(
    "555-55-5555", new Contact("Inigo Montoya"));
```

显然，当 Tuple 变得很大时，如果没有 Create() 方法，需要指定的类型参数数量可能会很麻烦。

## 嵌套泛型类型

包含类型上的类型参数会自动向下级联到嵌套类型。例如，如果包含类型包含类型参数 T，则类型 T 也可在嵌套类型上使用。如果嵌套类型包含其自己的名为 T 的类型参数，则这将隐藏包含类型中的类型参数，嵌套类型中对 T 的任何引用都将指向嵌套的 T 类型参数。幸运的是，在嵌套类型中重用相同的类型参数名称会导致编译器警告，以防止意外重叠（参见清单 11.18）。

## 清单 11.18：嵌套泛型类型

```
class Container<T, U>
{
    // Nested classes inherit type parameters.
    // Reusing a type parameter name will cause
    // a warning.
    class Nested<U>
    {
        void Method(T param0, U param1)
        {
        }
    }
}
```

将容器的类型参数在嵌套类型中可用的行为与嵌套类型行为一致，因为包含类型的私有成员也可从嵌套类型访问。规则很简单：类型在其出现的花括号内的任何位置都可用。

## 约束

泛型支持在类型参数上定义约束的功能。这些约束强制类型符合各种规则。以清单 11.19 中显示的 BinaryTree<T> 类为例。

## 清单 11.19：声明无约束的 BinaryTree<T> 类

```
public class BinaryTree<T>
{
    public BinaryTree( T item )
    {
        Item = item;
    }

    public T Item
    {
        get { return _item; }
        set { _item = value; }
    }

    private T _item;

    public Pair<BinaryTree<T>> SubItems
    {
        get { return _subItems; }
        set { _subItems = value; }
    }

    private Pair<BinaryTree<T>> _subItems;
}
```


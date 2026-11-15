

(一个有趣的旁注是，BinaryTree<T> 在内部使用 Pair<T>，之所以可行是因为 Pair<T> 只是另一种类型。)

假设你希望在将值分配给 SubItems 属性时，对 Pair<T> 值中的值进行排序。为了实现排序，SubItems 设置访问器使用所提供键的 CompareTo() 方法，如清单 11.20 所示。

## LISTING 11.20: 需要类型参数支持接口

```
public class BinaryTree<T>
{
    ...
    public Pair<BinaryTree<T>> SubItems
    {
        get { return _SubItems; }
        set
        {
            IComparable<T> first;
            // ERROR: Cannot implicitly convert type...
            first = value.First.Item; // Explicit cast required
            if (first.CompareTo(value.Second.Item) < 0)
            {
                // first is less than second.
                ...
            }
            else
            {
                // first and second are the same or
                // second is less than first.
                ...
            }
            _SubItems = value;
        }
    }
    private Pair<BinaryTree<T>> _SubItems;
}
```

在编译时，类型参数 T 是泛型的。当代码按所示编写时，编译器假设 T 上可用的成员仅限于从基类型 object 继承的成员，因为每种类型都以 object 为祖先。（因此，仅 ToString() 等方法可用于类型参数 T 的键实例。）结果，编译器显示编译错误，因为 CompareTo() 方法未在类型 object 上定义。

你可以将 T 参数强制转换为 IComparable<T> 接口，以便访问 CompareTo() 方法，如清单 11.21 所示。

## LISTING 11.21: 需要类型参数支持接口或抛出异常

```
public class BinaryTree<T>
{
    ...
    public Pair<BinaryTree<T>> SubItems
    {
        get { return _SubItems; }
        set
        {
            IComparable<T> first;
            first = (IComparable<T>)value.First.Item;
            if (first.CompareTo(value.Second.Item) < 0)
            {
                // first is less than second.
                ...
            }
            else
            {
                // second is less than or equal to first.
                ...
            }
            _SubItems = value;
        }
    }
    private Pair<BinaryTree<T>> _SubItems;
}
```

不幸的是，如果你现在声明一个 BinaryTree 类变量并提供一个未实现 IComparable<T> 接口的类型参数，则会遇到执行时错误——具体来说，是 InvalidCastException。这抵消了泛型的一个优势。

为了避免此异常并改为提供编译时错误，C# 允许你为泛型类中声明的每个类型参数提供可选的约束列表。约束声明泛型所要求的类型参数特征。你使用 where 关键字声明约束，后跟一个“参数-要求”对，其中参数必须是泛型类型中定义的参数之一，而要求是限制类型“派生自”的类或接口、默认构造函数的存在，或引用/值类型限制。

## 语言对比：C++ — 模板

C# 和 CLR 中的泛型与其他语言中的类似构造不同。尽管其他语言提供类似功能，但 C# 的类型安全性要高得多。C# 中的泛型既是语言特性也是平台特性——底层 2.0 运行时在其引擎中为泛型提供了深度支持。

C++ 模板与 C# 泛型有显著不同，因为 C# 利用了 CIL。C# 泛型被编译为 CIL，导致特化仅在每个值类型使用时才在执行时发生，而引用类型仅发生一次。

C++ 模板不支持的一个独特功能是显式约束。C++ 模板允许你编译可能属于类型参数也可能不属于的方法调用。因此，如果成员不存在于类型参数中，则会发生错误，可能伴随着晦涩的错误消息并指向源代码中意外的位置。然而，C++ 实现的优势在于可以在类型上调用运算符（+、- 等等）。C# 不支持在类型参数上调用运算符，因为运算符是静态的——它们无法通过接口或基类约束来识别。

该错误的问题在于它仅在使用模板时发生，而不是在定义时发生。因为 C# 泛型可以声明约束，编译器可以在定义泛型时防止此类错误，从而更早地识别无效假设。此外，在声明泛型类型的变量时，错误将指向变量的声明，而不是泛型实现中使用成员的位置。

值得注意的是，Microsoft C++ 中的 CLI 支持同时包含泛型和 C++ 模板，因为两者各有独特的特性。

## 接口约束

为了满足排序要求，你需要在 BinaryTree 类中使用 CompareTo() 方法。为了最有效地做到这一点，你需要对 T 类型参数施加约束。你需要 T 类型参数实现 IComparable<T> 接口。此语法出现在清单 11.22 中。

## LISTING 11.22: 声明接口约束

```
public class BinaryTree<T>
    where T: System.IComparable<T>
{
    ...
    public Pair<BinaryTree<T>> SubItems
    {
        get { return _SubItems; }
        set
        {
            IComparable<T> first;
            // Notice that the cast can now be eliminated.
            first = value.First.Item;
            if (first.CompareTo(value.Second.Item) < 0)
            {
                // first is less than second
                ...
            }
            else
            {
                // second is less than or equal to first.
                ...
            }
            _SubItems = value;
        }
    }
    private Pair<BinaryTree<T>> _SubItems;
}
```

鉴于清单 11.22 中添加了接口约束，编译器确保每次使用 BinaryTree 类时，你都指定实现 IComparable<T> 接口的类型参数。此外，在调用 CompareTo() 方法之前，你不再需要显式将变量强制转换为 IComparable<T> 接口。甚至不需要强制转换即可访问使用显式接口实现的成员，在其他上下文中，如果没有强制转换，这些成员会被隐藏。为了解决调用哪个成员，编译器首先直接检查类成员，然后查看显式接口成员。如果没有约束解析参数，则仅允许 object 的成员。

如果你尝试使用 System.Text.StringBuilder 作为类型参数创建 BinaryTree<T> 变量，你会收到编译器错误，因为 StringBuilder 未实现 IComparable<T>。错误与输出 11.3 中显示的类似。

## 输出 11.3:

```
error CS0309: The type 'System.Text.StringBuilder' must be convertible
to 'System.IComparable<T>' in order to use it as parameter 'T' in the
generic type or method 'BinaryTree<T>'
```

要为约束指定接口，你需要声明接口约束。此约束甚至避免了为调用显式接口成员实现而进行强制转换的需要。

## 基类约束

有时你可能希望将构造类型限制为特定的类派生。你可以使用基类约束来实现这一点，如清单 11.23 所示。

## LISTING 11.23: 声明基类约束

```
public class EntityDictionary<TKey, TValue>
    : System.Collections.Generic.Dictionary<TKey, TValue>
    where TValue : EntityBase
{
        ...
}
```

与 System.Collections.Generic.Dictionary<TKey, TValue> 本身不同，EntityDictionary<TKey, TValue> 要求所有 TValue 类型都派生自 EntityBase 类。通过要求派生，可以在泛型实现中始终执行强制转换操作，因为约束将确保所有类型参数都派生自基类，因此，与 EntityDictionary 一起使用的所有 TValue 类型参数都可以隐式转换为基类。

基类约束的语法与接口约束相同，只是在指定多个约束时，基类约束必须首先出现。然而，与接口约束不同，


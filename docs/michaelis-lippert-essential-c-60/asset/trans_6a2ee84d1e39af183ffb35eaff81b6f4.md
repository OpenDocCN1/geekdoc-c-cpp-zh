
T上可用的成员只有从基类型object继承的那些，因为每种类型都以object作为基类。因此，在类型参数T的实例上只能调用诸如ToString()之类的方法。结果，编译器会显示编译错误，因为CompareTo()方法未在object类型上定义。

如清单11.21所示，你可以将T参数强制转换为IComparable<T>接口来访问CompareTo()方法。

```csharp
public class BinaryTree<T>
{
    public T Item { get; set; }
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

遗憾的是，如果现在声明一个BinaryTree<SomeType>类变量，但类型参数并未实现IComparable<SomeType>接口，就会遇到执行时错误——具体来说是InvalidCastException。这消除了使用泛型的初衷之一：提高类型安全性。

为了避免此异常，并在类型参数未实现接口时生成编译时错误，C#允许你为泛型类型中声明的每个类型参数提供一个可选的约束列表。约束声明了泛型类型对提供给每个类型参数的类型实参所要求的特性。你使用where关键字声明约束，后跟一个“参数—要求”对，其中参数必须是泛型类型中声明的参数之一，要求描述了类型实参必须可转换到的类或接口、是否存在默认构造函数，或引用/值类型限制。

## 接口约束

为了确保二叉树的节点排序正确，你可以在`BinaryTree`类中使用`CompareTo()`方法。要做到这一点，最有效的方法是对T类型参数施加一个约束。也就是说，你需要T类型参数实现`IComparable<T>`接口。声明此约束的语法见清单11.22。

```csharp
public class BinaryTree<T>
    where T: System.IComparable<T>
{
    public T Item { get; set; }
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

当添加了清单11.22中的接口约束后，编译器会确保每次使用`BinaryTree<T>`类时，你指定的类型参数都实现了相应构造的`IComparable<T>`接口。此外，你不再需要在调用`CompareTo()`方法之前将变量显式强制转换为`IComparable<T>`接口。即使是访问使用显式接口实现的成员，也无需强制转换，在其它上下文中，这种成员若不进行强制转换就会被隐藏。在泛型类型参数类型的值上调用方法时，编译器会检查该方法是否与声明为约束的任何接口上的任何方法匹配。

如果你尝试使用`System.Text.StringBuilder`作为类型参数来创建`BinaryTree<T>`变量，将收到编译器错误，因为`StringBuilder`没有实现`IComparable<StringBuilder>`。该错误与输出11.3中显示的错误类似。

### 输出 11.3

```
error CS0311: The type 'System.Text.StringBuilder' cannot be used as type
parameter 'T' in the generic type or method 'BinaryTree<T>'. There is no
implicit reference conversion from 'System.Text.StringBuilder' to
'System.IComparable<System.Text.StringBuilder>'.
```

要为约束指定接口，需声明**接口类型约束**。这种约束甚至无需强制转换即可调用显式接口成员实现。

## 类类型约束

有时你可能希望将类型实参约束为可转换为某个特定的类类型。使用**类类型约束**即可做到这一点，如清单11.23所示。

### 清单11.23：声明类类型约束

```
public class EntityDictionary<TKey, TValue>
    : System.Collections.Generic.Dictionary<TKey, TValue>
    where TValue : EntityBase
{
    ...
}
```

在清单11.23中，`EntityDictionary<TKey, TValue>`要求为类型参数`TValue`提供的所有类型实参都可隐式转换为`EntityBase`类。通过要求这种转换，就可以在泛型实现中对`TValue`类型的值使用`EntityBase`的成员，因为约束将确保所有类型实参都可隐式转换为`EntityBase`类。

类类型约束的语法与接口类型约束相同，只不过类类型约束必须出现在任何接口类型约束之前（就像在类声明中基类必须出现在实现的接口之前一样）。然而，与接口约束不同，多个基类约束是不允许的，因为不可能从多个无关的类派生。同样，基类约束也不能指定密封类或非类类型。例如，C#不允许将类型参数约束为`string`或`System.Nullable<T>`，因为那样该类型参数就只有一种可能的类型实参了——那就称不上“泛型”了。如果类型参数被约束为单一类型，那首先就没有必要使用类型参数；直接使用该类型即可。

某些“特殊”类型不能作为类类型约束。详见本章后面的高级主题“约束限制”。

## struct/class 约束

另一个有价值的泛型约束是能够将类型实参限制为任何非可空值类型或任何引用类型。C#提供了一种特殊语法，它也适用于引用类型。无需指定T必须从哪个类派生，只需使用`struct`或`class`关键字，如清单11.24所示。

```
public struct Nullable<T> :
    IFormattable, IComparable,
    IComparable<Nullable<T>>, INullable
    where T : struct
{
    // ...
}
```

请注意，class约束——多少有些令人困惑——并不将类型实参限制为类类型，而是将其限制为引用类型。为使用class约束约束的类型参数提供的类型实参可以是任何类、接口、委托或数组类型。

由于类类型约束要求特定的类，将struct约束与类类型约束一起使用会相互矛盾。因此，不能组合struct和class约束。

struct约束有一个特殊之处：可空值类型不满足该约束。为什么？可空值类型是作为泛型类型`Nullable<T>`实现的，而`Nullable<T>`本身就对T应用了struct约束。如果可空值类型满足该约束，就可以定义无意义的类型`Nullable<Nullable<int>>`。双重可空整数会令人困惑到毫无意义的地步。（正如所料，简写语法`int??`也不允许。）

## 多重约束

对于任何给定的类型参数，可以指定任意数量的接口类型约束，但最多只能有一个类类型约束（正如一个类可以实现任意数量的接口，但只能继承自另一个类）。每个新约束都以逗号分隔的列表形式声明，跟在泛型类型参数和冒号之后。如果有多个类型参数，每个都必须以where关键字开头。在清单11.25中，泛型`EntityDictionary`类声明了两个类型参数：`TKey`和`TValue`。`TKey`类型参数有两个接口类型约束，`TValue`类型参数有一个类类型约束。

```
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
    ...
}
```

在这种情况下，`TKey`自身有多个约束，`TValue`还有一个额外约束。当对一个类型参数指定多个约束时，隐含的是AND关系。例如，如果为`TKey`提供类型C作为类型实参，C必须实现`IComparable<C>`和`IFormattable`。

注意每个where子句之间没有逗号。


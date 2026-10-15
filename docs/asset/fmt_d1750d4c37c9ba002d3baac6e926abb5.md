
```
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

## `struct`/`class` 约束

另一个有价值的泛型约束是能够将类型实参限制为任何非可空值类型或任何引用类型。C#提供了一种特殊语法，它也适用于引用类型。无需指定`T`必须从哪个类派生，只需使用`struct`或`class`关键字，如清单11.24所示。

```
public struct Nullable<T> :
    IFormattable, IComparable,
    IComparable<Nullable<T>>, INullable
    where T : struct
{
    // ...
}
```

请注意，`class`约束——多少有些令人困惑——并不将类型实参限制为类类型，而是将其限制为引用类型。为使用`class`约束约束的类型参数提供的类型实参可以是任何类、接口、委托或数组类型。

由于类类型约束要求特定的类，将`struct`约束与类类型约束一起使用会相互矛盾。因此，不能组合`struct`和`class`约束。

`struct`约束有一个特殊之处：可空值类型不满足该约束。为什么？可空值类型是作为泛型类型`Nullable<T>`实现的，而`Nullable<T>`本身就对`T`应用了`struct`约束。如果可空值类型满足该约束，就可以定义无意义的类型`Nullable<Nullable<int>>`。双重可空整数会令人困惑到毫无意义的地步。（正如所料，简写语法`int??`也不允许。）

## 多重约束

对于任何给定的类型参数，可以指定任意数量的接口类型约束，但最多只能有一个类类型约束（正如一个类可以实现任意数量的接口，但只能继承自另一个类）。每个新约束都以逗号分隔的列表形式声明，跟在泛型类型参数和冒号之后。如果有多个类型参数，每个都必须以`where`关键字开头。在清单11.25中，泛型`EntityDictionary`类声明了两个类型参数：`TKey`和`TValue`。`TKey`类型参数有两个接口类型约束，`TValue`类型参数有一个类类型约束。

```
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
    ...
}
```

在这种情况下，`TKey`自身有多个约束，`TValue`还有一个额外约束。当对一个类型参数指定多个约束时，隐含的是AND关系。例如，如果为`TKey`提供类型`C`作为类型实参，`C`必须实现`IComparable<C>`和`IFormattable`。

注意每个`where`子句之间没有逗号。

## 构造函数约束

在某些情况下，希望在泛型类内部创建类型参数类型的实例。例如在 11.26 节中，`EntityDictionary<TKey, TValue>` 类的 `MakeValue()` 方法必须创建对应于类型参数 `TValue` 的类型参数类型的实例。

### LISTING 11.26: Requiring a Default Constructor Constraint

```csharp
public class EntityBase<TKey>
{
    public TKey Key { get; set; }
}

public class EntityDictionary<TKey, TValue> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>, new()
{
    // ...
    public TValue MakeValue(TKey key)
    {
        TValue newEntity = new TValue();
        newEntity.Key = key;
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    // ...
}
```

由于并非所有对象都保证具有公共默认构造函数，编译器不允许你在未受约束的类型参数上调用默认构造函数。要覆盖此编译器限制，可以在指定所有其他约束之后添加文本 `new()`。此文本是构造函数约束，它要求对应于受约束类型参数的类型参数具有公共默认构造函数。只有默认构造函数约束可用。你不能指定一个约束来确保提供的类型参数提供一个带有形式参数的构造函数。

## 约束继承

泛型类型参数及其约束不会被派生类继承，因为泛型类型参数不是成员。记住，类继承是派生类具有基类所有成员的属性。创建一个继承自其他泛型类型的新泛型类型是一种常见做法。在这种情况下，由于派生泛型类型的类型参数成为泛型基类的类型参数，因此类型参数必须具有与基类上相同或更强的约束。困惑吗？请考虑 11.27 节。

### LISTING 11.27: Inherited Constraints Specified Explicitly

```csharp
class EntityBase<T> where T : IComparable<T>
{
    // ...
}

// ERROR:
// The type 'U' must be convertible to
// 'System.IComparable<U>' to use it as parameter
// 'T' in the generic type or method.
// class Entity<U> : EntityBase<U>
// {
//     ...
// }
```

在 11.27 节中，`EntityBase<T>` 要求为 `T` 提供的类型参数 `U` 由基类说明符 `EntityBase<U>` 实现 `IComparable<U>`。因此，`Entity<U>` 类需要对 `U` 要求相同的约束。未能这样做将导致编译时错误。此模式增加了程序员对派生类中基类的类型约束的认识，避免了程序员在使用派生类时可能发生的混淆，当发现约束但不了解其来源时。

我们尚未介绍泛型方法；我们将在本章后面介绍它们。现在，只需认识到方法也可能是泛型的，并且也可能对为其类型参数提供的类型参数施加约束。那么，当虚拟泛型方法被继承和重写时，约束如何处理？与在泛型类上声明的类型参数的情况相反，重写虚拟泛型方法（或显式接口方法）的约束是隐式继承的，并且可能不会重复声明（参见 11.28 节）。

### LISTING 11.28: Repeating Inherited Constraints on Virtual Members Is Prohibited

```csharp
class EntityBase
{
    public virtual void Method<T>(T t)
        where T : IComparable<T>
    {
        // ...
    }
}

class Order : EntityBase
{
    public override void Method<T>(T t)
    //    Constraints may not be repeated on overriding
    //    members
    //    where T : IComparable<T>
    {
        // ...
    }
}
```

在泛型类继承的情况下，可以通过添加基类上的约束（必需）以及其他约束来进一步约束派生类上的类型参数。然而，重写的虚拟泛型方法需要完全符合基类方法定义的约束。额外的约束可能会破坏多态性，因此不允许，并且重写方法上的类型参数约束是隐含的。

### ADVANCED TOPIC

## 约束限制

约束被适当限制以避免无意义的代码。例如，你不能将类类型约束与 `struct` 或 `class` 约束组合。也不能指定约束以将继承限制为特殊类型，例如 `object`、数组、`System.ValueType`、`System.Enum`（枚举）、`System.Delegate` 或 `System.MulticastDelegate`。

在某些情况下，约束限制可能更可取，但它们仍然不受支持。以下小节提供了一些不允许的约束的附加示例。

### Operator Constraints Are Not Allowed

你不能将类型参数约束为实现特定方法或运算符的类型，除非通过接口类型约束（用于方法）或类类型约束（用于方法和运算符）。由于这个原因，11.29 节中的泛型 `Add()` 不起作用。

```csharp
public abstract class MathEx<T>
{
    public static T Add(T first, T second)
    {
        // Error: Operator '+' cannot be applied to
        // operands of type 'T' and 'T'.
        // return first + second;
    }
}
```

在这种情况下，该方法假设 `+` 运算符对可作为 `T` 的类型参数提供的所有类型都可用。但没有任何约束可以防止你提供一个没有关联加法运算符的类型参数，因此会发生错误。不幸的是，除了使用实现加法运算符的类类型约束的类类型约束之外，没有办法指定在约束中需要加法运算符。

更一般地说，没有办法约束类型具有静态方法。

### OR Criteria Are Not Supported

如果你为类型参数提供多个接口或类约束，编译器始终假设约束之间存在 AND 关系。例如，`where T : IComparable<T>, IFormattable` 要求同时支持 `IComparable<T>` 和 `IFormattable`。没有办法在约束之间指定 OR 关系。因此，11.30 节的等价物不受支持。

```csharp
public class BinaryTree<T>
{
    // Error: OR is not supported.
    // where T: System.IComparable<T> || System.IFormattable
    ...
}
```

支持此功能将阻止编译器在编译时解析要调用哪个方法。

### Constraints of Type Delegate and Enum Are Not Valid

委托类型、数组类型和枚举类型可能不会用作类类型约束，因为它们都是有效地“密封”类型。（如果你不熟悉委托类型，请参阅第 12 章。）它们的基类型——`System.Delegate`、`System.MulticastDelegate`、`System.Array` 和 `System.Enum`——也不能用作约束。例如，当编译器遇到 11.31 节中的类声明时，将生成错误。

### LISTING 11.31: Inheritance Constraints Cannot Be of Type System.Delegate

```csharp
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

所有委托类型都被视为不能指定为类型参数的特殊类。这样做将阻止对 `Event()` 调用的编译时验证，因为使用数据类型 `System.Delegate` 和 `System.MulticastDelegate` 时事件触发的签名是未知的。相同的限制适用于任何枚举类型。

### Constructor Constraints Are Allowed Only for Default Constructors

11.26 节包括一个构造函数约束，强制为 `TValue` 提供的类型参数提供公共无参数构造函数。没有约束可以强制类型参数提供采用其他形式参数的构造函数。例如，你可能希望约束 `TValue`，以便为其提供的类型参数必须提供一个采用为 `TKey` 提供的类型参数的构造函数，但这是不可能的。11.32 节演示了无效代码。

### LISTING 11.32: Constructor Constraints Can Be Specified Only for Default Constructors

```csharp
public TValue New(TKey key)
{
```

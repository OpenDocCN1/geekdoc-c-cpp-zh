

不允许有多个基类约束，因为无法从多个类派生。同样，不能为密封类或特定结构体指定基类约束。例如，C# 不允许类型参数的约束派生自 string 或 System.Nullable<T>。

## struct/class 约束

另一个有价值的泛型约束是能够将类型参数限制为值类型或引用类型。编译器不允许在约束中将 System.ValueType 指定为基类。相反，C# 提供了也适用于引用类型的特殊语法。与其指定 T 必须派生的类，不如直接使用关键字 struct 或 class，如清单 11.24 所示。

### 清单 11.24：将类型参数指定为值类型

```
public struct Nullable<T> :
    IFormattable, IComparable,
    IComparable<Nullable<T>>, INullable
    where T : struct
{
    // ...
}
```

由于基类约束要求特定的基类，因此将 struct 或 class 与基类约束一起使用是没有意义的，实际上还可能导致冲突约束。因此，不能将 struct 和 class 约束与基类约束一起使用。

struct 约束有一个特殊特征。它将可能的类型参数限制为仅值类型，同时防止类型参数为 System.Nullable<T> 类型参数。为什么？如果没有最后这一限制，就可以定义荒谬的类型 Nullable<Nullable<T>>，这是荒谬的，因为 Nullable<T> 本身就允许支持 null 的值类型变量，因此可空-可空类型变得毫无意义。由于可空运算符 (?) 是声明可空值类型的 C# 快捷方式，struct 约束提供的 Nullable<T> 限制也防止了诸如以下代码：

```
int? number // Equivalent to Nullable<Nullable<int> if allowed
```

## 多个约束

对于任何给定的类型参数，您可以指定任意数量的接口作为约束，但不超过一个类，就像一个类可以实现任意数量的接口但只能继承自另一个类一样。每个新约束都在泛型类型和冒号后的逗号分隔列表中声明。如果有多个类型参数，每个都必须由 where 关键字前置。在清单 11.25 中，EntityDictionary 类包含两个类型参数：TKey 和 TValue。TKey 类型参数有两个接口约束，TValue 类型参数有一个基类约束。

### 清单 11.25：指定多个约束

```
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
    ...
}
```

在这种情况下，TKey 本身有多个约束，TValue 有额外约束。在对一个类型参数指定多个约束时，默认假设为 AND 关系。例如，TKey 必须实现 IComparable<TKey> 和 IFormattable。

请注意，每个 where 子句之间没有逗号。

## 构造函数约束

在某些情况下，在泛型类内部创建类型参数的实例是可取的。在清单 11.26 中，EntityDictionary<TKey, TValue> 类的 New() 方法必须创建类型参数 TValue 的实例。

### 清单 11.26：要求默认构造函数约束

```
public class EntityBase<TKey>
{
    private TKey _Key;

    public TKey Key
    {
        get{ return _key; }
        set{ _key = value; }
    }
}

public class EntityDictionary<TKey, TValue> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>, new()
{
    // ...

    public TValue New(TKey key)
    {
        TValue newEntity = new TValue();
        newEntity.Key = key;
        Add(newEntity.Key, newEntity);
        return newEntity;
    }

    // ...
}
```

由于并非所有对象都保证具有公共默认构造函数，编译器不允许您在类型参数上调用默认构造函数。要覆盖此编译器限制，请在指定所有其他约束后添加文本 `new()`。此文本是 **构造函数约束**，它强制装饰有构造函数约束的类型参数具有默认构造函数。仅提供默认构造函数约束。您不能为带参数的构造函数指定约束。

## 约束继承

约束会被派生类继承，但必须在派生类上显式指定。请参阅清单 11.27。

### 清单 11.27：显式指定继承的约束

```
class EntityBase<T> where T : IComparable<T>
{
    // ...
}
```

```
// ERROR:
// The type 'T' must be convertible to 'System.IComparable<T>'
// In order to use it as parameter 'T' in the generic type or
// method.
```

```
// class Entity<T> : EntityBase<T>
// {
//     ...
// }
```

由于 EntityBase 要求 T 实现 IComparable<T>，Entity 类需要显式包含相同的约束。如果不这样做，将导致编译错误。这提高了程序员对派生类中约束的认识，避免在使用派生类并发现约束但不了解其来源时产生混淆。

相比之下，泛型重写（或显式接口）方法上的约束是隐式继承的，不能重复说明（请参见清单 11.28）。

### 清单 11.28：显式指定继承的约束

```
class EntityBase<T> where T : IComparable<T>
{
    public virtual void Method<T>(T t)
        where T : IComparable<T>
    {
        // ...
    }
}
```

```
class Entity<T> : EntityBase<T>
{
    public virtual void Method<T>(T t)
        // Error: Constraints may not be
        // repeated on overriding members
        where T : IComparable<T>
    {
        // ...
    }
}
```

在继承情况下，基类上的类型参数可以通过添加不仅基类上的约束（必需），还可以添加其他约束来进一步约束。但是，重写成员需要符合基类方法中定义的“接口”。其他约束可能会破坏多态性，因此不允许，重写方法上的类型参数约束是隐含的。

## 约束限制

约束被适当限制以避免荒谬的代码。例如，您不能将基类约束与 struct 或 class 约束结合使用，也不能在 struct 约束类型参数上使用 Nullable<T>。此外，您不能指定约束来将继承限制为 object、数组、System.ValueType、System.Enum（枚举）、System.Delegate 和 System.MulticastDelegate 等特殊类型。

在某些情况下，约束限制也许更可取，但它们仍然不受支持。以下小节提供了一些不允许的约束的其他示例。

## 不允许运算符约束

约束的另一限制是，您不能指定类支持特定方法或运算符的约束，除非该方法或运算符在接口上。正因为如此，清单 11.29 中的泛型 Add() 无法工作。

### 清单 11.29：约束表达式不能要求运算符

```
public abstract class MathEx<T>
{
    public static T Add(T first, T second)
    {
        // Error: Operator '+' cannot be applied to
        // operands of type 'T' and 'T'.
        return first + second;
    }
}
```

在这种情况下，该方法假设 + 运算符在所有类型上都可用。但是，由于所有类型仅支持 object 的方法（不包括 + 运算符），因此会发生错误。不幸的是，无法在约束中指定 + 运算符；因此，以这种方式创建 add 方法要麻烦得多。造成此限制的一个原因是，无法约束类型具有静态方法。例如，您无法在接口上指定静态方法。


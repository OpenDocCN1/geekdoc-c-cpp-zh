

接口属性声明的特性、类型和标识符与类中的属性声明（§10.7）具有相同的含义。

接口属性声明的访问器与类属性声明（§10.7.2）的访问器相对应，不同之处在于接口访问器的主体必须始终是一个分号。因此，访问器仅指示该属性是可读写、只读还是只写。

如果存在 get 访问器，接口属性的类型必须是输出安全的；如果存在 set 访问器，则必须是输入安全的。

### 13.2.3 接口事件

接口事件使用 interface-event-declaration 声明：

```
interface-event-declaration:
    attributes_opt new_opt event type identifier ;
```

接口事件声明的特性、类型和标识符的含义与类中的事件声明（§10.8）相同。

接口事件的类型必须是输入安全的。

### 13.2.4 接口索引器

接口索引器使用 interface-indexer-declaration 声明：

```
interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }
```

接口索引器声明的特性、类型和形参列表的含义与类中的索引器声明（§10.9）相同。

接口索引器声明的访问器与类索引器声明（§10.9）的访问器相对应，不同之处在于访问器主体必须始终是一个分号。因此，访问器仅指示该索引器是可读写、只读还是只写。

### 13.2.5 接口成员访问

接口成员通过形式为 I.M 和 I[A] 的成员访问（§7.6.4）和索引器访问（§7.6.6.2）表达式进行访问，其中 I 是接口类型，M 是该接口类型的方法、属性或事件，A 是索引器参数列表。

对于严格单一继承的接口（继承链中的每个接口恰好有零个或一个直接基接口），成员查找（§7.4）、方法调用（§7.6.5.1）和索引器访问（§7.6.6.2）规则的效果与类和结构体完全相同：派生程度更高的成员会隐藏派生程度更低且具有相同名称或签名的成员。然而，对于多重继承的接口，当两个或更多不相关的基接口声明了具有相同名称或签名的成员时，可能会产生歧义。本节展示了此类情况的几个示例。在所有情况下，都可以使用显式转换来解决歧义。

例如

```
interface IList
{
    int Count { get; set; }
}
interface ICounter
{
    void Count(int i);
}
interface IListCounter: IList, ICounter {}
class C
{
    void Test(IListCounter x) {    // Error
        x.Count(1);                 // Error
        x.Count = 1;                // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1);     // Ok, invokes ICounter.Count
    }
}
```

前两个语句会导致编译时错误，因为在 IListCounter 中对 Count 的成员查找（§7.4）存在歧义。如示例所示，可以通过将 x 转换为适当的基接口类型来解决歧义。此类转换没有运行时开销——它们只是在编译时将实例视为派生程度较低的类型。

例如

```
interface IInteger
{
    void Add(int i);
}
interface IDouble
{
    void Add(double d);
}
interface INumber: IInteger, IDouble {}
class C
{
    void Test(INumber n) {
        n.Add(1);       // Invokes IInteger.Add
        n.Add(1.0);     // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);   // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);    // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §7.5.3 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换后，只有一个候选方法，因此不会产生歧义。

例如

```
interface IBase
{
    void F(int i);
}
interface ILeft: IBase
{
    new void F(int i);
}
interface IRight: IBase
{
    void G();
}
interface IDerived: ILeft, IRight {}
```

```csharp
class A
{
    void Test(IDerived d) {
        d.F(1);        // Invokes ILeft.F
        ((IBase)d).F(1);   // Invokes IBase.F
        ((ILeft)d).F(1);   // Invokes ILeft.F
        ((IRight)d).F(1);  // Invokes IBase.F
    }
}
```

成员 IBase.F 被成员 ILeft.F 隐藏。因此，调用 d.F(1) 选择 ILeft.F，尽管 IBase.F 在经由 IRight 的访问路径中似乎并未被隐藏。

多重继承接口中隐藏的直观规则很简单：如果一个成员在任意访问路径中被隐藏，那么它在所有访问路径中都被隐藏。因为从 IDerived 经 ILeft 到 IBase 的访问路径隐藏了 IBase.F，所以该成员在从 IDerived 经 IRight 到 IBase 的访问路径中也被隐藏。

## 13.3 完全限定的接口成员名称

接口成员有时通过其完全限定名称来引用。接口成员的完全限定名称由声明该成员的接口名称、一个点以及该成员的名称组成。成员的完全限定名称引用声明该成员的接口。例如，给定以下声明：

```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}
```

Paint 的完全限定名称是 IControl.Paint，SetText 的完全限定名称是 ITextBox.SetText。

在上面的示例中，不能将 Paint 引用为 ITextBox.Paint。

当接口是命名空间的一部分时，接口成员的完全限定名称包含命名空间名称。例如

```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

这里，Clone 方法的完全限定名称是 System.ICloneable.Clone。

## 13.4 接口实现

类和结构体可以实现接口。为了表示某个类或结构体直接实现某个接口，需要将该接口的标识符包含在类或结构体的基类列表中。例如：

```csharp
interface ICloneable
{
    object Clone();
}
```

```csharp
interface IComparable
{
    int CompareTo(object other);
}
class ListEntry: ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

直接实现某个接口的类或结构体，也会隐式地直接实现该接口的所有基接口。即使类或结构体没有在基类列表中显式列出所有基接口，这一点也成立。例如：

```csharp
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
class TextBox: ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

这里，类 TextBox 实现了 IControl 和 ITextBox。

当类 C 直接实现某个接口时，从 C 派生的所有类也隐式地实现该接口。类声明中指定的基接口可以是构造的接口类型（§4.4）。基接口本身不能是类型参数，但可以涉及范围内的类型参数。下面的代码演示了类如何实现和扩展构造类型：

```csharp
class C<U,V> {}
interface I1<V> {}
class D: C<string,int>, I1<string> {}
class E<T>: C<int,T>, I1<T> {}
```

泛型类声明的基接口必须满足 §13.4.2 中描述的唯一性规则。

### 13.4.1 显式接口成员实现

为了实现接口，类或结构体可以声明显式接口成员实现。显式接口成员实现是引用完全限定的接口成员名称的方法、属性、事件或索引器声明。例如：

```csharp
interface IList<T>
{
    T[] GetElements();
}
interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}
```



接口索引器的类型如果有 get 访问器则应为输出安全，如果有 set 访问器则应为输入安全。

### 18.4.6 接口成员访问

接口成员是通过成员访问 (§12.7.5) 和索引器访问 (§12.7.7.3) 表达式以 I.M 和 I[A] 的形式访问的，其中 I 是接口类型，M 是该接口类型的方法、属性或事件，A 是索引器参数列表。

对于严格单继承的接口（继承链中的每个接口恰好有零个或一个直接基接口），成员查找 (§12.5)、方法调用 (§12.7.6.2) 和索引器访问 (§12.7.7.3) 规则的效果与类和结构完全相同：更派生的成员会隐藏具有相同名称或签名的更低层成员。然而，对于多继承接口，当两个或多个不相关的基接口声明具有相同名称或签名的成员时，可能会出现歧义。本小节展示了若干示例，其中一些会导致歧义，而另一些则不会。在所有情况下，都可以使用显式转换来解决歧义。

[Example: 以下代码中

```csharp
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
    void Test(IListCounter x) {
        x.Count(1);        // Error
        x.Count = 1;       // Error
        ((IList)x).Count = 1;   // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1); // Ok, invokes ICounter.Count
    }
}
```

前两个语句会导致编译时错误，因为在 IListCounter 中 Count 的成员查找 (§12.5) 是不明确的。如示例所示，通过将 x 转换为适当的基接口类型可以解决歧义。此类转换没有运行时成本——它们仅在编译时将实例视为更低派生类型。 end example]

[Example: 以下代码中

```csharp
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
        n.Add(1);            // Invokes IInteger.Add
        n.Add(1.0);          // Only IDouble.Add is applicable
        ((IInteger)n).Add(1); // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);  // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §12.6.4 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换时，只有一个候选方法，因此没有歧义。 end example]

[Example: 以下代码中

```csharp
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
class A
{
    void Test(IDerived d) {
        d.F(1);               // Invokes ILeft.F
        ((IBase)d).F(1);      // Invokes IBase.F
        ((ILeft)d).F(1);      // Invokes ILeft.F
        ((IRight)d).F(1);     // Invokes IBase.F
    }
}
```

IBase.F 成员被 ILeft.F 成员隐藏。因此调用 d.F(1) 选择 ILeft.F，即使 IBase.F 在通过 IRight 导致访问路径中似乎未被隐藏。

多继承接口中隐藏的直观规则很简单：只要成员在任何访问路径中被隐藏，它就在所有访问路径中被隐藏。因为从 IDerived 到 ILeft 再到 IBase 的访问路径隐藏了 IBase.F，所以该成员也在从 IDerived 到 IRight 再到 IBase 的访问路径中被隐藏。 end example]

## 18.5 限定接口成员名称

接口成员有时通过其限定接口成员名称引用。接口成员的限定名称由声明该成员的接口的名称、一个点以及成员的名称组成。成员的限定名称引用声明该成员的接口。[Example: 给定以下声明

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

Paint 的限定名称为 IControl.Paint，SetText 的限定名称为 ITextBox.SetText。在上面的示例中，不可能将 Paint 引用为 ITextBox.Paint。 end example

当接口属于命名空间的一部分时，限定接口成员名称可以包含命名空间名称。[Example:

```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

在 System 命名空间内，ICloneable.Clone 和 System.ICloneable.Clone 都是 Clone 方法的限定接口成员名称。 end example]

## 18.6 接口实现

### 18.6.1 通用

接口可以由类和结构实现。为了表示类或结构直接实现接口，接口包含在该类或结构的基类列表中。[Example:

```csharp
interface ICloneable
{
    object Clone();
}
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

end example]

直接实现接口的类或结构还隐式实现该接口的所有基接口。即使类或结构在基类列表中没有显式列出所有基接口也是如此。[Example:

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

在这里，类 TextBox 同时实现了 IControl 和 ITextBox。 end example]

当类 C 直接实现接口时，从 C 派生的所有类也隐式实现该接口。

类声明中指定的基接口可以是构造接口类型 (§9.4, §18.2)。

[Example: 以下代码说明了类如何实现构造接口类型：

```csharp
class C<U,V> {}
interface I1<V> {}
class D: C<string,int>, I1<string> {}
class E<U>: C<U,int>, I1<U> {}
```

end example]

泛型类声明的基接口应满足 §18.6.3 中描述的唯一性规则。

### 18.6.2 显式接口成员实现

为了实现接口的目的，类或结构可以声明显式接口成员实现。显式接口成员实现是对引用限定接口成员名称的方法、属性、事件或索引器声明。[Example:

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
class List<T>: IList<T>, IDictionary<int,T>
{
    public T[] GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

这里 `IDictionary<int,T>.this` 和 `IDictionary<int,T>.Add` 是显式接口成员实现。 end example]

[Example: 在某些情况下，接口成员的名称可能不适合实现类，在这种情况下，接口成员可以使用显式接口成员实现来实现。例如，实现文件抽象的类很可能会实现一个 `Close` 成员函数，其效果是释放文件资源，并使用显式接口成员实现实现 `IDisposable` 接口的 `Dispose` 方法：

```csharp
interface IDisposable
{
    void Dispose();
}
class MyFile: IDisposable
{
    void IDisposable.Dispose()
    {
        Close();
    }
    public void Close()
    {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

end example]

不可能通过其限定接口成员名称在方法调用、属性访问、事件访问或索引器访问中访问显式接口成员实现。显式接口成员实现只能通过接口实例访问，在这种情况下仅通过其成员名称引用。

如果显式接口成员实现包含除 extern 或 async 之外的任何修饰符 (§15.6)，则为编译时错误。

如果显式接口方法实现包含 *type-parameter-constraints-clauses*，则为编译时错误。泛型显式接口方法实现的约束继承自接口方法。[Note: 显式接口成员实现与其他成员具有不同的可访问性特征。因为显式接口成员实现永远无法通过方法调用或属性访问中的限定接口成员名称访问，所以在某种意义上它们是私有的。然而，由于它们可以通过接口访问，所以在某种意义上它们也与声明它们的接口一样公开。

显式接口成员实现主要有两个目的：

- 因为显式接口成员实现无法通过类或结构实例访问，所以它们允许接口实现被排除在类或结构的公共接口之外。这在类或结构实现对该类或结构的消费者不感兴趣的内部接口时特别有用。
- 显式接口成员实现允许对具有相同签名的接口成员进行消歧。没有显式接口成员实现，类或结构就不可能对具有相同签名和返回类型的接口成员具有不同的实现，因为类或结构就不可能对具有相同签名但返回类型不同的接口成员有任何实现。

end note]

对于显式接口成员实现有效，类或结构必须在其基类列表中命名一个包含成员的接口，该成员的限定接口成员名称、类型、类型参数数量和参数类型与显式接口成员实现完全匹配。如果接口函数成员具有参数数组，则相关显式接口成员实现的相应参数允许但不是必须具有 params 修饰符。如果接口函数成员没有参数数组，则相关显式接口成员实现不得具有参数数组。[Example: 因此，在以下类中

```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}    // invalid
}
```

IComparable.CompareTo 的声明导致编译时错误，因为 IComparable 未列在 Shape 的基类列表中，也不是 ICloneable 的基接口。同样，在以下声明中

```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}
class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // invalid
}
```

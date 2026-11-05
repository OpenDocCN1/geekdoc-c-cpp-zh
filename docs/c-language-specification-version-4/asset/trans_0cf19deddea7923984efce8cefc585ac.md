
```
class List<T>: IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

这里 IDictionary<int,T>.this 和 IDictionary<int,T>.Add 是显式接口成员实现。

在某些情况下，接口成员的名称可能不适合实现该接口的类，在这种情况下，可以使用显式接口成员实现来实现该接口成员。例如，实现文件抽象的类很可能会实现一个 Close 成员函数，其作用是释放文件资源，并使用显式接口成员实现来实现 IDisposable 接口的 Dispose 方法：

```
interface IDisposable
{
    void Dispose();
}
class MyFile: IDisposable
{
    void IDisposable.Dispose() {
        Close();
    }
    public void Close() {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

不可能通过其完全限定名在方法调用、属性访问或索引器访问中访问显式接口成员实现。显式接口成员实现只能通过接口实例访问，在这种情况下仅通过其成员名引用。

显式接口成员实现包含访问修饰符是编译时错误，包含 abstract、virtual、override 或 static 修饰符也是编译时错误。

显式接口成员实现与其他成员具有不同的可访问性特征。因为显式接口成员实现永远无法通过其完全限定名在方法调用或属性访问中访问，所以在某种意义上它们是私有的。然而，由于它们可以通过接口实例访问，所以在某种意义上它们也是公共的。

显式接口成员实现主要有两个用途：

- 因为显式接口成员实现无法通过类或结构实例访问，所以它们允许将接口实现从类或结构的公共接口中排除。这在类或结构实现对该类或结构的消费者而言不感兴趣的内部接口时特别有用。
- 显式接口成员实现允许对具有相同签名的接口成员进行消歧。没有显式接口成员实现，类或结构就不可能对具有相同签名和返回类型的接口成员具有不同的实现，也就不可能对具有相同签名但返回类型不同的接口成员有任何实现。

要使显式接口成员实现有效，类或结构必须在其基类列表中命名一个接口，该接口包含一个成员，其完全限定名、类型和参数类型与显式接口成员实现完全匹配。因此，在下面的类中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}  // invalid
}
```

IComparable.CompareTo 的声明导致编译时错误，因为 IComparable 未列在 Shape 的基类列表中，也不是 ICloneable 的基接口。同样，在以下声明中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}
class Ellipse: Shape
{
    object ICloneable.Clone() {...}  // invalid
}
```

Ellipse 中 ICloneable.Clone 的声明导致编译时错误，因为 ICloneable 未明确列在 Ellipse 的基类列表中。

接口成员的完全限定名必须引用声明该成员的接口。因此，在以下声明中

```
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
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```

Paint 的显式接口成员实现必须写成 IControl.Paint。

## 13.4.2 已实现接口的唯一性

泛型类型声明所实现的接口对于所有可能的构造类型必须保持唯一。没有此规则，就不可能为某些构造类型确定要调用的正确方法。例如，假设允许泛型类声明写成如下形式：

```
interface I<T>
{
    void F();
}
class X<U,V>: I<U>, I<V>    // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

如果允许这样做，则在以下情况下将无法确定要执行哪段代码：

```
I<int> x = new X<int,int>();
x.F();
```

为了确定泛型类型声明的接口列表是否有效，执行以下步骤：

- 设 L 为在泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已存在接口的任何基接口添加到 L。
- 从 L 中删除任何重复项。
- 如果从 C 创建的任何可能构造类型在将类型参数代入 L 之后会导致 L 中的两个接口相同，则 C 的声明无效。确定所有可能的构造类型时不考虑约束声明。

在上面的类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为 U 和 V 为相同类型的任何构造类型都会导致这两个接口成为相同的类型。

可以在不同的继承级别指定接口并统一：

```
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {}
}
class Derived<U,V>: Base<U>, I<V>  // Ok
{
    void I<V>.F() {...}
}
```

此代码有效，即使 Derived<U,V> 同时实现了 I<U> 和 I<V>。代码

```
I<int> x = new Derived<int,int>();
x.F();
```

调用 Derived 中的方法，因为 Derived<int,int> 有效地重新实现了 I<int> (§13.4.6)。

## 13.4.3 泛型方法的实现

当泛型方法隐式实现接口方法时，每个方法类型参数给出的约束在两个声明中必须等价（在用适当的类型参数替换任何接口类型参数之后），其中方法类型参数按从左到右的序数位置标识。

然而，当泛型方法显式实现接口方法时，实现方法上不允许有约束。相反，约束是从接口方法继承的

```
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}
class C: I<object,C,string>
{
    public void F<T>(T t) {...}            // Ok
    public void G<T>(T t) where T: C {...} // Ok
    public void H<T>(T t) where T: string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在用相应的类型参数替换接口类型参数后，约束与接口中的约束匹配。方法 C.H<T> 的约束是错误，因为密封类型（本例中为 string）不能用作约束。省略约束也将是错误，因为隐式接口方法实现的约束必须匹配。因此，不可能隐式实现 I<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```
class C : I<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void I<object,C,string>.H<T>(T t) {
        string s = t; // Ok
        H<T>(t);
    }
}
```

在此示例中，显式接口成员实现调用了一个具有严格更弱约束的公共方法。请注意，从 t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中无法表达。

## 13.4.4 接口映射

类或结构必须为列在其基类列表中的接口的所有成员提供实现。在实现类或结构中查找接口成员实现的过程称为接口映射。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员声明，则该成员是 I.M 的实现。如果有多个成员匹配，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 是构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型参数使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。请注意，接口的成员包括从基接口继承的那些成员。

出于接口映射的目的，类成员 A 与接口成员 B 匹配的条件是：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。

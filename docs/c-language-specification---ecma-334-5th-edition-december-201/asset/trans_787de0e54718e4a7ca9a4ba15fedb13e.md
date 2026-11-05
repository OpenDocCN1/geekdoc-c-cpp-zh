
Ellipse 中 ICloneable.Clone 的声明会导致编译时错误，因为 ICloneable 并未显式列在 Ellipse 的基类列表中。end example]

显式接口成员实现的限定接口成员名称应引用该成员被声明的接口。[Example: 因此，在以下声明中

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

Paint 的显式接口成员实现必须写成 IControl.Paint，而不是 ITextBox.Paint。end example]

## 18.6.3 已实现接口的唯一性

泛型类型声明所实现的接口对于所有可能构造的类型都应保持唯一。没有此规则，就无法确定某些构造类型的正确调用方法。[Example: 假设允许泛型类声明写成如下形式：

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

如果允许这样做，则在以下情况下将无法确定执行哪段代码：

```
I<int> x = new X<int,int>();
x.F();
```

end example]

为了确定泛型类型声明的接口列表是否有效，执行以下步骤：

- 将 L 设为在泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已存在接口的任何基接口添加到 L。
- 从 L 中删除任何重复项。
- 如果从 C 创建的任何可能构造类型在将类型参数代入 L 之后会导致 L 中的两个接口相同，则 C 的声明无效。确定所有可能的构造类型时不考虑约束声明。

[Note: 在上面的类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为 U 和 V 为相同类型的任何构造类型都会导致这两个接口成为相同的类型。end note]

不同继承级别指定的接口可能统一：

```
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {...}
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

调用 Derived 中的方法，因为 Derived<int,int> 有效地重新实现了 I<int>（§18.6.7）。

## 18.6.4 泛型方法的实现

当泛型方法隐式实现接口方法时，每个方法类型参数给出的约束在两个声明中应等价（在用适当的类型参数替换任何接口类型参数之后），其中方法类型参数按从左到右的序数位置标识。[Example: 在以下代码中：

```
interface I<X, Y, Z>
{
    void F<T>(T t) where T: X;
    void G<T>(T t) where T: Y;
    void H<T>(T t) where T: Z;
}

class C: I<object,C,string>
{
    public void F<T>(T t) {...}          // Ok
    public void G<T>(T t) where T: C {...}   // Ok
    public void H<T>(T t) where T: string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在用相应的类型参数替换接口类型参数后，约束与接口中的约束匹配。方法 C.H<T> 的约束是错误，因为密封类型（本例中为 string）不能用作约束。省略约束也是错误，因为隐式接口方法实现的约束必须匹配。因此，不可能隐式实现 I<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```
class C: I<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void I<object,C,string>.H<T>(T t) {
        string s = t;  // Ok
        H<T>(t);
    }
}
```

在这种情况下，显式接口成员实现调用具有严格更弱约束的公共方法。从 t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中无法表达。end example]

[Note: 当泛型方法显式实现接口方法时，实现方法上不允许有约束（§15.7.1, §18.6.2）end note]。

## 18.6.5 接口映射

类或结构应提供基类列表中列出的接口的所有成员的实现。在实现类或结构中查找接口成员实现的过程称为 *接口映射*。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员声明，则该成员是 I.M 的实现。如果有多个成员匹配，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 为构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型参数使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。接口的成员包括从基接口继承的成员。

构造接口类型的成员被认为已将任何类型参数替换为 §15.3.3 中指定的相应类型参数。[Example: 例如，给定泛型接口声明：

```
interface I<T>
{
    T F(int x, T[,] y);
    T this[int y] { get; }
}
```

构造接口 I<string[]> 具有以下成员：

```
string[] F(int x, string[,][] y);
string[] this[int y] { get; }
```

end example

就接口映射而言，类或结构成员 A 与接口成员 B 匹配的条件为：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。
- A 和 B 都是索引器，并且 A 和 B 的类型和形式参数列表相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。

接口映射算法的显著含义是：

- 在确定实现接口成员的类或结构成员时，显式接口成员实现优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

[Example: 在以下代码中

```
interface ICloneable
{
    object Clone();
}
class C: ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```

C 的 ICloneable.Clone 成员成为 ICloneable 中 Clone 的实现，因为显式接口成员实现优先于其他成员。end example]

如果类或结构实现两个或多个包含具有相同名称、类型和参数类型的成员的接口，则可以将这些接口成员中的每一个映射到单个类或结构成员。[Example:

```
interface IControl
{
    void Paint();
}
interface IForm
{
    void Paint();
}
class Page: IControl, IForm
{
    public void Paint() {...}
}
```

在这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然，也可以为这两种方法分别提供显式接口成员实现。end example]

如果类或结构实现包含隐藏成员的接口，则某些成员可能需要通过显式接口成员实现来实现。[Example:

```
interface IBase
{
    int P { get; }
}
interface IDerived: IBase
{
    new int P();
}
```

此接口的实现至少需要一个显式接口成员实现，并将采用以下形式之一

```
class C: IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}
class C: IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}
class C: IDerived
{
    int IBase.P { get {...} }

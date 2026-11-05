
### 17.6.4 泛型方法的实现

当泛型方法隐式实现接口方法时，每个方法类型参数给出的约束在两个声明中应当是等价的（在将任何接口类型参数替换为适当的实参类型之后），其中方法类型参数按从左到右的序数位置标识。

*示例：* 如下代码所示：

```csharp
interface I<X, Y, Z>
{
    void F<T>(T t) where T : X;
    void G<T>(T t) where T : Y;
    void H<T>(T t) where T : Z;
}

class C : I<object, C, string>
{
    public void F<T>(T t) {...}             // Ok
    public void G<T>(T t) where T : C {...} // Ok
    public void H<T>(T t) where T : string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在将接口类型参数替换为相应的实参类型后，约束与接口中的约束相匹配。方法 C.H<T> 的约束是一个错误，因为密封类型（本例中为 string）不能用作约束。省略该约束也将是一个错误，因为隐式接口方法实现的约束必须匹配。因此，不可能隐式实现 I<object,C,string>.H<T>。该接口成员只能使用显式接口成员实现来实现：

```csharp
class C : I<object, C, string>
{
    ...
    public void H<U>(U u) where U : class {...}

    void I<object, C, string>.H<T>(T t)
    {
        string s = t; // Ok
        H<T>(t);
    }
}
```

在这种情况下，显式接口成员实现调用了一个具有严格更弱约束的公共方法。t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中未表达。 *结束示例*

*注意：* 当泛型方法显式实现接口方法时，实现方法上不允许有约束（§14.7.1, §17.6.2）。 *结束注意*

### 17.6.5 接口映射

类或结构必须为列在该类或结构基类列表中的接口的所有成员提供实现。在实现类或结构中定位接口成员实现的过程称为 *接口映射*。

类或结构 C 的接口映射为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现的声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员的声明，则该成员是 I.M 的实现。如果匹配的成员多于一个，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 为构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型实参使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。接口的成员包括从基接口继承的那些成员。

构造接口类型的成员被认为已将任何类型参数替换为 §14.3.3 中指定的相应类型实参。

*示例：* 例如，给定泛型接口声明：

```csharp
interface I<T>
{
    T F(int x, T[] y);
    T this[int y] { get; }
}
```

构造的接口 I<string[]> 具有以下成员：

```csharp
string[] F(int x, string[][] y);
string[] this[int y] { get; }
```

*结束示例*

出于接口映射的目的，类或结构成员 A 与接口成员 B 匹配的条件是：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，并且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。
- A 和 B 都是索引器，并且 A 和 B 的类型和形式参数列表相同，并且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。

接口映射算法的显著含义是：

- 在确定实现接口成员的类或结构成员时，显式接口成员实现优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

*示例：* 在以下代码中

```csharp
interface ICloneable
{
    object Clone();
}

class C : ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```

C 的 ICloneable.Clone 成员成为 ICloneable 中 Clone 的实现，因为显式接口成员实现优先于其他成员。

*结束示例*

如果类或结构实现两个或多个包含名称、类型和参数类型相同的成员的接口，则可以将这些接口成员中的每个都映射到单个类或结构成员上。

*示例：*

```csharp
interface IControl
{
    void Paint();
}

interface IForm
{
    void Paint();
}

class Page : IControl, IForm
{
    public void Paint() {...}
}
```

这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然，也可以为这两种方法分别提供显式的接口成员实现。

*结束示例*

如果类或结构实现包含隐藏成员的接口，则可能需要通过显式接口成员实现来实现某些成员。

*示例：*

```csharp
interface IBase
{
    int P { get; }
}

interface IDerived : IBase
{
    new int P();
}
```

该接口的实现至少需要一个显式接口成员实现，并将采用以下形式之一

```csharp
class C : IDerived
{
    int IBase.P { get; }
    int IDerived.P() {...}
}
```

```csharp
class C : IDerived
{
    public int P { get; }
    int IDerived.P() {...}
}
```

```csharp
class C : IDerived
{
    int IBase.P { get; }
    public int P() {...}
}
```

*结束示例*

当一个类实现多个具有相同基接口的接口时，基接口只能有一个实现。

示例： 在以下代码中

```csharp
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

interface IListBox : IControl
{
    void SetItems(string[] items);
}

class ComboBox : IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```

不可能为基类列表中命名的 IControl、由 ITextBox 继承的 IControl 以及由 IListBox 继承的 IControl 分别提供实现。事实上，这些接口没有单独身份的概念。相反，ITextBox 和 IListBox 的实现共享同一个 IControl 实现，并且 ComboBox 只是被认为实现了三个接口，IControl、ITextBox 和 IListBox。

*结束示例*

基类的成员参与接口映射。

示例： 在以下代码中

```csharp
interface Interface1
{
    void F();
}

class Class1
{
    public void F() {}
    public void G() {}
}

class Class2 : Class1, Interface1
{
    public new void G() {}
}
```

Class1 中的方法 F 用于 Class2 对 Interface1 的实现。

*结束示例*

### 17.6.6 接口实现继承

类继承其基类提供的所有接口实现。

在不显式重新实现接口的情况下，派生类不能以任何方式更改其从基类继承的接口映射。

示例： 在以下声明中

```csharp
interface IControl
{
    void Paint();
}

class Control : IControl
{
    public void Paint() {...}
}

class TextBox : Control
{
    public new void Paint() {...}
}
```

TextBox 中的 Paint 方法隐藏了 Control 中的 Paint 方法，但它不会更改 Control.Paint 到 IControl.Paint 的映射，并且通过类实例和接口实例对 Paint 的调用将具有以下效果

```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint(); // invokes Control.Paint();
```

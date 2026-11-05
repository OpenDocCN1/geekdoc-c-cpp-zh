
```csharp
class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。

当一个类实现接口时，它隐式地也实现了该接口的所有基接口。同样，接口的重实现也隐式地是对该接口所有基接口的重实现。例如：

```csharp
interface IBase
{
    void F();
}

interface IDerived: IBase
{
    void G();
}

class C: IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D: C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

这里，IDerived 的重实现也重实现了 IBase，将 IBase.F 映射到 D.F。

> JON SKEET 虽然这种做法在某些情况下确实很有用，但通常应避免使用，因为它会造成极大的混淆。通常，对同一对象使用相同的方法名和相同参数列表的每次调用都应导致调用相同的方法。有许多方法可以偏离这种理想情况，它们都应极其谨慎地使用，并且仅在绝对必要时才使用。

## 13.4.7 抽象类和接口

与非抽象类一样，抽象类必须为类基类列表中列出的接口的所有成员提供实现。然而，抽象类允许将接口方法映射到抽象方法。例如：

```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些方法必须在派生自 C 的非抽象类中被重写。

请注意，显式接口成员实现不能是抽象的，但显式接口成员实现当然可以调用抽象方法。例如：

```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

这里，派生自 C 的非抽象类将被要求重写 FF 和 GG，从而提供 IMethods 的实际实现。

## 14. 枚举

枚举类型是一种不同的值类型（§4.1），它声明了一组命名常量。

> JON SKEET 值得注意的是，这些“命名常量”本质上只是数字。它们无法表达行为，这与 C# 中的几乎所有其他内容相反。这是 Java 比 C# 更具表达力的极少数领域之一。在 Java 中，枚举具有更大的功能：例如，枚举可以声明方法然后为特定值重写它们。虽然可以在 C# 中模拟 Java 枚举的一些功能，但未来版本中语言（和框架）的支持将非常受欢迎。

示例

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

声明了一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。

### 14.1 枚举声明

枚举声明声明一个新的枚举类型。枚举声明以关键字 enum 开始，并定义枚举的名称、可访问性、底层类型和成员。

```
enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }
```

每个枚举类型都有一个对应的整型，称为该枚举类型的底层类型。此底层类型必须能够表示枚举中定义的所有枚举值。枚举声明可以显式声明 byte、sbyte、short、ushort、int、uint、long 或 ulong 的底层类型。请注意，char 不能用作底层类型。未显式声明底层类型的枚举声明的底层类型为 int。

> JON SKEET 这是语言中唯一几个地方之一，你不能用其完整等价类型替换类型的“简写”版本。例如，你不能按如下方式声明 Color 枚举：
> enum Color: System.Int64 { ... }

示例

```csharp
enum Color : long
{
    Red,
    Green,
    Blue
}
```

声明了一个底层类型为 long 的枚举。开发人员可能会选择使用 long 作为底层类型，如示例所示，以便使用在 long 范围内但不在 int 范围内的值，或为将来保留此选项。

### 14.2 枚举修饰符

enum-declaration 可选择包含一系列枚举修饰符：

```
enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier

enum-modifier:
    new
    public
    protected
    internal
    private
```

在枚举声明中，同一个修饰符出现多次是编译时错误。

枚举声明的修饰符与类声明（§10.1.1）的修饰符具有相同的含义。然而，请注意，abstract 和 sealed 修饰符不允许出现在枚举声明中。枚举不能是抽象的，也不允许派生。

### 14.3 枚举成员

枚举类型声明的主体定义零个或多个枚举成员，它们是枚举类型的命名常量。两个枚举成员不能具有相同的名称。

```
enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression
```

> **弗拉基米尔·雷舍特尼科夫** 在 Microsoft 对 C# 的实现中，枚举成员不能命名为 value__，因为此名称保留用于枚举的内部表示。

每个枚举成员都有一个关联的常量值。此值的类型是包含枚举的底层类型。每个枚举成员的常量值必须在枚举的底层类型范围内。示例

```csharp
enum Color : uint
{
  Red = -1,
  Green = -2,
  Blue = -3
}
```

导致编译时错误，因为常量值 -1、-2 和 -3 不在底层整型 uint 的范围内。

多个枚举成员可以共享相同的关联值。示例

```csharp
enum Color
{
  Red,
  Green,
  Blue,
  Max = Blue
}
```

显示了一个枚举，其中两个枚举成员——Blue 和 Max——具有相同的关联值。

枚举成员的关联值是隐式或显式赋值的。如果枚举成员的声明具有常量表达式初始值设定项，则该常量表达式的值隐式转换为枚举的底层类型，即为该枚举成员的关联值。如果枚举成员的声明没有初始值设定项，则其关联值按如下方式隐式设置：

- 如果枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为 0。
- 否则，枚举成员的关联值是通过将文本上前一个枚举成员的关联值增加 1 得到。此增加后的值必须在底层类型可以表示的值范围内；否则，会发生编译时错误。

> JON SKEET 对于 [Flags] 枚举，使用默认值几乎总是错误的做法，其中值通常应为 1、2、4、8 等——通常还有一个值为 0 的“None”。语言本可以帮助避免开发人员意外使用不适当的值，但很难判断在不增加超过应有复杂性的情况下能否很好地实现这一目标。

> BILL WAGNER 我更希望看到以下示例使用扩展方法实现。“Color.Red.StringFromColor()”在我看来比“StringFromColor(Color.Red)”读起来更好。
>
> 这种技术也开始解决了 Jon 关于无法表达行为的评论。

## 示例

```csharp
using System;
enum Color
{
    Red,
    Green = 10,
    Blue
}
```

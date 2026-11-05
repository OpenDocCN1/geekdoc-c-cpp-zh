

```csharp
class Base : IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}

class Derived : Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。

*示例结束*

当一个类实现一个接口时，它也会隐式实现该接口的所有基接口。同样，接口的重新实现也隐式地是该接口所有基接口的重新实现。

*示例：*

```csharp
interface IBase
{
    void F();
}

interface IDerived : IBase
{
    void G();
}

class C : IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D : C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

这里，IDerived 的重新实现也重新实现了 IBase，将 IBase.F 映射到 D.F。

*示例结束*

## 18.6.8 抽象类和接口

与非抽象类一样，抽象类应提供该类的基类列表中列出的接口的所有成员的实现。但是，允许抽象类将接口方法映射到抽象方法。

示例：

```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C : IMethods
{
    public abstract void F();
    public abstract void G();
}
```

这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些方法应在派生自 C 的非抽象类中重写。

示例结束

显式接口成员实现不能是抽象的，但显式接口成员实现当然可以调用抽象方法。

示例：

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

示例结束

## 19. 枚举

### 19.1 概述

*枚举类型*是一种独特的值类型（§8.3），它声明一组命名常量。

*示例：以下示例*

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

声明了一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。

*示例结束*

### 19.2 枚举声明

枚举声明声明一个新的枚举类型。枚举声明以关键字 `enum` 开头，并定义枚举的名称、可访问性、基础类型和成员。

```
enum_declaration
    : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
    ;

enum_base
    : ':' integral_type
    | ':' integral_type_name
    ;

integral_type_name
    : type_name // Shall resolve to an integral type other than char
    ;

enum_body
    : '{' enum_member_declarations? '}'
    | '{' enum_member_declarations ',' '}'
    ;
```

每个枚举类型都有一个对应的整型，称为该枚举类型的*基础类型*。此基础类型应能够表示枚举中定义的所有枚举值。如果存在 *enum_base*，则它显式声明基础类型。基础类型应是除 `char` 之外的*整型*（§8.3.6）之一。基础类型可以通过 *integral_type*（§8.3.5）或 *integral_type_name* 指定。*integral_type_name* 的解析方式与 *type_name*（§7.8.1）相同，包括考虑任何 using 指令（§14.5）。

> *注意：* `char` 类型不能用作基础类型，无论是通过关键字还是通过 `integral_type_name`。*注意结束*

未显式声明基础类型的枚举声明，其基础类型为 int。

示例：以下示例

```csharp
enum Color : long
{
    Red,
    Green,
    Blue
}
```

声明了一个基础类型为 long 的枚举。

示例结束

注意：开发者可能选择使用 long 作为基础类型，如示例所示，以便能够使用位于 long 范围内但不在 int 范围内的值，或为将来保留此选项。注意结束

注意：C# 允许在 enum_body 中出现尾随逗号，就像它允许在 array_initializer（§17.7）中出现尾随逗号一样。注意结束

枚举声明不能包含类型参数列表，但嵌套在泛型类声明或泛型结构声明内的任何枚举都是泛型枚举声明，因为创建构造类型（§8.4）时应提供包含类型的类型实参。

### 19.3 枚举修饰符

枚举声明可以选择性地包含一系列枚举修饰符：

```
enum_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;
```

同一修饰符在枚举声明中出现多次是编译时错误。

枚举声明的修饰符与类声明（§15.2.2）的修饰符含义相同。但是，枚举声明中不允许使用 abstract、sealed 和 static 修饰符。枚举不能是抽象的，也不允许派生。

### 19.4 枚举成员

枚举类型声明的体定义零个或多个枚举成员，这些成员是枚举类型的命名常量。任何两个枚举成员不能具有相同名称。

```
enum_member_declarations
    : enum_member_declaration (',' enum_member_declaration)*
    ;

enum_member_declaration
    : attributes? identifier ('=' constant_expression)?
    ;
```

每个枚举成员都有一个关联的常量值。此值的类型是包含该枚举的基础类型。每个枚举成员的常量值应在该枚举的基础类型的范围内。

示例：以下示例

```
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

导致编译时错误，因为常量值 -1、-2 和 -3 不在基础整型 uint 的范围内。

示例结束

多个枚举成员可以共享相同的关联值。

示例：以下示例

```
enum Color
{
    Red,
    Green,
    Blue,
    Max = Blue
}
```

展示了一个枚举，其中两个枚举成员——Blue 和 Max——具有相同的关联值。

示例结束

枚举成员的关联值通过隐式或显式方式赋值。如果枚举成员的声明具有 constant_expression 初始值设定项，则将该常量表达式的值隐式转换为枚举的基础类型后，即为该枚举成员的关联值。如果枚举成员的声明没有初始值设定项，则其关联值按如下方式隐式设置：

- 如果该枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为零。
- 否则，该枚举成员的关联值通过将文本上位于其前面的枚举成员的关联值加一获得。增加后的值应在基础类型可表示的值的范围内，否则发生编译时错误。

示例：以下示例

```csharp
enum Color
{
    Red,
    Green = 10,
    Blue
}

class Test
{
    static void Main()
    {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c)
    {
        switch (c)
        {
            case Color.Red:
                return $"Red = {(int) c}";
            case Color.Green:
                return $"Green = {(int) c}";
            case Color.Blue:
                return $"Blue = {(int) c}";
            default:
                return "Invalid color";
        }
    }
}
```

打印出枚举成员名称及其关联值。输出为：

```
Red = 0
Green = 10
Blue = 11
```

原因如下：

- 枚举成员 `Red` 被自动赋值为零（因为它没有初始值设定项，并且是第一个枚举成员）；
- 枚举成员 `Green` 被显式赋予值 `10`；
- 并且枚举成员 `Blue` 被自动赋值为比文本上位于其前面的成员大 1 的值。

*示例结束*

枚举成员的关联值不得直接或间接使用其自身关联枚举成员的值。除该循环性限制外，枚举成员初始值设定项可以自由引用其他枚举成员初始值设定项，而不论其文本位置如何。在枚举成员初始值设定项内，其他枚举成员的值始终被视为具有其基础类型，因此在引用其他枚举成员时不需要强制转换。

*示例：以下示例*

```csharp
enum Circular
{
    A = B,
    B
}
```

导致编译时错误，因为 `A` 和 `B` 的声明是循环的。`A` 显式依赖 `B`，而 `B` 隐式依赖 `A`。

*示例结束*


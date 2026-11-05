
## C# 语言规范

- 如果 S 具有类类型约束 A 且 T 具有类类型约束 B，则必须存在从 A 到 B 的同一性转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。
- 如果 S 还依赖于类型参数 U，且 U 具有类类型约束 A，而 T 具有类类型约束 B，则必须存在从 A 到 B 的同一性转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。

S 具有值类型约束而 T 具有引用类型约束是有效的。实际上，这将 T 限制为类型 System.Object、System.ValueType、System.Enum 以及任何接口类型。

如果类型参数的 where 子句包含构造函数约束（其形式为 `new()`），则可以使用 new 运算符创建该类型的实例（§7.6.10.1）。用于具有构造函数约束的类型参数的任何类型实参都必须具有公共无参数构造函数（对于任何值类型，此构造函数隐式存在），或者是具有值类型约束或构造函数约束的类型参数（有关详细信息，请参见 §10.1.5）。

以下是约束的示例：

```
interface IPrintable
{
    void Print();
}
interface IComparable<T>
{
    int CompareTo(T value);
}
interface IKeyProvider<T>
{
    T GetKey();
}
class Printer<T> where T : IPrintable { ... }
class SortedList<T> where T : IComparable<T> { ... }
class Dictionary<K,V>
    where K : IComparable<K>
    where V : IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

以下示例是错误的，因为它导致类型参数的依赖图中出现循环：

```
class Circular<S,T>
    where S : T
    where T : S    // Error, circularity in dependency graph
{
    ...
}
```

以下示例说明了其他无效情况：

```
class Sealed<S,T>
    where S : T
    where T : struct    // Error, T is sealed
{
    ...
}
class A { ... }
class B { ... }
class Incompat<S,T>
    where S: A, T
    where T: B    // Error, incompatible class-type constraints
{
    ...
}
class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A    // Error, A incompatible with struct
{
    ...
}
```

类型参数 T 的有效基类定义如下：

- 如果 T 没有主要约束或类型参数约束，则其有效基类为 object。
- 如果 T 具有值类型约束，则其有效基类为 System.ValueType。
- 如果 T 具有类类型约束 C 但没有类型参数约束，则其有效基类为 C。
- 如果 T 没有类类型约束但具有一个或多个类型参数约束，则其有效基类是其类型参数约束的有效基类集合中最包容的类型（§6.4.2）。一致性规则确保存在这样的最包容类型。
- 如果 T 同时具有类类型约束和一个或多个类型参数约束，则其有效基类是以下集合中最包容的类型（§6.4.2）：T 的类类型约束以及其类型参数约束的有效基类。一致性规则确保存在这样的最包容类型。
- 如果 T 具有引用类型约束但没有类类型约束，则其有效基类为 object。

为了这些规则的目的，如果 T 具有一个值类型约束 V，则改用 V 的最特定基类中为类类型的那个。这绝不会在显式给定的约束中发生，但当泛型方法的约束由重写方法声明或接口方法的显式实现隐式继承时可能发生。

这些规则确保有效基类始终是类类型。

类型参数 T 的有效接口集定义如下：

- 如果 T 没有次要约束，则其有效接口集为空。
- 如果 T 具有接口类型约束但没有类型参数约束，则其有效接口集为其接口类型约束集。
- 如果 T 没有接口类型约束但具有类型参数约束，则其有效接口集为其类型参数约束的有效接口集的并集。
- 如果 T 同时具有接口类型约束和类型参数约束，则其有效接口集为其接口类型约束集与其类型参数约束的有效接口集的并集。

如果类型参数具有引用类型约束，或者其有效基类不是 object 或 System.ValueType，则已知该类型参数为引用类型。

受约束的类型参数类型的值可用于访问约束所隐含的实例成员。在示例

```
interface IPrintable
{
    void Print();
}
class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```

中，可以直接在 x 上调用 IPrintable 的方法，因为 T 被约束为始终实现 IPrintable。

## 10.1.6 类体

类的类体定义该类的成员。

```
class-body:
    { class-member-declarations_opt }
```

## 10.2 分部类型

类型声明可以拆分到多个分部类型声明中。类型声明按照本节中的规则由其各部分构造而成，随后在程序的编译时和运行时处理的其余部分中将其视为单个声明。

如果类声明、结构声明或接口声明包含 partial 修饰符，则它表示分部类型声明。partial 不是关键字，仅当它在类型声明中紧接在 class、struct 或 interface 关键字之一之前，或在方法声明中紧接在类型 void 之前出现时，才作为修饰符起作用。在其他上下文中，它可以用作普通标识符。

分部类型声明的每个部分都必须包含 partial 修饰符。它必须具有相同的名称，并且与其他部分声明在同一命名空间或类型声明中。partial 修饰符指示类型声明的其他部分可能存在于其他地方，但不要求存在此类其他部分；具有单个声明的类型包含 partial 修饰符是有效的。

分部类型的所有部分必须一起编译，以便这些部分可以在编译时合并为单个类型声明。分部类型特别不允许扩展已编译的类型。

嵌套类型可以使用 partial 修饰符在多个部分中声明。通常，包含类型也使用 partial 声明，并且嵌套类型的每个部分在包含类型的不同部分中声明。

不允许在委托声明或枚举声明上使用 partial 修饰符。

### 10.2.1 特性

分部类型的特性通过以未指定的顺序合并每个部分的特性来确定。如果特性放置在多个部分上，则等效于在该类型上多次指定该特性。例如，以下两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

等效于如下声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

### 10.2.4 基类

当分部类声明包含基类指定时，它必须与包含基类指定的所有其他部分一致。如果分部类的任何部分都不包含基类指定，则基类变为 System.Object（§10.1.4.1）。

### 10.2.5 基接口

在多个部分中声明的类型的基接口集是在每个部分上指定的基接口的并集。特定基接口在每个部分上只能命名一次，但允许多个部分命名相同的基接口。任何给定基接口的成员必须只有一个实现。

在示例

```
partial class C: IA, IB {...}
partial class C: IC {...}
partial class C: IA, IB {...}
```

中，类 C 的基接口集为 IA、IB 和 IC。

通常，每个部分提供在该部分上声明的接口的实现；然而，这不是要求。一个部分可以为在不同部分上声明的接口提供实现：

```
partial class X
{
    int IComparable.CompareTo(object o) {...}
}
partial class X: IComparable
{
    ...
}
```

### 10.2.6 成员

除分部方法（§10.2.7）外，在多个部分中声明的类型的成员集只是每个部分中声明的成员集的并集。类型声明的所有部分的体共享同一声明空间（§3.3），并且每个成员（§3.7）的作用域延伸到所有部分的体。任何成员的可访问域始终包括封闭类型的所有部分；在一个部分中声明的私有成员可以从另一个部分自由访问。在类型的多个部分中声明同一成员是编译时错误，除非该成员是具有 partial 修饰符的类型。

```
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int y;
    }
}
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int z;
    }
}
```


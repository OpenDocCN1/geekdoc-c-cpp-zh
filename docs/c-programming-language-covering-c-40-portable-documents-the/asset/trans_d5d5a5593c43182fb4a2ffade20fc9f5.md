

## 17.5 互操作属性

注意：本节仅适用于 Microsoft .NET 的 C# 实现。

### 17.5.1 与 COM 和 Win32 组件的互操作

.NET 运行时提供了大量属性，使 C# 程序能够与使用 COM 和 Win32 DLL 编写的组件进行互操作。例如，可以将 DllImport 属性应用于静态 extern 方法，以指示该方法的实现位于 Win32 DLL 中。这些属性位于 `System.Runtime.InteropServices` 命名空间中，关于这些属性的详细文档可参阅 .NET 运行时文档。

### 17.5.2 与其他 .NET 语言的互操作

### 17.5.2.1 IndexerName 属性

索引器在 .NET 中使用带索引的属性实现，并且在 .NET 元数据中具有名称。如果索引器没有指定 IndexerName 属性，则默认使用名称 Item。IndexerName 属性允许开发人员覆盖此默认名称并指定其他名称。

```
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute : Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} }
    }
}
```

## 18. 不安全代码

前面各章定义的核心 C# 语言与 C 和 C++ 有一个显著区别，即省略了作为数据类型的指针。相反，C# 提供了引用，以及创建由垃圾回收器管理的对象的能力。这种设计与其他特性相结合，使 C# 成为一种比 C 或 C++ 安全得多的语言。在核心 C# 语言中，不可能存在未初始化的变量、“悬空”指针，或索引超出数组边界的表达式。因此，C 和 C++ 程序中经常出现的整类错误都被消除了。

虽然 C 或 C++ 中几乎每一种指针类型构造在 C# 中都有对应的引用类型，但在某些情况下，访问指针类型仍然是必要的。例如，如果没有对指针的访问，可能无法或不适合与底层操作系统进行交互、访问内存映射设备，或实现时间关键型算法。为满足这一需求，C# 提供了编写不安全代码的能力。

> > **CHRIS SELLS**  自从我开始编写 .NET 程序以来（早于 1.0 的 RTM），我从未发现有必要编写不安全代码。一次也没有。

在不安全代码中，可以声明和操作指针，在指针与整型之间执行转换，获取变量的地址，等等。从某种意义上说，在 C# 程序中编写不安全代码很像编写 C 代码。

事实上，从开发人员和用户的角度来看，不安全代码是一项“安全”的特性。不安全代码必须使用 unsafe 修饰符进行明确标记，因此开发人员不可能意外使用不安全特性；同时，执行引擎会确保不安全代码无法在不受信任的环境中执行。

### 18.1 不安全上下文

C# 的不安全特性仅在不安全上下文中可用。通过在类型或成员的声明中包含 unsafe 修饰符，或使用 unsafe 语句，可以引入不安全上下文：

- 类、结构、接口或委托的声明可以包含 unsafe 修饰符；此时，该类型声明的整个文本范围（包括类、结构或接口的主体）都被视为不安全上下文。
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数或静态构造函数的声明可以包含 unsafe 修饰符；此时，该成员声明的整个文本范围都被视为不安全上下文。
- unsafe 语句允许在代码块中使用不安全上下文。与之关联的代码块的整个文本范围都被视为不安全上下文。

下面给出了相应的语法扩展。为简洁起见，使用省略号（...）表示前面章节中出现的产生式。

```
class-modifier:
  ...
  unsafe

struct-modifier:
  ...
  unsafe

interface-modifier:
  ...
  unsafe

delegate-modifier:
  ...
  unsafe

field-modifier:
  ...
  unsafe

method-modifier:
  ...
  unsafe

property-modifier:
  ...
  unsafe
```

event-modifier:
...
unsafe

indexer-modifier:
...
unsafe

operator-modifier:
...
unsafe

constructor-modifier:
...
unsafe

destructor-declaration:
attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

static-constructor-modifiers:
extern_opt unsafe_opt static
unsafe_opt extern_opt static
extern_opt static unsafe_opt
unsafe_opt static extern_opt
static extern_opt unsafe_opt
static unsafe_opt extern_opt

embedded-statement:
...
unsafe-statement

unsafe-statement:
unsafe block

在下面的示例中：

```
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

结构声明中指定的 unsafe 修饰符使该结构声明的整个文本范围成为不安全上下文。因此，可以将 Left 和 Right 字段声明为指针类型。上面的示例也可以写成如下形式：

```
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

这里，字段声明中的 unsafe 修饰符使这些声明被视为不安全上下文。

除了建立不安全上下文，从而允许使用指针类型之外，unsafe 修饰符不会对类型或成员产生任何影响。在下面的示例中：

```
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B : A
{
    public override void F() {
        base.F();
        ...
    }
}
```

A 中 F 方法上的 unsafe 修饰符只会使 F 的文本范围成为不安全上下文，在该上下文中可以使用语言的不安全特性。在 B 中重写 F 时，无需重新指定 unsafe 修饰符——当然，除非 B 中的 F 方法本身需要访问不安全特性。

当指针类型属于方法签名的一部分时，情况略有不同：

```
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B : A
{
    public unsafe override void F(char* p) {...}
}
```

这里，由于 F 的签名包含指针类型，因此只能在不安全上下文中编写它。不过，可以通过以下任一方式引入不安全上下文：将整个类声明为 unsafe（如 A 中所示），或在方法声明中包含 unsafe 修饰符（如 B 中所示）。

### 18.2 指针类型

在不安全上下文中，类型（§4）除了可以是值类型或引用类型之外，也可以是指针类型。不过，在不安全上下文之外，指针类型也可以用于 typeof 表达式（§7.6.10.6），因为这种用法并不不安全。

```
type:
    ...
    pointer-type
```

指针类型由非托管类型或关键字 void 后跟一个 `*` 标记构成：

```
pointer-type:
    unmanaged-type *
    void *
```

```
unmanaged-type:
    type
```

指针类型中 `*` 前指定的类型称为该指针类型的所指类型。它表示指针类型值所指向的变量的类型。

与引用（引用类型的值）不同，指针不会受到垃圾回收器的跟踪——垃圾回收器不知道指针及其所指向的数据。因此，指针不能指向引用或包含引用的结构，并且指针的所指类型必须是非托管类型。

非托管类型是指任何不是引用类型或构造类型、且在任意嵌套层级中都不包含引用类型字段或构造类型字段的类型。换句话说，非托管类型包括以下类型之一：

- sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 或 bool。
- 任意枚举类型。
- 任意指针类型。
- 任意用户定义的结构类型，只要它不是构造类型，并且只包含非托管类型的字段。


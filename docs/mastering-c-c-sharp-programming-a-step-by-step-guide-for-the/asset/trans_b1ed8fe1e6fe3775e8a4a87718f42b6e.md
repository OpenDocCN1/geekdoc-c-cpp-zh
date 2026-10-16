

## 使用不安全代码

C# 与 C 和 C++ 之类的语言有一个不同之处，即它没有将指针作为数据类型。取而代之的是引用，我们能够创建由垃圾回收器管理的对象。再加上其他一些很酷的特性，这种设计使 C# 成为所有编程语言中最安全的语言之一。从核心上讲，该语言不允许我们将变量置于未初始化状态，不允许我们悬空指针，也不允许索引数组的表达式超出其边界。这样做消除了你在 C 和 C++ 语言中经常遇到的大量 bug。

在 C 和 C++ 中，几乎每种构造类型的指针都有一个对应的 C# 引用类型。然而，这并不能阻止某些情况下必须访问指针类型的需求。例如，访问内存映射的设备、尝试与操作系统交互，以及实现时间关键的算法——如果不能访问指针，这些操作既不实际，通常也不可能实现。为了帮助实现这一点，C# 允许我们编写不安全代码。

借助不安全代码，你可以声明指针并对其进行操作，可以在整型和指针之间进行转换，可以获取变量，等等。说实话，不安全代码与在 C# 程序中包含 C 或 C++ 代码实际上没有什么不同。

从用户、开发者和程序员的角度来看，不安全代码实际上是一个安全的功能。但是，需要使用 `unsafe` 修饰符对其进行标记，从而显式声明它，并防止程序员或开发者意外使用被声明为不安全的特性。从代码执行的方式来看，不安全代码不能也不会在不受信任的环境中执行。

## 不安全上下文

不言而喻，C# 的不安全特性只能在不安全上下文中使用，我们可以通过在成员或类型声明中添加 `unsafe` 修饰符来创建不安全上下文，也可以使用 `unsafe_statement`。

如果你在 struct、class、delegate 或 interface 声明中包含 `unsafe` 修饰符，则该类型的整个声明（包括 interface、struct 或 class）将被视为不安全上下文。

你也可以将 `unsafe` 修饰符添加到字段、属性、方法、运算符、索引器、事件析构函数、实例构造函数或静态构造函数声明中，整个成员声明就变成了不安全上下文。

如果你使用 `unsafe_statement`，它会创建一个供使用的不安全上下文，从上下文的角度来看，整个范围都变成了不安全上下文。

下面你可以看到每种 `unsafe_statement` 所需的语法：

```
class_modifier_unsafe
  : 'unsafe'
  ;
```

```
struct_modifier_unsafe
  : 'unsafe'
  ;
```

```
interface_modifier_unsafe
  : 'unsafe'
  ;
```

```
delegate_modifier_unsafe
  : 'unsafe'
  ;

field_modifier_unsafe
  : 'unsafe'
  ;

method_modifier_unsafe
  : 'unsafe'
  ;

property_modifier_unsafe
  : 'unsafe'
  ;

event_modifier_unsafe
  : 'unsafe'
  ;

indexer_modifier_unsafe
  : 'unsafe'
  ;

operator_modifier_unsafe
  : 'unsafe'
```

```
; 

constructor_modifier_unsafe
: 'unsafe'
;

destructor_declaration_unsafe
: attributes? 'extern'? 'unsafe'? '~' identifier '(' ')' destructor_body
| attributes? 'unsafe'? 'extern'? '~' identifier '(' ')' destructor_body
;

static_constructor_modifiers_unsafe
: 'extern'? 'unsafe'? 'static'
| 'unsafe'? 'extern'? 'static'
| 'extern'? 'static' 'unsafe'?
| 'unsafe'? 'static' 'extern'?
| 'static' 'extern'? 'unsafe'?
| 'static' 'unsafe'? 'extern'?
;

embedded_statement_unsafe
: unsafe_statement
| fixed_statement
;

unsafe_statement
```

```
: 'unsafe' block
;
```

这里有一个例子：

```
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

在这个例子中，我们在 struct 的声明中指定了 `unsafe` 修饰符，这使声明的整个文本范围成为不安全上下文。因此，你可以将 Left 字段和 Right 字段声明为指针类型。你也可以这样写这个例子：

```
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

在这个例子中，`unsafe` 修饰符位于字段声明中，这使这些声明成为不安全上下文。

除了创建允许我们使用指针类型的不安全上下文之外，`unsafe` 修饰符对任何成员或类型都没有任何影响。

下面是另一个例子：

public class A
```
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}
```

```
public class B: A
{
    public override void F() {
        base.F();
        ...
    }
}
```

在这个例子中，我们在名为 A 的类中为方法 F 添加了 `unsafe` 修饰符，它所做的只是将方法的文本范围变成不安全上下文。在 B 中，F 已被重写，我们不需要再次指定该修饰符。只有在类 B 中的 F 方法需要访问任何不安全特性时，你才需要这样做。

当方法签名包含指针类型时，情况略有不同：

```
public unsafe class A
{
    public virtual void F(char* p) {...}
}
```

```
public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

因为 F 的签名中包含指针类型，所以我们只能在不安全上下文中编写它。我们可以通过两种方式做到这一点——就像我们对 A 所做的那样，将整个类变成不安全上下文；或者，就像我们对 B 所做的那样，将 `unsafe` 修饰符添加到方法声明中。

## 指针类型

在不安全上下文中，类型可以是 value_type、reference_type 或 pointer_type。但是，你也可以在不安全上下文之外的表達式中使用 pointer_type，因为这种使用不被视为不安全：

```
type_unsafe
  : pointer_type
  ;
```

我们将 pointer_types 写成 unmanaged_types，或者使用 `void` 关键字和 `*` 标记：

```
pointer_type
  : unmanaged_type '*'
  | 'void' '*'
  ;
```

```
unmanaged_type
  : type
  ;
```

在 pointer_type 中，我们在 `*` 标记之前指定的类型称为指针类型的引用类型（referent type）。它用于表示指针类型值所指向的变量类型。

与引用类型的值不同，垃圾回收器不会跟踪指针。事实上，垃圾回收器甚至不知道指针的存在，更不用说它们指向的数据了。这就是为什么指针不允许指向引用或包含引用的结构；此外，指针的引用类型必须是 unmanaged_type。

非托管类型是任何不是构造类型或 reference_type 的类型，并且不会在任何嵌套级别包含构造类型的字段或 reference_type 的字段。基本上，非托管类型包括以下任何类型：

- sbyte
- byte
- short
- ushort
- int
- uint
- long
- ulong
- char
- float
- double
- decimal
- bool
- 任何 enum_types
- 任何 pointer_types
- 任何由用户定义的 struct_type——不能是构造类型，并且其字段只能包含 unmanaged_types 类型

混合引用和指针时应遵循的规则是：引用或对象引用可以包含指针，但指针引用不能包含引用。

你可以在这里看到一些指针类型：

| 指针类型 | 描述 |
|---|---|
| `byte*` | 指向字节的指针 |
| `char*` | 指向字符的指针 |
| `int**` | 指向 int 指针的指针 |
| `int*[]` | 指向 int 的指针的一维数组 |
| `void*` | 指向未知类型的指针 |

对于任何实现，所有指针类型都必须具有相同的表示形式和大小。

在 C 和 C++ 中，我们可以在一个声明中声明多个指针，但在 C# 中，我们只将 `*` 与基础类型一起写出；它不能用作各个指针名称的前缀标点符号。例如：

```
`int* pi, pj;    // it isn’t written as int *pi, *pj;`
```

对于类型为 T* 的指针，其值表示一个变量（也是 T 类型）的地址。可以使用指针的解引用运算符来访问该变量。例如，假设我们有一个名为 P 的变量，它是 int* 类型。表达式 *P 告诉我们 int 变量位于 P 中指定的地址处。

与对象引用一样，我们可以有值为 null 的指针。当你对空指针使用解引用运算符时，结果将是由实现定义的行为，并且全零位用于表示值为 null 的指针。

为了表示指向未知类型的指针，我们使用 void* 类型。由于我们没有未知的引用类型，因此不能对 void* 类型的指针应用解引用运算符。我们也不能对这些指针进行任何算术运算。但是，void* 指针可以转换为另一种类型，其他类型也可以转换为 void*。

指针类型完全是另一类类型。与值类型和引用类型不同，指针类型不能从对象继承，并且对象和指针之间不存在转换。


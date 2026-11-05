
```
namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a;       // refers to N1.N2.A
        R1.N2.A b;       // refers to N1.N2.A
        R2.A c;          // refers to N1.N2.A
    }
}
```

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名为 N1.N2.A 的类声明。end example]

尽管 partial 类型 (§15.2.7) 的每个部分都在同一个命名空间内声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可以存在不同的 extern 别名指令和 using 指令。在解释一个部分内的简单名称 (§12.7.3) 时，仅考虑包含该部分的命名空间主体和编译单元的 extern 别名指令和 using 指令。这可能导致同一个标识符在不同的部分中具有不同的含义。[示例：

```
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;          // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = widgets.LinkedList;

    partial class A
    {
        List y;          // y has type widgets.LinkedList
    }
}
```

end example]

使用别名可以命名封闭构造的类型，但不能在不提供类型参数的情况下命名未绑定的泛型类型声明。[示例：

```
namespace N1
{
    class A<T>
    {
        class B {}
    }
}
namespace N2
{
    using W = N1.A;          // Error, cannot name unbound generic type
    using X = N1.A.B;        // Error, cannot name unbound generic type
    using Y = N1.A<int>;     // Ok, can name closed constructed type
    using Z<T> = N1.A<T>;    // Error, using alias cannot have type parameters
}
```

end example]

```
type-declaration:
  class-declaration
  struct-declaration
  interface-declaration
  enum-declaration
  delegate-declaration
```

类型声明可以作为编译单元中的顶层声明出现，也可以作为命名空间、类或结构中的成员声明出现。

当类型 T 的类型声明作为编译单元中的顶层声明出现时，该类型声明的完全限定名 (§8.8.2) 与该声明的非限定名 (§8.8.2) 相同。当类型 T 的类型声明出现在命名空间、类或结构声明内时，该类型声明的完全限定名 (§8.8.3) 为 S.N，其中 S 是包含的命名空间、类或结构声明的完全限定名，N 是该声明的非限定名。

在类或结构内部声明的类型称为嵌套类型 (§15.3.9)。

类型声明允许的访问修饰符以及默认访问级别取决于声明发生的上下文 (§8.5.2)：

- 在编译单元或命名空间中声明的类型可以具有 public 或 internal 访问级别。默认值为 internal 访问。
- 在类中声明的类型可以具有 public、protected internal、protected、internal 或 private 访问级别。默认值为 private 访问。
- 在结构中声明的类型可以具有 public、internal 或 private 访问级别。默认值为 private 访问。

## 14.8 限定别名成员

### 14.8.1 通用

命名空间别名限定符 :: 使得可以保证类型名称查找不受新类型和成员引入的影响。命名空间别名限定符始终出现在两个标识符之间，分别称为左手标识符和右手标识符。与常规的 . 限定符不同，:: 限定符的左手标识符仅作为 extern 或 using 别名进行查找。

限定别名成员提供了对全局命名空间以及可能被其他实体隐藏的 extern 或 using 别名的显式访问。

```
qualified-alias-member:
  identifier :: identifier type-argument-list_opt
```

限定别名成员可以用作命名空间或类型名 (§8.8)，或用作成员访问 (§12.7.5) 中的左操作数。

限定别名成员由两个标识符组成，分别称为左手标识符和右手标识符，由 :: 标记分隔，并可选择跟随类型参数列表。当左手标识符为 global 时，则在全局命名空间中搜索右手标识符。对于任何其他左手标识符，该标识符将作为 extern 或 using 别名进行查找 (§14.4 和 §14.5.2)。如果不存在此类别名或别名引用类型，则会发生编译时错误。如果别名引用命名空间，则在该命名空间中搜索右手标识符。

限定别名成员有两种形式之一：

- N :: I<A1, ..., Ak>，其中 N 和 I 表示标识符，<A1, ..., Ak> 是类型参数列表。（K 始终至少为 1。）
- N :: I，其中 N 和 I 表示标识符。（在这种情况下，K 被视为零。）

使用此记法，限定别名成员的含义确定如下：

- 如果 N 是标识符 `global`，则在全局命名空间中搜索 I：
  - 如果全局命名空间包含名为 I 的命名空间且 K 为零，则 *qualified-alias-member* 引用该命名空间。
  - 否则，如果全局命名空间包含名为 I 的非泛型类型且 K 为零，则 *qualified-alias-member* 引用该类型。
  - 否则，如果全局命名空间包含名为 I 且具有 K 个类型参数的类型，则 *qualified-alias-member* 引用使用给定类型参数构造的该类型。
  - 否则，*qualified-alias-member* 未定义并发生编译时错误。
- 否则，从直接包含 *qualified-alias-member* 的命名空间声明 (§14.3)（如果有）开始，继续每个封闭的命名空间声明（如果有），直至包含 *qualified-alias-member* 的编译单元，以下步骤将被评估直到定位到一个实体：
  - 如果命名空间声明或编译单元包含将 N 与类型关联的 *using-alias-directive*，则 *qualified-alias-member* 未定义并发生编译时错误。
  - 否则，如果命名空间声明或编译单元包含将 N 与命名空间关联的 *extern-alias-directive* 或 *using-alias-directive*，则：
    - 如果与 N 关联的命名空间包含名为 I 的命名空间且 K 为零，则 *qualified-alias-member* 引用该命名空间。
    - 否则，如果与 N 关联的命名空间包含名为 I 的非泛型类型且 K 为零，则 *qualified-alias-member* 引用该类型。
    - 否则，如果与 N 关联的命名空间包含名为 I 且具有 K 个类型参数的类型，则 *qualified-alias-member* 引用使用给定类型参数构造的该类型。
    - 否则，*qualified-alias-member* 未定义并发生编译时错误。
- 否则，*qualified-alias-member* 未定义并发生编译时错误。

[示例：在代码中：

```csharp
using S = System.Net.Sockets;
class A {
    public static int x;
}
class C {
    public void F(int A, object S) {
        // Use global::A.x instead of A.x
        global::A.x += A;

        // Use S::Socket instead of S.Socket
        S::Socket s = S as S::Socket;
    }
}
```

类 A 使用 global::A 引用，类型 System.Net.Sockets.Socket 使用 S::Socket 引用。如果改用 A.x 和 S.Socket，则会因 A 和 S 解析为参数而导致编译时错误。end example]

[注意：标识符 `global` 只有在用作 *qualified-alias-name* 的左手标识符时才具有特殊含义。它不是关键字，也不是别名本身；它是一个上下文关键字 (§7.4.4)。在代码中：

```csharp
class A { }
class C {
    global::A x;   // Error: global is not defined
    global::A y;   // Valid: References A in the global namespace
}
```

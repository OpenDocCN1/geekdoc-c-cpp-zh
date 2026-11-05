
```
class B: A {}
}
```

以上，在 N3 命名空间中的成员声明内，A 是 N1.N2.A 的别名，因此类 N3.B 派生自类 N1.N2.A。可以通过创建 R 对 N1.N2 的别名然后引用 R.A 来获得相同的效果：

```
namespace N3
{
    using R = N1.N2;

    class B : R.A {}
}
```

结束示例

在包含 extern_alias_directive 的编译单元或命名空间体内的 using 指令、全局属性和成员声明中，由 extern_alias_directive 引入的标识符可用于引用关联的命名空间。

示例：例如：

```
namespace N1
{
    extern alias N2;

    class B : N2::A {}
}
```

以上，在 N1 命名空间中的成员声明内，N2 是对程序源代码外部定义的某个命名空间的别名。类 N1.B 派生自类 N2.A。可以通过创建 A 对 N2.A 的别名然后引用 A 来获得相同的效果：

```
namespace N1
{
    extern alias N2;

    using A = N2::A;

    class B : A {}
}
```

结束示例

extern_alias_directive 或 using_alias_directive 使别名在特定的编译单元或命名空间体内可用，但它不会向底层声明空间贡献任何新成员。换句话说，别名指令不是传递的，而是仅影响它出现的编译单元或命名空间体。

示例：在以下代码中

```
namespace N3
{
    extern alias R1;

    using R2 = N1.N2;
}
```

```
namespace N3
{
    class B : R1::A, R2.I {} // Error, R1 and R2 unknown
}
```

引入 R1 和 R2 的别名指令的作用域仅扩展到包含它们的命名空间体中的成员声明，因此在第二个命名空间声明中 R1 和 R2 是未知的。然而，将别名指令放在包含的编译单元中会使别名在两个命名空间声明中都可用：

```
extern alias R1;
```

```
using R2 = N1.N2;
```

```
namespace N3
{
    class B : R1::A, R2.I {}
}
```

```
namespace N3
{
    class C : R1::A, R2.I {}
}
```

结束示例

编译单元或 namespace_body 中的每个 extern_alias_directive 或 using_alias_directive 都会向直接包含的编译单元或命名空间体的别名声明空间（§7.3）贡献一个名称。别名指令的标识符在相应的别名声明空间内必须是唯一的。别名标识符不必在全局声明空间或相应命名空间的声明空间内唯一。

示例：

```
extern alias X;
extern alias Y;
```

```
using X = N1.N2; // Error: alias X already exists
```

```
class Y {} // Ok
```

名为 X 的 using 别名导致错误，因为在同一个编译单元中已存在名为 X 的别名。名为 Y 的类与名为 Y 的 extern 别名不冲突，因为这些名称被添加到不同的声明空间。前者被添加到全局声明空间，后者被添加到此编译单元的别名声明空间。

当别名名称与命名空间的成员名称相同时，使用任一名称都必须适当地限定：

```
namespace N1.N2
{
    class B {}
}
```

```
namespace N3
{
    class A {}
}
```

```
class B : A {}
}
namespace N3
{
    using A = N1.N2;
    using B = N1.N2.B;
    class W : B {} // Error: B is ambiguous
    class X : A.B {} // Error: A is ambiguous
    class Y : A::B {} // Ok: uses N1.N2.B
    class Z : N3.B {} // Ok: uses N3.B
}
```

在 N3 的第二个命名空间体中，未限定的 B 用法会导致错误，因为 N3 包含一个名为 B 的成员，并且该命名空间体还声明了名为 B 的别名；A 也是如此。类 N3.B 可以作为 N3.B 或 global::N3.B 引用。别名 A 可以在限定别名成员（§14.8）中使用，例如 A::B。别名 B 基本上是无用的。它不能在 qualified_alias_member 中使用，因为只有命名空间别名才能在 qualified_alias_member 中使用，而 B 别名的是一个类型。

结束示例

就像常规成员一样，由 alias_directives 引入的名称会被嵌套作用域中同名成员隐藏

示例：在以下代码中

```
using R = N1.N2;
namespace N3
{
    class R {}
    class B: R.A {} // Error, R has no member A
}
```

在 B 的声明中对 R.A 的引用会导致编译时错误，因为 R 引用的是 N3.R，而不是 N1.N2。

结束示例

extern_alias_directives 的书写顺序无关紧要。同样，using_alias_directives 的书写顺序也无关紧要，但所有 using_alias_directives 必须在同一个编译单元或命名空间体中位于所有 extern_alias_directives 之后。由 using_alias_directive 引用的 namespace_or_type_name 的解析不受 using_alias_directive 本身或直接包含的编译单元或命名空间体中的其他 using_directives 影响，但可能受直接包含的编译单元或命名空间体中的 extern_alias_directives 影响。换句话说，using_alias_directive 的 namespace_or_type_name 的解析就像直接包含的编译单元或命名空间体没有 using_directives 但具有正确的 extern_alias_directives 集合一样。

示例：在以下代码中

```
namespace N1.N2 {}
namespace N3
{
```

```
extern alias X;

using R1 = X::N; // OK
using R2 = N1; // OK
using R3 = N1.N2; // OK
using R4 = R2.N2; // Error, R2 unknown
}
```

最后一个 using_alias_directive 导致编译时错误，因为它不受前一个 using_alias_directive 影响。第一个 using_alias_directive 不会导致错误，因为 extern 别名 X 的作用域包含 using_alias_directive。

*结束示例*

using_alias_directive 可以为任何命名空间或类型创建别名，包括它出现的命名空间以及该命名空间内嵌套的任何命名空间或类型。

通过别名访问命名空间或类型与通过其声明名称访问该命名空间或类型得到的结果完全相同。

*示例：给定*

```
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a; // refers to N1.N2.A
        R1.N2.A b; // refers to N1.N2.A
        R2.A c; // refers to N1.N2.A
    }
}
```

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名称为 N1.N2.A 的类声明。

*结束示例*

尽管 partial type（§15.2.7）的每个部分都在同一个命名空间内声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可以存在不同的 extern_alias_directives 和 using_directives。在解释一个部分内的简单名称（§12.8.4）时，仅考虑包含该部分的命名空间体和编译单元的 extern_alias_directives 和 using_directives。这可能导致同一个标识符在不同部分中具有不同的含义。

*示例：*

```
namespace N
{
    using List = System.Collections.ArrayList;
```

```
partial class A
{
    List x; // x has type System.Collections.ArrayList
}
}
```

```
namespace N
{
    using List = Widgets.LinkedList;

    partial class A
    {
        List y; // y has type Widgets.LinkedList
    }
}
```

结束示例

使用别名可以命名封闭构造类型，但不能在不提供类型参数的情况下命名未绑定泛型类型声明。

示例：

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
    using W = N1.A;      // Error, cannot name unbound generic type
    using X = N1.A.B;    // Error, cannot name unbound generic type
    using Y = N1.A<int>; // Ok, can name closed constructed type
    using Z<T> = N1.A<T>; // Error, using alias cannot have type parameters
}
```

结束示例

## 14.5.3 using 命名空间指令

using_namespace_directive 将命名空间中包含的类型导入到直接包含的编译单元或命名空间体中，使每个类型的标识符能够在不加限定的情况下使用。

```
using_namespace_directive
    : 'using' namespace_name ';'
    ;
```

在包含 using_namespace_directive 的编译单元或命名空间体中的成员声明内，可以直接引用给定命名空间中包含的类型。

示例：

```
namespace N1.N2
{
    class A {}
}
```

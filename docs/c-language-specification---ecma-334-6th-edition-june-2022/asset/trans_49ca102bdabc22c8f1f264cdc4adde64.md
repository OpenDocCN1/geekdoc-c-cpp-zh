

```
extern alias E;

using R1 = E::N; // OK
using R2 = N1; // OK
using R3 = N1.N2; // OK
using R4 = R2.N2; // Error, R2 unknown
}
```

最后一个 using_alias_directive 会导致编译时错误，因为它不受前一个 using_alias_directive 的影响。第一个 using_alias_directive 不会导致错误，因为 extern 别名 E 的作用域包含该 using_alias_directive。

示例结束

using_alias_directive 可以为任何命名空间或类型创建别名，包括它所在的命名空间以及该命名空间中嵌套的任何命名空间或类型。

通过别名访问命名空间或类型，与通过其声明名称访问该命名空间或类型得到的结果完全相同。

示例：给定

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

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名为 N1.N2.A 的类声明。

示例结束

尽管分部类型（§14.2.7）的每个部分都声明在同一个命名空间中，但这些部分通常写在不同的命名空间声明中。因此，每个部分都可以存在不同的 extern_alias_directives 和 using_directives。当在一个部分内解释简单名称（§11.7.4）时，只考虑包含该部分的命名空间体和编译单元的 extern_alias_directives 和 using_directives。这可能导致同一标识符在不同部分中具有不同含义。

示例：

```
namespace N
{
    using List = System.Collections.ArrayList;
    partial class A
    {
        List x; // x has type System.Collections.ArrayList
    }
}
namespace N
{
    using List = Widgets.LinkedList;
    partial class A
    {
        List y; // y has type Widgets.LinkedList
    }
}
```

*示例结束*

使用别名可以命名封闭构造类型，但不能在未提供类型实参的情况下命名未绑定泛型类型声明。

*示例：*

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

*示例结束*

## 13.5.3 使用命名空间指令

using_namespace_directive 将命名空间中包含的类型导入到直接包含它的编译单元或命名空间体中，使每个类型的标识符无需限定即可使用。

```
using_namespace_directive
    : 'using' namespace_name ';'
    ;
```

在包含 using_namespace_directive 的编译单元或命名空间体的成员声明中，可以直接引用给定命名空间中包含的类型。

*示例：*

```
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1.N2;
    class B : A {}
}
```

在上面的代码中，在 N3 命名空间的成员声明内，N1.N2 的类型成员可直接使用，因此类 N3.B 派生自类 N1.N2.A。

示例结束

using_namespace_directive 导入给定命名空间中包含的类型，但明确不会导入嵌套命名空间。

示例：在以下代码中

```
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1;
    class B : N2.A {} // Error, N2 unknown
}
```

using_namespace_directive 导入 N1 中包含的类型，但不导入 N1 中嵌套的命名空间。因此，B 的声明中对 N2.A 的引用会导致编译时错误，因为作用域中没有名为 N2 的成员。

示例结束

与 using_alias_directive 不同，using_namespace_directive 可以导入其标识符已在包含它的编译单元或命名空间体中定义的类型。实际上，由 using_namespace_directive 导入的名称会被包含它的编译单元或命名空间体中同名成员隐藏。

示例：

```
namespace N1.N2
{
    class A {}
    class B {}
}

namespace N3
{
    using N1.N2;
    class A {}
}
```

这里，在 N3 命名空间的成员声明内，A 指的是 N3.A，而不是 N1.N2.A。

示例结束

当多个导入的命名空间引入相同类型名称时，名称可能产生歧义，因此 using_alias_directive 可用于消除引用的歧义。

示例：在以下代码中

```
namespace N1
{
    class A {}
}

namespace N2
{
    class A {}
}

namespace N3
{
    using N1;
    using N2;

    class B : A {} // Error, A is ambiguous
}
```

N1 和 N2 都包含成员 A，并且由于 N3 同时导入二者，因此在 N3 中引用 A 会导致编译时错误。在这种情况下，可以通过限定对 A 的引用来解决冲突，或者通过引入选择特定 A 的 using_alias_directive 来解决。例如：

```
namespace N3
{
    using N1;
    using N2;
    using A = N1.A;

    class B : A {} // A means N1.A
}
```

示例结束

此外，当同一编译单元或命名空间体中由 using_namespace_directives 或 using_static_directives 导入的多个命名空间或类型包含同名的类型或成员时，将该名称作为 simple_name 的引用会被视为有歧义。

示例：

```
namespace N1
{
    class A {}
}

class C
{
    public static int A;
}

namespace N2
{
    using N1;
    using static C;
    class B
    {
        void M()
        {
            A a = new A();  // Ok, A is unambiguous as a type-name
            A.Equals(2);    // Error, A is ambiguous as a simple-name
        }
    }
}
```

N1 包含类型成员 A，C 包含静态字段 A，并且由于 N2 同时导入二者，因此将 A 作为 simple_name 引用会产生歧义，并导致编译时错误。

示例结束

与 using_alias_directive 一样，using_namespace_directive 不会向编译单元或命名空间的底层声明空间贡献任何新成员，而只影响它所在的编译单元或命名空间体。

using_namespace_directive 引用的 namespace_name 的解析方式与 using_alias_directive 引用的 namespace_or_type_name 相同。因此，同一编译单元或命名空间体中的 using_namespace_directives 彼此不影响，并且可以按任意顺序书写。

## 13.5.4 使用 static 指令

using_static_directive 将类型声明中直接包含的嵌套类型和静态成员导入到直接包含它的编译单元或命名空间体中，使每个成员和类型的标识符无需限定即可使用。

```
using_static_directive
    : 'using' 'static' type_name ';'
    ;
```

在包含 using_static_directive 的编译单元或命名空间体的成员声明中，可以直接引用给定类型声明中直接包含的可访问嵌套类型和静态成员（扩展方法除外）。

示例：

```
namespace N1
{
    class A
    {
        public class B {}
        public static B M() => new B();
    }
}

namespace N2
{
    using static N1.A;

    class C
    {
        void N()
        {
            B b = M();
        }
    }
}
```

在前面的代码中，在 N2 命名空间的成员声明内，N1.A 的静态成员和嵌套类型可直接使用，因此方法 N 能够引用 N1.A 的 B 和 M 两个成员。

示例结束

using_static_directive 明确不会将扩展方法作为静态方法直接导入，而是使它们可用于扩展方法调用（§11.7.8.3）。

示例：

```
namespace N1
{
    static class A
    {
        public static void M(this string s){}
    }
}

namespace N2
{
    using static N1.A;

    class B
    {
        void N()
        {
            M("A");    // Error, M unknown
            "B".M();    // Ok, M known as extension method
            N1.A.M("C"); // Ok, fully qualified
        }
    }
}
```

using_static_directive 导入 N1.A 中包含的扩展方法 M，但仅作为扩展方法导入。因此，B.N 主体中对 M 的第一次引用会导致编译时错误，因为作用域中没有名为 M 的成员。

示例结束

using_static_directive 只导入给定类型中直接声明的成员和类型，不导入基类中声明的成员和类型。

示例：

```
namespace N1
{
    static class A
    {
        public static void M(string s){}
    }

    static class B : A
```


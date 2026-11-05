
## 13.3 命名空间声明

*命名空间声明* 由关键字 namespace 后跟命名空间名称和主体组成，后面可选跟一个分号。

```
namespace_declaration
    : 'namespace' qualified_identifier namespace_body ';'?
    ;

qualified_identifier
    : identifier ('.' identifier)*
    ;

namespace_body
    : '{' extern_alias_directive* using_directive* namespace_member_declaration* '}'
    ;
```

*命名空间声明* 可以作为 *编译单元* 中的顶级声明出现，也可以作为另一个 *命名空间声明* 内的成员声明出现。当 *命名空间声明* 作为 *编译单元* 中的顶级声明出现时，该命名空间成为全局命名空间的成员。当 *命名空间声明* 出现在另一个 *命名空间声明* 内时，内部命名空间成为外部命名空间的成员。无论哪种情况，命名空间的名称在包含它的命名空间内都应唯一。

命名空间隐式为 public，并且命名空间的声明不能包含任何访问修饰符。

在 *命名空间主体* 内，可选的 *using 指令* 导入其他命名空间、类型和成员的名称，使它们可以直接引用，而不必通过限定名引用。可选的 *命名空间成员声明* 向命名空间的声明空间贡献成员。请注意，所有 *using 指令* 都必须出现在任何成员声明之前。

*命名空间声明* 的 *限定标识符* 可以是单个标识符，也可以是由“.”标记分隔的标识符序列。后一种形式允许程序定义嵌套命名空间，而不必在词法上嵌套多个命名空间声明。

```
Example:

namespace N1.N2
{
    class A {}
    class B {}
}

is semantically equivalent to

namespace N1
{
    namespace N2
    {
        class A {}
        class B {}
    }
}

end example
```

命名空间是开放式的，两个具有相同完全限定名（§7.8.2）的命名空间声明贡献到同一个声明空间（§7.3）。

示例：在以下代码中

```
namespace N1.N2
{
    class A {}
}

namespace N1.N2
{
    class B {}
}
```

上述两个命名空间声明贡献到同一个声明空间，在这种情况下声明了两个完全限定名分别为 N1.N2.A 和 N1.N2.B 的类。由于这两个声明贡献到同一个声明空间，如果每个声明都包含一个同名成员的声明，则本来会导致错误。

示例结束

## 13.4 extern 别名指令

extern 别名指令引入一个标识符，该标识符用作命名空间的别名。对被设置别名的命名空间的指定位于程序源代码之外，并且也适用于被设置别名的命名空间的嵌套命名空间。

```
extern_alias_directive
    : 'extern' 'alias' identifier ';'
    ;
```

extern 别名指令的作用域延伸到直接包含它的 *编译单元* 或 *命名空间主体* 的 using 指令、全局特性和命名空间成员声明。

在包含 extern 别名指令的编译单元或命名空间主体中，可以使用该 extern 别名指令引入的标识符来引用被设置别名的命名空间。如果该标识符为单词 global，则会导致编译时错误。

extern 别名指令引入的别名与 using 别名指令引入的别名非常相似。有关 extern 别名指令和 using 别名指令的更详细讨论，请参见 §13.5.2。

alias 是上下文关键字（§6.4.4），仅当它在 extern 别名指令中紧跟在 extern 关键字之后时才有特殊含义。

如果程序声明了未提供外部定义的 extern 别名，则会发生错误。

示例：以下程序声明并使用两个 extern 别名 X 和 Y，它们各自表示一个不同命名空间层次结构的根：

```
extern alias X;
extern alias Y;

class Test
{
    X::N::A a;
    X::N::B b1;
    Y::N::B b2;
    Y::N::C c;
}
```

该程序声明了 extern 别名 X 和 Y 的存在，但这些别名的实际定义位于程序外部。现在可以将同名的 N::B 类分别引用为 X::N::B 和 Y::N::B，或者使用命名空间别名限定符，引用为 X::N::B 和 Y::N::B。示例结束

## 13.5 using 指令

### 13.5.1 概述

using 指令有助于使用在其他命名空间中定义的命名空间和类型。using 指令会影响命名空间或类型名称（§7.8）和简单名称（§11.7.4）的名称解析过程，但与声明不同，using 指令不会向使用它们的编译单元或命名空间的基础声明空间贡献新成员。

```
using_directive
  : using_alias_directive
  | using_namespace_directive
  | using_static_directive
;
```

using 别名指令（§13.5.2）引入命名空间或类型的别名。

using 命名空间指令（§13.5.3）导入命名空间的类型成员。

using 静态指令（§13.5.4）导入类型的嵌套类型和静态成员。

using 指令的作用域延伸到直接包含它的编译单元或命名空间主体的命名空间成员声明。using 指令的作用域特别不包括其同级的 using 指令。因此，同级的 using 指令不会相互影响，并且它们的书写顺序无关紧要。相比之下，extern 别名指令的作用域包括在同一编译单元或命名空间主体中定义的 using 指令。

### 13.5.2 using 别名指令

using 别名指令引入一个标识符，该标识符在直接包含它的编译单元或命名空间主体中用作命名空间或类型的别名。

```
using_alias_directive
  : 'using' identifier '=' namespace_or_type_name ';'
  ;
```

在包含 using 别名指令的编译单元或命名空间主体中，在全局特性和成员声明内，可以使用该 using 别名指令引入的标识符来引用给定的命名空间或类型。

示例：

```
namespace N1.N2
{
  class A {}
}
namespace N3
{
  using A = N1.N2.A;
  class B: A {}
}
```

上例中，在 N3 命名空间的成员声明内，A 是 N1.N2.A 的别名，因此类 N3.B 派生自类 N1.N2.A。通过为 N1.N2 创建别名 R，然后引用 R.A，也可以获得相同的效果：

```
namespace N3
{
    using R = N1.N2;
    class B : R.A {}
}
```

在包含 extern 别名指令的编译单元或命名空间主体中，在 using 指令、全局特性和成员声明内，可以使用该 extern 别名指令引入的标识符来引用关联的命名空间。

```
namespace N1
{
    extern alias N2;
    class B : N2::A {}
}
```

上例中，在 N1 命名空间的成员声明内，N2 是某个命名空间的别名，该命名空间的定义位于程序源代码之外。类 N1.B 派生自类 N2.A。通过为 N2.A 创建别名 A，然后引用 A，也可以获得相同的效果：

```
namespace N1
{
    extern alias N2;
    using A = N2::A;
    class B : A {}
}
```

extern 别名指令或 using 别名指令使别名在特定编译单元或命名空间主体内可用，但它不会向基础声明空间贡献任何新成员。换言之，别名指令不是传递性的，而只影响其所在的编译单元或命名空间主体。

示例：在以下代码中

```
namespace N3
{
    extern alias R1;
    using R2 = N1.N2;
}

namespace N3
{
    class B : R1::A, R2.I {} // Error, R1 and R2 unknown
}
```

引入 R1 和 R2 的别名指令的作用域仅延伸到包含它们的命名空间主体中的成员声明，因此在第二个命名空间声明中 R1 和 R2 是未知的。但是，将别名指令放在包含这些命名空间声明的编译单元中，会使别名在这两个命名空间声明内都可用：

```
extern alias R1;

using R2 = N1.N2;

namespace N3
{
    class B : R1::A, R2.I {}
}

namespace N3
{
    class C : R1::A, R2.I {}
}
```

示例结束

编译单元或命名空间主体中的每个 extern 别名指令或 using 别名指令都会向直接包含它的编译单元或命名空间主体的别名声明空间（§7.3）贡献一个名称。别名指令的标识符应在对应的别名声明空间中唯一。该别名标识符不必在全局声明空间或对应命名空间的声明空间中唯一。

示例：

```
extern alias A;
extern alias B;

using A = N1.N2; // Error: alias A already exists

class B {} // Ok
```

名为 A 的 using 别名会导致错误，因为同一编译单元中已经存在名为 A 的别名。名为 B 的类不会与名为 B 的 extern 别名冲突，因为这些名称被添加到不同的声明空间。前者被添加到全局声明空间，后者被添加到此编译单元的别名声明空间。

当别名名称与命名空间成员的名称匹配时，对任一者的使用都必须进行适当的限定：

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

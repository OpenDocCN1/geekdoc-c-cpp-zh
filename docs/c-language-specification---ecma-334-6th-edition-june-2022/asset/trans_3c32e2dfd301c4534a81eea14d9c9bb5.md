
- `return` — 目标是返回值
- 对于方法声明上的特性，默认目标是该方法。否则，当 *attribute_target* 等于：
  - `method` — 目标是该方法
  - `return` — 目标是返回值
- 对于运算符声明上的特性，默认目标是该运算符。否则，当 *attribute_target* 等于：
  - `method` — 目标是该运算符
  - `return` — 目标是返回值
- 对于属性或索引器声明的 get 访问器声明上的特性，默认目标是关联方法。否则，当 *attribute_target* 等于：
  - `method` — 目标是关联方法
  - `return` — 目标是返回值
- 对于属性或索引器声明的 set 访问器上指定的特性，默认目标是关联方法。否则，当 *attribute_target* 等于：
  - `method` — 目标是关联方法
  - `param` — 目标是唯一的隐式参数
- 对于省略 *event_accessor_declarations* 的事件声明上指定的特性，默认目标是该 *event* 声明。否则，当 *attribute_target* 等于：
  - `event` — 目标是事件声明
  - `field` — 目标是字段
  - `method` — 目标是方法
- 对于不省略 *event_accessor_declarations* 的事件声明，默认目标是 *method*。
  - `method` — 目标是关联方法
  - `param` — 目标是唯一参数

在所有其他上下文中，允许包含 *attribute_target_specifier*，但并非必需。

示例：类声明可以包含或省略说明符 *type*：

```
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

*示例结束。*

实现可以接受其他 *attribute_targets*，其用途由实现定义。不识别此类 *attribute_target* 的实现应发出警告，并忽略包含它的 *attribute_section*。

按照约定，特性类的命名带有 Attribute 后缀。attribute_name 可以包含或省略该后缀。具体而言，attribute_name 的解析如下：

- 如果 attribute_name 最右侧的标识符是逐字标识符（§6.4.3），则 attribute_name 按 type_name（§7.8）解析。如果结果不是派生自 System.Attribute 的类型，则发生编译时错误。
- 否则，
  - attribute_name 按 type_name（§7.8）解析，但会抑制任何错误。如果此解析成功且得到派生自 System.Attribute 的类型，则该类型是本步骤的结果。
  - 将字符 Attribute 追加到 attribute_name 中最右侧的标识符，并将得到的标记字符串按 type_name（§7.8）解析，但会抑制任何错误。如果此解析成功且得到派生自 System.Attribute 的类型，则该类型是本步骤的结果。

如果上述两个步骤中恰好有一个得到派生自 System.Attribute 的类型，则该类型是 attribute_name 的结果。否则发生编译时错误。

示例：如果同时找到带此后缀和不带此后缀的特性类，则存在二义性，并导致编译时错误。如果 attribute_name 的拼写使其最右侧标识符是逐字标识符（§6.4.3），则只匹配不带后缀的特性，从而可以解决此类二义性。示例

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class Example : Attribute
{
}

[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute : Attribute
{
}

[Example]      // Error: ambiguity
class Class1 {}

[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}

[@Example]      // Refers to Example
class Class3 {}

[@ExampleAttribute]  // Refers to ExampleAttribute
class Class4 {}
```

展示了两个名为 Example 和 ExampleAttribute 的特性类。特性 [Example] 有二义性，因为它可能引用 Example 或 ExampleAttribute。使用逐字标识符可以在这种罕见情况下指定确切意图。特性 [ExampleAttribute] 没有二义性（尽管如果存在名为 ExampleAttributeAttribute 的特性类，它就会有二义性！）。如果移除类 Example 的声明，那么两个特性都引用名为 ExampleAttribute 的特性类，如下所示：

```
using System;

[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute : Attribute
{}

[Example]    // Refers to ExampleAttribute
class Class1 {}

[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}

[@Example]    // Error: no attribute named "Example"
class Class3 {}
```
*示例结束*

在同一实体上多次使用单次使用特性类会导致编译时错误。

*示例：* 示例

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute : Attribute
{
    public HelpStringAttribute(string value)
    {
        Value = value;
    }

    public string Value { get; }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

导致编译时错误，因为它试图在 Class1 的声明上多次使用 HelpString，而 HelpString 是单次使用特性类。

如果以下所有陈述均为真，则表达式 E 是 attribute_argument_expression：

- E 的类型是特性参数类型（§21.2.4）。
- 在编译时，E 的值可以解析为以下之一：
  - 常量值。
  - 使用 typeof_expression（§11.7.16）获得的 System.Type 对象，该表达式指定非泛型类型、封闭构造类型（§8.4.3）或未绑定泛型类型（§8.4.4），但不能是开放泛型类型（§8.4.3）。
  - attribute_argument_expressions 的一维数组。

*示例：*

```csharp
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field)]
public class TestAttribute : Attribute
{
    public int P1 { get; set; }
    public Type P2 { get; set; }
    public object P3 { get; set; }
}
[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}
class <T> {
[Test(P2 = typeof(T))] // Error – T not a closed type.
int x1;
[Test(P2 = typeof(<T>))] // Error – C<T> not a closed type.
int x2;
[Test(P2 = typeof(<int>))] // Ok
int x3;
[Test(P2 = typeof(<>))] // Ok
int x4;
}
```
*示例结束*

在多部分中声明的类型的特性，通过以未指定顺序组合其每个部分的特性来确定。如果将同一特性放在多个部分上，则等效于在该类型上多次指定该特性。

示例：以下两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

等效于以下单个声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

类型参数上的特性以相同方式组合。

## 21.4 特性实例

### 21.4.1 概述

特性实例是在运行时表示特性的实例。特性由特性类、位置参数和命名参数定义。特性实例是特性类的实例，该实例使用位置参数和命名参数初始化。

检索特性实例涉及编译时和运行时处理，如下列子条款所述。

### 21.4.2 特性的编译

对带有特性类 T、*positional_argument_list* P、*named_argument_list* N 并指定在程序实体 E 上的 *attribute* 进行编译时，通过以下步骤将其编译到程序集 A 中：

- 遵循编译形式为 `new T(P)` 的 *object_creation_expression* 的编译时处理步骤。这些步骤要么导致编译时错误，要么确定 T 上可在运行时调用的实例构造函数 C。
- 如果 C 不具有公共可访问性，则发生编译时错误。
- 对于 N 中的每个 *named_argument* Arg：
  - 令 Name 为 *named_argument* Arg 的 *identifier*。
  - Name 应标识 T 上的非静态可读写公共字段或属性。如果 T 没有此类字段或属性，则发生编译时错误。
- 如果 *positional_argument_list* P 中的任何值或 *named_argument_list* N 中的某个值的类型为 `System.String`，且该值不是 Unicode 标准所定义的格式良好值，则编译后的值是否等于检索到的运行时值（§21.4.3）由实现定义。
  *注意：例如，包含高代理项 UTF-16 代码单元且其后未紧跟低代理项代码单元的字符串不是格式良好的。注释结束*
- 将以下信息（用于特性的运行时实例化）存储在编译器因编译包含该特性的程序而输出的程序集中：特性类 T、T 上的实例构造函数 C、*positional_argument_list* P、*named_argument_list* N 以及关联的程序实体 E，并且这些值在编译时完全解析。

### 21.4.3 特性实例的运行时检索

由 T、C、P 和 N 表示并与 E 关联的特性实例，可以在运行时使用以下步骤从程序集 A 中检索：

- 遵循执行形式为 `new T(P)` 的 *object_creation_expression* 的运行时处理步骤，使用实例构造函数 C 和在编译时确定的值。这些步骤要么导致异常，要么生成 T 的实例 O。
- 按顺序对于 N 中的每个 *named_argument* Arg：
  - 令 Name 为 *named_argument* Arg 的 *identifier*。如果 Name 未标识 O 上的非静态公共可读写字段或属性，则抛出异常。
  - 令 Value 为对 Arg 的 *attribute_argument_expression* 求值的结果。
  - 如果 Name 标识 O 上的字段，则将此字段设置为 Value。
  - 否则，Name 标识 O 上的属性。将此属性设置为 Value。
  - 结果是 O，即特性类 T 的实例，已使用 *positional_argument_list* P 和 *named_argument_list* N 初始化。

*注意：在 A 中存储 T、C、P、N（并将其与 E 关联）的格式，以及指定 E 并从 A 中检索 T、C、P、N 的机制（并因此说明如何在运行时获得特性实例），超出了本标准的范围。注释结束*

*示例：* 在 CLI 的实现中，可以通过以下程序检索在编译 §21.2.3 中示例程序所创建的程序集中的 `Help` 特性实例：

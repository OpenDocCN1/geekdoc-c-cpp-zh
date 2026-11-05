
- `type` — 一个委托、类、结构体、枚举和接口。
- `typevar` — 一个类型参数。

某些上下文允许在多个目标上指定属性。程序可以通过包含 *属性目标说明符* 来显式指定目标。如果没有 *属性目标说明符*，则应用默认值，但可以使用 *属性目标说明符* 来确认或覆盖默认值。上下文的解析如下：

- 对于委托声明上的属性，默认目标是委托。否则当属性目标等于时：
  - `type` — 目标是委托
  - `return` — 目标是返回值
- 对于方法声明上的属性，默认目标是方法。否则当 *属性目标* 等于时：
  - `method` — 目标是方法
  - `return` — 目标是返回值
- 对于运算符声明上的属性，默认目标是运算符。否则当 *属性目标* 等于时：
  - `method` — 目标是运算符
  - `return` — 目标是返回值
- 对于属性或索引器声明的 get 访问器声明上的属性，默认目标是相关方法。否则当 *属性目标* 等于时：
  - `method` — 目标是相关方法
  - `return` — 目标是返回值
- 对于属性或索引器声明的 set 访问器上指定的属性，默认目标是相关方法。否则当 *属性目标* 等于时：
  - `method` — 目标是相关方法
  - `param` — 目标是唯一的隐式参数
- 对于省略事件访问器声明的事件声明上指定的属性，默认目标是事件声明。否则当 *属性目标* 等于时：
  - `event` — 目标是事件声明
  - `field` — 目标是字段
  - `method` — 目标是方法
- 在事件声明未省略事件访问器声明的情况下，默认目标是方法。
  - `method` — 目标是相关方法
  - `param` — 目标是唯一的参数

在所有其他上下文中，包含 *属性目标说明符* 是允许的但不必要。[*示例:* 一个类声明可以包含或省略说明符 *类型*:]

```
[type: Author("Brian Kernighan")]
class Class1 {}
[Author("Dennis Ritchie")]
class Class2 {}
```

示例结束。

实现可以接受其他属性目标，其用途由实现定义。不识别此类属性目标的实现应发出警告并忽略包含的属性部分。

按惯例，属性类以 Attribute 为后缀命名。属性名可以包含或省略此后缀。具体而言，属性名按如下方式解析：

- 如果属性名的最右标识符是逐字标识符（§7.4.3），则属性名被解析为类型名（§8.8）。如果结果不是派生自 System.Attribute 的类型，则会发生编译时错误。
- 否则，
  - 属性名被解析为类型名（§8.8），但任何错误都被抑制。如果此解析成功并且结果是派生自 System.Attribute 的类型，则该类型是此步骤的结果。
  - 将字符 Attribute 追加到属性名中最右的标识符，并将 resulting token 字符串解析为类型名（§8.8），但任何错误都被抑制。如果此解析成功并且结果是派生自 System.Attribute 的类型，则该类型是此步骤的结果。

如果上述两个步骤中恰好有一个导致派生自 System.Attribute 的类型，则该类型是属性名的结果。否则会发生编译时错误。

[示例: 如果同时找到带有和不带此后缀的属性类，则存在歧义，并会导致编译时错误。如果属性名的拼写使得其最右标识符是逐字标识符（§7.4.3），则仅匹配不带后缀的属性，从而能够解决此类歧义。示例

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class Example: Attribute
{}
[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute: Attribute
{}
[Example]          // Error: ambiguity
class Class1 {}
[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}
[@Example]          // Refers to Example
class Class3 {}
[@ExampleAttribute]  // Refers to ExampleAttribute
class Class4 {}
```

显示了两个名为 Example 和 ExampleAttribute 的属性类。属性 [Example] 是模棱两可的，因为它可能指 Example 或 ExampleAttribute。使用逐字标识符允许在这种罕见情况下指定确切的意图。属性 [ExampleAttribute] 不存在歧义

（尽管如果存在名为 ExampleAttributeAttribute 的属性类则会存在歧义）。如果删除类 Example 的声明，则两个属性都引用名为 ExampleAttribute 的属性类，如下所示：

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute: Attribute
{
}
[Example]            // Refers to ExampleAttribute
class Class1 {}
[ExampleAttribute]   // Refers to ExampleAttribute
class Class2 {}
[@Example]           // Error: no attribute named "Example"
class Class3 {}
```

示例结束

对同一实体多次使用单次使用属性类是编译时错误。[示例: 示例

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;
    public HelpStringAttribute(string value) {
        this.value = value;
    }
    public string Value { get {...} }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

会导致编译时错误，因为它尝试在 Class1 的声明上多次使用 HelpString，而 HelpString 是一个单次使用属性类。示例结束

表达式 E 是属性参数表达式当且仅当满足以下所有条件时：

- E 的类型是属性参数类型（§22.2.4）。
- 在编译时，E 的值可以解析为以下之一：
  - 一个常量值。
  - 使用 typeof 表达式（§12.7.12）获得的 System.Type 对象，该表达式指定非泛型类型、闭合构造类型（§9.4.3）或非绑定泛型类型（§9.4.4），但不是开放类型（§9.4.3）。
  - 属性参数表达式的单维数组。

[示例:

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }
}
```

```
public Type P2 {
    get {...}
    set {...}
}
public object P3 {
    get {...}
    set {...}
}
[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}
class C<T> {
    [My(P2 = typeof(T))]    // Error - T not a closed type.
    int x1;
    [My(P2 = typeof(C<T>))]    // Error - C<T> not a closed type.
    int x2;
    [My(P2 = typeof(C<int>))]    // Ok
    int x3;
    [My(P2 = typeof(C<>))]    // Ok
    int x4;
}
```

示例结束

声明在多个部分中的类型的属性是通过以未指定顺序组合其每个部分的属性来确定的。如果在多个部分上放置相同的属性，则等同于在该类型上多次指定该属性。[示例: 两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

等同于以下单个声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

示例结束

类型参数上的属性以相同方式组合。

## 22.4 属性实例

### 22.4.1 通用

属性实例是表示运行时属性的实例。属性由属性类、位置参数和命名参数定义。属性实例是属性类的实例，其使用位置参数和命名参数进行初始化。

获取属性实例涉及编译时和运行时的处理，如以下小节所述。

### 22.4.2 属性的编译

具有属性类 T、位置参数列表 P、命名参数列表 N 并指定在程序实体 E 上的属性的编译通过以下步骤编译为程序集 A：

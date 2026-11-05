
## 17. 属性

C# 语言的大部分功能使程序员能够为程序中定义的实体指定声明性信息。例如，类中方法的访问性是通过为其添加方法修饰符 public、protected、internal 和 private 来指定的。

C# 使程序员能够发明新的声明性信息类型，称为属性。程序员随后可以将属性附加到各种程序实体，并在运行时环境中检索属性信息。例如，一个框架可能会定义一个 HelpAttribute 属性，该属性可以放置在某些程序元素（如类和方法）上，以提供这些程序元素与其文档之间的映射。

属性是通过属性类的声明来定义的 (§17.1)，属性类可以具有位置参数和命名参数 (§17.1.2)。属性是使用属性规范 (§17.2) 附加到 C# 程序中的实体，并在运行时作为属性实例检索 (§17.3)。

### 17.1 属性类

派生自抽象类 System.Attribute 的类，无论是直接还是间接，都称为属性类。属性类的声明定义了一种可以放置在声明上的新属性类型。按惯例，属性类以 Attribute 为后缀命名。使用属性时可以包含或省略此后缀。

### 17.1.1 属性用法

AttributeUsage 属性 (§17.4.1) 用于描述属性类如何被使用。

AttributeUsage 具有一个位置参数 (§17.1.2)，使属性类能够指定其可使用的声明类型。示例

```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{
    ...
}
```

定义了一个名为 SimpleAttribute 的属性类，只能放置在类声明和接口声明上。示例

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

显示了 Simple 属性的几种用法。尽管此属性定义时名称为 SimpleAttribute，但在该属性使用时可以省略 Attribute 后缀，从而得到简短名称 Simple。因此，上面的示例在语义上等同于以下内容：

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

AttributeUsage 具有一个名为 AllowMultiple 的命名参数 (§17.1.2)，指示该属性是否可以对给定实体指定多次。如果属性类的 AllowMultiple 为 true，则该属性类为多用属性类，可以在实体上指定多次。如果属性类的 AllowMultiple 为 false 或未指定，则该属性类为单用属性类，最多只能在实体上指定一次。

示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;
    public AuthorAttribute(string name) {
        this.name = name;
    }
    public string Name {
        get { return name; }
    }
}
```

定义了一个名为 AuthorAttribute 的多用属性类。示例

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

显示了一个类声明，其中使用了两次 Author 属性。

AttributeUsage 还有另一个名为 Inherited 的命名参数，指示当属性指定在基类上时，是否也会被派生自该基类的类继承。如果属性类的 Inherited 为 true，则该属性会被继承。如果属性类的 Inherited 为 false 则该属性不会被继承。如果未指定，其默认值是 true。

未附加 AttributeUsage 属性的属性类 X，如

```csharp
using System;
class X: Attribute {...}
```

所示，等同于以下内容：

```csharp
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### 17.1.2 位置参数和命名参数

属性类可以具有位置参数和命名参数。属性类的每个公共实例构造函数都为该属性类定义了一个有效的位置参数序列。属性类的每个非静态公共读写字段和属性都为该属性类定义一个命名参数。

示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute : Attribute
{
    public HelpAttribute(string url) {  // Positional parameter
        ...
    }

    public string Topic {
        get {...}
        set {...}
    }  // Named parameter

    public string Url {
        get {...}
    }
}
```

定义了一个名为 HelpAttribute 的属性类，它有一个位置参数 url 和一个命名参数 Topic。尽管 Url 属性是非静态的且为公共，但它不定义命名参数，因为它不是可读写的。

该属性类可能按如下方式使用：

```
[Help("http://www.mycompany.com/.../class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### 17.1.3 属性参数类型

属性类的位置参数和命名参数的类型仅限于属性参数类型，具体如下：

- 以下类型之一：bool、byte、char、double、float、int、long、sbyte、short、string、uint、ulong、ushort。
- 类型 object。
- 类型 System.Type。
- 枚举类型，前提是它具有公共可访问性，并且其中嵌套的类型（如有）也具有公共可访问性 (§17.2)。
- 上述类型的单维数组。

构造函数参数或公共字段如果不具有这些类型之一，则不能在属性规范中用作位置参数或命名参数。

### 17.2 属性规范

属性规范是将先前定义的属性应用于声明。属性是为声明指定的额外声明性信息的一部分。属性可以在全局作用域指定（以指定包含程序集或模块的属性），也可以用于类型声明 (§9.6)、类成员声明 (§10.1.5)、接口成员声明 (§13.2)、结构成员声明 (§11.2)、枚举成员声明 (§14.3)、访问器声明 (§10.7.2)、事件访问器声明 (§10.8.1) 和形式参数列表 (§10.6.1)。

属性在属性节中指定。属性节由一对方括号组成，方括号包围一个或多个属性的逗号分隔列表。在此类列表中指定属性的顺序，以及附加到同一程序实体的节的排列顺序，均无关紧要。例如，属性规范 [A] [B]、[B] [A]、[A, B] 和 [B, A] 是等价的。

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    field
    event
    method
    param
    property
    return
    type

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name
```

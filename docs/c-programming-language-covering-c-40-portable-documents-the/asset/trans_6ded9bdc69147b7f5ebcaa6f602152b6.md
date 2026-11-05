
## 17. 特性

C# 语言的许多部分使程序员能够指定关于程序中定义的实体的声明性信息。例如，类中方法的可访问性通过使用*方法修饰符* *public*、*protected*、*internal* 和 *private* 修饰它来指定。

C# 使程序员能够发明新种类的声明性信息，称为*特性*。然后，程序员可以将特性附加到各种程序实体，并在运行时环境中检索特性信息。例如，框架可能定义一个 HelpAttribute 特性，该特性可以放在某些程序元素（如类和方法）上，以提供从这些程序元素到其文档的映射。

> > **JESSE LIBERTY** 特性的一个常见而强大的用法可以在 Silverlight 和 WPF 中看到，其中特性用于指示与某个类关联的可用*视图状态*。
> >
> > 同样，测试库使用特性将测试方法与支持方法区分开来。Web 服务使用特性指定哪些方法暴露给客户端。

特性通过声明*特性类*（§17.1）来定义，特性类可以具有位置参数和命名参数（§17.1.2）。在 C# 程序中使用*特性说明*（§17.2）将特性附加到实体，并且可以在运行时作为*特性实例*（§17.3）检索。

> > **ERIC LIPPERT** 尽量只使用特性来谈论*类型本身*，而不是表示该类型*语义*的细节。例如，假设你有一个类 *Book*，它有一个属性 *Author*。这是该类语义的一部分：该类表示书籍，而书籍有作者。如果你把 *AuthorAttribute* 放在类 *Book* 上，那并不表示*书籍*的作者，而是表示*类*的作者。类 *Television* 可能有一个属性 *Obsolete*，用于指示某个特定型号是否已停产。如果你把 *ObsoleteAttribute* 放在该类上，这意味着*类本身*已过时，而不是它表示一个过时的产品。

### 17.1 特性类

直接或间接从抽象类 System.Attribute 派生的类都是特性类。特性类的声明定义了一种可以放在声明上的新特性。按照约定，特性类的名称带有 Attribute 后缀。特性的使用可以包含或省略此后缀。

### 17.1.1 特性用法

特性 AttributeUsage（§17.4.1）用于描述特性类可以如何被使用。

AttributeUsage 有一个位置参数（§17.1.2），使特性类能够指定它可用于哪些种类的声明。示例

```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{
    ...
}
```

定义了一个名为 SimpleAttribute 的特性类，它只能放在类声明和接口声明上。示例

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

展示了 Simple 特性的若干用法。尽管该特性定义时名称为 SimpleAttribute，但在使用该特性时，可以省略 Attribute 后缀，从而得到短名称 Simple。因此，上面的示例在语义上等价于以下内容：

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

AttributeUsage 有一个名为 AllowMultiple 的命名参数（§17.1.2），它指示该特性是否可以为一个给定实体指定多次。如果某个特性类的 AllowMultiple 为 true，则该特性类是多次使用特性类，可以在一个实体上指定多次。如果某个特性类的 AllowMultiple 为 false 或未指定，则该特性类是单次使用特性类，在一个实体上最多只能指定一次。

示例

```
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

定义了一个名为 AuthorAttribute 的多次使用特性类。示例

```
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

展示了一个类声明，其中使用了两次 Author 特性。

> CHRIS SELLS 对于正在阅读此示例却不知道 Brian Kernighan 或 Dennis Ritchie 是谁的读者：真可耻！他们是真正的软件传奇。

> JON SKEET 虽然我同意 Chris 的看法，但我当然希望所涉及的两位可敬绅士都不会编写一个名为 Class1 的类。

AttributeUsage 还有另一个名为 Inherited 的命名参数，它指示当特性在基类上指定时，是否也由派生自该基类的类继承。如果某个特性类的 Inherited 为 true，则该特性会被继承。如果某个特性类的 Inherited 为 false，则该特性不会被继承。如果未指定，则其默认值为 true。

一个未附加 AttributeUsage 特性的特性类 X，如下所示：

```
using System;
class X: Attribute {...}
```

等价于以下内容：

```
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true
)]
class X: Attribute {...}
```

### 17.1.2 位置参数和命名参数

> **BILL WAGNER** 在大多数情况下，使用命名参数会得到更清晰、更易于理解的程序。位置参数应仅用于只有一个属性的特性，且该属性由特性名称明确表示，例如 AuthorAttribute。

特性类可以具有*位置参数*和*命名参数*。特性类的每个公共实例构造函数都为该特性类定义有效的位置参数序列。特性类的每个非静态公共读写字段和属性都为该特性类定义命名参数。

示例

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) { // Positional parameter
        ...
    }

    public string Topic {
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

定义了一个名为 HelpAttribute 的特性类，它有一个位置参数 url 和一个命名参数 Topic。尽管属性 Url 是非静态且公共的，但它并不定义命名参数，因为它不是读写的。

该特性类可能按如下方式使用：

```
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}
[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### 17.1.3 特性参数类型

特性类的位置参数和命名参数的类型限于特性参数类型：

- 以下类型之一：bool、byte、char、double、float、int、long、sbyte、short、string、uint、ulong、ushort。
- 类型 object。
- 类型 System.Type。
- 枚举类型，前提是它具有公共可访问性，并且嵌套它的类型（如果有）也具有公共可访问性（§17.2）。
- 上述类型的一维数组。

> JON SKEET 请注意，decimal 不能用作参数类型，即使你可以声明 decimal 常量。这是 CLI 规则渗入 C# 的一个例子。

> MAREK SAFAR 尽管支持数组，但引用类型的特性不允许数组协变。同样，在需要类型 object 的地方不能使用 C# 4.0 的 dynamic 类型。

不具有这些类型之一的构造函数参数或公共字段不能用作特性说明中的位置参数或命名参数。

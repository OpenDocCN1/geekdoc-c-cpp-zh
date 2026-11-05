
委托可以引用静态方法（例如前例中的 Square 或 Math.Sin）或实例方法（例如前例中的 m.Multiply）。引用实例方法的委托还引用特定的对象，并且当通过委托调用实例方法时，该对象在调用中成为 this。

委托也可以使用匿名函数创建，匿名函数是“内联方法”，即即时创建的。匿名函数可以看到周围方法的局部变量。因此上面的乘数示例可以更轻松地编写，而无需使用 Multiplier 类：

```
double[] doubles = Apply(a, (double x) => x * 2.0);
```

委托的一个有趣且有用的特性是它不知道也不关心其引用方法的类；唯一重要的是被引用方法具有与委托相同的参数和返回类型。

> BILL WAGNER  委托的此特性使它们成为提供组件之间接口的优秀工具，其耦合度尽可能低。

## 1.12 属性

类型、成员和 C# 程序中的其他实体支持控制其行为某些方面的修饰符。例如，方法的访问性使用 public、protected、internal 和 private 修饰符控制。C# 将此功能推广，使得用户定义的类型声明信息可以附加到程序实体并在运行时检索。程序通过定义和使用属性来指定此额外的声明信息。

以下示例声明了一个 HelpAttribute 属性，可以将其放置在程序实体上以提供指向其关联文档的链接。

```
using System;

public class HelpAttribute: Attribute
{
    string url;
    string topic;

    public HelpAttribute(string url) {
        this.url = url;
    }

    public string Url {
        get { return url; }
    }
}
```
```csharp
public string Topic {
    get { return topic; }
    set { topic = value; }
}
```

所有属性类都派生自 .NET Framework 提供的 System.Attribute 基类。可以通过在相关声明正前方的方括号内给出其名称以及任何参数来应用属性。如果属性的名称以 Attribute 结尾，则在引用属性时可以省略该部分名称。例如，HelpAttribute 属性可以如下使用。

```
```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) { }
}
```
```

此示例将 HelpAttribute 附加到 Widget 类，并将另一个 HelpAttribute 附加到该类中的 Display 方法。属性类的公共构造函数控制在将属性附加到程序实体时必须提供的信息。可以通过引用属性类的公共读写属性（例如之前对 Topic 属性的引用）来提供额外信息。

以下示例展示了如何使用反射在运行时检索给定程序实体的属性信息。

```
```csharp
using System;
using System.Reflection;
class Test
{
    static void ShowHelp(MemberInfo member) {
        HelpAttribute a = Attribute.GetCustomAttribute(member,
            typeof(HelpAttribute)) as HelpAttribute;
        if (a == null) {
            Console.WriteLine("No help for {0}", member);
        }
        else {
            Console.WriteLine("Help for {0}:", member);
            Console.WriteLine(" Url={0}, Topic={1}",
                a.Url, a.Topic);
        }
    }
    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```
```

当通过反射请求特定属性时，将使用程序源中提供的信息调用属性类的构造函数，并返回 resulting 属性实例。如果通过属性提供了额外信息，则在返回属性实例之前将这些属性设置为给定值。

> **BILL WAGNER** 属性的全部潜力将在 C# 编译器的某个未来版本实现时得以实现，该版本使开发人员能够读取属性并在编译器创建 IL 之前使用它们修改代码模型。我希望能够使用属性来改变代码的行为，自 C# 首次发布以来我就想要这样做。

*本页特意留空*

## 2. 词法结构

### 2.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元 (§9.1)。源文件是有序的 Unicode 字符序列。源文件通常与文件系统中的文件一一对应，但这种对应关系不是必需的。为了最大限度地提高可移植性，建议文件系统中的文件使用 UTF-8 编码。

从概念上讲，程序的编译使用三个步骤：

- 1. 转换，将文件从特定的字符集和编码方案转换为 Unicode 字符序列。
- 2. 词法分析，将 Unicode 输入字符流翻译成标记流。
- 3. 语法分析，将标记流翻译成可执行代码。

### 2.2 语法

本规范使用两种语法来描述 C# 编程语言的语法。词法语法 (§2.2.2) 定义了 Unicode 字符如何组合形成行终止符、空白、注释、标记和预处理指令。语法语法 (§2.2.3) 定义了词法语法产生的标记如何组合形成 C# 程序。

### 2.2.1 语法记法

词法和语法语法使用语法产生式呈现。每个语法产生式定义一个非终结符以及该非终结符可能扩展为非终结符或终结符序列。 在语法产生式中，非终结符以斜体显示，终结符以等宽字体显示。

语法产生式的第一行是非终结符的名称，后跟冒号。每个后续缩进的行包含非终结符的可能扩展，表示为非终结符或终结符序列。例如，产生式

```
```
while-statement:
    while ( boolean-expression ) embedded-statement
```
```

定义 while-statement 由标记 while 组成，后跟标记“(”，后跟 boolean-expression，后跟标记“)”，后跟 embedded-statement。

当非终结符有多个可能扩展时，备选方案列在单独的行上。例如，产生式

```
```
statement-list:
    statement
    statement-list statement
```
```

定义 statement-list 要么由 statement 组成，要么由 statement-list 后跟 statement 组成。换句话说，该定义是递归的，并指定语句列表由一个或多个语句组成。

下标后缀“_opt”用于表示可选符号。产生式

```
```
block:
    { statement-list_opt }
```
```

是以下内容的简写

```
```
block:
    {   }
    { statement-list }
```
```

并定义 block 由“{”和“}”标记包围的可选 statement-list 组成。

备选方案通常列在单独的行上，尽管在备选方案很多的情况下，短语“one of”可能会先于单行给出的扩展列表。这只是逐行列出每个备选方案的简写。例如，产生式

```
```
real-type-suffix: one of
    F f D d M m
```
```

是以下内容的简写

```
```
real-type-suffix:
    F
    f
    D
    d
    M
    m
```
```

### 2.2.2 词法语法

C# 的词法语法在 §2.3、§2.4 和 §2.5 中呈现。词法语法的终结符是 Unicode 字符集的字符，词法语法指定字符如何组合形成标记 (§2.4)、空白 (§2.3.3)、注释 (§2.3.2) 和预处理指令 (§2.5)。

C# 程序中的每个源文件必须符合词法语法 (§2.3) 的 *input* 产生式。

### 2.2.3 语法语法

C# 的语法语法在后续章节和附录中呈现。语法语法的终结符是词法语法定义的标记，语法语法指定标记如何组合形成 C# 程序。

C# 程序中的每个源文件必须符合语法语法 (§9.1) 的 *compilation-unit* 产生式。

### 2.3 词法分析

*input* 产生式定义了 C# 源文件的词法结构。C# 程序中的每个源文件必须符合此词法语法产生式。

```
```
input:
    input-section_opt

input-section:
    input-section-part
    input-section input-section-part

input-section-part:
    input-elements_opt new-line
    pp-directive
```
```

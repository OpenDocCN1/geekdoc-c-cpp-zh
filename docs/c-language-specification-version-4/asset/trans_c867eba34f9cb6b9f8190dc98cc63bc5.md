
此示例将 HelpAttribute 附加到 Widget 类，并将另一个 HelpAttribute 附加到该类中的 Display 方法。属性类的公共构造函数控制在将属性附加到程序实体时必须提供的信息。可以通过引用属性类的公共读写属性来提供附加信息（如之前对 Topic 属性的引用）。

以下示例展示了如何使用反射在运行时检索给定程序实体的属性信息。

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
            Console.WriteLine("  Url={0}, Topic={1}", a.Url, a.Topic);
        }
    }

    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```

当通过反射请求特定属性时，将使用程序源中提供的信息调用属性类的构造函数，并返回由此产生的属性实例。如果通过属性提供了附加信息，则在返回属性实例之前，这些属性将被设置为给定值。

## 2. 词法结构

### 2.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元（§9.1）。源文件是有序的 Unicode 字符序列。源文件通常与文件系统中的文件一一对应，但这种对应关系不是必需的。为了最大限度地提高可移植性，建议将文件系统中的文件使用 UTF-8 编码。

概念上讲，程序的编译使用三个步骤：

- 1. 转换，将文件从特定的字符集和编码方案转换为 Unicode 字符序列。
- 2. 词法分析，将 Unicode 输入字符流转换为标记流。
- 3. 语法分析，将标记流转换为可执行代码。

### 2.2 语法

本规范使用两种语法来描述 C# 编程语言的语法。词法语法（§2.2.2）定义了 Unicode 字符如何组合形成行终止符、空白、注释、标记和预处理指令。语法语法（§2.2.3）定义了词法语法产生的标记如何组合形成 C# 程序。

### 2.2.1 语法记法

词法和语法语法使用语法产生式呈现。每个语法产生式定义一个非终结符以及该非终结符可能扩展为非终结符或终结符序列。 在语法产生式中，非终结符以斜体显示，而终结符以等宽字体显示。

语法产生式的第一行是非终结符的名称，后跟冒号。每个后续缩进的行包含非终结符的可能扩展，表示为非终结符或终结符的序列。例如，产生式：

```
while-statement:
    while ( boolean-expression ) embedded-statement
```

定义 while-statement 由标记 while 组成，后跟标记“（”，后跟 boolean-expression，后跟标记“）”，后跟 embedded-statement。

当非终结符有多个可能的扩展时，备选方案会列在单独的行上。例如，产生式：

是简写形式：

```
~~~
    block:
        {   }
        {   statement-list   }
~~~
```

并定义 *block* 由可选的 *statement-list* 组成，被“{”和“}”标记包围。

备选方案通常列在单独的行上，尽管在备选方案很多的情况下，短语“one of”可能会先于在一行上给出的扩展列表。这只是逐行列出每个备选方案的简写形式。例如，产生式：

```
~~~
    real-type-suffix:  one of
        F   f   D   d   M   m
~~~
```

是简写形式：

```
~~~
    real-type-suffix:
        F
        f
        D
        d
        M
        m
~~~
```

### 2.2.2 词法语法

C# 的词法语法在 §2.3、§2.4 和 §2.5 中呈现。词法语法的终结符是 Unicode 字符集的字符，词法语法指定字符如何组合形成标记（§2.4）、空白（§2.3.3）、注释（§2.3.2）和预处理指令（§2.5）。

C# 程序中的每个源文件必须符合词法语法（§2.3）的 *input* 产生式。

### 2.2.3 语法语法

C# 的语法语法在随后本章的章节和附录中呈现。语法语法的终结符是由词法语法定义的标记，语法语法指定标记如何组合形成 C# 程序。

C# 程序中的每个源文件必须符合语法语法（§9.1）的 *compilation-unit* 产生式。

### 2.3 词法分析

*input* 产生式定义了 C# 源文件的词法结构。C# 程序中的每个源文件必须符合此词法语法产生式。

```
~~~
    input:
        input-section_opt

    input-section:
        input-section-part
        input-section  input-section-part

    input-section-part:
        input-elements_opt  new-line
        pp-directive
~~~
```

```
input-elements:
  input-element
  input-elements input-element

input-element:
  whitespace
  comment
  token
```

五个基本元素构成了 C# 源文件的词法结构：行终止符（§2.3.1）、空白（§2.3.3）、注释（§2.3.2）、标记（§2.4）和预处理指令（§2.5）。在这些基本元素中，只有标记在 C# 程序的语法语法（§2.2.3）中才有意义。

C# 源文件的词法处理包括将文件简化为标记序列，该序列成为语法分析的输入。行终止符、空白和注释可以用于分隔标记，预处理指令可以导致源文件的某些部分被跳过，但除此之外，这些词法元素对 C# 程序的语法结构没有影响。

当多个词法语法产生式匹配源文件中的字符序列时，词法处理总是形成最长的可能词法元素。例如，字符序列 // 被处理为单行注释的开始，因为该词法元素比单个 / 标记更长。

### 2.3.1 行终止符

行终止符将 C# 源文件的字符划分为行。

```
new-line:
  Carriage return character (U+000D)
  Line feed character (U+000A)
  Carriage return character (U+000D) followed by line feed character (U+000A)
  Next line character (U+0085)
  Line separator character (U+2028)
  Paragraph separator character (U+2029)
```

为了与添加文件结束标记的源代码编辑工具兼容，并使源文件能够作为一系列正确终止的行来查看，以下转换按顺序应用于 C# 程序中的每个源文件：

- 如果源文件的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果源文件非空且源文件的最后一个字符不是回车（U+000D）、换行（U+000A）、行分隔符（U+2028）或段落分隔符（U+2029），则在源文件末尾添加一个回车字符（U+000D）。

### 2.3.2 注释

支持两种形式的注释：单行注释和定界注释。单行注释以字符 // 开始并延伸到源行末尾。定界注释以字符 /* 开始并以字符 */ 结束。定界注释可以跨越多行。

```
comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt
```

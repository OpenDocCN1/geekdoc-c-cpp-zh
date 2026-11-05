
| 格式说明符 | 描述 |
|---|---|
| \ | 使用 C 语言格式序列，例如 '\n'（换行）。在某些语言中，当转义字符本身作为字面量使用时，要求在其前面再加一个转义字符。否则，编译器会将该字符解释为转义序列。并非所有编程语言都要求支持此转义字符。 |
| 'ABC' "ABC" | **字面量字符串：** 用单引号或双引号括起来的字符会按字面复制到输出字符串中，不影响格式。 |
| ;（分号） | **节分隔符：** ';' 字符用于在格式字符串中分隔正数、负数和零的节。（下面将详细介绍此功能。） |
| 其他 | **所有其他字符：** 所有其他字符都会按字面量存储到输出字符串中其出现的位置。 |

注意，对于定点格式字符串（不包含 'E0'、'E+0'、'E-0'、'e0'、'e+0' 或 'e-0' 的字符串），数字会舍入到小数点分隔符右侧的零占位符或数字占位符数量所指定的小数位数。如果自定义格式不包含小数点分隔符，则数字舍入到最接近的整数。如果数字的位数多于小数点分隔符左侧的零占位符或数字占位符的数量，则多余的数字会紧挨着第一个零占位符或数字占位符之前复制到输出字符串中。

自定义格式最多可包含三个节，节之间由节分隔符字符分隔，用于为正数、负数和零值指定不同的格式。各节的解释如下：

- **一个节：** 自定义格式适用于所有值（正数、负数和零）。负值包含负号。
- **两个节：** 第一节适用于正值和零，第二节适用于负值。如果要格式化的值为负，但按第二节中的格式舍入后变为零，则生成的零按第一节格式化。负值不包含负号，以便完全控制负值的表示形式。例如，可以使用类似于 '######.####;(######.####)' 的自定义格式，用括号表示负数。
- **三个节：** 第一节适用于正值，第二节适用于负值，第三节适用于零。第二节可以为空（分号之间不出现任何内容），在这种情况下，第一节适用于所有非零值，且负值包含负号。如果要格式化的数字非零，但按第一节或第二节中的格式舍入后变为零，则生成的零按第三节格式化。

System.Enum 和 System.DateTime 类型也支持使用格式说明符来格式化值的字符串表示形式。特定格式说明符的含义取决于要格式化的数据类型（数值、日期/时间、枚举）。有关每种类型支持的格式说明符的完整列表，请参阅 System.Enum 和 System.Globalization.DateTimeFormatInfo。

## C.5 库类型缩写

本规范引用了以下库类型。这些类型的完整名称（包括全局命名空间限定符）列于下方。在本规范中，这些类型以完全限定名、省略全局命名空间限定符的名称、或省略命名空间的简单非限定类型名出现。例如，本规范中使用的类型 `ICollection<T>` 始终表示类型 `global::System.Collections.Generic.ICollection<T>`。

- global::System.Action
- global::System.ArgumentException
- global::System.ArithmeticException
- global::System.Array
- global::System.ArrayTypeMismatchException
- global::System.Attribute
- global::System.AttributeTargets
- global::System.AttributeUsageAttribute
- global::System.Boolean
- global::System.Byte
- global::System.Char
- global::System.Collections.Generic.ICollection<T>
- global::System.Collections.Generic.IEnumerable<T>
- global::System.Collections.Generic.IEnumerator<T>
- global::System.Collections.Generic.IList<T>
- global::System.Collections.Generic.IReadOnlyCollection<out T>
- global::System.Collections.Generic.IReadOnlyList<out T>
- global::System.Collections.ICollection
- global::System.Collections.IEnumerable
- global::System.Collections.IList
- global::System.Collections.IEnumerator
- global::System.Decimal
- global::System.Delegate
- global::System.Diagnostics.ConditionalAttribute
- global::System.DivideByZeroException
- global::System.Double
- global::System.Enum
- global::System.Exception
- global::System.GC
- global::System.ICollection
- global::System.IDisposable
- global::System.IEnumerable
- global::System.IEnumerable<out T>
- global::System.IList
- global::System.IndexOutOfRangeException
- global::System.Int16
- global::System.Int32
- global::System.Int64
- global::System.IntPtr
- global::System.InvalidCastException
- global::System.InvalidOperationException
- global::System.Linq.Expressions.Expression<TDelegate>
- global::System.MemberInfo
- global::System.NotSupportedException
- global::System.Nullable<T>
- global::System.NullReferenceException
- global::System.Object
- global::System.ObsoleteAttribute
- global::System.OutOfMemoryException
- global::System.OverflowException
- global::System.Runtime.CompilerServices.CallerFileAttribute
- global::System.Runtime.CompilerServices.CallerLineNumberAttribute
- global::System.Runtime.CompilerServices.CallerMemberNameAttribute
- global::System.Runtime.CompilerServices.ICriticalNotifyCompletion
- global::System.Runtime.CompilerServices.IndexerNameAttribute
- global::System.Runtime.CompilerServices.INotifyCompletion
- global::System.Runtime.CompilerServices.TaskAwaiter
- global::System.Runtime.CompilerServices.TaskAwaiter<T>
- global::System.SByte
- global::System.Single
- global::System.StackOverflowException
- global::System.String
- global::System.SystemException
- global::System.Threading.Monitor
- global::System.Threading.Tasks.Task
- global::System.Threading.Tasks.Task<TResult>
- global::System.Type
- global::System.TypeInitializationException
- global::System.UInt16
- global::System.UInt32
- global::System.UInt64
- global::System.UIntPtr
- global::System.ValueType

资料性文本结束。

## D. 文档注释

**本附录为资料性内容。**

### D.1 概述

C# 为程序员提供了一种机制，使其可以使用包含 XML 文本的注释语法来记录代码。在源代码文件中，具有特定形式的注释可用于指示工具根据这些注释及其前面的源代码元素生成 XML。使用此类语法的注释称为**文档注释**。它们必须紧邻用户定义类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为**文档生成器**。（该生成器可以是 C# 编译器本身，但不必是。）文档生成器生成的输出称为**文档文件**。文档文件用作**文档查看器**的输入：文档查看器是一种旨在以某种可视方式显示类型信息及其关联文档的工具。

符合规范的 C# 编译器不要求检查文档注释的语法；此类注释只是普通注释。但是，允许符合规范的编译器进行此类检查。

本规范建议在文档注释中使用一组标准标记，但不要求使用这些标记；如果需要，也可以使用其他标记，只要遵循格式良好的 XML 规则即可。对于面向 CLI 的 C# 实现，它还提供了有关文档生成器和文档文件格式的信息。未提供有关文档查看器的信息。

### D.2 简介

具有特定形式的注释可用于指示工具根据这些注释及其前面的源代码元素生成 XML。此类注释是以三个斜杠（///）开头的*单行注释*（§6.3.3），或是以一个斜杠和两个星号（/**）开头的*分隔注释*（§6.3.3）。它们必须紧邻其所注释的用户定义类型或成员之前。特性节（§21.3）被视为声明的一部分，因此文档注释必须位于应用于类型或成员的特性之前。

为便于说明，下面以两条语法规则展示文档注释的格式：*Single_Line_Doc_Comment* 和 *Delimited_Doc_Comment*。但是，这些规则*并非* C# 语法的一部分，而是分别表示 *Single_Line_Comment* 和 *Delimited_Comment* 词法规则的特定格式。

```
Syntax:
Single_Line_Doc_Comment
  : '///' Input_Character*
  ;

Delimited_Doc_Comment
```

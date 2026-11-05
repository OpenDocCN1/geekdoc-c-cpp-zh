
| Format Specifier | Description |
|---|---|
| \ | with C language formatting sequences, such as '\n' (newline). In some languages, the escape character itself is required to be preceded by an escape character when used as a literal. Otherwise, the compiler interprets the character as an escape sequence. This escape character is not required to be supported in all programming languages. |
| 'ABC' "ABC" | **Literal string:** Characters enclosed in single or double quotes are copied to the output string literally, and do not affect formatting. |
| ; (semicolon) | **Section separator:** The ';' character is used to separate sections for positive, negative, and zero numbers in the format string. (This feature is described in detail below.) |
| Other | **All other characters:** All other characters are stored in the output string as literals in the position in which they appear. |

Note that for fixed-point format strings (strings not containing an 'E0', 'E+0', 'E-0', 'e0', 'e+0', or 'e-0'), numbers are rounded to as many decimal places as there are Zero or Digit placeholders to the right of the decimal separator. If the custom format does not contain a decimal separator, the number is rounded to the nearest integer. If the number has more digits than there are Zero or Digit placeholders to the left of the decimal separator, the extra digits are copied to the output string immediately before the first Zero or Digit placeholder.

A custom format can contain up to three sections separated by section separator characters, to specify different formatting for positive, negative, and zero values. The sections are interpreted as follows:

- **One section:** The custom format applies to all values (positive, negative and zero). Negative values include a negative sign.
- **Two sections:** The first section applies to positive values and zeros, and the second section applies to negative values. If the value to be formatted is negative, but becomes zero after rounding according to the format in the second section, then the resulting zero is formatted according to the first section. Negative values do not include a negative sign to allow full control over representations of negative values. For example, a negative can be represented in parenthesis using a custom format similar to '######.####;(######.####)'.
- **Three sections:** The first section applies to positive values, the second section applies to negative values, and the third section applies to zeros. The second section can be empty (nothing appears between the semicolons), in which case the first section applies to all nonzero values, and negative values include a negative sign. If the number to be formatted is nonzero, but becomes zero after rounding according to the format in the first or second section, then the resulting zero is formatted according to the third section.

The System.Enum and System.DateTime types also support using format specifiers to format string representations of values. The meaning of a specific format specifier varies according to the kind of data (numeric, date/time, enumeration) being formatted. See System.Enum and System.Globalization.DateTimeFormatInfo for a comprehensive list of the format specifiers supported by each type.

## C.5 Library Type Abbreviations

The following library types are referenced in this specification. The full names of those types, including the global namespace qualifier are listed below. Throughout this specification, these types appear as either the fully qualified name; with the global namespace qualifier omitted; or as a simple unqualified type name, with the namespace omitted as well. For example, the type `ICollection<T>`, when used in this specification, always means the type `global::System.Collections.Generic.ICollection<T>`.

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

End of informative text.

## D. Documentation comments

**This annex is informative.**

### D.1 General

C# provides a mechanism for programmers to document their code using a comment syntax that contains XML text. In source code files, comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede. Comments using such syntax are called **documentation comments**. They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method). The XML generation tool is called the **documentation generator**. (This generator could be, but need not be, the C# compiler itself.) The output produced by the documentation generator is called the **documentation file**. A documentation file is used as input to a **documentation viewer**: a tool intended to produce some sort of visual display of type information and its associated documentation.

A conforming C# compiler is not required to check the syntax of documentation comments; such comments are simply ordinary comments. A conforming compiler is permitted to do such checking, however.

This specification suggests a set of standard tags to be used in documentation comments, but use of these tags is not required, and other tags may be used if desired, as long as the rules of well-formed XML are followed. For C# implementations targeting the CLI, it also provides information about the documentation generator and the format of the documentation file. No information is provided about the documentation viewer.

### D.2 Introduction

Comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements that they precede. Such comments are *Single-Line_Comments* (§6.3.3) that start with three slashes (///), or *Delimited_Comments* (§6.3.3) that start with a slash and two asterisks (/**). They must immediately precede a user-defined type or a member that they annotate. Attribute sections (§21.3) are considered part of declarations, so documentation comments must precede attributes applied to a type or member.

For expository purposes, the format of document comments is shown below as two grammar rules: *Single_Line_Doc_Comment* and *Delimited_Doc_Comment*. However, these rules are *not* part of the C# grammar, but rather, they represent particular formats of *Single_Line_Comment* and *Delimited_Comment* lexer rules, respectively.

```
Syntax:
Single_Line_Doc_Comment
  : '///' Input_Character*
  ;

Delimited_Doc_Comment
```

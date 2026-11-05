
## 2.2. Top-Level Statements

Since C# 9, one source file in a program may use top-level statements as long as the program does not include any other entry point methods. It is a syntactic sugar to help remove some boilerplate code. The top-level statements are automatically wrapped in the Main method of an implicitly defined startup class.

Top-level statements can access the command line arguments using the implicitly defined variable args of type string[].

If the top-level statements return an integer value, that value becomes the integer return code to the operating system/runtime.

The top-level statements may contain async expressions.

For example,

```
Console.WriteLine("Hello World");
```

A file including this one line of code, using the implicit global using feature available since C# 10, is more or less equivalent to something like the following:

```
namespace Namespace1 {
    class Program {
        static void Main(string[] args) {
            Console.WriteLine("Hello World!");
        }
    }
}
```

As of C# 11, there are some restrictions:

- Only one file in your application may use top-level statements.
- All top-level statements in that file should be placed before any other namespace members such as type declarations.
- A program cannot have both top-level statements and an explicit entry point, e.g., a Main method.

## 2.3. Declarations

A C# program comprises a series of namespaces. A namespace can include other declarations, or "members". When the non-namespace member declarations are included in a program with no explicitly specified enclosing namespace, they belong to the "global namespace".

Namespace members can be type declarations or other (nested) namespace declarations. Type declarations are used to define classes, structs, records, enums, interfaces, and delegates. A type declaration can include other members. For instance, class declarations can contain declarations for constants, fields, properties, events, indexers, operators, methods, instance and static constructors, finalizers, and other nested types.

## 2.4. Access Control

Access of the top-level type declarations (e.g., within a namespace) can be controlled using one of the following accessibility declarations:

Note that namespaces do not provide access limitations. That is, they are all implicitly

Access of the members of the type declarations (top-level or nested) is largely limited by the accessibility of their containing types, and it can be additionally controlled using some of the following access modifiers, depending on the types:

Note that

All members of an interface or an enum are public by default, and access modifiers cannot be used.

Any access modifiers can be used for the members of a class.

Only public and private can be used for the members of a struct.

The default access level is private for the members of a class, record, and struct.

## 2.5. Blocks and Scopes

### 2.5.1. Scopes

C# is a lexically scoped language. The scope of a name is statically determined to be a particular region of program text, within which the entity declared by the name can be referred to without qualification of the name.

Scopes can be nested, and an inner scope may redeclare the meaning of a name from an outer scope. The name from the outer scope is then said to be "hidden" in the region of program text covered by the inner scope, and access to the hidden name is only possible by using the qualified name.

### 2.5.2. Blocks

A block statement permits multiple statements to be written in contexts where a single statement is allowed. A block consists of zero, one, or more statements written between the delimiters { and }.

For example,

```
{
  STATEMENTS
}
```

The STATEMENTS consists of zero, one, or more statements.

Note that the scope of a local variable or constant declared in a block is effectively the same block.

## 3. Lexical Analysis

C# uses a 16-bit encoding of Unicode code points in character and string values. A Unicode escape sequence, \U or \u followed by a hexadecimal number, can be used to represent a Unicode code point in certain lexical contexts. That is, the Unicode escape sequences are processed in character literals, string literals, interpolated string expressions, and identifiers (but, not in keywords). For example, the sequence \u0061 in a string literal "\u0061pple" represents a lowercase letter 'a'. Hence this string literal is equivalent to

### 3.1. Lexical Elements

The following 5 elements make up the lexical structure of a C# program:

- Line terminators,
- White space,
- Comments,
- Compiler, or pre-processing, directives, and
- Tokens such as keywords and literals.

Compiler directives allow selective compilation of a program text, but otherwise they have no impact on its syntactic structure.

### 3.1.1. Line terminators

Line terminator elements divide the characters of a C# compilation unit into lines. Line terminators are:

- Carriage return
- Line feed
- Next line character
- Line separator and
- Paragraph separator

### 3.1.2. White space

White space in C# is defined as

- Any character with Unicode class Zs, including the ASCII space character
- The horizontal tab character
- The vertical tab character and
- The form feed character

### 3.1.3. Comments

C# supports two forms of comments, the C-style delimited comments and the C++-style single-line comments.

A delimited comment begins and ends with the character sequences `/*` and `*/` respectively.

A single-line comment begins with the character sequence `//` and extends to the end of the same line.

```
/* Delimited comment can span
multiple lines */
using /*or, even just a portion of a line */ System;

// A single line comment.
Console.WriteLine("Hello /* Not a comment */ World.");
```

Note that comments cannot be included in the <u>string</u>. White spaces and comments act as separators for tokens.

### 3.2. Tokens

Of the 5 basic [lexical elements] listed in the previous section, only tokens are significant in the syntactic grammar of a C# program. Tokens can be classified into identifiers, keywords, literals, operators, and other punctuation symbols. [Literals] are explained in the next section.

### 3.2.1. Identifiers

The C# identifiers comprise Unicode characters, and the rules of identifiers are generally similar to those found in other C-style languages. For example, an identifier can start with a letter or an underscore _ and it can include other letters and numbers, etc. There are a few things to note:

Unicode escape sequences are permitted in identifiers.

Use of more than one consecutive underscores (e.g., __ is, although legal, discouraged.

An identifier can be optionally preceded with a single @ character.

The verbatim identifiers are typically used to "escape" the C# keywords, and otherwise its use is discouraged.

In this chapter, we introduce query expressions and use them to express many of the queries from the preceding chapter.

# Introducing Query Expressions

Two of the operations that developers most frequently perform are **filtering** the collection to eliminate unwanted items and **projecting** the collection so that the items take a different form. For example, given a collection of files, we could filter it to create a new collection of only the files with a .cs extension or only the files larger than 1 million bytes. We could also project the file collection to create a new collection of paths to the directories where the files are located and the corresponding directory size. Query expressions provide straightforward syntaxes for both of these common operations. Listing 16.1 shows a query expression that filters a collection of strings; Output 16.1 shows the results.

# LISTING 16.1: Simple Query Expression

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

static string[] Keywords = {
    "abstract", "add", "alias", "as", "ascending",
    "async", "await", "base", "bool", "break",
    "by", "byte", "case", "catch", "char", "checked",
    "class", "const", "continue", "decimal", "default",
    "delegate", "descending", "do", "double",
    "dynamic", "else", "enum", "event", "equals",
    "explicit", "extern", "false", "finally", "fixed",
    "from", "float", "for", "foreach", "get", "global",
    "group", "goto", "if", "implicit", "in", "int",
    "into", "interface", "internal", "is", "lock", "long",
    "join", "let", "nameof", "namespace", "new", "null",
    "object", "on", "operator", "orderby", "out",
    "override", "params", "partial", "private", "protected",
    "public", "readonly", "ref", "remove", "return", "sbyte",
    "sealed", "select", "set", "short", "sizeof",
    "stackalloc", "static", "string", "struct", "switch",
    "this", "throw", "true", "try", "typeof", "uint", "ulong",
    "unsafe", "ushort", "using", "value", "var", "virtual",
    "unchecked", "void", "volatile", "where", "while", "yield"};
```
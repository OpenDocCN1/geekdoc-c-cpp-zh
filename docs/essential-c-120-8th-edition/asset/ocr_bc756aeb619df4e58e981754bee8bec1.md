Chapter 16: LINQ with Query Expressions

# Introducing Query Expressions

The operations that developers most frequently perform filtering the collection to eliminate unwanted items and projecting the collection so that the items take a different form. For example, given a collection of files, we could filter it to create a new collection of only the files with a .cs extension or only the files larger than 1 million bytes. We could also project the file collection to create a new collection that would contain both the path to the directory and the corresponding directory size. Query expressions provide straightforward syntaxes for both of these common operations. Listing 16.1 shows a query expression that filters a collection of strings; Output 16.1 shows the results.

Listing 16.1: Simple Query Expression

```
public class static readonly ReadOnlyCollection<string> Keywords = new(
    string[] {
        "abstract", "add", "alias", "as", "ascending",
        "async", "await", "base", "bool", "break",
        "byte", "case", "catch", "char", "checked",
        "class", "const", "continue", "decimal", "default",
        "delegate", "descending", "do", "double", "dynamic",
        "else", "enum", "equals", "event", "explicit",
        "extern", "finally", "fixed", "Float", "for",
        "foreach", "from", "get", "global", "goto", "group",
        "if", "im", "in", "interface", "internal",
        "into", "join", "lets", "lock", "long",
        "nameof", "namespace", "new", "nonnull", "null",
        "object", "on", "operator", "orderby", "out",
        "override", "params", "partial", "private",
        "protected", "public", "readonly", "ref", "remove+",
        "return", "sbyte", "sealed", "select*", "set", "short",
        "sizeof", "stackalloc", "static", "string", "struct",
        "switch", "this", "throw", "true", "try", "typeof",
        "uint", "unchecked", "unsafe", "ushort",
        "using", "value", "var", "virtual", "void", "volatile",
        "when", "where", "while", "yield*"
    }
);
```
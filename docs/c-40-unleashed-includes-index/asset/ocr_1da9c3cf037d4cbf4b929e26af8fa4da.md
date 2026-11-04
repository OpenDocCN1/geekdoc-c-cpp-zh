```
```csharp
for (int i = 0; i >= 0; i--)
{
    // Use integer value i if desired.
}
```
```

# MANUAL ARRAY INDEXING OR FOREACH?

Given the length of an array and the fact that indexing is zero-based, the typical loop structure shown earlier is a popular technique to iterate over the elements of an array. However, enumeration over collections—including arrays—is such a common thing that the BCL defines IEnumerable and IEnumerator interfaces for such tasks. Languages such as C# and VB provide for-each loop constructs that build on top of that. So unless you need the index for elements, a foreach loop will yield cleaner code.

The iterator part is where a postfix increment operator is used, effectively increasing the integer variable i with 1. In effect, we're only using the postfix increment operator for this side effect in the preceding example. However, being expressions, those operators produce a value that can be used any place expressions can occur. The difference between postfix and prefix behavior lies in what the resulting value is.

+   - Prefix operators perform the increment or decrement operation first and produce the resulting value.
+   - Postfix operators produce the value before the increment or decrement operation is carried out.

# PRE, POST, IN

To make sure everyone is on the same page, a short explanation of vocabulary is in order here. Pre stands for before or “in front of.” Examples include !b, -i, ~f, and ++x, where the operator appears before its operand. Post is the opposite, meaning “after,” as in x++, where the operator appears behind the operand. Finally, in means “in between,” as with a + b and other binary operators in C#.

Prefix and postfix notation are not limited to unary operators; you can think of + a b and a b + as valid syntaxes for addition. In fact, LISP prefers the use of prefix syntax, whereas evaluators typically like postfix notation. (For example, in the stack-driven world of IL, an operator appears after the operands are pushed onto the evaluation stack.)

A few examples will clarify this behavior, starting with the postfix case:

```
```csharp
int x = 0;

// The value before the increment is assigned, so y will be set to 0.
int y = x++;
```
```
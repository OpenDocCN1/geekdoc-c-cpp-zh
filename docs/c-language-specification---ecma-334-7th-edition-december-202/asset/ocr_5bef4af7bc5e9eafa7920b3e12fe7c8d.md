Since the TextWriter and TextReader classes implement the IDisposable interface, the example can use using statements to ensure that the underlying file is properly closed following the write or read operations.

*end example*

# 13.15 The yield statement

The yield statement is used in an iterator block (§13.3) to yield a value to the enumerator object (§15.14.5) or enumerable object (§15.14.6) of an iterator or to signal the end of the iteration.

```
yield_statement
  : 'yield' 'return' expression ';'
  | 'yield' 'break' ';'
  ;
```

yield is a contextual keyword (§6.4.4) and has special meaning only when used immediately before a return or break keyword.

There are several restrictions on where a yield statement can appear, as described in the following.

+   - It is a compile-time error for a yield statement (of either form) to appear outside a method_body, operator_body, or accessor_body.
+   - It is a compile-time error for a yield statement (of either form) to appear inside an anonymous function.
+   - It is a compile-time error for a yield statement (of either form) to appear in the finally clause of a try statement.
+   - It is a compile-time error for a yield return statement to appear anywhere in a try statement that contains any catch_clauses.

Example: The following example shows some valid and invalid uses of yield statements.

```
delegate IEnumerable<int> D();

IEnumerator<int> GetEnumerator()
{
    try
    {
        yield return 1; // Ok
        yield break;    // Ok
    }
    finally
    {
        yield return 2; // Error, yield in finally
        yield break;    // Error, yield in finally
    }
    try
    {
        yield return 3; // Error, yield return in try/catch
        yield break;    // Ok
    }
    catch
    {
        yield return 4; // Error, yield return in try/catch
    }
}
```
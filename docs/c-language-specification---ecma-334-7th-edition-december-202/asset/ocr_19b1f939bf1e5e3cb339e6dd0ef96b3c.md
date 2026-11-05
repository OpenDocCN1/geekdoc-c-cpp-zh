```
```
while (e.MoveNext())
{
    V v = (V)(T)e.Current;
    «embedded_statement»
}
finally
{
    ... // Dispose e
}
```
```

The variable e is not visible to or accessible to the expression x or the embedded statement or any other source code of the program. The variable v is read-only in the embedded statement. If there is not an explicit conversion (§10.3) from T (the iteration type) to V (the local_variable_type in the foreach statement), an error is produced and no further steps are taken.

When the iteration variable is a reference variable (§9.7), a foreach statement of the form

```
foreach (ref V v in x) «embedded_statement»
```

is then equivalent to:

```
```
{
    E e = ((C)(x)).GetEnumerator();
    try
    {
        while (e.MoveNext())
        {
            ref V v = ref e.Current;
            «embedded_statement»
        }
    }
    finally
    {
        ... // Dispose e
    }
}
```
```

The variable e is not visible or accessible to the expression x or the embedded statement or any other source code of the program. The reference variable v is read-write in the embedded statement, but v shall not be ref-reassigned (§12.21.3). If there is not an identity conversion (§10.2.2) from T (the iteration type) to V (the local_variable_type in the foreach statement), an error is produced and no further steps are taken.

A foreach statement of the form foreach (ref readonly V v in x) «embedded_statement» has a similar equivalent form, but the reference variable v is ref readonly in the embedded statement, and therefore cannot be ref-reassigned or reassigned.

Note: If x has the value null, a System.NullReferenceException is thrown at run-time. end note

An implementation is permitted to implement a given foreach_statement differently; e.g., for performance reasons, as long as the behavior is consistent with the above expansion.

The placement of v inside the while loop is important for how it is captured (§12.19.6.2) by any anonymous function occurring in the embedded_statement.

# Example:
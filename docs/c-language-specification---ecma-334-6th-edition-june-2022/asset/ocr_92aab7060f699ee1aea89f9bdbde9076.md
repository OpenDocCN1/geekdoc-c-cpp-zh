interface as described below. It is recommended that a warning be issued if overload resolution produces anything except an unambiguous public instance method or no applicable methods.

+   - If the return type E of the GetEnumerator method is not a class, struct or interface type, an error is produced and no further steps are taken.
+   - Member lookup is performed on E with the identifier Current and no type arguments. If the member lookup produces no match, the result is an error, or the result is anything except a public instance property that permits reading, an error is produced and no further steps are taken.
+   - Member lookup is performed on E with the identifier MoveNext and no type arguments. If the member lookup produces no match, the result is an error, or the result is anything except a method group, an error is produced and no further steps are taken.
+   - Overload resolution is performed on the method group with an empty argument list. If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, or its return type is not bool, an error is produced and no further steps are taken.
+   - The collection type is X, the enumerator type is E, and the iteration type is the type of the Current property.

Otherwise, check for an enumerable interface:

+   - If among all the types T_i for which there is an implicit conversion from X to IEnumerable<T_i>, there is a unique type T such that T is not dynamic and for all the other T_i there is an implicit conversion from IEnumerable<T> to IEnumerable<T_i>, then the collection type is the interface IEnumerable<T>, the enumerator type is the interface IEnumerator<T>, and the iteration type is T.
+   - Otherwise, if there is more than one such type T, then an error is produced and no further steps are taken.
+   - Otherwise, if there is an implicit conversion from X to the System.Collections.IEnumerable interface, then the collection type is this interface, the enumerator type is the interface System.Collections.IEnumerator, and the iteration type is object.
+   - Otherwise, an error is produced and no further steps are taken.

The above steps, if successful, unambiguously produce a collection type C, enumerator type E and iteration type T. A foreach statement of the form

```
foreach (V v in x) «embedded_statement»

is then expanded to:
{
    E e = ((C)x).GetEnumerator();
    try
    {
        while (e.MoveNext())
        {
            V v = (V)(T)e.Current;
            «embedded_statement»
        }
    }
    finally
```
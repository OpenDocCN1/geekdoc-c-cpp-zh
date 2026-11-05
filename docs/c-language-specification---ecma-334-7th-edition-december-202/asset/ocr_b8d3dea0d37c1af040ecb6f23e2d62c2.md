+   - The for statement is reachable and no for_condition is present.
+   - The for statement is reachable and a for_condition is present and does not have the constant value false.

The end point of a for statement is reachable if at least one of the following is true:

+   - The for statement contains a reachable break statement that exits the for statement.
+   - The for statement is reachable and a for_condition is present and does not have the constant value true.

# 13.9.5 The foreach statement

The foreach statement enumerates the elements of a collection, executing an embedded statement for each element of the collection.

```
foreach_statement
    : 'foreach' '(' ref_kind? local_variable_type identifier 'in'
      expression ')' embedded_statement
    ;
```

The local_variable_type and identifier of a foreach statement declare the iteration variable of the statement. If the var identifier is given as the local_variable_type, and no type named var is in scope, the iteration variable is said to be an implicitly typed iteration variable, and its type is taken to be the element type of the foreach statement, as specified below.

If the foreach_statement contains both or neither ref and readonly, the iteration variable denotes a variable that is treated as read-only. Otherwise, if foreach_statement contains ref without readonly, the iteration variable denotes a variable that shall be writable.

The iteration variable corresponds to a local variable with a scope that extends over the embedded statement. During execution of a foreach statement, the iteration variable represents the collection element for which an iteration is currently being performed. If the iteration variable denotes a read-only variable, a compile-time error occurs if the embedded statement attempts to modify it (via assignment or the ++ and -- operators) or pass it as a ref or out parameter.

In the following, for brevity, IEnumerable, IEnumerator, IEnumerable<T> and IEnumerator<T> refer to the corresponding types in the namespaces System.Collections and System.Collections.Generic.

The compile-time processing of a foreach statement first determines the collection type, enumerator type and iteration type of the expression. This determination proceeds as follows:

+   - If the type X of expression is an array type then there is an implicit reference conversion from X to the IEnumerable interface (since System.Array implements this interface). The collection type is the IEnumerable interface, the enumerator type is the IEnumerator interface and the iteration type is the element type of the array type X.
+   - If the type X of expression is dynamic then there is an implicit conversion from expression to the IEnumerable interface (§10.2.10). The collection type is the IEnumerable interface and the enumerator type is the IEnumerator interface. If the var identifier is given as the local_variable_type then the iteration type is dynamic, otherwise it is object.
+   - Otherwise, determine whether the type X has an appropriate GetEnumerator method:
+     - Perform member lookup on the type X with identifier GetEnumerator and no type arguments. If the member lookup does not produce a match, or it produces an ambiguity, or produces a match that is not a method group, check for an enumerable interface as described below. It is
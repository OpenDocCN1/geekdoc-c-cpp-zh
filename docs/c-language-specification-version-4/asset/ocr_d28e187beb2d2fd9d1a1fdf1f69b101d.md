+   - The for statement contains a reachable break statement that exits the for statement.
+   - The for statement is reachable and a for-condition is present and does not have the constant value true.

# 8.8.4 The foreach statement

The foreach statement enumerates the elements of a collection, executing an embedded statement for each element of the collection.

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

The type and identifier of a foreach statement declare the iteration variable of the statement. If the var identifier is given as the local-variable-type, and no type named var is in scope, the iteration variable is said to be an implicitly typed iteration variable, and its type is taken to be the element type of the foreach statement, as specified below. The iteration variable corresponds to a read-only local variable with a scope that extends over the embedded statement. During execution of a foreach statement, the iteration variable represents the collection element for which an iteration is currently being performed. A compile-time error occurs if the embedded statement attempts to modify the iteration variable (via assignment or the ++ and -- operators) or pass the iteration variable as a ref or out parameter.

The compile-time processing of a foreach statement first determines the collection type, enumerator type and element type of the expression. This determination proceeds as follows:

+   - If the type X of expression is an array type then there is an implicit reference conversion from X to the System.Collections.IEnumerable interface (since System.Array implements this interface). The collection type is the System.Collections.IEnumerable interface, the enumerator type is the System.Collections.IEnumerator interface and the element type is the element type of the array type X.
+   - If the type X of expression is dynamic then there is an implicit conversion from expression to the System.Collections.IEnumerable interface (§6.1.8). The collection type is the System.Collections.IEnumerable interface and the enumerator type is the System.Collections.IEnumerator interface. If the var identifier is given as the local-variable-type then the element type is dynamic, otherwise it is object.
+   - Otherwise, determine whether the type X has an appropriate GetEnumerator method:
+     - Perform member lookup on the type X with identifier GetEnumerator and no type arguments. If the member lookup does not produce a match, or it produces an ambiguity, or produces a match that is not a method group, check for an enumerable interface as described below. It is recommended that a warning be issued if member lookup produces anything except a method group or no match.
+     - Perform overload resolution using the resulting method group and an empty argument list. If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, check for an enumerable interface as described below. It is recommended that a warning be issued if overload resolution produces anything except an unambiguous public instance method or no applicable methods.
+     - If the return type E of the GetEnumerator method is not a class, struct or interface type, an error is produced and no further steps are taken.
+     - Member lookup is performed on E with the identifier Current and no type arguments. If the member lookup produces no match, the result is an error, or the result is anything except a public instance property that permits reading, an error is produced and no further steps are taken.
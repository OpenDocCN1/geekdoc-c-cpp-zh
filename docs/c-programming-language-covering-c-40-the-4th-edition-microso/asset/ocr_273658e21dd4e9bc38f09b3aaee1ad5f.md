If the yield return statement is within one or more try blocks, the associated finally blocks are not executed at this time.

+   - The state of the enumerator object is changed to suspended.
+   - The MoveNext method returns true to its caller, indicating that the iteration successfully advanced to the next value.

+   * When a yield break statement is encountered (§8.14):
+     - If the yield break statement is within one or more try blocks, the associated finally blocks are executed.
+     - The state of the enumerator object is changed to after.
+     - The MoveNext method returns false to its caller, indicating that the iteration is complete.

+   * When the end of the iterator body is encountered:
+     - The state of the enumerator object is changed to after.
+     - The MoveNext method returns false to its caller, indicating that the iteration is complete.

+   * When an exception is thrown and propagated out of the iterator block:
+     - Appropriate finally blocks in the iterator body will have been executed by the exception propagation.
+     - The state of the enumerator object is changed to after.
+     - The exception propagation continues to the caller of the MoveNext method.

# 10.14.4.2 The Current Property

An enumerator object's Current property is affected by yield return statements in the iterator block.

When an enumerator object is in the suspended state, the value of Current is the value set by the previous call to MoveNext. When an enumerator object is in the before, running, or after states, the result of accessing Current is unspecified.

For an iterator with a yield type other than object, the result of accessing Current through the enumerator object's IEnumerable implementation corresponds to accessing Current through the enumerator object's IEnumerator<T> implementation and casting the result to object.
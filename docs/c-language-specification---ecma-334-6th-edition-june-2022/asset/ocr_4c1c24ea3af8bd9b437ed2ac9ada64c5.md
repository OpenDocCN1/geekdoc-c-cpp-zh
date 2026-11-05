+   6. When a `System.ArithmeticException` (or a subclass thereof) is thrown when performing a decimal remainder operation (§11.9.4).
+   7. The impact of thread termination when a thread has no handler for an exception, and the thread is itself terminated (§12.10.6).
+   8. The impact of thread termination when no matching `catch` clause is found for an exception and the code that initially started that thread is reached. (§20.4).
+   9. The mappings between pointers and integers (§22.5.1).
+   10. The effect of applying the unary * operator to a `null` pointer (§22.6.2).
+   11. The behavior when pointer arithmetic overflows the domain of the pointer type (§22.6.6, §22.6.7).
+   12. The result of the `sizeof` operator for non-pre-defined value types (§22.6.9).
+   13. The behavior of the `fixed` statement if the array expression is `null` or if the array has zero elements (§22.7).
+   14. The behavior of the `fixed` statement if the string expression is `null` (§22.7).
+   15. The value returned when a stack allocation of size zero is made (§22.9).

# B.4 Unspecified behavior

+   1. The time at which the finalizer (if any) for an object is run, once that object has become eligible for finalization (§7.9).
+   2. The value of the result when converting out-of-range values from `float` or `double` values to an integral type in an `unchecked` context (§10.3.2).
+   3. The exact target object and target method of the delegate produced from an `anonymous_method_expression` contains (§10.7.2).
+   4. The layout of arrays, except in an unsafe context (§11.7.15.5).
+   5. Whether there is any way to execute the `block` of an anonymous function other than through evaluation and invocation of the `lambda_expression` or `anonymous_method-expression` (§11.16.3).
+   6. The exact timing of static field initialization (§14.5.6.2).
+   7. The result of invoking `MoveNext` when an `enumerator` object is running (§14.14.5.2).
+   8. The result of accessing `Current` when an enumerator object is in the before, running, or after states (§14.14.5.3).
+   9. The result of invoking `Dispose` when an `enumerator` object is in the running state (§14.14.5.4).
+   10. The attributes of a type declared in multiple parts are determined by combining, in an unspecified order, the attributes of each of its parts (§21.3).
+   11. The order in which `members` are packed into a struct (§22.6.9).
+   12. An exception occurs during `finalizer` execution, and that execution is not caught (§20.4).
+   13. If more than one member matches, which member is the implementation of I.M. (§17.6.5)
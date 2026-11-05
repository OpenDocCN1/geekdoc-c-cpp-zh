# 7.12.1 Boolean Conditional Logical Operators

When the operands of && or || are of type bool, or when the operands are of types that do not define an applicable operator & or operator | but do define implicit conversions to bool, the operation is processed as follows:

+   - The operation x && y is evaluated as x ? y : false. In other words, x is first evaluated and converted to type bool. Then, if x is true, y is evaluated and converted to type bool, and this becomes the result of the operation. Otherwise, the result of the operation is false.
+   - The operation x || y is evaluated as x ? true : y. In other words, x is first evaluated and converted to type bool. Then, if x is true, the result of the operation is true. Otherwise, y is evaluated and converted to type bool, and this becomes the result of the operation.

# 7.12.2 User-Defined Conditional Logical Operators

When the operands of && or || are of types that declare an applicable user-defined operator & or operator |, both of the following must be true, where T is the type in which the selected operator is declared:

+   - The return type and the type of each parameter of the selected operator must be T. In other words, the operator must compute the logical AND or the logical OR of two operands of type T, and must return a result of type T.
+   - T must contain declarations of operator true and operator false.

A binding-time error occurs if either of these requirements is not satisfied. Otherwise, the && or || operation is evaluated by combining the user-defined operator true or operator false with the selected user-defined operator:

+   - The operation x && y is evaluated as T.false(x) ? x : T.&(x, y), where T.false(x) is an invocation of the operator false declared in T, and T.&(x, y) is an invocation of the selected operator &. In other words, x is first evaluated and operator false is invoked on the result to determine if x is definitely false. Then, if x is definitely false, the result of the operation is the value previously computed for x. Otherwise, y is evaluated, and the selected operator & is invoked on the value previously computed for x and the value computed for y to produce the result of the operation.
+   - The operation x || y is evaluated as T.true(x) ? x : T.|(x, y), where T.true(x) is an invocation of the operator true declared in T, and T.|(x, y) is an invocation of the selected operator |. In other words, x is first evaluated and operator true is invoked on the result to determine if x is definitely true. Then, if x is definitely true, the result of the operation is the value previously computed for x. Otherwise, y is evaluated, and the selected operator | is invoked on the value previously computed for x and the value computed for y to produce the result of the operation.
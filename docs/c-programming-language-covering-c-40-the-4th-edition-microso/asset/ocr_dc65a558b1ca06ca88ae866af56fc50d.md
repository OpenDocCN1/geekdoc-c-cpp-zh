User-defined operator declarations cannot modify the syntax, precedence, or associativity of an operator. For example, the / operator is always a binary operator, always has the precedence level specified in §7.3.1, and is always left-associative.

While it is possible for a user-defined operator to perform any computation it pleases, implementations that produce results other than those that are intuitively expected are strongly discouraged. For example, an implementation of operator == should compare the two operands for equality and return an appropriate bool result.

> > **BILL WAGNER**  In addition to following this rule, you should limit the use of user-defined operators to those times when the operation will be obvious to the vast majority of the developers who use your code.

> > **ERIC LIPPERT**  The overloadable operators are all mathematical or logical in nature. If you are building a library of mathematical objects such as matrices, vectors, and so on, by all means create user-defined operators. But please resist the temptation to make “cute” operators, such as “a Customer plus an Order produces an Invoice.”

The descriptions of individual operators in §7.6 through §7.12 specify the predefined implementations of the operators and any additional rules that apply to each operator. The descriptions make use of the terms *unary operator overload resolution*, *binary operator overload resolution*, and *numeric promotion*, definitions of which are found in the following sections.

# 7.3.3 Unary Operator Overload Resolution

An operation of the form `op x` or `x op`, where *op* is an overloadable unary operator, and x is an expression of type X, is processed as follows:

+   - The set of candidate user-defined operators provided by X for the operation `operator op(x)` is determined using the rules of §7.3.5.
+   - If the set of candidate user-defined operators is not empty, then this becomes the set of candidate operators for the operation. Otherwise, the predefined unary operator `op` implementations, including their lifted forms, become the set of candidate operators for the operation. The predefined implementations of a given operator are specified in the description of the operator (§7.6 and §7.7).
+   - The overload resolution rules of §7.5.3 are applied to the set of candidate operators to select the best operator with respect to the argument list (x), and this operator becomes
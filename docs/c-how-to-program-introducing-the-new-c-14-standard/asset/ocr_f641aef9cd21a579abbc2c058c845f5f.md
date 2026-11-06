+   - *An operator’s associativity cannot be changed by overloading*—if an operator normally associates from left to right, then so do all of its overloaded versions.
+   - *An operator’s “arity”* (that is, the number of operands an operator takes) *cannot be changed*—overloaded unary operators remain unary operators; overloaded binary operators remain binary operators. C++’s only ternary operator, `?:`, cannot be overloaded. Operators `&`, `*`, `+` and `-` all have both unary and binary versions that can be separately overloaded.
+   - *Only existing operators can be overloaded*—you cannot create new ones.
+   - You *cannot* overload operators to change how an operator works on fundamental-type values. For example, you cannot make the `+` operator subtract two `int`s. Operator overloading works only with *objects of user-defined types* or with a mixture of an object of a user-defined type and an object of a fundamental type.
+   - Related operators, like `+` and `+=`, must be overloaded separately.
+   - When overloading `()`, `[]`, `->` or any of the assignment operators, the operator overloading function *must* be declared as a class member. For all other overloadable operators, the operator overloading functions can be member functions or non-member functions.

![](bbox=[0.12, 0.765, 0.196, 0.825])

# Software Engineering Observation

10.1
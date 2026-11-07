# 11.3.4 Rules and Restrictions on Operator Overloading

As you prepare to overload operators for your own classes, there are several rules and restrictions you should keep in mind:

+   - **An operator’s precedence cannot be changed by overloading.** Parentheses can be used to change the order of evaluation of overloaded operators in an expression.
+   - **An operator’s grouping (i.e., associativity) cannot be changed by overloading.** If an operator normally groups left-to-right, then so do its overloaded versions.
+   - **An operator’s “arity” (the number of operands an operator takes) cannot be changed by overloading.** Overloaded unary operators remain unary operators, and overloaded binary operators remain binary operators. The only ternary operator (`?:`) cannot be overloaded. Operators `&`, `*`, `+` and `-` each have unary and binary versions that can be overloaded separately.
+   - **Only existing operators can be overloaded.** You cannot create new ones.
+   - **You cannot overload operators to change how an operator works on only fundamental-type values.** For example, you cannot make `+` subtract two ints.
+   - Operator overloading works only with **objects of user-defined types** or with a **mixture of an object of a user-defined type and an object of a fundamental type.**
+   - **Related operators, like `+` and `+=`, generally must be overloaded separately.** In C++20, if you define `==` for your class, C++ provides `!=` for you—it simply returns the opposite of `==`.
+   - **When overloading `()`, `[]`, `->` or `=`, the operator overloading function must be declared as a class member.** You’ll see later that this is required when the left operand must be an object of your custom class type. Operator functions for all other overloadable operators may be member or non-member functions.

You should overload operators for class types to work as closely as possible to how they work with fundamental types. Avoid excessive or inconsistent use of operator overloading, as this can make a program cryptic and difficult to read.

# Checkpoint

+   1. **(Fill-in)** An overloaded operator function’s name is the keyword ______ followed by the operator’s symbol.  
+      **Answer:** operator.
+   2. **(True/False)** Operators overloaded as member functions must be declared static.  
+      **Answer:** False. Actually, they must be non-static because they are called on and operate on an object of the class.
+   3. **(Discussion)** The assignment operator (`=`) may be used with most classes to perform memberwise assignments of the data members. The default assignment operator assigns each data member from the “source” object (on the right) to the “target” object (on the left). When can such memberwise assignments be dangerous?  
+      **Answer:** This can be dangerous for classes that have pointer members.
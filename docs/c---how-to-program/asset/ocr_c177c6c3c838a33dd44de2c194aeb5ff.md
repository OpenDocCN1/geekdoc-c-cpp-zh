+   - One example of an overloaded operator built into C++ is operator `<<`, which is used both as the stream insertion operator and as the bitwise left-shift operator. Similarly, `>>` is also overloaded; it’s used both as the stream extraction operator and as the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library.
+   - C++ overloads `+` and `-` to perform differently, depending on their context in integer arithmetic, floating-point arithmetic and pointer arithmetic.
+   - The jobs performed by overloaded operators can also be performed by explicit function calls, but operator notation is often more natural.

# Section 18.2 Using the Overloaded Operators of Standard Library Class string

+   - Standard class `string` is defined in header `<string>` and belongs to namespace `std`.
+   - Class `string` provides many overloaded operators, including equality, relational, assignment, addition, addition assignment (for concatenation) and subscript operators.
+   - Class `string` provides member function `empty` (p. 719), which returns true if the string is empty; otherwise, it returns false.
+   - Standard class `string` member function `substr` (p. 719) obtains a substring of a length specified by the second argument, starting at the position specified by the first argument. When the second argument is not specified, `substr` returns the remainder of the string on which it’s called.
+   - Class `string`’s overloaded `[]` operator does not perform any bounds checking. Therefore, you must ensure that operations using standard class `string`’s overloaded `[]` operator do not accidentally manipulate elements outside the bounds of the string.
+   - Standard class `string` provides bounds checking with member function `at` (p. 720), which “throws an exception” if its argument is an invalid subscript. By default, this causes the program to terminate. If the subscript is valid, function `at` returns a reference or a const reference to the character at the specified location depending on the context.

# Section 18.3 Fundamentals of Operator Overloading

+   - An operator is overloaded by writing a non-static member-function definition or non-member function definition in which the function name is the keyword `operator` followed by the symbol for the operator being overloaded.
+   - When operators are overloaded as member functions, they must be non-static, because they must be called on an object of the class and operate on that object.
+   - To use an operator on class objects, you must define an overloaded operator function, with three exceptions—the assignment operator (`=`), the address operator (`&`), and the comma operator (`,`).
+   - You cannot change the precedence and associativity of an operator by overloading.
+   - You cannot change the “arity” of an operator (i.e., the number of operands an operator takes).
+   - You cannot create new operators—only existing operators can be overloaded.
+   - You cannot change the meaning of how an operator works on objects of fundamental types.
+   - Overloading an assignment operator and an addition operator for a class does not imply that `+=` is also overloaded. You must explicitly overload `operator +=` for that class.
+   - Overloaded `()`, `[]`, `->` and assignment operators must be declared as class members. For the other operators, the overloaded operator functions can be class members or non-member functions.

# Section 18.4 Overloading Binary Operators

+   - A binary operator can be overloaded as a non-static member function with one argument or as a non-member function with two arguments (one of those arguments must be either a class object or a reference to a class object).
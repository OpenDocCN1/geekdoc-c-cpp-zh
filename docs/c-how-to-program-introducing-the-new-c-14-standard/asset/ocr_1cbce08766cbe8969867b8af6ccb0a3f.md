# Section 10.2 Using the Overloaded Operators of Standard Library Class

# `string`

+   - Standard class `string` is defined in header `<string>` and belongs to namespace `std`.
+   - Class `string` provides many overloaded operators, including equality, relational, assignment, addition assignment (for concatenation) and subscript operators.
+   - The stream manipulator `boolalpha` (p. 452) sets an output stream to display condition values as the strings `"false"` and `"true"`, rather than `0` and `1`.
+   - Class `string` provides member function `empty` (p. 452), which returns `true` if the `string` is empty; otherwise, it returns `false`.
+   - A C++14 `string-object literal` (p. 452) is indicated by placing the letter `s` immediately following the closing `"` of a string literal.
+   - Standard class `string` member function `substr` (p. 452) obtains a substring of a length specified by the second argument, starting at the position specified by the first argument. When the second argument is not specified, `substr` returns the remainder of the `string` on which it’s called.
+   - Class `string`’s overloaded `[]` operator does not perform any bounds checking. Therefore, you must ensure that operations using standard class `string`’s overloaded `[]` operator do not
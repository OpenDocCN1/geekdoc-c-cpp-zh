# Testing Self-Assignment with the `string`  
Copy Assignment Operator

Line 62 uses class `string`’s overloaded copy assignment (`=`) operator to demonstrate that it handles *self-assignment* properly—we’ll see when we build class `Array` later in the chapter that self-assignment can be dangerous for objects that manage their own memory, and we’ll show how to deal with the issues. Line 63 confirms that `s4` still has the same value after the self-assignment.

# `string` Class `[]` Operator

Lines 66–67 use class `string`’s overloaded `[]` operator to create *values* that enable new characters to replace existing characters in `s1`. Lines 68–69 output the new value of `s1`. Class `string`’s *overloaded `[]` operator* does not perform any bounds checking. Therefore, *you must* ensure that operations using class `string`’s *overloaded `[]` operator* do not accidentally manipulate elements outside the bounds of the `string`. Class `string` does provide bounds checking in its member function `at`, which throws an exception if its argument is an *invalid subscript*. If the subscript is valid, function `at` returns the character at the specified location as a modifiable *lvalue* or a nonmodifiable *lvalue* (e.g., a `const` reference), depending on the context in which the call appears. For example:
+   - *Arithmetic* – Operators that perform arithmetic operations. If we use objects of different types, we must perform type conversions (this process is automatic for built-in types, although in many cases it can lead to value and precision loss and therefore should be avoided)
+   - *Comparisons* – Operators that compare objects for which the comparison operators are defined. The result is true or false, both of type bool
+   - *Logical* – Operations on objects of type bool. The result is true or false, both of type bool
+   - *Bitwise* – Operations on integer types, such as (unsigned) char, int, short, and long. These operations are performed in a bit-by-bit fashion

In C++, operators can be overloaded: we can change their meaning to serve specific purposes for objects (Section 4.4). In this fashion, the bitwise left-shift << operator has been overloaded and is commonly used with output streams, such as the std::cout object representing a screen. However, operator precedence and associativity rules cannot be changed.

Note that, unlike the address and pointer dereferencing operators, a reference is not an operator. It is always preceded by a type, and together they mean “reference-to-a-type.”

In C++20, the “spaceship operator” <=> has been added. Its official name is the *three-way comparison operator*, since basically it compares two objects, say x and y, and gives the answer: x<y, or x>y, or x==y. However, <=> does much more than return information about the strength of the relation between objects, and whether it allows only equality or ordering as well. For more on comparisons, see https://en.cppreference.com/w/cpp/language/operator_comparison.

# 3.20  Summary

# Things to Remember

+   - Learn all aspects of the operators. Check their precedence and associativity
+   - Try not to mix types in expressions – do not count on implicit type conversion
+   - Only the && (and), || (or), and , (comma) operators have a strict left-to-right evaluation order. Do not assume any specific order for other operators
+   - For built-in types, the second operand of && is not evaluated if the first one evaluates to false. Similarly, the second operand of || is not evaluated if the first one evaluates to true
+   - If possible, split expressions instead of using complicated ones. Use parentheses to enhance readability
+   - For indirect access to objects, prefer references versus pointers
+   - Split code into relatively small fragments – functions – each of which has a well-defined purpose, a meaningful name, and a short list of parameters. If more parameters are necessary, compose them into a class or a structure
+   - Embed data and its related functions in a class. Designate a compact set of functions as the class’s public interface. Put everything else in the private sections of the class. Be sure to initialize all data members (with initializer lists { } and/or constructors)
+   - Prefer using containers (e.g. vector, string, array) and algorithms (e.g. find, copy, accumulate, transform) from the Standard Library rather than writing your own
+   - Well analyze the problem before design. Make a design before implementation
# ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

+   - An attempt is made to use the value of a void expression, or an implicit or explicit conversion (except to void) is applied to a void expression (6.3.2.2).

+   - Conversion of a pointer to an integer type produces a value outside the range that can be represented (6.3.2.3).

+   - Conversion between two pointers produces a result that is incorrectly aligned (6.3.2.3).

+   - A pointer is used to call a function whose is not compatible with the referenced type (6.3.2.3).

+   - An unmatched ' or " character is encountered on a logical source line during tokenization. (6.4).

+   - A reserved keyword is used in translation phase 7 or 8 for some purpose other than a keyword (6.4.1).

+   - A universal character name in an identifier does not designate a character whose encoding falls into one of the specified ranges (6.4.2.1).

+   - The initial character of an identifier is a universal character designating a digit (6.4.2.1).

+   - Two identifiers differ only in nonsignificant characters (6.4.2.2).

+   - The identifier __func_ is explicitly declared (6.4.2.2).

+   - The program attempts to modify a string literal (6.4.5).

+   - The characters ', ' \ // or /* occur in the sequence between the < and > delimiters, or the characters '\', /, or /* in the sequence between the " delimiters, in a header name preprocessing token (6.4.7).

+   - A side effect on a scalar object is unintended relative to a different effect on the same scale object or a value computation using the value of the same scale object (6.5).

+   - An exceptional condition occurs during the evaluation of an expression (6.5).

+   - An object has its stored value other than an lvalue of an allowable type (6.5).

+   - For a call to a function without a function prototype in scope, the number of arguments does not equal the number of parameters (6.5.2.2).

+   - For a call to a function without a function prototype in scope where the function is defined with a function prototype, either the prototype ends with an ellipsis or the types of the arguments after promotion are not compatible with the types of the parameters (6.5.2.2).

# §J.2 Portability issues 559
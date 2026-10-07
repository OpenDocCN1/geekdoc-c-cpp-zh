are not both based on the same object (6.7.3.1).

+   A restrict-qualified pointer is assigned a value based on another restricted pointer whose block neither began execution before the block associated with this pointer, nor ended before the assignment (6.7.3.1).

+   A function with external linkage is declared with an inline function specifier, but is not also defined in the same translation unit (6.7.4).

+   A function declared with a _noreturn function specifier returns to its caller (6.7.4).

+   The definition of an object has an alignment specifier and another declaration of that object has a different alignment specifier (6.7.5).

+   Declarations of an object in different translation units have different alignment identifiers (6.7.5).

+   Two pointer types that are required to be compatible are not identically qualified, or are not pointers to compatible types (6.7.6.1).

+   The size expression in an array declaration is not a constant expression and evaluates at execution time to a nonpositive value (6.7.6.2).

+   In a context requiring two types to be compatible, they do not have compatible element types, or their sizes evaluate to unequal values (6.7.6.2).

+   A declaration of an array parameter includes the keyword static within the [ and the corresponding argument does not provide access to the first element of an array with at least the specified number of elements (6.7.6.3).

+   A storage-class specifier or type modifier qualifies the keyword void as a function type list (6.7.6.3).

+   In a context requiring two functions to be compatible, they do not have return types, or their parameters disagree in use of the ellipsis terminator and the number of parameters (default argument promotion, when there is no parameter type list or when one type is specified by a function definition with an identifier list) (6.7.6.3).

+   The value of an unnamed member of a structure or union is used (6.7.9).

+   The initializer for a scalar is neither a single expression nor a single expression enclosed in braces (6.7.9).

+   The initializer for a structure or union that has automatic storage duration is neither an initializer list nor a single expression that has compatible structure or union type (6.7.9).

+   The initializer for an aggregate or union, other than an array initialized by a string literal, is not a brace-enclosed list of initializers for its elements or members (6.7.9).
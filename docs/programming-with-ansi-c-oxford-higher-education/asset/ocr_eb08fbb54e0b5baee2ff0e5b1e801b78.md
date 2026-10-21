+   - Friends are useful for cases such as overloading insertion and extraction (>> and <<) operators and also when we want the first argument to the operators to be a built-in type.
+   - The case where we need dynamic memory allocation in constructor also needs assignment operator.
+   - The [] operator can be overloaded to provide array boundary checking and the () operator can be overloaded to make objects behave in the same way as functions.

+   - Function objects improve the readability of the code and make it possible to be inline.
+   - When we need to allocate and deallocate memory in a non-conventional way, we can overload new and delete.
+   - It is possible and sometimes useful to convert one type of object into another. It is also possible to convert a built-in type to object and vice versa. Constructors and operator functions help us in these conversions.

# KEYWORDS

Built-in type to user-defined  This refers to the conversion from built-in type to an object.

Extraction operator  The >> operator, which is used to read from the keyboard, is known as the extraction operator. It is also known as the input operator.

Function objects  Objects of the classes where the () operator is overloaded can be written with a () and can be treated similar to functions. Such objects that can be called like a function are known as function objects.

Insertion operator  The << operator, which is used to write to the console, is known as the insertion operator. It is also known as the output operator.

Forward definition  It is a prototype of the class that permits definition of the class name only at the beginning.

Object to built-in type conversion  This refers to the conversion from an object to a built-in type.

Operator function  Functions beginning with the keyword operator and having an operator specified as the next word in the function name are called operator functions. These functions replace the specified operator when the expression containing that operator is invoked.

Operator overloading  This is the process of giving an existing operator an additional meaning.

User-defined conversion  When we need to convert between different types, we can guide the compiler how to convert from one type to another by writing operator functions or constructors. These constructors and operator functions are known as user-defined conversions.

Wrapper class  This is a class that makes a C-like structure or a built-in type data represented as a class. For example, an Integer wrapper class represents a data type int as a class.

# EXERCISES

# Multiple Choice Questions

1. When overloading unary operators ________.
(a) no argument is passed explicitly
(b) one argument is to be passed explicitly
(c) no argument is passed implicitly
(d) no argument is passed explicitly only if overloaded as member functions

2. The advantage of operator overloading is ________.
(a) better readability
(b) easy usage
(c) easy coding
(d) Both (a) and (b)

3. The operators created using friend function can also be created by member functions.
(a) Always true
(b) Always false
(c) Partially true
(d) Never true

4. What will the following statement do?
Matrix operator *(int multiplier, Matrix tempMatrix);
(a) Overload the * (multiplication) operator for Matrix class.
(b) Compiler will generate an error.
(c) Overload the * (pointer) operator for Matrix class.
(d) Linker will generate an error.

5. All operators can be overloaded for ________.
(a) predefined types
(b) user-defined types
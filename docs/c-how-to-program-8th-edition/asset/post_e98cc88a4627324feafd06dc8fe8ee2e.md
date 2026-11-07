
- Standard class `string` member function `substr` (p. 455) obtains a substring of a length specified by the second argument, starting at the position specified by the first argument. When the second argument is not specified, `substr` returns the remainder of the string on which it’s called.
- Class `string`’s overloaded `[]` operator does not perform any bounds checking. Therefore, you must ensure that operations using standard class `string`’s overloaded `[]` operator do not accidentally manipulate elements outside the bounds of the string.
- Standard class `string` provides bounds checking with member function `at` (p. 456), which “throws an exception” if its argument is an invalid subscript. By default, this causes the program to terminate. If the subscript is valid, function `at` returns a reference or a `const` reference to the character at the specified location depending on the context.

## Section 11.3 Fundamentals of Operator Overloading

- An operator is overloaded by writing a non-static member-function definition or non-member function definition in which the function name is the keyword `operator` followed by the symbol for the operator being overloaded.
- When operators are overloaded as member functions, they must be non-static, because they must be called on an object of the class and operate on that object.
- To use an operator on class objects, that operator must be overloaded, with three exceptions—the assignment operator (`=`), the address operator (`&`) and the comma operator (`,`).
- You cannot change the precedence and associativity of an operator by overloading.
- You cannot change the “arity” of an operator (i.e., the number of operands an operator takes).
- You cannot create new operators—only existing operators can be overloaded.
- You cannot change the meaning of how an operator works on objects of fundamental types.
- Overloading an assignment operator and an addition operator for a class does not imply that the `+=` operator is also overloaded. Such behavior can be achieved only by explicitly overloading operator `+=` for that class.
- Overloaded `()`, `[]`, `->` and assignment operators must be declared as class members. For the other operators, the overloaded operator functions can be class members or non-member functions.

## Section 11.4 Overloading Binary Operators

- A binary operator can be overloaded as a non-static member function with one argument or as a non-member function with two arguments (one of those arguments must be either a class object or a reference to a class object).

## Section 11.5 Overloading the Binary Stream Insertion and Stream Extraction Operators

- The overloaded stream insertion operator (`<<`) is used in an expression in which the left operand has type `ostream &`. For this reason, it must be overloaded as a non-member function. To be a member function, operator `<<` would have to be a member of the ostream class, but this is not possible, since we are not allowed to modify C++ Standard Library classes. Similarly, the overloaded stream extraction operator (`>>`) must be a non-member function.
- Another reason to choose a non-member function to overload an operator is to enable the operator to be commutative.
- When used with `cin`, `setw` restricts the number of characters read to the number of characters specified by its argument.
- `istream` member function `ignore` discards the specified number of characters in the input stream (one character by default).
- Overloaded input and output operators are declared as friends if they need to access non-public class members directly for performance reasons.

## Section 11.6 Overloading Unary Operators

- A unary operator for a class can be overloaded as a non-static member function with no arguments or as a non-member function with one argument; that argument must be either an object of the class or a reference to an object of the class.
- Member functions that implement overloaded operators must be non-static so that they can access the non-static data in each object of the class.

## Section 11.7 Overloading the Unary Prefix and Postfix `++` and `--` Operators

- The prefix and postfix increment and decrement operators can all be overloaded.
- To overload the pre- and post-increment operators, each overloaded operator function must have a distinct signature. The prefix versions are overloaded like any other unary operator. The postfix increment operator’s unique signature is accomplished by providing a second argument, which must be of type int. This argument is not supplied in the client code. It’s used implicitly by the compiler to distinguish between the prefix and postfix versions of the increment operator. The same syntax is used to differentiate between the prefix and postfix decrement operator functions.

## Section 11.9 Dynamic Memory Management

- Dynamic memory management (p. 469) enables you to control the allocation and deallocation of memory in a program for any built-in or user-defined type.
- The free store (sometimes called the heap; p. 469) is a region of memory assigned to each program for storing objects dynamically allocated at execution time.
- The new operator (p. 469) allocates storage of the proper size for an object, runs the object’s constructor and returns a pointer of the correct type. The new operator can be used to dynamically allocate (p. 469) any fundamental type (such as int or double) or class type. If new is unable to find space in memory for the object, it indicates that an error occurred by “throwing” an “exception.” This usually causes the program to terminate immediately, unless the exception is handled.
- To destroy a dynamically allocated object and free its space, use the delete operator (p. 469).
- An array of objects can be allocated dynamically with new as in

```cpp
int *ptr = new int[100];
```

which allocates an array of 100 integers and assigns the starting location of the array to ptr. The preceding array of integers is deleted (p. 469) with the statement

```cpp
delete [] ptr;
```

## Section 11.10 Case Study: Array Class

- A copy constructor initializes a new object of a class by copying the members of an existing one. Classes that contain dynamically allocated memory typically provide a copy constructor, a destructor and an overloaded assignment operator.
- The implementation of member function `operator=` should test for self-assignment (p. 481), in which an object is being assigned to itself.
- The compiler calls the const version of `operator[]` when the subscript operator is used on a const object and calls the non-const version of the operator when it’s used on a non-const object.
- The array subscript operator (`[]`) can be used to select elements from other types of containers. Also, with overloading, the index values no longer need to be integers.

## Section 11.11 Operators as Member Functions vs. Non-Member Functions

- Operator functions can be member functions or non-member functions—non-member functions are often made friends for performance reasons. Member functions use this pointer implicitly to obtain one of their class object arguments (the left operand for binary operators). Arguments for both operands of a binary operator must be explicitly listed in a non-member function call.
- When an operator function is implemented as a member function, the leftmost (or only) operand must be an object (or a reference to an object) of the operator’s class.
- If the left operand must be an object of a different class or a fundamental type, this operator function must be implemented as a non-member function.
- A non-member operator function can be made a friend of a class if that function must access private or protected members of that class directly.

## Section 11.12 Converting between Types

- The compiler cannot know in advance how to convert among user-defined types, and between user-defined types and fundamental types, so you must specify how to do this. Such conversions can be performed with conversion constructors (p. 484)—single-argument constructors (p. 484) that turn objects of other types (including fundamental types) into objects of a particular class.
- Any single-argument constructor can be thought of as a conversion constructor.
- A conversion operator (p. 484) must be a non-static member function. Overloaded cast-operator functions (p. 484) can be defined for converting objects of user-defined types into fundamental types or into objects of other user-defined types.
- An overloaded cast operator function does not specify a return type—the return type is the type to which the object is being converted.
- When necessary, the compiler can call cast operators and conversion constructors implicitly to create temporary objects.

## Section 11.13 explicit Constructors

- C++ provides the keyword `explicit` (p. 486) to suppress implicit conversions via conversion constructors when such conversions should not be allowed. A constructor that’s declared explicit cannot be used in an implicit conversion.

## Section 11.14 Building a String Class

- Overloading the function call operator `()` (p. 487) is powerful, because functions can take an arbitrary number of parameters.

## Self-Review Exercises

- 11.1 Fill in the blanks in each of the following:
    - a) Suppose a and b are integer variables and we form the sum a + b. Now suppose c and d are floating-point variables and we form the sum c + d. The two + operators here are clearly being used for different purposes. This is an example of __________.
    - b) Keyword __________ introduces an overloaded-operator function definition.
    - c) To use operators on class objects, they must be overloaded, with the exception of operators __________, __________ and __________.
    - d) The __________, __________ and __________ of an operator cannot be changed by overloading the operator.
    - e) The operators that cannot be overloaded are __________, __________, __________ and __________.
    - f) The __________ operator reclaims memory previously allocated by new.

# Answers to Self-Review Exercises

23.1 a) False. Keywords typename and class in this context also allow for a type parameter of a fundamental type. b) True. c) False. Template parameter names among function templates need not be unique. d) True.

23.2 a) function-template specializations, class-template specializations. b) template, angle brackets (< and >). c) overload. d) parameterized. e) scope resolution.

# Exercises

23.3 (Operator Overloads in Templates) Write a simple function template for predicate function isEqualTo that compares its two arguments of the same type with the equality operator (==) and returns true if they are equal and false otherwise. Use this function template in a program that calls isEqualTo only with a variety of fundamental types. Now write a separate version of the program that calls isEqualTo with a user-defined class type, but does not overload the equality operator. What happens when you attempt to run this program? Now overload the equality operator (with the operator function) operator==. Now what happens when you attempt to run this program?

23.4 (Array Class Template) Reimplement class Array from Figs. 18.10–18.11 as a class template.

23.5 Distinguish between the terms “function template” and “function-template specialization.”

23.6 Explain which is more like a stencil—a class template or a class-template specialization?

23.7 What’s the relationship between function templates and overloading?

23.8 The compiler performs a matching process to determine which function-template specialization to call when a function is invoked. Under what circumstances does an attempt to make a match result in a compile error?

23.9 Why is it appropriate to refer to a class template as a parameterized type?

23.10 Explain why a C++ program would use the statement Array< Employee > workerList( 100 );

23.11 Review your answer to Exercise 23.10. Explain why a C++ program might use the statement Array< Employee > workerList;

23.12 Explain the use of the following notation in a C++ program: template< typename T > Array< T >::Array( int s )

23.13 Why might you use a nontype parameter with a class template for a container such as an array or stack?
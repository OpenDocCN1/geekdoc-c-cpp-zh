You saw that operator new throws bad_alloc exceptions when dynamic memory allocation fails. We also showed how dynamic memory allocation failures were handled in legacy C++ code with set_new_handler.

We introduced the C++ standard library exception class hierarchy and created a custom exception class that inherited from a C++ standard library exception class. You learned why it’s important to catch exceptions by reference to enable exception handlers to catch exception types related by inheritance and without slicing. We also introduced logging exceptions into a file that developers can analyze later for debugging purposes.

We discussed why some organizations disallow exception handling. You also saw that some libraries provide dual interfaces, so developers can choose whether to use versions of functions that throw exceptions or versions that set error codes.

The chapter concluded with an introduction to the contracts feature, originally adopted for C++20 but delayed to a future C++ version. We showed how to use contracts to test preconditions, postconditions and assertions at runtime. You learned that these test conditions that should always be true in correct code. You saw that if such conditions are false, contract violations occur and, by default, the code terminates immediately. This enables you to find errors faster, eliminate them during development and create more robust code.

Chapter 6 introduced the array and vector standard library classes. In Chapter 13, you’ll learn about many additional C++ standard library containers as well as iterators, which are used by standard library algorithms to walk through containers and manipulate their elements.

# Exercises

+   12.1 If no exceptions are thrown in a try block, where does control proceed after the try block completes execution?
+   
+   12.2 What happens if an exception is thrown outside a try block?
+   
+   12.3 Give a key advantage and a key disadvantage of using catch(...).
+   
+   12.4 What happens if no catch handler matches the type of a thrown object?
+   
+   12.5 What happens if several handlers match the type of the thrown object?
+   
+   12.6 Suppose a catch handler with a precise match to an exception object type is available. Under what circumstances might a different handler be executed for exception objects of that type?
+   
+   12.7 What does the statement throw; in a catch handler do?
+   
+   12.8 *(Exceptional Conditions)* List various exceptional conditions that have occurred throughout this textbook. List as many additional exceptional conditions as you can. For each of these exceptions, describe briefly how a program typically would handle the exception using the exception-handling techniques discussed in this chapter. Some typical exceptions are division by zero, arithmetic overflow, array subscript out of bounds, exhaustion of the free store, etc.
+   
+   12.9 *(catch Parameter)* Under what circumstances would you not provide a parameter name when defining the type of object that will be caught by a handler?
# Exception Handling, Stack Unwinding and Rethrowing Exceptions

You’ve seen exceptions get thrown (Section 6.15) and try…catch used to handle them (Section 9.7.11). This chapter reviews these exception-handling concepts in an example that demonstrates the flows of control

+   - when a program executes successfully and
+   - when an exception occurs.

We discuss use-cases for catching then rethrowing exceptions, and show how C++ handles an exception that is not caught in a particular scope. We introduce logging exceptions into a file or database that developers can review later for debugging purposes.

# When to Use Exceptions and Exception Safety Guarantees

Exceptions are not for all types of error handling, so we discuss when and when not to use them. We also introduce the exception safety guarantees you can provide in your code—from none at all to indicating with noexcept that your code does not throw exceptions.

# Exceptions in the Context of Constructors and Destructors

We discuss why exceptions are used to indicate errors during construction and why destructors should not throw exceptions. We also demonstrate how to use function try blocks to catch exceptions from a constructor’s member-initializer list.

# Handling Dynamic Memory Allocation Failures

By default, new throws exceptions when dynamic memory allocation fails. We demonstrate how to catch such bad_alloc exceptions. We also show how dynamic memory allocation failures were handled in legacy code before bad_alloc was added to C++.

# Standard Library Exception Hierarchy and Custom Exception Classes

We introduce the C++ standard library exception-handling class hierarchy. We create a custom exception class that inherits from one of the C++ standard library exception classes. You’ll see why it’s important to catch exceptions by reference to enable exception handlers to catch derived-class exception types.

# Exceptions Are Not Universally Used

Most C++ features have a zero-overhead principle in which you do not pay a price for a given feature unless you use it.⁸ Exceptions violate this principle—programs with exception handling have a larger memory footprint. Some organizations disallow exception handling for this and other reasons. We’ll discuss why some libraries provide dual interfaces, enabling developers to choose whether to use versions of functions that throw exceptions or versions that set error codes.

# Looking Ahead to Contracts

The chapter concludes with an introduction to contracts. This feature was originally targeted for C++20 but delayed to a future version. We’ll introduce preconditions, postconditions and assertions, which you’ll see are implemented as contracts tested at execution time. If such conditions fail, a contract violation occurs. By default, the code terminates

8. Herb Sutter, “De-fragmenting C++: Making Exceptions and RTTI More Affordable and Usable,” September 23, 2021. Accessed April 18, 2023. https://www.youtube.com/watch?v=ARPY83yNAwk.
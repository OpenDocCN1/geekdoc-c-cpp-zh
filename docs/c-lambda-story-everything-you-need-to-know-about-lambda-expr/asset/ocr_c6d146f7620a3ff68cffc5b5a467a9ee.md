# Appendix A - List of Techniques

Below you can find a list of techniques and patterns used throughout the book:

C++11 Chapter

+   - Calculating the number of invocations - An example of instrumenting a default functor to extend it with additional functionality.
- Deriving from lambda - A basic technique that allows you to wrap a closure type and extend it with additional functionality.
- IIFE - Immediately Invoked Function Expression - An efficient way to compute the value of a const variable which requires a complex initialisation without creating an extra function.
- Passing C++: a captureless lambda as a function pointer to C-style API functions.
- How to store lambdas in a container - we can do a little trick and store lambdas wrapped in std::function.

C++14 Chapter

+   - Replacing std::bind1, std::bind2nd - how to use Modern C++ and replace deprecated functionality.
- An optimisation thanks to capture with initialiser - An example of storing a temporary value used for the body of the lambda.
- Perfect forwarding with generic lambdas - How to use std::forward on a generic argument to pass it further down the stack.
- LIFING with lambdas - This allows a set of function overloads into a function template that takes a callable object. For example, when you call algorithms from the Standard Library.
- Recursive lambdas - Several tricks you can use to call the closure object inside its body.
- Variadic generic lambdas - How to use variadic arguments in a lambda expression.
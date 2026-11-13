# KEY TERMS

**Binary recursion** A simple unary recursive function calls itself once, whereas the binary recursive function calls itself twice. A factorial is a unary function, whereas Fibonacci is a binary recursion.

**Recurrence relation** A recurrence is a well-defined mathematical function written in terms of itself; it is a mathematical function defined recursively such as n! = n x (n – 1)!

**Depth of recursion** The number of times a function calls itself is known as the recursive depth of that function.

**Recursive functions** A function may call itself or call other functions and the called functions in turn may call the calling function. Such functions are called recursive functions.

**Direct and indirect recursion** When a recursive function calls itself directly, it is called direct recursion and when the function calls another function, which in turn calls the first function, it is called an indirect recursion.

**Stack overflow in recursion** Each time a function calls itself, it stores one or more variables on the stack. Since the stack holds a limited amount of memory, functions with a high recursive depth may crash because of the non-availability of memory. Such a situation is known as stack overflow.

**End condition** Recursive functions usually have and in fact should have a condition that would terminate the recursive calls. This terminating condition is called end condition. In the function factorial, when n = 1 the function returns 1. If this condition were not present, the function would keep calling itself with the values 3, 2, 1, 0, -1, -2, ... and so on till infinity. Such recursion is known as endless recursion.

**Tail recursion** A recursive function is said to be tail recursive if there are no pending operations to be performed on return from a recursive call; otherwise it is called a non-tail recursion. The factorial function is an example of non-tail recursion, whereas binary search is an example of tail recursion.

**Linear and tree recursion** Depending on the way the recursion grows, it is classified as linear or tree. A recursive function is said to be linearly recursive when no pending operation involves another recursive call. If there is another recursive call in the set of operations to be completed after the recursion is over, then it is called a tree recursion. Factorial is an example of linear recursion and Fibonacci is an example of tree recursion.

**Winding and unwinding of recursion** All recursive functions go through two distinct phases. The first phase, winding, occurs when the function is calling itself and pushing values onto the stack. The second phase, unwinding, occurs when the function is popping values from the stack, usually after the end condition.

# EXERCISES

# Multiple choice questions

+   1. Infinite recursion occurs when
+   (a) a base case is omitted
+   (b) a base case is never reached
+   (c) both (a) and (b)
+   (d) none of the above

+   2. Fibonacci function Fib(n) = Fib(n – 1) + Fib(n – 2) is an example of
+   (a) direct recursion
+   (b) tree recursion
+   (c) linear recursion
+   (d) both (a) and (b)
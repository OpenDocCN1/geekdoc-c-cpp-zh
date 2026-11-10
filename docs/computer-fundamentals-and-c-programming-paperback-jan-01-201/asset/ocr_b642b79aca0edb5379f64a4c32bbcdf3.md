| OUTPUT: |
|---|
| Call number: 1<br>Call number: 2<br>...<br>Call number: 523171<br>Call number: 523172<br>Segmentation fault |

Because the **static** variable count is defined and initialized just once, it can track the number of calls made to **main**. You are aware that function variables and parameters are saved in a separate region of memory called the stack. With every recursive call, the stack grows in size, and if this growth goes unchecked, the stack will eventually overflow. (See Inset entitled “How Functions Use the Stack” in Section 11.13.2.) In this program, after **main** has called itself 523,172 times, stack overflow occurs and terminates the program with a “segmentation fault.” This is not the way recursive functions are meant to be used.

A recursive function is typically used with one or more arguments that represent a subset of the problem. Each call contains a part of the solution which cannot be delivered to its caller until return of the call it has made to itself. The function typically includes a check for a *terminating condition* which at some point changes to stop further recursion. The calls then return in reverse sequence of their invocation, moving closer to the final solution with every return.

# 11.13.1  `factorial_rec.c`: Using a Recursive Function to Compute Factorial

Let’s consider the familiar recursive function that computes the factorial of a number. This is simply the product of all integers from 1 to the number. For instance, 6!, the factorial of 6, is 6 × 5 × 4 × 3 × 2 × 1 = 720. But 6! can also be expressed as a 6 × 5! in the same way as 5! is expressed as 5 × 4!. We can thus express the factorial of a number in this manner:

factorial(n) = n × factorial(n - 1)

Recursion is at work here because the factorial of a number can be described in terms of the factorial of another number. Our task now is to define a function that repeatedly calls itself until *n* = 1. This represents the terminating condition that stops further calls from being made. Program 11.11 uses this recursive technique.

Let’s now examine what the **factorial** function actually delivered in its six invocations. The final solution (the value of 6!), which is stored in the variable **result**, is determined by the return values of all recursive calls. This value can thus be made available only after these calls have returned. The first call made to **factorial(6)** returns the following value:

6 * factorial(5)

This call is kept pending because its return value depends on the return value of **factorial(5)**. A call to **factorial(5)** is made next, but this call can’t return either because it has to make a call to **factorial(4)**. In this way, all recursive calls are kept pending until a call is made to **factorial(1)**. The terminating condition (*n* == 1) evaluates to true here, so **factorial(1)** returns 1 without making any further calls. This enables **factorial(2)** to return, followed by **factorial(3)**, and so on until **factorial(6)** returns with the final answer.
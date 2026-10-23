In the above program, print(x+1) is increment type of recursive call. We are considering that the value of x passed initially is 1. With the help of this program, we are aiming to print the number from 10 to 1. To terminate the recursive call, base condition has been specified as 10. As soon as the value of x will reach 10, calling of the function will be terminated due to the base condition involved.

# 14.3 ACTIVATION RECORD

In the modern programming language, functions are widely used to accomplish a specific task. Functions invoked consist of local variables that are utilized in that specific call. These local variables are destroyed at the time of exit. However, in recursion, these local variables need to exist so that they can be utilized at substantive calls. In recursion, function returns only the base condition is met. Consequently, all these calls are stored in the stack, so that they should work in last in first out (LIFO) order. The portion of the stack used for function invocation is known as stack frame or activate record.

Block of information (“frames”) associated with each function call include:

+   - Parameters
+   - Local variables
+   - Return address after call.
+   - Location to put return value, when function exits.
+   - Control link to the caller’s activation record.
+   - Saved registers.
+   - Intermediate results.

# 14.4 TYPES OF RECURSION

To meet the diverse requirement, various types of recursive function exist and are used based on their requirement. Prevailing recursion types can be categorized into the following:

+   - Linear recursion
+   - Tail recursion
+   - Non tail recursion
+   - Binary recursion
+   - Mutual recursion
+   - Indirect recursion

# 14.4.1 Linear recursion

In the linear recursion, recursive function calls to itself and placed at the end of the function. It continues to execute the group of statements till the base condition is not reached. It is the simplest type of recursion and it is widely used.

Consider the case to determine the factorial of a given number ‘n’. It is already known to us
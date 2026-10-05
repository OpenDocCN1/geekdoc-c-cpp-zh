# 5.2. CALL BY VALUE AND CALL BY REFERENCE

A very interesting topic is 'call' by value and reference'.

So far, the reader would have come across so many function calls, some of them had no arguments, and some did have. Those which had arguments actually passed the values of the variables.

For example, consider the Program5.3, where the function factorial(num) passed the value of the actual parameter "num" to the dummy variable "num" in the function definition. What actually happens while passing the value of a variable to the function definition?

+   A copy of the value is given to the function definition.

+   The function definition deals with the copy of the original variable, and not with the original value.

+   Here is the knot. Any modification to the value inside the function definition won't affect the original.

+   The original will remain as such in the memory.

![](bbox=[0.183, 0.363, 0.816, 0.683])

Figure 5.1 Pass By Value

Program 5.6 would explain the concept more clearly.
The commas used in line 16 of *Fig. 6.3* to separate the arguments to function `maximum` are not comma operators as discussed in *Section 5.5*. The comma operator guarantees that its operands are evaluated left to right. The order of evaluation of a function’s arguments, however, is not specified by the C++ standard. Thus, different compilers can evaluate function arguments in different orders.

![](bbox=[0.124, 0.354, 0.19, 0.412])

# Portability Tip 6.2

Sometimes when a function’s arguments are expressions, such as those with calls to other functions, the order in which the compiler evaluates the arguments could affect the values of one or more of the arguments. If the evaluation order changes between compilers, the argument values passed to the function could vary, causing subtle logic errors.

![](bbox=[0.118, 0.698, 0.19, 0.752])

# Error-Prevention Tip 6.2

If you have doubts about the order of evaluation of a function’s arguments and whether the order would affect the values passed to the function, evaluate the arguments in separate assignment statements before the function call, assign the result of each
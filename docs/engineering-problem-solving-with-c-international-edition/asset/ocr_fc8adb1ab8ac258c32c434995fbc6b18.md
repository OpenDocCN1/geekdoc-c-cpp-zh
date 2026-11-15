Assume that a reference to this function is max(x_sum, y_sum) and that x_sum and y_sum are integers containing the values 3 and 8, respectively. Then, the following memory snapshot shows the transfer of values from the actual parameters to the formal parameters when the reference max(x_sum, y_sum) is made:

![](bbox=[0.38, 0.175, 0.76, 0.275])

The statements in the function will then return the value 8 as the value of the reference max(x_sum, y_sum).

Now suppose that a reference to the function max is made using float variables t_1 and t_2. If t_1 and t_2 contain the values 2.8 and 4.6, then the following transfer of parameters occurs when the reference max(t_1, t_2) is executed:

![](bbox=[0.38, 0.395, 0.76, 0.505])

The statements in the function will then return the value 4 to the statement containing the reference max(t_1, t_2). Obviously, the wrong value has been returned by the function. However, the problem is not in the function; the problem is that the function was referenced with the wrong types of actual parameters.

Additional errors can be introduced if the actual parameters are out of order. These errors may not be detected by the compiler, and they can be difficult to locate; therefore, be especially careful that the order of the formal parameters and the actual parameters match.

The function reference in the $inc example is a call-by-value reference, or a reference-by value. When a function reference is made, the value of the actual parameter is passed to the function and is used as the value of the corresponding formal parameter. In general, a C function cannot change the value of an actual parameter. Exceptions occur when the actual parameters are arrays (discussed in Chapter 5) or are pointers (discussed in Chapter 6); these exceptions generate a call-by-reference or a reference-by-address, which will be discussed in these later chapters.

![](bbox=[0.1, 0.6, 0.18, 0.65])

Call-by-value Reference-by value

Call-by-reference Reference-by-address

Scope

# Storage Class and Scope

In the sample programs presented thus far, we have declared variables within a main function and within programmer-defined functions. It is also valid to define a variable before the main function. Therefore, it is important to be able to determine the scope of a function or a variable, where scope refers to the portion of the program in which it is valid to reference the function or variable; scope is also sometimes defined in terms of the portion of the program in
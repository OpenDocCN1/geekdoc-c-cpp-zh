are assigned to their corresponding formal parameters, and the function begin executing. Another way to say it is that during a function call, the actual parameters are bound to their corresponding formal parameters.

The parameters used within a function definition are called formal parameters. Formal parameters behave as local variables within the function's body; as such, the name of a formal parameter will not conflict with any local variable or formal parameter names from other functions. This means as a function developer you may choose a parameter name that best represents the parameter's role in the function.

![](bbox=[0.225, 0.31, 0.27, 0.35])

If you are writing a function, you cannot predict the caller's actual parameters. You must be able to handle any value the caller sends. The compiler will ensure that the types of the caller's parameters are compatible with the declared types of your formal parameters.

To remember the difference between formal and actual parameters, remember this:

+   - A formal parameter is a parameter declared and used in a function's formal definition.
+   - An actual parameter is a parameter supplied by the caller when the caller actually uses (invokes or calls) the function.

When the call `value1 = prompt(1);` is executed in main, and the statement `std::cout << "Please enter integer #" << n << ": ";` within the body of prompt is executed, n will have the value 1. Similarly, when the call `value2 = prompt(2);` is executed in main, and the statement `std::cout << "Please enter integer #" << n << ": ";` within the body of prompt is executed, n will have the value 2. In the case of `value1 = prompt(1);` n within prompt is bound to 1, and in the case of `value2 = prompt(2);` n within prompt is bound to 2.
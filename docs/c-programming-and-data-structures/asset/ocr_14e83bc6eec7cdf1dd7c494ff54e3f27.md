# Just Remember

+   - It is a syntax error if the types in the declaration and function definition do not match.
+   - It is a syntax error if the number of actual parameters in the function call do not match the number in the declaration statement.
+   - It is a logic error if the parameters in the function call are placed in the wrong order.
+   - It is illegal to use the name of a formal argument as the name of a local variable.
+   - Using void as return type when the function is expected to return a value is an error.
+   - Trying to return a value when the function type is marked void is an error.
+   - Variables in the parameter list must be individually declared for their types. We cannot use multiple declarations (like we do with local or global variables).
+   - A return statement is required if the return type is anything other than void.
+   - If a function does not return any value, the return type must be declared void.
+   - If a function has no parameters, the parameter list must be declared void.
+   - Placing a semicolon at the end of header line is illegal.
+   - Forgetting the semicolon at the end of a prototype declaration is an error.
+   - Defining a function within the body of another function is not allowed.
+   - It is an error if the type of data returned does not match the return type of the function.
+   - It will most likely result in logic error if there is a mismatch in data types between the actual and formal arguments.
+   - Functions return integer value by default.
+   - A function without a return statement cannot return a value, when the parameters are passed by value.
+   - A function that returns a value can be used in expressions like any other C variable.
+   - When the value returned is assigned to a variable, the value will be converted to the type of the variable receiving it.
+   - Function cannot be the target of an assignment.

+   - A function with void return type cannot be used in the right-hand side of an assignment statement. It can be used only as a stand-alone statement.
+   - A function that returns a value cannot be used as a stand-alone statement.
+   - A return statement can occur anywhere within the body of a function.
+   - A function can have more than one return statement.
+   - A function definition may be placed either after or before the main function.
+   - Where more functions are used, they may be placed in any order.
+   - A global variable used in a function will retain its value for future use.
+   - A local variable defined inside a function is known only to that function. It is destroyed when the function is exited.
+   - A global variable is visible only from the point of its declaration to the end of the program.
+   - When a variable is redeclared within its scope either in a function or in a block, the original variable is not visible within the scope of the redeclared variable.
+   - A local variable declared static retains its value even after the function is exited.
+   - Static variables are initialized at compile time and therefore they are initialized only once.
+   - Use parameter passing by values as far as possible to avoid inadvertent changes to variables of calling function in the called function.
+   - Although not essential, include parameter names in the prototype declarations for documentation purposes.
+   - Avoid the use of names that hide names in outer scope.
+   - The use of functions gives C a modular-based programming approach.
+   - A function is typically characterised by its name, type and parameters.
+   - It is a good practice to name a function on the lines of its functionality.
+   - A function can return multiple values.
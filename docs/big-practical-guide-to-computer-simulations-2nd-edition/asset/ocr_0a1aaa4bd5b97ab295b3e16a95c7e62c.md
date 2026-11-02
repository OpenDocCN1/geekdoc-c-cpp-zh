```
Theta(-0.100000)=0.000000
Theta(-0.000000)=0.000000
Theta(0.100000)=1.000000
Theta(0.200000)=1.000000
```

To be able to use the function `step_function()` inside `main()`, the compiler has to "be aware" of it when it compiles the code for `main()`. There are four ways of achieving this:

+   (1) The full function definition of `step_function()` appears before `main()` in the source file. Then, when the compiler reaches the source code of `main()`, it will have processed already the part where `step_function()` is defined, hence the function is known to the compiler. In this way, `step_function()` is a global object, hence it can also be called from other functions, not only `main()`.
+   
+   (2) The full function definition comes after `main()` in the source file. To make the compiler aware of the existence of `step_function()` when it processes `main()`, one has to perform a declaration in advance, which is called *function prototype*. This means that in the source code before the definition of `main()`, the following line has to appear:
+   
+   ```
+   double step_function(double);
+   ```
+   
+   Note the closing semicolon at the end of the line. The function prototype carries all the information which has to be known outside the function: the function name, the types and order of the arguments, and the type of the return argument.
+   
+   All other functions which appear in the source code behind the function prototype of `step_function()` can use calls to `step_function()` in their code. Hence, if all function prototypes are listed at the beginning, each function is allowed to call each other function.
+   
+   (3) Very often, the source code is distributed over many source files. This usually happens if your simulation program is large and can be decomposed into several independent modules. There might be, for example, one module for setting up the simulation, another for auxiliary functions, some for the main simulation functions, and so forth. In this case, the second possibility has to be used, too. This means that for each
instructions are stored in the memory, which are executed by the CPU. At this stage, it is impossible for us to determine the exact memory addresses where each of our statements will be stored; hence, we have given line numbers to each of the statements in the program starting from 1000. Remember that these are line numbers we have given and not the real addresses of the statements in RAM; however, we will use these line numbers as if they are addresses to explain the concept of activation frames.

When a function is called, the activation frame for the function is created and pushed on the stack. When the function execution is completed, the activation frame for the function is popped out from the stack. When you run the program, operating system invokes the `main()` function to start the execution of program from `main()`. Since `main()` is the first function being invoked, its activation frame is pushed into stack as shown in Figure 7.32. There is no need to store return value in `main()` function’s activation frame because we have created it as a void type function.

There are two local variables `a` and `res` declared in `main()` which are present in the activation frame of `main()`. The function `main()` does not take any arguments (we have not use command line arguments in this program) and hence this section of activation frame is empty. C/C++ library code invokes the `main()` function and hence after `main()` completes the control returns to the library code and the operating system console. The activation frame also contains some temporary data needed by C/C++ runtime environment which is not shown in the sketches we have drawn. This information is not something we should worry about while learning programming, but this point should be mentioned for the sake of completeness.

The statement

```
```c
res = f1(a);
```
```

![](bbox=[0.261, 0.59, 0.649, 0.889])

**Figure 7.32:** Activation frame of `main()`
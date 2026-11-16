directs the preprocessor to augment our source code with the declarations of a collection of mathematical functions in the cmath library. The sqrt function is among them. Table 8.1 lists some of the other commonly used mathematical functions available in the cmath library. The compiler needs this augmented code so it can check to see if we are using the sqrt function properly.

The expression

```
sqrt(input)
```

is a function invocation, also known as a function call. A function provides a service to the code that uses it. Here, our main function is the caller¹ that uses the service provided by the sqrt function. We say main calls, or invokes, sqrt passing it the value of input. The expression sqrt(input) evaluates to the square root of the value of the variable input. Behind the scenes—inside the black box as it were—precompiled C code uses the value of the input variable to compute its square root. There is nothing special about this precompiled C code that constitutes the sqrt function; it was written by a programmer or team of programmers working for the library vendor using the same tools we have at our disposal. In Chapter 9 we will write our own functions, but for now we will enjoy the functions that others have provided for us.

When calling a function, a pair of parentheses follow the function's name. Information that the function requires to perform its task must appear within these parentheses. In the expression

```
sqrt(input)
```

input is the information the function needs to do its work. We say input is the argument, or parameter, passed to the function. We also can say “we are passing input to the sqrt function.”

While we might say “we are passing input to the sqrt function,” the program really is not giving the function access to main's input variable. The sqrt function itself cannot change the value of main's input variable, it simply uses the variable's value to perform the computation.

The following simple analogy may help explain how the communication works between main and sqrt. The main function has work to do, but instead of doing all the work itself, it delegates some of the work (in this case the hard part) to sqrt. When main needs to compute the square root of input, it writes down the value of its input variable on a piece of paper and hands it to sqrt. main then sits idly until sqrt finishes its work. The sqrt function accepts main's note and begins working on the task (computing the square root of the number on the note main gave it). When it is finished, sqrt does two things: sqrt hands back to main a different piece of paper with the answer, and sqrt throws away the piece of paper main originally passed to it. When main receives the note from sqrt it uses the information on the note and then discards the note. The main function then can continue with its other business.

The sqrt function thus has no access to main's original input variable; it has only a copy of input, as if “written on a piece of paper.” (Similarly, if the sqrt function uses any variables to do its work, main is oblivious to them and has no way to access them.) After sqrt is finished and returns to main its computed answer, sqrt discards its copy of input (by analogy, the function “throws away” the paper with the copy of input that main gave it). Thus, during a function call the parameter is a temporary, transitory value used only to communicate information to the function. The parameter lives only as long as the function is executing.

Figure 8.2 illustrates a program's execution involving simple function calls.

Figure 8.2 shows that a program's execution begins in its main function. Here main calls the sqrt function twice. A vertical bar represents the time that a function is active, or “alive.” A function's variables
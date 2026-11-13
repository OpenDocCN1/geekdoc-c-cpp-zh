# 1.10.1 Why are Functions Needed?

Let us analyse the reasons why segmenting a program into manageable chunks is an important aspect of programming.

+   - Dividing the program into separate well-defined functions facilitates each function to be written and tested separately. This simplifies the process of getting the total program to work.
+   - Understanding, coding, and testing multiple separate functions is easier than doing the same for one big function.
+   - If a big program has to be developed without using any function other than main(), then there will be countless lines in the main() function and maintaining that program will be a difficult task.
+   - All the libraries in C contain a set of functions that the programmers are free to use in their programs. These functions have been pre-written and pre-tested, so the programmers can use them without worrying about their code details. This speeds up program development, by allowing the programmer to concentrate only on the code that he has to write.
+   - Like C libraries, programmers can also write their own functions and use them from different points in the main program or any other program that needs its functionalities.
+   - When a big program is broken into comparatively smaller functions, then different programmers working on that project can divide the workload by writing different functions.

# 1.10.2 Using Functions

A function can be compared to a black box that takes in inputs, processes it, and then outputs the result. However, we may also have a function that does not take any inputs at all, or a function that does not return any value at all. While using functions, we will be using the following terminologies:

+   - A function f() uses another function g is known as the calling function, and g is known as the called function.
+   - The inputs that a function takes are known as arguments.
+   - When a called function returns some result back to the calling function, it is said to return that result.
+   - The calling function may or may not pass parameters to the called function. If the called function accepts arguments, the calling function will pass parameters, else not.
+   - Function declaration is a declaration statement that identifies a function name, a list of arguments that it accepts, and the type of data it returns.
+   - Function definition consists of a function header that identifies the function, followed by the body of the function containing the executable code for that function.

# Function Declaration

Before using a function, the compiler must know the number of parameters and the type of parameters that the function expects to receive and the data type of value that it will return to the calling program. Placing the function declaration statement prior to its use enables the compiler to make a check on the arguments used while calling that function.

The general format for declaring a function that accepts arguments and returns a value as result can be given as:

```
return_data_type function_name(data_type variable1, data_type variable2...);
```

Here, function_name is a valid name for the function. Naming a function follows the same rules that are followed while naming variables. A function should have a meaningful name that must specify the task that the function will perform.
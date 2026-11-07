the function invokes macro va_start (line 27) to initialize object ap for use by va_arg and va_end. The va_start macro receives:

+   - the object ap, and
+   - the identifier of the rightmost argument in the parameter list before the ellipsis (i in this example)—va_start uses this argument to determine where the variable-length argument list begins.

Next, the average function repeatedly adds the variable-length argument list’s arguments to the variable total1 (lines 30–32). The macro va_arg retrieves the next value to add to total1. The macro receives two arguments:

+   - the object ap, and
+   - the value type expected in the argument list—double in this case.

The macro returns the argument’s value. Line 34 invokes the macro va_end with the object ap as an argument to facilitate a normal return to the caller from average. Finally, line 35 calculates the average and returns it to main.

You might wonder how functions with variable-length argument lists like printf and scanf know what type to use in each va_arg macro call. The answer is that, as the program executes, they scan the format conversion specifiers in the format control string to determine the type of the next argument to process.

# Self Check

1 (Fill-In) The function prototype for printf is

```
int printf(const char *format, ...);
```

The ellipsis (...) in the prototype indicates that the function receives ______. Answer: a variable number of arguments of any type.

2 (Multiple Choice) Which macro corresponds to the description: “To access the arguments in a variable-length argument list, an object of this type must be defined.” a) va_start b) va_end c) va_list d) va_arg Answer: c.

# 15.3 Using Command-Line Arguments

Command-line arguments are commonly used to pass options and filenames to a program. The main function may receive arguments from a command line if the function’s parameter list contains the parameters int argc and char *argv[]:

+   - The argc parameter receives the number of command-line arguments that the user has entered.
+   - The argv parameter is an array of strings containing the command-line arguments.
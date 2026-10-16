+   2. Control then transfers from the line containing the function call (in main()) to the first statement of celsiusToFahrenheit(), which begins execution using the value of its parameter.
+   3. When a return statement (or the final statement of the function) is executed, control transfers back to the caller (i.e., the main function), where execution resumes.

+   - Local variables, constants, and parameters of a function are defined only while that function is executing. They can be accessed only within the function—not from outside.
+   - The keyword void is used to specify the return type of a function that does not return any values. Such functions are called with statements of the form function_Name(argument_list);

The ability to define functions is a powerful tool in programming. If some problem requires that an operation not provided in C++ be applied to some item in that problem, we can simply

+   1. define a function to perform that operation, and
+   2. apply that function to the item

as we did with the temperature-conversion operation celsiusToFahrenheit(). Also, as we will see in the next section, such functions can then be stored in a library, from which they can be retrieved when needed.

# 6.4 AN INTRODUCTION TO LIBRARIES

We have seen that if a problem requires some new operation, we can define a function to perform it and then call it just as if were provided in C++. In essence, we are extending C++’s collection of operations. However, although such programmer-defined functions provide a significant improvement over using only expressions, they do not in themselves make it easy to reuse our work. For example, to use the celsiusToFahrenheit() function from Example 6.2 in another program, we would have to copy its prototype and its definition from that program and insert them at the appropriate places in the new program. We might use the copy-and-paste capabilities of a text editor or word processor to do this or we might simply make a copy of the program in Example 6.2, delete everything between the prototype and definition of celsiusToFahrenheit(), and then write the new program between this prototype and definition.

To facilitate reusability, C++’s parent language C provides several standard libraries, which are simply files containing items that can be shared by different programs and by other libraries. For example, we have used the function pow() from C’s standard library cmath to compute powers, and in the preceding chapter we used the assert() function from C’s cassert library to check whether certain conditions are true. To use one of these functions, for example, pow(), we need only include the library in the program:

```
#include <cmath>
```
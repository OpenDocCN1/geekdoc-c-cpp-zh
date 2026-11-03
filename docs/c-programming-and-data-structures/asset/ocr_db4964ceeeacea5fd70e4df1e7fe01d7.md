The variables declared inside a function are known as local variables and therefore their values are local to the function and cannot be accessed by any other function. We shall discuss more about this later in the chapter.

The function value calculates the final amount for a given period and prints the results as before. Control is transferred back on reaching the closing brace of the function. Note that the function does not return any value.

The function println is called twice. The first call passes the character 'Z', while the second passes the character 'C' to the function. These are assigned to the formal argument ch for printing lines (see the output).

> **Variable Number of Arguments**
> Some functions have a variable number of arguments and data types which cannot be known at compile time. The printf and scanf functions are typical examples. The ANSI standard proposes new symbol called the ellipsis to handle such functions. The ellipsis consists of three periods (...) and used as shown below:
> double area(float d,...)
> Both the function declaration and definition should use ellipsis to indicate that the arguments are arbitrary both in number and type.

# 5.12 ARGUMENTS WITH RETURN VALUES

The function value in Fig. 5.7 receives data from the calling function through arguments, but does not send back any value. Rather, it displays the results of calculations at the terminal. However, we may not always wish to have the result of a function displayed. We may use it in the calling function for further processing. Moreover, to assure a high degree of portability between programs, a function should generally be coded without involving any I/O operations. For example, different programs may require different output formats for display of results. These shortcomings can be overcome by handing over the result of a function to its calling function where the returned value can be used as required by the program.

A self-contained and independent function should behave like a 'black box' that receives a predefined form of input and outputs a desired value. Such functions will have two-way data communication as shown in Fig. 5.8

We shall modify the program in Fig. 5.7 to illustrate the use of two-way data communication between the calling and the called functions.

![](bbox=[0.55, 0.65, 0.88, 0.84])

Fig. 5.8 Two-way data communication between functions

> **EXAMPLE 5.3** In the program presented in Fig. 5.7 modify the function value, to return the final amount calculated to the main, which will display the required output at the terminal. Also extend the versatility of the function println by having it to take the length of the line as an argument.

The modified program with the proposed changes is presented in Fig. 5.9. One major change is the movement of the printf statement from value to main.

```
Program
void println (char ch, int len);
value (float, float, int);
```
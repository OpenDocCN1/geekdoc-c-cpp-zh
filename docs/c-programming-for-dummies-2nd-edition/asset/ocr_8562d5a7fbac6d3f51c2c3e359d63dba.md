The function returns no values and requires no arguments, so its data type is void and void appears in the parentheses.

Line 13 accesses the function. The function is called as its own statement. It doesn't require any arguments or return any values, and it appears on a line by itself, as shown in the listing. When the program encounters that statement, program execution jumps up to the function. The function's statements are executed, and then control returns to the next line in the code after the function was called.

Lines 22 through 25 define the function itself. The function's data type, void, is specified on Line 22, followed by the function name, and then the parentheses with void specified because arguments aren't passed to the function.

The function's sole statement is held between curly brackets. The prompt() function uses the printf() function to output a prompt, which makes it seem like the function isn't necessary, but many examples of one-line functions can be found in lots of programs.

**Exercise 10-2:** Modify the source code from Listing 10-1 to add the busy() function, which contains the while loop now in the main() function. (Copy Lines 7 through 16 into the new function.) Have the main() function call the busy() function.

![](bbox=[0.2, 0.65, 0.3, 0.78])

+   - C has no limit on what you can do in a function. Any statements you can stuff into the main() function can go into any function. Indeed, main() is simply another function in your program, albeit the program's chief function.
+   - The main() function has arguments, so don't be tempted to edit its empty parentheses and stick the word void in there. In other words, this construct is wrong:
+   - Other programming languages may refer to a function as a subroutine or procedure.

```
```c
int main(void)
```
```

The main() function in C has two arguments. It's possible to avoid listing them when you're not going to use them, by keeping parentheses empty. Chapter 15 discusses using the main() function's arguments.

![](bbox=[0.2, 0.85, 0.3, 0.95])

# Prototyping (or not)

What happens when you don't prototype? As with anything in programming, the compiler or linker lets you know with a warning or error message when you
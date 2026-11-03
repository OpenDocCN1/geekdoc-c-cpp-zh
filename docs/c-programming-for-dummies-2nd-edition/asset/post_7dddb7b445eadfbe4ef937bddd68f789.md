
## IN THIS CHAPTER
- Creating a function
- Avoiding the prototype
- Working with variables in a function
- Passing arguments to a function
- Returning values from a function
- Using return to leave a function

## Chapter 10
### Fun with Functions
When it comes to getting work done, it's a program's functions that do the heavy lifting. The C language comes with libraries full of functions, which help bolster the basics of the language, the keywords, the operators, and so on. When these C library functions fall short, you concoct your own functions.

### Anatomy of a Function
The tools that are needed to craft your own functions are brief. After deciding the function's purpose, you give it a unique name, toss in some parentheses and curly brackets, and you're pretty much done. Of course, the reality is a bit more involved.

### Constructing a function
All functions are dubbed with a name, which must be unique; no two functions can have the same name, nor can a function have the same name as a keyword or variable used in the code.

The name is followed by parentheses, which are then followed by a set of curly brackets. So, in its simplest construction, a function looks like this:

```
type function() { }
```

In the preceding example, type defines the function's data type, which is related to the value returned from the function. Options for type include all the standard C data types — char, int, float, double — and also void for functions that don't return anything.

function is the function's name. It's followed by a pair of parentheses, which can, optionally, contain values passed to the function. These values are called arguments. Not every function features arguments.

Central to a function are its statements, enclosed in curly brackets. These statements are what make the function do its thing.

Functions that return a value must use the return keyword. The return statement either ends the function directly or passes a value back to the statement that called the function. For example:

```
return;
```

This statement ends a function and doesn't pass on a value. Any statements in the function after return are ignored.

```
return(something);
```

This statement passes the value of the something variable back to the statement that called the function. The something must be of the same data type as the function, an int, a float, and so on.

Functions that don't return values are declared of the void type. Those functions end with the last statement held in the curly brackets; a return statement isn't required.

One more important thing! Functions must be prototyped in your code. This is so that the compiler understands the function and sees to it that you use it properly. The prototype describes the value returned and any arguments the function requires. The prototype must appear in your source code before any statement calls the function. Listing 10-1 shows a prototype example at Line 3.

![](img/dcc0cd79d4a45cfce24fa49d85442884_149_0.png)

### LISTING 10-1: Basic Function; No Return
```
#include <stdio.h>

void prompt();    /* function prototype */

int main()
{
    int loop;
    char input[32];

    loop=0;
    while(loop<5)
    {
        prompt();
        fgets(input,32,stdin);
        loop=loop+1;
    }
    return(0);
}

/* Display prompt */

void prompt(void)
{
    printf("C:\\DOS> ");
}
```

### Exercise 10-1: Use the source code from Listing 10-1 to create a new program. Build and run.
The program displays a prompt five times, allowing you to type various commands. Of course, nothing happens when you type commands, though you can program those actions later, if you like. Here’s how this program works in regard to creating a function:

Line 3 lists the function prototype. It’s essentially a copy of the first line of the function (from Line 22), but ending with a semicolon. It can also be written like this:

```
void prompt(void);
```

The function returns no values and requires no arguments, so its data type is void and void appears in the parentheses.

Line 13 accesses the function. The function is called as its own statement. It doesn't require any arguments or return any values, and it appears on a line by itself, as shown in the listing. When the program encounters that statement, program execution jumps up to the function. The function's statements are executed, and then control returns to the next line in the code after the function was called.

Lines 22 through 25 define the function itself. The function's data type, void, is specified on Line 22, followed by the function name, and then the parentheses with void specified because arguments aren't passed to the function.

The function's sole statement is held between curly brackets. The prompt() function uses the printf() function to output a prompt, which makes it seem like the function isn't necessary, but many examples of one-line functions can be found in lots of programs.

**Exercise 10-2:** Modify the source code from Listing 10-1 to add the busy() function, which contains the while loop now in the main() function. (Copy Lines 7 through 16 into the new function.) Have the main() function call the busy() function.

![](img/dcc0cd79d4a45cfce24fa49d85442884_151_0.png)

- C has no limit on what you can do in a function. Any statements you can stuff into the main() function can go into any function. Indeed, main() is simply another function in your program, albeit the program's chief function.
- The main() function has arguments, so don't be tempted to edit its empty parentheses and stick the word void in there. In other words, this construct is wrong:
- Other programming languages may refer to a function as a subroutine or procedure.

```
int main(void)
```

The main() function in C has two arguments. It's possible to avoid listing them when you're not going to use them, by keeping parentheses empty. Chapter 15 discusses using the main() function's arguments.

![](img/dcc0cd79d4a45cfce24fa49d85442884_151_1.png)

### Prototyping (or not)
What happens when you don't prototype? As with anything in programming, the compiler or linker lets you know with a warning or error message when you goof — or the program just doesn't run properly. It's not the end of the world — no, not like programming a military robot or designing genetic code for a new species of Venus flytrap.

### Exercise 10-3: Modify the source code from Exercise 10-1. Comment out the prototype from Line 3. Build the result.
Build errors are wonderful things, delightfully accurate yet entirely cryptic. Here are the warning and error messages generated by my compiler and linker, showing only the relevant parts of each message:

```
13 warning: implicit declaration of function 'prompt'
22 error: conflicting types for 'prompt'
```

The first warning occurs at Line 13 in my source code file, where the prompt() function is used inside the main() function. The compiler is telling you that a function is called without a prototype. As the message says, you're implicitly declaring a function. That's a no-no, but not a full-on error; the compiler generates object code, praying that the linker can resolve the unknown function.

The error occurs where the prompt() function dwells in the program. In my source code, it's at Line 22. The prompt() function's data type is incorrect because the linker assumes integer as an unknown function's data type.

You may draw the conclusion that prototyping is an absolute necessity in your C code. This assumption isn't entirely true. You can avoid prototyping by reordering the functions in your source code. As long as a function is listed before it's used, you don't need a prototype.

### Exercise 10-4: Edit your source code from Exercise 10-3. Remove the function prototype that was commented out at Line 3. Cut-and-paste (move) the prompt() function from the bottom of the source code listing to the top, above the main() function. Save, build, and run.
Listing 10-2 shows what I conjured up as a solution for Exercise 10-4.

### LISTING 10-2: Avoiding the Function Prototype
```
#include <stdio.h>

/* display prompt */

void prompt(void)
```
(continued)

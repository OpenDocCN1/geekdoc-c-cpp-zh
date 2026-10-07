# Understanding Functions

To understand functions, you need to understand what functions are and how they are used.

# A Function Defined

First the definition: A function is a named, independent section of C code that performs a specific task and optionally returns a value to the calling program. Now take a look at the parts of this definition:

+   - Function is named. Each function has a unique name. By using that name in another part of the program, you can execute the statements contained in the function. This is known as calling the function. A function can be called from another function.

+   - Function is independent. A function can perform its task without interference from or with other parts of the program.

+   - Function performs a specific task. This is the easy part of the definition. A task is a discrete job that your program must perform as part of its overall operation, such as sending a line of text to a printer, sorting an array into numerical order, or calculating a cube.

+   - Function can return a value to the calling program. When your program calls a function, the statements it contains are executed. If you want them to, these statements can pass information back to the calling program.

That's all there is to define a function. Keep the previous definition in mind as you look at the next section.

# A Function Illustrated

Listing 5.1 contains a user-defined function.

Input
LISTING 5.1 cube.c: A Program That Uses a Function to Calculate the Cube of a Number

```
1: // Demonstrates a simple function
2: #include <stdio.h>
3: 
4: long cube(long x);
5: 
6: long input, answer;
7: 
8: int main(void )
9: {
```
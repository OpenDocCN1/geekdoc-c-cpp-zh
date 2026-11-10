# **HOW IT WORKS: How Does scanf Work?**

When you key in, say, 75, in response to the previous **scanf** call, **scanf** doesn't read the input as the integer 75 but as two separate characters '7' and '5'. **scanf** knows (because %d) that you meant to specify an integer, so it first converts '7' and '5' to the binary equivalent of the number 75. Because of a special property of C functions, **scanf** has to peek into the memory location of a variable, say, **your_number**, to place this converted value there. The & in **&your_number** provides the memory address of **your_number**. **printf** doesn't need the & because it evaluates a variable and doesn't assign one.

The first **printf** prompts for an integer, and the one you key in is converted to an integer and saved by **scanf** in the variable **your_number**. The inset (*How It Works*) explains the necessity of conversion and the role of the & operator.

**Caution:** It is a common semantic error to omit the & in the variable list of **scanf**. The compiler will generate a warning but will still proceed with the creation of the executable. The program, however, won't work.

**Takeaway:** It is impossible to assign a variable using a function that takes a variable name as a function argument. You have to use the & prefix.

# ## 4.9 third_prog.c: AN INTERACTIVE PROGRAM FEATURING REPETITION

We have considered sequence (Program 4.1) and decision making (Program 4.2). This program (Program 4.3) features repetition, the third tenet of structured programming. Using two invocations of **scanf**, the program accepts a character and a number, and then runs a **while** statement (a loop) to print that character as many times as the number. To keep the program short and simple, validation of user input has been avoided.

This time we see three variable assignments in one line. This is legal because C requires statements to be terminated with a semicolon and doesn't care whether they are on separate lines or not. The variable counter is initialized to 0 but not the other variables which are assigned by **scanf**.

Program execution pauses twice—at the two **scanf** statements. The first **scanf** saves the character entered in the variable **letter**. The next **scanf** converts and saves the input in the variable **your_number**. Expectedly, the format specifiers (%c and %d) are different for the two calls. You need to remind yourself that variables in **scanf** must have the & prefix.

The **while** loop repeats the statements in its body. Like **if**, **while** uses a *control expression* to determine how often these statements are repeated (if at all). Each loop *iteration* prints one user-input character before incrementing the value of counter. Control then reverts to the top of the loop where the condition, i.e., control expression (counter < your_number) is rechecked. If the condition is met (true), the loop body is repeated, otherwise the loop is terminated. Because **printf** doesn't use a \n here, the character is printed multiple times but in one line.
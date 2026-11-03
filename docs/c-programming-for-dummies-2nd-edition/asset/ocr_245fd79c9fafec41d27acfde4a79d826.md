> Main isn't a keyword; it's a function. It's the required first function in all C language source code.
> 
> Unlike other functions, main() doesn't need to be prototyped. It does, however, use specific arguments, which is a topic covered in Chapter 15.

# Returning something to the operating system

Proper protocol requires that when a program quits, it provides a value to the operating system. Call it a token of respect. That value is an integer (a whole number), usually zero, but sometimes other values are used, depending on what the program does and what the operating system expects.

Continue with Exercise 3-1: Update the source code for ex0301.c to reflect the changes shown in Listing 3-7.

# LISTING 3-7: Adding the return Statement

```
int main()
{
    return(1);
}
```

First, the main() function is declared to be an integer function. The int keyword tells the compiler that the function returns, or generates, an integer value.

The return statement sends the value 1 back to the operating system, effectively ending the main() function and, therefore, the program.

Continue with Exercise 3-1: Save, build, and run the project.

The results are similar to the previous run, but if you're using the Code::Blocks IDE, you see the return value of 1 specified in the summary text:

```
Process returned 1 (0x1)
```

If you like, edit the code again and change the return value to something else — say, 5. That value appears in the Code::Blocks output when you run the project.
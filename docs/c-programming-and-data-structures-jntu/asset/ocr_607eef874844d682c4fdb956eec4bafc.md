able statements and therefore anything between /* and */ is ignored by the compiler. In general, a comment can be inserted anywhere blank spaces can occur—at the beginning, middle, or end of a line, but never in the middle of a word.

Because comments do not affect the execution speed and the size of a program, we should use them liberally in our porgrams. They help the programmers and other users in understanding the various functions and operations of a program and serve as an aid to debugging and testing. We shall see the use of comment lines more in the examples that follow.

Let us now look at the printf() function, the only executable statement of the program.

```
printf("I see, I remember");
```

printf is a predefined, standard C function for printing output. Predefined means that it is a function that has already been written and compiled, and linked together with our program at the time of linking. The concepts of compilation and linking are explained later in this chapter (Section 2.4). The printf function causes everything between the starting and the ending quotation marks to be printed out. In this case, the output will be:

I see, I remember

Note that the print line ends with a semicolon. Every statement in C should end with a semicolon (;) mark.

Suppose we want to print the above quotation in two lines as

I see,
I remember !

This can be achieved by adding another printf function as shown below:

```
printf("I see, \n");
printf("I remember !");
```

The information contained between the parentheses is called the argument of the function. The argument of the first printf function is "I see,\n" and the second is "I remember !". These arguments are simply strings of characters to be printed out.
To end execution of the program and return control to the operating system, we use a return 0; statement:

```
/* Exit program. */
return 0;
```

This statement returns a value of 0 to the operating system. A value of zero indicates a successful end of execution.

The body of the main function then ends with the right brace on a line by itself and another comment line to delineate the end of the main function:

```
}
/*--------------------------------------*/
```

![](bbox=[0.145, 0.282, 0.205, 0.332])

Note that we have also included blank lines (also called white space) in the program to separate different components. These blank lines make a program more readable and easier to modify. The declarations and statements within the main function were indented to show the structure of the program. This spacing provides a consistent style, and makes our programs easier to read.

Now that we have closely examined the C program from Chapter 1, we can compare its structure to the general form of a C program:

```
preprocessing directives
int main(void)
{
 declarations;
 statements;
}
```

This structure is evident in the programs developed in this chapter and in following chapters.

# MODIFY!

+   1. Create a file containing the sample program discussed in this section. Use either an editor that is part of your C compiler or use a word processor.* Then compile and execute the program. You should get this output: The distance between the two points is 3.61
+   2. Change the values given to the two points to the coordinates (–1, 6) and (2, 4). Run the program with these new values. Did the distance change? Explain.
+   3. Change the values given to the two points to the coordinates (1, 0) and (5, 7). Check the program’s answer with your calculator.
+   4. Change the values given to the two points to the coordinates (2, 4) and (2, 4). Does the program given the correct answer?

*If you use a word processor to generate the file, make sure you save it as a text file.

### 14.2.2 Redirecting Input with |

The second method of redirecting input is piping. A pipe (|) causes the output of one program to be redirected as the input to another. Suppose program random outputs a series of random integers; the output of random can be "piped" directly to program sum using the command line

```
$ random | sum
```

This causes the sum of the integers produced by random to be calculated. Piping is performed identically in Linux/UNIX, Windows and OS X.

### 14.2.3 Redirecting Output

The standard output stream can be redirected to a file by using the redirect output symbol (>). For example, to redirect the output of program random to file out, use

```
$ random > out
```

Finally, program output can be appended to the end of an existing file by using the append output symbol (>>). For example, to append the output from program random to file out created in the preceding command line, use the command line

```
$ random >> out
```

## 14.3 Variable-Length Argument Lists

It's possible to create functions that receive an *unspecified* number of arguments. Most programs in the text have used the standard library function printf, which, as you know, takes a variable number of arguments. As a minimum, printf must receive a string as its first argument, but printf can receive any number of additional arguments. The function prototype for printf is

```c
int printf(const char *format, ...);
```

The ellipsis (...) in the function prototype indicates that the function receives a *variable number of arguments of any type*. The ellipsis must always be placed at the *end* of the parameter list.

The macros and definitions of the variable arguments headers <stdarg.h> (Fig. 14.1) provide the capabilities necessary to build functions with variable-length argument lists. Figure 14.2 demonstrates function average (lines 25–39) that receives a variable number of arguments. The first argument of average is always the number of values to be averaged.

| Identifier | Explanation |
|---|---|
| va_list | A type suitable for holding information needed by macros va_start, va_arg and va_end. To access the arguments in a variable-length argument list, an object of type va_list must be defined. |

Fig. 14.1 stdarg.h variable-length argument-list type and macros. (Part 1 of 2.)

| Identifier | Explanation |
| --- | --- |
| `va_start` | A *macro* that's invoked before the arguments of a variable-length argument list can be accessed. The macro initializes the object declared with `va_list` for use by the `va_arg` and `va_end` macros. |
| `va_arg` | A *macro* that expands to the value of the next argument in the variable-length argument list—the value has the type specified as the macro's second argument. Each invocation of `va_arg` modifies the object declared with `va_list` so that it points to the next argument in the list. |
| `va_end` | A *macro* that facilitates a normal return from a function whose variable-length argument list was referred to by the `va_start` macro. |

**Fig. 14.1** | *stdarg.h variable-length argument list type and macros. (Part 2 of 2.)*

```c
1 // Fig. 14.2: fig14_02.c
2 // Using variable-length argument lists
3 #include <stdio.h>
4 #include <stdarg.h>
5
6 double average(int i, ...); // prototype
7
8 int main(void)
9 {
10 double w = 37.5;
11 double x = 22.5;
12 double y = 1.7;
13 double z = 10.2;
14
15 printf("%s%1.1f\n%s%1.1f\n%s%1.1f\n%s%1.1f\n\n",
 "w = ", w, "x = ", x, "y = ", y, "z = ", z);
16 printf("%s%3.1f\n%s%3.1f\n%s%3.1f\n",
 "The average of w and x is ", average(2, w, x),
 "The average of w, x, and y is ", average(3, w, x, y),
 "The average of w, x, y, and z is ",
 average(4, w, x, y, z));
17 }
18
19 // calculate average
20 double average(int i, ...)
21 {
22 double total = 0; // initialize total
23 va_list ap; // stores information needed by va_start and va_end
24
25 va_start(ap, i); // initializes the va_list object
26
27 // process variable-length argument list
28 for (int j = 1; j <= i; ++j) {
29 total += va_arg(ap, double);
30 }
```

**Fig. 14.2** | *Using variable-length argument lists. (Part 1 of 2.)*

```c
36
37 va_end(ap); // clean up variable-length argument list
38 return total / i; // calculate average
39 }
```

```
w = 37.5
x = 22.5
y = 1.7
z = 10.2

The average of w and x is 30.000
The average of w, x, and y is 20.567
The average of w, x, y, and z is 17.975
```

Fig. 14.2 | Using variable-length argument lists. (Part 2 of 2.)

Function average (lines 25–39) uses all the definitions and macros of header <stdarg.h>, except va_copy (Section E.8.10), which was added in C11. Object ap, of type va_list (line 28), is used by macros va_start, va_arg and va_end to process the variable-length argument list of function average. The function begins by invoking macro va_start (line 30) to initialize object ap for use in va_arg and va_end. The macro receives two arguments—object ap and the identifier of the rightmost argument in the argument list before the ellipsis—i in this case (va_start uses i here to determine where the variable-length argument list begins). Next, function average repeatedly adds the arguments in the variable-length argument list to variable total (lines 33–35). The value to be added to total is retrieved from the argument list by invoking macro va_arg. Macro va_arg receives two arguments—object ap and the type of the value expected in the argument list—double in this case. The macro returns the value of the argument. Function average invokes macro va_end (line 37) with object ap as an argument to facilitate a normal return to main from average. Finally, the average is calculated and returned to main.

> **Common Programming Error 14.1**
> Placing an ellipsis in the middle of a function parameter list is a syntax error—an ellipsis may be placed only at the end of the parameter list.

You might wonder how functions with variable-length argument lists like printf and function scanf know what type to use in each va_arg macro. The answer is that, as the program executes, they scan the format conversion specifiers in the format control string to determine the type of the next argument to be processed.

## 14.4 Using Command-Line Arguments

On many systems, it's possible to pass arguments to main from a command line by including parameters int argc and char *argv[] in the parameter list of main. Parameter argc receives the number of command-line arguments that the user has entered. Parameter argv is an array of strings in which the actual command-line arguments are stored. Common uses of command-line arguments include passing options to a program and passing filenames to a program.

Figure 14.3 copies a file into another file one character at a time. We assume that the executable file for the program is called mycopy. A typical command line for the mycopy program on a Linux/UNIX system is

```bash
$ mycopy input output
```

This command line indicates that file input is to be copied to file output. When the program is executed, if argc is not 3 (mycopy counts as one of the arguments), the program prints an error message and terminates. Otherwise, argv array contains the strings "mycopy", "input" and "output". The second and third arguments on the command line are used as filenames by the program. The files are opened using function fopen. If both files are opened successfully, characters are read from file input and written to file output until the end-of-file indicator for file input is set. Then the program terminates. The result is an exact copy of file input (if no errors occur during processing). See your system documentation for more information on command-line arguments. [Note: In Visual C++, you specify command-line arguments by right clicking the project name in the Solution Explorer and selecting Properties, then expanding Configuration Properties, selecting Debugging and entering the arguments in the textbox to the right of Command Arguments.]

```c
1 // Fig. 14.3: fig14_03.c
2 // Using command-line arguments
3 #include <stdio.h>
4
5 int main(int argc, char *argv[])
6 {
7 // check number of command-line arguments
8 if (argc != 3) {
9 puts("Usage: mycopy infile outfile");
10 }
11 else {
12 FILE *inFilePtr; // input file pointer
13
14 // try to open the input file
15 if ((inFilePtr = fopen(argv[1], "r")) != NULL) {
16 FILE *outFilePtr; // output file pointer
17
18 // try to open the output file
19 if ((outFilePtr = fopen(argv[2], "w")) != NULL) {
20 int c; // holds characters read from source file
21
22 // read and output characters
23 while ((c = fgetc(inFilePtr)) != EOF) {
24 fputc(c, outFilePtr);
25 }
26
27 fclose(outFilePtr); // close the output file
28 }
29 else { // output file could not be opened
30 printf("File \"%s\" could not be opened\n", argv[2]);
31 }
32 }
33 }
34 }
```

**Fig. 14.3** | Using command-line arguments. (Part 1 of 2.)

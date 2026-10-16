```
argv[2] contains: want
argv[3] contains: an
argv[4] contains: argument
```

From these examples it should be evident that the values of argc and argv depend on what the user enters on the command line when invoking the program. If the user enters the name of the program followed by i arguments, then the value of argc will be i + 1, the number of character strings entered on the command line; argv[0] will refer to the name of the program; and argv[1] through argv[i] will refer to the i arguments that were entered.

# 15.5.2 Example: A Square Root Calculator

As a simple illustration of the use of argv and argc, consider the problem of designing a square root calculator that allows the user to enter the value(s) to be processed on the command line and that then calculates and displays the square roots of each value. For example, if the command

```
$ sroot 4 9 16 25
```

is entered, the values 2, 3, 4, and 5 are to be displayed.

Because the program must process command-line arguments, it receives the arguments through the parameters of the main function (i.e., argc and argv). Here are some possibilities of what the user might enter:

```
$ sroot                  // error—no data to process (argc is 1)
$ sroot A                // error—nonnumeric data (argc is 2, argv[1] is "A")
$ sroot -1               // error—negative data (argc is 2, argv[1] is "-1")
$ sroot 9                // one value (argc is 2, argv[1] is "9")
$ sroot 4 9              // two values (argc is 3, argv[1] is "4", argv[2] is "9")
```

From the first example, we see that valid input requires argc > 1. Also, each argv[i] refers to a character string, and we must take the square root of a value of type double. This means that the character string stored in argv[i] must be converted to the corresponding double value. Fortunately, C++ provides the strtod() function in cstdlib that performs this operation. That function can also be used to make our program more foolproof by checking its return value—strtod() returns 0 if it is unable to convert the string to a numeric value, which is the case in the second and third examples. Once we have converted the character string to the corresponding double value, all that remains is to find its square root, which is easy, using the sqrt() function declared in cmath. We then simply display the value and its square root.

We can thus construct the following algorithm, which checks that at least one command-line argument has been given, and if so, uses a loop to process each argument.
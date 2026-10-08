
# 15.5 Program Termination with exit and atexit

The general library `<stdlib.h>` provides methods of terminating program execution by means other than a conventional return from `main`.

## exit Function

The `exit` terminates a program immediately. This function often is used to terminate a program when an error is detected. The function takes one argument—normally, `EXIT_SUCCESS` or `EXIT_FAILURE`: These contain implementation-defined values for successful termination.

## atexit Function

The `atexit` registers a function to call when the program terminates by reaching the end of `main` or when `exit` is invoked. This function takes as an argument another function’s name. Recall that a function name cannot have arguments and return a value. When a program terminates, any functions previously registered with `atexit` are invoked in the reverse order of their registration.

## Using Functions exit and atexit

Figure 15.3 tests function `exit` and `atexit`. The program prompts the user to determine whether the program should be terminated with `exit` or by reaching the end of `main`. Function `print` is executed at program termination in each case.

```c
// fig15_03.c
// Using the exit and atexit functions
#include <stdio.h>
#include <stdlib.h>

void print(void); // prototype

main(void) {
    atexit(print); // register function print
    puts("Enter 1 to terminate program with exit\n");
    puts("Enter 2 to terminate program normally\n");
    int answer = 0; // user
    scanf("%d", &answer);

    // call exit if answer is 1
    if (answer == 1) {
        puts("\nTerminating program with function exit\n");
        exit(EXIT_SUCCESS);
    }

    puts("\nTerminating program by reaching the end of main\n");
}

// display message before termination
void print(void) {
    puts("Executing function print at program termination\n");
    puts("Program terminated\n");
}
```

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_761_0.png)

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_761_1.png)

Fig. 15.3 | Using the `exit` and `atexit` functions.

# Self Check

1 (**Multiple Choice**) Which of the following statements is *false*?

- a) Variables declared outside any function definition are global variables.
- b) Global variables are accessible to any function defined in the same file after the variable is declared.
- c) Global variables are also accessible to functions in other files.
- d) once a global variable is defined, it is known to all the application's files.

**Answer:** d) is *false*. Actually, global variables must be declared in *each* file in which they’re used.

- 2 (**Fill-In**) Any identifier that’s declared at that scope is _______ by default.

**Answer:** `extern`.

- 3 (**True/False**) You should prefer global variables to local variables because global variables enforce the principle of least privilege. False. Actually, you should avoid global variables unless application performance is critical because they *violate* the principle of least privilege.

- 4 (**Fill-In**) Applying `static` to a global variable or a function prevents it from being used by any function that’s not defined in the same file—this is called _______ linkage.

**Answer:** `internal`.

- 5 (**True/False**) The following global variable definition indicates that `PI` is known only to functions in the file which it is defined:

```c
static const double PI = 3.14159;
```

**Answer:** *True*.

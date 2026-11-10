On a Linux system, **gcc** calls the assembler (4.2.3) to create the .o files before it invokes the linker to create a single executable. Using the -c option, you can create only the object files and without creating **a.out**.

```
gcc -c a.c b.c c.c
```

*Creates only* a.o, b.o *and* c.o

For single-source programs (where functions are stored in the same file as the main program itself), we normally don’t need the intermediate .o file. However, in a real-life scenario, we are often compelled to do a *partial* compilation and maintain these .o files. To understand why, let’s examine a multi-source application.

# 17.13.1 A Multi-Source Application

Our sample application computes the interest on a recurring deposit. The main program, **rec_deposit.c** (Program 17.7a), accepts three arguments representing the principal, interest and term. The maturity amount is written to the standard output. The main program invokes three functions:

+   - **arg_check** This function checks whether the right number of arguments has been keyed in. It is defined in **arg_check.c** which includes arg_check.h (Program 17.7b).
+   - **quit** This function prints a message and terminates the program. It is defined in **quit.c** and includes quit.h (Program 17.7c).
+   - **compute** It computes the interest from the three arguments provided. This function is not placed in a separate file.

**arg_check** and **quit** are useful reusable functions. **compute** is maintained in the main file only to understand why this too should be moved to its own source file. The two header files contain—apart from the usual include statements—the prototypes of their respective functions. These functions are used in **main**, so their header files must be included in **rec_deposit.c** also.

```
```c
#include <math.h>
#include "quit.h"
#include "arg_check.h"
float compute(float, float, float);
int main(int argc, char **argv) {
    float principal, interest, term, sum;
    char *mesg = "Three arguments required\n";
    char *mesg2 = "All arguments must be positive\n";
    arg_check(4, argc, mesg, 1);       /* Checks for three arguments */
    sscanf(argv[1], "%f", &principal); /* Converting strings to float */
    sscanf(argv[2], "%f", &interest);
    sscanf(argv[3], "%f", &term);

    if (principal <= 0 || interest <= 0 || term <= 0)
        quit(mesg2, 2);                /* Quits with 2 as $? on error */
```
```
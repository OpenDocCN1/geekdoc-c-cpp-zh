```
```
}
```
```

Listing 5.7 contains a loop that iterates through the command line arguments and prints them via the `printf()` function. After compiling the code, launch the program in Listing 5.7 as follows (you can use different arguments):

```
```
/PrintCmdLineArguments 1 a 2 b 3 c
```
```

The output is here:

```
```
Display Command Line Arguments
Argument 0 = "./PrintCmdLineArguments"
Argument 1 = "1"
Argument 2 = "a"
Argument 3 = "2"
Argument 4 = "b"
Argument 5 = "3"
Argument 6 = "c"
```
```

You can easily check for the number of arguments and perform an early exit with the `exit()` function, as shown in the following code block:

```
```c
#include <stdio.h>
#include <stdlib.h> // required for the exit() function

int main(int argc, char *argv[])
{
    if( argc < 3 )
    {
        fprintf(stderr, "Not enough Arguments: %d\n", argc);
        exit(-1);
    }

    // proceed normally...
}
```
```

Although you can perform an early exit with the `abort()` function, keep in mind that the latter does not flush
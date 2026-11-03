1. Begin a new program with a preprocessor instruction to include the standard input/output functions and constants

```c
#include <stdio.h>
#include <limits.h>
```

2. Add a main function that contains statements to output the size and range of the short int data type

```c
int main()
{
printf("short int... \t size: %d bytes \t", sizeof( short int ));
printf("%d to %d \n", SHRT_MAX, SHRT_MIN );
}
```

3. Next, insert statements to output the size and range of the long int data type

```c
printf("long int... \t size: %d bytes \t", sizeof( long int ));
printf("%ld to %ld \n", LONG_MAX, LONG_MIN );
```

4. Now, insert statements to output the size of other data

```c
printf("char... \t size: %d byte \n", sizeof( char ));
printf("float... \t size: %d bytes \n", sizeof( float ));
printf("double... \t size: %d bytes \n", sizeof( double ));
```

5. Insert a final statement to return a zero integer value, as required by the function declaration

```c
return 0;
```

6. Save the program file, then compile and execute the program to see the data type sizes and ranges

![](bbox=[0.7, 0.07, 0.85, 0.22])

![](bbox=[0.7, 0.55, 0.85, 0.7])

Notice how the \t tab escape sequence is used in this example to space the output.

![](bbox=[0.15, 0.75, 0.85, 0.98])
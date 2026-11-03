Output:
    FLAG is defined
    a = 21, b = 5
    Program completed

The macro FLAG has been defined, so the statements between #ifdef and #endif are compiled. If we delete the definition of macro FLAG from the program, then these statements won't be compiled and the output of the program would be-
    a = 20, b = 4
    Program completed

```
/*P12.18 Program to understand the use of #undef and #ifdef directives*/
#include<stdio.h>
#define FLAG
main()
{
    int a=20,b=4;
    #ifdef FLAG
    printf("FLAG is defined\n");
    a++;
    b++;
    #endif
    #undef FLAG
    #ifdef FLAG
    printf("Preprocessor\n");
    a++;
    b++;
    #endif
    printf("a = %d, b= %d\n",a,b);
    printf("Program completed\n");
}
```

Output:
    FLAG is defined
    a = 21, b = 5
    Program completed

Here we have undefined the macro FLAG in the middle of program. So the macro FLAG is defi
only for the part of the program that is before the #undef directive, and it is undefined for the r
of the program.

```
/*P12.19 Program to understand the use of #ifndef directive*/
#include<stdio.h>
main()
{
    int a=20,b=4;
    #ifndef MAX
    printf("MAX is not defined\n");
    a--;
    b--;
    #endif
```
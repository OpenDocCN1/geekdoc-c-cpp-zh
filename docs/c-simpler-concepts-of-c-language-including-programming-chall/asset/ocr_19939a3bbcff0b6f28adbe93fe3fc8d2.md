# STORAGE QUALIFIERS

```
/* 1.c */
# include <stdio.h>
int count = 10;
void write();
main () {
    write();
}
```

```
/* 2.c */
extern int count;
void write () {
    printf("\n the count is %d",count);
}
```

Compilation Steps:
gcc -c 1.c

Compilation Steps:
gcc -c 2.c

```
Execution (to run)
$ gcc -o 1.o 2.o output
$ ./output
$ the count is 10
```

# Program 6.5 Use of extern storage qualifier.

# extern Methods

So far the extern variables are discussed. Not only variables, but also methods can be declared extern. For instance, declaring 'extern int increase()' suggests the compiler that the method's definition is somewhere else and that program will be linked during execution!

# Important Note

The extern keyword greatly helps in increasing reusability. Sometimes 2 or more programs may want to collaborate with one another, in such times, we can have a common file where all the common variables and methods are initialized. Any change made by any program will affect the global variables declared in the external file. Also note that, the file where the global variables are declared should't have a main().

# POINTS TO REMEMBER

+   1. There are 4 standard storage qualifiers available for the programmers in C language.
2. Any variable which is declared in the body of a function is by default automatic.
3. If not initialized with a value, auto variables will get garbage in it.
4. Static is the default storage class for global variables.
5. Static variables will have zero initialized to it, if not by programmer.
6. Register is a special storage qualifier which occupies storage space from CPU registers.
7. Extern is very widely used type of storage qualifier for actions across many object files.

# 6.2 QUI

```
1. main ()
{
int i =10;
```

## 29. MEMORY MANAGEMENT

This chapter explains dynamic memory management in C. The C programming language provides several functions for memory allocation and management. These functions can be found in the **<stdlib.h>** header file.

| S.N. | Function and Description |
|------|--------------------------|
| 1 | **void *calloc(int num, int size);**<br>This function allocates an array of **num elements** each of which size in bytes will be **size**. |
| 2 | **void free(void *address);**<br>This function releases a block of memory specified by address. |
| 3 | **void *malloc(int num);**<br>This function allocates an array of **num** bytes and leave them uninitialized. |
| 4 | **void *realloc(void *address, int newsize);**<br>This function re-allocates memory extending it up to **newsize**. |

### Allocating Memory Dynamically

While programming, if you are aware of the size of an array, then it is easy and you can define it as an array. For example, to store a name of any person, it can go up to a maximum of 100 characters, so you can define something as follows:

```c
char name[100];
```

But now let us consider a situation where you have no idea about the length of the text you need to store, for example, you want to store a detailed description about a topic. Here we need to define a pointer to character without defining how much memory is required and later, based on requirement, we can allocate memory as shown in the below example:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char name[100];
    char *description;

    strcpy(name, "Zara Ali");

    /* allocate memory dynamically */
    description = malloc( 200 * sizeof(char) );
    if( description == NULL )
    {
        fprintf(stderr, "Error - unable to allocate required memory\n");
    }
    else
    {
        strcpy( description, "Zara ali a DPS student in class 10th");
    }
    printf("Name = %s\n", name );
    printf("Description: %s\n", description );
}
```

When the above code is compiled and executed, it produces the following result.

```text
Name = Zara Ali
Description: Zara ali a DPS student in class 10th
```

Same program can be written using **calloc();** only thing is you need to replace malloc with calloc as follows:

```c
calloc(200, sizeof(char));
```

So you have complete control and you can pass any size value while allocating memory, unlike arrays where once the size is defined, you cannot change it.

## 30. COMMAND LINE ARGUMENTS

It is possible to pass some values from the command line to your C programs when they are executed. These values are called command line arguments and many times they are important for your program especially when you want to control your program from outside instead of hard coding those values inside the code.

The command line arguments are handled using main() function arguments where argc refers to the number of arguments passed, and argv[] is a pointer array which points to each argument passed to the program. Following is a simple example which checks if there is any argument supplied from the command line and take action accordingly:

```c
#include <stdio.h>

int main( int argc, char *argv[] )
{
    if( argc == 2 )
    {
    printf("The argument supplied is %s\n", argv[1]);
    }
    else if( argc > 2 )
    {
    printf("Too many arguments supplied.\n");
    }
    else
    {
    printf("One argument expected.\n");
    }
}
```

When the above code is compiled and executed with a single argument, it produces the following result.

```text
$ ./a.out testing
The argument supplied is testing
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_182_0.png)

When the above code is compiled and executed with two arguments, it produces the following result.

```text
$ ./a.out testing1 testing2
Too many arguments supplied.
```

When the above code is compiled and executed without passing any argument, it produces the following result.

```text
$ ./a.out
One argument expected
```

It should be noted that **argv[0]** holds the name of the program itself and **argv[1]** is a pointer to the first command line argument supplied, and argv[n] is the last argument. If no arguments are supplied, argc will be one, and if you pass one argument, then **argc** is set at 2.

You pass all the command line arguments separated by a space, but if argument itself has a space then you can pass such arguments by putting them inside double quotes "" or single quotes ''. Let us re-write above example once again where we will print program name and we also pass a command line argument by putting inside double quotes:

```c
#include <stdio.h>

int main( int argc, char *argv[] )
{
    printf("Program name %s\n", argv[0]);

    if( argc == 2 )
    {
        printf("The argument supplied is %s\n", argv[1]);
    }
    else if( argc > 2 )
    {
        printf("Too many arguments supplied.\n");
    }
    else
    {
        printf("One argument expected.\n");
    }
}
```

When the above code is compiled and executed with a single argument separated by space but inside double quotes, it produces the following result.

```text
$ ./a.out "testing1 testing2"

Program name ./a.out
The argument supplied is testing1 testing2
```

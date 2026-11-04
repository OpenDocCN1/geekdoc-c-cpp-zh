```
if(*row >= ROWS || *row < 0 || *col >= COLS || *col < 0)
{
    printf("Out of bound dimensions\n");
    continue;
}
if(s[*row][*col] == 1)
{
    printf("Error: This card is already flipped\n"
    continue;
}
s[*row][*col] = 1; /* Change the card position to face up.
    return;
}
```

# Passing Data in main() Function

When we run a program from the command line, we'll often need to pass data to it. For example, suppose that the executable file hello.exe is stored in C disk. The command line:

```
C:\>hello 100 200
```

executes the program hello and passes the values 100 and 200 to main(). To get the data, main() must be defined like this:

```
int main(int argc, char *argv[])
```

Although you can use any names, argc (argument count) and argv (argument vector) are, by convention, the typical choices. And because the compiler translates an array parameter to pointer, many prefer to write **argv instead of *argv[].

The value of argc is equal to the number of the command line arguments, including the name of the program itself. For example, in the previous command line, argc is 3. The arguments should be separated with space(s), to distinguish the values.

The argv parameter is an array of pointers to the command line arguments, which are stored in string form. argv[0] pointer points to the name of the program, while the other pointers up to argv[argc-1] point to the remaining arguments. The last argv element is the argv[argc], which is always NULL. In our example, the arguments hello, 100, and 200 are passed to main() as strings. In particular, argv[0] points to the string "hello", argv[1] points to "100", argv[2] points to "200", and argv[3] is NULL.

For example, the following program checks if the user entered the correct user name and password. Suppose that these are user and ps wd, respectively.

```
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
```
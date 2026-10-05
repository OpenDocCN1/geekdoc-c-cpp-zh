# COMMAND LINE ARGUMENTS

Ok, what is the second way?

2. Assign the command line arguments to global variables, which can then be accessed by any function. Refer Program 12.6 for reference; but since global variables cause some problems in very large programs, it is generally not used!

```
#include<stdio.h>
void func();
int argc;
char *argv[10];
void main(int argc, char *argv[])
{
    int i;
    for(i=0;i<argc;i++)
        argv1[i]=argv[i];
    argc1=argc;
    func();
    getch();
}

void func()
{
    int i;
    printf("%d", argc1);
    for(i=0;i<argc1;i++)
        printf("%%s", argv[i]);
}
```

# Program 12.6 Assigning command line args to global variables.

The reader is encouraged to answer the questions in quiz section to test the % of understanding.

POINTS TO REMEMBER

+   - Parameters can be passed to the function main() from the operating system prompt as command line arguments.
- The command line arguments are accepted into special parameters to main( ), namely, argc and argv.
- argc decodes argument count which includes the program name also, and, argv, the argument vector.
- Parameters passed from command prompt are all of type character arrays.
- Minimum number of arguments that should be passed is one (The program name).
- argc and argv values are local to the main(). They cannot be accessed from outside!

# 12.3. QUIZ

+   1. Define command line arguments.
2. argc and argv are local to main() – TRUE/FALSE.
3. What do the characters 'c' and 'v' in argc and argv imply?
4. Give the output of the following program. If executed as follows from the command prompt?
C:\turboc<prog> cmdline_prog 1 2 3
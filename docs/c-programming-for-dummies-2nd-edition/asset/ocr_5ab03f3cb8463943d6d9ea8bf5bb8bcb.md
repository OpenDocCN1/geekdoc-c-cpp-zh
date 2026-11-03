# LISTING 10-1: Basic Function; No Return

```
#include <stdio.h>

void prompt();    /* function prototype */

int main()
{
    int loop;
    char input[32];

    loop=0;
    while(loop<5)
    {
        prompt();
        fgets(input,32,stdin);
        loop=loop+1;
    }
    return(0);
}

/* Display prompt */

void prompt(void)
{
    printf("C:\\DOS> ");
}
```

# Exercise 10-1: Use the source code from Listing 10-1 to create a new program. Build and run.

The program displays a prompt five times, allowing you to type various commands. Of course, nothing happens when you type commands, though you can program those actions later, if you like. Here’s how this program works in regard to creating a function:

Line 3 lists the function prototype. It’s essentially a copy of the first line of the function (from Line 22), but ending with a semicolon. It can also be written like this:

```
void prompt(void);
```
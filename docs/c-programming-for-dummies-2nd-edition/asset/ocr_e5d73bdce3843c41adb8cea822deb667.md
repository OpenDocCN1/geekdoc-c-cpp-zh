# LISTING 15-3: (continued)

```
void sub(void)
{
    puts("Which is the plan.");
    exit(0);
}
```

You must include the stdlib.h header file to use the exit() function, and it consumes an int value as an argument for the exit status, similar to the value passed by return in the main() function.

Exercise 15-5: Type the source code from Listing 15-3 into your edit. Build and run the program.

# Running another program

The system() function directs your program to run another program or to issue a command. For example:

```
system("blorf");
```

The preceding statement directs the operating system to issue the blorf command, running whatever program has that name or carrying out whatever actions the blorf command dictates.

After running the command, control returns to your program, which continues with the statement following the system() function.

Listing 15-4 contains two system() functions; your code needs only one. Use the first system() statement if you're using Windows; use the second statement if you're using anything else. Or you can just comment out the statement rather than delete it.

# LISTING 15-4: Clearing Things Up

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    printf("Press Enter to clear the screen.");
    getchar();
```
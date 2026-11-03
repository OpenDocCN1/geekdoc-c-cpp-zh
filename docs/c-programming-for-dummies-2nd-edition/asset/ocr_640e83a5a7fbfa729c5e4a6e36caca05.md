# Linking two source code files

The most basic multi-module monster project has two source code files. Each file is separate — written, saved, and compiled individually — but eventually brought together as one unit by the linker. The linker, which is part of the build process in Code::Blocks, is what creates a single program from several different modules.

# What's a module?

A module is a compiled object file. The various object files are linked to build a program. The entire operation starts with separate source code files, starting with Listing 24-1.



```
```c
#include <stdio.h>
#include <stdlib.h>
void second(void);
int main()
{
    printf("Second module, I send you greetings!\n");
    second();
    return 0;
}
```
```

Listing 24-1 shows the main.c module. In it, you see the second() function prototyped at Line 4. This prototype is required because the second() function is called at Line 11, but it exists in another module — just like C library functions exist elsewhere. You don't need to prototype all functions found in another module, only those referenced or called.

Exercise 24-1: Fire up a new project in your IDE named ex2401. Create the project as you normally would. Type the source code from Listing 24-1 into the editor as you normally would. Don't build yet! After all, the code references the second() function, which doesn't seem to exist anywhere. It's prototyped, as is required for any function that's used in your code, but the second() function is found in another module. To create this next module in the Code::Blocks IDE, follow these steps:
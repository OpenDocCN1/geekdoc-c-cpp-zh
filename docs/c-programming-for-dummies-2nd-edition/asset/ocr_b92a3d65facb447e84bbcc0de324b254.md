# LISTING 24-4: Code for second.c Using the Global Variable

```
```c
#include <stdio.h>

extern int count;

void second(void)
{
    printf("%d\n",count+1);
}
```
```

The second.c source code file declares external variable count, which is found in the main.c file. To properly access this variable, Line 3 in Listing 24-4 identifies it as an external int. The count variable is then used in the second() function — specifically, at Line 7. Its value is retained between modules and all functions in which it's used.

**Exercise 24-2:** Create a new project in Code::Blocks that incorporates both source code files shown in Listings 24-3 and 24-4. Build and run.

To build the project at the command prompt: Update the two source code files from Exercise 24-1 and build per the directions at the end of the preceding section.

# Creating a custom header file

As multi-module projects grow more complex, you find that the first part of each source code file gets longer and longer: More prototypes, more constants, and more external variables, structures, and other whatnot are required for each module. Rather than burden your source code files with redundancies, you can create a header file for the project.

A header file contains just about everything you can put into a source code file. Specifically, it's best to put items in the header file that would otherwise be required for every source code module. Listing 24-5 shows a sample header file.

# LISTING 24-5: Header File ex2403.h

```
```c
#include <stdio.h>
#include <stdlib.h>

/* structures */
struct thing {
```
```
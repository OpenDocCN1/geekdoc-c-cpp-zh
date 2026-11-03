To use a local header file, you specify the #include preprocessor directive at the start of the source code file, as in any other header file. The big difference is that double quotes are used instead of angle brackets. For example:

```
#include "ex24O3.h"
```

The double quotes direct the compiler to look for the header file in the current directory. If the file isn't in that directory, you must specify a pathname, as in

```
#include "headers/ex24O3.h"
```

Listing 24-6 uses the header file from Listing 24-5.

# LISTING 24-6: Project ex24O3 main.c Source Code

```
#include "ex24O3.h"

human person;

int main()
{
    fillstructure();
    printstructure();
    return 0;
}

void fillstructure(void)
{
    printf("Enter your name: ");
    fgets(person.name,31,stdin);
    printf("Enter your age: ");
    scanf("%d",&person.age);
}

void printstructure(void)
{
    printf("You are %s\n",person.name);
    printf("And you are %d years old.\n",person.age);
}
```
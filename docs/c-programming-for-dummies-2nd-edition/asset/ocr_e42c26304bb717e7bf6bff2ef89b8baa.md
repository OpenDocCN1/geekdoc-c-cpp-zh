# Filling a structure

As with other variables, you can initialize a structure variable when it's created. You first define the structure type and then declare a structure variable with its member values preset. Ensure that the preset values match the order and type of members defined in the structure, as shown in Listing 14-2.

# LISTING 14-2 Declaring an Initialized Structure

```
```c
#include <stdio.h>

int main()
{
    struct president
    {
        char name[40];
        int year;
    };
    struct president first = {
        "George Washington",
        1789
    };

    printf("The first president was %s\n",first.name);
    printf("He was inaugurated in %d\n",first.year);

    return(0);
}
```
```

Exercise 14-3: Create a new program by typing the source code from Listing 14-2 into the editor. Build and run.

You can also declare a structure and initialize it in one statement:

```
```c
struct president
{
    char name[40];
    int year;
} first = {
    "George Washington",
    1789
};
```
```
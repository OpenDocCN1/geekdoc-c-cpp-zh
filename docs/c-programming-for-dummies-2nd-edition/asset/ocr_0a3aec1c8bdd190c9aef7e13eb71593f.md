# Exercise 14-4

Modify your source code from Exercise 14-3 so that the structure and variable are declared and initialized as one statement.

# Exercise 14-5

Add another president structure variable, second, to your code, initializing that structure with information about the second president, John Adams, who was inaugurated in 1797. Display the contents of both structures.

# Making an array of structures

Creating individual structure variables, one after the other, is boring and wasteful as creating a series of any individual variable type. The solution for multiple structures is the same as for multiple individual variables: array.

A structure array is declared like this:

```
struct scores player[4];
```

This statement declares an array of scores structures. The array is named player, and it contains four structure variables as its elements.

The structures in the array are accessed using a combination of array and structure notation. For example:

```
player[2].name
```

The variable in the preceding line accesses the name member in the third element (2) in the player structure array. Yes, that's the third element because the first element would be referenced like this:

```
player[0].name
```

Arrays start numbering with the element 0, not element 1.

> Line 10 in Listing 14-3 declares an array of four scores structures. The array is named player. Lines 13 through 19 fill each structure in the array. Lines 21 through 27 display each structure's member values.

# Listing 14-3: Arrays of Structures

```
#include <stdio.h>

int main()
{
    struct scores {
        char name[30];
        int score;
    } player[4];

    int i;

    for (i = 0; i < 4; i++) {
        printf("Enter name and score for player %d: ", i);
        scanf("%s %d", player[i].name, &player[i].score);
    }

    printf("\n");

    for (i = 0; i < 4; i++) {
        printf("Player %d: %s %d\n", i, player[i].name, player[i].score);
    }

    return 0;
}
```
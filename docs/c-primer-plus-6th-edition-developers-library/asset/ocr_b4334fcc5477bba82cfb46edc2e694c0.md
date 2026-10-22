Suppose you don’t specify the array size?

```
int stuff[] = {1, [6] = 23};      // what happens?
int staff[] = {1, [6] = 4, 9, 10}; // what happens?
```

The compiler will make the array big enough to accommodate the initialization values. So stuff will have seven elements, numbered 0-6, and staff will have two more elements, or 9.

# Assigning Array Values

After an array has been declared, you can assign values to array members by using an array index, or subscript. For example, the following fragment assigns even numbers to an array:

```
/* array assignment */
#include <stdio.h>
#define SIZE 50
int main(void)
{
    int counter, evens[SIZE];

    for (counter = 0; counter < SIZE; counter++)
        evens[counter] = 2 * counter;
    ...
}
```

Note that the code uses a loop to assign values element by element. C doesn’t let you assign one array to another as a unit. Nor can you use the list-in-braces form except when initializing. The following code fragment shows some forms of assignment that are not allowed:

```
/* nonvalid array assignment */
#define SIZE 5
int main(void)
{
    int oxen[SIZE] = {5,3,2,8};      /* ok here      */
    int yaks[SIZE];

    yaks = oxen;                    /* not allowed  */
    yaks[SIZE] = oxen[SIZE];        /* out of range */
    yaks[SIZE] = {5,3,2,8};         /* doesn't work */
```

Recall that the last element of oxen is oxen[SIZE-1], so oxen[SIZE] and yaks[SIZE] refer to data past the ends of the two arrays.

# Array Bounds

You have to make sure you use array indices that are within bounds; that is, you have to make sure they have values valid for the array. For instance, suppose you make the following declaration:

```
int doofi[20];
```
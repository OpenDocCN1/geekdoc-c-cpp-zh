# LISTING 12-7: An Array of Strings

```
#include <stdio.h>

int main()
{
    int const size = 3;
    char caesar[size][9] = {
        "Julius",
        "Augustus",
        "Nero"
    };
    int x, index;

    for(x=0;x<size;x++)
    {
        index = 0;
        while(caesar[x][index] != '\0')
        {
            putchar(caesar[x][index]);
            index++;
        }
        putchar('\n');
    }
    return(0);
}
```

Line 6 in Listing 12-7 declares a two-dimensional char array: caesar. The first value in square brackets is the number of items (strings) in the array, set by the constant size. The second value in square brackets is the maximum size required to hold the largest string. The largest string is Augustus with eight letters, so nine characters are required for storage, which includes the terminating \0 or null character.

Because all items in the array's second dimension must have the same number of elements, all strings are stored using nine characters. Yep, this configuration is wasteful, but it's the way the system works. Figure 12-1 illustrates this concept.

**Exercise 12-18:** Type the source code from Listing 12-7 into your editor; build and run the program.
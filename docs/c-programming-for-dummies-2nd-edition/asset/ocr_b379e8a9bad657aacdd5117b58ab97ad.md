# LISTING 21-1: Oh, So This Is the Time?

```
#include <stdio.h>
#include <time.h>

int main()
{
    time_t tictoc;

    time(&tictoc);
    printf("The time is now %ld\n",tictoc);
    return(0);
}
```

Line 2 in Listing 21-2 brings in the time.h header file, which is required for various time functions in C.

Line 6 declares the time_t variable tictoc. The time() function at Line 8 requires the address of a time_t variable as its argument. The time value is placed directly into variable tictoc (in its memory location).

Finally, in Line 9, the resulting value — the Unix epoch — is output by using the %ld conversion character, long int.

# Exercise 21-1: Type the source code from Listing 21-1 into your editor. Build and run.

# Exercise 21-2: Edit your solution from Exercise 21-1, replacing Line 8 with

```
tictoc=time(NULL);
```

The time() function requires a memory location as an argument, but it also returns a time_t value. You can use either the format just presented or the format shown at Line 8 in Listing 21-1, depending on which weirdo symbol, the & or NULL, frightens you the most.

![](bbox=[0.15, 0.82, 0.25, 0.95])

Back in the 1970s and '80s, BASIC programmers would write for loops in their code to pause program execution. I recall that my trusty old TRS-80 required a loop that counted from 1 to 100 to delay execution by one second. Today's systems are far faster, and such loops can no longer be relied upon to accurately delay program execution.
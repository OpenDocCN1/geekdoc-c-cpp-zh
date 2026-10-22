Here’s another chance to practice using multiple files. Use one file for Listing 12.7 and one for Listing 12.8. The extern keyword reminds you that rand0() is defined in a separate file, but it’s not required.

The output is this:

```
16838
5758
10113
17515
31051
```

The output looks random, but let’s run it again. This time the result is as follows:

```
16838
5758
10113
17515
31051
```

Hmmm, that looks familiar; this is the “pseudo” aspect. Each time the main program is run, you start with the same seed of 1. You can get around this problem by introducing a second function called srand1() that enables you to reset the seed. The trick is to make next a static variable with internal linkage known only to rand1() and srand1(). (The C library equivalent to srand1() is called srand().) Add srand1() to the file containing rand1(). Listing 12.9 is the modification.

# Listing 12.9 The s_and_r.c Program

```
/* s_and_r.c -- file for rand1() and srand1() */
/* uses ANSI C portable algorithm */
static unsigned long int next = 1; /* the seed */

int rand1(void)
{
/* magic formula to generate pseudorandom number */
    next = next * 1103515245 + 12345;
    return (unsigned int) (next/65536) % 32768;
}

void srand1(unsigned int seed)
{
    next = seed;
}
```
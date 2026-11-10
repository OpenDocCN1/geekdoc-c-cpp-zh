```
    p = "Samsung Galaxy";          p now contains address of 'S'
    p = stg4;                      p points to the string "Xolo"
```

Note that arrays have fixed addresses which can't be changed even though their contents can be. For instance, you can reassign any element, say, stg4[3] to 'C'. But you can't change the value stg4 evaluates to.

# ### 13.2.4 When an Array of Characters Is Not a String

An array of characters is not a string when it doesn't include the '\0' character as the terminator. Usually, we don't bother to include the NUL because the compiler does this job for us, but negligence on our part can prevent the compiler from doing so. Consider the following declarations:

```
    char stg5[5] = {'f', 'i', 'o', 'a', 't'};        This isn't a string ...
    char stg6[30] = {'f', 'i', 'o', 'a', 't'};        ... but this one is.
```

In this scenario, stg5 has no space left to store the NUL character. When printf encounters this string, it continues printing beyond the 't' until it encounters a NUL somewhere on the way. This means looking at a region of memory not reserved for it. You may see extra characters printed at the end of the word float or the program could even crash.

The NUL character has not been explicitly inserted in stg6, so one would be tempted to conclude that stg6 is not a string. However, stg6 is a partially initialized array, which by definition, has the uninitialized elements set to NUL. Hence, stg6 is a string.

> > **Takeaway:** The compiler automatically inserts NUL when (i) a double-quoted set of characters is used as the value, or (ii) the array is partially initialized. When assigning an array, there must be room for the NUL to be included.

# ## 13.3 intro2strings.c: DECLARING AND INITIALIZING STRINGS

Program 13.1 demonstrates the techniques of assigning string values to array and pointer variables. It also shows how sizeof computes the size of an array containing a string. Finally, the program runs scanf in a loop to repeatedly assign an array. One of the arrays is not a string, and the output shows the consequences of not using the NUL character when it should have been used.

The program declares and initializes four arrays in four different ways. It also assigns one of the arrays to a pointer. Three of the arrays (stg1, stg2 and stg4) are valid strings because they are terminated—explicitly or implicitly—by NUL. However, stg3 is not a valid string. Observe that sizeof doesn't return the string length but the number of bytes used by the array in memory.

Printing of stg3 has created problems on this machine. printf failed to stop after printing char, but intruded into the territory used by stg2 to print double as well. You may not get the same output, but the output would still be unpredictable because there's no guarantee that printf will find NUL at the end of the character sequence.

Finally, scanf runs in a loop to read multiple words and assign each word in turn to stg1. To read a line as a single string, scanf needs to use the scan set (9.11.1), but the fgets function (13.4.3) also does the job. We'll use both techniques in this chapter.
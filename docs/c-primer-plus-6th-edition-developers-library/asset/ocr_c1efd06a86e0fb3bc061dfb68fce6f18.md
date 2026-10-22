Now let’s take a more detailed look at the selection sort. Here is an outline in pseudocode:

```
for n = first to n = next-to-last element,
    find largest remaining number and place it in the nth element
```

The plan works like this: First, start with n = 0. Scan the entire array, find the largest number, and swap it with the first element. Next, set n = 1 and then scan all but the first element of the array. Find the largest remaining number and swap it with the second element. Continue this process until reaching the next-to-last element. Now only two elements are left. Compare them and place the larger in the next-to-last position. This leaves the smallest element of all in the final position.

It looks like a for loop task, but we still have to describe the “find and place” process in more detail. One way to select the largest remaining value is to compare the first and second elements of the remaining array. If the second is larger, swap the two values. Now compare the first element with the third. If the third is larger, swap those two. Each swap moves a larger element to the top. Continue this way until you have compared the first with the last element. When you finish, the largest value is now in the first element of the remaining array. You have sorted the array for the first element, but the rest of the array is in a jumble. Here is the procedure in pseudocode:

```
for n - second element to last element,
    compare nth element with first element; if nth is greater, swap values
```

This process looks like another for loop. It will be nested in the first for loop. The outer loop indicates which array element is to be filled, and the inner loop finds the value to put there. Putting the two parts of the pseudocode together and translating them into C, we get the function in Listing 11.29. Incidentally, the C library includes a more advanced sorting function called qsort(). Among other things, it uses a pointer to a function to make the sorting comparison. Chapter 16, “The C Preprocessor and the C Library,” gives examples of its use.

# The ctype.h Character Functions and Strings

Chapter 7, “C Control Statements: Branching and Jumps,” introduced the ctype.h family of character-related functions. These functions can’t be applied to a string as a whole, but they can be applied to the individual characters in a string. Listing 11.30, for example, defines a function that applies the toupper() function to each character in a string, thus converting the whole string to uppercase. It also defines a function that uses ispunct() to count the number of punctuation characters in a string. Finally, the program uses strchr(), as described earlier, to handle the newline, if any, in the string read by fgets().

# Listing 11.30 The mod_str.c Program

```
/* mod_str.c -- modifies a string */
#include <stdio.h>
#include <string.h>
```
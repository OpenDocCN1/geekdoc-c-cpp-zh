```
Your name of 11 letters occupies 40 memory cells.
The phrase of praise has 31 letters and occupies 32 memory cells.
```

See what happens. The array name has 40 memory cells, and that is what the sizeof operator reports. Only the first 11 cells are needed to hold Serendipity, however, and that is what strlen() reports. The twelfth cell in the array name contains the null character, and its presence tells strlen() when to stop counting. Figure 4.4 illustrates this concept with a shorter string.

![](bbox=[0.18, 0.31, 0.82, 0.46])

Figure 4.4 The strlen() function knows when to stop.

When you get to PRAISE, you find that strlen() again gives you the exact number of characters (including spaces and punctuation) in the string. The sizeof operator gives you a number one larger because it also counts the invisible null character used to end the string. The program didn’t tell the computer how much memory to set aside to store the phrase. It had to count the number of characters between the double quotes itself.

As mentioned in Chapter 3, “Data and C,” the C99 and C11 standards use a %zd specifier for the type used by the sizeof operator. This also applies for type returned by strlen(). For earlier versions of C you need to know the actual type returned by sizeof and strlen(); typically that would be unsigned or unsigned long.

One other point: The preceding chapter used sizeof with parentheses, but this example doesn’t. Whether you use parentheses depends on whether you want the size of a type or the size of a particular quantity. Parentheses are required for types but are optional for particular quantities. That is, you would use sizeof(char) or sizeof(float) but can use sizeof name or sizeof 6.28. However, it is all right to use parentheses in these cases, too, as in sizeof (6.28).

The last example used strlen() and sizeof for the rather trivial purpose of satisfying a user’s potential curiosity. Actually, however, strlen() and sizeof are important programming tools. For example, strlen() is useful in all sorts of character-string programs, as you’ll see in Chapter 11.

Let’s move on to the #define statement.
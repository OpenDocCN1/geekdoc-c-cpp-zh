```
stop = get_long();
while (start != 0 || stop != 0)
{
    if (bad_limits(start, stop, MIN, MAX))
        printf("Please try again.\n");
    else
    {
        answer = sum_squares(start, stop);
        printf("The sum of the squares of the integers ");
        printf("from %ld to %ld is %g\n", start, stop, answer);
    }
    printf("Enter the limits (enter 0 for both "
           "limits to quit):\n");
    printf("lower limit: ");
    start = get_long();
    printf("upper limit: ");
    stop = get_long();
}
```

# The Input Stream and Numbers

When writing code to handle bad input, such as that used in Listing 8.7, you should have a clear picture of how C input works. Consider a line of input like the following:

```
is 28 12.4
```

To our eyes, it looks like a string of characters followed by an integer followed by a floating-point value. To a C program it looks like a stream of bytes. The first byte is the character code for the letter i, the second is the character code for the letter s, the third is the character code for the space character, the fourth is the character code for the digit 2, and so on. So if get_long() encounters this line, which begins with a nondigit, the following code reads and discards the entire line, including the numbers, which just are other characters on the line:

```
while ((ch = getchar()) != '\n')
    putchar(ch); // dispose of bad input
```

Although the input stream consists of characters, the scanf() function can convert them to a numeric value if you tell it to. For example, consider the following input:

```
42
```

If you use scanf() with a %c specifier, it will just read the 4 character and store it in a char variable. If you use the %s specifier, it will read two characters, the 4 character and the 2 character, and store them in a character string. If you use the %d specifier, scanf() reads the same two characters, but then proceeds to calculate that the integer value corresponding to them is 4 × 10 + 2, or 42. It then stores the integer binary representation of that value in an int variable. If you use an %f specifier, scanf() reads the two characters, calculates that they correspond to
```
ch = getchar();        /* read next character */
while (getchar() != '\n')
    continue;          /* skip rest of line */
return ch;
}
```

# Mixing Character and Numeric Input

Creating menus provides another illustration of how mixing character input with numeric input can cause problems. Suppose, for example, the count() function (choice c) were to look like this:

```
void count(void)
{
    int n,i;

    printf("Count how far? Enter an integer:\n");
    scanf("%d", &n);
    for (i = 1; i <= n; i++)
        printf("%d\n", i);
}
```

If you then responded by entering 3, scanf() would read the 3 and leave a newline character as the next character in the input queue. The next call to get_choice() would result in get_first() returning this newline character, leading to undesirable behavior.

One way to fix that problem is to rewrite get_first() so that it returns the next non-whitespace character rather than just the next character encountered. We leave that as an exercise for the reader. A second approach is having the count() function tidy up and clear the newline itself. This is the approach this example takes:

```
void count(void)
{
    int n,i;

    printf("Count how far? Enter an integer:\n");
    n = get_int();
    for (i = 1; i <= n; i++)
        printf("%d\n", i);
    while ( getchar() != '\n')
        continue;
}
```

This function also uses the get_long() function from Listing 8.7, but changes it to get_int() to fetch type int instead of type long; recall that the original checks for valid input and gives the user a chance to try again. Listing 8.8 shows the final menu program.
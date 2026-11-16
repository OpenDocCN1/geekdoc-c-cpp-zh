# Arrays of Character Strings

Consider the following array declaration:

```
char name[5][10] = { "Bailey", "Beatty", "Mace", "Miller", "Zedon" };
```

that sets up a rectangular two dimensional array of 5 rows each of length 10 columns. Note that it is necessary for us to declare a row's length large enough to at least hold the largest name:

![](bbox=[0.052, 0.31, 0.883, 0.473])

As you can see, this is a great waste of storage. Fortunately, C gives us the ability to declare an array with each row's length determined by the string it's initialized to:

```
char *name[] = { "Bailey", "Beatty", "Mace", "Miller", "Zedon" };
```

Here, name is an array of 5 pointers to character strings. Each character string is an array of characters, so we have 5 pointers to arrays:

![](bbox=[0.052, 0.69, 0.883, 0.891])
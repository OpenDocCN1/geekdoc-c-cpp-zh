Now some code:

```
// caps2.c
while ((c = getchar()) != EOF) {
    if (isspace(c)) {
        putchar(c);
    } else {
        putchar(toupper(c));
        while (isspace(c = getchar())) {
            putchar(c);
        }
        putchar(c);
    }
}
```

Let's see if we can redesign this algorithm and code:

First the algorithm:

```
// caps3.c
for each input character c
    if c is the first letter of a word
        output capitalized c
    else
        output c
```

Now the code:

```
// caps4.c
for (wasWhite = 1; (c = getchar()) != EOF; wasWhite = isspace(c)) {
    putchar (!isspace(c) && wasWhite ? toupper(c) : c);
}
```

Note that this redesign results in a simpler program.
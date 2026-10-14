![](bbox=[0.04, 0.02, 0.82, 0.15])

The 100 bytes of memory (not all of which are shown) pointed to by line are those allocated by malloc. (They are brand-new memory, conceptually a bit different from the memory which the compiler arranges to have allocated automatically for our conventional variables. The 100 boxes in the figure don't have a name next to them, because they're not storage for a variable we've declared.)

As a second example, we might have occasion to allocate a piece of memory, and to copy a string into it with strcpy:

```
char *p = (char *)malloc(15);
```

```
/* incomplete -- malloc's return value not checked */
strcpy(p,"Hello, world!");
```

When copying strings, remember that all strings have a terminating \0 character. If you use strlen to count the characters in a string for you, that count will not include the trailing \0, so you must add one before calling malloc:

```
char *somestring, *copy;
...
copy = (char *)malloc(strlen(somestring) + 1); /* +1 for \0 */
/* incomplete -- malloc's return value not checked */
strcpy(copy, somestring);
```
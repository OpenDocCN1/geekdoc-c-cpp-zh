# Release 4

```
char *first, *last;
char *fullname;

fullname = malloc(strlen(first)+strlen(last)+2);
strcpy(fullname, first);
strcat(fullname, ".");
strcat(fullname, last);
```

Release 4 worked fine in system tests. In the field, though, it was run on a machine with a very small memory and crashed when malloc() failed, returning NULL.

# Release 5

```
char *first, *last;
char *fullname;

fullname = malloc(strlen(first) + strlen(last) + 2);
if (fullname == NULL)
    error();
strcpy(fullname, first);
strcat(fullname, ".");
strcat(fullname, last);
```

Release 5 no longer crashes. However, it gradually eats up memory when it is running for long enough.

Another huge debugging effort finds the problem, fixed in Release 6.
in an apparently unrelated part of the system.

# Introduction-

This Chapter lists the common C programming errors that the author sees time and time again. Solutions to the errors are also presented.

# 2. Beginner Errors-

These are errors that beginning C students often make. However, the professionals still sometimes make them too!

# 2.1 Forgetting to put a break in a switch statement.

Remember that C does not break out of a switch statement if a case is encountered.

# For example:

```
int x = 2;
switch(x) {
case 2:
    printf("Two\n");
case 3:
    printf("Three\n");
}
```

# Output:

Two
Three

# Put a break to break out of the switch:

```
int x = 2;
switch(x) {
case 2:
    printf("Two\n");
    break;
case 3:
    printf("Three\n");
    break; /* not necessary, but good if additional cases are added later */
}
```

# 2.2 Using = instead of ==

C's = operator is used exclusively for assignment and returns the value assigned. The == operator is used exclusively for comparison and returns an integer value (0 for false, not 0 for true). Because of these return values, the C compiler often does not flag an error when = is used when one really wanted an ==.
The conditional statement is very useful for shortening programs. We can rewrite the following if-else statement:

```
if (x > y) {
    printf("%d\n", x);
} else {
    printf("%d\n", y);
}
```

as

```
printf("%d\n", x > y ? x : y);
```

In the following statement:

```
num = value > 0 ? ++x : ++y;
```

only one of the expressions, either ++x or ++y gets evaluated, but never both!

Two functions are shown below using the conditional operator. Note that they also use functions from the ctype.h library:

```
// convert lower case to upper case
char toUpper(char c) {
    return islower(c) ? c - 32 : c);
}

// convert upper case to lower case
char toLower(char c) {
    return isupper(c) ? c + 32 : c);
}
```
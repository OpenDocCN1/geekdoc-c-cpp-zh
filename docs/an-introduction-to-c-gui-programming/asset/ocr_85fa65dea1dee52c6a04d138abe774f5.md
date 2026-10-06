```
int a[10] = { 0, 11, 22, 33, 44, 55, 66, 77, 88, 99 };
```

Note here that this only works when the array is first declared, once it exists, you can't use this shortcut and will need to iterate through the array indices, setting each value in turn

![](bbox=[0.036, 0.24, 0.866, 0.375])

![](bbox=[0.036, 0.435, 0.866, 0.545])

# Strings

In C, a string is just another array, it is an array of single characters. As we saw in chapter 2, a character is a specific type in C called char holds a single byte, which is enough to hold an alphanumeric character. A string with ten characters would be:

```
char mystery[10];
```

Or, to initialise it at the same time:

```
char mystery[10] = "thestring";
```

One important thing to remember is that a string in C must always end with a byte set to zero, and that the memory required to hold this final zero (called the string terminator) must be allocated when you declare the string So mystery, which is declared as an array of ten chars, can only hold text of nine or fewer letters.
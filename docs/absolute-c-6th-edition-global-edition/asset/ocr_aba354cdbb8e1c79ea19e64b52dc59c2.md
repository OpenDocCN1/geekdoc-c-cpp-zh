# EXAMPLE: (continued)

If your program intends to use the contents of argv, then it should verify that arguments were actually input by ensuring that argc is appropriately set. Otherwise, your program may produce incorrect results when accessing argv.

# Self-Test Exercises

1. Which of the following declarations are equivalent?

```
char stringVar[10] = "Hello";
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
char stringVar[10] = {"H", "e", "l", "l", "o"};
char stringVar[6] = "Hello";
char stringVar[] = "Hello";
```

2. What C-string will be stored in singingString after the following code is run?

char singingString[20] = "DoBeDo";
strcat(singingString, " to you");

Assume that the code is embedded in a complete program and that an include directive for <cstring> is in the program file.

3. What (if anything) is wrong with the following code?

char stringVar[] = "Hello";
strcat(stringVar, " and Good-bye.");
cout << stringVar;

Assume that the code is embedded in a complete program and that an include directive for <cstring> is in the program file.

4. Suppose the function strlen (which returns the length of its string argument) was not already defined for you. Give a function definition for strlen. Note that strlen has only one argument, which is a C-string. Do not add additional arguments; they are not needed.
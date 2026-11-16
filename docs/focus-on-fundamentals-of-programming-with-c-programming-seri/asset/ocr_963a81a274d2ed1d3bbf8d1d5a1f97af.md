then the very next line in your program should contain the following statement:

```
```
fprintf(fp, "Hello, world.\n");
```
```

Likewise, if your program contains the following type of printf() statement:

```
```
printf("The sum equals %d\n", sum);
```
```

then the very next line in your program should contain the following statement:

```
```
fprintf(fp, "The sum equals %d\n", sum);
```
```

In each case, the fprintf() statement will cause the identical output to be sent to the csis.txt output file.

+   - Finally, the statement in main() just before the return statement should be:

```
```
fclose(fp);
```
```

This statement will close the csis.txt data file before the program completes execution.

Note that fopen() is the traditional ANSI C function used to work with files and is used in a Mac, Linux, or other non-Microsoft environment. However, as most students typically use Microsoft's Visual Studio environment, the text will utilize Microsoft's more secure fopen_s() function.
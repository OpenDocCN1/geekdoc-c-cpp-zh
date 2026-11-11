The system usually provides two blank spaces between the numbers. However, this can be increased by selecting a suitable field width for the numbers or by introducing a 'tab' character between the specifications. For example, the statement

```
````c
printf("a = %d\t b = %d", a, b);
````
```

will provide four blank spaces between the two fields. We can also print them on two separate lines by using the statement

```
````c
printf("a = %d\n b = %d", a, b);
````
```

Messages and headings can be printed by using the character strings directly in the printf statement. Examples:

```
````c
printf("\n OUTPUT RESULTS \n");
printf("Code\t Name\t Age\n");
printf("Error in input data\n");
printf("Enter your name\n");
````
```

# ## LEARNING OUTCOMES

+   - While using getchar function, care should be exercised to clear any unwanted characters in the input stream. LO 6.1
+   - Do not forget to include <stdio.h> headerfile when using functions from standard input/output library. LO 6.1
+   - Do not forget to include <ctype.h> header file when using functions from character handling library. LO 6.2
+   - Provide proper field specifications for every variable to be read or printed. LO 6.3
+   - Enclose format control strings in double quotes. LO 6.3
+   - Do not forget to use address operator & for basic type variables in the input list of scanf. LO 6.3
+   - Do not specify any precision in input field specifications. LO 6.3
+   - Do not provide any white-space at the end of format string of a scanf statement. LO 6.3
+   - Do not use commas in the format string of a scanf statement. LO 6.3
+   - Use double quotes for character string constants. LO 6.4
+   - Use single quotes for single character constants. LO 6.4
+   - Provide sufficient field width to handle a value to be printed. LO 6.4
+   - Be aware of the situations where output may be imprecise due to formatting. LO 6.4
+   - Do not forget to close the format string in the scanf or printf statement with double quotes. LO 6.4
+   - Using an incorrect conversion code for data type being read or written will result in runtime error. LO 6.4
+   - Do not forget the comma after the format string in scanf and printf statements. LO 6.4
+   - Not separating read and write arguments is an error. LO 6.4
+   - Using an address operator & with a variable in the printf statement will result in runtime error. LO 6.4

# ## KEY TERMS TO REMEMBER

+   - getchar: Reads one character from standard input. LO 6.1
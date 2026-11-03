The reason you see incorrect output is that scanf() is very specific. It fetches only the variable type specified by the conversion character. So if you want a floating-point value, you must specify a float variable and use the appropriate conversion character; %f, in this case.

Exercise 7-15: Modify the source code from Listing 7-6 so that a floating-point number is requested, input, and displayed.

![](bbox=[0.12, 0.3, 0.22, 0.45])

+   - You don't need to prefix a char array variable with an ampersand in the scanf() function; when using scanf() to read in a string, just specify the string variable name.
+   - The scanf() function stops reading text input at the first whitespace character, space, tab, or Enter key.

# Using fgets() for text input

For a general-purpose text input function, one that reads beyond the first whitespace character, I recommend the fgets() function. Like most of the other text I/O functions, it's prototyped in the stdio.h header file. Here's the format:

```
char * fgets(char *restrict s, int n, FILE *restrict stream);
```

Frightening, no? The fgets() function is a file function, which reads text from a file, as in “file get string.” That’s how programmers talk after an all-nighter.

File functions are covered in Chapter 22, but because the operating system considers standard input like a file, you can use fgets() to read text from the keyboard.

Here's a simplified version of the fgets() function as it applies to reading text input:

```
fgets(string,size,stdin);
```

In this example, string is the name of a char array, a string variable; size is the number of characters to input plus one for the null character. Effectively, the size value is the same size as the char array. The final argument is the stdin constant, the name of the standard input device as defined in the stdio.h header file.
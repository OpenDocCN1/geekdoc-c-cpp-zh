# Line Input

The line-input functions read a line from an input stream—they read all characters up to the next newline character. The standard library has two line input functions, gets() and fgets().

# The gets() Function

You were introduced to the gets() function in Lesson 10, “Working with Characters and Strings.” This is a straightforward function, reading a line from stdin and storing it in a string. The function prototype is

```
char *gets(char *str);
```

You probably interpret this prototype by yourself. gets() takes a pointer to type char as its argument and returns a pointer to type char. The gets() function reads characters from stdin until a newline(\n) or end-of-file is encountered; the newline is replaced with a null character, and the string is stored at str.

The return value is a pointer to the string (the same as str). If gets() encounters an error or an end-of-file before any input, a null pointer is returned.

Before calling gets(), you must allocate sufficient memory space to store the string, using the methods covered in Lesson 10. This function has no way of knowing space pointed to by str is allocated; the string is input and stored starting at str in either case. If the space hasn’t been allocated, the string might overwrite other data and cause program errors.

Listings 10.5 and 10.6 gets().

# The fgets() Function

The fgets() library is similar to gets() in that it reads a line of text from an input stream. It is more flexible because it lets the programmer specify the specific input stream to use and the maximum number of characters to be input. The fgets() function is often used to input text from disk files, covered in Lesson 17. To use it for input, you specify stdin as the input stream. The prototype of fgets() is

```
char *fgets(char *str, int n, FILE *fp);
```

The last parameter, FILE *fp, is used to specify the input stream. For now, specify the standard input stream, stdin, as the stream argument.

The pointer str indicates where the input string is stored. The argument n specifies the maximum number of characters to be input. The fgets() function reads characters from the input stream until a newline or end-of-file is encountered or n-1 characters are read. The newline is included in the string and terminated with a \0 before it is stored. The return values of fgets() are the same as described earlier for gets().
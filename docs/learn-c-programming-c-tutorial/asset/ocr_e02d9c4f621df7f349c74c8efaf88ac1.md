| Mode | Description |
|---|---|
| `a+` | Opens a text file for both reading and writing. It creates the file if it does not exist. The reading will start from the beginning but writing can only be appended. |

If you are going to handle binary files, then you will use the following access modes instead of the above-mentioned ones:

```
```text
"rb", "wb", "ab", "rb+", "r+b", "wb+", "w+b", "ab+", "a+b"
```
```

# Closing a File

To close a file, use the fclose( ) function. The prototype of this function is:

```
```c
int fclose( FILE *fp );
```
```

The **fclose()** function returns zero on success, or **EOF** if there is an error in closing the file. This function actually flushes any data still pending in the buffer to the file, closes the file, and releases any memory used for the file. The EOF is a constant defined in the header file **stdio.h**.

There are various functions provided by C standard library to read and write a file, character by character, or in the form of a fixed length string.

# Writing a File

Following is the simplest function to write individual characters to a stream:

```
```c
int fputc( int c, FILE *fp );
```
```

The function **fputc()** writes the character value of the argument c to the output stream referenced by fp. It returns the written character written on success otherwise **EOF** if there is an error. You can use the following functions to write a null-terminated string to a stream:

```
```c
int fputs( const char *s, FILE *fp );
```
```

The function **fputs()** writes the string s to the output stream referenced by fp. It returns a non-negative value on success, otherwise **EOF** is returned in case of any error. You can use **int fprintf(FILE *fp,const char *format, ...)** function as well to write a string into a file. Try the following example.

Make sure you have **/tmp** directory available. If it is not, then before proceeding, you must create this directory on your machine.

```
```c
#include <stdio.h>
```
```

## Creating a file

A special data type for handling files is defined in the stdio.h header file. It is called a “file pointer” and has the syntax FILE *fp. File pointers are used to open, read, write, and close files. In a C program, a file pointer called “file_ptr” can be created with the declaration FILE *file_ptr ;

![](img/db19f3858a1e321646bf2590afd29547_202_0.png)

A file pointer points to a structure defined in the stdio.h header file that contains information about the file. This includes details about the current character and if the file is being read or written.

Before a file can be read or written it firstly must always be opened with the fopen() function. This takes two arguments to specify the name and location of the file, and a “mode” in which to open the file. The fopen() function returns a file pointer if successful, or a NULL value upon failure.

Once a file has been successfully opened it can be read or added to, or new text can be written in the file, depending on the mode specified in the call to the fopen() function. Following this, the open file must then always be closed by calling the fclose() function and specifying the file pointer as its single argument.

The table below lists all the possible file modes that can be specified as the second argument to the fopen() function:

| File mode | Operation |
|---|---|
| r | Open an existing file to read |
| w | Open an existing file to write. Creates a new file if none exists, or opens an existing file and discards all its previous contents |
| a | Appends text. Opens or creates a text file for writing at the end of the file |
| r+ | Opens a text file to read from or write to |
| w+ | Opens a text file to write or read from |
| a+ | Opens or creates a text file to read from or write to at the end of the file |

Note: Where the mode includes a b after any of the file modes listed above, the operation relates to a binary file rather than a text file – for example, rb or wb

All the standard functions for file input/output are contained in the stdio.h header file.

For convenience, all the text files in the examples in this chapter are located in the MyPrograms folder that also contains the C source code files. On Windows the directory is c:\MyPrograms, and on Linux systems it's at /home/MyPrograms.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_203_0.png)

- 2. Add a main function that declares a file pointer

```
int main()
{
FILE *file_ptr ;
}
```

- 3. Next, in the main function block, attempt to create a file for writing to

```
file_ptr = fopen( "data.txt", "w" );
```

- 4. Now, output a message to confirm the attempt succeeded, then close the file and return a zero integer value as required by the function declaration

```
if(file_ptr != NULL)
{
    printf( "File created\n" );
    fclose( file_ptr );
    return 0 ;
}
```

- 5. Finally, output an alternative message if the attempt fails

```
else
{
    printf( "Unable to create file\n" ); return 1 ;
}
```

- 6. Save the program file, then compile and execute the program to attempt to create a text file

![](img/db19f3858a1e321646bf2590afd29547_204_0.png)

![](img/db19f3858a1e321646bf2590afd29547_204_1.png)

Notice that both file name and file mode arguments must be enclosed within double quotes.

![](img/db19f3858a1e321646bf2590afd29547_204_2.png)

Notice that this program returns a value of 1 to the system when the attempt to open the file fails – this tells the system that all did not go well.

## Reading & writing characters

### Standard input

The **scanf()** function, used in previous examples, is the simplified version of a function named **fscanf()** that requires an input filestream as its first argument. This indicates a source from where a series of characters will be introduced into the program.

In C programming, the filestream named **stdin** represents the keyboard and is the default source for the **scanf()** function. The function call **scanf(...)** is the same as **fscanf( stdin, ... )** .

### Standard output

Similarly, the **printf()** function is the simplified version of a function named **fprintf()** that requires an output filestream as its first argument. This indicates a destination where a series of characters will be output from the program.

The filestream named **stdout** represents the monitor, and is the default source for the **printf()** function. The function call **printf(...)** is the same as **fprintf( stdout, ... )** .

Other standard functions, which have **stdin** or **stdout** as their default filestreams, also have equivalents allowing an alternative filestream to be specified. These can be used to read files by specifying a file pointer as an alternative to reading from the **stdin** filestream. They can also be used to write files by specifying an alternative to the **stdout** filestream:

- The **fputc()** function can be used to write to a filestream one character at a time – typically by looping through a **char** array. Its companion **fgetc()** can be used to read from a filestream one character at a time.
- The **fputs()** function can be used to write to a filestream one line at a time, and its companion **fgets()** can be used to read from a filestream one line at a time.
- The **fread()** function can be used to read an entire filestream, and its partner **fwrite()** can write an entire filestream.
- The **fscanf()** function and the **fprintf()** functions can be used to read and write filestreams with strings and numbers.

![](img/db19f3858a1e321646bf2590afd29547_207_0.png)

Another standard output filestream named stderr is used to output error messages.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_207_1.png)

writechars.c

- 2. Add a main function that declares a file pointer, a loop counter variable, and an initialized character array

```
int main()
{
    FILE *file_ptr ; int i ;
    char text[50] = { "Text, one character at a time." } ;
}
```

- 3. Next, in the main function block, attempt to create a file for writing to

```
file_ptr = fopen( "chars.txt" , "w" ) ;
```

- 4. Now, output a message to confirm the attempt succeeded, write each character from the array, then close the file and return the required zero integer value

```
if( file_ptr != NULL )
{
    printf( "File chars.txt created\n" ) ;
    for( i = 0 ; text[i] ; i++ ) { fputc( text[i], file_ptr ) ; }
    fclose( file_ptr ) ;
    return 0 ;
}
```

- 5. Finally, output an alternative message if the attempt fails

```
else { printf( "Unable to create file\n" ) ; return 1 ; }
```

- 6. Save the program file, then compile and execute the program to attempt to write a text file

![](img/db19f3858a1e321646bf2590afd29547_208_0.png)

![](img/db19f3858a1e321646bf2590afd29547_208_1.png)

![](img/db19f3858a1e321646bf2590afd29547_208_2.png)

The fputc() function returns the ASCII code of the current character, or a constant called EOF denoting that the end of the file is reached.

## Reading & writing lines

The fgetc() function is not the most efficient way to read text into a program, as it must be called repeatedly to read each character. It is better to employ the fgets() function that reads text one whole line at a time.

The fgets() function requires three arguments. The first argument specifies a char pointer or char array to which the text will be assigned. The second argument must be an integer specifying the maximum number of characters to read per line. The third argument is a file pointer specifying where to read from.

Similarly, the fputc() function, which writes text one character at a time, is less efficient than the fputs() function that writes text line by line. The fputs() function requires two arguments to specify the text to write and a file pointer denoting the file to be written to. A newline character is added by fputs() after the line is written. This function returns zero when successful, or the EOF constant when an error occurs or the end of the file is reached.

![](img/db19f3858a1e321646bf2590afd29547_209_0.png)

lines.c

- 1. Begin a new program with a preprocessor instruction to include the standard input/output and string functions

```
#include <stdio.h>
#include <string.h>
```

- 2. Add a main function that declares a file pointer and an uninitialized character array

```
int main()
{
FILE *file_ptr ;
char text[50] ;
}
```

- 3. Next, in the main function block, attempt to open a local text file for both reading and appending to

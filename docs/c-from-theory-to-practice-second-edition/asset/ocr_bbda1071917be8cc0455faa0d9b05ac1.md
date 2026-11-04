Comments: This code is reliable with the assumption that the failure reason of fopen() is that the file does not exist, not some other reason. Also, we assume that no other running application will create the file in the time interval between checking and creating the file.

# Read Data from a Text File

The most common functions to read data from a text file are: fscanf(), fgets(), and fgetc(). These functions are mostly used with text files; however, we can use them to read data from binary files as well.

> For simplicity, we assume that if the function we used to read data returns EOF, it is because the end of file is reached, not because of a read error. However, a robust program should check the reason for failure.

# The fscanf() Function

The fscanf() function is used to read a variable number of different data items from an input file. Like scanf(), fscanf() uses a format string to define the order and the type of data that will be read from the file. It is declared in stdio.h

```
int fscanf(FILE* fp, const char *format, ...);
```

The only difference between them is that scanf() always reads from stdin, while fscanf() reads from the file indicated by fp.

As discussed, the operating system (e.g., Unix) may allow the redirection of stdin. For example, if the name of the executable is test and we write in the command line:

```
test <input.txt
```

the input read from stdin (e.g., with scanf()) won't be read from the keyboard, but from the input.txt file. Also, we can combine both redirections. For example:

```
test <input.txt >output.txt
```

fscanf() returns the number of data items successfully read from the file and assigned to program variables. If either the end of file is reached or the read operation fails, it returns EOF. Later, we'll see that we can use feof() to determine which one happened. The following program assumes that the test.txt text file contains the annual temperatures in an area. It reads them and displays those within [-5, 5].

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
```
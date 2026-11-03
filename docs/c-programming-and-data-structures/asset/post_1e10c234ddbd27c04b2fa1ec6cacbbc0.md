
ftell would give the relative offset (in bytes) of the current position. This means that n bytes have already been read (or written).

rewind takes a file pointer and resets the position to the start of the file. For example, the statement

```
rewind(fp);
 n = ftell(fp);
```

would assign 0 to n because the file position has been set to the start of the file by rewind. Remember, the first byte in the file is numbered as 0, second as 1, and so on. This function helps us in reading a file more than once, without having to close and open the file. Remember that whenever a file is opened for reading or writing, a rewind is done implicitly.

fseek function is used to move the file position to a desired location within the file. It takes the following form:

```
fseek(file_ptr, offset, position);
```

file_ptr is a pointer to the file concerned, offset is a number or variable of type long, and position is an integer number. The offset specifies the number of positions (bytes) to be moved from the location specified by position. The position can take one of the following three values:

| Value | Meaning |
|---|---|
| 0 | Beginning of file |
| 1 | Current position |
| 2 | End of file |

The offset may be positive, meaning move forwards, or negative, meaning move backwards. Examples in Table 8.2 illustrate the operations of the fseek function:

## Table 8.2 Operations of fseek Function

| Statement | Meaning |
|---|---|
| fseek(fp,0L,0); | Go to the beginning. (Similar to rewind) |
| fseek(fp,0L,1); | Stay at the current position. (Rarely used) |
| fseek(fp,0L,2); | Go to the end of the file, past the last character of the file. |
| fseek(fp,m,0); | Move to (m+1)th byte in the file. |
| fseek(fp,m,1); | Go forward by m bytes. |
| fseek(fp,-m,1); | Go backward by m bytes from the current position. |
| fseek(fp,-m,2); | Go backward by m bytes from the end. (Positions the file to the mth character from the end.) |

When the operation is successful, fseek returns a zero. If we attempt to move the file pointer beyond the file boundaries, an error occurs and fseek returns -1 (minus one). It is good practice to check whether an error has occurred or not, before proceeding further.

## EXAMPLE 8.5 Write a program that uses the functions ftell and fseek.

![](img/fe6da5f61b1e2c77309bbee135b45e35_423_0.png)

We are reading the file twice. First, we are reading the content of every fifth position and printing its value along with its position on the screen. The second time, we are reading the contents of the file from the end and printing the same on the screen.

During the first reading, the file pointer crosses the end-of-file mark when the parameter n of fseek(fp,n,0) becomes 30. Therefore, after printing the content of position 30, the loop is terminated.

For reading the file from the end, we use the statement fseek(fp, -1L, 2); to position the file pointer to the last character. Since every read causes the position to move forward by one position, we have to move it back by two positions to read the next character. This is achieved by the function fseek(fp, -2L, 1); in the while statement. This statement also tests whether the file pointer has crossed the file boundary or not. The loop is terminated as soon as it crosses it.

```
Program
#include <stdio.h>
main()
{
    FILE *fp;
    long n;
    char c;
    fp = fopen("RANDOM", "w");
    while((c = getchar()) != EOF)
        putc(c,fp);
    printf("No. of characters entered = %ld\n", ftell(fp));
    fclose(fp);
    fp = fopen("RANDOM","r");
    n = 0L;
    while(feof(fp) == 0)
    {
        fseek(fp, n, 0);  /* Position to (n+1)th character */
        printf("Position of %c is %ld\n", getc(fp),ftell(fp));
        n = n+5L;
    }
    putchar('\n');
    fseek(fp,-1L,2);   /* Position to the last character */
    do
    {
        putchar(getc(fp));
    }
    while(!fseek(fp,-2L,1));
    fclose(fp);
}
```

### Output

ABCDEFGHIJKLMNOPQRSTUVWXYZ
No. of characters entered = 26

```
scanf("%d", &response);
} while (response == 1);

n = ftell(fp);   /* Position of last character */
fclose(fp);

fp = fopen(filename, "r");

while(ftell(fp) < n)
{
    fscanf(fp,"%s %d %f %d", &item.name, &item.number, &item.price, &item.quantity);
    fprintf(stdout,"%s %d %.2f %d\n", item.name, item.number, item.price, item.quantity);
}
fclose(fp);
}
void append(struct invent_record *product, FILE *ptr)
{
    printf("Item name:");
    scanf("%s", product->name);
    printf("Item number:");
    scanf("%d", &product->number);
    printf("Item price:");
    scanf("%f", &product->price);
    printf("Quantity:");
    scanf("%d", &product->quantity);
    fprintf(ptr, "%s %d %.2f %d", product->name, product->number, product->price, product->quantity);
}
```

### Output

Type filename:INVENTORY
Item name:XXX
Item number:444
Item price:40.50
Quantity:34
Item XXX appended.
Do you want to add another item(1 for YES /0 for NO)?1
Item name:YYY
Item number:555
Item price:50.50
Quantity:45
Item YYY appended.
Do you want to add another item(1 for YES /0 for NO)?0

AAA-1    111    17.50    115
BBB-2    125    36.00    75
C-3      247    31.75    104
XXX      444    40.50    34
YYY      555    50.50    45

## Just Remember

- Do not try to use a file before opening it.
- Remember, when an existing file is open using ‘w’ mode, the contents of file are deleted.
- When a file is used for both reading and writing, you must open it in ‘w+’ mode.
- EOF is integer type with a value –1. Therefore, we must use an integer variable to test EOF.
- It is an error to omit the file pointer when using a file function.
- It is an error to open a file for reading when it does not exist.
- It is an error to try to read from a file that is in write mode and vice versa.
- It is an error to attempt to place the file marker before the first byte of a file.
- It is an error to access a file with its name rather than its file pointer.
- It is a good practice to close all files before terminating a program.
- Use getw and putw for reading and writing an integer to a file.
- You must choose an appropriate file access mode depending upon the type of file operation that you want to perform.
- It is always advisable to implement an error-handling mechanism through the use of ferror function.
- Use the fseek function to move to any desired location in a file.

## Multiple Choice Questions

1. Which of the following tasks are not performed by the fopen function?
(a) Creating a new file which does not already exist
(b) Opening an existing file
(c) Deleting the existing file and creating a new one with the same name
(d) Opening an existing file in append mode

2. Which of the following is true for getc function?
(a) Read a string from the file
(b) Read a character from the file
(c) Read a character from the console
(d) Read a string from the console

3. Which of the following tasks are performed by the rewind function?
(a) Set the file pointer to the end of the file
(b) Set the file pointer to the beginning of the file
(c) Set the file pointer to any desired position in the file
(d) Erase all the file contents and place the file pointer at the beginning

4. Which of the following are not i/o functions in C?
(a) fscanf      (b) fseek
(c) fget        (d) forward

5. What is the functionality of a+ file access mode?
(a) Open the file for appending data to it
(b) Open the file in read-write mode for appending data to it
(c) Append the contents of one file into another
(d) None of the above

6. Which of the following is true for putc?
(a) Put one character at a time into the file
(b) Put one string at a time into the file
(c) Put one character at a time into the console
(d) Put one string at a time into the console

7. Which of the following functions is used to read an integer value from a file?
(a) getw      (b) getc
(c) gets      (d) geti

## Review Questions

8. Which of the following file-handling functions is analogous to the standard i/o function printf?
(a) fprintf
(b) fprint
(c) fprints
(d) fprintfline

9. What will the function call fseek(fp,m,0) do?
(a) Move to the mth byte in the file
(b) Move to the (m-1)th byte in the file
(c) Move to the (m+1)th byte in the file
(d) Move to a location which is m positions ahead of the current file pointer position

10. Command line functions are:
(a) Passed at run time
(b) Passed at compile time
(c) Passed to the main function during preprocessing of the program
(d) Passed during dynamic memory allocation

11. End of file is represented by which of the following?
(a) eof
(b) EOF
(c) '/0'
(d) Any garbage value

12. What is the type and value of EOF?
(a) int, 0
(b) int, 1
(c) int, -1
(d) char, 1

13. Which of the following is a commonly used function for error-handling?
(a) ferr
(b) ferror
(c) feof
(d) None of the above

14. Which of the following is not a file access mode?
(a) r+
(b) w+
(c) a-
(d) a+

15. In C, files can be manipulated in which of the following modes?
(a) text
(b) int
(c) binary
(d) All of the above

8.1 State whether the following statements are true or false.
(a) A file must be opened before it can be used.
(b) All files must be explicitly closed.
(c) Files are always referred to by name in C programs.
(d) Using fseek to position a file beyond the end of the file is an error.
(e) Function fseek may be used to seek from the beginning of the file only.

8.2 Fill in the blanks in the following statements.
(a) The mode ______ is used for opening a file for updating.
(b) The function ______ may be used to position a file at the beginning.
(c) The function ______ gives the current position in the file.
(d) The function ______ is used to write data to randomly accessed file.

8.3 Describe the use and limitations of the functions getc and putc.

8.4 What is the significance of EOF?

8.5 When a program is terminated, all the files used by it are automatically closed. Why is it then necessary to close a file during execution of the program?

8.6 Distinguish between the following functions:
(a) getc and getchar
(b) printf and fprintf
(c) feof and ferror

8.7 How does an append mode differ from a write mode?

8.8 What are the common uses of rewind and ftell functions?

8.9 Explain the general format of fseek function?

8.10 What is the difference between the statements rewind(fp); and fseek(fp,0L,0);?

```
FILE *fptr;
fptr = fopen("data", "a+");
```

```
FILE(*p)(void)
```

```
while ( (c = getchar()) != EOF )
putc(c, f1);
```

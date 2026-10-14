
```
if((ifp = fopen("input.dat", "r")) == NULL)
{
printf("can't open file\n");
exit or return
```

You don't have to write these “collapsed" tests if you're not comfortable with them, but you'll see them in other people's code, so you should be able to read them.

## Self Assessment Questions

- 1. The type FILE is predefined in the header file ________.
- 2. We may add a “+” character to the mode string in the fopen function to indicate that we want to both read and write. (True/False)

## 13.3 Closing Files

Although you can open multiple files, there's a limit to how many you can have open at once. If your program will open many files in succession, you'll want to close each one as you're done with it; otherwise the standard I/O library could run out of the resources it uses to keep track of open files. Closing a file simply involves calling fclose with the file pointer as its argument:

```
fclose(fp);
```

Calling fclose arranges that (if the file was open for output) any last, buffered output is finally written to the file, and that those resources used by the operating system (and the C library) for this file are released. If you forget to close a file, it will be closed automatically when the program exits.

## Self Assessment Questions

- 3. Closing a file simply involves calling fclose with the __________ as its argument.
- 4. If you forget to close a file, it will be closed automatically when the program exits. (True/False)

## 13.4 Input/Output Operations on Files

For each of the I/O library functions we've been using so far, there's a companion function which accepts an additional file pointer argument telling it where to read from or write to. The companion function to printf is fprintf, and the file pointer argument comes first. To print a string to the output.dat file we opened in the previous section, we might call

```
fprintf(ofp, "Hello, world!\n");
```

The companion function to getchar is getc, and the file pointer is its only argument. To read a character from the input.dat file we opened in the previous section, we might call

```
int c;
c = getc(ifp);
```

The companion function to putchar is putc, and the file pointer argument comes last. To write a character to output.dat, we could call

```
putc(c, ofp);
```

Our own getline function calls getchar and so always reads the standard input. We could write a companion fgetline function which reads from an arbitrary file pointer:

```
#include <stdio.h>
```

/* Read one line from fp, */
/* copying it to line array (but no more than max chars). */
/* Does not place terminating \n in line array. */
/* Returns line length, or 0 for empty line, or EOF for end-of-file. */

```
int fgetline(FILE *fp, char line[], int max)
{
int nch = 0;
int c;
max = max - 1; /* leave room for '\0' */

while((c = getc(fp)) != EOF)
{
if(c == '\n')
break;
```

```
if(nch < max)
{
line[nch] = c;
nch = nch + 1;
}
if(c == EOF && nch == 0) return EOF;

line[nch] = '\0';
return nch;
}
```

Now we could read one line from ifp by calling char line[MAXLINE];
...
fgetline(ifp, line, MAXLINE);

## Program 13.1: Writing a data to the file

```
#include <stdio.h>
main()
{
FILE *fp;
char stuff[25];
int index;
fp = fopen("TENLINES.TXT","w"); /* open for writing */
strcpy(stuff,"This is an example line.");
for (index = 1; index <= 10; index++)
fprintf(fp,"%s Line number %d\n", stuff, index);
```

```
fclose(fp); /* close the file before ending program */
}
```

## 13.4.1 Predefined Streams

Besides the file pointers which we explicitly open by calling fopen, there are also three predefined streams. stdin is a constant file pointer corresponding to standard input, and stdout is a constant file pointer corresponding to standard output. Both of these can be used anywhere a file pointer is called for; for example, getchar() is the same as getc(stdin) and putchar(c) is the same as putc(c, stdout). The third predefined stream is stderr. Like stdout, stderr is typically connected to the screen by default. The difference is that stderr is not redirected when the standard output is redirected. For example, under Unix or MS-DOS, when you invoke

```
program > filename
```

anything printed to stdout is redirected to the file filename, but anything printed to stderr still goes to the screen. The intention behind stderr is that it is the “standard error output”; error messages printed to it will not disappear into an output file. For example, a more realistic way to print an error message when a file can't be opened would be

```
if((ifp = fopen(filename, "r")) == NULL)
{
    fprintf(stderr, "can't open file %s\n", filename);
    exit or return
}
```

where filename is a string variable indicating the file name to be opened. Not only is the error message printed to stderr, but it is also more informative in that it mentions the name of the file that couldn't be opened.

## Program 13.2: To read a data file input.dat

Suppose you had a data file consisting of rows and columns of numbers:

1 2 34
5 6 78
9 10 112

Suppose you wanted to read these numbers into an array. (Actually, the array will be an array of arrays, or a “multidimensional" array; ) We can write code to do this by putting together several pieces: the fgetline function we just showed, and the getwords function from which each line broken into words. Assuming that the data file is named input.dat, the code would look like this: #define MAXLINE 100

```
#define MAXROWS 10
#define MAXCOLS 10
```

```
int array[MAXROWS][MAXCOLS]; char *filename = "input.dat"; FILE *ifp;
char line[MAXLINE];
char *words[MAXCOLS];
int nrows = 0;
int n; int i;
```

```
ifp = fopen(filename, "r");
if(ifp == NULL)
{
fprintf(stderr,"can't open %s\n", filename); exit(EXIT_FAILURE);
}
```

```
```c
while(fgetline(ifp, line, MAXLINE) != EOF) {

if(nrows >= MAXROWS)

{
    fprintf(stderr, "too many rows\n");
    exit(EXIT_FAILURE);
}

n = getwords(line, words, MAXCOLS);

for(i = 0;i < n;i++)
    array[nrows][i] = atoi(words[i]);

nrows++;
}
```
```

Each trip through the loop reads one line from the file, using fgetsline. Each line is broken up into “words” using getwords; each “word” is actually one number. The numbers are however still represented as strings, so each one is converted to an int by calling atoi before being stored in the array. The code checks for two different error conditions (failure to open the input file, and too many lines in the input file) and if one of these conditions occurs, it prints an error message, and exits. The exit function is a Standard library function which terminates your program. It is declared in <stdlib.h>, and accepts one argument, which will be the exit status of the program. EXIT_FAILURE is a code, also defined by <stdlib.h>, which indicates that the program failed. Success is indicated by a code of EXIT_SUCCESS, or simply 0. (These values can also be returned from main(); calling exit with a particular status value is essentially equivalent to returning that same status value from main.)

## Self Assessment Questions

- 5. The companion function to putchar is put, and the file pointer
argument comes first. (True/False)
- 6. Besides the file pointers which we explicitly open by calling fopen, there are also __________ predefined streams.
- 7. getchar() is the same as getc(stdin).(True/False)

## 13.5 Error Handling during I/O operations

The standard I/O functions maintain two indicators with each open stream to show the end-of-file and error status of the stream. These can be interrogated and set by the following functions:

```
#include <stdio.h>
void clearerr(FILE *stream);
int feof(FILE *stream);
int ferror(FILE *stream);
void perror(const char *s);
```

clearerr clears the error and EOF indicators for the stream.

feof returns non-zero if the stream's EOF indicator is set, zero otherwise. ferror returns non-zero if the stream's error indicator is set, zero otherwise.

perror prints a single-line error message on the program's standard output, prefixed by the string pointed to by s, with a colon and a space appended. The error message is determined by the value of errno and is intended to give some explanation of the condition causing the error. For example, this program produces the error message shown:

```
#include <stdio.h>
```

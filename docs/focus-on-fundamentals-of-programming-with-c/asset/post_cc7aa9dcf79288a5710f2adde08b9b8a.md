
This creates a file containing the output of foo. Any values displayed by printf() would not be displayed at the terminal but instead would be written into the file called outFile.txt. Error messages, if any, will continue to be displayed on the terminal window, instead of being buried inside the output file.

![](img/7f36c52b5170b89b142dbb7b1ea4666b_195_0.png)

A similar redirection is possible for the standard input. Any call to a function that normally reads data from the terminal, such as getchar() and scanf(), can be made to read its information from a file. For example, we can run program foo using data that we have stored in a file called inFile.txt:

```
foo < inFile.txt
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_195_1.png)

Finally, we can combine both input redirection and output redirection:

```
foo < inFile.txt > outFile.txt
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_196_0.png)

```
FILE * cis
fprintf( cis, "text");
stdout
fscanf( cis, "%d", &x);
scanf( "%d", &x)
fscanf( stdin, "%d", &x);
```

## Getchar()

I/O is not part of C proper but are basic extensions necessary for writing most programs.

getchar() returns the next character from standard input (keyboard) and returns it as a function return value. If there is no more input then EOF (end of file) is returned instead. It is therefore usual to compare the value returned by getchar() against EOF before using it.

At some point during program execution, the user may indicate “no more input” by entering ^z (control z) (or in some environments ^d) and EOF will be returned from getchar().

getchar() and EOF are defined in a standard include file named stdio.h which we must include in all of our compilations:

```
#include <stdio.h>
```

Certain C expressions become part of our standard vocabulary such as:

```
while ((c = getchar()) != EOF)
```

This expression is used at the beginning of a loop that gets a character at a time from the standard input. Look closely at the expression and note the "extra" pair of parentheses. Can you figure out why are they needed?

Next, think about the difference between:

```
while (c = getchar())
```

and

```
while (c == getchar())
```

It can take a long time to see the difference and sometimes even longer to decide which one you really want!

Here's a program to count the number of characters read from an input stream until an EOF is encountered:

```
#include <stdio.h>

int main(void) {
    int c, count = 0;

    while ((c = getchar()) != EOF) {
        ++count;
    }
    printf("%d\n", count);
    return 0;
}
```

Note that c is declared to be an int rather than a char. This is because EOF is given a defined value of -1. On some machines a char can only be a positive value and therefore to return a -1 we define c to be an int.

We can replace the while statement above with a for statement:

```
#include <stdio.h>

int main(void) {
    int count;

    for (count = 0; getchar() != EOF; ++count) {
        ;
    }
    printf("%d\n", count);
    return 0;
}
```

## We can also count newlines:

```
#include <stdio.h>

void main(void) {
    int c, count = 0;

    while ((c = getchar()) != EOF) {
        if (c == '\n') {
            ++count;
        }
    }
    printf("%d\n", count);
    return 0;
}
```

## Here's a program to map a program's input to lower case:

```
#include <stdio.h>
#include <ctype.h>

void main(void) {
    int c;

    while ((c = getchar()) != EOF) {
        printf("%c", isupper(c) ? tolower(c) : c);
    }
    return 0;
}
```

## Here's an expression that causes blank characters in the input stream to be skipped:

```
while ((c = getchar()) != ' ') {
}
```

Because C contains no built-in function to read an entire line of input, it could be called a rather primitive language. However, this encourages tool building! So let's build a function to read a line of input and package it as a function named getLine() to be used whenever needed.

The following program copies lines of input onto the output. It reads one line at a time into string buf. A null terminator is put at the end of string buf. If the input is at EOF, the value of EOF is returned.

```
#include <stdio.h>
#define BUFSIZ 81
int getLine(char buf[]);
int main(void) {
    char buf[BUFSIZ];
    while (getLine(buf) != EOF) {
        printf("%s", buf);
    }
    return 0;
}
int getLine(char buf[]) {
    char c;
    int i = 0;
    do {
        c = getchar();
        buf[i++] = c;
    } while(c != '\n');
    buf[i-1] = '\0';
    return i;
}
```

Watch how we can rewrite getLine() more simply:

```
int getLine(char buf[]) {
    char c;
    int i = 0;
    while ((buf[i++] = getchar()) != '\n') {
    ;
    }
    buf[i] = '\0';
    return i;
}
```

## Putchar()

putchar() outputs a single character to standard output (terminal window). The arguments to putchar() should be one individual character, either variable or constant:

```
putchar(c);
putchar('a');
putchar('\n');
```

If you just need to output a single character without format, use putchar() instead of printf(). Here's a program, copy.c that copies its input to output:

```
#include <stdio.h>

int main(void) {
    int c;

    while ((c = getchar()) != EOF) {
        putchar(c);
    }
    return 0;
}
```

Note, if this program is applied to a file of 100 bytes, it will call getchar() 101 times. The first 100 calls will return a data byte. The 101st call will return the EOF value. Therefore the test is evaluated 101 times and the loop body is executed 100 times.

With this program we can write our own command line copy command using I/O redirection:

```
copy < infile.txt > outfile.txt
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_202_0.png)

Here's a program to map its input to lower case:

```
#include <stdio.h>
#include <ctype.h>
int main(void) {
    int c;
    while ((c = getchar()) != EOF) {
        putchar(isupper(c) ? tolower(c) : c);
    }
    return 0;
}
```

Finally, let's write some code that reads text of all lower case letters and selectively capitalize the first letter of each word. A letter will be defined as any non-whitespace character.

## First an algorithm:

```
for each whitespace character w
    output w
for each word
    capitalize initial letter
    for each succeeding letter
        output c
for each whitespace character w
    output w
```

## Now some code:

```
while ((c = getchar()) != EOF) {
    if (isspace(c)) {
        putchar(c);
    } else {
        putchar(toupper(c));
        while (isspace(c = getchar())) {
            putchar(c);
        }
        putchar(c);
    }
}
```

Let's see if we can redesign this algorithm and code:

## First the algorithm:

```
for each input character c
    if c is the first letter of a word
        output capitalized c
    else
        output c
```

## Now the code:

```
for (wasWhite = 1; (c = getchar()) != EOF; wasWhite = isspace(c)) {
    putchar (isspace(c) && wasWhite ? toupper(c) : c);
}
```

Note that this design results in a simpler program.

## Text Files

A text file is a sequence of *characters* terminated by an *end-of-file marker*. The length of the file is not specified when the file is defined. The characters in the file are stored on a storage device other than the memory occupied by the program while the program is executing, such as a disk drive.

Note the emphasis on characters. That's all there is in a text file, just characters. Sprinkled among the characters may be newline characters, '\n', or tab '\t' characters. In addition, each data element in the file (words, numeric data) is usually (though not always) separated from the others by blanks.

The advantage of files is that they can exist independently of the program that creates or uses the data in the file. The size of the file is also not a limiting factor as we can increase the file size simply by adding a character to the end of the file.

## Accessing Text Files

A text file is accessed via a pointer to a structure that is defined in the standard header file `stdio.h` as `FILE`. This structure `FILE` contains members (fields) that describe the current state of the file.

C communicates with files using a data type called a *file pointer*. This type is defined within `stdio.h`, and is written as `FILE *`. A file pointer called `fp` is declared in a statement like:

```
FILE *fp;
```

Your program must first open a file before it can access it. This is done using the `fopen()` function, which returns the required file pointer. `fopen()` is declared as follows:

```
FILE *fopen(char *fileName, char *fileMode);
```

`fopen()` opens a file for I/O and returns a pointer to `FILE`. Both `fileName` and `fileMode` are strings. File names may be any valid file name that can exist under the operating system and can include path information:

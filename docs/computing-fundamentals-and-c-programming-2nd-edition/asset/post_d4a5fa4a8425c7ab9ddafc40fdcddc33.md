
### WORKED-OUT PROBLEM 14.7

Write a C program to reverse the first n characters in a file. The file name and the value of n are specified on the command line. Incorporate validation of arguments, that is, the program should check that the number of arguments passed and the value of n are meaningful.

```c
Program
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <string.h>

void main(int argc, char *argv[])
{
    FILE *fs;
    char str[100];
    int i,n,j;

    if(argc!=3)/*Checking the number of arguments given at command line*/
    {
        puts("Improper number of arguments.");
        exit(0);
    }

    n=atoi(argv[2]);
    fs = fopen(argv[1], "r");/*Opening the source file in read mode*/
    if(fs==NULL)
    {
        printf("Source file cannot be opened.");
        exit(0);
    }

    i=0;
    while(1)
    {
        if((str[i]=fgetc(fs))!=EOF)/*Reading contents of file character by character*/
        j=i+1;
        else
            break;
    }
    fclose(fs);
    fs=fopen(argv[1],"w"); /*Opening the file in write mode*/
    if(n<0||n>strlen(str))
    {
        printf("Incorrect value of n. Program will terminate...\n\n");
        getch();
        exit(1);
    }

    j=strlen(str);
    for (i=1;i<=n;i++)
    {
        fputc(str[j],fs);
        j--;
    }
    fclose(fs);

    printf("\n%d characters of the file successfully printed in reverse order",n);
    getch();
}

Output
D:\TC\BIN\program source.txt 5
5 characters of the file successfully printed in reverse order
```

**Fig. 14.7**  *Program to reverse n characters in a file*

## 14.7 COMMAND LINE ARGUMENTS

What is a command line argument? It is a parameter supplied to a program when the program is invoked. This parameter may represent a filename the program should process. For example, if we want to execute a program to copy the contents of a file named **X_FILE** to another one named **Y_FILE**, then we may use a command line like

C > PROGRAM X_FILE Y_FILE

where **PROGRAM** is the filename where the executable code of the program is stored. This eliminates the need for the program to request the user to enter the filenames during execution. How do these parameters get into the program?

We know that every C program should have one **main** function and that it marks the beginning of the program. But what we have not mentioned so far is that it can also take arguments like other functions. In fact **main** can take two arguments called **argc** and **argv** and the information contained in the command line is passed on to the program through these arguments, when **main** is called up by the system.

The variable **argc** is an argument counter that counts the number of arguments on the command line. The **argv** is an argument vector and represents an array of character pointers that point to the command

```c
/* Writing content of the file to screen                  */

printf("Contents of %s file\n\n", argv[1]);
fp = fopen(argv[1], "r");
for(i = 2; i < argc; i++)
{
    fscanf(fp,"%s", word);
    printf("%s ", word);
}

fclose(fp);
printf("\n\n");

/* Writing the arguments from memory */

for(i = 0; i < argc; i++)
    printf("%d %s \n", i*5, argv[i]);
}

Output

C:\F12_7 TEXT AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG

No. of arguments in Command line = 9

Contents of TEXT file

AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG

C:\F12_7.EXE
TEXT
    AAAAAA
       BBBBBB
          CCCCCC
             DDDDDD
                EEEEEE
                   FFFFFF
                      GGGGGG
```

**Fig. 14.8** *Use of command line arguments*

## LEARNING OUTCOMES

- Do not try to use a file before opening it. LO 14.1
- Remember, when an existing file is open using 'w' mode, the contents of file are deleted. LO 14.1
- When a file is used for both reading and writing, we must open it in 'w+' mode. LO 14.1
- It is an error to omit the file pointer when using a file function. LO 14.1
- It is an error to open a file for reading when it does not exist. LO 14.1
- It is an error to access a file with its name rather than its file pointer. LO 14.1
- It is a good practice to close all files before terminating a program. LO 14.1
- EOF is integer type with a value -1. Therefore, we must use an integer variable to test EOF. LO 14.2
- It is an error to try to read from a file that is in write mode and vice versa. LO 14.2
- To avoid I/O errors while working with files, it is a good practice to include error handling code in programs by using functions such as feof and ferror. LO 14.3
- It is an error to attempt to place the file marker before the first byte of a file. LO 14.4
- It is a good practice to check the return value of fseek function every time it is invoked. A positive return value ensures that the file pointer is within the file boundaries. LO 14.5

## KEY TERMS TO REMEMBER

- **Filename:** It is a string of characters that make up a valid filename for the operating system. LO 14.1
- **fseek:** It is a function that sets the position to a desired point in the file. LO 14.4
- **ftell:** It is a function that returns the current position in the file. LO 14.4
- **rewind:** It is a function that sets the position to the beginning of the file. LO 14.4
- **Command line argument:** It is a parameter supplied to a program from command prompt when the program is invoked. LO 14.5

## REVIEW QUESTIONS

### Fill in the Blanks

1. The mode ______ is used for opening a file for updating. LO 14.1
2. The function ______ is used to write data to randomly accessed file. LO 14.2
3. The function ______ gives the current position in the file. LO 14.4
4. The function ______ may be used to position a file at the beginning. LO 14.4

### True or False Statements

1. A file must be opened before it can be used. LO 14.1
2. All files must be explicitly closed. LO 14.1

Levels of Difficulty

Low; Medium; High

3. Files are always referred to by name in C programs.
4. Using **fseek** to position a file beyond the end of the file is an error.
5. Function **fseek** may be used to seek from the beginning of the file only.

### Discussion Questions

1. Describe the use and limitations of the functions **getc** and **putc**.
2. What is the significance of EOF?
3. When a program is terminated, all the files used by it are automatically closed. Why is it then necessary to close a file during execution of the program?
4. Distinguish between the following functions:
   (a) getc and getchar
   (b) printf and fprintf
   (c) feof and ferror
5. How does an append mode differ from a write mode?
6. What are the common uses of **rewind** and **ftell** functions?
7. Explain the general format of **fseek** function?
8. What is the difference between the statements `rewind(fp);` and `fseek(fp,0L,0);`?

9. What does the following statement mean?

```c
FILE (*fp) (void)
```

10. What does the following statement do?

```c
while ( (c = getchar( ) ) != EOF )
    putc(c, fl);
```

11. What does the following statement do?

```c
while ( (m = getw(fl) ) != EOF)
    printf("%5d", m);
```

12. What does the following segment do?

```c
for ( i = 1; i <= 5; i++ )
{
    fscanf(stdin, "%s", name);
    fprintf(fp, "%s", name);
}
. . .
```

13. What is the purpose of the following functions?
    (a) feof()
    (b) ferror()
14. Give examples of using feof and ferror in a program.

**Table 15.1 Preprocessor Directives**

| Directive | Function |
|---|---|
| #define | Defines a macro substitution |
| #undef | Undefines a macro |
| #include | Specifies the files to be included |
| #ifdef | Test for a macro definition |
| #endif | Specifies the end of #if. |
| #ifndef | Tests whether a macro is not defined. |
| #if | Test a compile-time condition |
| #else | Specifies alternatives when #if test fails. |

These directives can be divided into three categories which are as follows:

1. Macro substitution directives.
2. File inclusion directives.
3. Compiler control directives.

## 15.2 MACRO SUBSTITUTION LO 15.1

Macro substitution is a process where an identifier in a program is replaced by a predefined string composed of one or more tokens. The preprocessor accomplishes this task under the direction of #define statement. This statement, usually known as a macro definition (or simply a macro) takes the following general form:

```c
#define identifier string
```

If this statement is included in the program at the beginning, then the preprocessor replaces every occurrence of the identifier in the source code by the string. The keyword #define is written just as shown (starting from the first column) followed by the identifier and a string, with at least one blank space between them. Note that the definition is not terminated by a semicolon. The string may be any text, while the identifier must be a valid C name.

There are different forms of macro substitution. The most common forms are as follows:

1. Simple macro substitution.
2. Argumented macro substitution.
3. Nested macro substitution.

### Simple Macro Substitution

Simple string replacement is commonly used to define constants. Examples of definition of constants are as follows:

```c
#define COUNT 100
#define FALSE 0
#define SUBJECTS 6
#define PI 3.1415926
#define CAPITAL "DELHI"
```

Notice that we have written all macros (identifiers) in capitals. It is a convention to write all macros in capitals to identify them as symbolic constants. A definition, such as

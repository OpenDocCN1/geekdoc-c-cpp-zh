
**Comments:** We could present a simpler solution similar to C.15.16. That is, we could declare grd_arr as an ordinary pointer, store the grades in the allocated memory, and read the grades from this memory in groups of five, in order to calculate the average grade of each student. The reason we choose this solution is to remember how to handle the allocated memory as a two-dimensional array.

## The feof() Function

The feof() function is used to determine whether the end of file is reached. It is declared in stdio.h:

```
int feof(FILE *fp);
```

If a read operation attempts to read beyond the end of file indicated by fp, feof() returns a nonzero value, 0 otherwise. As we've seen, when we are using a read function we examine its return value to determine if it is executed successfully or not. If the operation is unsuccessful, we can use feof() to determine whether the failure was due to an end of file condition or for another reason. For example, the following program reads the contents of a text file (assume that each line has less than 100 characters) and if fgets() fails, we use feof() to see why.

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
    char str[100];

    fp = fopen("test.txt", "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    while(1)
    {
        if(fgets(str, sizeof(str), fp) != NULL)
            printf("%s", str);
        else
        {
            if(feof(fp))
                printf("End of file\n");
            else  printf("Failed for another reason\n");
            break;
        }
    }
    fclose(fp);
    return 0;
}
```

## Exercise

C.15.22 Assume that each line of the test.c text file contains less than 100 characters. What does the following “badly written” program do?

```
#include <stdio.h>
int main(void)
{
    FILE *fp;
    char str[100];
    for(fp = fopen("test.c", "r"); fp && !feof(fp); fgets(str, sizeof(str), fp) ? printf("%s", str) : 1);
    return fp ? fclose(fp) : 0;
}
```

Answer: The program uses fgets() to read and display each line of test.c, while the loop is executed as long as the end of file is not reached. If fopen() fails, fp would be equal to NULL, the loop won't be executed and the program returns 0. Otherwise, fclose() closes the file and the program returns its return value.

## Unsolved Exercises

U.15.1 Suppose that the grades.txt text file contains the grades of a number of students. Write a program that reads the file and displays the best and the worst grades, the average grade of those who failed (grade < 5), and the average grade of those who succeeded (grade ≥ 5). Suppose that the grades are within [0, 10].

U.15.2 Write a program that finds the sequential doubled words (e.g., "In this this chapter we we present...") in a user selected text file and writes them into another text file. Assume that each word has less than 100 characters.

U.15.3 Suppose that each line of the students.txt text file contains the grades of the students in three courses. Write a program that reads the file and displays the average grade of each course. For example, if the file content is:

5      3.5      9
9      6        4.5

the program should display: 7   4.75   6.75

U.15.4 Write a program that checks if two user selected text files have the same content.

## U15.6

Write a program that reads the names of two text files from the command line and appends the content of the second file into the first one. Then, the program should display the content of the first file. Assume that each line contains less than 100 characters.

## U15.7

Write a program that reads a name of a text file and copies its content in reverse order, that is, from the last character up to the first one, into a second user selected text file. Hint: Open the first file as binary.

## U15.8

Suppose that each line of the students.txt text file contains the name of a student (less than 100 characters) and his grades in three courses. Write a program that reads the file and displays the name(s) of the student(s) with the best average grade. Assume that there are fewer than 300 students and more than one student may have the same best average grade.

## U15.9

Write a program that reads the name of a text file from the command line and displays its longest line. Assume that there is no more than one line with the same longer length. The program should also display the occurrences of each digit [0, 9] in the file. Furthermore, the program should read an integer (e.g., x) and display the last x lines of the file. The program should check that the input number is not greater than the number of the total lines. For example, if the user enters 3 the program should display the last three lines of the file. There is one restriction; the program should read each line only once. Assume that there are fewer than 1000 lines and each line contains fewer than 100 characters.

## U15.10

Write a program that reads the name of a text file and the number of a line and replaces that line with a new input text. If the line has more characters than the new text, the extra characters until the end of line should be replaced with the space character. If it has fewer, the replacement should be done until the end of line. It is mandatory to use getchar() and putc() to read and write to the file and getchar() to read the new text. For example, if the file content is:

```
```
First
Second
Third
```
```

and the user enters as line number 2 and the text New, the file becomes:

```
```
First
New
Third
```
```

if the users enters 1 and Introduction, it becomes:

```
```
Intro
Second
Third
```
```

## U15.11

Define the structure type book with members: title, author, and price. Suppose that the book.dat binary file contains 100 of those structures. Write a program that reads the sequence number of a book entry (e.g., 25), the new data, and replace the existing data
with the new data. Then, the program should read from the file the data of that entry and display them, in order to verify that it was written correctly.

## U15.12

Consider the file book.dat of the previous exercise. Write a program that reads the existing entries and writes them in the book_rvs.dat binary file in reverse order, that is, the last entry should be written first, the last but one written second, and so on.

## U15.13

Suppose that the grades.dat binary file contains the grades of a number of students. The number of students is stored in the beginning of the file. Write a program that reads the file and writes the grades sorted in ascending order in the grd_sort.dat binary file.

## 16

## The Preprocessor

Although the preprocessor can be a separate program, it is typically integrated with the compiler to improve compilation speed. It is a software program that processes a C program before it is compiled. Its major capabilities involve file inclusion, macro substitution, and conditional compilation. First, we’ll discuss how to define and use macros in a C program. We’ll devote the rest of the chapter to describe preprocessor directives and operators.

## Simple Macros

The behavior of the preprocessor is controlled by directives. The directives are special commands that begin with a # character and instruct the preprocessor to do something. For example, the #include directive instructs the preprocessor to open a specified file and include its contents into the program. Directives can appear anywhere in the program. A line that contains a single # is legal; it has no effect, though. Another directive we’ve been using is the #define directive. We’ve used it to define a simple macro, that is, a symbolic name associated with a constant value. To define a simple macro we write:

```
#define macro_name replacement_characters
```

The macro_name has the same form as a variable name. The replacement_characters are arbitrary. Typically, most programmers choose capital letters to name macros (we do the same), in order to distinguish them from program variables. The scope of the name begins from the point of its definition until the end of the file. For example, in the following program:

```
#include <stdio.h>

#define LEN 200

int main(void)
{
    int i, arr[LEN];

    for(i = 0; i < LEN; i++)
        arr[i] = i+LEN;

    return 0;
}
```


**Comments:** This code is reliable with the assumption that the failure reason of `fopen()` is that the file does not exist, not some other reason. Also, we assume that no other running application will create the file in the time interval between checking and creating the file.

## Read Data from a Text File

The most common functions to read data from a text file are: `fscanf()`, `fgets()`, and `fgetc()`. These functions are mostly used with text files; however, we can use them to read data from binary files as well.

> For simplicity, we assume that if the function we used to read data returns EOF, it is because the end of file is reached, not because of a read error. However, a robust program should check the reason for failure.

### The fscanf() Function

The `fscanf()` function is used to read a variable number of different data items from an input file. Like `scanf()`, `fscanf()` uses a format string to define the order and the type of data that will be read from the file. It is declared in `stdio.h`.

```
int fscanf(FILE* fp, const char *format, ...);
```

The only difference between them is that `scanf()` always reads from `stdin`, while `fscanf()` reads from the file indicated by `fp`.

As discussed, the operating system (e.g., Unix) may allow the redirection of `stdin`. For example, if the name of the executable is `test` and we write in the command line:

```
test <input.txt
```

the input read from `stdin` (e.g., with `scanf()`) won't be read from the keyboard, but from the `input.txt` file. Also, we can combine both redirections. For example:

```
test <input.txt >output.txt
```

`fscanf()` returns the number of data items successfully read from the file and assigned to program variables. If either the end of file is reached or the read operation fails, it returns EOF. Later, we'll see that we can use `feof()` to determine which one happened. The following program assumes that the `test.txt` text file contains the annual temperatures in an area. It reads them and displays those within [-5, 5].

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    FILE *fp;
    int k;
    double temp;

    fp = fopen("test.txt", "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    while(1)
    {
        k = fscanf(fp, "%lf", &temp); /* Since fscanf() reads one item, the return value 1 indicates that the value was successfully read and assigned to temp. */
        if(k != 1)
            break;
        if(temp >= -5 && temp <= 5)
            printf("%f\n", temp);
    }
    fclose(fp);
    return 0;
}
```

We could omit the declaration of `k` and write:

```c
if(fscanf(fp, "%lf", &temp) != 1)
```

Also, we could put `fscanf()` inside the `while` statement and write it like this:

```c
while(fscanf(fp, "%lf", &temp) == 1)
```

As a matter of style, we prefer the `while(1)` statement to make clearer the terminating condition of the loop.

We also suggest to test the return value of `fscanf()` against the number of the assigned items, rather than `EOF`. For example, suppose that the following code reads the floats contained in a text file:

```c
float i;
while(fscanf(fp, "%d", &i) != EOF)
{
    /* Do some work with i */
}
```

Although `i` is not assigned with a correct value due to the wrong specifier `%d`, `fscanf()` does not return `EOF` and the loop continues. Had we written:

```c
while(fscanf(fp, "%d", &i) != 1)
```

the wrong assignment would have been traced and the loop would terminate.

Before using `fscanf()`, the programmer is supposed to know the type of the stored data and their order in the file. For example, in the following program, it is assumed that the programmer knows that each line of the `test.txt` file contains a string of less than 100 characters, an integer and a double number, in order to pass the right arguments in `fscanf()`.

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    FILE *fp;
    char str[100];
    int i;
    double d;

    fp = fopen("test.txt", "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    while(1)
    {
        if(fscanf(fp, "%s%d%lf", str, &i, &d) != 3)
            break;
        printf("%s %d %f\n", str, i, d);
    }
    fclose(fp);
    return 0;
}
```

Like `scanf()`, `fscanf()` uses the space character to distinguish the read values.

> As with `scanf()`, be careful when using `%s` in `fscanf()` to read strings. If the string contains many words, only the first will be read.

Since `stdin` is associated with the keyboard by default, if we replace the first argument of `fscanf()` with `stdin`, a call of `fscanf()` is equivalent to a call of `scanf()`. For example, the following program uses `fscanf()` and `fprintf()`, instead of `scanf()` and `printf()`, to read an integer and a double number and display them.

```c
#include <stdio.h>

int main(void)
{
    int i;
    double d;

    fprintf(stdout, "Enter an integer and a double: ");
    if(fscanf(stdin, "%d%lf", &i, &d) == 2)
        fprintf(stdout, "%d %f\n", i, d);
    return 0;
}
```

## Exercises

**C.15.6** Write a program that reads products' codes (less than 20 characters each) and their prices and stores them in a text file, as follows:

```
C101 17.5
C102 32.8
...
```

If the user enters `-1` for price, the insertion of products should terminate. Then, the program should read a product's code and search the file to find and display its price.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    FILE *fp;
    char flag, str[20], prod[20];
    double prc;

    fp = fopen("test.txt", "w+");  /* Open file for reading and writing. */
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    while(1)
    {
        printf("Enter price: ");
        scanf("%lf", &prc);
        if(prc == -1)
            break;
        getchar();
        printf("Enter product code: ");
        read_text(str, sizeof(str), 1);
        fprintf(fp, "%s %f\n", str, prc);
    }
    getchar();
    printf("Enter product code to search for: ");
    read_text(prod, sizeof(prod), 1);

    flag = 0;
    fseek(fp, 0, SEEK_SET);
    while(1)
    {
        if(fscanf(fp, "%s%lf", str, &prc) != 2)
            break;
        if(strcmp(str, prod) == 0)
        {
            flag = 1;
            break; /* Since the product is found exit from the loop. */
        }
    }
    if(flag == 0)
        printf("The %s product is not listed\n", prod);
    else
        printf("The price for product %s is %f\n", prod, prc);
    fclose(fp);
    return 0;
}
```

**Comments:** We could use first the `w` mode to open the file to write data, then close it, and reopen it with the `r` mode to read data. To avoid that, we used the `r+w` mode and the `fseek()` function to rewind the file pointer at the beginning of the file and start reading from there. We'll talk about `fseek()` in a short while.

**C.15.7** Suppose that each line of the `students.txt` text file contains the names of the students and their grades in two lessons, as follows:

|       |        |       |       |
|-------|--------|-------|-------|
| John  | Morne  | 7     | 8.12  |
| Sahil | Nehrud | 4.5   | 9     |
| Koon  | Lee    | 2     | 5.75  |

Write a program that reads each line of `students.txt` and stores in `suc.txt` the names and grades of the students with average grade greater than or equal to 5, while in `fail.txt` the students with average grade less than 5. To read the grades, use double variables and assume that the names are less than 100 characters. The program should display the number of students written in each file.

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    FILE *fp_in, *fp_suc, *fp_fail;
    char fnm[100], lnm[100];
    int suc_stud, fail_stud;
    double grd1, grd2;

    fp_in = fopen("students.txt", "r");
    if(fp_in == NULL)
    {
        printf("Error: students.txt can't be loaded\n");
        exit(EXIT_FAILURE);
    }
    fp_suc = fopen("suc.txt", "w");
    if(fp_suc == NULL)
    {
        fclose(fp_in);
        printf("Error: suc.txt can't be created\n");
    }
```

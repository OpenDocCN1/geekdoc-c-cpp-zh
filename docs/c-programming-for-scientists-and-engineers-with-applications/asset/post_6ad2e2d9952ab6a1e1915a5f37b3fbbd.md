
# Failsafe Input of Numbers

The following decimal numbers contained in a data myfile2.dat,

```
695.23 23.5647 0.2034 2349.7658
```

are to be input into the variables var1, var2, var3, and var4.

The following code shows the input.:

```
FILE *inptr;
```

```
float var1, var2, var3, var4;
```

```
inptr = fopen("myfile2.dat", "r");
```

```
if(inptr)
{
    scanf(inptr, "%f %f", &var1, &var2);
    fscanf(inptr, "%f %f", &var3, &var4);
}
else
{
    printf("myfile2.dat not available\n");
}
```

Notice that if the file is opened successfully for input, inptr is a pointer to the file that is interpreted as "true," otherwise inptr is a null pointer that is read from the input file and stored in the variables var1, var2, var3, and var4. If the file is not successfully opened for input then an error message is displayed on the screen.

# 3.2.4 Output to a Data File

Output to a data file uses a function call to the fprintf( ) library function. The general form of the function call is:

```
fprintf(file pointer, "format control string", var1,....varn);
```

The first argument must be the output file pointer; the next, the format control string; and the remaining arguments, a list of variables. The following examples show output to a data file.

Output of Numbers The format control field for the output of integer numbers is %.d. To space the individual data values in the output, blank spaces must be provided within the format control field. The following examples show the output of integer numbers. The numbers in storage are as follows:

| var1 | var2 | var3 | var4 |
|---|---|---|---|
| 65438 | 87.63900 | .256170 | -1032 |

The statements needed to output these numbers into a data file myfile3.dat are as follows:

```
int var1, var4;
float var2, var3;

FILE *outptr;

outptr = fopen("myfile3.dat", "w");

fprintf(outptr, "%d %f %f %d", var1, var2, var3, var4);
```

The output statement uses the format control field "%d %f %f %d", which specifies the types of numbers to be written to the output file. There are four control fields within the format control string that correspond to four variables specified in the output statement. The output written to the data file myfile3.dat is as follows:

Before:

![](img/8356e6c3bfe3b10354682c60b1e74b1d_165_0.png)

# 3.2 File Input and Output

After:

```
myfile3.dat
outptr----> 65438  87.639000  256167 -1032 uuuuu...
      record marker
```

Notice that the numbers written to the output data file have two spaces between them. These spaces correspond to the spaces provided in the format string. After the numbers have been written, the record marker points to the next available data items, ready for another fprintf statement.

Failsafe Output of Numbers The following decimal numbers are to be written to the beginning of a myfile5.dat:

| var1 | var2 | var3 | var4 |
| --- | --- | --- | --- |
| 435.7654 | 0.876230 | -125.7650 | 8256.035 |

The statements needed are as follows:

```
int var1, var2, var3, var4;
```

FILE *outptr;

outptr = fopen("myfile5.dat", "w");

```

if(outptr)
{
    printf("%f %f %f", var1, var2, var3, var4);
}
else
{
    printf("myfile5.dat not available");
}
```

The error message will be displayed on the standard output device if the file is already opened or if it cannot be found.

Building a Data File Assume that a file graph.dat is to be created from pairs of real numbers entered from a keyboard, which represent the coordinates of points on a graph; the file will be built by the following program. Entry of numbers will continue until an end of file (CTRL Z–control character) is entered.

```
#include <stdio.h>
int main() 
{
    float x, y;
    FILE *graphptr;

    graphptr = fopen("graph.dat", "w");

    if(graphptr) {
        while(scanf("%f %f", &x, &y)) {
            fprintf(graphptr, "%f %f", x, y);
        }
        fclose(graphptr);
    }
    else {
        printf("File <graph.dat> is not available");
    }

    return 0;
}
```

Assuming that the file is already opened, more data is added to it, rather than overwritten.

Listing a Data File The following program shows the coordinates of points on a graph; the file will be built by the following program. Entry of numbers will continue until an end of file (CTRL Z–control character) is entered.

```c
#include <stdio.h>
int main()
{
    float x, y;
    FILE *graphptr;

    graphptr = fopen("graph.dat", "w");

    if(graphptr) {
        while(scanf("%f %f", &x, &y)) {
            fprintf(graphptr, "%f %f", x, y);
        }
        fclose(graphptr);
    }
    else {
        printf("File <graph.dat> is not available");
    }

    return 0;
}
```

The coordinates of points on a graph are displayed by the following program:

```c
#include <stdio.h>
int main()
{
    float x, y;
    FILE *fptr;

    fptr = fopen("graph.dat", "r");

    if(fptr) {
        while(fscanf(fptr, "%f %f", &x, &y)) {
            printf("%f %f\n", x, y);
        }
        fclose(fptr);
    } else {
        printf("File <graph.dat> is not available");
    }

    return 0;
}
```

# 3.3 Field Width Specification

Within the format control string, the width for each of the control fields can be specified for both the input and output variables. The specification of the number of characters to output is very important when uniform output needs to be displayed or written to the data file. The following examples and program show the input and output format width specifications.

## 3.3.1 Input Field Width Specification

The general form of the field width specification is as follows:
%nd for integer numbers, n must be a numeric literal specifying the number of positions for digits and signs, e.g., %7d, %10d.
%nf for real numbers, n must be a numeric literal specifying the total of digits, decimal point position, and sign position, e.g., %10f, %6f.

The following examples show input with control field width specification.

Input of Integer Numbers The following numbers are to be input into the variables var1, var2, and var3:

7865-5134690487

The code to input these numbers is as follows:

```
int var1, var2, var3;
```

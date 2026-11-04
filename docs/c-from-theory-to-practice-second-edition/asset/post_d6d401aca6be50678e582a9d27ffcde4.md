
The ftell() function is used to find the current position of a file pointer. It is declared in stdio.h:

```
long int ftell(FILE *fp);
```

ftell() returns the current position of the file pointer associated with fp. The position is expressed as the number of bytes from the beginning of the file. If an error occurs, ftell() returns -1. ftell() may be used together with fseek() to return to a previous file position, like this:

```
long int old_pos;
/* ... open file and do some work with it. */
old_pos = ftell(fp);
/* ... do some other work. */
fseek(fp, old_pos, SEEK_SET); /* return back to the old position. */
```

> Tip: It is safer to use fseek() and ftell() with binary rather than text files because potential translations of the new line character can produce unexpected results. fseek() is guaranteed to work with text files only if:

- a. offset is 0 or
- b. offset is obtained from a previous call to ftell() and origin is set to SEEK_SET.

## Write and Read Data from a Binary File

The fwrite() and fread() functions are used to write and read data from a binary file. These functions are used primarily with binary files, although we can use them, with some care, with text files as well.

### The fwrite() Function

The fwrite() function is very useful for writing large blocks of data in a single step. It is declared in stdio.h:

```
int fwrite(const void *buf, size_t size, size_t count, FILE *fp);
```

The first argument points to the memory that holds the data to be written in the file indicated by fp. The third argument specifies how many elements will be written in the file, while the second one specifies the size of one element in bytes. The product of the second and third arguments specifies the number of the bytes to be written in the file. For example, to write an array of 1000 integers, the second argument should be equal to the size of one integer, that is, 4, while the third argument should be equal to 1000.

```
int arr[1000];
fwrite(arr, 4, 1000, fp);
```

The best practice is to use the sizeof operator to specify the size of one element, in order to make your program platform independent. For example, it'd be better to write:

```
fwrite(arr, sizeof(int), 1000, fp);
```

As another example, the following code writes one double number:

```
double a = 1.2345;
fwrite(&a, sizeof(double), 1, fp);
```

fwrite() returns the number of the elements actually written in the file. If the return value equals the third argument, it is implied that the fwrite() was executed successfully. If not, a write error occurred.

Some programmers prefer to declare the total memory size and make the number of elements equal to 1. For example:

```
fwrite(arr, 1000*sizeof(int), 1, fp);
```

Don't do that. If fwrite() fails, it will return 0 and you'll have no idea if any and how many integers were stored in the file. The same applies for fread().

### The fread() Function

Like fwrite(), fread() is very useful for reading large blocks of data in a single step. It is declared in stdio.h:

```
int fread(void *buf, size_t size, size_t count, FILE *fp);
```

The first argument points to the memory in which the read data will be stored. Like fwrite() arguments, the second argument specifies the size of one element in bytes, while the third one specifies how many elements will be read from the file.

> Because two systems may differ (e.g., the size of types), there is no guarantee that a file written with the fwrite() function will be read correctly with the fread() function in another system.

fread() returns the number of the elements actually read from the file. As with fwrite(), this value should be tested against the third argument. If they are equal, fread() was executed successfully. Otherwise, either the end of file is reached or a read error occurred. In the following example, a double number is read and stored into a:

```
double a;
fread(&a, sizeof(double), 1, fp);
```

As another example, 1000 integers are read and stored into array arr:

```
int arr[1000];
fread(arr, sizeof(int), 1000, fp);
```

> It is safer to use fwrite() and fread() with binary rather than text files because potential translations of the new line character can produce unexpected results.

For example, suppose that we use fwrite() to write a string of 50 characters in a text file and the value of count is set to 50. If the program runs in Windows and the string contains new line character(s), the replacement(s) with the \r\n pair would make its size more than 50; therefore, fwrite() won't write the entire string.

### Exercises

C.15.13 Write a program that declares an array of 5 integers with values 10, 20, 30, 40, and 50 and writes them in a binary file. Then, the program should read an integer and replace the third stored integer with the input number. The program should read and display the file's content before it ends.

```
#include <stdio.h>
#include <stdlib.h>

#define SIZE 5

int main(void)
{
    FILE *fp;
    int i, arr[SIZE] = {10, 20, 30, 40, 50};

    fp = fopen("test.bin", "w+b"); /* Open binary file for reading and writing */
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    fwrite(arr, sizeof(int), SIZE, fp);

    printf("Enter new value: ");
    scanf("%d", &i);
    fseek(fp, 2*sizeof(int), SEEK_SET); /* Since each integer is 4 bytes, fseek() moves the file pointer 2*sizeof(int) = 8 bytes from the beginning of the file to get to the third integer. */
    fwrite(&i, sizeof(int), 1, fp);

    fseek(fp, 0, SEEK_SET);
    if(fread(arr, sizeof(int), SIZE, fp) != SIZE)
    {
        fclose(fp);
        printf("Error: fread() failed\n");
        exit(EXIT_FAILURE);
    }
```

```
if(strcmp(str, tmp_str) == 0)
{
    found = 1;
    break;
}
}
if(found == 0)
    printf("\n%s isn't found\n", tmp_str);
else
    printf("\n%s is found\n", tmp_str);
fclose(fp);
return 0;
}
```

C.15.15 Suppose that the purpose of the following program is to write a string into a binary file, read it from the file, and display it. Is this code error-free?

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE* fp;
    char str1[5], str2[] = "test";

    if((fp = fopen("text.bin", "w+b")) != NULL)
    {
        fwrite(str2, 1, 4, fp);
        fread(str1, 1, 4, fp);
        printf("%s\n", str1);
        fclose(fp);
    }
    return 0;
}
```

**Answer:** As you guess, there are several errors. The first bug is that the file pointer is not rewinded to the beginning of the file before calling `fread()`. This bug is eliminated by adding:

```
fseek(fp, 0, SEEK_SET);
```

between `fwrite()` and `fread()`. Now, `fread()` reads successfully the four characters and stores them into `str1`. The second bug is that `str1` is not null terminated; therefore, `printf()` won’t work properly. To eliminate this bug, add this statement before `printf()`:

```
str1[4] = '\0';
```

or initialize `str1` like:

```
char str1[5] = {0};
```

C.15.16 Suppose that the test.bin binary file contains a student’s grades. The number of grades is declared in the beginning of the file. Write a program that reads the grades from the binary file (use the `float` type) and stores them in a dynamically allocated memory. Then, the program should read a number and display the grades greater than that number.

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
    int i, grd_num;
    float *grd_arr, grd;

    fp = fopen("test.bin", "rb");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    if(fread(&grd_num, sizeof(int), 1, fp) != 1)
    {
        fclose(fp);
        printf("Error: fread() failed\n");
        exit(EXIT_FAILURE);
    }
    grd_arr = (float*) malloc(grd_num * sizeof(float)); /* Allocate memory to store the grades. */
    if(grd_arr == NULL)
    {
        fclose(fp);
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    /* Read all grades and check if they are read successfully. */
    if(fread(grd_arr, sizeof(float), grd_num, fp) == grd_num)
    {
        printf("Enter grade: ");
        scanf("%f", &grd);
        for(i = 0; i < grd_num; i++)
            if(grd_arr[i] > grd)
                printf("%f\n", grd_arr[i]);
    }
    else
        printf("Error: fread() failed to read grades\n");

    free(grd_arr);
    fclose(fp);
    return 0;
}
```

C.15.17 A common method that antivirus software uses to identify viruses is signature-based detection. The signature is a sequence of bytes (e.g., F3 BA 20 63 7A 1B) that identify a particular virus. When a file is scanned, the antivirus software searches the

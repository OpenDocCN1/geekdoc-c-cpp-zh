
Let us compile and run the above program that will create a file **file.txt**, and then it will write following text line and finally it will close the file using **fclose()** function.

```
This is tutorialspoint.com
```

## void clearerr(FILE *stream)

### Description

The C library function **void clearerr(FILE *stream)** clears the end-of-file and error indicators for the given stream.

### Declaration

Following is the declaration for clearerr() function.

```c
void clearerr(FILE *stream)
```

### Parameters

- **stream** -- This is the pointer to a FILE object that identifies the stream.

### Return Value

This should not fail and do not set the external variable *errno* but in case it detects that its argument is not a valid stream, it must return -1 and set *errno* to EBADF.

### Example

The following example shows the usage of clearerr() function.

```c
#include <stdio.h>

int main()
{
   FILE *fp;
   char c;

   fp = fopen("file.txt", "w");

   c = fgetc(fp);
   if( ferror(fp) )
   {
      printf("Error in reading from file : file.txt\n");
   }

   clearerr(fp);
   if( ferror(fp) )
   {
      printf("Error in reading from file : file.txt\n");
   }
   fclose(fp);

   return(0);
}
```

Assuming we have a text file file.txt, which is an empty file, let us compile and run the above program, this will produce the following result because we try to read a file which we opened in write only mode.

```
Error reading from file "file.txt"
```

## int feof(FILE *stream)

### Description

The C library function int feof(FILE *stream) tests the end-of-file indicator for the given stream.

### Declaration

Following is the declaration for feof() function.

```c
int feof(FILE *stream)
```

### Parameters

- stream -- This is the pointer to a FILE object that identifies the stream.

### Return Value

This function returns a non-zero value when End-of-File indicator associated with the stream is set, else zero is returned.

### Example

The following example shows the usage of feof() function.

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    if(fp == NULL)
    {
        perror("Error in opening file");
        return(-1);
    }
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

Assuming we have a text file **file.txt**, which has the following content. This file will be used as an input for our example program:

```
This is tutorialspoint.com
```

Let us compile and run the above program, this will produce the following result:

```
This is tutorialspoint.com
```

## int ferror(FILE *stream)

### Description

The C library function **int ferror(FILE *stream)** tests the error indicator for the given stream.

### Declaration

Following is the declaration for ferror() function.

```c
int ferror(FILE *stream)
```

### Parameters

- **stream** -- This is the pointer to a FILE object that identifies the stream.

### Return Value

If the error indicator associated with the stream was set, the function returns a non-zero value else, it returns a zero value.

### Example

The following example shows the usage of ferror() function.

```c
#include <stdio.h>

int main()
{
    FILE *fp;
    char c;

    fp = fopen("file.txt", "w");

    c = fgetc(fp);
    if( ferror(fp) )
    {
        printf("Error in reading from file : file.txt\n");
    }

    clearerr(fp);
    if( ferror(fp) )
    {
        printf("Error in reading from file : file.txt\n");
    }
    fclose(fp);

    return(0);
}
```

Assuming we have a text file file.txt, which is an empty file. Let us compile and run the above program that will produce the following result because we try to read a file which we opened in write only mode.

```c
fprintf(stdout, "and this will appear when programm\n");
fprintf(stdout, "will come after sleeping 5 seconds\n");

sleep(5);

return(0);
}
```

Let us compile and run the above program that will produce the following result. Here program keeps buffering the output into buff until it faces first call to fflush(), after which it again starts buffering the output and finally sleeps for 5 seconds. It sends remaining output to the STDOUT before program comes out.

```
Going to set full buffering on
This is tutorialspoint.com
This output will go into buff
and this will appear when programm
will come after sleeping 5 seconds
```

## int fgetpos(FILE *stream, fpos_t *pos)

### Description

The C library function int fgetpos(FILE *stream, fpos_t *pos) gets the current file position of the stream and writes it to pos.

### Declaration

Following is the declaration for fgetpos() function.

```c
int fgetpos(FILE *stream, fpos_t *pos)
```

### Parameters

- stream -- This is the pointer to a FILE object that identifies the stream.
- pos -- This is the pointer to a fpos_t object.

### Return Value

This function returns zero on success, else non-zero value in case of an error.

### Example

The following example shows the usage of fgetpos() function.

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    fpos_t position;

    fp = fopen("file.txt","w+");
    fgetpos(fp, &position);
    fputs("Hello, World!", fp);

    fsetpos(fp, &position);
    fputs("This is going to override previous content", fp);
    fclose(fp);

    return(0);
}
```

Let us compile and run the above program to create a file **file.txt** which will have the following content. First of all we get the initial position of the file using **fgetpos()** function and then we write *Hello, World!* in the file, but later we have used **fsetpos()** function to reset the write pointer at the beginning of the file and then over-write the file with the following content:

This is going to override previous content

Now let us see the content of the above file using the following program:

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    int n = 0;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }

    fclose(fp);

    return(0);
}
```

## FILE *fopen(const char *filename, const char *mode)

### Description

The C library function FILE *fopen(const char *filename, const char *mode) opens the filename pointed to, by filename using the given mode.

### Declaration

Following is the declaration for fopen() function.

```c
FILE *fopen(const char *filename, const char *mode)
```

### Parameters

- **filename** -- This is the C string containing the name of the file to be opened.
- **mode** -- This is the C string containing a file access mode. It includes:

| mode | Description |
|------|-------------|
| "r" | Opens a file for reading. The file must exist. |
| "w" | Creates an empty file for writing. If a file with the same name already exists, its content is erased and the file is considered as a new empty file. |
| "a" | Appends to a file. Writing operations, append data at the end of the file. The file is created if it does not exist. |
| "r+" | Opens a file to update both reading and writing. The file must exist. |
| "w+" | Creates an empty file for both reading and writing. |
| "a+" | Opens a file for reading and appending. |

### Return Value

This function returns a FILE pointer. Otherwise, NULL is returned and the global variable errno is set to indicate the error.

### Example

The following example shows the usage of fopen() function.

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE * fp;

    fp = fopen ("file.txt", "w+");
    fprintf(fp, "%s %s %s %d", "We", "are", "in", 2012);

    fclose(fp);

    return(0);
}
```

Let us compile and run the above program that will create a file file.txt with the following content:

We are in 2012

Now let us see the content of the above file using the following program:

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
```

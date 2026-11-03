```
printf("%d\t",student.roll);
printf("%f\n",student.marks);
}
```

In this case, the last record of the program may be processed twice, since in C end of file is indicated only after an input function has made an attempt to read at the end of file.

# 11.14.2 ferror()

Declaration: int ferror(FILE *fptr);

The macro ferror() is used for detecting any error occurred during read or write operations on a file. It returns a nonzero value if an error occurs i.e. if the error indicator for that file is set, otherwise it returns zero.

```
/*P11.22 Program to understand the use of ferror()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int ch;
    fptr=fopen("test","w");
    ch=getc(fptr);
    if(ferror(fptr))
    {
        printf("Error in read operation\n");
        exit(1);
    }
    else
        printf("%c",ch);
    fclose(fptr);
}
```

# Output:

Error in read operation

Here the file is opened in write mode and an attempt is made to read from the file, this gives an error which is detected by ferror().

Generally the return value of the input function is checked to stop reading from the file. Almost all input functions return same value on end of file and on error, so to distinguish between these two cases, the functions feof() and ferror() are used.

```
/*P11.23 Program to understand the use of feof() and ferror()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int ch;
    if((fptr=fopen("myfile.c","r"))==NULL)
    {
        printf("File doesn't exist\n");
        exit(1);
    }
    else
```
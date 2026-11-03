# 11.9 Integer I/O

# 11.9.1 putw ()

Declaration: int putw(int value, FILE *fptr)

This function writes an integer value to the file pointed to by fptr. It returns the integer written to the file on success, and EOF on error.

```
/*P11.3 Program to understand the use of putw() function*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int value;
    fptr=fopen("num.dat","wb");
    for(value=1;value<=30;value++)
        putw(value,fptr);
    fclose(fptr);
}
```

This program will write integers from 1 to 30 into the file "num.dat".

# 11.9.2 getw ()

Declaration: int getw( FILE *fptr );

This function returns the integer value from the file associated with fptr. It returns the next integer from the input file on success, and EOF on error or end of file.

```
/*P11.4 Program to understand the use of getw() function*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int value;
    fptr=fopen("num.dat","rb");
    while((value=getw(fptr))!=EOF)
        printf("%d\t",value);
    fclose(fptr);
}
```

This program will read and print integers from the file "num.dat" which was created earlier.

If getw() is used with text files then it will stop reading if integer 26 is present in the file because in text files end of file is denoted by ASCII 26 which is also a valid integer value. So getw() should not be used with text files.

The value of EOF is -1 which is a valid integer value, so this program will work correctly if -1 is not present in file, if -1 exists in the file then getw() will stop reading and all the values beyond -1 will be left unread. So we should use feof() to check end of file and ferror() to check error. These functions are discussed later in this chapter.
In Listing 5.20, we have tried to read an entire sentence from a file. First, we have opened the file in the read-only mode and then read an entire sentence from the file using the fgets() function.

Output of the preceding program is as follows:

```
```
THIS IS HOW WE READ SENTENCE FROM A FILE.
```
```

In the next section, let's learn how to create a file.

# Creating a File

A file needs to be created before it can be processed. A text file or stream-oriented file can be created in two ways. It can be created either with the help of some external word processor or by writing some program that writes information into a data file. Unformatted files can only be created with the help of programs. Listing 5.21 shows how to create a file:

Listing 5.21: Creating a File

```
```c
#include<stdio.h>

    int main()
    {
        char ch='A';
        FILE *fp;

        fp = fopen("D:\\create_readme.txt","w");

        if(!fp)
        {
            printf("\n Failed to open the file");
            return 0;
        }

        putc(ch, fp);
        fclose(fp); /* For closing the file pointer */
        getch();

        return 0;
    }
```
```

The preceding program creates a data file in the write mode. Next, let's learn how to write to a file.

# Writing to a File

After opening a file in the write mode (which is done by using "w" in the fopen() function), a user can write information in the file by using the functions, such as fputc() and fputs(). The fputc() function allows a user to write characters in a file; whereas, the fputs() function allows a user to have multi-line writes to a file. Listing 5.22 shows how to write to a file by using the fputc() function:

Listing 5.22: Writing to a File

```
```c
#include<stdio.h>

    int main()
    {
        char character;
        FILE *fp,*fd;

        fp = fopen("D:\\readme.txt", "r");
        fd = fopen("D:\\readme_new.txt", "w");

        if(!fp)
```
```
```
}
```

# Closing a file:

When we have finished reading the file, we need to close it. This is done by fclose(). This is used as; fclose(fp);

To close the file we do not need the filename. The fclose() function performs three main tasks.

+   1. The characters in the buffer would be written to the file on the disk.
+   2. At the end of file a character with ASCII value 26 would get written.
+   3. The buffer gets eliminated from the file.

1. Write a program to count the number of characters, spaces, tab, new lines in a file.

```
#include<stdio.h>
main()
{
FILE *fp;
char ch;
int lines=0,tab=0,space=0,characters=0;
fp=fopen("text.c","r");
while(1) /* infinite loop*/
{
ch = fgetc(fp);
if(ch == EOF)
break;
characters++;
if(ch == 32)
space++;
if(ch == '\n')
lines++;
if(ch == '\t')
tab++;
}

```
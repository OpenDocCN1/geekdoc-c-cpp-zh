}

# ********************
** file Handling **
********************

# 109. Wap to read a line of text from screen and store in to File.

```
#include<stdio.h>
#include<conio.h>
#include<stdlib>
#include<string.h>
void main()
{
    FILE *fp;
    char str[20];
    fp=fopen("sample.txt","w");
    printf("\n Enter a line of text");
    gets(str);
    fprintf(fp,"%s",str);
    fclose(fp);
    getch();
}
```

# 110. Wap to read a line of text from a file and Display it.

```
#include<stdio.h>
#include<conio.h>
#include<stdlib>
#include<string.h>
void main()
{
    FILE *fp;
    char str[20];
    fp=fopen("sample.txt","r");
    if(fp==null)
    {
```
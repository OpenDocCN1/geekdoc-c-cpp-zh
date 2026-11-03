```
```c
fclose(ft);
fs=fopen("Source2.txt","r");/*Opening the 2nd source file*/
if(fs==NULL)
{
printf("Cannot open source file");
exit(1);
}
ft=fopen("Target.txt","r+");/*Opening the target file again*/
if(ft==NULL)
{
printf("Cannot open target file");
fclose(fs);
exit(0);
}
fseek(ft,0L,2);/*Using fseek to move to the end of the file*/
for(;fscanf(fs,"%d",&c)!=EOF;)/*Reading integers from file*/
fprintf(ft," %d",c);/*Writing integers to the file*/
/*Closing the file streams*/
fclose(fs);
fclose(ft);
printf("Files merged successfully; you can check the output by opening Target.txt file");
getch();
}
```
```

# Output

Files merged successfully; you can check the output by opening Target.txt file

# EXAMPLE A.79 Write a program to open a file using command line arguments and display its contents.

# Program

```
```c
/* Program for demonstrating the use of command line arguments*/
/*Program file name: fileopen.c*/
/*Assuming source file Source.txt is placed inside the ../bin/ location*/
#include <stdio.h>
#include <conio.h>
void main(int argc, char *argv[])
{
char ch;
FILE *fp;
if(argc!=2)/*Checking the number of arguments given at command line*/
{
printf("Usage: fileopen <filename>");
exit(0);
}
fp=fopen(argv[1],"r");
if(fp==NULL)
{
printf("Cannot open the file");
exit(0);
}
while((ch=fgetc(fp))!=EOF)
{
printf("%c",ch);
}
fclose(fp);
}
```
```
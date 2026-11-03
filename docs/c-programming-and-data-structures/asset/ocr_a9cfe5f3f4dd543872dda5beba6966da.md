# EXAMPLE A.76 Write a program to read a list of integers from one file and copy the same in reverse order in another file.

```
Program
/*Program for demonstrating the use of getw and putw*/
#include <stdio.h>
#include <conio.h>
/*
This program uses source file named S1, which contains the following elements:
1
2
3
4
5
*/
void main()
{
FILE *fs,*ft,*fp;/*Declaring file access pointers*/
int i,j,arr[10],num;
clrscr();
fs = fopen("S1","r");/*Opening the source file in read mode*/
if (fs==NULL)
{
printf("Source file cannot be opened.");
exit(0);
}
ft = fopen("S2","w");/*Opening the destination file in write mode*/
if (ft==NULL)
{
printf("Target file cannot be opened.");
fclose(fs);
exit(0);
}
i=0;
while((arr[i]=getw(fs))!=EOF)/*Reading integers from source file and storing them in array arr[]*/
i=i+1;
fclose(fs);
for(j=i-1;j>=0;j--)
putw(arr[j],ft);/*Copying the source integer list into target file in reverse order*/
fclose(ft);
/*Verifying the contents of the target file*/
fp = fopen("T2","r");
if (fp==NULL)
{
printf("Target file cannot be opened.");
```
You can read and write streams to a file using the fread() and fwrite() functions provided by C. As an example, consider the following code.

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
struct employee
{
char name[25];
char phone;
int employee[3];
} employee *fptr;
FILE *fptr;
int num,i;
fptr=fopen("hello.txt","ab+");//opening file in binary mode
clrscr();    //to write records
if (fptr==NULL)
{
printf("The file does not exist");
exit(1);
}
else
{
printf("How many records do you want to enter\n");
scanf("%d", &num);
printf("Enter the names and phone numbers\n");
for(i=0;i<num;i++)
{
scanf("%s %d", &employee[i].name, &employee[i].phone);
}
printf("Adding records to a file\n");
i=0;
do
{
fwrite(&employee, sizeof(employee),1,fptr);
i++;
}
while(i<num);
fclose(fptr);
i=0;
fptr=fopen("hello.txt","rb"); //opening file in binary
// mode to read records
printf("records entered are\n");
do
{
fread(&employee, sizeof(employee), 1, fptr);
printf("%s %d", employee[i].name, employee[i].phone);
i++;
}
while(i<num);
fclose(fptr);
getch();
}
}
```
```

Fig. 13.2 C program using streams
```
#include<stdio.h>
#include<conio.h>
Struct book
{
char name[10];
int pages;
float price;
};
void main()
{
struct book b;

printf("\n Enter information about book");

printf("\n Enter Name  of the book");
gets(b.name);

printf("\n Enter total pages and price of the book");
scanf("%d%f",&b.pages,&b.price);

printf("\n Displaying information about book");
printf("\n name =%s",b.name);
printf("\n pages=%d",b.pages);
printf("\n price=%d",b.price);
getch();
}
```

# 103. Wap to create a structure of student, read info. of ten students and print name of those students whose marks is grater then 90.

```
#include<stdio.h>
#include<conio.h>
Struct student
{
char name[10];
int r_no;
float marks;
};
```
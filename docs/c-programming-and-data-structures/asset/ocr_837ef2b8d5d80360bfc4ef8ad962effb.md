# A.2 Computer Programming

```
```c
void main()
{
int dd,mm,yyyy;
clrscr();
printf("Enter the date in dd mm yyyy format ");
scanf("%d %d %d", &dd, &mm, &yyyy); /*Reading the date values*/
/*Checking whether day, month, and year is correct */
if((dd==1 || dd==31 || mm==1 || mm==12 || yyyy==0 || (mm==2 && dd==29))
printf("NO");
else
printf("YES");
}
getch();
```
```

Output
Enter the date in dd mm yyyy format 22 09 2001
YES

# EXAMPLE A.3 Write a program to determine whether an input number is even or odd.

```
```c
/*Program for demonstrating use of Modulo Division Operator */
/*include <stdio.h> */
/*include <conio.h> */
void main()
{
int num;
clrscr();
printf("\nEnter a number : ");
scanf("%d",&num); /*Reading an Integer*/
if(num%2==0) /*Using % operator to compute the remainder value*/
printf("\n%d is an even number",num);
else
printf("\n%d is an odd number",num);
getch();
}
```
```

Output
Enter a number: 55
55 is an odd number
# 8. /* Write a C program to generate all the prime numbers between 1 and n, where n is a value supplied by the user by using C99 standards.(long long int,declare variables with in for loop) */

```
#include <stdio.h>

void main()
{
long long int no,check;   // long long int
clrscr();
printf("<-----------------------------PRIME NO. SERIES--------------------------");
printf("-->");
printf("\n\n\n\t\tINPUT THE VALUE OF N: ");
scanf("%ld",&no);
printf("\n\n\nTHE PRIME NO. SERIES B/W 1 TO %lld : \n\n",no);

for(int counter = 1; counter <= no; counter++)   // declare counter with in for
{
check = 0;
//THIS LOOP WILL CHECK A NO TO BE PRIME NO. OR NOT.

for(int counter1 = counter-1; counter1 > 1 ; counter1--)
if(counter%counter1 == 0)
{
check++;      // INCREMENT CHECK IF NO. IS NOT A PRIME NO.
break;
}
if(check == 0)
printf("%d\t",counter);
}
getch();
}
```

# 9. /* Write a program to print text and numbers by using C99 standards */

```
#include<stdio.h>
int main(void)
{
printf("%-20s","this is a test"); // left justified
printf("%10.3f",12.234657);
return 0;
}
```
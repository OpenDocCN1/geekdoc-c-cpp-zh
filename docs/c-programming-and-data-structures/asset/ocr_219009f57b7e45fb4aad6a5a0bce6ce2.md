# EXAMPLE A.51 Write a program to generate the one's complement of a given binary number.

# Program

```
/*Program for demonstrating the passing of a string as a parameter to a function*/
#include <stdio.h>
#include <conio.h>

char b[16]; /*array for storing the result of one's complement*/

void main()
{
char a[16];
int i;
void ones(char[]); /*Declaring the function prototype for generating one's complement*/
clrscr();

printf("Enter a binary number: ");
gets(a);/*Reading the input binary number*/

ones(a); /*Calling the function by passing input binary string a*/

printf("\nThe 1's compliment of %s is %s", a,b); /*Displaying the result*/
getch();
}

void ones(char str[])
{
int i;
char c[16];
for(i=0;str[i]!='\0'; i++)
{
if (str[i]!='0' && str[i]!='1')
{
printf("\nincorrect binary number format...the program will quit");
getch();
exit(0);
}
/*Changing the binary digits from 0 to 1 and vice versa*/
if (str[i]=='0')
b[i]='1';
else
b[i]='0';
}
b[i]='\0';
}
```

# Output

Enter a binary number: 11001001

The 1's compliment of 11001001 is 00110110
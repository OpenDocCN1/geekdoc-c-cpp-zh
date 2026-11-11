test fails & so the loop finishes. The program proceeds with the statements after the loop.

# Programming Problems

# Problem 1

Write a program to print only the numbers from 1 to 100 with the help of while loop.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
i=1;
while(i<=100)
{
printf("\n %d",i);
i++;
}
getch();
}
```
```

# Problem 2

Write a program to print the numbers from 100 to 1 with the help of while loop.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
i=100;
while(i>=1)
{
printf("\n %d",i);
i--;
}
getch();
}
```
```

# Problem 3

Write a program to print only the even numbers from 1 to 100 with the help of while loop.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
```
```

```
```c
void main()
{
int i;
i=1;
while(i<=100)
{
if(i%2==0)
printf("\n %d",i);
i++;
}
getch();
}
```
```

# Problem 4

Write a program to print only the odd numbers from 1 to 100 with the help of while loop.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
i=1;
while(i<=100)
{
if(i%2==1)
printf("\n %d",i);
i++;
}
getch();
}
```
```

# Problem 5

Program for generating ‘N’ natural numbers using while loop:

# Solution

```
```c
# include < stdio.h > // include the stdio.h file
void main() // Start of your program
{
int n, i=0; //Declare and initialize the variables
printf("Enter the upper limit number"); // Message to the user
scanf("%d", &n); //read and store the number
while(i<=n) // While statement with condition
{ // Body of the loop
printf("%d",i); // print the value of i
I++; // increment I to the next natural number.
```
```
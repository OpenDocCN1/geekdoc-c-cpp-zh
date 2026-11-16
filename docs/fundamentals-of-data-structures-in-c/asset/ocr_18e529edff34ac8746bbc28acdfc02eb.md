```
s = squares(i);
sum += s;
printf("Square of %d is %d", i, s);
}
printf("\nSum of the squares is %d", sum);
}
int squares(int b)
{
return(b * b);
}
```

```
The program displays the following output
Enter the limit : 5
Square of 1 is 1
Square of 2 is 4
Square of 3 is 9
Square of 4 is 16
Square of 5 is 25
Sum of the squares is 55
```

# Program S13:

Write a program to check whether the given number is palindrome or not.

```
/* palinnum.c */
#include<stdio.h>
#include<stdlib.h>
void main()
{
long int a = 0, b = 0, c = 0, d = 0, e = 0;
printf("Enter the number : ");
scanf("%d", &a);
e = a;
while(a > 0)
{
b = a % 10;
c = c + b;
a = a / 10;
d = b + d * 10;
}
if(e == d) /* check whether the reverse and the original number are equal */
printf("%d is a Palindrome number", e);
else
printf("%d is not a Palindrome number", e);
}
```
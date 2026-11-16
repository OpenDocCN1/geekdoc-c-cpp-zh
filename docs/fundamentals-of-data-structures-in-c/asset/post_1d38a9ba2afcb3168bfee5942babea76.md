
less than zero and the condition in the else block (i.e., the printf() function) is executed and displays the message

String Yuvaraj is greater than string Jebaraj

Note that the value returned by the strcmp() function is usually the difference between the ascii values of the unequal characters of the first mismatch between the two strings.

## 1.16.5 The strrev() function

The strrev() (string reverse) function is used to reverse a string. This function takes only one argument. The general form or the syntax of strrev() function is

```
x = strrev(string);
```

where x is the string variable to hold the reversed string and string is the valid string variable or a string constant which stores the string to be reversed. Program 1.21 helps you to understand things better.

### Program 1.21 :

```
/* strrev.c */ #include<stdio.h> #include<string.h> void main() { char x[20]; printf("Enter the string : "); gets(x); printf("The reversed string is : %s", strrev(x)); }
```

The program displays the following output

RUN1 Enter the string : Aravind The reversed string is : ndivrA RUN2 Enter the string : Gayathri Devi The reversed string is : iveD irhtayagA

In Program 1.21 the input string is stored in the array x and is passed as an argument to the strrev() function which reverses the string and displays the output.

Note that the space in between the strings is also reversed in the above output.

## 1.16.6 The strlwr() function

The strlwr() (string lower) function is used to convert a string to lowercase. This function takes only one argument. The general form or the syntax of strlwr() function is

```
x = strlwr(string);
```

where x is the string variable to hold the lowercase converted string and string is the valid string or constant which contains the string (uppercase). Program 1.22 helps you to understand things better.

### Program 1.22 :

```
/* strlwr.c */
#include<stdio.h>
#include<string.h>
void main()
{
 char x[20];
 printf("Enter the string : ");
 gets(x);
 printf("The case changed string is : %s", strlwr(x));
 }
```

The program displays the following output

RUN1 Enter the string : PRAMILA
The case changed string is : pramila
RUN2 Enter the string : ZaHiRa
The case changed string is : zahira

In Program 1.22 function strlwr() changes the uppercase letters to its lowercase and displays the output. If the input string entered is in uppercase, the compiler gives no error and automatically displays the output. Note that for each program in this chapter we have included #include<string.h>, because all the string functions are pre-defined in the header file string.h.

## 1.17 Simple Programs

### Program S1 :

Write a program for swapping (interchanging) two numbers (using three variables).

```
/* swap1.c */
#include<stdio.h>
void main()
{
int a, b, c;
printf("Enter two numbers : ");
scanf("%d %d", &a, &b);
printf("Before swapping . . \n");
printf("A = %d B = %d", a, b);
c = a;
a = b;
b = c;
printf("After swapping . . \n");
printf("A = %d B = %d", a, b);
}
```

The program displays the following output

Enter two numbers : 90 70
Before swapping . .
A = 90 B = 70
After swapping . .
A = 70 B = 90

### Program S2 :

Write a program for swapping (interchanging) two numbers (using two variables).

```
/* swap2.c */
#include<stdio.h>
void main()
{
int a, b;
printf("Enter two numbers : ");
scanf("%d %d", &a, &b);
printf("Before swapping . . \n");
printf("A = %d B = %d", a, b);
a = a + b;
b = a - b;
a = a - b;
printf("After swapping . . \n");
printf("A = %d B = %d", a, b);
}
```

The program displays the following output

Enter two numbers : 23 54
Before swapping . .
A = 23 B = 54
After swapping . .
A = 54 B = 23

### Program S3:

Write a program for swapping two numbers without using arithmetic operators.

```
/* swap3.c */
#include<stdio.h>
void main()
{
 int a, b;
 printf("Enter two numbers : ");
 scanf("%d %d", &a, &b);
 printf("Before swapping . . \n");
 printf("A = %d B = %d", a, b);
 a = a ^ b;
 b = a ^ b;
 a = a ^ b;
 printf("\nAfter swapping . . \n");
 printf("A = %d B = %d", a, b);
}
```

The program displays the following output

Enter two numbers : 90 70
Before swapping . .
A = 90 B = 70
After swapping . .
A = 70 B = 90

### Program S4:

Write a program to convert temperature in centigrade to fahrenheit.

```
/* temp_f_c.c */
#include<stdio.h>
void main()
{
 float cent, fahren;
 printf("Enter temperature in centigrade : ");
 scanf("%f", &cent);
 fahren = (1.8 * cent + 32);
/* cent = (fahren - 32) / 1.8; for converting temperature in fahrenheit to centigrade */
 printf("The temperature in fahrenheit is %.2f", fahren);
}
```

The program displays the following output

Enter temperature in centigrade : 45
The temperature in fahrenheit is 113.00

### Program S5 :

Write a program to find the maximum of three numbers using an if statement.

```
/* max1_f.c */
#include<stdio.h>
void main()
{
 float a, b, c, max;
 printf("Enter three numbers : ");
 scanf("%f %f %f", &a, &b, &c);
 max = a;
 if (b > max)
     max = b;
 if (c > max)
     max = c;
 printf("Largest of three numbers is %.2f", max);
}
```

The program displays the following output

Enter three numbers : 45.75 65.00 34.998
Largest of three numbers is 65.00

### Program S6 :

Write a program to find whether the given number is odd or even.

```
/* odd_even.c */
#include<stdio.h>
void main()
{
    int num;
    printf("Enter the number : ");
    scanf("%d", &num);
    if (num % 2 == 1)    /* find the modulus of the number */
        printf("The number is odd");
    else
        printf("The number is even");
}
```

The program displays the following output

RUN1 Enter the number : 46
    The number is even
RUN2 Enter the number : 73
    The number is odd

### Program S7 :

Write a program to find simple and compound interest.

```
/* sim_com.c */
#include<stdio.h>
void main()
{
    int n;
    float p, r, dur, simple, compound, total;
    printf("Enter principal,rate,no.of.years,compounding/year \n");
    scanf("%f %f %d %d", &p, &r, &dur, &n);
    simple = (p * dur * r) / 100;
    printf("Simple Interest is %.2f", simple);
    total = p * pow((double) (1+r/(n*100)), (double) (n*dur));
    compound = total - p;
    printf("Compound Interest is %.2f", compound);
}
```

The program displays the following output

Enter principal,rate,no.of.years,compounding/year
34 124 5 6
Simple Interest is 210.80
Compound Interest is 8636.00

### Program S8 :

Write a program to find whether the given year is leap or not.

```
/* leapyear.c */
#include<stdio.h>
void main()
{
 int x;
 printf("Enter the year : ");
 scanf("%d",&x);
 if ((x % 4 == 0) && (x % 100 == 0) || (x % 400 != 0))
 printf("%d is a leap year", x);
 else
 printf("%d is not a leap year", x);
}
```

The program displays the following output

RUN1 Enter the year : 1999
1999 is not a leap year
RUN2 Enter the year : 2000
2000 is a leap year

### Program S9 :

Write a program to find the factorial of a given number.

```
/* factorial.c */
#include<stdio.h>
void main()
{
 long i, j, x = 1;
 printf("Enter the number : ");
 scanf("%d",&i);
 for (j = 1 ; j <= i ; j++)
 x = j * x;
 printf("Factorial value of %d is %d", i, x);
}
```

The program displays the following output

Enter the number : 5
Factorial value of 5 is 120

### Program S10 :

Write a program to find the sum of digits of an integer.

```
/* digitsum.c */
#include<stdio.h>
void main()
{
 long x, y = 0, z = 0;
 printf("Enter the number : ");
 scanf("%ld", &x);
 while (x > 0)
{
 y = x % 10;
 z = z + y;
 x = x / 10;
}
printf("The sum of the digits in the integer is %ld", z);
}
```

The program displays the following output

Enter the number: 1234
The sum of the digits in the integer is 10

### Program S.11 :

Write a program to find the average of first 'n' natural numbers using gauss method

```
/* ave_gaus.c */
#include<stdio.h>
void main()
{
 int n;
 float sum = 0, i, ave;
 printf("Enter a number : ");
 scanf("%d", &n);
 for(i = 1 ; i <= n ; i++)
 {
 sum = sum + i;
 }
 ave = (float)sum / (float)n; /* type casting */
 printf("Average of %2d numbers is %.2f\n", n, ave);
 printf("Average by gauss method is %.2f", ((float)n*((float)n+1.0)/2.0)/(float)n);
}
```

The program displays the following output

Enter a number : 12
Average of 12 numbers is 6.50
Average by gauss method is 6.50

### Program S.12 :

Write a program using functions to find the square of first N numbers and to calculate its sum.

```
/* square.c */
#include<stdio.h>
int squares(int);
void main()
{
 int i, n, s, sum = 0;
 printf("Enter the limit : ");
 scanf("%d", &n);
 for(i = 1 ; i <= n ; i++)
 {
```

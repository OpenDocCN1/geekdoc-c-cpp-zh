![](images/00001.jpeg)

© Copyright 2016 by Rohit Gupta- All rights reserved.

This book is copyright protected. This is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part or the content within this book without the consent of the author or copyright owner.

Except as permitted under India Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

This book is a work of pure practical knowledge. Any resemblance to other book is entirely coincidental.

Table of Contents

[1\. Write a program to perform addition, subtraction, multiplication and division.](#part0000_split_002.html__Toc447016990)

[2\. How to add two numbers without using the plus operator?](#part0000_split_003.html__Toc447016991)

[3\. How to subtract two numbers without using the subtraction operator ?](#part0000_split_004.html__Toc447016992)

[4\. Write a program for swapping of two numbers.](#part0000_split_005.html__Toc447016993)

[5\. Write a program to add digits of a number or calculate sum of digits.](#part0000_split_006.html__Toc447016994)

[6\. Write a program to print complex number.](#part0000_split_007.html__Toc447016995)

[7\. Write a program to check whether input alphabet is a vowel or not.](#part0000_split_008.html__Toc447016996)

[8\. Write a program to check if given integer is positive or negative.](#part0000_split_009.html__Toc447016997)

[9\. Write a program to find the area of a trapezium.](#part0000_split_010.html__Toc447016998)

[10\. Write a program for swapping of two numbers using function (call by value).](#part0000_split_011.html__Toc447016999)

[11\. Write a program to find greatest number between three numbers.](#part0000_split_013.html__Toc447017000)

[12\. Write a program to find greatest number among four numbers by ternary operator.](#part0000_split_014.html__Toc447017001)

[13\. Write a program to find smallest number among four numbers by using ternary operator.](#part0000_split_015.html__Toc447017002)

[14\. Write a program to find largest element using dynamic memory allocation.](#part0000_split_016.html__Toc447017003)

[15\. Write a program to print perfect numbers from 1 to 100.](#part0000_split_017.html__Toc447017004)

[16\. Write a program to reverse a given number.](#part0000_split_018.html__Toc447017005)

[17\. Write a program to find generic root of number or sum of digits of a number unit we don't get a single digit.](#part0000_split_019.html__Toc447017006)

[18\. Write a Program to print numbers from 1 to n numbers without using loop.](#part0000_split_021.html__Toc447017007)

[19\. Write a program to find the sum of first n natural numbers using For loop.](#part0000_split_022.html__Toc447017008)

[20\. Write a program to check whether a number is even or odd.](#part0000_split_023.html__Toc447017009)

[21\. Write a program to calculate the sum of odd & even numbers upto n numbers.](#part0000_split_024.html__Toc447017010)

[22\. Write a program to check whether a number is strong or not.](#part0000_split_025.html__Toc447017011)

[23\. Write a program of simple bubble sort implementation using array ascending order.](#part0000_split_026.html__Toc447017012)

[24\. How to calculate power of a number in C.](#part0000_split_027.html__Toc447017013)

[25\. Write a program to check whether a year is leap year or not.](#part0000_split_028.html__Toc447017014)

[26\. Write a program to find HCF and LCM of numbers.](#part0000_split_029.html__Toc447017015)

[27\. Write a program to print multiplication table.](#part0000_split_031.html__Toc447017016)

[28\. Write a program to print prime numbers between 1-200 using break and continue.](#part0000_split_033.html__Toc447017017)

[29\. Write a program to check whether a number is prime number or not.](#part0000_split_034.html__Toc447017018)

[30\. Write a program to find prime factor of number.](#part0000_split_036.html__Toc447017019)

[31. Write a program to find factorial of a number.](#part0000_split_037.html__Toc447017020)

[32\. Write a program to print Fibonacci series.](#part0000_split_038.html__Toc447017021)

[33\. Write a program to print Armstrong numbers from 1 to 500.](#part0000_split_039.html__Toc447017022)

[34\. Write a program to check whether a number is Armstrong number or not.](#part0000_split_040.html__Toc447017023)

[35\. Write a program to check whether a number is Prime or Armstrong number using user-defined function.](#part0000_split_041.html__Toc447017024)

[36\. Write a program to check whether a number can be express as sum of two prime numbers.](#part0000_split_042.html__Toc447017025)

[37\. Write a program to check whether a number is palindrome or not.](#part0000_split_043.html__Toc447017026)

[38\. Write a program to reverse a number and check if it is a palindrome.](#part0000_split_044.html__Toc447017027)

[39\. Write a program to find out the sum of in A.P. series.](#part0000_split_045.html__Toc447017028)

[40\. Write a program to find out the sum of G.P series.](#part0000_split_046.html__Toc447017029)

[41\. Write a program to find out the sum of infinite G.P. series.](#part0000_split_047.html__Toc447017030)

[42\. Write a program to find out the sum of series 1 + 2 + …. + n.](#part0000_split_048.html__Toc447017031)

[43\. Write a program to find out the sum of series 1^3 + 2^3 + …. + n^3.](#part0000_split_049.html__Toc447017032)

[44\. Write a program to find roots of a quadratic equation.](#part0000_split_050.html__Toc447017033)

[45\. Write a program to print rectangle pyramid of numbers.](#part0000_split_051.html__Toc447017034)

[46\. Write a program to print numerical as Pascal’s triangle pattern.](#part0000_split_052.html__Toc447017035)

[47\. Write a program to print “*” as inverted Pascal’s triangle pattern.](#part0000_split_053.html__Toc447017036)

[48\. Write a program to print numerical as Floyd’s triangle pattern.](#part0000_split_055.html__Toc447017037)

[49\. Write a program to print character as Floyd’s triangle pattern.](#part0000_split_057.html__Toc447017038)

[50\. Write a program to print “*” as inverted Floyd’s triangle pattern.](#part0000_split_058.html__Toc447017039)

[51\. Write a program to print diamond pattern.](#part0000_split_059.html__Toc447017040)

[52\. Write a program to search an element in an array using binary search.](#part0000_split_060.html__Toc447017041)

[53\. Write a program for binary to decimal conversion.](#part0000_split_061.html__Toc447017042)

[54\. Write a program for decimal to octal converter.](#part0000_split_062.html__Toc447017043)

[55\. How to convert large binary number to hexadecimal.](#part0000_split_063.html__Toc447017044)

[56\. Write a program for hexadecimal to binary conversion.](#part0000_split_064.html__Toc447017045)

[57\. Write a program to convert octal number to decimal number.](#part0000_split_065.html__Toc447017046)

[58\. Write a program to covert each digits of a number in English word.](#part0000_split_066.html__Toc447017047)

[59\. Write a program for multiplication of two binary numbers.](#part0000_split_067.html__Toc447017048)

[60\. Write a program which prints initial of any name.](#part0000_split_068.html__Toc447017049)

[61\. Write a program for addition of matrices.](#part0000_split_069.html__Toc447017050)

[62\. Write a program to find sum of diagonal elements of a matrix.](#part0000_split_070.html__Toc447017051)

[63\. Write a program to check whether two matrices are equal or not.](#part0000_split_071.html__Toc447017052)

[64\. Write a program to check whether a given matrix is identity matrix or not.](#part0000_split_072.html__Toc447017053)

[65\. Write a program to check whether a given matrix is a sparse matrix or dense matrix.](#part0000_split_073.html__Toc447017054)

[66\. Write a program to calculate sum of the elements of each row and column.](#part0000_split_074.html__Toc447017055)

[67\. Write a program to find the frequency of Odd and Even numbers in the given matrix.](#part0000_split_075.html__Toc447017056)

[68\. Write a program for swapping of two arrays.](#part0000_split_076.html__Toc447017057)

[69\. Write a program to print lower triangular matrix.](#part0000_split_077.html__Toc447017058)

[70\. Write a program to print upper triangular matrix.](#part0000_split_078.html__Toc447017059)

[71\. Write a program for multiplication of two matrices.](#part0000_split_079.html__Toc447017060)

[72\. Write a program to find inverse of a matrix.](#part0000_split_081.html__Toc447017061)

[73\. Write a program to find transpose of matrix.](#part0000_split_082.html__Toc447017062)

[74\. Write a program to find determinant of a matrix.](#part0000_split_084.html__Toc447017063)

[75\. Write a program to find the largest element in an array.](#part0000_split_086.html__Toc447017064)

[76\. Write a program to find the second largest element in an array.](#part0000_split_087.html__Toc447017065)

[77\. Write a program to find the second smallest element in an array.](#part0000_split_088.html__Toc447017066)

[78\. Write a program to insert an element in an array at desired position.](#part0000_split_089.html__Toc447017067)

[79\. Write a program to remove duplicate elements in an array.](#part0000_split_091.html__Toc447017068)

[80\. Write a program to delete an element at desired position from an array.](#part0000_split_092.html__Toc447017069)

[81\. Write a program to compare two strings using “strcmp” functions.](#part0000_split_093.html__Toc447017070)

[82\. Write a program to compare two strings without using string functions.](#part0000_split_094.html__Toc447017071)

[83\. Write a program to find length of string using “strlen” function.](#part0000_split_095.html__Toc447017072)

[84\. Write a program to find length of string without using library function.](#part0000_split_096.html__Toc447017073)

[85\. Write a program to copy string using “strcpy” library function.](#part0000_split_097.html__Toc447017074)

[86\. Write a program to copy string without using strcpy library function.](#part0000_split_098.html__Toc447017075)

[87\. Write a program to reverse a string using “strrev” library function.](#part0000_split_099.html__Toc447017076)

[88\. Write a program to reverse a string without using strrev library function.](#part0000_split_100.html__Toc447017077)

[89\. Write a program for Swapping of strings.](#part0000_split_101.html__Toc447017078)

[90\. Write a Program to sort a string in alphabetic order.](#part0000_split_103.html__Toc447017079)

[91\. Write a program to find palindrome of string.](#part0000_split_104.html__Toc447017080)

[92\. Write a program to find palindrome of string without using string function.](#part0000_split_105.html__Toc447017081)

[93\. Write a program for String concatenation using “strcat” string functions.](#part0000_split_107.html__Toc447017082)

[94\. Write a program for String concatenation without using string functions.](#part0000_split_108.html__Toc447017083)

[95\. Write a program to check whether entered character is uppercase letter or not without using library function.](#part0000_split_109.html__Toc447017084)

[96\. Write a program for Conversion from uppercase to lower case.](#part0000_split_111.html__Toc447017085)

[97\. Write a program to delete vowels from string.](#part0000_split_112.html__Toc447017086)

[98\. Write a program to count number of capital letters, small letter, digits, special symbol at given string.](#part0000_split_113.html__Toc447017087)

[99\. Write a program to find number of vowels, consonants, digits and white space.](#part0000_split_115.html__Toc447017088)

[100\. Write a program to check whether two strings are anagrams or not.](#part0000_split_116.html__Toc447017089)

[101\. Write a program to remove all characters in second string which are present in first string.](#part0000_split_117.html__Toc447017090)

[102\. Write a program to reverse a string using both recursion and iteration.](#part0000_split_118.html__Toc447017091)

[103\. Write a program will accept Year, Month and Date from the user and will display the day of the month.](#part0000_split_119.html__Toc447017092)

[104\. Write a program to convert string into ASCII values.](#part0000_split_120.html__Toc447017093)

[105\. Write a program to convert from roman numbers to english numbers.](#part0000_split_121.html__Toc447017094)

[106\. Write a program to convert any number to english word.](#part0000_split_122.html__Toc447017095)

[107\. Write a program to add two numbers using pointer.](#part0000_split_123.html__Toc447017096)

[108\. Write a program to add two numbers using call by reference.](#part0000_split_124.html__Toc447017097)

[109\. Write a program for swapping to variables using pointer (call by reference).](#part0000_split_125.html__Toc447017098)

[110\. Write a program to compute sum of the array elements using pointers.](#part0000_split_127.html__Toc447017099)

[111\. Write a program to find size of structure data type without using size of operator.](#part0000_split_128.html__Toc447017100)

[112\. Write a program to store and display information of single student using structure.](#part0000_split_129.html__Toc447017101)

[113\. Write a program to read and print details of 50 students using structure.](#part0000_split_130.html__Toc447017102)

[114\. Write a program to store information using structure with dynamically memory allocation.](#part0000_split_131.html__Toc447017103)

[115\. Write a program to print sum of two complex numbers by passing structure to a function.](#part0000_split_132.html__Toc447017104)

[116\. Write a program to see difference between union and structure.](#part0000_split_133.html__Toc447017105)

[117\. Write a program to read or open a file.](#part0000_split_134.html__Toc447017106)

[118\. Write a program to copy files.](#part0000_split_135.html__Toc447017107)

[119\. Write a program to merge two files.](#part0000_split_136.html__Toc447017108)

[120\. Write a program to delete a file.](#part0000_split_137.html__Toc447017109)

[121\. Write a C program to write all the members of an array of structure to a file using fwrite(). Read the array from the file and display on the screen.](#part0000_split_138.html__Toc447017110)

[122\. Write a program to write on data file and read from data file.](#part0000_split_139.html__Toc447017111)

[123\. Write a program to concatenate many files and store them in a file.](#part0000_split_140.html__Toc447017112)

[124\. Write a program to find number of lines in text file.](#part0000_split_141.html__Toc447017113)

[125\. Write a program to replace specified line in a text file.](#part0000_split_142.html__Toc447017114)

[126\. Write a program to delete specific line from a text file.](#part0000_split_143.html__Toc447017115)

[127\. Write a program to implement stooge sort.](#part0000_split_144.html__Toc447017116)

[128\. Write a program to get LCM of two numbers using recursion.](#part0000_split_145.html__Toc447017117)

[129\. Write a program to find GCD of numbers using recursion.](#part0000_split_146.html__Toc447017118)

[130\. Write a program to get power of a number using recursion.](#part0000_split_147.html__Toc447017119)

[131\. Write a program to find factorial of number using recursion.](#part0000_split_148.html__Toc447017120)

[132\. Write a program to print Fibonacci series using recursion.](#part0000_split_149.html__Toc447017121)

[133\. Write a program to convert decimal number to binary number using recursion.](#part0000_split_150.html__Toc447017122)

[134\. Write a program to find the largest number in array using recursion.](#part0000_split_151.html__Toc447017123)

[135\. Write a program to find reverse of number using recursion.](#part0000_split_152.html__Toc447017124)

[136\. Write a program to display ATM transaction.](#part0000_split_153.html__Toc447017125)

[Quick MCQ:](#part0000_split_154.html__Toc447017126)

[Answers-](#part0000_split_155.html__Toc447017127)

[Interview Q & A:](#part0000_split_156.html__Toc447017128)

# 
1\. Write a program to perform addition, subtraction, multiplication and division.

#include<stdio.h>

#include<conio.h>

int main()

{

int first, second, add, subtract, multiply;

float divide;

printf("Enter two integers:\n");

scanf("%d%d", &first, &second);

           add = first + second;

           subtract = first - second;

           multiply = first * second;

           divide = first / (float)second;

printf("Sum = %d\n",add);

printf("Difference = %d\n",subtract);

printf("Multiplication = %d\n",multiply);

printf("Division = %.2f\n",divide);

return 0;

getch();

}

Sample Output:

Enter two integers:

3

5

Sum = 8

Difference = -2

Multiplication = 15

Division = 0.60

# 
2\. How to add two numbers without using the plus operator?

#include<stdio.h>

#include<conio.h>

int main()

{

int a,b;

int sum;

printf("Enter any two integers: ");

scanf("%d%d",&a,&b);

sum = a - ~b -1;

printf("Sum of two integers: %d",sum);

return 0;

getch();

}

Sample output:

Enter any two integers: 5, 10

Sum of two integers: 15

Formula:
In C ~ is 1's complement operator. This is equivalent to:  

~b = -(b + 1)

So, a - ~b -1

= a-[-(b + 1)] -1

= a + b + 1 - 1

= a + b

# 
3\. How to subtract two numbers without using the subtraction operator ?

#include<stdio.h>

#include<conio.h>

int main()

{

int a,b;

int subtract;

printf("Enter any two integers: ");

scanf("%d%d",&a,&b);

subtract = a + ~b + 1;

printf("Difference of two integers: %d",subtract);

return 0;

getch();

}

Sample Output:

Enter any two integers: 5, 4

Difference of two integers: 1

Formula:
In C ~ is 1's complement operator. This is equivalent to:  

~b = -(b + 1)

So, a + ~b +1

= a+[-(b + 1)] +1

= a - b - 1 + 1

= a - b

# 
4\. Write a program for swapping of two numbers.

#include<stdio.h>

#include<conio.h>

int main()

{

int a,b,temp;

printf("Enter any two integers: ");

scanf("%d%d",&a,&b);

printf("Before swapping: a = %d, b=%d",a,b);

           temp = a;

           a = b;

           b = temp;

printf("\nAfter swapping: a = %d, b=%d",a,b);

return 0;

getch();

}

Sample output:

Enter any two integers: 3, 6

Before swapping: a = 3, b=6

After swapping: a = 6, b=6

# 
5\. Write a program to add digits of a number or calculate sum of digits.

#include<stdio.h>

#include<conio.h>

int main()

{

int num,sum=0,r;

printf("Enter a number: ");

scanf("%d",&num);

            while(num)

{

                       r=num%10;

                       num=num/10;

                       sum=sum+r;

}

printf("Sum of digits of number:  %d",sum);

return 0;

getch();

}

Sample output:

Enter a number: 123

Sum of digits of number:  6

# 
6\. Write a program to print complex number.

#include<stdio.h>

#include<conio.h>

int main()

{

int a,b;

printf("Enter the real part of complex number: ");

scanf("%d",&a);

printf("Enter the imaginary part of complex number: ");

scanf("%d",&b);

printf("\nComplex number is: %d%+di",a,b );

return 0;

getch();

}

Sample output:

Enter the real part of complex number: 4

Enter the imaginary part of complex number: 2

Complex number is: 4+2i

Complex numbers definition:

Complex numbers are two dimensional numbers i.e. it consists real part and imaginary part.

Complex numbers are written as a + ib

Where a and b are real numbers and i2 = -1

# 
7\. Write a program to check whether input alphabet is a vowel or not.

#include<stdio.h>

#include<conio.h>

int main()

{

char ch;

printf("Enter a character:\n");

scanf("%c", &ch);

if (ch == 'a' || ch == 'A' || ch == 'e' || ch == 'E' || ch == 'i' || ch == 'I' || ch =='o' || ch=='O' || ch == 'u' || ch == 'U')

           printf("%c is a vowel.\n", ch);

     else

           printf("%c is not a vowel.\n", ch);

return 0;

getch();

}

Sample Output:

Enter a character: i

i is a vowel

# 
8\. Write a program to check if given integer is positive or negative.

#include<stdio.h>

#include<conio.h>

int main()

{

int number;

printf("Enter a number: \n");

scanf("%d", &number);

           if (number >= 0)

printf("%d is a positive number \n", number);

          else

printf("%d is a negative number \n", number);

getch();

}

Sample Output:

Enter a number: -4

-4 is negative number

# 
9\. Write a program to find the area of a trapezium.

#include<stdio.h>

#include<conio.h>

int main()

{

float b1,b2,h;

float area;

printf("Enter the size of two bases and height of the trapezium : ");

scanf("%f%f%f",&b1,&b2,&h);

area = 0.5 * ( b1 + b2 ) * h ;

printf("Area of trapezium is: %.3f",area);

return 0;

getch();

}

Sample output:

Enter the size of two bases and height of the trapezium: 5, 8, 3

Area of trapezium is: 19.500

Formula of area of trapezium:

Area = (1/2) * (a + b) * h

# 
10\. Write a program for swapping of two numbers using function (call by value).

#include<stdio.h>

#include<conio.h>

void swap(int a, int b)

{

int temp;

    temp = a;

    a = b;

    b = temp;

}

int main()

{

int num1 = 10, num2 = 30;

printf("Before swapping:\n num1 = %d\n num2 = %d\n", num1, num2);

swap(num1, num2);

printf("After swapping:\n num1 = %d\n num2 = %d \n", num2, num1);

return 0;

getch();

}

Sample Output:

Before swapping:

num1 = 10

num2 = 30

After swapping:

num1 =30

num2 = 10

# 
11\. Write a program to find greatest number between three numbers.

#include<stdio.h>

#include<conio.h>

int main()

{

int a,b,c;

printf("\nEnter 3 numbers: ");

scanf("%d %d %d",&a,&b,&c);

            if(a-b>0 && a-c>0)

printf("\nGreatest is a :%d",a);

            else

            if(b-c>0)

printf("\nGreatest is b :%d",b);

            else

printf("\nGreatest is c :%d",c);

return 0;

getch();

}

Sample output:

Enter 3 numbers: 2, 6, 4

Greatest is b: 6

# 
12\. Write a program to find greatest number among four numbers by ternary operator.

# include<stdio.h>

# include<conio.h>

main( )

{

int a,b,c,d,big;

printf("Enter value a:");

scanf("%d",&a);

printf("Enter the value of b:");

scanf("%d",&b);

printf("Enter the value of c:");

scanf("%d",&c);

printf("Enter the value of d:");

scanf("%d",&d);

big=(a>b)?(a>c)?(a>d)?a:d:(c>d)?c:d:(b>c)?(b>d)?b:d:(c>d)?c:d;

printf("Biggest of the given 4 numbers is: %d",big);

getch();

}

Sample output:

Enter value a: 8

Enter the value of b: 4

Enter the value of c: 9

Enter the value of d: 6

Biggest of the given 4 numbers is: 9

Ternary Operator:

The ternary operator is an operator that takes three arguments. The first argument is a comparison argument, the second is the result upon a true comparison, and the third is the result upon a false comparison.It is commonly referred to as Conditional Operator.

In computer programming, ?: is a ternary operator that is part of the syntax for a basic conditional expression in several programming languages.

Syntax:  expression 1 ? expression 2 : expression 3

# 
13\. Write a program to find smallest number among four numbers by using ternary operator.

# include <stdio.h>

# include <conio.h>

main( )

{

int a,b,c,d,small;

printf("Enter value a: ");

scanf("%d",&a);

printf("Enter the value of b: ");

scanf("%d",&b);

printf("Enter the value of c: ");

scanf("%d",&c);

printf("Enter the value of d: ");

scanf("%d",&d);

small=(a<b)?(a<c)?(a<d)?a:d:(c<d)?c:d:(b

<c)?(b<d)?b:d:(c<d)?c:d;

printf("Smallest of the given 4 numbers is: %d",small);

getch();

}

Sample output:

Enter value a: 5

Enter the value of b: 7

Enter the value of c: 3

Enter the value of d: 9

Smallest of the given 4 numbers is: 3

# 
14\. Write a program to find largest element using dynamic memory allocation.

#include <stdio.h>

#include <stdlib.h>

#include <conio.h>

int main()

{

int i,n;

float *data;

printf("Enter total number of elements(1 to 100): ");

scanf("%d",&n);

data=(float*)calloc(n,sizeof(float));

             if(data==NULL)

{

printf("Error!!! memory not allocated.");

                  exit(0);

}

printf("\n");

             for(i=0;i<n;++i)

{

printf("Enter Number %d: ",i+1);

scanf("%f",data+i);

}

             for(i=1;i<n;++i)

{

             if(*data<*(data+i))

                   *data=*(data+i);

}

printf("Largest element = %.2f",*data);

return 0;

getch();

}

Sample output:

Enter total number of elements (1 to 100): 10

Enter Number 1: 5

Enter Number 2: 8

Enter Number 3: 6.2

Enter Number 4: 5.4

Enter Number 5: 30

Enter Number 6: -7

Enter Number 7: -56

Enter Number 8: 53

Enter Number 9: 56

Enter Number 10: 34

Largest element = 56.00

Dynamic Memory Allocation:

The exact size of array is unknown untill the compile time,i.e., time when a compier compiles code written in a programming language into a executable form. The size of array you have declared initially can be sometimes insufficient and sometimes more than required. Dynamic memory allocation allows a program to obtain more memory space, while running or to release space when no space is required.

Although, C language inherently does not has any technique to allocated memory dynamically, there are 4 library functions under "stdlib.h" for dynamic memory allocation.

Function                            Use of Function

malloc()              Allocates requested size of bytes and returns a pointer first byte of allocated space.

Syntax:              ptr=(cast-type*)malloc(byte-size)

calloc()              Allocates space for an array elements, initializes to zero and then returns a pointer to memory.

Syntax:              ptr=(cast-type*)calloc(n,element-size);

free()                            dellocate the previously allocated space.

Syntax:                            free(ptr);

realloc()                            Change the size of previously allocated space.

Syntax:                            ptr=realloc(ptr,newsize);

# 
15\. Write a program to print perfect numbers from 1 to 100.

#include<stdio.h>

#include<conio.h>

int main()

{

int n,i,sum;

printf("Perfect numbers are: ");

            for(n=1;n<=100;n++)

{

                   i=1;

                   sum = 0;

             while(i<n)

{

             if(n%i==0)

                   sum=sum+i;

                   i++;

}

             if(sum==n)

printf("%d ",n);

}

return 0;

getch();

}

Sample Output:

Perfect numbers are: 6, 28

Definition of perfect number or What is perfect number ? 

Perfect number is a positive number which sum of all positive divisors excluding that number is equal to that number. For example 6 is perfect number since divisor of 6 are 1, 2 and 3.  Sum of its divisor is

1 + 2+ 3 =6

Note: 6 is the smallest perfect number.

Next perfect number is 28 since 1+ 2 + 4 + 7 + 14 = 28

Some more perfect numbers: 496, 8128

# 
16\. Write a program to reverse a given number.

#include<stdio.h>

#include<conio.h>

int main()

{

int num,r,reverse=0;

printf("Enter any number: ");

scanf("%d",&num);

            while(num)

{

                     r=num%10;

                     reverse=reverse*10+r;

                     num=num/10;

}

printf("Reversed of number: %d",reverse);

return 0;

getch();

}

Sample output:

Enter any number: 12

Reversed of number: 21

# 
17\. Write a program to find generic root of number or sum of digits of a number unit we don't get a single digit.

#include<stdio.h>

#include<conio.h>

int main()

{

long int num,sum,r;

printf("\nEnter any number:-");

scanf("%ld",&num);

            while(num>10)

{

                      sum=0;

    while(num)

{

              r=num%10;

              num=num/10;

              sum+=r;

}

    if(sum>10)

       num=sum;

    else

    break;

}

printf("\nGeneric root of number:%ld",sum);

return 0;

getch();

}

Sample output:

Enter any number: 731

Generic root of number: 2

Generic Root:

Generic root of a number is defined as the sum of digits of a number until we get a single digit.

For example: Generic root of 456: 4 + 5 + 6 = 15 since 15 is two digit numbers so 1 + 5 = 6.

# 
18\. Write a Program to print numbers from 1 to n numbers without using loop.

#include<stdio.h>

#include<conio.h> 

void num(int);

int main()

{

int n;

printf("\nEnter n  number:");

scanf("%d", &n);

num(n);

return 0;

}

void num(int n)

{

static int c = 1;

if (c == n+1)

return;

printf("%d\n", c);

c++;

num(n);

}

Sample output:

Enter n number: 100

1 2 3 4 5 6 7 8 9 10………50……80……100

# 
19\. Write a program to find the sum of first n natural numbers using For loop.

#include<stdio.h>

#include<conio.h>

int main()

{

int  num, n, sum = 0;

printf("Enter the value of n: ");

scanf("%d", &n);

    for (num = 1; num <= 50; num++)

    {

        sum = sum + num;

    }

    printf("Sum = %4d\n", sum);

    getch();

}

Sample Output:

Enter the value of n: 50

Sum = 1275

# 
20\. Write a program to check whether a number is even or odd.

#include<stdio.h>

#include<conio.h>

int main()

{

int n;

printf("Input an integer:\n");

scanf("%d", &n);

n%2 == 0 ? printf("Even\n") : printf("Odd\n");

return 0;

getch();

}

Sample output:

Input an integer: 2

Even

Input an integer: 3

Odd

# 
21\. Write a program to calculate the sum of odd & even numbers upto n numbers.

#include<stdio.h>

#include<conio.h>

int main()

{

int i, n, odd_sum = 0, even_sum = 0;

printf("Enter the value of n:\n");

scanf("%d", &n);

           for (i = 1; i <= n; i++)

{

           if (i % 2 == 0)

               even_sum = even_sum + i;

           else

               odd_sum = odd_sum + i;

}

printf("Sum of all odd numbers  = %d\n", odd_sum);

printf("Sum of all even numbers = %d\n", even_sum);

getch();

}

Sample Output:

Enter the value of n: 10

Sum of all odd numbers  = 25

Sum of all even numbers = 30

# 
22\. Write a program to check whether a number is strong or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int num,i,f,r,sum,temp;

int min,max;

printf("Enter minimum range: ");

scanf("%d",&min);

printf("Enter maximum range: ");

scanf("%d",&max);

printf("Strong numbers in given range are: ");

            for(num=min; num <= max; num++)

{

                 temp = num;

                 sum=0;

            while(temp)

{

                     i=1;

                     f=1;

                    r=temp%10;

             while(i<=r)

{

                      f=f*i;

                      i++;

}

                      sum=sum+f;

                      temp=temp/10;

}

                if(sum==num)

printf("%d ",num);

}

return 0;

getch();

}

Sample output:

Enter minimum range: 100

Enter maximum range: 100000

Strong numbers in given range are: 145, 40585

Definition of strong number:

A number is called strong number if sum of the factorial of its digit is equal to number itself. For example: 145 since

1! + 4! + 5! = 1 + 24 + 120 = 145

# 
23\. Write a program of simple bubble sort implementation using array ascending order.

#include<stdio.h>

#include<conio.h>

int main()

{

int s,temp,i,j,a[20];

printf("Enter total numbers of elements: ");

scanf("%d",&s);

printf("Enter %d elements: ",s);

            for(i=0;i<s;i++)

scanf("%d",&a[i]);

            for(i=s-2;i>=0;i--)

{

            for(j=0;j<=i;j++)

{

            if(a[j]>a[j+1])

{

                   temp=a[j];

                   a[j]=a[j+1];

                   a[j+1]=temp;

}

}

}

printf("After sorting: ");

             for(i=0;i<s;i++)

printf(" %d",a[i]);

return 0;

getch();

}

Sample output:

Enter total numbers of elements: 5

Enter 5 elements: 6 2 0 11 9

After sorting:  0 2 6 9 11

# 
24\. How to calculate power of a number in C.

#include<stdio.h>

#include<conio.h>

int main()

{

int pow,num,i=1;

long int sum=1;

printf("\nEnter a number: ");

scanf("%d",&num);

printf("\nEnter power: ");

scanf("%d",&pow);

  while(i<=pow)

{

     sum=sum*num;

     i++;

}

printf("\n%d to the power %d is: %ld",num,pow,sum);

return 0;

getch();

}

Sample output:

Enter a number: 4

Enter power: 2

4 to the power 2 is: 16

# 
25\. Write a program to check whether a year is leap year or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int year;

printf("Enter any year: ");

scanf("%d",&year);

    if(((year%4==0)&&(year%100!=0))||(year%400==0))

printf("%d is a leap year",year);

    else

printf("%d is not a leap year",year);

return 0;

getch();

}

Sample output:

Enter any year: 2010

2010 is not a leap year

# 
26\. Write a program to find HCF and LCM of numbers.

#include<stdio.h>

#include<conio.h> 

int main()

{

int a, b, x, y, t, hcf, lcm;

printf("Enter two integers:\n");

scanf("%d%d", &x, &y);

a = x;

b = y;

 while (b != 0)

{

    t = b;

    b = a % b;

    a = t;

}

hcf = a;

lcm = (x*y)/hcf;

printf("Highest common factor of %d and %d = %d\n", x, y, hcf);

printf("Least common multiple of %d and %d = %d\n", x, y, lcm);

return 0;

getch();

}

Sample output:

Enter two integers: 9, 24

Highest common factor of 9 and 24 = 3

Least common multiple of 9 and 24 = 72

# 
27\. Write a program to print multiplication table.

#include<stdio.h>

#include<conio.h>

int main()

{

int r,i,j,k;

printf("Enter the number range: ");

scanf("%d",&r);

  for(i=1;i<=r;i++)

{

  for(j=1;j<=10;j++)

printf("%d*%d=%d ",i,j,i*j);

printf("\n");

}

return 0;

getch();

}

Sample Output:

Enter the number range: 5

1*1=1 1*2=2 1*3=3 1*4=4 1*5=5 1*6=6 1*7=7 1*8=8 1*9=9 1*10=10

2*1=2 2*2=4 2*3=6 2*4=8 2*5=10 2*6=12 2*7=14 2*8=16 2*9=18 2*10=20

3*1=3 3*2=6 3*3=9 3*4=12 3*5=15 3*6=18 3*7=21 3*8=24 3*9=27 3*10=30

4*1=4 4*2=8 4*3=12 4*4=16 4*5=20 4*6=24 4*7=28 4*8=32 4*9=36 4*10=40

5*1=5 5*2=10 5*3=15 5*4=20 5*5=25 5*6=30 5*7=35 5*8=40 5*9=45 5*10=50

# 
28\. Write a program to print prime numbers between 1-200 using break and continue.

#include<conio.h>

#include<math.h>

#include<stdio.h>

int main()

{

int i, j;

i = 2;

          while ( i < 300 )

{

                    j = 2;

          while ( j < sqrt(i) )

{

          if ( i % j == 0 )

          break;

          else

{

                    ++j;

          continue;

}

}

          if ( j > sqrt(i) )

printf("%d\t", i);

                    ++i;

}

return 0;

getch();

}

Sample output:

Note: 2 is only even prime number.

2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293.

Prime Numbers:

A natural number greater than one has not any other divisors except 1 and itself. In other word we can say which has only two divisors 1 and number itself.

For example: 5

Their divisors are 1 and 5.

# 
29\. Write a program to check whether a number is prime number or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int n, i, flag=0;

printf("Enter a positive integer: ");

scanf("%d",&n);

             for(i=2;i<=n/2;++i)

{

             if(n%i==0)

{

                      flag=1;

             break;

}

}

              if (flag==0)

printf("%d is a prime number.",n);

              else

printf("%d is not a prime number.",n);

return 0;

getch();

}

Sample output:

Enter a positive integer: 29

29 is a prime number.

# 
30\. Write a program to find prime factor of number.

#include<stdio.h>

#include<conio.h>

int main()

{

int num,i=1,j,k;

printf("\nEnter a number:");

scanf("%d",&num);

  while(i<=num)

{

      k=0;

      if(num%i==0)

{

      j=1;

   while(j<=i)

{

   if(i%j==0)

      k++;

      j++;

}

   if(k==2)

printf("\n%d is a prime factor",i);

}

      i++;

}

return 0;

getch();

}

Sample output:

Enter a number: 27

3 is a prime factor

Prime Factor:

The prime factors of a positive integer are the prime numbers that divide that integer exactly.

Example: The prime factors of 15 are 3 and 5 (3×5=15, and 3 and 5 are prime numbers).

# 
31. Write a program to find factorial of a number.

#include<stdio.h>

#include<conio.h>

int findFactorial(int);

int main()

{

int i,factorial,num;

printf("Enter a number: ");

scanf("%d",&num);

factorial = findFactorial(num);

printf("Factorial of %d is: %d",num,factorial);

return 0;

getch();

}

int findFactorial(int num)

{

int i,f=1;

       for(i=1;i<=num;i++)

      f=f*i;

return f;

}

Sample output:

Enter a number: 8

Factorial of 8 is: 40320

Factorial (n!):             

The factorial of n is denoted by n! and calculated by the product of integer numbers from 1 to n.

For n>0,

n! = 1×2×3×4×...×n

# 
32\. Write a program to print Fibonacci series.

#include<stdio.h>

#include<conio.h>

int main()

{

int k,r;

long int i=0l,j=1,f;

printf("Enter the number range:");

scanf("%d",&r);

printf("FIBONACCI SERIES: ");

printf("%ld %ld",i,j);

    for(k=2;k<r;k++)

{

         f=i+j;

         i=j;

         j=f;

printf(" %ld",j);

}

return 0;

getch();

}

Sample output:

Enter the number range: 15

FIBONACCI SERIES: 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

# 
33\. Write a program to print Armstrong numbers from 1 to 500.

#include<stdio.h>

#include<conio.h>

int main()

{

int num,r,sum,temp;

   for(num=1;num<=500;num++)

{

         temp=num;

         sum = 0;

   while(temp!=0)

{

         r=temp%10;

         temp=temp/10;

         sum=sum+(r*r*r);

}

   if(sum==num)

printf("%d ",num);

}

return 0;

getch();

}

Sample output:

1 153 370 371 407

What is an Armstrong number ?

Those numbers which sum of its digits to power of number of its digits is equal to that number are known as Armstrong numbers.

Example: 153

Total digits in 153 is 3

AND 1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153

# 
34\. Write a program to check whether a number is Armstrong number or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int n, n1, rem, num=0;

printf("Enter a positive  integer: ");

scanf("%d", &n);

n1=n;

           while(n1!=0)

{

                      rem=n1%10;

                      num+=rem*rem*rem;

                      n1/=10;

}

            if(num==n)

printf("%d is an Armstrong number.",n);

            else

printf("%d is not an Armstrong number.",n);

return 0;

getch();

}

Sample output:

Enter a positive integer: 143

143 is not an Armstrong number.

# 
35\. Write a program to check whether a number is Prime or Armstrong number using user-defined function.

#include<stdio.h>

#include<conio.h>

int prime(int n);

int armstrong(int n);

int main()

{

char c;

int n,temp=0;

printf("Eneter a positive integer: ");

scanf("%d",&n);

printf("Enter P to check prime and  A to check Armstrong number: ");

                     c=getche();

               if (c=='p' || c=='P')

{

                      temp=prime(n);

               if(temp==1)

printf("\n%d is a prime number.", n);

               else

printf("\n%d is not a prime number.", n);

}

                if (c=='a' || c=='A')

{

                       temp=armstrong(n);

                if(temp==1)

printf("\n%d is an Armstrong number.", n);

                else

printf("\n%d is not an Armstrong number.",n);

}

return 0;

getch();

}

int prime(int n)

{

int i, flag=1;

                for(i=2; i<=n/2; ++i)

{

                if(n%i==0)

{

                flag=0;

                break;

}

}

                 return flag;

}

int armstrong(int n)

{

int num=0, temp, flag=0;

                           temp=n;

                while(n!=0)

{

                           num+=(n%10)*(n%10)*(n%10);

                           n/=10;

}

                 if (num==temp)

                            flag=1;

                 return flag;

}

Sample output:

Enter a positive integer: 76

Enter P to check prime and A to check Armstrong number: p

76 is not a prime number.

Enter a positive integer: 143

Enter P to check prime and A to check Armstrong number: a

143 is not an Armstrong number.

# 
36\. Write a program to check whether a number can be express as sum of two prime numbers.

#include<stdio.h>

#include<conio.h>

int prime(int n);

int main()

{

int n, i, flag=0;

printf("Enter a positive integer: ");

scanf("%d",&n);

               for(i=2; i<=n/2; ++i)

{

               if (prime(i)!=0)

{

               if ( prime(n-i)!=0)

{

printf("%d = %d + %d\n", n, i, n-i);

                       flag=1;

}

}

}

               if (flag==0)

printf("%d can't be expressed as sum of two prime numbers.",n);

return 0;

getch();

}

int prime(int n)

{

int i, flag=1;

               for(i=2; i<=n/2; ++i)

               if(n%i==0)

               flag=0;

return flag;

}

Sample output:

Enter a positive integer: 34

34 = 3 + 31

34 = 5 + 29

34 = 11 + 23

34 = 17 + 17

# 
37\. Write a program to check whether a number is palindrome or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int n, reverse = 0, temp;

printf("Enter a number:\n");

scanf("%d",&n);

temp = n; 

   while( temp != 0 )

{

      reverse = reverse * 10;

      reverse = reverse + temp%10;

      temp = temp/10;

}

   if ( n == reverse )

printf("%d is a palindrome number.\n", n);

   else

printf("%d is not a palindrome number.\n", n);

return 0;

getch();

}

Sample output:

Enter a number: 123321

123321 is a palindrome number.

Enter a number: 123456

123456 is not a palindrome number.

Palindrome Number:

A palindromic number or numeral palindrome is a number that remains the same when its digits are reversed. Like 16461, for example, it is "symmetrical".

# 
38\. Write a program to reverse a number and check if it is a palindrome.

#include<stdio.h>

#include<conio.h>

int main()

{

int num, temp, remainder, reverse = 0;

printf("Enter an integer: ");

scanf("%d", &num);

temp = num;

           while (num > 0)

{

           remainder = num % 10;

           reverse = reverse * 10 + remainder;

           num /= 10;

}

printf("Given number is = %d\n", temp);

printf("Its reverse is  = %d\n", reverse);

           if (temp == reverse)

printf("Number is a palindrome \n");

           else

printf("Number is not a palindrome \n");

getch();

}

Sample Output:

Enter an integer: 2476

Given number is = 2476

Its reverse is  = 6742

Number is not a palindrome

# 
39\. Write a program to find out the sum of in A.P. series.

#include<stdio.h>

#include<conio.h>

int main()

{

int a,d,n,i,tn;

int sum=0;

printf("Enter the first number of the A.P. series: ");

scanf("%d",&a);

printf("Enter the total numbers in the A.P. series: ");

scanf("%d",&n);

printf("Enter the common difference of A.P. series: ");

scanf("%d",&d);

sum = ( n * ( 2 * a + ( n -1 ) * d ) )/ 2;

tn = a + (n-1) * d;

printf("Sum of the series A.P.: ");

            for(i=a;i<=tn; i= i + d )

{

            if (i != tn)

printf("%d + ",i);

            else

printf("%d = %d ",i,sum);

}

return 0;

getch();

}

Sample output:

Enter the first number of the A.P. series: 1

Enter the total numbers in the A.P. series: 5

Enter the common difference of A.P. series: 3

Sum of the series: 1 + 4 + 7 + 10 + 13 = 35

Definition of arithmetic progression (A.P.):

A series of numbers in which difference of any two consecutive numbers is always a same number that is constant. This constant is called as common difference.

Example of A.P. series:

5 10 15 20 25 …

Here common difference is 5 since difference of any two consecutive numbers for example 20 – 15 or 25 -20 is 5.

Sum of A.P. series:

Sn = n/2(2a + (n-1) d)

Tn term of A.P. series:

Tn = a + (n-1) d 

# 
40\. Write a program to find out the sum of G.P series.

#include<stdio.h>

#include<math.h>

#include<conio.h>

int main()

{

float a,r,i,tn;

int n;

float sum=0;

printf("Enter the first number of the G.P. series: ");

scanf("%f",&a);

printf("Enter the total numbers in the G.P. series: ");

scanf("%d",&n);

printf("Enter the common ratio of G.P. series: ");

scanf("%f",&r);

           sum = (a*(1 - pow(r,n+1)))/(1-r);

           tn = a * (1 -pow(r,n-1));

printf("tn term of G.P.: %f",tn);

printf("\nSum of the G.P.: %f",sum);

return 0;

getch();

}

Sample output:

Enter the first number of the G.P. series: 1

Enter the total numbers in the G.P. series: 5

Enter the common ratio of G.P. series: 2

tn term of G.P. : -15.000000

Sum of the G.P. : 63.000000

Definition of geometric progression (G.P.):

A series of numbers in which ratio of any two consecutive numbers is always a same number that is constant. This constant is called as common ratio.

Example of G.P. series:

2 4 8 16 32 64

Here common difference is 2 since ratio any two consecutive numbers for example 32 / 16 or 64/32 is 2.

Sum of G.P. series:

Sn =a(1–rn+1)/(1-r)

Tn term of G.P. series:

Tn = arn-1          

Sum of infinite G.P. series:

Sn = a/(1-r)  if 1 > r

   = a/(r-1)  if r > 1

# 
41\. Write a program to find out the sum of infinite G.P. series.

#include<stdio.h>

#include<conio.h>

int main()

{

float a,r;

float sum=0;

printf("Enter the first number of the G.P. series: ");

scanf("%f",&a);

printf("Enter the common ratio of G.P. series: ");

scanf("%f",&r);

           if(1 > r)

               sum = a/(1-r);

           else

               sum = a/(r-1);

printf("\nSum of the infinite G.P. series: %f",sum);

return 0;

getch();

}

Sample output:

Enter the first number of the G.P. series: 1

Enter the common ratio of G.P. series: .5

Sum of the infinite G.P. series: 0.250000

Enter the first number of the G.P. series: 5

Enter the common ratio of G.P. series: 2

Sum of the infinite G.P. series: 5.000000

# 
42\. Write a program to find out the sum of series 1 + 2 + …. + n.

#include<stdio.h>

#include<conio.h>

int main()

{

int n,i;

int sum=0;

printf("Enter the n i.e. max values of series: ");

scanf("%d",&n);

            sum = (n * (n + 1)) / 2;

printf("Sum of the series: ");

            for(i =1;i <= n;i++)

{

            if (i!=n)

printf("%d + ",i);

            else

printf("%d = %d ",i,sum);

}

return 0;

getch();

}

Sample output:

Enter the n i.e. max values of series: 5

Sum of the series: 1 + 2 + 3 + 4 + 5 = 15

# 
43\. Write a program to find out the sum of series 1^3 + 2^3 + …. + n^3.

#include<stdio.h>

#include<math.h>

#include<conio.h>

int main()

{

int n,i;

int sum=0;

printf("Enter the n i.e. max values of series: ");

scanf("%d",&n);

    sum = pow(((n * (n + 1) ) / 2),2);

printf("Sum of the series : ");

    for(i =1;i<=n;i++)

{

    if (i != n)

printf("%d^3 + ",i);

    else

printf("%d^3 = %d ",i,sum);

}

return 0;

getch();

}

Sample output:

Enter the n i.e. max values of series: 3

Sum of the series: 1^3 + 2^3 + 3^3 = 36

Mathematical Formula:

Sum of the series 1 + 2 + 3 + … + n = n (n+1)/2

Mathematical Formula:

Sum of the series 13 + 23 + 33 + … + n3 = (n (n+1)/2)2

# 
44\. Write a program to find roots of a quadratic equation.

#include<stdio.h>

#include<math.h>

#include<conio.h>

int main()

{

float a, b, c, determinant, r1,r2, real, imag;

printf("Enter coefficients a, b and c: ");

scanf("%f%f%f",&a,&b,&c);

                       determinant=b*b-4*a*c;

              if (determinant>0)

{

                       r1= (-b+sqrt(determinant))/(2*a);

                       r2= (-b-sqrt(determinant))/(2*a);

printf("Roots are: %.2f and %.2f",r1 , r2);

}

               else if (determinant==0)

{

                        r1 = r2 = -b/(2*a);

printf("Roots are: %.2f and %.2f", r1, r2);

}

               else

{

                        real= -b/(2*a);

                        imag = sqrt(-determinant)/(2*a);

printf("Roots are: %.2f+%.2fi and %.2f-%.2fi", real, imag, real, imag);

}

return 0;

getch();

}

Sample output:

Enter coefficients a, b and c: 2

4

6

Roots are: -1.00+1.41i and -1.00-1.41i

# 
45\. Write a program to print rectangle pyramid of numbers.

#include<stdio.h>

#include<conio.h>

int main()

{

int number, row, col;

printf("\nEnter Number of Rows to be display : ");

scanf("%d", &number);

             for (row = 1; number >= row; row++)

{

             for (col = 1; col <= number; col++)

printf("%d\t", row);

printf("\n");

}

return 0;

getch();

}

Sample output:

Enter Number of Rows to be display: 5

1       1       1       1       1

2       2       2       2       2

3       3       3       3       3

4       4       4       4       4

5       5       5       5       5

# 
46\. Write a program to print numerical as Pascal’s triangle pattern.

#include<stdio.h>

#include<conio.h>

long fact(int);             

int main()

{

int line,i,j;

printf("Enter the no. of lines: ");

scanf("%d",&line);

           for(i=0;i<line;i++)

{

           for(j=0;j<line-i-1;j++)

printf(" ");

           for(j=0;j<=i;j++)

printf("%ld ",fact(i)/(fact(j)*fact(i-j)));

printf("\n");

}

return 0;

getch();

}

long fact(int num)

{

long f=1;

int i=1;

           while(i<=num)

{

                f=f*i;

                i++;

}

return f;

}

Sample output:

Enter the no. of lines: 8

1

1 1

1 2 1

1 3 3 1

1 4 6 4 1

1 5 10 10 5 1

1 6 15 20 15 6 1

1 7 21 35 35 21 7 1

# 
47\. Write a program to print “*” as inverted Pascal’s triangle pattern.

#include<stdio.h>

#include<conio.h>

int main()

{

int rows,i,j,space;

printf("Enter number of rows: ");

scanf("%d",&rows);

           for(i=rows;i>=1;--i)

{

           for(space=0;space<rows-i;++space)

printf("  ");

           for(j=i;j<=2*i-1;++j)

printf("* ");

           for(j=0;j<i-1;++j)

printf("* ");

printf("\n");

}

return 0;

getch();

}

Sample output:

Enter number of rows: 8

***************

*************

***********

*********

*******

*****

***

*

# 
48\. Write a program to print numerical as Floyd’s triangle pattern.

#include<stdio.h>

#include<conio.h>

int main()

{

int i,j,r,k=1;

printf("Enter the range: ");

scanf("%d",&r);

printf("FLOYD'S TRIANGLE\n\n");

   for(i=1;i<=r;i++)

{

   for(j=1;j<=i;j++,k++)

printf(" %d",k);

printf("\n");

}

return 0;

getch();

}

Sample output:

Enter the range: 8

FLOYD'S TRIANGLE

  1

 2 3

 4 5 6

 7 8 9 10

 11 12 13 14 15

 16 17 18 19 20 21

 22 23 24 25 26 27 28

 29 30 31 32 33 34 35 36

# 
49\. Write a program to print character as Floyd’s triangle pattern.

# include <stdio.h>

# include <conio.h>

main( )

{

char i,j;

for(i=65;i<=70;i++)

{

for(j=65;j<=i;j++)

printf("%c",j);

printf("\n");

}

getch( );

}

Sample output:

A

AB

ABC

ABCD

ABCDE

ABCDEF

# 
50\. Write a program to print “*” as inverted Floyd’s triangle pattern.

#include<stdio.h>

#include<conio.h>

int main()

{

int i,j,rows;

printf("Enter the number of rows: ");

scanf("%d",&rows);

            for(i=rows;i>=1;--i)

{

            for(j=1;j<=i;++j)

{

printf("* ");

}

printf("\n");

}

return 0;

getch();

}

Sample Output:

Enter the number of rows: 10

**********

*********

********

*******

******

*****

****

***

**

*

# 
51\. Write a program to print diamond pattern.

#include<stdio.h>

#include<conio.h> 

int main()

{

int n, c, k, space = 1;

printf("Enter number of rows\n");

scanf("%d", &n);

space = n - 1;

    for (k = 1; k <= n; k++)

{

    for (c = 1; c <= space; c++)

printf(" ");

space--;

    for (c = 1; c <= 2*k-1; c++)

printf("*");

printf("\n");

}

space = 1;

    for (k = 1; k <= n - 1; k++)

{

    for (c = 1; c <= space; c++)

printf(" ");

space++;

    for (c = 1 ; c <= 2*(n-k)-1; c++)

printf("*");

printf("\n");

}

return 0;

getch();

}

Sample output:

Enter number of rows

10

         *

        ***

       *****

      *******

     *********

    ***********

   *************

  ***************

*****************

*******************

*****************

  ***************

   *************

    ***********

     *********

      *******

       *****

        ***

         *

# 
52\. Write a program to search an element in an array using binary search.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[10],i,n,m,c=0,l,u,mid;

printf("Enter the size of an array: ");

scanf("%d",&n);

printf("Enter the elements in ascending order: ");

    for(i=0;i<n;i++)

{

scanf("%d",&a[i]);

}

printf("Enter the number to be search: ");

scanf("%d",&m);

          l=0,u=n-1;

    while(l<=u)

{

         mid=(l+u)/2;

         if(m==a[mid])

{

         c=1;

     break;

}

     else if(m<a[mid])

{

             u=mid-1;

}

     else

             l=mid+1;

}

     if(c==0)

printf("The number is not found.");

     else

printf("The number is found.");

return 0;

getch();

}

Sample output:

Enter the size of an array: 5

Enter the elements in ascending order: 4 7 8 11 21

Enter the number to be search: 11

The number is found.

# 
53\. Write a program for binary to decimal conversion.

#include<stdio.h>

#include<conio.h>

int main()

{

long int binaryNumber,decimalNumber=0,j=1,remainder;

printf("Enter any number any binary number: ");

scanf("%ld",&binaryNumber);

     while(binaryNumber!=0)

{

           remainder=binaryNumber%10;

           decimalNumber=decimalNumber+remainder*j;

           j=j*2;

           binaryNumber=binaryNumber/10;

}

printf("Equivalent decimal value: %ld",decimalNumber);

return 0;

getch();

}

Sample output:

Enter any number any binary number: 1101

Equivalent decimal value: 13

Formula:

Binary number system: 

It is base 2 number system which uses the digits from 0 and 1.

Decimal number system:

It is base 10 number system which uses the digits from 0 to 9.

Convert from binary to decimal Formula:

For this we multiply each digit separately from right side by 1, 2, 4, 8, 16 … respectively then add them.

Binary number to decimal conversion with example

For example we want to convert binary number 101111 to decimal:

Step1:  1 * 1 = 1

Step2:  1 * 2 = 2

Step3:  1 * 4 = 4

Step4:  1 * 8 = 8

Step5:  0 * 16 = 0

Step6:  1 * 32 = 32

Its decimal value: 1 + 2 + 4+ 8+ 0+ 32 = 47

That is (101111)2 = (47)10

# 
54\. Write a program for decimal to octal converter.

#include<stdio.h>

#include<conio.h>

int main()

{

long int decimalNumber,remainder,quotient;

int octalNumber[100],i=1,j;

printf("Enter any decimal number: ");

scanf("%ld",&decimalNumber);

quotient = decimalNumber;

        while(quotient!=0)

{

                  octalNumber[i++]= quotient % 8;

                   quotient = quotient / 8;

}

printf("Equivalent octal value of decimal number %d: ",decimalNumber);

          for(j = i -1 ;j> 0;j--)

printf("%d",octalNumber[j]);

return 0;

getch();

}

Sample output:

Enter any decimal number: 50

Equivalent octal value of decimal number 50: 62

Algoritham:

Octal number system: 

It is base 8 number system which uses the digits from 0 to 7.

Decimal number system:

It is base 10 number system which uses the digits from 0 to 9

Decimal to octal conversion method:

Step 1: Divide the original decimal number by 8

Step 2: Divide the quotient by 8

Step3: Repeat the step 2 until we get quotient equal to zero.

Result octal number would be remainders of each step in the reverse order.

Decimal to octal conversion with example:

For example we want to convert decimal number 525 in the octal.

Step 1:  525 / 8  Remainder : 5 , Quotient : 65

Step 2:   65 / 8  Remainder : 1 , Quotient : 8

Step 3:    8 / 8  Remainder : 0 , Quotient : 1

Step 4:    1 / 8  Remainder : 1 , Quotient : 0

So equivalent octal number is: 1015

That is (525)10 = (1015)8

# 
55\. How to convert large binary number to hexadecimal.

#include<stdio.h>

#include<conio.h>

#define MAX 1000

int main()

{

char binaryNumber[MAX],hexaDecimal[MAX];

int temp;

long int i=0,j=0;

printf("Enter any number any binary number: ");

scanf("%s",binaryNumber);

         while(binaryNumber[i])

{

                  binaryNumber[i] = binaryNumber[i] -48;

                  ++i;

}

                   --i;

          while(i-2>=0)

{

                    temp =  binaryNumber[i-3] *8 +binaryNumber[i-2] *4 +  binaryNumber[i-1] *2 + binaryNumber[i] ;

           if(temp > 9)

                     hexaDecimal[j++] = temp + 55;

           else

                     hexaDecimal[j++] = temp + 48;

                     i=i-4;

}

            if(i ==1)

                         hexaDecimal[j] = binaryNumber[i-1] *2 + binaryNumber[i] + 48 ;

             else if(i==0)

                          hexaDecimal[j] =  binaryNumber[i] + 48 ;

              else

                          --j;

printf("Equivalent hexadecimal value: ");

              while(j>=0)

{

printf("%c",hexaDecimal[j--]);

}

return 0;

getch();

}

Sample output:

Enter any number any binary number: 1010011011100011110

001001111011110001000100011101110111011110

Equivalent hexadecimal value: 14DC789EF111DDDE

Formula:

Binary to hexadecimal conversion method:

Step1: Arrange the binary number in the group 4 from right side.

Step 2:  Replace the each group with following values:

| Binary  number | Hexadecimal  values |
| 0000 | 0 |
| 0001 | 1 |
| 0010 | 2 |
| 0011 | 3 |
| 0100 | 4 |
| 0101 | 5 |
| 0110 | 6 |
| 0111 | 7 |
| 1000 | 8 |
| 1001 | 9 |
| 1010 | A |
| 1011 | B |
| 1100 | C |
| 1101 | D |
| 1110 | E |
| 1111 | F |

Binary to hexadecimal conversion examples:

For example we want to convert binary number 11011010101001101 to hexadecimal.

Step 1: 0001 1011 0101 0100 1101

Step 2:  1     B    5    4   D

So (1011010101001101)2 = (1B54D)16

# 
56\. Write a program for hexadecimal to binary conversion.

#include<stdio.h>

#include<conio.h>

#define MAX 1000

int main()

{

char binaryNumber[MAX],hexaDecimal[MAX];

long int i=0;

printf("Enter any hexadecimal number: ");

scanf("%s",hexaDecimal);

printf("\nEquivalent binary value: ");

       while(hexaDecimal[i])

{

       switch(hexaDecimal[i])

{

             case '0': printf("0000"); break;

             case '1': printf("0001"); break;

             case '2': printf("0010"); break;

             case '3': printf("0011"); break;

             case '4': printf("0100"); break;

             case '5': printf("0101"); break;

             case '6': printf("0110"); break;

             case '7': printf("0111"); break;

             case '8': printf("1000"); break;

             case '9': printf("1001"); break;

             case 'A': printf("1010"); break;

             case 'B': printf("1011"); break;

             case 'C': printf("1100"); break;

             case 'D': printf("1101"); break;

             case 'E': printf("1110"); break;

             case 'F': printf("1111"); break;

             case 'a': printf("1010"); break;

             case 'b': printf("1011"); break;

             case 'c': printf("1100"); break;

             case 'd': printf("1101"); break;

             case 'e': printf("1110"); break;

             case 'f': printf("1111"); break;

             default:  printf("\nInvalid hexadecimal digit %c ",hexaDecimal[i]); 

return 0;

}

              i++;

}

return 0;

getch();

}

Sample output:

Enter any hexadecimal number: 2AD5

Equivalent binary value: 0010101011010101

Formula: (use above chart)

Hexadecimal to binary conversion method:

To convert or change the hexadecimal number to binary number replace the each octal digits by a binary number using hexadecimal to binary chart.

Hexadecimal to binary conversion examples:

For example we want to convert or change hexadecimal number 65B2 to binary. For this we will replace each hexadecimal digit to binary values using the above table:

Hexadecimal number: 6    5    B    2

Binary values:     0110 0101 1011 0010

So (65B2)16 = (0110010110110010)2

# 
57\. Write a program to convert octal number to decimal number.

#include<stdio.h>

#include<math.h>

#include<conio.h>

int main()

{

long int octal,decimal =0;

int i=0;

printf("Enter any octal number: ");

scanf("%ld",&octal);

      while(octal!=0)

{

        decimal = decimal + (octal % 10) * pow(8,i++);

        octal = octal/10;

}

printf("Equivalent decimal value: %ld",decimal);

return 0;

getch();

}

Sample output:

Enter any octal number: 346

Equivalent decimal value: 230

Formula:

Octal to decimal conversion method:

To convert an octal number to decimal number multiply each digits separately of octal number from right side by  8^0,8^1,8^2,8^3 … respectively and then find out the sum of them.

Octal to decimal conversion examples:

For example we want to convert octal number 3401 to decimal number.

Step 1: 1 * 8 ^0 = 1*1 =1

Step 2: 0 * 8 ^1 = 0*8 =0

Step 3: 4 * 8 ^2 = 4*64 =256

Step 4: 3 * 8 ^3 = 3*512 =1536

Sum= 1 + 0 + 256 + 1536 = 1793

So, (3401)8 = (1793)10

# 
58\. Write a program to covert each digits of a number in English word.

#include<stdio.h>

#include<conio.h>

int main()

{

int number,i=0,j,digit;

char * word[1000];

printf("Enter any integer: ");

scanf("%d",&number);

      while(number)

{

            digit = number %10;

            number = number /10;

      switch(digit)

{

             case 0: word[i++] = "zero"; break;

             case 1: word[i++] = "one"; break;

             case 2: word[i++] = "two"; break;

             case 3: word[i++] = "three"; break;

             case 4: word[i++] = "four"; break;

             case 5: word[i++] = "five"; break;

             case 6: word[i++] = "six"; break;

             case 7: word[i++] = "seven"; break;

             case 8: word[i++] = "eight"; break;

             case 9: word[i++] = "nine"; break;

}

}

       for(j=i-1;j>=0;j--)

{

printf("%s ",word[j]);

}

return 0;

getch();

}

Sample output:

Enter any integer: 23451208

two three four five one two zero eight

# 
59\. Write a program for multiplication of two binary numbers.

#include<stdio.h>

#include<conio.h>

int binaryAddition(int,int);

int main()

{

long int binary1,binary2,multiply=0;

int digit,factor=1;

printf("Enter any first binary number: ");

scanf("%ld",&binary1);

printf("Enter any second binary number: ");

scanf("%ld",&binary2);

       while(binary2!=0)

{

               digit =  binary2 %10;

       if(digit ==1)

{

               binary1=binary1*factor;

               multiply=binaryAddition(binary1,multiply);

}

        else

               binary1=binary1*factor;

               binary2 = binary2/10;

               factor = 10;

}

printf("Product of two binary numbers: %ld",multiply);

return 0;

getch();

}

int binaryAddition(int binary1,int binary2)

{

int i=0,remainder = 0,sum[20];

int binarySum=0;

      while(binary1!=0||binary2!=0)

{

               sum[i++]=(binary1 %10 + binary2 %10 + remainder )% 2;

               remainder=(binary1 %10 + binary2 %10 + remainder ) / 2;

               binary1 = binary1/10;

               binary2 = binary2/10;

 }

       if(remainder!=0)

                sum[i++] = remainder;

                 --i;

       while(i>=0)

                binarySum = binarySum*10 + sum[i--];

return binarySum;

}

Sample output:

Enter any first binary number: 1101

Enter any second binary number: 11

Product of two binary numbers: 100111

# 
60\. Write a program which prints initial of any name.

#include<stdio.h>

#include<conio.h>

int main()

{

char str[20];

int i=0;

printf("Enter a string: ");

gets(str);

printf("%c",*str);

         while(str[i]!='\0')

{

         if(str[i]==' ')

{

              i++;

printf("%c",*(str+i));

}

               i++;

}

return 0;

getch();

}

Sample output:

Enter a string: Rohit Kumar Gupta

RKG

# 
61\. Write a program for addition of matrices.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[3][3],b[3][3],c[3][3],i,j;

printf("Enter the First matrix:");

        for(i=0;i<3;i++)

        for(j=0;j<3;j++)

scanf("%d",&a[i][j]);

printf("\nEnter the Second matrix:");

        for(i=0;i<3;i++)

        for(j=0;j<3;j++)

scanf("%d",&b[i][j]);

printf("\nThe First matrix is:\n");

        for(i=0;i<3;i++)

{

printf("\n");

        for(j=0;j<3;j++)

printf("%d\t",a[i][j]);

}

printf("\nThe Second matrix is:\n");

        for(i=0;i<3;i++)

{

printf("\n");

        for(j=0;j<3;j++)

printf("%d\t",b[i][j]);

}

        for(i=0;i<3;i++)

        for(j=0;j<3;j++)

           c[i][j]=a[i][j]+b[i][j];

printf("\nThe Addition of two matrix is:\n");

        for(i=0;i<3;i++)

{

printf("\n");

        for(j=0;j<3;j++)

printf("%d\t",c[i][j]);

}

return 0;

getch();

}

Sample output:

Enter the First matrix: 2 4 6 8 0 1 3 5 7

Enter the Second matrix: 1 2 3 4 5 6 7 8 9

The First matrix is:

2       4       6

8       0       1

3       5       7

The Second matrix is:

1       2       3

4       5       6

7       8       9

The Addition of two matrices is:

3       6       9

12      5       7

10      13      16

# 
62\. Write a program to find sum of diagonal elements of a matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[10][10],i,j,sum=0,m,n;

printf("\nEnter the row and column of matrix: ");

scanf("%d %d",&m,&n);

printf("\nEnter the elements of matrix: ");

        for(i=0;i<m;i++)

        for(j=0;j<n;j++)

scanf("%d",&a[i][j]);

printf("\nThe matrix is\n");

        for(i=0;i<m;i++)

{

printf("\n");

        for(j=0;j<m;j++)

{

printf("%d\t",a[i][j]);

}

}

        for(i=0;i<m;i++)

{

        for(j=0;j<n;j++)

{

        if(i==j)

           sum=sum+a[i][j];

}

}

printf("\n\nSum of the diagonal elements of a matrix is: %d",sum);

return 0;

getch();

}

Sample output:

Enter the row and column of matrix: 3 3

Enter the elements of matrix: 2

3

5

6

7

9

2

6

7

The matrix is

2       3       5

6       7       9

2       6       7

Sum of the diagonal elements of a matrix is: 16

# 
63\. Write a program to check whether two matrices are equal or not.

#include<stdio.h>

#include<stdlib.h>

#include<conio.h>

int main()

{

int a[10][10], b[10][10];

int i, j, row1, column1, row2, column2, flag = 1;

printf("Enter the order of the matrix A \n");

scanf("%d %d", &row1, &column1);

printf("Enter the order of the matrix B \n");

scanf("%d %d", &row2, &column2);

printf("Enter the elements of matrix A \n");

             for (i = 0; i < row1; i++)

{

             for (j = 0; j < column1; j++)

{

scanf("%d", &a[i][j]);

}

}

printf("Enter the elements of matrix B \n");

              for (i = 0; i < row2; i++)

{

              for (j = 0; j < column2; j++)

{

scanf("%d", &b[i][j]);

}

}

printf("MATRIX A is \n");

              for (i = 0; i < row1; i++)

{

              for (j = 0; j < column1; j++)

{

printf("%3d", a[i][j]);

}

printf("\n");

}

printf("MATRIX B is \n");

               for (i = 0; i < row2; i++)

{

               for (j = 0; j < column2; j++)

{

printf("%3d", b[i][j]);

}

printf("\n");

}

                 if (row1 == row2 && column1 == column2)

{

printf("Matrices can be compared \n");

                   for (i = 0; i < row1; i++)

{

                   for (j = 0; j < column2; j++)

{

                   if (a[i][j] != b[i][j])

{

                           flag = 0;

                   break;

}

}

}

}

                    else

{

printf(" Cannot be compared\n");

                    exit(1);

}

                     if (flag == 1)

printf("Two matrices are equal \n");

                     else

printf("But, two matrices are not equal \n");

return 0;

getch();

}

Sample output:

Enter the order of the matrix A

3

3

Enter the order of the matrix B

3

3

Enter the elements of matrix A

1

2

3

4

5

6

7

8

9

Enter the elements of matrix B

1

2

3

4

5

6

7

8

9

MATRIX A is

  1  2  3

  4  5  6

  7  8  9

MATRIX B is

  1  2  3

  4  5  6

  7  8  9

Matrices can be compared

Two matrices are equal.

# 
64\. Write a program to check whether a given matrix is identity matrix or not.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[10][10];

int i, j, row, column, flag = 1;

printf("Enter the order of the matrix A \n");

scanf("%d %d", &row, &column);

printf("Enter the elements of matrix A \n");

              for (i = 0; i < row; i++)

{

              for (j = 0; j < column; j++)

{

scanf("%d", &a[i][j]);

}

}

printf("MATRIX A is \n");

               for (i = 0; i < row; i++)

{

               for (j = 0; j < column; j++)

{

printf("%3d", a[i][j]);

}

printf("\n");

}

               for (i = 0; i < row; i++)

{

               for (j = 0; j < column; j++)

{

               if (a[i][j] != 1 && a[j][i] != 0)

{

                      flag = 0;

              break;

}

}

}

               if (flag == 1 )

printf("It is identity matrix \n");

               else

printf("It is not a identity matrix \n");

return 0;

getch();

}

Sample output:

Enter the order of the matrix A

2

3

Enter the elements of matrix A

1

2

3

9

8

7

MATRIX A is

  1  2  3

  9  8  7

It is not an identity matrix

Identity Matrix:

A square matrix in which all the elements of the principal diagonal are ones and all other elements are zeros. The effect of multiplying a given matrix by an identity matrix is to leave the given matrix unchanged.

# 
65\. Write a program to check whether a given matrix is a sparse matrix or dense matrix.

#include<stdio.h>

#include<conio.h>

int main ()

{

static int array[10][10];

int i, j, m, n;

int counter = 0;

printf("Enter the order of the matix \n");

scanf("%d %d", &m, &n);

printf("Enter the co-efficients of the matix \n");

              for (i = 0; i < m; ++i)

{

              for (j = 0; j < n; ++j)

{

scanf("%d", &array[i][j]);

              if (array[i][j] == 0)

{

                     ++counter;

}

}

}

               if (counter > ((m * n) / 2))

{

printf("The given matrix is sparse matrix \n");

}

               else

printf("The given matrix is dense matrix \n");

printf("There are %d number of zeros", counter);

return 0;

getch();

}

Sample output:

Enter the order of the matix

2

3

Enter the co-efficients of the matix

2

3

5

0

7

0

The given matrix is dense matrix.

There are 2 numbers of zeros.

Note-

A sparse matrix is a matrix in which most of the elements are zero. By contrast, if most of the elements are nonzero, then the matrix is considered dense.

# 
66\. Write a program to calculate sum of the elements of each row and column.

#include<stdio.h>

#include<conio.h>

int Addrow(int array1[10][10], int k, int c);

int Addcol(int array1[10][10], int k, int r);

int main()

{

int arr[10][10];

int i, j, row, col, rowsum, colsum, sumall=0;

printf("Enter the order of the matrix \n");

scanf("%d %d", &row, &col);

printf("Enter the elements of the matrix \n");

              for (i = 0; i < row; i++)

{

              for (j = 0; j < col; j++)

{

scanf("%d", &arr[i][j]);

}

}

printf("Input matrix is \n");

              for (i = 0; i < row; i++)

{

              for (j = 0; j < col; j++)

{

printf("%3d", arr[i][j]);

}

printf("\n");

}

               for (i = 0; i < row; i++)

{

                      rowsum = Addrow(arr, i, col);

printf("Sum of row %d = %d\n", i + 1, rowsum);

}

              for (j = 0; j < col; j++)

{

                      colsum = Addcol(arr, j, row);

printf("Sum of column  %d = %d\n", j + 1, colsum);

}

               for (j = 0; j < row; j++)

{

                      sumall = sumall + Addrow(arr, j, col);

}

printf("Sum of all elements of matrix = %d\n", sumall);

}

int Addrow(int array1[10][10], int k, int c)

{

int rsum = 0, i;

                for (i = 0; i < c; i++)

{

                       rsum = rsum + array1[k][i];

}

return(rsum);

}

int Addcol(int array1[10][10], int k, int r)

{

int csum = 0, j;

                for (j = 0; j < r; j++)

{

                       csum = csum + array1[j][k];

}

return(csum);

getch();

}

Sample output:

Enter the order of the matrix

3

3

Enter the elements of the matrix

1

2

3

4

5

6

7

8

9

Input matrix is

  1  2  3

  4  5  6

  7  8  9

Sum of row 1 = 6

Sum of row 2 = 15

Sum of row 3 = 24

Sum of column 1 = 12

Sum of column 2 = 15

Sum of column 3 = 18

Sum of all elements of matrix = 45

# 
67\. Write a program to find the frequency of Odd and Even numbers in the given matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

static int array[10][10];

int i, j, m, n, even = 0, odd = 0;

printf("Enter the order of the matrix: \n");

scanf("%d %d", &m, &n);

printf("Enter the coefficients of matrix: \n");

                   for (i = 0; i < m; ++i)

{

              for (j = 0; j < n; ++j)

{

scanf("%d", &array[i][j]);

               if ((array[i][j] % 2) == 0)

{

                     ++even;

}

               else

                     ++odd;

}

}

printf("The given matrix is: \n");

                    for (i = 0; i < m; ++i)

{

               for (j = 0; j < n; ++j)

{

printf(" %d", array[i][j]);

}

printf("\n");

}

printf("\n The frequency of occurance of odd number = %d \n", odd);

printf("The frequency of occurance of even number = %d\n", even);

return 0;

getch();

}

Sample output:

Enter the order of the matrix:

2

3

Enter the coefficients of matrix:

1

2

3

4

5

6

The given matrix is:

1 2 3

4 5 6

The frequency of occurance of odd number = 3

The frequency of occurance of even number = 3

# 
68\. Write a program for swapping of two arrays.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[10],b[10],c[10],i;

printf("Enter First array:");

        for(i=0;i<10;i++)

scanf("%d",&a[i]);

printf("\nEnter Second array:");

        for(i=0;i<10;i++)

scanf("%d",&b[i]);

printf("Arrays before swapping:");

printf("\nFirst array:");

        for(i=0;i<10;i++)

{

printf("%d",a[i]);

}

printf("\nSecond array:");

        for(i=0;i<10;i++)

{

printf("%d",b[i]);

}

        for(i=0;i<10;i++)

{

            c[i]=a[i];

            a[i]=b[i];

            b[i]=c[i];

}

printf("\nArrays after swapping:");

printf("\nFirst array:");

        for(i=0;i<10;i++){

            printf("%d",a[i]);

  }

  printf("\nSecond array:");

  for(i=0;i<10;i++){

            printf("%d",b[i]);

  }

  return 0;

getch();

}

Sample output:

Enter First array: 1 2 3 4 5 6 7 8 9 9

Enter Second array: 9 8 7 6 5 4 3 2 1 1

Arrays before swapping:

First array: 1 2 3 4 5 6 7 8 9 9

Second array: 9 8 7 6 5 4 3 2 1 1

Arrays after swapping:

First array: 9 8 7 6 5 4 3 2 1 1

Second array: 1 2 3 4 5 6 7 8 9 9

# 
69\. Write a program to print lower triangular matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[3][3],i,j;

float determinant=0;

printf("Enter the 9 elements of matrix: ");

         for(i=0;i<3;i++)

         for(j=0;j<3;j++)

scanf("%d",&a[i][j]);

printf("\nThe matrix is\n");

         for(i=0;i<3;i++)

{

printf("\n");

         for(j=0;j<3;j++)

printf("%d\t",a[i][j]);

}

printf("\nSetting zero in upper triangular matrix\n");

         for(i=0;i<3;i++)

{

printf("\n");

         for(j=0;j<3;j++)

         if(i>=j)

printf("%d\t",a[i][j]);

         else

printf("%d\t",0);

}

return 0;

getch();

}

Sample output:

Enter the 9 elements of matrix: 1

2

3

4

5

6

7

8

9

The matrix is

1       2       3

4       5       6

7       8       9

Setting zero in upper triangular matrix

1       0       0

4       5       0

7       8       9

# 
70\. Write a program to print upper triangular matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[3][3],i,j;

float determinant=0;

printf("Enter the 9 elements of matrix: ");

         for(i=0;i<3;i++)

         for(j=0;j<3;j++)

scanf("%d",&a[i][j]);

printf("\nThe matrix is\n");

         for(i=0;i<3;i++)

{

printf("\n");

         for(j=0;j<3;j++)

printf("%d\t",a[i][j]);

}

printf("\nSetting zero in lower triangular matrix\n");

         for(i=0;i<3;i++)

{

printf("\n");

         for(j=0;j<3;j++)

         if(i<=j)

printf("%d\t",a[i][j]);

         else

printf("%d\t",0);

}

return 0;

getch();

}

Sample output:

Enter the 9 elements of matrix: 1

2

3

4

5

6

7

8

9

The matrix is

1       2       3

4       5       6

7       8       9

Setting zero in lower triangular matrix

1       2       3

0       5       6

0       0       9

# 
71\. Write a program for multiplication of two matrices.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[5][5],b[5][5],c[5][5],i,j,k,sum=0,m,n,o,p;

printf("\nEnter the row and column of first matrix:");

scanf("%d %d",&m,&n);

printf("\nEnter the row and column of second matrix:");

scanf("%d %d",&o,&p);

         if(n!=o)

{

printf("Matrix mutiplication is not possible");

printf("\nColumn of first matrix must be same as row of second matrix");

}

         else

{

printf("\nEnter the First matrix:");

         for(i=0;i<m;i++)

         for(j=0;j<n;j++)

scanf("%d",&a[i][j]);

printf("\nEnter the Second matrix:");

         for(i=0;i<o;i++)

         for(j=0;j<p;j++)

scanf("%d",&b[i][j]);

printf("\nThe First matrix is:\n");

         for(i=0;i<m;i++)

{

printf("\n");

         for(j=0;j<n;j++)

{

printf("%d\t",a[i][j]);

}

}

printf("\nThe Second matrix is:\n");

         for(i=0;i<o;i++)

{

printf("\n");

         for(j=0;j<p;j++)

{

printf("%d\t",b[i][j]);

}       

}

         for(i=0;i<m;i++)

         for(j=0;j<p;j++)

              c[i][j]=0;

         for(i=0;i<m;i++)

{ 

         for(j=0;j<p;j++)

{

              sum=0;

         for(k=0;k<n;k++)

              sum=sum+a[i][k]*b[k][j];

              c[i][j]=sum;

}

}

}

printf("\nThe multiplication of two matrix is:\n");

         for(i=0;i<m;i++)

{

printf("\n");

         for(j=0;j<p;j++)

{

printf("%d\t",c[i][j]);

}

}

return 0;

getch();

}

Sample output:

Enter the row and column of first matrix: 2 2

Enter the row and column of second matrix: 2 2

Enter the First matrix: 2 3 4 5

Enter the Second matrix: 6 7 8 9

The First matrix is:

2       3

4       5

The Second matrix is:

6       7

8       9

The multiplication of two matrices is:

36      41

64      73

# 
72\. Write a program to find inverse of a matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[3][3],i,j;

float determinant=0;

printf("Enter the 9 elements of matrix: ");

          for(i=0;i<3;i++)

          for(j=0;j<3;j++)

scanf("%d",&a[i][j]);

printf("\nThe matrix is\n");

          for(i=0;i<3;i++)

{

printf("\n");

          for(j=0;j<3;j++)

printf("%d\t",a[i][j]);

}

          for(i=0;i<3;i++)

          determinant = determinant + (a[0][i]*(a[1][(i+1)%3]*a[2][(i+2)%3] - a[1][(i+2)%3]*a[2][(i+1)%3]));

printf("\nInverse of matrix is: \n\n");

          for(i=0;i<3;i++)

{

          for(j=0;j<3;j++)

printf("%.2f\t",( (a[(i+1)%3][(j+1)%3]*a[(i+2)%3][(j+2)%3]) - (a[(i+1)%3][(j+2)%3]*a[(i+2)%3][(j+1)%3]) )/ determinant);

printf("\n");

}

return 0;

getch();

}

Sample output:

Enter the 9 elements of matrix: 3

5

2

1

5

8

3

9

2

The matrix is

3       5       2

1       5       8

3       9       2

Inverse of matrix is:

0.70    -0.25   0.07

-0.09   -0.00   0.14

-0.34   0.25    -0.11

# 
73\. Write a program to find transpose of matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[10][10], trans[10][10], r, c, i, j;

printf("Enter rows and column of matrix: ");

scanf("%d %d", &r, &c);

printf("\nEnter elements of matrix:\n");

          for(i=0; i<r; ++i)

          for(j=0; j<c; ++j)

{

printf("Enter elements a%d%d: ",i+1,j+1);

scanf("%d",&a[i][j]);

}

printf("\nEntered Matrix: \n");

           for(i=0; i<r; ++i)

           for(j=0; j<c; ++j)

{

printf("%d  ",a[i][j]);

            if(j==c-1)

printf("\n\n");

}

           for(i=0; i<r; ++i)

           for(j=0; j<c; ++j)

{

                 trans[j][i]=a[i][j];

}

printf("\nTranspose of Matrix:\n");

            for(i=0; i<c; ++i)

            for(j=0; j<r; ++j)

{

printf("%d  ",trans[i][j]);

           if(j==r-1)

printf("\n\n");

}

return 0;

getch();

}

Sample output:

Enter rows and column of matrix: 2

3

Enter elements of matrix:

Enter elements a11: 1

Enter elements a12: 2

Enter elements a13: 3

Enter elements a21: 4

Enter elements a22: 5

Enter elements a23: 6

Entered Matrix:

1  2  3

4  5  6

Transpose of Matrix:

1  4

2  5

3  6

# 
74\. Write a program to find determinant of a matrix.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[3][3],i,j;

int determinant=0;

printf("Enter the 9 elements of matrix: ");

        for(i=0;i<3;i++)

        for(j=0;j<3;j++)

scanf("%d",&a[i][j]);

printf("\nThe First matrix is\n");

        for(i=0;i<3;i++)

{

printf("\n");

        for(j=0;j<3;j++)

printf("%d\t",a[i][j]);

}

        for(i=0;i<3;i++)

            determinant = determinant + (a[0][i]*(a[1][(i+1)%3]*a[2][(i+2)%3] - a[1][(i+2)%3]*a[2][(i+1)%3]));

printf("\nDeterminant of matrix is: %d",determinant);

return 0;

getch();

}

Sample output:

Enter the 9 elements of matrix: 1

3

2

5

4

6

7

9

8

The First matrix is

1       3       2

5       4       6

7       9       8

Determinant of matrix is: 18

# 
75\. Write a program to find the largest element in an array.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[50],size,i,big;

printf("\nEnter the size of the array: ");

scanf("%d",&size);

printf("\nEnter %d elements in to the array: ”, size);

        for(i=0;i<size;i++)

scanf("%d",&a[i]);

            big=a[0];

        for(i=1;i<size;i++)

{

        if(big<a[i])

            big=a[i];

}

printf("\nBiggest: %d",big);

return 0;

getch();

}

Sample output:

Enter the size of the array: 5

Enter 5 elements in to the array: 3

6

9

8

7

Biggest: 9

# 
76\. Write a program to find the second largest element in an array.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[50],size,i,j=0,big,secondbig;

printf("Enter the size of the array: ");

scanf("%d",&size);

printf("Enter %d elements in to the array: ", size);

        for(i=0;i<size;i++)

scanf("%d",&a[i]);

               big=a[0];

        for(i=1;i<size;i++)

{

        if(big<a[i])

{

            big=a[i];

            j = i;

}

}

            secondbig=a[size-j-1];

        for(i=1;i<size;i++)

{

        if(secondbig <a[i] && j != i)

            secondbig =a[i];

}

printf("Second biggest: %d", secondbig);

return 0;

getch();

}

Sample output:

Enter the size of the array: 5

Enter 5 elements in to the array: 2

4

6

8

9

Second biggest: 8

# 
77\. Write a program to find the second smallest element in an array.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[50],size,i,j=0,small,secondsmall;

printf("Enter the size of the array: ");

scanf("%d",&size);

printf("Enter %d elements in to the array: ", size);

        for(i=0;i<size;i++)

scanf("%d",&a[i]);

                                small=a[0];

        for(i=1;i<size;i++)

{

                      if(small>a[i])

{

            small=a[i];

            j = i;

}

}

                                 secondsmall=a[size-j-1];

        for(i=1;i<size;i++){

        if(secondsmall > a[i] && j != i)

            secondsmall =a[i];

}

printf("Second smallest: %d", secondsmall);

return 0;

getch();

}

Sample output:

Enter the size of the array: 5

Enter 5 elements in to the array: 5 7 3 2 6

Second smallest: 3

# 
78\. Write a program to insert an element in an array at desired position.

#include<stdio.h>

#include<conio.h> 

int main()

{

int array[100], position, c, n, value;

printf("Enter number of elements in array\n");

scanf("%d", &n);

printf("Enter %d elements\n", n);

        for (c = 0; c < n; c++)

scanf("%d", &array[c]);

printf("Enter the location where you wish to insert an element\n");

scanf("%d", &position);

printf("Enter the value to insert\n");

scanf("%d", &value);

        for (c = n - 1; c >= position - 1; c--)

             array[c+1] = array[c]; 

             array[position-1] = value;

printf("Resultant array is\n");

        for (c = 0; c <= n; c++)

printf("%d\n", array[c]);

return 0;

getch();

}

Sample output:

Enter number of elements in array

5

Enter 5 elements

1

2

3

4

5

Enter the location where you wish to insert an element

3

Enter the value to insert

8

Resultant array is

1

2

8

3

4

5

# 
79\. Write a program to remove duplicate elements in an array.

#include<stdio.h>

#include<conio.h>

int main()

{

int arr[50];

int *p;

int i,j,k,size,n;

printf("\nEnter size of the array: ");

scanf("%d",&n);

printf("\nEnter %d elements into the array: ",n);

        for(i=0;i<n;i++)

scanf("%d",&arr[i]);

            size=n;

            p=arr;

        for(i=0;i<size;i++)

{

        for(j=0;j<size;j++)

{

        if(i==j)

{

        continue;

}

        else if(*(p+i)==*(p+j))

{

             k=j;

             size--;

        while(k < size)

{

              *(p+k)=*(p+k+1);

               k++;

}

               j=0;

}

}

}

printf("\nThe array after removing duplicates is: ");

        for(i=0;i < size;i++)

{

printf(" %d",arr[i]);

}

return 0;

getch();

}

Sample output:

Enter size of the array: 5

Enter 5 elements into the array: 1

2

2

3

3

The array after removing duplicates is:  1 2 3

# 
80\. Write a program to delete an element at desired position from an array.

#include<stdio.h>

#include<conio.h>

int main()

{

int a[50],i,pos,size;

printf("\nEnter size of the array: ");

scanf("%d",&size);

printf("\nEnter %d elements in to the array: ",size);

        for(i=0;i<size;i++)

scanf("%d",&a[i]);

printf("\nEnter position where to delete: ");

scanf("%d",&pos);

                                i=0;

        while(i!=pos-1)

            i++;

        while(i<10)

{

            a[i]=a[i+1];

            i++;

}

                                  size--;

        for(i=0;i<size;i++)

printf(" %d",a[i]);

return 0;

getch();

}

Sample output:

Enter size of the array: 5

Enter 5 elements in to the array: 1

2

3

4

5

Enter position where to delete: 3

1 2 4 5

# 
81\. Write a program to compare two strings using “strcmp” functions.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char a[100], b[100];

printf("Enter the first string: ");

gets(a);

printf("Enter the second string: ");

gets(b);

           if (strcmp(a,b) == 0)

printf("Entered strings are equal.\n");

           else

printf("Entered strings are not equal.\n");

return 0;

getch();

}

Sample Output:

Enter the first string: rohit

Enter the second string: rohit

Entered strings are equal.

# 
82\. Write a program to compare two strings without using string functions.

#include<stdio.h>

#include<conio.h>

int stringCompare(char[],char[]);

int main()

{

char str1[100],str2[100];

int compare;

printf("Enter first string: ");

scanf("%s",str1);

printf("Enter second string: ");

scanf("%s",str2);

compare = stringCompare(str1,str2);

          if(compare == 1)

printf("Both strings are equal.");

        else

printf("Both strings are not equal");

return 0;

getch();

}

int stringCompare(char str1[],char str2[])

{

int i=0,flag=0;

          while(str1[i]!='\0' && str2[i]!='\0')

{

         if(str1[i]!=str2[i])

{

               flag=1;

         break;

}

               i++;

}

           if (flag==0 && str1[i]=='\0' && str2[i]=='\0')

return 1;

         else

return 0;

}

Sample output:

Enter first string: Rohit

Enter second string: Rohit

Both strings are equal.

Enter first string: Rohit

Enter second string: Kumar

Both strings are not equal.

# 
83\. Write a program to find length of string using “strlen” function.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char a[100];

int length;

printf("Enter a string to calculate it's length: ");

gets(a);

length = strlen(a);

printf("Length of entered string is = %d\n",length);

return 0;

getch();

}

Sample Output:

Enter a string to calculate it's length: awesome

Length of entered string is = 7

# 
84\. Write a program to find length of string without using library function.

#include<stdio.h>

#include<conio.h>

int main()

{

char str[100];

int length;

printf("\nEnter the String : ");

gets(str);

                        length = 0;

      while (str[length] != '\0')

                        length++;

printf("\nLength of the String is : %d", length);

return(0);

getch();

}

Sample program:

Enter the String: rohit

Length of the String is: 5

# 
85\. Write a program to copy string using “strcpy” library function.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char source[1000], destination[1000];

printf("Input a string: ");

gets(source);

strcpy(destination, source);

printf("Source string:      \"%s\"\n", source);

printf("Destination string: \"%s\"\n", destination);

return 0;

getch();

}

Sample output:

Input a string: amazing

Source string: “amazing”

Destination string: “amazing”

# 
86\. Write a program to copy string without using strcpy library function.

#include<stdio.h>

#include<conio.h>

void stringCopy(char[],char[]);

int main()

{

char str1[100],str2[100];

printf("Enter any string: ");

scanf("%s",str1);

stringCopy(str1,str2);

printf("After copying: %s",str2);

return 0;

getch();

}

void stringCopy(char str1[],char str2[])

{

int i=0;

        while(str1[i]!='\0')

{

              str2[i] = str1[i];

              i++;

}

              str2[i]='\0';

}

Sample output:

Enter any string: rohit

After copying: rohit

# 
87\. Write a program to reverse a string using “strrev” library function.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char arr[100];

printf("Enter a string to reverse: ");

gets(arr);

strrev(arr);

printf("Reverse of entered string is: %s\n",arr);

return 0;

getch();

}

Sample Output:

Enter a string to reverse: spectacular

Reverse of entered string is: ralucatceps

# 
88\. Write a program to reverse a string without using strrev library function.

#include<stdio.h>

#include<conio.h>

int main()

{

char str[50];

char rev[50];

int i=-1,j=0;

printf("Enter any string : ");

scanf("%s",str);

         while(str[++i]!='\0');

         while(i>=0)

                  rev[j++] = str[--i];

                  rev[j]='\0';

printf("Reverse of string is : %s",rev);

return 0;

getch();

}

Sample output:

Enter any string: rohit

Reverse of string is: tihor

# 
89\. Write a program for Swapping of strings.

#include<stdio.h>

#include<string.h>

#include<conio.h>

#include<malloc.h>

int main()

{

char first[100], second[100], *temp;

printf("Enter the first string:\n");

gets(first);

printf("Enter the second string:\n");

gets(second);

printf("\nBefore Swapping:\n");

printf("First string: %s\n",first);

printf("Second string: %s\n\n",second);

            temp = (char*)malloc(100);

            strcpy(temp,first);

            strcpy(first,second);

            strcpy(second,temp);

printf("After Swapping:\n");

printf("First string: %s\n",first);

printf("Second string: %s\n",second);

return 0;

getch();

}

Sample output:

Enter the first string:

hello

Enter the second string:

bye

Before Swapping:

First string: hello

Second string: bye

After Swapping:

First string: bye

Second string: hello

# 
90\. Write a Program to sort a string in alphabetic order.

#include<stdio.h>

#include<conio.h>

#include<stdlib.h>

#include<string.h>

int main()

{

char ch, input[100], output[100];

int no[26] = {0}, n, c, t, x;

printf("Enter some text\n");

scanf("%s", input);

             n = strlen(input);

        for (c = 0; c < n; c++)

{

             ch = input[c] - 'a';

             no[ch]++;

}

             t = 0;

        for (ch = 'a'; ch <= 'z'; ch++)

{

             x = ch - 'a';

        for (c = 0; c < no[x]; c++)

{

             output[t] = ch;

             t++;

}

}

             output[t] = '\0';

printf("%s\n", output);

return 0;

getch();

}

Sample program:

Enter some text

game

aegm

# 
91\. Write a program to find palindrome of string.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char a[100], b[100];

printf("Enter the string to check if it is a palindrome: ");

gets(a);

strcpy(b,a);

strrev(b);

         if (strcmp(a,b) == 0)

printf("Entered string is a palindrome\n");

        else

printf("Entered string is not a palindrome\n");

return 0;

getch();

}

Sample Output:

Enter the string to check if it is a palindrome: amazing

Entered string is not a palindrome

# 
92\. Write a program to find palindrome of string without using string function.

#include<stdio.h>

#include<conio.h>

int main()

{

char str[100];

int i=0,j=-1,flag=0;

printf("Enter a string: ");

scanf("%s",str);

          while(str[++j]!='\0');

              j--;

        while(i<j)

        if(str[i++] != str[j--]){

              flag=1;

        break;

}

        if(flag == 0)

printf("The string is a palindrome");

        else

printf("The string is not a palindrome");

return 0;

getch();

}

Sample output:

Enter a string: rohit

The string is not a palindrome

Enter a string: wow

The string is a palindrome

# 
93\. Write a program for String concatenation using “strcat” string functions.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int main()

{

char a[1000], b[1000];

printf("Enter the first string: ");

gets(a);

printf("Enter the second string: ");

gets(b);

strcat(a,b);

printf("String obtained on concatenation is %s\n",a);

return 0;

getch();

}

Sample Output:

Enter the first string: awesome

Enter the second string: amazing

String obtained on concatenation is awesomeamazing

# 
94\. Write a program for String concatenation without using string functions.

#include<stdio.h>

#include<conio.h>

void stringConcat(char[],char[]);

int main()

{

char str1[100],str2[100];

int compare;

printf("Enter first string: ");

scanf("%s",str1);

printf("Enter second string: ");

scanf("%s",str2);

               stringConcat(str1,str2);

printf("String after concatenation: %s",str1);

return 0;

getch();

}

void stringConcat(char str1[],char str2[])

{

int i=0,j=0;

        while(str1[i]!='\0')

{

             i++;

}

          while(str2[j]!='\0')

{

              str1[i] = str2[j];   

              i++;

              j++;

}

str1[i] = '\0';

}

Sample output:

Enter first string: rohit

Enter second string: kumar

String after concatenation: rohitkumar

# 
95\. Write a program to check whether entered character is uppercase letter or not without using library function.

#include<stdio.h>

#include<conio.h>

int main()

{

char ch;

printf("\nEnter The Character : ");

scanf("%c", &ch);

               if (ch >= 'A' && ch <= 'Z')

{

printf("Character is uppercase Letters");

}             else if (ch >= 'a' && ch <= 'z')

{

printf("Character is Not Uppercase Letters");

}

                else

{

printf("Non alphabet character");

}

return(0);

getch();

}

Sample output:

Enter The Character : d

Character is Not Uppercase Letters

Enter The Character : D

Character is uppercase Letters

# 
96\. Write a program for Conversion from uppercase to lower case.

#include<stdio.h>
#include<string.h>

#include<conio.h>

int main()

{

char str[20];

int i;

printf("Enter any string:");

scanf("%s",str);

printf("The string is:%s",str);

        for(i=0;i<=strlen(str);i++)

{

        if(str[i]>=65&&str[i]<=90)

            str[i]=str[i]+32;

}

printf("\nThe string in lower case is:%s",str);

return 0;

getch();

}

Sample output:

Enter any string: ROHIT

The string is: ROHIT

The string in lower case is: rohit

# 
97\. Write a program to delete vowels from string.

#include<stdio.h>

#include<string.h>

#include<conio.h>

int check_vowel(char);

int main()

{

char s[100], t[100];

int i, j = 0;

printf("Enter a string to delete vowels:\n");

gets(s);

        for(i = 0; s[i] != '\0'; i++)

{

        if(check_vowel(s[i]) == 0)

{

             t[j] = s[i];

             j++;

}

}

             t[j] = '\0';

             strcpy(s, t);

printf("String after deleting vowels: %s\n", s);

return 0;

getch();

}

int check_vowel(char c)

{

          switch(c)

{

          case 'a':

          case 'A':

          case 'e':

          case 'E':

          case 'i':

          case 'I':

          case 'o':

          case 'O':

          case 'u':

          case 'U':

          return 1;

          default:

return 0;

}

}

Sample output:

Enter a string to delete vowels:

rohit kumar gupta

String after deleting vowels: rht kmr gpt

# 
98\. Write a program to count number of capital letters, small letter, digits, special symbol at given string.

#include<conio.h>

#include<stdio.h>

int main(void)

{

char str[80];

int x, cap, small, dig, sym;

printf("\nEnter a string : ");

gets(str);

                x = cap = small = dig = sym = 0;

            for( ; str[x] != '\0' ; x++)

{

             if(str[x] >= 'A' && str[x] <= 'Z') cap++;

             else if(str[x] >= 'a' && str[x] <= 'z') small++;

             else if(str[x] >= '0' && str[x] <= '9')  dig++;

             else sym++;

}

printf("\nCapital letters %d\nSmall letters %d", cap, small);

printf("\nDigits %d\nSpecial symbols %d", dig, sym);

return 0;

getch();

}

Sample output:

Enter a string: Rohit@123

Capital letters 1

Small letters 4

Digits 3

Special symbols 1

# 
99\. Write a program to find number of vowels, consonants, digits and white space.

#include<stdio.h>

#include<conio.h>

int main()

{

char line[150];

int i,v,c,ch,d,s,o;

o=v=c=ch=d=s=0;

printf("Enter a line of string:\n");

gets(line);

               for(i=0;line[i]!='\0';++i)

{

        if(line[i]=='a' || line[i]=='e' || line[i]=='i' || line[i]=='o' || line[i]=='u' || line[i]=='A' || line[i]=='E' || line[i]=='I' || line[i]=='O' || line[i]=='U')

                       ++v;

        else if((line[i]>='a'&& line[i]<='z') || (line[i]>='A'&& line[i]<='Z'))

                       ++c;

        else if(line[i]>='0'&&c<='9')

                       ++d;

        else if (line[i]==' ')

                       ++s;

}

printf("Vowels: %d",v);

printf("\nConsonants: %d",c);

printf("\nDigits: %d",d);

printf("\nWhite spaces: %d",s);

return 0;

getch();

}

Sample output:

Enter a line of string:

My name is Rohit Kumar Gupta

Vowels: 6

Consonants: 9

Digits: 0

White spaces: 2

# 
100\. Write a program to check whether two strings are anagrams or not.

#include<stdio.h>

#include<conio.h>

int check_anagram(char [], char []);

int main()

{

char a[100], b[100];

int flag;

printf("Enter first string:\n");

gets(a);

printf("Enter second string:\n");

gets(b);

flag = check_anagram(a, b);

           if (flag == 1)

printf("\"%s\" and \"%s\" are anagrams.\n", a, b);

           else

printf("\"%s\" and \"%s\" are not anagrams.\n", a, b);

return 0;

getch();

}

int check_anagram(char a[], char b[])

{

int first[26] = {0}, second[26] = {0}, c = 0;

            while (a[c] != '\0')

{

                       first[a[c]-'a']++;

                       c++;

}

c = 0;

               while (b[c] != '\0')

{

                          second[b[c]-'a']++;

                          c++;

}

               for (c = 0; c < 26; c++)

{

               if (first[c] != second[c])

return 0;

}

return 1;

}

Sample output:

Enter first string: creative

Enter second string: reactive

"creative" and "reactive" are anagrams.

Anagram:

A word, phrase, or name formed by rearranging the letters of another, such as spar, formed from rasp.

# 
101\. Write a program to remove all characters in second string which are present in first string.

#include <stdio.h>

#include <conio.h>

#include <string.h>

#include <ctype.h>

#include <stdlib.h>

#define CHAR_SIZE 26

void alphacheck(char *, int []);

void create(char [], char [], int[]);

int main()

{

char str1[50], str2[50];

int a1[CHAR_SIZE] = {0};

char str2_rem[50];

printf("Enter string1: ");

scanf("%s", str1);

printf("Enter string2: ");

scanf("%s", str2);

alphacheck(str1, a1);

create(str2_rem, str2, a1);

printf("On removing characters from second string we get: %s\n", str2_rem);

return 0;

getch();

}

void alphacheck(char *str, int a[])

{

int i, index;

                for (i = 0; i < strlen(str); i++)

{

                       str[i] = tolower(str[i]);

                       index = str[i] - 'a';

                 if (!a[index])

{

                       a[index] = 1;

}

}

printf("\n");

}

void create(char str_rem[], char str[], int list[])

{

int i, j = 0, index;

                 for (i = 0; i < strlen(str); i++)

{

                        index = str[i] - 'a';

                 if (!list[index])

{

                         str_rem[j++] = str[i];

}

}

                          str_rem[j] = '\0';

}

Sample output:

Enter string1: develop

Enter string2: developer

On removing characters from second string we get: r

# 
102\. Write a program to reverse a string using both recursion and iteration.

#include<stdio.h>

#include<conio.h>

#include<string.h>

void disp_str1_rec(char *);

int main()

{

char str1[100], *ptr;

int len1 = 0, i;

char ch;

printf("Enter the string:\n");

scanf("%[^\n]s", str1);

ptr = str1;

len1 = strlen(str1);

printf("Using iteration:\n");

             for (i = len1 - 1; i >= 0;i--)

{

                   ch = str1[i];

printf("%c", ch);

}

printf("\nUsing recurssion:\n");

disp_str1_rec(ptr);

getch();

}

void disp_str1_rec(char *stng)

{

char ch;

             if (*stng != '\0')

{

                 ch = *stng;

                 stng++;

                 disp_str1_rec(stng);

printf("%c", ch);

}

              else

return;

}

Sample output:

Enter the string:

Developer

Using iteration:

repoleveD

Using recurssion:

repoleveD

# 
103\. Write a program will accept Year, Month and Date from the user and will display the day of the month.

#include<stdio.h>

#include<conio.h>

#include<math.h>

int fm(int date, int month, int year)

{

int fmonth, leap;

         if ((year % 100 == 0) && (year % 400 != 0))

              leap = 0;

         else if (year % 4 == 0)

              leap = 1;

         else

              leap = 0;

   fmonth = 3 + (2 - leap) * ((month + 2) / (2 * month))

         + (5 * month + month / 9) / 2;

   fmonth = fmonth % 7;

return fmonth;

}

int day_of_week(int date, int month, int year)

{

int dayOfWeek;

int YY = year % 100;

int century = year / 100;

printf("\nDate: %d/%d/%d \n", date, month, year);

   dayOfWeek = 1.25 * YY + fm(date, month, year) + date - 2 * (century % 4);

   dayOfWeek = dayOfWeek % 7;

              switch (dayOfWeek)

{

              case 0:

                         printf("weekday = Saturday");

              break;

              case 1:

                         printf("weekday = Sunday");

              break;

              case 2:

                         printf("weekday = Monday");

              break;

              case 3:

                         printf("weekday = Tuesday");

              break;

              case 4:

                         printf("weekday = Wednesday");

              break;

              case 5:

                         printf("weekday = Thursday");

              break;

              case 6:

                         printf("weekday = Friday");

              break;

              default:

                         printf("Incorrect data");

}

return 0;

getch();

}

int main()

{

int date, month, year;

printf("\nEnter the year: ");

scanf("%d", &year);

printf("\nEnter the month: ");

scanf("%d", &month);

printf("\nEnter the date: ");

scanf("%d", &date);

day_of_week(date, month, year);

return 0;

}

Sample output:

Enter the year: 2016

Enter the month: 02

Enter the date: 26

Date: 26/2/2016

Weekday = Friday

# 
104\. Write a program to convert string into ASCII values.

#include<stdio.h>

#include<conio.h>

int main()

{

char str[100];

int i=0;

printf("Enter any string: ");

scanf("%s",str);

printf("ASCII values of each characters of given string: ");

            while(str[i])

printf("%d ",str[i++]);

return 0;

getch();

}

Sample output:

Enter any string: Rohit

ASCII values of each characters of given string: 82 111 104 105 116

What is ASCII ?

ASCII (American Standard Code for Information Interchange) is the most common format for text files in computers and on the Internet. In an ASCII file, each alphabetic, numeric, or special character is represented with a 7-bit binary number (a string of seven 0s or 1s). 128 possible characters are defined.

# 
105\. Write a program to convert from roman numbers to english numbers.

#include<stdio.h>

#include<conio.h>

#include<string.h>

int digitValue(char);

int main()

{

char roman_Number[1000];

int i=0;

long int number =0;

printf("Enter any roman number (Valid digits are I, V, X, L, C, D, M):  \n");

scanf("%s",roman_Number);

             while(roman_Number[i])

{

              if(digitValue(roman_Number[i]) < 0)

{

printf("Invalid roman digit : %c",roman_Number[i]);

return 0;

}

              if((strlen(roman_Number) -i) > 2)

{

              if(digitValue(roman_Number[i]) <

digitValue(roman_Number[i+2]))

{

printf("Invalid roman number");

return 0;

}

}

               if(digitValue(roman_Number[i]) >= digitValue(roman_Number[i+1]))

             number = number + digitValue(roman_Number[i]);

         else

{

             number = number + (digitValue(roman_Number[i+1]) - digitValue(roman_Number[i]));

             i++;

}

             i++;

}

printf("Its decimal value is : %ld",number);

return 0;

}

int digitValue(char c)

{

int value=0;

               switch(c)

{

                      case 'I': value = 1; break;

                      case 'V': value = 5; break;

                      case 'X': value = 10; break;

                      case 'L': value = 50; break;

                      case 'C': value = 100; break;

                      case 'D': value = 500; break;

                      case 'M': value = 1000; break;

                      case '\0': value = 0; break;

                      default: value = -1; 

}

return value;

}

Sample output:

Enter any roman number (Valid digits are I, V, X, L, C, D, M):

XVIII

Its decimal value is : 18

# 
106\. Write a program to convert any number to english word.

#include<stdio.h>

#include<conio.h>

#include<string.h>

void toWord(int,int);

char * getPositionValue(int);

char * digitToWord(int);

char  word[100][30];

int i =0;

int main()

{

int j,k,subnumer;

unsigned long int number;

printf("Enter any postive number: ");

scanf("%lu",&number);

             if(number ==0)

{

printf("Zero");

return 0;

}

             while(number)

{

             if(i==1)

{

                  toWord(number %10,i);

                  number = number/10;

}

             else

{

                   toWord(number %100,i);

                   number = number/100;

}

                   i++;

}

printf("Number in word: ");

                   *word[i-1] = *word[i-1] - 32;

             for(j=i-1;j>=0;j--)

{

printf("%s",word[j]);

}

getch();

return 0;

}

void toWord(int number,int position)

{

char  numberToword[100]={" "};

              if(number ==0)

{

}

              else if (number < 20 ||number %10==0)

{

                  strcpy(numberToword,digitToWord(number));

}

              else

{

                  strcpy(numberToword,digitToWord((number/10)*10));

                  strcat(numberToword,digitToWord(number%10));

}

                  strcat(numberToword,getPositionValue(position));

                  strcpy(word[i],numberToword);

}

char * getPositionValue(int postion)

{

static char positionValue[10]=" ";

        switch(postion)

{

                case 1: strcpy(positionValue,"hundreds "); break;

                case 2: strcpy(positionValue,"thousand "); break;

                case 3: strcpy(positionValue,"lakh "); break;

                case 4: strcpy(positionValue,"crore "); break;

                case 5: strcpy(positionValue,"arab "); break;

                case 6: strcpy(positionValue,"kharab "); break;

                case 7: strcpy(positionValue,"neel "); break;

                case 8: strcpy(positionValue,"padam "); break;

}

return positionValue;

}

char * digitToWord(int digit)

{

static char digitInWord[10]=" ";

         switch(digit)

{

                 case 1: strcpy(digitInWord , "one "); break;

                 case 2: strcpy(digitInWord , "two "); break;

                 case 3: strcpy(digitInWord , "three "); break;

                 case 4: strcpy(digitInWord , "four "); break;

                 case 5: strcpy(digitInWord , "five "); break;

                 case 6: strcpy(digitInWord , "six "); break;

                 case 7: strcpy(digitInWord , "seven "); break;

                 case 8: strcpy(digitInWord , "eight "); break;

                 case 9: strcpy(digitInWord , "nine ");break;

                 case 10: strcpy(digitInWord , "ten "); break;

                 case 11: strcpy(digitInWord , "eleven "); break;

                 case 12: strcpy(digitInWord , "twelve "); break;

                 case 13: strcpy(digitInWord , "thirteen "); break;

                 case 14: strcpy(digitInWord , "fourteen "); break;

                 case 15: strcpy(digitInWord , "fifteen "); break;

                 case 16: strcpy(digitInWord , "sixteen "); break;

                 case 17: strcpy(digitInWord , "seventeen "); break;

                 case 18: strcpy(digitInWord , "eighteen "); break;

                 case 19: strcpy(digitInWord , "nineteen "); break;

                 case 20: strcpy(digitInWord , "twenty "); break;

                 case 30: strcpy(digitInWord , "thirty "); break;

                 case 40: strcpy(digitInWord , "fourty "); break;

                 case 50: strcpy(digitInWord , "fifty "); break;

                 case 60: strcpy(digitInWord , "sixty "); break;

                 case 70: strcpy(digitInWord , "seventy "); break;

                 case 80: strcpy(digitInWord , "eighty "); break;

                 case 90: strcpy(digitInWord,"ninety "); break;

}

return digitInWord;

}

Sample output:

Enter any postive number: 2385

Number in word: Two thousand three hundreds eighty five

# 
107\. Write a program to add two numbers using pointer.

#include<stdio.h>

#include<conio.h>

int main()

{

int first, second, *p, *q, sum;

printf("Enter two integers to add: ");

scanf("%d%d", &first, &second);

p = &first;

q = &second;

sum = *p + *q;

printf("Sum of entered numbers = %d\n",sum);

return 0;

getch();

}

Sample Output:

Enter two integers to add: 3 , 5

Sum of entered numbers = 8

# 
108\. Write a program to add two numbers using call by reference.

#include<stdio.h>

#include<conio.h>

long add(long *, long *);

int main()

{

long first, second, *p, *q, sum;

printf("Input two integers to add: ");

scanf("%ld%ld", &first, &second);

sum = add(&first, &second);

printf("(%ld) + (%ld) = (%ld)\n", first, second, sum);

return 0;

getch();

}

long add(long *x, long *y)

{

long sum;

sum = *x + *y;

return sum;

}

Sample Output:

Input two integers to add: 4, 5

(4) + (5) = (9)

# 
109\. Write a program for swapping to variables using pointer (call by reference).

#include<stdio.h>

#include<conio.h>

void swap(int *num1, int *num2)

{

int temp;

temp = *num1;

*num1 = *num2;

*num2 = temp;

}

int main()

{

int num1, num2;

printf("\nEnter the first number : ");

scanf("%d", &num1);

printf("\nEnter the Second number : ");

scanf("%d", &num2);

swap(&num1, &num2);

printf("\nFirst number  : %d", num1);

printf("\nSecond number : %d", num2);

return (0);

}

Sample output:

Enter the first number: 12

Enter the Second number: 22

First number: 22

Second number: 12

# 
110\. Write a program to compute sum of the array elements using pointers.

#include<stdio.h>

#include<conio.h>

int main()

{

 int numArray[10];

 int i, sum = 0;

 int *ptr;

 printf("\nEnter 10 elements : ");

             for (i = 0; i < 10; i++)

 scanf("%d", &numArray[i]);

                     ptr = numArray;

             for (i = 0; i < 10; i++)

{

                     sum = sum + *ptr;

                     ptr++;

}

printf("The sum of array elements : %d", sum);

getch();

}

Sample output:

Enter 10 elements: 11 12 13 14 15 16 17 18 19 20

The sum of array elements is 155.

# 
111\. Write a program to find size of structure data type without using size of operator.

#include<stdio.h>

#include<conio.h>

struct student

{

    int roll;

    char name[100];

    float marks;

};

int main()

{

struct student *ptr = 0;

ptr++;

printf("Size of the structure student:  %d",ptr);

return 0;

getch();

}

Sample output:

Size of the structure student:  108

# 
112\. Write a program to store and display information of single student using structure.

#include<stdio.h>

#include<conio.h>

struct student

{

    char name[50], subject[50];

    int roll;

    float marks;

};

int main()

{

struct student s;

printf("Enter information of students:\n\n");

printf("Enter name: ");

scanf("%s",s.name);

printf("Enter roll number: ");

scanf("%d",&s.roll);

printf("Enter subject:");

scanf("%s",s.subject);

printf("Enter marks: ");

scanf("%f",&s.marks);

printf("\nDisplaying Information\n");

printf("Name: %s\n",s.name);

printf("Subject: %s\n",s.subject);

printf("Roll: %d\n",s.roll);

printf("Marks: %.2f\n",s.marks);

return 0;

getch();

}

Sample output:

Enter information of students:

Enter name: Rohit

Enter roll number: 24

Enter subject: CSE

Enter marks: 82

Displaying Information

Name: Rohit

Subject: CSE

Roll: 24

Marks: 82.00

# 
113\. Write a program to read and print details of 50 students using structure.

#include<stdio.h>

#include<conio.h>

#define SIZE 50

struct student

{

   char name[30];

   int rollno;

   int sub[3];

};

int main()

{

int i, j, max, count, total, n, a[SIZE], ni;

struct student st[SIZE];

printf("Enter how many students: ");

scanf("%d", &n);

            for (i = 0; i < n; i++)

{

printf("\nEnter name and roll number for student %d : ", i);

scanf("%s", &st[i].name);

scanf("%d", &st[i].rollno);

}

             for (i = 0; i < n; i++)

{

             for (j = 0; j <= 2; j++) {

printf("\nEnter marks of student %d for subject %d : ", i, j);

scanf("%d", &st[i].sub[j]);

}

}

             for (i = 0; i < n; i++)

{

                    total = 0;

             for (j = 0; j < 3; j++)

{

                    total = total + st[i].sub[j];

}

printf("\nTotal marks obtained by student %s are %d", st[i].name,total);

                    a[i] = total;

}

             for (j = 0; j < 3; j++)

{

                    max = 0;

             for (i = 0; i < n; i++)

{

             if (max < st[i].sub[j])

{

                     max = st[i].sub[j];

                     ni = i;

}

}

printf("\nStudent %s got maximum marks = %d in Subject : %d",st[ni].name, max, j);

}

max = 0;

              for (i = 0; i < n; i++)

{

              if (max < a[i])

{

                     max = a[i];

                     ni = i;

}

}

printf("\n%s obtained the total highest marks.", st[ni].name);

getch();

}

Sample output:

Enter how many students: 2

Enter name and roll number for student 0: Rohit

24

Enter name and roll number for student 1: Rohan

25

Enter marks of student 0 for subject 0: 72

Enter marks of student 0 for subject 1: 78

Enter marks of student 0 for subject 2: 85

Enter marks of student 1 for subject 0: 75

Enter marks of student 1 for subject 1: 86

Enter marks of student 1 for subject 2: 89

Total marks obtained by student Rohit are 235

Total marks obtained by student Rohan are 250

Student Rohan got maximum marks = 75 in Subject: 0

Student Rohan got maximum marks = 86 in Subject: 1

Student Rohan got maximum marks = 89 in Subject: 2

Rohan obtained the total highest marks.

# 
114\. Write a program to store information using structure with dynamically memory allocation.

#include<stdio.h>

#include<stdlib.h>

#include<conio.h>

struct name

{

   int a;

   char c[30];

};

int main()

{

struct name *ptr;

int i,n;

printf("Enter n: ");

scanf("%d",&n);

ptr=(struct name*)malloc(n*sizeof(struct name));

             for(i=0;i<n;++i)

{

printf("Enter string and integer respectively:\n");

scanf("%s%d",&(ptr+i)->c, &(ptr+i)->a);

}

printf("Displaying Information:\n");

             for(i=0;i<n;++i)

printf("%s\t%d\t\n",(ptr+i)->c,(ptr+i)->a);

return 0;

getch();

}

Sample output:

Enter n: 2

Enter string and integer respectively:

Programming

22

Enter string and integer respectively:

Structure

33

Displaying Information:

Programming     22

Structure       33

# 
115\. Write a program to print sum of two complex numbers by passing structure to a function.

#include<stdio.h>

#include<conio.h>

typedef struct complex

{

    float real;

    float imag;

}complex;

complex add(complex n1,complex n2);

int main(){

complex n1,n2,temp;

printf("For 1st complex number \n");

printf("Enter real and imaginary respectively:\n");

scanf("%f%f",&n1.real,&n1.imag);

printf("\nFor 2nd complex number \n");

printf("Enter real and imaginary respectively:\n");

scanf("%f%f",&n2.real,&n2.imag);

            temp=add(n1,n2);

printf("Sum=%.1f+%.1fi",temp.real,temp.imag);

return 0;

}

complex add(complex n1,complex n2)

{

         complex temp;

         temp.real=n1.real+n2.real;

temp.imag=n1.imag+n2.imag;

return(temp);

getch();

}

Sample output:

For 1st complex number

Enter real and imaginary respectively:

2

4

For 2nd complex number

Enter real and imaginary respectively:

6

7

Sum=8.0+11.0i

# 
116\. Write a program to see difference between union and structure.

#include<stdio.h>

#include<conio.h>

union job

{

char name[32];

float salary;

int worker_no;

}u;

struct job1

{

char name[32];

float salary;

int worker_no;

}s;

int main()

{

printf("size of union = %d",sizeof(u));

printf("\nsize of structure = %d", sizeof(s));

return 0;

getch();

}

Sample Output:

size of union = 32

size of structure = 40

# 
117\. Write a program to read or open a file.

#include<stdio.h>

#include<stdlib.h>

#include<conio.h> 

int main()

{

char ch, file_name[25];

FILE *fp;

printf("Enter the name of file you wish to see\n");

gets(file_name);

fp = fopen(file_name,"r");

             if( fp == NULL )

{

perror("Error while opening the file.\n");

exit(EXIT_FAILURE);

}

printf("The contents of %s file are :\n", file_name);

             while( ( ch = fgetc(fp) ) != EOF )

printf("%c",ch);

fclose(fp);

return 0;

getch();

}

# 
118\. Write a program to copy files.

#include<stdio.h>

#include<stdlib.h> 

int main()

{

char ch, source_file[20], target_file[20];

FILE *source, *target;

printf("Enter name of file to copy\n");

gets(source_file);

source = fopen(source_file, "r");

             if( source == NULL )

{

printf("Press any key to exit...\n");

exit(EXIT_FAILURE);

}

printf("Enter name of target file\n");

gets(target_file);

target = fopen(target_file, "w");

             if( target == NULL )

{

             fclose(source);

printf("Press any key to exit...\n");

exit(EXIT_FAILURE);

}

              while( ( ch = fgetc(source) ) != EOF )

                       fputc(ch, target);

printf("File copied successfully.\n");

fclose(source);

fclose(target);

return 0;

}

# 
119\. Write a program to merge two files.

#include<stdio.h>

#include<stdlib.h>

#include<conio.h>

int main()

{

FILE *fs1, *fs2, *ft;

char ch, file1[20], file2[20], file3[20];

printf("Enter name of first file\n");

gets(file1);

printf("Enter name of second file\n");

gets(file2);

printf("Enter name of file which will store contents of two files\n");

gets(file3);

                    fs1 = fopen(file1,"r");

                    fs2 = fopen(file2,"r");

              if( fs1 == NULL || fs2 == NULL )

{

perror("Error ");

printf("Press any key to exit...\n");

getch();

exit(EXIT_FAILURE);

}

ft = fopen(file3,"w");

              if( ft == NULL )

{

perror("Error ");

printf("Press any key to exit...\n");

exit(EXIT_FAILURE);

}

              while( ( ch = fgetc(fs1) ) != EOF )

                        fputc(ch,ft);

               while( ( ch = fgetc(fs2) ) != EOF )

                        fputc(ch,ft);

printf("Two files were merged into %s file successfully.\n",file3);

                        fclose(fs1);

                        fclose(fs2);

                        fclose(ft);

return 0;

}

# 
120\. Write a program to delete a file.

#include<stdio.h>

#include<conio.h>

int main()

{

int status;

char file_name[25];

printf("Enter the name of file you wish to delete\n");

gets(file_name);

status = remove(file_name);

             if( status == 0 )

printf("%s file deleted successfully.\n",file_name);

             else

{

printf("Unable to delete the file\n");

perror("Error");

}

return 0;

getch();

}

# 
121\. Write a C program to write all the members of an array of structure to a file using fwrite(). Read the array from the file and display on the screen.

#include<stdio.h>

#include<conio.h>

struct s

{

char name[50];

int height;

};

int main()

{

struct s a[5],b[5];  

FILE *fptr;

int i;

fptr=fopen("file.txt","wb");

            for(i=0;i<5;++i)

{

fflush(stdin);

printf("Enter name: ");

gets(a[i].name);

printf("Enter height: ");

scanf("%d",&a[i].height);

}

fwrite(a,sizeof(a),1,fptr);

fclose(fptr);

fptr=fopen("file.txt","rb");

fread(b,sizeof(b),1,fptr);

           for(i=0;i<5;++i)

{

printf("Name: %s\nHeight: %d",b[i].name,b[i].height);

}

fclose(fptr);

getch();

}

# 
122\. Write a program to write on data file and read from data file.

#include<stdio.h>

#include<conio.h>

struct Student

{

   int roll;

   char name[12];

   int percent;

} s1 = { 10, "SMJC", 80 };

int main()

{

FILE *fp;

struct Student s2;

fp = fopen("ip.txt", "w");

fwrite(&s1, sizeof(s1), 1, fp);

fclose(fp);

fp = fopen("ip.txt", "r");

fread(&s2, sizeof(s2), 1, fp);

fclose(fp);

printf("\nRoll : %d", s2.roll);

printf("\nName : %s", s2.name);

printf("\nPercent : %d", s2.percent);

return (0);

getch();

}

# 
123\. Write a program to concatenate many files and store them in a file.

#include<stdio.h>

#include<conio.h>

void concatenate(FILE *fp1,FILE *fp2,char *argv[],int argc);

int main(int argc,char *argv[]){

FILE *fp1,*fp2;

concatenate(fp1,fp2,argv,argc);

return 0;

getch();

}

void concatenate(FILE *fp1,FILE *fp2,char **argv,int argc)

{

int i,ch;

fp2=fopen("files","a");

           for(i=1;i<argc-1;i++)

{

                  fp1=fopen(argv[i],"r");

            while((ch=getc(fp1))!=EOF)

                   putc(ch,fp2);

}

}

# 
124\. Write a program to find number of lines in text file.

#include<stdio.h>

#include<conio.h>

int main()

{

FILE *fileptr;

int count_lines = 0;

char filechar[40], chr;

printf("Enter file name: ");

scanf("%s", filechar);

fileptr = fopen(filechar, "r");

chr = getc(fileptr);

               while (chr != EOF)

{

               if (chr == 'n')

{

                          count_lines = count_lines + 1;

}

                          chr = getc(fileptr);

}

                          fclose(fileptr);

printf("There are %d lines in %s  in a file\n", count_lines, filechar);

return 0;

getch();

}

# 
125\. Write a program to replace specified line in a text file.

#include<stdio.h>

#include<conio.h>

int main(void)

{

FILE *fileptr1, *fileptr2;

char filechar[40];

char c;

int delete_line, temp = 1;

printf("Enter file name: ");

scanf("%s", filechar);

fileptr1 = fopen(filechar, "r");

c = getc(fileptr1);

              while (c != EOF)

{

printf("%c", c);

c = getc(fileptr1);

}

printf(" \n Enter line number to be deleted and replaced");

scanf("%d", &delete_line);

rewind(fileptr1);

fileptr2 = fopen("replica.c", "w");

c = getc(fileptr1);

            while (c != EOF)

{

            if (c == 'n')

{

                  temp++;

}

             if (temp != delete_line)

{

                  putc(c, fileptr2);

}

             else

{

              while ((c = getc(fileptr1)) != 'n')

{

}

                         printf("Enter new text");

                         fflush(stdin);

                         putc('n', fileptr2);

              while ((c = getchar()) != 'n')

                         putc(c, fileptr2);

                         fputs("n", fileptr2);

                         temp++;

}

                         c = getc(fileptr1);

}

                          fclose(fileptr1);

                          fclose(fileptr2);

                          remove(filechar);

                          rename("replica.c", filechar);

                          fileptr1 = fopen(filechar, "r");

                          c = getc(fileptr1);

               while (c != EOF)

{

                          printf("%c", c);

                          c = getc(fileptr1);

}

fclose(fileptr1);

return 0;

getch();

}

# 
126.  Write a program to delete specific line from a text file.

#include<stdio.h>

#include<conio.h>

int main()

{

FILE *fileptr1, *fileptr2;

char filename[40];

char ch;

int delete_line, temp = 1;

printf("Enter file name: ");

scanf("%s", filename);

fileptr1 = fopen(filename, "r");

ch = getc(fileptr1);

              while (ch != EOF)

{

              printf("%c", ch);

                         ch = getc(fileptr1);

}

                         rewind(fileptr1);

              printf(" \n Enter line number of the line to be deleted:");

              scanf("%d", &delete_line);

                         fileptr2 = fopen("replica.c", "w");

                         ch = getc(fileptr1);

              while (ch != EOF)

{

                          ch = getc(fileptr1);

               if (ch == '\n')

                          temp++;

               if (temp != delete_line)

{

               putc(ch, fileptr2);

}

}

                            fclose(fileptr1);

                            fclose(fileptr2);

                            remove(filename);

                            rename("replica.c", filename);

printf("\n The contents of file after being modified are as follows:\n");

                            fileptr1 = fopen(filename, "r");

                            ch = getc(fileptr1);

               while (ch != EOF)

{

               printf("%c", ch);

                            ch = getc(fileptr1);

}

                            fclose(fileptr1);

return 0;

getch();

}

# 
127\. Write a program to implement stooge sort.

#include<stdio.h>

#include<conio.h>

void stoogesort(int [], int, int);

int main()

{

int b[7], i;

printf("Enter the values you want to sort using STOOGE SORT!!!:\n");

            for (i = 0;i < 7;i++)

scanf(" %d", &b[i]);

stoogesort(b, 0, 6);

printf("sorted by stooge sort \n");

            for (i = 0;i < 7;i++)

{

printf("%d ", b[i]);

}

printf("\n");

getch();

return 0;

}

void stoogesort(int a[], int i, int j)

{

int temp, k;

               if (a[i] > a[j])

{

                   temp = a[i];

                   a[i] = a[j];

                   a[j] = temp;

}

                if ((i + 1) >= j)

return;

                     k = (int)((j - i + 1) / 3);

                     stoogesort(a, i, j - k);

                     stoogesort(a, i + k, j);

                     stoogesort(a, i, j - k);

}

Sample output:

Enter the values you want to sort using STOOGE SORT!!!:

23

43

12

45

97

56

34

sorted by stooge sort

12 23 34 43 45 56 97

# 
128\. Write a program to get LCM of two numbers using recursion.

#include<stdio.h>

#include<conio.h>

int lcm(int,int);

int main()

{

int a,b,l;

printf("Enter any two positive integers ");

scanf("%d%d",&a,&b);

            if(a>b)

                l = lcm(a,b);

            else

                l = lcm(b,a);

printf("LCM of two integers is %d",l);

getch();

return 0;

}

int lcm(int a,int b)

{

static int temp = 1;

            if(temp % b == 0 && temp % a == 0)

return temp;

                temp++;

                lcm(a,b);

return temp;

}

Sample output:

Enter any two positive integers 2

5

LCM of two integers is 10

# 
129\. Write a program to find GCD of numbers using recursion.

#include<stdio.h>

#include<conio.h>

int gcd(int, int);

int main()

{

int a, b, result;

printf("Enter the two numbers to find their GCD: ");

scanf("%d%d", &a, &b);

result = gcd(a, b);

printf("The GCD of %d and %d is %d.\n", a, b, result);

getch();

}

int gcd(int a, int b)

{

            while (a != b)

{

             if (a > b)

{

return gcd(a - b, b);

}

             else

{

return gcd(a, b - a);

}

}

return a;

}

Sample output:

Enter the two numbers to find their GCD: 100

70

The GCD of 100 and 70 is 10.

# 
130\. Write a program to get power of a number using recursion.

#include<stdio.h>

#include<conio.h>

int main()

{

int pow,num;

long int res;

long int power(int,int);

printf("\nEnter a number: ");

scanf("%d",&num);

printf("\nEnter power: ");

scanf("%d",&pow);

res=power(num,pow);

printf("\n%d to the power %d is: %ld",num,pow,res);

getch();

return 0;

}

int i=1;

long int sum=1;

long int power(int num,int pow)

{

            if(i<=pow)

{

                sum=sum*num;

                power(num,pow-1);

}

            else

return sum;

}

Sample output:

Enter a number: 24

Enter power: 2

24 to the power 2 is: 576

# 
131\. Write a program to find factorial of number using recursion.

#include<stdio.h>

#include<conio.h>

int fact(int);

int main()

{

int num,f;

printf("\nEnter a number: ");

scanf("%d",&num);

f=fact(num);

printf("\nFactorial of %d is: %d",num,f);

getch();

return 0;

}

int fact(int n)

{

              if(n==1)

return 1;

              else

return(n*fact(n-1));

}

Sample output:

Enter a number: 6

Factorial of 6 is: 720

# 
132\. Write a program to print Fibonacci series using recursion.

#include<stdio.h>

#include<conio.h>

void printFibonacci(int);

int main()

{

int k,n;

long int i=0,j=1,f;

printf("Enter the range of the Fibonacci series: ");

scanf("%d",&n);

printf("Fibonacci Series: ");

printf("%d %d ",0,1);

printFibonacci(n);

getch();

return 0;

}

void printFibonacci(int n)

{

static long int first=0,second=1,sum;

            if(n>0)

{

                sum = first + second;

                first = second;

                second = sum;

printf("%ld ",sum);

printFibonacci(n-1);

}

}

Sample output:

Enter the range of the Fibonacci series: 20

Fibonacci Series: 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765 10946

# 
133\. Write a program to convert decimal number to binary number using recursion.

#include<stdio.h>

#include<conio.h>

long toBinary(int);

int main()

{

long binaryNo;

int decimalNo;

printf("Enter any decimal number: ");

scanf("%d",&decimalNo);

binaryNo = toBinary(decimalNo);

printf("Binary value is: %ld",binaryNo);

getch();

return 0;

}

long toBinary(int decimalNo)

{

static long binaryNo,remainder,factor = 1;

            if(decimalNo != 0)

{

                 remainder = decimalNo % 2;

                 binaryNo = binaryNo + remainder * factor;

                 factor = factor * 10;

                 toBinary(decimalNo / 2);

}

return binaryNo;

}

Sample output:

Enter any decimal number: 221

Binary value is: 11011101

# 
134\. Write a program to find the largest number in array using recursion.

#include<stdio.h>

#include<conio.h>

#define MAX 100

int getMaxElement(int []);

int size;

int main()

{

int arr[MAX],max,i;

printf("Enter the size of the array: ");

scanf("%d",&size);

printf("Enter %d elements of an array: ", size);

            for(i=0;i<size;i++)

scanf("%d",&arr[i]);

max=getMaxElement(arr);

printf("Largest element of an array is: %d",max);

getch();

return 0;

}

int getMaxElement(int arr[])

{

static int i=0,max =-9999;

             if(i < size)

{

             if(max<arr[i])

                  max=arr[i];

                  i++;

getMaxElement(arr);

}

return max;

}

Sample output:

Enter the size of the array: 5

Enter 5 elements of an array: 5

8

3

9

4

Largest element of an array is: 9

# 
135\. Write a program to find reverse of number using recursion.

#include<stdio.h>

#include<math.h>

#include<conio.h>

int rev(int, int);

int main()

{

int num, result;

int length = 0, temp;

printf("Enter an integer number to reverse: ");

scanf("%d", &num);

temp = num;

           while (temp != 0)

{

                   length++;

                   temp = temp / 10;

}

                   result = rev(num, length);

printf("The reverse of %d is %d.\n", num, result);

return 0;

getch();

}

int rev(int num, int len)

{

if (len == 1)

{

return num;

}

else

{

return (((num % 10) * pow(10, len - 1)) + rev(num / 10, --len));

}

}

Sample Output:

Enter an integer number to reverse: 123456

The reverse of 123456 is 654321.

# 
136\. Write a program to display ATM transaction.

#include<stdio.h>

#include<conio.h>

unsigned long amount=1000, deposit, withdraw;

int choice, pin, k;

char transaction ='y';

int main()

{

              while (pin != 1520)

{

printf("ENTER YOUR SECRET PIN NUMBER: ");

scanf("%d", &pin);

              if (pin != 1520)

printf("PLEASE ENTER VALID PASSWORD\n");

}

              do

{

printf("********Welcome to ATM Service**************\n");

                            printf("1\. Check Balance\n");

                            printf("2. Withdraw Cash\n");

                            printf("3\. Deposit Cash\n");

                            printf("4. Quit\n");

printf("******************?**************************?*\n\n");

                            printf("Enter your choice: ");

                            scanf("%d", &choice);

switch (choice)

{

case 1:

              printf("\n YOUR BALANCE IN Rs : %lu ", amount);

break;

case 2:

              printf("\n ENTER THE AMOUNT TO WITHDRAW: ");

              scanf("%lu", &withdraw);

              if (withdraw % 100 != 0)

              {

              printf("\n PLEASE ENTER THE AMOUNT IN MULTIPLES OF 100");

              }

              else if (withdraw >(amount - 500))

              {

              printf("\n INSUFFICENT BALANCE");

              }

              else

              {

                            amount = amount - withdraw;

              printf("\n\n PLEASE COLLECT CASH");

              printf("\n YOUR CURRENT BALANCE IS%lu", amount);

              }

break;

case 3:

              printf("\n ENTER THE AMOUNT TO DEPOSIT");

              scanf("%lu", &deposit);

                        amount = amount + deposit;

              printf("YOUR BALANCE IS %lu", amount);

break;

case 4:

              printf("\n THANK U USING ATM");

break;

default:

              printf("\n INVALID CHOICE");

              }

              printf("\n\n\n DO U WISH TO HAVE ANOTHER TRANSCATION?(y/n): \n");

              fflush(stdin);

              scanf("%c", &transaction);

              if (transaction == 'n'|| transaction == 'N')

                    k = 1;

              }

              while (!k);

              printf("\n\n THANKS FOR USING OUT ATM SERVICE");

              getch();

}

Sample Output:

ENTER YOUR SECRET PIN NUMBER: 2345

PLEASE ENTER VALID PASSWORD

ENTER YOUR SECRET PIN NUMBER: 1520

********Welcome to ATM Service**************

1\. Check Balance

2\. Withdraw Cash

3\. Deposit Cash

4\. Quit

******************?**************************?*

Enter your choice: 2

  ENTER THE AMOUNT TO WITHDRAW: 2000

  INSUFFICENT BALANCE

  DO U WISH TO HAVE ANOTHER TRANSCATION?(y/n):

y

********Welcome to ATM Service**************

1\. Check Balance

2\. Withdraw Cash

3\. Deposit Cash

4\. Quit

******************?**************************?*

Enter your choice: 2

  ENTER THE AMOUNT TO WITHDRAW: 200

  PLEASE COLLECT CASH

  YOUR CURRENT BALANCE IS 800

  DO U WISH TO HAVE ANOTHER TRANSCATION?(y/n):

n

THANKS FOR USING OUT ATM SERVICE

Note-

All programs have been successfully run and checked on Dev C++ 5.9.2

# 
Quick MCQ:

1\. Which is valid C expression ?

a) int my_num = 100,000;

b) int my_num = 100000;
c) int my num = 1000;

d) int $my_num = 10000;

2\. What is the size of an int data type ?

a) 4 Bytes

b) 8 Bytes
c) Depends on the system/compiler

d) Cannot be determined

3\. Which is correct with respect to size of the datatypes ?

a) char > int > float

b) int > char > float
c) char < int < double

d) double > char > int

4\. Which of the following declaration is not supported by C ?

a) String str;

b) char *str;
c) float str = 3e2;

d) Both (a) and (c)

5\. Which of the following is not a pointer declaration ?

a) char a[10];             

b) char a[] = {‘1’, ‘2’, ‘3’, ‘4’};
c) char *str;

d) char a;

6\. Is there any difference between following declarations ?

1: extern int fun();

2: int fun();

a) Both are identical

b) No difference, except extern int fun(); is probably in another file

c) int fun(); is overrided with extern int fun();

d) None of these

7\. Which statement will you add in the following program to work it correctly ?

#include<stdio.h>

int main()

{

    printf("%f\n", log(36.0));

    return 0;

}

a) #include<conio.h>

b) #include<math.h>

c) #include<stdlib.h>

d) #include<dos.h>

8\. By default a real number is treated as a

a) Float

b) double

c) long double

d) far double

9\. What will happen if in a C program you assign a value to an array element whose subscript exceeds the size of array?

a) The element will be set to 0.

b) The compiler would report an error.

c) The program may crash if some important data gets overwritten.

d) The array size would appropriately grow.

10\. In C, if you pass an array as an argument to a function, what actually gets passed ?

a) Value of elements in array

b) First element of the array

c) Base address of the array

d) Address of the last element of array

11\. Which of the following are unary operators in C ?

1.  !

2.  sizeof

3.  ~

4.  &&

a) 1, 2

b) 1, 3

c) 2, 4

d) 1, 2, 3

12\. The keyword used to transfer control from a function back to the calling function is

a) Switch

b) goto

c) go back

d) return

13\. What is (void*)0 ?

a) Representation of NULL pointer

b) Representation of void pointer

c) Error

d) None of above

14\. What is the output of this C code ?

#include <stdio.h>

    int main()

    {

        int a = 1, b = 1, c;

        c = a++ + b;

        printf("%d, %d", a, b);

    }

a) a = 1, b = 1

b) a = 2, b = 1
c) a = 1, b = 2

d) a = 2, b = 2

15\. What is the output of this C code ?

#include <stdio.h>

    int main()

    {

        int a = 5, b = -7, c = 0, d;

        d = ++a && ++b || ++c;

        printf("\n%d %d %d %d", a,  b,  c,  d);

    }

a) 6 -6 0 0

b) 6 -5 0 1
c) -6 -6 0 1

d) 6 -6 0 1

16\. Which of the following cannot be checked in a switch-case statement ?

a) Character

b) Integer

c) Float

d) Enum

17\. Which of the following is the correct usage of conditional operators used in C ?

a) a>b ? c=30 : c=40;

b) a>b ? c=30;

c) max = a>b ? a>c?a:c:b>c?b:c

d) return (a>b)?(a:b)

18\. What will be the output of the program ?

#include<stdio.h>

int main()

{

    float a=0.7;

    if(a < 0.7)

        printf("C\n");

    else

        printf("C++\n");

    return 0;

}

a) C

b) C++

c) Compiler error

d) Non of above

19\. If the two strings are identical, then strcmp() function returns

a) -1

b) 1

c) 0

d) Yes

20\. The library function used to find the last occurrence of a character in a string is

a) strnstr()

b) laststr()

c) strrchr()

d) strstr()

21\. Which of the following function is more appropriate for reading in a multi-word string ?

a) printf();

b) scanf();

c) gets();

d) puts();

22\. To print out a and b given below, which of the following printf() statement will you use ?

#include<stdio.h>

float a=3.14;

double b=3.14;

a) printf("%f %lf", a, b);

b) printf("%Lf %f", a, b);

c) printf("%Lf %Lf", a, b);             

d) printf("%f %Lf", a, b);

23\. Which of the following are themselves a collection of different data types ?

a) string

b) structures

c) char

d) All of the mentioned

24\. Which of the following is not user defined data type ?

1 :              struct book

{

    char name[10];

    float price;

    int pages;

};

2 :              long int l = 2.35;

3 :              enum day {Sun, Mon, Tue, Wed};

a) 1

b) 2

c) 3

d) Both 1 and 2

25\. What is the similarity between a structure, union and enumeration ?

a) All of them let you define new values

b) All of them let you define new data types

c) All of them let you define new pointers

d) All of them let you define new structures

26\. If a variable is a pointer to a structure, then which of the following operator is used to access data members of the structure through the pointer variable ?

a) .

b) &

c) *

d) ->

27\. A pointer is

a) A keyword used to create variables

b) A variable that stores address of an instruction

c) A variable that stores address of other variable

d) All of the above

28\. What does the following declaration mean ?

int (*ptr)[10];

a) ptr is array of pointers to 10 integers

b) ptr is a pointer to an array of 10 integers

c) ptr is an array of 10 integers

d) ptr is an pointer to array

29\. In the following code, the P2 is Integer Pointer or Integer

?

typedef int *ptr;

ptr p1, p2;

a) Integer

b) Integer pointer

c) Error in declaration

d) None of above

30\. If there is any error while opening a file, fopen will return

a) Nothing

b) EOF

c) NULL

d) Depends on compiler

# 
Answers-

1) b   2) c   3) c   4) a   5) d   6) b   7) b   8) b   9) c   10) c   11) d   12) d   13) a   14) b   15) d   16) c   17) c   18) a   19) c   20) c   21) c 22) a   23) b   24) b                 25) b   26) d   27) c   28) b   29) b   30) c

# 
Interview Q & A:

Q.1 Can a program be compiled without main() function ?

Yes, it can be but cannot be executed, as the execution requires main() function definition.

Q.2 What is the difference between variable declaration and variable definition ?

Declaration associates type to the variable whereas definition gives the value to the variable.

Q.3 What is the default value of local and global variables ?

Local variables get garbage value and global variables get a value 0 by default.

Q.4 is it possible to create your own header files ?

Yes, it is possible to create a customized header file. Just include in it the function prototypes that you want to use in your program, and use the #include directive followed by the name of your header file.

Q.5 What is the use of a semicolon (;) at the end of every program statement ?

It has to do with the parsing process and compilation of the code. A semicolon acts as a delimiter, so that the compiler knows where each statement ends, and can proceed to divide the statement into smaller elements for syntax checking.

Q.6 Can I use  “int” data type to store the value 32768? Why ?

No. “int” data type is capable of storing values from -32768 to 32767\. To store 32768, you can use “long int” instead. You can also use “unsigned int”, assuming you don’t intend to store negative values.

Q.7 In C language, the variables NAME, name, and Name are all the same. TRUE or FALSE ?

FALSE. C language is a case sensitive language. Therefore, NAME, name and Name are three uniquely different variables.

Q.8 What is wrong with this statement? myName = “Robin”;

You cannot use the = sign to assign values to a string variable. Instead, use the strcpy function. The correct statement would be: strcpy(myName, “Robin”);

Q.9 What are actual arguments?

When you create and use functions that need to perform an action on some given values, you need to pass these given values to that function. The values that are being passed into the called function are referred to as actual arguments.

Q.10 Can the “if” function be used in comparing strings ?

No. “if” command can only be used to compare numerical values and single character values. For comparing string values, there is another function called strcmp that deals specifically with strings.

Q.11 What is the difference between the expression “++a”  and “a++” ?

In the first expression, the increment would happen first on variable a, and the resulting value will be the one to be used. This is also known as a prefix increment. In the second expression, the current value of variable a would the one to be used in an operation, before the value of a itself is incremented. This is also known as postfix increment.

Q. 12 How a negative integer is stored ?

Get the two's compliment of the same positive integer. Eg: 1101 (-5)

Step-1 ? One's compliment of 5 : 1010

Step-2 ? Add 1 to above, giving 1011, which is -5.

Q.13 How many operators are there under the category of ternary operators ?

There is only one operator and is conditional operator (? : ).

Q.14 Does a break is required by default case in switch statement ?

Yes, if it is not appearing as the last case and if we do not want the control to flow to the following case after default if any.

Q.15 Which key word is used to perform unconditional branching ?

goto

Q.16 Which function can be used to release the dynamic allocated memory ?

free()

Q.17 What is a pointer on pointer ?

It's a pointer variable which can hold the address of another pointer variable. It de-refers twice to point to the data held by the designated pointer variable.

Eg: int x = 5, *p=&x, **q=&p;

Q.18 What is the advantage of declaring void pointers ?

When we do not know what type of the memory address the pointer variable is going to hold, then we declare a void pointer for such.

Q.19 When to user -> (arrow) operator ?

If the structure/union variable is a pointer variable, to access structure/union elements the arrow operator is used.

Q.20 What is a nested structure ?

A structure containing an element of another structure as its member is referred so.

Thanks for reading my book. I hope you must have learned lots of programming knowledge from this book.

Quick Favor Please!!!!

Take a minute to leave a review on Amazon letting me know if you have learned from this book.

Thank You!!!!
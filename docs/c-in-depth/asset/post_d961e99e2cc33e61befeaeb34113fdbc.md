
![](img/a76c706396af8b310f291a5313a27079_153_0.png)

## 6.19.2 Advantages And Disadvantages Of Recursion

The use of recursion makes the code more compact and elegant. It simplifies the logic and hence makes the program easier to understand. But the code written using recursion is less efficient since recursion is a slow process because of many function calls involved in it.

Most problems with recursive solutions also have an equivalent non-recursive (generally iterative) solutions. A non recursive solution increases performance while a recursive solution is simpler.

## 6.19.3 Local Variables In Recursion

We know each function has some local variables that exist only inside that function. When a function is called recursively, then for each call a new set of local variables is created (except static), their name is same but they are stored at different places and contain different values. These values are remembered by the compiler till the end of function call, so that these values are available in the unwinding phase.

## 6.20 Some Additional Problems

### Problem 1

Write a program to convert a binary or octal number to a decimal number depending on user's choice.

```
/*P6.28 Program to convert a binary or octal number to a decimal number*/
#include<stdio.h>
main()
{
    int num,base,result;
    char choice;
    printf("Enter 'b' for binary and 'o' for octal : ");
    scanf("%c",&choice);
    printf("Enter the number : ");
    scanf("%d",&num);
    if(choice=='b')
        base=2;
    else
        base=8;
    result=func(num,base);
    printf("Decimal number is %d\n",result);
}
func(int n,int base)
{
    int rem,d,j=1,dec=0;
    while(n>0)
    {
        rem=n%10; /* taking last digit */
        d=rem*j;
        dec+=d;
        j*=base;
        n/=10;   /* skipping last digit */
    }
    return dec;
}
```

### Problem 2

Write a program to implement these formulae of permutations and combinations.

The formula for number of permutations of n objects taken r at a time-
p(n, r) = n! / (n-r)!
The formula for number of combinations of n objects taken r at a time is-
c(n, r) = n! / r! * (n-r)!
This can also be written as-
c(n, r) = p(n, r) / r!

```
/*P6.29 Program to find out permutations and combinations*/
#include<stdio.h>
long factorial(int);
long perm(int,int);
long comb(int,int);
main()
{
    int n,r;
    printf("Enter n : ");
    scanf("%d",&n);
    printf("Enter r : ");
    scanf("%d",&r);
    printf("Total combinations are : %ld\n",comb(n,r));
    printf("Total permutations are : %ld\n",perm(n,r));
}
long comb(int n,int r)
{
    long c;
    c=perm(n,r)/factorial(r);
    return c;
}
long perm(int n,int r)
{
    long p;
    p=factorial(n)/factorial(n-r);
    return p;
}
long factorial(int k)
{
    long fact=1;
    while( k>0 )
    {
        fact*=k;
        k--;
    }
    return fact;
}
```

### Problem 3

Write a program to print Pascal's triangle.

```
1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1
1 6 15 20 15 6 1
```

```
/*P6.30 Program to print Pascal's triangle*/
#include<stdio.h>
long factorial(int);
long comb(int,int);
main()
{
	int i,j,k;
	printf("Enter number of rows for Pascal's triangle : ");
	scanf("%d",&k);
	for(i=0;i<k;i++)
	{
		for(j=0;j<=i;j++)
			printf("%5ld",comb(i,j));
		printf("\n");
	}
}
long comb(int n,int r)
{
	long c;
	c=factorial(n)/(factorial(r)*factorial(n-r)) ;
	return c;
}
long factorial(int k)
{
	long fact=1;
	while(k>0)
	{
		fact*=k;
		k--;
	}
	return fact;
}
```

### Problem 4

Write a program to convert a decimal number to a roman number. The roman numbers corresponding to decimal numbers are as-

| 1 - i | 9 - ix | 100 - c |
|-------|--------|---------|
| 4 - iv | 10 - x | 500 - d |
| 5 - v | 50 - l | 1000 - m |

Some examples are:

- 14 xiv
- 48 xxxxviii
- 123 cxxiii
- 772 dcclxii
- 1009 mix
- 2856 mmdccclvi

```
/*#include<stdio.h>
int roman(int,int,char);
main()
{
int num;
printf("Enter a number : ");
scanf("%d",&num);
if(num>=1000)
num=roman(num,1000,'m');
if(num>=500)
    num=roman(num,500,'d');
if(num>=100)
    num=roman(num,100,'c');
if(num>=50)
    num=roman(num,50,'l');
if(num>=10)
    num=roman(num,10,'x');
if(num>=5)
    num=roman(num,5,'v');
if(num>=1)
    roman(num,1,'i');
printf("\n");
}
int roman(int n,int k,char c)
{
    if(n==9)
    {
        printf("ix");
        return 0;
    }
    if(n==4)
    {
        printf("iv");
        return 0;
    }
    while(n>=k)
    {
        printf("%c",c);
        n=n-k;
    }
    return n;
}
```

### Problem 5

Write a program that prints the reverse of a positive integer using recursion.

```
/*P6.32 Program to print the reverse of a positive integer*/
#include<stdio.h>
void reverse(long int n);
main()
{
    long int num;
    printf("Enter number : ");
    scanf("%ld",&num);
    reverse(num);
    printf("\n");
}
void reverse(long int n)
{
    int rem;
    if(n==0)
    return;
    else
    {
        rem=n%10;
        printf("%d",rem);
        n/=10;
        reverse(n);
    }
}
```

### Problem 6

Write a program that reads a number and prints whether the given number is divisible by 11 or not by using the algorithm which states that a number is divisible by 11 if and only if the difference of the sums of digits at odd positions and even positions is either zero or divisible by 11.

```
/* P6.33 Program that tests whether a number is divisible by 11 or not */
#include<stdio.h>
void test(long int x);
main()
{
    long int num;
    printf("Enter the number to be tested : ");
    scanf("%ld",&num);
    test(num);
}
void test(long int n)
{
    int s1=0,s2=0,k;
    while(n>0)
    {
        s1+=n%10;
        n/=10;
        s2+=n%10;
        n/=10;
    }
    k=s1>s2?(s1-s2):(s2-s1);
    if(k>10)
        test(k);
    else if(k==0)
        printf("The number is divisible by 11\n");
    else
        printf("The number is not divisible by 11\n");
}
```

### Problem 7

Write a program that uses a recursive function to convert a decimal number to (i) Binary (ii) Octal (iii) Hexadecimal depending on user's choice.

## Functions

Program to convert a decimal number to Binary, Octal or Hexadecimal

```
/* P6.34 Program to convert a decimal number to Binary, Octal or Hexadecimal */
#include<stdio.h>
void convert(int, int);
main()
{
int num,base;
int choice;
while(1)
{
printf("\n1.Binary\n");
printf("\n2.Octal\n");
printf("\n3.Hexadecimal\n");
printf("\n4.Exit\n");
printf("Enter your choice : ");
scanf("%d",&choice);
switch(choice)
{
case 1:
base=2;
break;
case 2:
base=8;
break;
case 3:
base=16;
break;
case 4:
exit(1);
default:
printf("Wrong choice\n");
continue; /*Takes to start of while loop*/
}
printf("Enter the number in decimal: ");
scanf("%d",&num);
convert(num,base);
printf("\n");
}
}
void convert(int num,int base)
{
int rem;
rem=num%base;
num/=base;
if (num>0)
convert(num,base);
if(rem<10)
printf("%d", rem);
else
printf("%c",rem-10+'A');
}
```

### Problem 8

Write a program to find out the prime factors of a number using both iterative and recursive methods. Prime factors of 56 are 2, 2, 7, prime factors of 98 are 2, 7, prime factors of 121 are 11, 11.

```
/*P6.35 Program to print the prime factors*/
#include <stdio.h>
void pfact(int num);
void rpact(int n);
main()
{
int num;
printf("Enter a number : ");
scanf("%d",&num);
pfact(num);printf("\n");
rpact(num);printf("\n");
}
void pfact(int num)
{
int i;
for(i=2;num!=1;i++)
{
while(num%i==0)
{
printf("%d ",i);
num=num/i;
}
}
}
void rpact(int num)
{
static int i=2;
if(num==1)
return;
else
{
while(num%i==0)
{
printf("%d ",i);
num=num/i;
}
}
i++;
rpact(num);
}
```

### Problem 9

Write a program to find out the sum of this series, both by iterative and recursive methods.

```
/*P6.36 Program to find out the sum of series*/
#include<stdio.h>
long int fact(int num);
double power(float x,int n);
double series(float x,int n);
double rseries(float x,int n);
main()
{
    float x;
    int n;
    printf("Enter x : ");
    scanf("%f",&x);
    printf("Enter number of terms : ");
    scanf("%d",&n);
    printf("Iterative    %f\n",series(x,n));
    printf("Recursive    %f\n",rseries(x,n));
}
long int fact(int num)
{
    int i;
    long int f=1;
    for(i=1;i<=num;i++)
        f=f*i;
    return f;
}
double power(float x,int n)
{
    int i;
    float p=1;
    for(i=1;i<=n;i++)
        p=p*x;
    return p;
}
double series(float x,int n)
{
    int i,j,sign=1;
    float term,sum;
    for(i=1;i<=n;i++)
    {
        sign=(i&2==0)?-1:1;
        j=2*i-1;
        term=sign*power(x,j)/fact(j);
        sum+=term;
    }
    return sum;
}
double rseries(float x,int n)
{
    int sign=1;
    float term,sum;
    if(n==0)
```

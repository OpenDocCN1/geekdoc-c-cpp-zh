
## Consider the following e.g.

```
1. int x=2,y;
 y = x > 5 ? 3 : 5;
```

Output: 5

since the value of x is less than 5 so the condition is false hence the part of statement after semicolon ( : ) will be executed.

```
2. int a=5,b=4,c;
 a>b? g = a: g = b;
```

Output:- This will give an error ‘LValue required’. The error can be overcome by enclosing the statement in the : part within a pair of parentheses. a>b? g = a: (g = b); In absence of parentheses the compiler believes that b is being assigned to the result of the expression to the left of second = . Hence it reports an error.

The limitation of the conditional operators is that only one statement is allowed after ? : .

```
3. Are the two statements same:
 a<=20?b=30;c=30;
 a<=20?b:c=30;
```

Output:- No

```
4. int a=10,b;
 a>=5?b=100:b=200;
 printf("%d",b);
```

Output- Lvalue error occurs.

The second assignment should be written in parentheses as follows: a>=5?b=100:(b=200);

```
5. Rewrite the following set of statements using conditional operators:
int a=1,b;
if(a>10)
b=20;
```

Output:- int a=1,b,dummy;
a>10?b=20:(dummy=1);

Note that the following will not work: a>10?b=20;;

```
6. Can you suggest some other way to write the following expression such that 30 is used only once?
a<=20?b=30;c=30;
```

Output:- ((a<=20)?b:&c)=30;

## 8. Bitwise operators –

Some programs require working on the bits(0 and 1) such as programs interacting with the hardware parts of the computer. Thus C contains several special operators which allow working on the bits.

*The bitwise operators are generally categorized into three types:*

- 1. **The one’s complement operator(~)**
- 2. **The logical bitwise operator.(&, |, ^)**
- 3. **The shift operators.(<<, >>)**
- In all there are 6 bitwise operators.

## One’s complement operator:

Also referred as the complementation operator. It is a unary operator that inverts the bits of the operand, i.e. all 0s become 1 and all 1s become 0s. The operand for the operator must always be an integer value(int, short int, long int, unsigned, char).

```
```c
unsigned int a= 5, b;
b = ~a;
printf("%u",b);
```
```

**Output:-** will be 65530.

Let us evaluate the output now: the binary equivalent of the number 5 will be

0000 0000 0000 0101.

As already said one’s complement converts all the 1s to 0s and all 0s to 1s.so the complement will be 1111 1111 1111 1010 and converting the number to a decimal number will give—

1*2¹⁵+1*2¹⁴+1*2¹³+1*2¹²+1*2¹¹+1*2¹⁰+1*2⁹+1*2⁸+1*2⁷+1*2⁶+1*2⁵+1*2⁴+1*2³-

32768+16384+8192+4096+2048+1024+512+256+128+64+32+16+8+0+2+0
and the final answer will be 65530.

## 9. The logical bitwise operators:

There are three logical bitwise operators bitwise AND(&), bitwise OR (|) ,bitwise XOR (^). Each of these operators requires two integer values to work.

Each of the operands are individually converted into their respective binary numbers.The left most bit of the binary number is called the most significant bit or MSB. While the right most bit is called the least significant bit.

| Operand 1 | Operand 2 | & | \| | ^ |
|----------|----------|---|----|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

The above table explains the working of all the logical bit wise operators.

## The shift operators:

The two bit wise shift operators are left shift (<<) and the right shift (>>). Each of these operators also requires two operands. The first integer operand that represents the bit pattern to be shifted. The second operand indicates the number of bits to be shifted.

```
int a,b;
a=20<<2;
b=20>>2;
printf("%d %d",a,b);
Output: 80, 5
```

The program will convert 20 to its binary equivalent i.e. 0000 0000 0001 0100 shifting 2 bits to the left would result the bits to be 0000 0000 0101 0000 and the integer number will be 80. if the bits of the integer number 20 are shifted 2 bits to the right side the binary number will be 0000 0000 0000 0101.

Thus shifting the number to right by 1 reduces the number to half, while shifting the number to left by 1 bit doubles the number.

Comma operator works from left to right but returns the right most value. This operator is generally used in the for loop. The expressions separated by comma operator are solved from left to right. On using the comma operator the value and the type of right most operand is returned. For e.g. in the assignment statement below:

```
i = (j = 1, k = 2, 3, 4);
```

The expressions j = 1, k = 2, 3, 4 are evaluated first. Then the value of the expression is returned as 4 and assigned to i.

| 1. int a; a = 5,6; printf("%d",a); Output:- 5 | 2. int a; a = (5,6); printf("%d",a); Output:- 6 |

## Some Solved Programs:

1. If a four digit number is input through the keyboard, write a program to obtain the sum of the first and last digit of the number.

```
int n,a,b,sum;
printf("Enter a four digit number: ");
scanf("%d",&n);
a=n%10;
b=n/1000;
sum = a + b;
printf("Sum of the first and last digit is %d", sum);
getch();
```

2. Print the range of a number. E.g. number 78 is between 70 and 79, 102 is between 100 and 109.

```
int n,lower_r,upper_r;
printf("Enter a number: ");
scanf("%d",&n);
lower_r = n %10 * 10;    /*the arithmetic operators work from left to right*/
upper_r = lower_r + 10;
printf("Range is %d - %d",lower_r,upper_r);
getch();
```

## 3. Print the various denominations of a given rupee. E.g. if a person has 1779 in his pocket the program should print the following.

500 x 3 = 1500, 100 x 2 = 200, 50 x 1 = 50, 20 x 1 = 20, 10 x 0 = 0, 5 x 1 = 5, 2 x 2 = 4, 1 x 0 = 0

```
int Rs,a,b,c,d,e,f,g,h;
clrscr();
printf("Enter the amount: ");
scanf("%d",&Rs);
a= Rs/500;
Rs = Rs%500;
b = Rs/100;
Rs=Rs%100;
c=Rs/50;
Rs=Rs%50;
d=Rs/20;
Rs=Rs%20;
e=Rs/10;
Rs=Rs%10;
f=Rs/5;
Rs=Rs%5;
g=Rs/2;
Rs=Rs%2;
h=Rs/1;
printf("The various denominations of the given rupees are\n500 X %2d\n100 X %2d\n 50 X %2d\n 20 X %2d\n 10 X %2d\n 5 X %2d\n\n 2 X %2d\n 1 X %2d",a,b,c,d,e,f,g,h);
getch();
```

![](img/3a2b6e5e90a58a56458b0539952c0cd2_55_0.png)

Ohhh Yes! Demm Man ....
We don't know that
We are new Fuc*in Programmers! LoL

## Multiple choice questions:

1. A whole number with a decimal point is known as:
a. floating point number.
b. character.
c. integer.
d. none.

2. The declaration unsigned u indicates:
a. u is a character
b. u is an unsigned integer
c. u is unsigned character
d. u is unsigned long integer

3. Which statement must not end with semicolon:
a. #define
b. variable declaration
c. assignment
d. none

4. Point out the valid variable names:
a. gross salary
b. gross-salary
c. AVG
d. AVG.

5. If a is an integer variable, a =5/2 will return a value.
a. 2.5
b. 3
c. 2
d. 0

6. The expression, a=7/22*(3.14+2)*3/5 is evaluated to
a. 8.28
b. 6.28
c. 3.14
d. 0

7. The expression a=30*1000+2768 evaluates to
a. 32768
b. -32768
c. 113040
d. 0

8. The expression a=4+2%-8 evaluates to
a. -6
b. 6
c. 4
d. none of the above

9. Hierarchy decides which operator
a. is most important
b. is used first
c. is fastest
d. operates on largest numbers

10. In C a variable can not contain
a. blank spaces
b. hyphen ( - )
c. decimal point
d. all the above

11. Arithmetic instructions can not Contain--
a. variables.
b. constant.
c. variable names on right of equal.
d. variable names on left of equal.

12. Which of the following is odd one out
a. +
b. -
c. /
d. **

13. What will be the value of d assuming it to be float after the operation d=2/7.0
a. 0
b. 0.2857
c. can not be determined.
d. none of the above.

Answers-
1(a) 2(b) 3(a) 4(c)
5(c) 6(d) 7 (b) 8(b)
9(b) 10(d) 11(c) 12(d) 13(b)

## Theory Questions –

- 1. Explain what are data types? Name all the data types in c language with their size in bytes (in dos operating system). List all the format specifiers. Also write the formula by which we can calculate the range of a given data type.
- 2. Calculate the range of int by this.
- 3. How many keywords are present in C. Give the name of all the keywords?
- 4. Explain all the naming rules of a variable in c.
- 5. Characteristics of a program.
- 6. Name all the escape sequences.
- 7. What do you mean by precedence of operators? List all the available operators in c in the order of their precedence. (higher to lower)
- 8. What do you mean by typecasting? Explain implicit and explicit typecasting

## Give the output of the following -

```
1. int i =4, z=12;
   if( i = 5||z>50)
   printf("\nwelcome in matrix");
   else
   printf("\n you may go now");
```

Output: welcome in matrix
First in if i is assigned with 5 that is non zero value and assume as true now this value involve with (||) OR op. and in the case of OR operator if first condition is true it is not go for the next one and jumps out with true value this is known as "short circuit ".

```
2. int i=4,z=12;
   if(i=5&&z>5)
      printf("hello");
   else
      printf("bye");
```

13. What should we do to treat the constant 3.14 as a long double?

Output: Use 3.14l

14. What will be the output of the following statement:
    printf("%% %d
%%d",sizeof(3.14f),
    sizeof(3.14), sizeof(3.14l));
    a. 4 4 4
    b. 4 garbage value
garbage value
    c. 4 8 10
    d. Error
Output: c

15. How floats are stored in binary form?
Output: Floating point numbers

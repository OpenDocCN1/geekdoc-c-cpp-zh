
## De Morgan’s laws

Augustus De Morgan (1806-1871), mathematician friend of Boole, showed that (a) NOT (sORp) is equivalent to NOTs AND NOTp and (b) NOT (sANDp) is equivalent to NOTs OR NOTp. In programming languages, including C, truth-values, TRUE and FALSE, are understood as 1 and 0, respectively. So we can do the first law test this example:

```
main() {if(!((1||0)==(!1&&!0)) puts("\n It's right!");}
```

With the next, we can make the verification of the second law:

```
main() {if(!((1&&0)==(!1||!0)) puts(" This works!");}
```

## Axioms of Aristotle

Formal Logic was invented by Aristotle from three basic axioms, which he called:

- A) Contradiction principle (N(Ns) is equivalent to s);
- B) Excluded middle principle (s is valid or Ns);
- C) Principle of identity (s is equivalent to s).

In the above lines, s is any sentence and N means “not”, “denial” or “to deny” (principles A and C were already used by other philosophers, then Aristotle has brought the principle B). When John Von Neumann directed the construction of the ENIAC computer in 1945, he introduced the so-called “Von Neumann architecture”, assembly of the processor that operates on the axioms of Aristotle. You can check if the current processor maintains that architecture, writing to the first principle:

```
main() {if(!(!!(1<2))==(1<2))puts("\nPrinciple 1 is valid.");}
```

For the second principle, we make:

```
main() {if((1<2)||(!(1<2)))puts("\nPrinciple 2 is valid.");}
```

For the principle of identity, the test is:

```
main() {if((1<2)==(1>2))puts("\nPrinciple 3 is valid.");}
```

Once the comparison of the if is made between the truth values of sentences, the comparative equality, ‘= =’, also has the meaning of “is equivalent to”, i. e., compares equivalence. The truth value of ‘1<2’ is 1 and the one of ‘1>2’ is 0. Thus, to write a true sentence, type ‘1’, as was done in the above exemplification of Morgan’s laws.

The following program illustrates the use of Boolean operator ‘&&’:

## Example-program #8

```
/* Program "PascalTr.cpp" */

#include <stdio.h>
#include <stdlib.h>

int m[20][20]; char p[80];

int i,j,k,n;
main()
{
    printf("\n Type integer lower than 20:\n");
    gets(p); n=atoi(p);
    if (n>0 && n<16)
    {
        printf("\n\n Pascal Triangle: ");
        m[1][1]=1; m[2][1]=1; m[2][2]=1; k=4;
        printf("\n\n 1\n 1 1");
        for(i=3;i<=n+1;i++) {for(j=1;j<=i;j++){
        m[i][j]=m[i-1][j-1]+m[i-1][j];}
        for(i=3;i<=n+1;i++)
            { j=2;printf("\n 1");while(j<k && k<=n+2)
            { printf("%4d",m[i][j]); j++;
            } k++;
        }
        printf("\n\n");
    }
else if (n<=0) printf("Negative number.");
else if (n>15)
printf("n>15:It does not fit in the screen;");
}
```

Modifications to exercise: Transform the final two lines, beginning with else, in a single line, using the symbol "|", of the connective OR. To do this, type in the if condition, within the parentheses, the expression 'n<2 or n>15', translating it to C; then print the message "The number must be positive and lesser than 16", using the printf() function. Second amendment: Before closing the last brace, which is the closing of the Pascal's triangle end. Start taking the cursor to the beginning of the line of the last brace and pressing Ctrl + N. This line to be printed on the screen can be drawn with the symbol of 'underscore' ("_"), which should be part of an argument puts() or a printf() inside a for loop. Perhaps you have not noticed, but the if that was created in the first amendment above is optional, or more than that, unnecessary. Instead of else if(...) printf(...);, you can just write else printf().

Note that the construction of Pascal's triangle in the program used Stifel's Relation: the sum of two adjacent numbers on the line results in the low number, such as 4 6.

## Bitwise operators

Three logical operators are used in bitwise operations. They are the connectives '&' (bitwise AND), '|' (bitwise OR) and '^' (bitwise XOR). The other bitwise operators are '<<' (scroll to the left, 'left shift'), '>>' (scroll to the right, 'right shift') and '~' (complementary of one, which is unary operator). Any of these operators can only be used with integers or characters.

Taking a = 0x03A1 and b = 0x12B0, we have: a&b = 0x12a0, a|b = 0x13B1 and a^b = 0x1111. What happens is that the operator '&' turns into zeros the bits that in both variables are not equal to 1 and maintains 1 those that are 1 in equivalent positions of the two numbers. Applied to binary numbers 1001 and 1110, it would produce the number 1000. We have such a mini-program:

```
main() { int m,k,p; m=0x101A; k=0x1001; p=m&k; printf("%x\n",p); }
```

The operator "|", the bitwise OR, transforms in 1 the bit that is 1 in one of the numbers
or in both. For example, under this operator, the binary numbers 1010 and 1100 produce the number 1110, also binary.

You can try something like:

```c
main( ) {int m,k,h; m=0x1094; k=0x0F0C; h=m|k; printf("%x\n",h);}
```

The difference between the OR and XOR operators is as it follows: in the aORb expression is valid what is valid for a and also for b, simply; but in the aXORb is valid what is valid in a but not in b or what is valid in b but not in a. In Set Theory this corresponds, for two sets A and B, to what is called symmetric difference between A and B; which is given by (A-B) ∪ (B-A). In C language we can see the XOR operator, denoted by '^', exemplified in:

```c
main( ) {int m,k,n; m=0x04A2; k=0x1D0A; n=m^k; printf("%x\n",n);}
```

The left shift operator ('<<') shifts to the left in the given variable the number of positions specified on the right. For example, n=p<<4 makes n to contain the bits of p, but with four places out of phase to the left, which multiplies the number by 2⁴. It is a very fast way to multiply a hexadecimal number by powers of 16. An example might be:

```c
main( ) {int m,k; m=0x001A; k=m<<8; printf("%x\n",k);}
```

The right shift operator ('>>') works similarly as above, but it moves bits to the right, obviously. An example of using this operator is:

```c
main( ) {int m,j; m=0xF2B0; j=m>>4; printf("%x\n",j);}
```

For the inversion of all bits of a variable you can use the operator complementary of 1 ('~'). With this unary operator, all bits of value 1 become zero and all bits that are zero get with value 1. Thus, the binary number 1001 would be 0110. An example of the use of this operator is:

```c
main( ) {int m,i; m=0x000A; i=~m; printf("%x\n",i);}
```

Note that a digit of a hexadecimal number (0xnnnn) is four digits of a binary number, because the hexadecimal digit of higher value, F, which has value 15, is written as 1111 in binary base.

As the reader knows, hexadecimal digits are 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E and F. The advantage of using hexadecimal is that its conversion to the binary code processor is made of a far more quickly way than what occurs with a number given in the base ten.

## The truth table

From the propositional calculus, or as Boolean wanted, the algebra of logic, we get the tables with the truth values of sentences compositions. For sentences s and p and using T and F to “True” and “False”, we have:

s p sANDp   s p sORp   s NOTs

| s | p | sANDp | s | p | sORp | s | NOTs |
|---|---|---|---|---|---|---|---|
| T | T | T | T | T | T | T |  |
| T | F | F | T | F | T | F |  |
| F | T | F | F | T | T |  |  |
| F | F | F | F | F | F |  |  |

s p sXORp   s p sIMPp   s p sEQVp

| s | p | sXORp | s | p | sIMPp | s | p | sEQVp |
|---|---|---|---|---|---|---|---|---|
| T | T | F | T | T | T | T | T | T |
| T | F | T | T | F | F | T | F | F |
| F | T | T | F | T | T | F | T | F |
| F | F | F | F | F | T | F | F | T |

## Peirce’s logical gates

Charles Sanders Peirce, in the nineteenth century, was who realized the possibility to reproduce in electrical circuits the results observed in Boolean operators. The operators AND, OR and NOT are as follows:

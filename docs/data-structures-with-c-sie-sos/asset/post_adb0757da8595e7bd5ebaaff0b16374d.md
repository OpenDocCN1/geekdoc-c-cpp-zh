
## MEAN(A, B, C, AVE)

where the parameter AVE is assigned the average of A, B, C. Then the statement Call MEAN(T1, T2, T3, TEST) also has the effect of assigning the average of T1, T2 and T3 to TEST. Generally speaking, we will use procedures rather than function subalgorithms.

## 2.8 VARIABLES, DATA TYPES

Each variable in any of our algorithms or programs has a data type which determines the code that is used for storing its value. Four such data types follow:

- 1. Character. Here data are coded using some character code such as EBCDIC or ASCII. The 8-bit EBCDIC code of some characters appears in Fig. 2.7. A single character is normally stored in a byte.
- 2. Real (or floating point). Here numerical data are coded using the exponential form of the data.
- 3. Integer (or fixed point). Here positive integers are coded using binary representation, and negative integers by some binary variation such as 2's complement.
- 4. Logical. Here the variable can have only the value true or false; hence it may be coded using only one bit, 1 for true and 0 for false. (Sometimes the bytes 1111 1111 and 0000 0000 may be used for true and false, respectively.)

The data types of variables in our algorithms will not be explicitly stated as with computer programs but will usually be implied by the context.

## Example 2.11

Suppose a 32-bit memory location X contains the following sequence of bits: 0110 1100 1100 0111 1101 0110 0110 1100

| Char. | Zone | Numeric | Hex | Char. | Zone | Numeric | Hex | Char. | Zone | Numeric | Hex |
|---|---|---|---|---|---|---|---|---|---|---|---|
| A | 1100 | 0001 | C1 | S | 1110 | 0010 | E2 | blank | 0100 | 0000 | 40 |
| B | | 0010 | C2 | T | | 0011 | E3 | . | | 1011 | 4B |
| C | | 0011 | C3 | U | | 0100 | E4 | < | | 1100 | 4C |
| D | | 0100 | C4 | V | | 0101 | E5 | ( | | 1101 | 4D |
| E | | 0101 | C5 | W | | 0110 | E6 | + | 0100 | 1110 | 4E |
| F | | 0110 | C6 | X | | 0111 | E7 | & | 0101 | 0000 | 50 |
| G | | 0111 | C7 | Y | | 1000 | E8 | $ | | 1011 | 5B |
| H | | 1000 | C8 | Z | 1110 | 1001 | E9 | * | | 1100 | 5C |
| I | 1100 | 1001 | C9 | | | | | ) | | 1101 | 5D |
| J | 1101 | 0001 | D1 | 0 | 1111 | 0000 | F0 | ; | 0101 | 1110 | 5E |
| K | | 0010 | D2 | 1 | | 0001 | F1 | - | 0110 | 0000 | 60 |
| L | | 0011 | D3 | 2 | | 0010 | F2 | / | | 0001 | 61 |
| M | | 0100 | D4 | 3 | | 0011 | F3 | . | | 1011 | 6B |
| N | | 0101 | D5 | 4 | | 0100 | F4 | % | | 1100 | 6C |
| O | | 0110 | D6 | 5 | | 0101 | F5 | > | | 1110 | 6E |
| P | | 0111 | D7 | 6 | | 0110 | F6 | ? | 0110 | 1111 | 6F |
| Q | | 1000 | D8 | 7 | | 0111 | F7 | : | 0110 | 1010 | 7A |
| R | 1101 | 1001 | D9 | 8 | | 1000 | F8 | # | | 1011 | 7B |
| | | | | 9 | 1111 | 1001 | F9 | @ | | 1100 | 7C |
| | | | | | | | | = | 0111 | 1110 | 7E |

Fig. 2.7 Part of the EBCDIC Code

There is no way to know the content of the cell unless the data type of X is known.
(a) Suppose X is declared to be of character type and EBCDIC is used. Then the four characters %GO% are stored in X.
(b) Suppose X is declared to be of some other type, such as integer or real. Then an integer or real number is stored in X.

The following C program demonstrates how the same value is interpreted differently based on different associated data types:

## Program 2.6

```
#include <stdio.h>
#include <conio.h>

void main()
{
char c1='1';
int c2=1;
clrscr();

printf("c1 (char) = %c \\nc1's ASCII value = %d\\nc2 (int) = %d",c1,c1,c2);
getch();
}
```

Output:
c1 (char) = 1
c1's ASCII value = 49
c2 (int) = 1

In the above program, variable c1 treats 1 as a character while variable c2 treats 1 as an integer.

## Local and Global Variables

The organization of a computer program into a main program and various subprograms has led to the notion of local and global variables. Normally, each program module contains its own list of variables, called local variables, which can be accessed only by the given program module. Also, subprogram modules may contain parameters, variables which transfer data between a subprogram and its calling program.

## Example 2.12

Consider the procedure SWITCH(AAA, BBB) in Example 2.10. The variables AAA and BBB are parameters; they are used to transfer data between the procedure and a calling algorithm. On the other hand, the variable TEMP in the procedure is a local variable. It “lives” only in the procedure; i.e., its value can be accessed and changed only during the execution of the procedure. In fact, the name TEMP may be used for a variable in any other module and the use of the name will not interfere with the execution of the procedure SWITCH.

## Program 2.7

```c
/* C implementation of the SWITCH procedure */
#include <stdio.h>
#include <conio.h>

int AAA=10;
int BBB=20;
void SWITCH(void);

void main()
{
clrscr();

printf("AAA = %d BBB = %d",AAA,BBB);
SWITCH();
printf("\nAfter calling SWITCH procedure, AAA = %d BBB = %d",AAA,BBB);
getch();
}

void SWITCH(void)
{
int TEMP;
TEMP=AAA;
AAA=BBB;
BBB=TEMP;
return;
}
```

Output:
AAA = 10 BBB = 20
After calling SWITCH procedure, AAA = 20 BBB = 10

Language designers realized that it would be convenient to have certain variables which can be accessed by some or even all the program modules in a computer program. Variables that can be accessed by all program modules are called global variables, and variables that can be accessed by some program modules are called nonlocal variables. Each programming language has its own syntax for declaring such variables. For example, FORTRAN uses a COMMON statement to declare global variables, and Pascal uses scope rules to declare global and nonlocal variables.

Accordingly, there are two basic ways for modules to communicate with each other:

- 1. Directly, by means of well-defined parameters
- 2. Indirectly, by means of nonlocal and global variables

The indirect change of the value of a variable in one module by another module is called a side effect. Readers should be very careful when using nonlocal and global variables, since errors caused by side effects may be difficult to detect.

## SOLVED PROBLEMS

### Mathematical Notations and Functions

2.1 Find (a) $\lfloor 7.5 \rfloor, \lfloor -7.5 \rfloor, \lfloor -18 \rfloor, \lfloor \sqrt{30} \rfloor, \lfloor \sqrt[3]{30} \rfloor, \lfloor \pi \rfloor$; and (b) $\lceil 7.5 \rceil, \lceil -7.5 \rceil, \lceil -18 \rceil, \lceil \sqrt{30} \rceil, \lceil \sqrt[3]{30} \rceil, \lceil \pi \rceil$.

(a) By definition, $\lfloor x \rfloor$ denotes the greatest integer that does not exceed $x$, called the floor of $x$. Hence,
\(\lfloor 7.5 \rfloor = 7 \quad \lfloor -7.5 \rfloor = -8 \quad \lfloor -18 \rfloor = -18\)
\(\lfloor \sqrt{30} \rfloor = 5 \quad \lfloor \sqrt[3]{30} \rfloor = 3 \quad \lfloor \pi \rfloor = 3\)

(b) By definition, $\lceil x \rceil$ denotes the least integer that is not less than $x$, called the ceiling of $x$. Hence,
\(\lceil 7.5 \rceil = 8 \quad \lceil -7.5 \rceil = -7 \quad \lceil -18 \rceil = -18\)
\(\lceil \sqrt{30} \rceil = 6 \quad \lceil \sqrt[3]{30} \rceil = 4 \quad \lceil \pi \rceil = 4\)

2.2 (a) Find $26 \pmod 7, 34 \pmod 8, 2345 \pmod 6, 495 \pmod 11$.
(b) Find $-26 \pmod 7, -2345 \pmod 6, -371 \pmod 8, -39 \pmod 3$.
(c) Using arithmetic modulo 15, evaluate $9 + 13, 7 + 11, 4 - 9, 2 - 10$.

(a) Since $k$ is positive, simply divide $k$ by the modulus $M$ to obtain the remainder $r$. Then $r = k \pmod M$
Thus
\(5 = 26 \pmod 7 \quad 2 = 34 \pmod 8 \quad 5 = 2345 \pmod 6 \quad 0 = 495 \pmod 11\)

(b) When $k$ is negative, divide $|k|$ by the modulus to obtain the remainder $r'$. Then $k \equiv -r' \pmod M$. Hence $k \pmod M = M - r'$ when $r' \neq 0$. Thus
\(-26 \pmod 7 = 7 - 5 = 2 \quad -371 \pmod 8 = 8 - 3 = 5\)
\(-2345 \pmod 6 = 6 - 5 = 1 \quad -39 \pmod 3 = 0\)

(c) Use $a \pm M \equiv a \pmod M$:
\(9 + 13 = 22 \equiv 22 - 15 = 7 \quad 7 + 11 = 18 \equiv 18 - 15 = 3\)
\(4 - 9 = -5 \equiv -5 + 15 = 10 \quad 2 - 10 = -8 \equiv -8 + 15 = 7\)

2.3 List all the permutations of the numbers 1, 2, 3, 4.

Note first that there are $4! = 24$ such permutations:

- 1234 1243 1324 1342 1423 1432
- 2134 2143 2314 2341 2413 2431
- 3124 3142 3214 3241 3412 3421
- 4123 4132 4213 4231 4312 4321

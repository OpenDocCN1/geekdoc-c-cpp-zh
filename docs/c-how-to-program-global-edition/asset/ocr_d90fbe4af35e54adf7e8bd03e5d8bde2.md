# Common Programming Error 2.8

Confusing the equality operator == with the assignment operator =. To avoid this confusion, the equality operator should be read "double equals" and the assignment operator should be read "gets" or "is assigned the value of." As you’ll see, confusing these operators may not cause an easy-to-recognize compilation error, but may cause extremely subtle logic errors.

| Algebraic equality or relational operator | C equality or relational operator | Example of C condition | Meaning of C condition |
|---|---|---|---|
| *Relational operators* |  |  |  |
| > | > | x > y | x is greater than y |
| < | < | x < y | x is less than y |
| ≥ | >= | x >= y | x is greater than or equal to y |
| ≤ | <= | x <= y | x is less than or equal to y |
| *Equality operators* |  |  |  |
| = | == | x == y | x is equal to y |
| ≠ | != | x != y | x is not equal to y |

**Fig. 2.12** | Equality and relational operators.

Figure 2.13 uses six if statements to compare two numbers entered by the user. If the condition in any of these if statements is true, the printf statement associated with that if executes. The program and three sample execution outputs are shown in the figure.

```
~~~c
1  // Fig. 2.13: fig02_13.c
2  // Using if statements, relational
3  // operators, and equality operators.
4  #include <stdio.h>
5
6  // function main begins program execution
7  int main( void )
8  {
9     printf( "Enter two integers, and I will tell you\n" );
10    printf( "the relationships they satisfy: " );
11
12    int num1; // first number to be read from user
13    int num2; // second number to be read from user
14
15    scanf( "%d %d", &num1, &num2 ); // read two integers
16
17    if ( num1 == num2 ) {
18       printf( "%d is equal to %d\n", num1, num2 );
19    } // end if
20
~~~
```

**Fig. 2.13** | Using if statements, relational operators, and equality operators. (Part 1 of 2.)
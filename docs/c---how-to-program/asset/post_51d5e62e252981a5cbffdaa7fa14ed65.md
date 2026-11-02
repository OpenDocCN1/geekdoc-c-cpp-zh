
The complete second refinement appears in Fig. 3.9. We use blank lines to set off the while statement for program readability.

This pseudocode is now sufficiently refined for conversion to C. The C program and two sample executions are shown in Fig. 3.10. We’ve taken advantage of a feature of C that allows initialization to be incorporated into definitions (lines 9–11). Such initialization occurs at compile time. Also, notice that when you output an unsigned int you use the %u conversion specifier (lines 33–34).

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student to one
4
5  While student counter is less than or equal to ten
6      Input the next exam result
7
8      If the student passed
9          Add one to passes
10     else
11         Add one to failures
12
13     Add one to student counter
14
15  Print the number of passes
16  Print the number of failures
17  If more than eight students passed
18     Print "Bonus to instructor!"
```

Fig. 3.9 | Pseudocode for examination-results problem.

![](img/d0d3b7423c2d9e5650be79209ea1885d_122_0.png)

> **Software Engineering Observation 3.5**
> 
> *Experience has shown that the most difficult part of solving a problem on a computer is developing the algorithm for the solution. Once a correct algorithm has been specified, the process of producing a working C program is normally straightforward.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_122_1.png)

> **Software Engineering Observation 3.6**
> 
> *Many programmers write programs without ever using program-development tools such as pseudocode. They feel that their ultimate goal is to solve the problem on a computer and that writing pseudocode merely delays the production of final output.*

```
1 // Fig. 3.10: fig03_10.c
2 // Analysis of examination results.
3 #include <stdio.h>
4
```

Fig. 3.10 | Analysis of examination results. (Part 1 of 3.)

```
// function main begins program execution
int main( void )
{
   // initialize variables in definitions
   unsigned int passes = 0; // number of passes
   unsigned int failures = 0; // number of failures
   unsigned int student = 1; // student counter
   int result; // one exam result

   // process 10 students using counter-controlled loop
   while ( student <= 10 ) {

      // prompt user for input and obtain value from user
      printf( "%s", "Enter result (1=pass,2=fail): " );
      scanf( "%d", &result );

      // if result 1, increment passes
      if ( result == 1 ) {
         passes = passes + 1;
      } // end if
      else { // otherwise, increment failures
         failures = failures + 1;
      } // end else

      student = student + 1; // increment student counter
   } // end while

   // termination phase; display number of passes and failures
   printf( "Passed %u\n", passes );
   printf( "Failed %u\n", failures );

   // if more than eight students passed, print "Bonus to instructor!"
   if ( passes > 8 ) {
      puts( "Bonus to instructor!" );
   } // end if
} // end function main
```

```
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Passed 6
Failed 4
```

**Fig. 3.10** | Analysis of examination results. (Part 2 of 3.)

```
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Passed 9
Failed 1
Bonus to instructor!
```

**Fig. 3.10** | Analysis of examination results. (Part 3 of 3.)

## 3.11 Assignment Operators

C provides several assignment operators for abbreviating assignment expressions. For example, the statement

```
c = c + 3;
```

can be abbreviated with the addition assignment operator += as

```
c += 3;
```

The += operator adds the value of the expression on the *right* of the operator to the value of the variable on the *left* of the operator and stores the result in the variable on the *left* of the operator. Any statement of the form

```
variable = variable operator expression;
```

where *operator* is one of the binary operators +, −, *, / or % (or others we’ll discuss in Chapter 10), can be written in the form

```
variable operator= expression;
```

Thus the assignment c += 3 adds 3 to c. Figure 3.11 shows the arithmetic assignment operators, sample expressions using these operators and explanations.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12;* |  |  |  |
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

**Fig. 3.11** | Arithmetic assignment operators.

## 3.12 Increment and Decrement Operators

C also provides the unary increment operator, ++, and the unary decrement operator, --, which are summarized in Fig. 3.12. If a variable c is to be incremented by 1, the increment operator ++ can be used rather than the expressions c = c + 1 or c += 1. If increment or decrement operators are placed before a variable (i.e., prefixed), they're referred to as the preincrement or predecrement operators, respectively. If increment or decrement operators are placed after a variable (i.e., postfixed), they're referred to as the postincrement or postdecrement operators, respectively. Preincrementing (predecrementing) a variable causes the variable to be incremented (decremented) by 1, then its new value is used in the expression in which it appears. Postincrementing (postdecrementing) the variable causes the current value of the variable to be used in the expression in which it appears, then the variable value is incremented (decremented) by 1.

| Operator | Sample expression | Explanation |
| --- | --- | --- |
| `++` | `++a` | Increment a by 1, then use the new value of a in the expression in which a resides. |
| `++` | `a++` | Use the current value of a in the expression in which a resides, then increment a by 1. |
| `--` | `--b` | Decrement b by 1, then use the new value of b in the expression in which b resides. |
| `--` | `b--` | Use the current value of b in the expression in which b resides, then decrement b by 1. |

Fig. 3.12 | Increment and decrement operators

Figure 3.13 demonstrates the difference between the preincrementing and the postincrementing versions of the ++ operator. Postincrementing the variable c causes it to be incremented *after* it is used in the printf statement. Preincrementing the variable c causes it to be incremented *before* it is used in the printf statement.

```
1   // Fig. 3.13: fig03_13.c
2   // Preincrementing and postincrementing.
3   #include <stdio.h>
4
5   // function main begins program execution
6   int main( void )
7   {
8       int c; // define variable
9
10      // demonstrate postincrement
11      c = 5; // assign 5 to c
12      printf( "%d\n", c ); // print 5
13      printf( "%d\n", c++ ); // print 5 then postincrement
14      printf( "%d\n", c ); // print 6
```

Fig. 3.13 | Preincrementing and postincrementing. (Part 1 of 2.)

```
15
16      // demonstrate preincrement
17      c = 5; // assign 5 to c
18      printf( "%d\n", c ); // print 5
19      printf( "%d\n", ++c ); // preincrement then print 6
20      printf( "%d\n", c ); // print 6
21   } // end function main
```

```
5
5
6

5
6
6
```

Fig. 3.13 | Preincrementing and postincrementing. (Part 2 of 2.)

The program displays the value of c before and after the ++ operator is used. The decrement operator (--) works similarly.

## Good Programming Practice 3.4

*Unary operators should be placed directly next to their operands with no intervening spaces.*

The three assignment statements in Fig. 3.10

```
passes = passes + 1;
failures = failures + 1;
student = student + 1;
```

can be written more concisely with assignment operators as

```
passes += 1;
failures += 1;
student += 1;
```

with preincrement operators as

```
++passes;
++failures;
++student;
```

or with postincrement operators as

```
passes++;
failures++;
student++;
```

It's important to note here that when incrementing or decrementing a variable in a statement by itself, the preincrement and postincrement forms have the same effect. It's only when a variable appears in the context of a larger expression that preincrementing and postincrementing have different effects (and similarly for predecrementing and postdecrementing). Of the expressions we've studied thus far, only a simple variable name may be used as the operand of an increment or decrement operator.

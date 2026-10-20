```
```java
10    // total even integers from 2 through 20
11    for ( int number = 2; number <= 20; number += 2 )
12        total += number;
13
14    System.out.printf( "Sum is %d\n", total ); // display results
15 } // end main
16 } // end class Sum
```
```

```
Sum is 110
```

Fig. 5.5 | Summing integers with the for statement. (Part 2 of 2.)

The *initialization* and *increment* expressions can be comma-separated lists that enable you to use multiple initialization expressions or multiple increment expressions. For example, *although this is discouraged*, you could merge the body of the for statement in lines 11–12 of Fig. 5.5 into the increment portion of the for header by using a comma as follows:

```
```java
for ( int number = 2; number <= 20; total += number, number += 2 )
    ; // empty statement
```
```

> **Good Programming Practice 5.1**  
> For readability limit the size of control-statement headers to a single line if possible.

# Application: Compound-Interest Calculations

Let’s use the for statement to compute compound interest. Consider the following problem:

> A person invests $1000 in a savings account yielding 5% interest. Assuming that all the interest is left on deposit, calculate and print the amount of money in the account at the end of each year for 10 years. Use the following formula to determine the amounts:
> 
> \[a = p(1 + r)^n\]
> 
> where
> 
> - *p* is the original amount invested (i.e., the principal)
> - *r* is the annual interest rate (e.g., 0.05 for 5%)
> - *n* is the number of years
> - *a* is the amount on deposit at the end of the *n*th year.

The solution to this problem (Fig. 5.6) involves a loop that performs the indicated calculation for each of the 10 years the money remains on deposit. Lines 8–10 in method main declare double variables amount, principal and rate, and initialize principal to 1000.0 and rate to 0.05. Java treats floating-point constants like 1000.0 and 0.05 as type double. Similarly, Java treats whole-number constants like 7 and -22 as type int.

```
```java
1  // Fig. 5.6: Interest.java
2  // Compound-interest calculations with for.

4  public class Interest
5  {
```
```

Fig. 5.6 | Compound-interest calculations with for. (Part 1 of 2.)
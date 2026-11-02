```
```c
// Fig. 4.5: fig04_05.c
// Summation with for.
#include <stdio.h>

int main(void)
{
    unsigned int sum = 0; // initialize sum

    for (unsigned int number = 2; number <= 100; number += 2) {
        sum += number; // add number to sum
    }

    printf("Sum is %u\n", sum);
}
```
```

```
```
Sum is 2550
```
```

**Fig. 4.5** | Summation with for.

# ### Application: Compound-Interest Calculations

The next example computes compound interest using the for statement. Consider the following problem statement:

> > A person invests $1000.00 in a savings account yielding 5% interest. Assuming that
> > all interest is left on deposit in the account, calculate and print the amount of money
> > in the account at the end of each year for 10 years. Use the following formula for
> > determining these amounts:

a = p(1 + r)^n

where

+   - *p* is the original amount invested (i.e., the principal)
+   - *r* is the annual interest rate (for example, .05 for 5%)
+   - *n* is the number of years
+   - *a* is the amount on deposit at the end of the *n*th year.

This problem involves a loop that performs the indicated calculation for each of the 10 years the money remains on deposit. The solution is shown in Fig. 4.6.

```
```c
// Fig. 4.6: fig04_06.c
// Calculating compound interest.
#include <stdio.h>
#include <math.h>

int main(void)
{
    double principal = 1000.0; // starting principal
    double rate = .05; // annual interest rate

    // output table column heads
    printf("%4s%21s\n", "Year", "Amount on deposit");
```
```

**Fig. 4.6** | Calculating compound interest. (Part 1 of 2.)
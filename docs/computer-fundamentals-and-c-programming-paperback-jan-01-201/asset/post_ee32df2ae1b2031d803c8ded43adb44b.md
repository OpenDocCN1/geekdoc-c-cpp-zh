
However, we can sometimes update the key variable in the control expression itself and get rid of one statement in the loop body. The following code related to the program `while_intro.c` will also work:

```c
short i = 0, sum = 0;
while (++i <= 10) {
    sum += i;
    printf("%hd ", sum);
}
printf("\nSum of first 10 integers = %hd\n", sum);
```

i initialized to 0 not 1; ++i instead of i; Prints 55

The updating of the key variable i has now been moved to the control expression, but this movement needs the initial value of i to be changed as well.

> **Note:** When you change the key variable in the control expression to one having prefix or postfix operators, you also need to change either the relational operator (say, > to >=) or the initial value of the key variable.

## 8.3 THREE PROGRAMS USING `while`

Before we continue exploring this loop in C, let’s examine three simple programs that use simple control expressions. All of these programs are revised in subsequent chapters to use arrays and functions. Two of the later versions also use the *recursive* technique in contrast to the *iterative* approach of loops that is pursued here.

### 8.3.1 `factorial.c`: Determining the Factorial of a Number

The factorial of a positive integer *n* (denoted by *n*!) is the product of all positive integers less than or equal to *n*. Thus, 4! = 4 × 3 × 2 × 1 = 24. Program 8.2 uses a `while` loop to compute the factorial of an integer supplied by the user. Section 11.13.1 shows an alternative way of solving the same problem using a function.

```c
/* factorial.c: Program to determine factorial of a number
                  without using a function. */
#include <stdio.h>
int main(void)
{
    short num1, num2;
    unsigned int factorial = 1;      /* unsigned doubles the maximum value */
    printf("Factorial of which number? ");
    scanf("%hd", &num1);
    num2 = num1;                     /* Saving num1 before it changes */
    while (num1 >= 1) {
        factorial *= num1;
        num1--;
    }
    printf("Factorial of %hd = %d\n", num2, factorial);
    return 0;
}
```

PROGRAM 8.2: `factorial.c`

| Factorial of which number? | Result |
|---|---|
| 4 | Factorial of 4 = 24 |
| 6 | Factorial of 6 = 720 |
| 1 | Factorial of 1 = 1 |

PROGRAM OUTPUT: **factorial.c**

### 8.3.2 `extract_digits.c`: Program to Reverse Digits of an Integer

Program 8.3 performs the dual task of reversing the digits of an integer and printing their sum. Using 10 as the divisor, each digit is extracted from the right using the / and % operators. The program has the demerit of not saving the digits, so you can’t perform any other task with them once printing is complete.

```c
/* extract_digits.c: Reverses the digits of an integer. Prints and sums
   the digits using the % and / operators. */
#include <stdio.h>
int main(void)
{
    unsigned int number;
    short last_digit, sum = 0;

    printf("Key in an integer: ");
    scanf("%d", &number);

    while (number != 0) {
        last_digit = number % 10;          /* Extracts last digit */
        number = number / 10;              /* Removes last digit */
        sum += last_digit;
        printf("%hd ", last_digit);
    }
    printf("\nSum of digits: %hd\n", sum);
    return 0;
}
```

PROGRAM 8.3: **extract_digits.c**

```
Key in an integer: 13569
9 6 5 3 1
Sum of digits: 24
```

PROGRAM OUTPUT: **extract_digits.c**

In every iteration of the **while** loop, the / operation removes the last digit and the % operation saves this digit. This is how the values of the variables `last_digit` and `number` change with every loop iteration:

| | Iteration 1 | Iteration 2 | Iteration 3 | Iteration 4 | Iteration 5 |
|---|---|---|---|---|---|
| last_digit | 9 | 6 | 5 | 3 | 1 |
| number | 1356 | 135 | 13 | 1 | 0 |

The program is inflexible; we can't use this technique to print the digits in the sequence they occur in the number. We need to save every digit, not with five variables, but with an *array* of five elements. We'll revisit the program in Section 10.7.1.

### 8.3.3 `fibonacci_ite.c`: Printing and Summing the Fibonacci Numbers

Every student of computer science would have encountered the Fibonacci sequence of numbers at some point in their learning curve. In this sequence, which starts with the values 0 and 1, each subsequent term is the sum of the previous two. This relationship can be seen in the first 12 terms of this sequence:

0 1 1 2 3 5 8 13 21 34 55 89

Here, 55 is the sum of its two predecessors, 34 and 21, while 21 is the sum of 13 and 8. Program 8.4 prints and sums *n* terms of the sequence where *n* is provided by the user. The program employs a **while** loop that runs *n* times. In each iteration, the sum of the variables prev1 and prev2 are saved in sum and printed. Note that the first two terms are generated from the logic which has not treated them in an exceptional manner. This has been made possible by careful selection of the initialized values of four variables.

```c
/* fibonacci_ite.c: Uses the iterative technique to generate terms of
   the Fibonacci series and compute the sum of terms. */

#include <stdio.h>
int main(void)
{
    short num;
    unsigned long prev1 = 0, prev2 = 0, sum = 1, sum_terms = 0;
    short i = 0;

    printf("Enter last term of series: ");
    scanf("%hd", &num);

    while (i++ < num) {
        printf("%ld ", sum);          /* Prints each term */
        sum_terms += sum;             /* Sums all terms */
        prev1 = prev2;
        prev2 = sum;
        sum = prev1 + prev2;          /* Sums previous two terms */
    }
    printf("\nSum of first %hd terms = %ld\n", num, sum_terms);
    return 0;
}
```

**PROGRAM 8.4:** `fibonacci_ite.c`

```
Enter last term of series: 15
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610
Sum of first 15 terms = 1596
```

PROGRAM OUTPUT: **fibonacci_ite.c**

The Fibonacci sequence can also be generated by using a *recursive* function, i.e., a function that calls itself repeatedly. Section 11.4.3 examines this function and its demerits compared to the iterative approach used here.

## 8.4 LOADING THE CONTROL EXPRESSION

Repetition creates opportunities for using functions as control expressions. For instance, the **getchar** function, a member of the I/O family of functions, fetches a character from the keyboard and returns its ASCII value. The **putchar** function uses this value to display the character. Consider the following code snippet:

```
int c;
c = getchar();                 Gets the first character
while (c != EOF) {             EOF is end-of-file
    putchar(c);                Displays the character
    c = getchar();             Fetches the next character
}
```

This appears to be a simple way of retrieving a string of text from keyboard input. But because **getchar** returns the ASCII value of the fetched character, you can move the **getchar** statement itself to the control expression:

```c
while ((c = getchar()) != EOF)
    putchar(c);
```

This works perfectly and looks clean as well because a single **getchar** is used. The != has a higher precedence than the =, so parentheses must be provided around the assignment (c = getchar()). This ensures that the return value of **getchar** is assigned to c before c is compared to EOF (end-of-file).

Many functions return a value. **scanf** returns the number of items successfully read and **printf** returns the number of characters written, so these functions can also be used as control expressions:

```c
while (scanf("%d", &num) == 1)
while (printf("Enter the amount: "))
```

Both **getchar** and **putchar** are discussed in Chapter 9 which examines the major I/O functions. The **scanf** and **printf** functions are also examined in the same chapter.

### 8.4.1 Merging Entire Loop Body with the Control Expression

A previous example merged both calls to **getchar** to a single call in the control expression. But **putchar** also returns a value (that of the character written), so why not move it too to the control expression? Yes, we can do that as well:

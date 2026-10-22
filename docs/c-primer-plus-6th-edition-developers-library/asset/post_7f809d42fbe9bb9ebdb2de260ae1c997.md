
## Summary

The main topic of this chapter has been program control. C offers you many aids for structuring your programs. The while and the for statements provide entry-condition loops. The for statements are particularly suited for loops that involve initialization and updating. The comma operator enables you to initialize and update more than one variable in a for loop. For the less common occasion when an exit-condition loop is needed, C has the do while statement.

A typical while loop design looks like this:

```
get first value
while (value meets test)
{
    process the value
    get next value
}
```

A for loop doing the same thing would look like this:

```
for (get first value; value meets test; get next value)
    process the value
```

All these loops use a test condition to determine whether another loop cycle is to be executed. In general, the loop continues if the test expression evaluates to a nonzero value; otherwise, it terminates. Often, the test condition is a relational expression, which is an expression formed by using a relational operator. Such an expression has a value of 1 if the relation is true and a value of 0 otherwise. Variables of the _Bool type, introduced by C99, can only hold the value 1 or 0, signifying true or false.

In addition to relational operators, this chapter looked at several of C's arithmetic assignment operators, such as += and *=. These operators modify the value of the left-hand operand by performing an arithmetic operation on it.

Arrays were the next subject. Arrays are declared using brackets to indicate the number of elements. The first element of an array is numbered 0; the second is numbered 1, and so forth. For example, the declaration

```
double hippos[20];
```

creates an array of 20 elements, and the individual elements range from hippos[0] through hippos[19]. The subscripts used to number arrays can be manipulated conveniently by using loops.

Finally, the chapter showed how to write and use a function with a return value.

## Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

- 1. Find the value of quack after each line; each of the final five statements uses the value of quack produced by the preceding statement.
  ```
  int quack = 2;
  quack += 5;
  quack *= 10;
  quack -= 6;
  quack /= 8;
  quack %= 3;
  ```

- 2. Given that value is an int, what output would the following loop produce?
  ```
  for ( value = 36; value > 0; value /= 2 )
      printf("%3d", value);
  ```
  What problems would there be if value were double instead of int?

- 3. Represent each of the following test conditions:
  a. x is greater than 5.
  b. scanf() attempts to read a single double (called x) and fails.
  c. x has the value 5.

- 4. Represent each of the following test conditions:
  a. scanf() succeeds in reading a single integer.
  b. x is not 5.
  c. x is 20 or greater.

- 5. You suspect that the following program is not perfect. What errors can you find?
  ```
  #include <stdio.h>
  int main(void)
  {
      int i, j, list(10);
  
      for (i = 1, i <= 10, i++)
      {
          list[i] = 2*i + 3;
          for (j = 1, j >= i, j++)
              printf(" %d", list[j]);
  ```

```
printf("\n");
}
/* line 11 */
/* line 12 */
```

- 6. Use nested loops to write a program that produces this pattern:

$$$$$$$$ 
$$$$$$$$ 
$$$$$$$$ 
$$$$$$$$

- 7. What will each of the following programs print?

a.
```
#include <stdio.h>

int main(void)
{
    int i = 0;

    while (++i < 4)
        printf("Hi! ");
    do
        printf("Bye! ");
    while (i++ < 8);
    return 0;
}
```

b.
```
#include <stdio.h>

int main(void)
{
    int i;
    char ch;

    for (i = 0, ch = 'A'; i < 4; i++, ch += 2 * i)
        printf("%c", ch);
    return 0;
}
```

- 8. Given the input Go west, young man!, what would each of the following programs produce for output? (The ! follows the space character in the ASCII sequence.)

a.
```
#include <stdio.h>
```
```
int main(void)
{
    char ch;

    scanf("%c", &ch);
    while ( ch != 'g' )
    {
        printf("%c", ch);
        scanf("%c", &ch);
    }
    return 0;
}
```

b.
```
#include <stdio.h>

int main(void)
{
    char ch;

    scanf("%c", &ch);
    while ( ch != 'g' )
    {
        printf("%c", ++ch);
        scanf("%c", &ch);
    }
    return 0;
}
```

c.
```
#include <stdio.h>

int main(void)
{
    char ch;

    do {
        scanf("%c", &ch);
        printf("%c", ch);
    } while ( ch != 'g' );
    return 0;
}
```

d.
```
#include <stdio.h>

```
{ char ch;

scanf("%c", &ch);
for ( ch = '$'; ch != 'g'; scanf("%c", &ch) )
    printf("%c", ch);
return 0;
}
```

9. What will the following program print?

```
#include <stdio.h>
int main(void)
{
    int n, m;

    n = 30;
    while (++n <= 33)
        printf("%d|",n);

    n = 30;
    do
        printf("%d|",n);
    while (++n <= 33);

    printf("\n***\n");

    for (n = 1; n*n < 200; n += 4)
        printf("%d\n", n);

    printf("\n***\n");

    for (n = 2, m = 6; n < m; n *= 2, m+= 2)
        printf("%d %d\n", n, m);

    printf("\n***\n");

    for (n = 5; n > 0; n--)
    {
        for (m = 0; m <= n; m++)
            printf("=");
        printf("\n");
    }
    return 0;
}
```

10. Consider the following declaration:

```
double mint[10];
```

- a. What is the array name?
- b. How many elements does the array have?
- c. What kind of value can be stored in each element?
- d. Which of the following is a correct usage of scanf() with this array?
  i. scanf("%lf", mint[2])
  ii. scanf("%lf", &mint[2])
  iii. scanf("%lf", &mint)

11. Mr. Noah likes counting by twos, so he’s written the following program to create an array and to fill it with the integers 2, 4, 6, 8, and so on. What, if anything, is wrong with this program?

```
#include <stdio.h>
#define SIZE 8
int main(void)
{
    int by_twos[SIZE];
    int index;

    for (index = 1; index <= SIZE; index++)
        by_twos[index] = 2 * index;
    for (index = 1; index <= SIZE; index++)
        printf("%d ", by_twos[index]);
    printf("\n");
    return 0;
}
```

12. You want to write a function that returns a long value. What should your definition of the function include?

13. Define a function that takes an int argument and that returns, as a long, the square of that value.

14. What will the following program print?

```
#include <stdio.h>
int main(void)
{
    int k;
```

If your system doesn’t encode letters in numeric order, see the suggestion in programming exercise 3.

- 5. Have a program request the user to enter an uppercase letter. Use nested loops to produce a pyramid pattern like this:
  A
  ABA
  ABCBA
  ABCDCBA
  ABCDEDCBA

The pattern should extend to the character entered. For example, the preceding pattern would result from an input value of E. Hint: Use an outer loop to handle the rows. Use three inner loops in a row, one to handle the spaces, one for printing letters in ascending order, and one for printing letters in descending order. If your system doesn’t use ASCII or a similar system that represents letters in strict number order, see the suggestion in programming exercise 3.

- 6. Write a program that prints a table with each line giving an integer, its square, and its cube. Ask the user to input the lower and upper limits for the table. Use a for loop.

- 7. Write a program that reads a single word into a character array and then prints the word backward. Hint: Use strlen() (Chapter 4) to compute the index of the last character in the array.

- 8. Write a program that requests two floating-point numbers and prints the value of their difference divided by their product. Have the program loop through pairs of input values until the user enters nonnumeric input.

- 9. Modify exercise 8 so that it uses a function to return the value of the calculation.

- 10. Write a program that requests lower and upper integer limits, calculates the sum of all the integer squares from the square of the lower limit to the square of the upper limit, and displays the answer. The program should then continue to prompt for limits and display answers until the user enters an upper limit that is equal to or less than the lower limit. A sample run should look something like this:

```
Enter lower and upper integer limits: 5 9
The sums of the squares from 25 to 81 is 255
Enter next set of limits: 3 25
The sums of the squares from 9 to 625 is 5520
Enter next set of limits: 5 5
Done
```

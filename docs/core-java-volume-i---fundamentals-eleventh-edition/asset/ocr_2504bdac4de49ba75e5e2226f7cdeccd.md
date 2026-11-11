```
```java
int i = 10;
while (i > 0)
{
    System.out.println("Counting down . . . " + i);
    i--;
}
```
```

Listing 3.5 shows a typical example of a for loop.

The program computes the odds of winning a lottery. For example, if you must pick six numbers from the numbers 1 to 50 to win, then there are (50 × 49 × 48 × 47 × 46 × 45)/(1 × 2 × 3 × 4 × 5 × 6) possible outcomes, so your chance is 1 in 15,890,700. Good luck!

In general, if you pick *k* numbers out of *n*, there are

\[
\frac{n \times (n - 1) \times (n - 2) \times \cdots \times (n - k + 1)}{1 \times 2 \times 3 \times 4 \times \cdots \times k}
\]

possible outcomes. The following for loop computes this value:

```
```java
int lotteryOdds = 1;
for (int i = 1; i <= k; i++)
    lotteryOdds = lotteryOdds * (n - i + 1) / i;
```
```

> **NOTE:** See Section 3.10.3, “The ‘for each’ Loop,” on p. 110 for a description of the enhanced for loop (also called “for each” loop) that was added to the Java language in Java 5.

# **Listing 3.5** `LotteryOdds/LotteryOdds.java`

```
```java
import java.util.*;

/**
 * This program demonstrates a <code>for</code> loop.
 * @version 1.20 2004-02-10
 * @author Cay Horstmann
 */
public class LotteryOdds
{
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);

        System.out.print("How many numbers do you need to draw? ");
        int k = in.nextInt();
```
```
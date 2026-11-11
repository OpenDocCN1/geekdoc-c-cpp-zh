
```
38    }
39  }
```

### Listing 3.4 Retirement2/Retirement2.java

```java
1  import java.util.*;
2
3  /**
4   * This program demonstrates a <code>do/while</code> loop.
5   * @version 1.20 2004-02-10
6   * @author Cay Horstmann
7   */
8  public class Retirement2
9  {
10    public static void main(String[] args)
11    {
12       Scanner in = new Scanner(System.in);
13
14       System.out.print("How much money will you contribute every year? ");
15       double payment = in.nextDouble();
16
17       System.out.print("Interest rate in %: ");
18       double interestRate = in.nextDouble();
19
20       double balance = 0;
21       int year = 0;
22
23       String input;
24
25       // update account balance while user isn't ready to retire
26       do
27       {
28          // add this year's payment and interest
29          balance += payment;
30          double interest = balance * interestRate / 100;
31          balance += interest;
32
33            year++;
34
35            // print current balance
36            System.out.printf("After year %d, your balance is %,.2f%n", year, balance);
37
38            // ask if ready to retire and get input
39            System.out.print("Ready to retire? (Y/N) ");
40            input = in.next();
41        }
42        while (input.equals("N"));
43    }
44 }
```

### 3.8.4 Determinate Loops

The `for` loop is a general construct to support iteration controlled by a counter or similar variable that is updated after every iteration. As [Figure 3.12](#) shows, the following loop prints the numbers from 1 to 10 on the screen:

```java
for (int i = 1; i <= 10; i++)
    System.out.println(i);
```

The first slot of the `for` statement usually holds the counter initialization. The second slot gives the condition that will be tested before each new pass through the loop, and the third slot specifies how to update the counter.

Although Java, like C++, allows almost any expression in the various slots of a `for` loop, it is an unwritten rule of good taste that the three slots should only initialize, test, and update the same counter variable. One can write very obscure loops by disregarding this rule.

![](img/0e7b74ef51a065c077b42cd87b362288_154_0.png)

**Figure 3.12** Flowchart for the `for` statement

Even within the bounds of good taste, much is possible. For example, you can have loops that count down:

```java
for (int i = 10; i > 0; i--)
    System.out.println("Counting down . . . " + i);
System.out.println("Blastoff!");
```

**CAUTION:**

Be careful with testing for equality of floating-point numbers in loops. A `for` loop like this one

```java
for (double x = 0; x != 10; x += 0.1) . . .
```

might never end. Because of roundoff errors, the final value might not be reached exactly. In this example, x jumps from 9.99999999999998 to 10.09999999999998 because there is no exact binary representation for 0.1.

When you declare a variable in the first slot of the `for` statement, the scope of that variable extends until the end of the body of the `for` loop.

```java
for (int i = 1; i <= 10; i++)
{
    . . .
}
// i no longer defined here
```

In particular, if you define a variable inside a `for` statement, you cannot use its value outside the loop. Therefore, if you wish to use the final value of a loop counter outside the `for` loop, be sure to declare it outside the loop header.

```java
int i;
for (i = 1; i <= 10; i++)
{
    . . .
}
```

```java
18        int n = in.nextInt();
19
20        /*
21         * compute binomial coefficient n*(n-1)*(n-2)*...*(n-k+1)/(1*2*3*...*k)
22         */
23
24        int lotteryOdds = 1;
25        for (int i = 1; i <= k; i++)
26            lotteryOdds = lotteryOdds * (n - i + 1) / i;
27
28        System.out.println("Your odds are 1 in " + lotteryOdds + ". Good luck!");
29    }
30 }
```

### 3.8.5 Multiple Selections with `switch`

The `if/else` construct can be cumbersome when you have to deal with multiple alternatives for the same expression. The `switch` statement makes this easier, particularly with the form that has been introduced in Java 14.

For example, if you set up a menu system with four alternatives like that in Figure 3.13, you could use code that looks like this:

```java
Scanner in = new Scanner(System.in);
System.out.print("Select an option (1, 2, 3, 4) ");
int choice = in.nextInt();
switch (choice)
{
    case 1 ->
        . . .
    case 2 ->
        . . .
    case 3 ->
        . . .
    case 4 ->
        . . .
    default ->
        System.out.println("Bad input");
}
```

**Figure 3.13** Flowchart for the `switch` statement

A case label can be

- A constant expression of type char, byte, short, or int
- An enumerated constant
- A string literal
- More than one of these, separated by commas

For example,

```java
String input = . . .;
switch (input.toLowerCase())
{
    case "yes", "y" ->
        . . .
    case "no", "n" ->
        . . .
    default ->
        . . .
}
```

The “classic” form of the `switch` statement, which dates all the way back to the C language, has been supported since Java 1.0. It has the form:

```java
int choice = . . .;
switch (choice)
{
    case 1:
        . . .
        break;
    case 2:
        . . .
        break;
    case 3:
        . . .
        break;
    case 4:
        . . .
        break;
    default:
        // bad input
        . . .
        break;
}
```

Execution starts at the `case` label that matches the value on which the selection is performed and continues until the next `break` or the end of the `switch`. If none of the case labels match, then the `default` clause is executed, if it is present.

**CAUTION:**

It is possible for multiple alternatives to be triggered. If you forget to add a `break` at the end of an alternative, execution falls through to the next alternative! This behavior is plainly dangerous and a common cause for errors.

To detect such problems, compile your code with the `-Xlint:fallthrough` option, like this:

```java
javac -Xlint:fallthrough Test.java
```

Then the compiler will issue a warning whenever an alternative does not end with a `break` statement.

If you actually want to use the fallthrough behavior, tag the surrounding method with the annotation `@SuppressWarnings("fallthrough")`. Then no warnings will be generated for that method. (An annotation is a mechanism for supplying information to the compiler or a tool that processes Java source or class files. Volume II has an in-depth coverage of annotations.)

These two forms of `switch` are *statements*. In [Section 3.5.9, “Switch Expressions,”] on p. 58, you saw a `switch` *expression*, which yields a value. It doesn’t have the fallthrough behavior.

For symmetry, Java 14 also introduces a `switch` expression with fallthrough, for a total of four forms of `switch`. [Table 3.7] shows them all.

In the fallthrough variants, each case ends with a colon. If the cases end with arrows `->`, then there is no fallthrough. You can’t mix colons and arrows in a single `switch` statement.

Note the `yield` keyword with `switch` expressions. Like `break`, it terminates execution. Unlike `break`, it also yields a value—the value of the expression.

To use statements in a branch of a `switch` expression without fallthrough, you must use braces and `yield`, as in the example in the table that adds a logging statement to a branch:

```java
case "Spring" ->
    {
        System.out.println("spring time!");
        yield 6;
    }
```

Each branch of a `switch` *expression* must yield a value. Most commonly, each value follows an `->` arrow:

```java
case "Summer", "Winter" -> 6;
```

If that is not possible, use a `yield` statement.

**Table 3.7** The four forms of `switch`

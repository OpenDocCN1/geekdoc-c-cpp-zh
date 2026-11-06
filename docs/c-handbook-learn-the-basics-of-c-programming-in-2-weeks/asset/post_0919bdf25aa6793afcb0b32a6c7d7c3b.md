
```java
3
4  int a = 20, b = 30;
5  if (a > b)
6      System.out.println("a is greater than b");
7  if (a < b)
8      System.out.println("b is greater than a");
9  }
10 }
```

What do you think will this program print?

## Understanding the if-else (or nested if) Statement

Like the *if* statement, the if-else statement also commands the computer to execute a particular block of codes under the if statement only if the expression within the statement is true. If the statement is false, then the else statement must be executed next and only if the condition within the else option is satisfied.

The if statement follows this syntax:

```text
if (<conditional expression>) {

<statement action>

} else {

<statement action>
}
```

Take a look at the sample program below:

```java
public class IfElseStatementDemo {

public static void main(String[] args) {
int a = 20, b = 20;
if (a > b) {
System.out.println("a is greater than b");
} else if (a < b){
System.out.println("b is greater than a");
} else {

System.out.println("a is equal to b");

}
}
}
```

If you will try to analyze it:

Line 4 gives you the given data that the program needs to work with.

Line 5 has a condition that if *a* is greater than *b*, then it will print “a is greater than b”. If you will look at the given data, the statement is false, and that prompts the program to execute the next statement, which is else statement.

Line 7 presented another option or condition; unfortunately, it is still false.

All that’s left is to print “a is equal to b”.

The program won’t execute the statement under the if or *else-if* statement because both statements are false. However, the else statement at the bottom does not present any condition and that tells the program to print “a is equal to b”, which is actually true.

Try changing the given data in the program and see how the program responds.

## The Switch

The switch statement is also known as a case statement where you provide different options for the user and the program will execute it. The switch statement is similar to if-else statement wherein there are options presented and the program will seek the first option that proves to be true. It will execute the statement under the if-else option that returns a value true.

The switch statement is more orderly than the if-else statement. It is also easier to maintain the program if it’s coded in an orderly fashion. If you have many options to present, then you should use the switch statement.

Here is the syntax for the switch statement:

```text
switch (<non-long integral expression>) {
    case 1:

        <statement 1>

        break;

    case 2:

        <statement 2>

        break;
    case n:

        <statement n>

        break;

    default:

        <statement>
} // end of switch or case statement
```

Look at the sample program below:

```java
public class SwitchCaseStatementDemo {
public static void main(String[] args) {
    int a = 10, b = 30, c = 20;
    int response = 0;
    if (a > b && a > c) {
        response = 1;
    } else if (b > a && b > c) {
        response = 2;
    } else if (c > a && c > b){
        response = 3;
    }
    switch (response) {
    case 1:
        System.out.println("a is the biggest number");
    break;
    case 2:
        System.out.println("b is the biggest number");
    break;
20  case 3:
21      System.out.println("c is the biggest number");
22      break;
23  default:
24      System.out.println("Error encountered, try again");
25  }
26 }
27 }
```

You need to initialize the *int* response, which you need for your *switch* statement. If you remove it, your program will not work.

You can change the data that you need to work with and see the result. You can try changing the condition under each *if-else* statements and see what happens. Make sure that when you change something, the change should be consistent with the whole program. Otherwise, your program won’t work or will yield a different result.

## The Loop Statements

The loop statements are: while statement, do-while statement, and for.

### The while Statement

The while statement tells the program to continue doing the block of codes below it, while the condition or statement remains true. The program will only stop repeating or doing the instructions of the code when the statement becomes false.

This is the syntax for the while loop:

```text
while (<loop condition>)
<statements>
```

Here is the sample program:

```java
1  public class SampleWhileLoop {
2
3  public static void main(String[] args) {
int count = 1;

System.out.println("Output Numbers 1 - 10");

while (count != 11) {
    System.out.println(count++);
}
}
}
```

We need to initialize *int* count to 1. In Line 6, it only means that when count is already equal to 11, it won’t print any more. In Line 7 ‘count++’ tells the program to increment count by 1 so in the next loop it will print 2. It needs to increment count again and in the next loop it will print 3 and so on, and will only stop printing when count equals 11.

### The do-while Statement

The do-while loop or statement is similar to the while statement, except the action is given first before the actual condition for the program to check before executing the statement. This can give the program more control because it makes sure that the loop will be performed at least once.

This is the syntax for the do-while statement:

```text
do
<loop body>
while (<loop condition>);
```

Here is a sample program:

```java
1 public class SampleDoWhileStatement {
2
3 public static void main(String[] args) {
4 int sheep = 1;
5 System.out.println("Output Numbers 1 - 10");
6 do {
7 System.out.println(sheep++);
8 } while (sheep <= 10);
9 }
10 }
```

### The for Loop or Statement

The for loop is applicable for a task or program that needs to execute a certain block of codes for a certain number of times. It's like repeating the same process repeatedly as long as the condition remains true. You need to initialize the counter that will control the loop.

This is the syntax that you need to follow:

```text
for (<initialization>; <loop condition>; <increment expression>)
<loop body>
```

Here is the sample program:

```java
1 public class SampleForLoop {
2
3     public static void main(String[] args) {
4         System.out.println("Output Numbers 1 - 10");
5         for (int number = 1; number <= 10; number++) {
6             System.out.println(number);
7         }
8     }
9 }
```

Look at Line 5, you need to initialize your counter ‘number’, set the condition that number must be less than or equal to 10, and increment number by 1. The next statement prints the counter number, which is initially ‘1’.

When counter number becomes 2, it is still less than 10, and the counter increments by 1 again. The next statement will now print ‘2’.

The whole cycle will repeat until the counter number = 10. The counter will still increment by one, and the last statement will print ‘10’.

Once the counter number turns 11, it won’t satisfy the next condition that the counter number should be less than or equal to 10. The program will no longer execute the remaining statements.

Java is easy and fun to learn. Keep on advancing and discover more wonderful things that you can do with Java programming.

## Conclusion

Thank you again for downloading this book!

I hope this book was able to help you to understand the Java basics that you need to know in order to create a Java program with ease.

The next step is to keep on practicing what you have learned and learning more commands as you go along.

Finally, if you enjoyed this book, then I’d like to ask you for a favor, would you be kind enough to leave a review for this book on Amazon? It’d be greatly appreciated!

Click here to leave a review for this book on Amazon!

Also be sure to signup for my technology and programming newsletter to get your FREE books and learn more about how to program. Click Here.

Thank you and good luck!

Click Here to get step by step instructions for setting up your Wordpress site with Bluehost.

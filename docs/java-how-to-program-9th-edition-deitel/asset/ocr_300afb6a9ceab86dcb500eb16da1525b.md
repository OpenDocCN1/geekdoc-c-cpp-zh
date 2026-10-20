14.23
+ 18.67
--------
32.91

but a person adding the individual numbers as displayed would expect the sum to be 32.90. You’ve been warned!

# Error-Prevention Tip 5.5

Do not use variables of type double (or float) to perform precise monetary calculations. The imprecision of floating-point numbers can cause errors. In the exercises, you’ll learn how to use integers to perform precise monetary calculations. Java also provides class java.math.BigDecimal to perform precise monetary calculations. For more information, see download.oracle.com/javase/6/docs/api/java/math//BigDecimal.html.

# 5.5 do...while Repetition Statement

The do...while repetition statement is similar to the while statement. In the while, the program tests the loop-continuation condition at the beginning of the loop, before executing the loop’s body; if the condition is false, the body never executes. The do...while statement tests the loop-continuation condition after executing the loop’s body; therefore, the body always executes at least once. When a do...while statement terminates, execution continues with the next statement in sequence. Figure 5.7 uses a do...while (lines 10–14) to output the numbers 1–10.

```
1 // Fig. 5.7: DoWhileTest.java
2 // do...while repetition statement.
3
4 public class DoWhileTest
5 {
6 public static void main( String[] args )
7 {
8 int counter = 1; // initialize counter
9
10 do
11 {
12 System.out.printf( "%d  ", counter );
13 ++counter;
14 } while ( counter <= 10 ); // end do...while
15
16 System.out.println(); // outputs a newline
17 } // end main
18 } // end class DoWhileTest
```

1 2 3 4 5 6 7 8 9 10

Fig. 5.7 | do...while repetition statement.

Line 8 declares and initializes control variable counter. Upon entering the do...while statement, line 12 outputs counter’s value and line 13 increments counter. Then the pro-
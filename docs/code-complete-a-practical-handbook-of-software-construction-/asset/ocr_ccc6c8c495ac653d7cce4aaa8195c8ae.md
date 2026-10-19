to how complicated the expression inside the if or while is to make sure that the statement is fully tested. The easiest way to make sure that you’ve gotten all the bases covered is to calculate the number of paths through the program and then develop the minimum number of test cases that will exercise every path through the program.

You might have heard of “code coverage” testing or “logic coverage” testing. They are approaches in which you test all the paths through a program. Since they cover all paths, they’re similar to structured basis testing, but they don’t include the idea of covering all paths with a minimal set of test cases. If you use code coverage or logic coverage testing, you might create many more test cases than you would need to cover the same logic with structured basis testing.

Cross-Reference This procedure is similar to the one for measuring complexity in “How to Measure Complexity” in Section 19.6.

You can compute the minimum number of cases needed for basis testing in this straightforward way:

+   1. Start with 1 for the straight path through the routine.
+   2. Add 1 for each of the following keywords, or their equivalents: if, while, repeat, for, and, and or.
+   3. Add 1 for each case in a case statement. If the case statement doesn’t have a default case, add 1 more.

Here’s an example:

# Simple Example of Computing the Number of Paths Through a Java Program

```
Statement1;
Statement2;
if ( x < 10 ) {
  Statement3;
}
Statement4;
```

Count “1” for the routine itself.

Count “2” for the if.

In this instance, you start with one and count the if once to make a total of two. That means that you need to have at least two test cases to cover all the paths through the program. In this example, you’d need to have the following test cases:

+   - Statements controlled by if are executed (x < 10).
+   - Statements controlled by if aren’t executed (x >= 10).

The sample code needs to be a little more realistic to give you an accurate idea of how this kind of testing works. Realism in this case includes code containing defects.
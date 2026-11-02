A run of the code in Figure 7-11 is shown in Figure 7-12. Compare Figure 7-12 with the run in Figure 7-8.

Figure 7-12:
A run of the postincrement code (the code in Figure 7-11).

![](bbox=[0.25, 0.28, 0.42, 0.48])

+   - With preincrement in Figure 7-8, the second number that's displayed is 29.
+   - With postincrement in Figure 7-12, the second number that's displayed is 28.

In Figure 7-12, the number 29 doesn't show up on the screen until the end of the run, when the computer executes one last System.out.println(gumballs).

![](bbox=[0.12, 0.7, 0.22, 0.82])

Are you trying to decide between using preincrement or postincrement? Ponder no longer. Most programmers use postincrement. In a typical Java program, you often see things like gumballs++. You seldom see things like ++gumballs.

In addition to preincrement and postincrement, Java has two operators that use --. These operators are called predecrement and postdecrement.

+   - With predecrement (--gumballs), the computer subtracts 1 from the variable's value before the variable is used in the rest of the statement.
+   - With postdecrement (gumballs--), the computer subtracts 1 from the variable's value after the variable is used in the rest of the statement.

# Assignment operators

If you read the previous section — the section about operators that add 1 — you may be wondering whether you can manipulate these operators to add 2, or add 5, or add 100000. Can you write gumballs+++ and still call yourself a Java programmer? Well, you can't. If you try it, Eclipse will give you an error message:

```
Invalid argument to operation ++/--
```
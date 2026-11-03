+   3. Test for a specified condition for execution of the loop.
+   4. Incrementing the counter.

The test may be either to determine whether the loop has been repeated the specified number of times or to determine whether a particular condition has been met.

The C language provides for three loop constructs for performing loop operations. They are:

+   1. The while statement.
+   2. The do statement.
+   3. The for statement.

We shall discuss the features and applications of each of these statements in this chapter.

# 7.2 THE WHILE STATEMENT

The simplest of all the looping structures in C is the while statement. We have used while in many of our earlier programs. The basic format of the while statement is

```
while (test condition)
{
    body of the loop
}
```

The while is an entry-controlled loop statement. The test-condition is evaluated and if the condition is true, then the body of the loop is executed. After execution of the body, the test-condition is once again evaluated and if it is true, the body is executed once again. This process of repeated execution of the body continues until the test-condition finally becomes false and the control is transferred out of the loop. On exit, the program continues with the statement immediately after the body of the loop.

The body of the loop may have one or more statements. The braces are needed only if the body contains two or more statements. However, it is a good practice to use braces even if the body has only one statement.

We can rewrite the program loop discussed in Sec. 7.1 as follows:

```
sum = 0;
n = 1;
while(n <= 10)
{
    sum = sum + n * n;
    n = n+1;
}
printf("sum = %d\n", sum);
```

The body of the loop is executed 10 times for n = 1, 2, ......, 10 each time adding the square of the value of n, which is incremented inside the loop. The test condition may also be written as n < 11; the result would be the same.
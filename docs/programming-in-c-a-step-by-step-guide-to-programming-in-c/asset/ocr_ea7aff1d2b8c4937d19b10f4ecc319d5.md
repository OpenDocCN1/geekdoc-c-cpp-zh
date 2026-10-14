```
printf("%d\n", x);
x = x * 2;
}
```

(Once again, we've used braces {} to enclose the group of statements which are to be executed together as the body of the loop.)

The general syntax of a while loop is

```
while( expression )
statement(s)
```

A while loop starts out like an if statement: if the condition expressed by the expression is true, the statement is executed. However, after executing the statement, the condition is tested again, and if it's still true, the statement is executed again. (Presumably, the condition depends on some value which is changed in the body of the loop.) As long as the condition remains true, the body of the loop is executed over and over again. (If the condition is false right at the start, the body of the loop is not executed at all.) As another example, if you wanted to print a number of blank lines, with the variable n holding the number of blank lines to be printed, you might use code like this:

```
while(n > 0)
{
printf("\n");
n = n - 1;
}
```

After the loop finishes (when control “falls out" of it, due to the condition being false), n will have the value 0.

You use a while loop when you have a statement or group of statements which may have to be executed a number of times to complete their task. The controlling expression represents the condition “the loop is not done" or “there's
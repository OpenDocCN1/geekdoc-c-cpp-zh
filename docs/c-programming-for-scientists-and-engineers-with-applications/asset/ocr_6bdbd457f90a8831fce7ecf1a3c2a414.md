# 208 Control Structures

```
else if (y > z)
printf("The largest number is: %d\n", y);
```

```
else
printf("The largest number is : %d\n", z);
```

Note that even if all the numbers are the same, the correct answer will be printed by the default case.

|| Condition Consider the case where two different types of data are to be processed the same way. The following example shows the implementation of the || operator in a compound condition. This is shown in the flowchart in Figure 4.7.

![](bbox=[0.335, 0.365, 0.755, 0.706])

Figure 4.7 Flowchart of a compound condition

The code with the simple conditions is:

```
if(cond1)
{
  stmt1;
  stmt2;
}
else if(cond2)
```
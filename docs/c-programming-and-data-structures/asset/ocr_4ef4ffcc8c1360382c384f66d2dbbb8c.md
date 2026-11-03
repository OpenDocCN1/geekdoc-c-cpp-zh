```
else
    n = n + 1;
}
printf("Terms = %d Sum = %f\n", count, sum);
}
```

Output

Enter value of x:0
Terms = 2 Sum = 1.000000
Enter value of x:0.1
Terms = 5 Sum = 1.105171
Enter value of x:0.5
Terms = 7 Sum = 1.648720
Enter value of x:0.75
Terms = 8 Sum = 2.116997
Enter value of x:0.99
Terms = 9 Sum = 2.691232
Enter value of x:1
Terms = 9 Sum = 2.718279

Fig. 2.6 Illustration of if...else statement

The program uses count to count the number of terms added. The program stops when the value of the term is less than 0.0001 (ACCURACY). Note that when a term is less than ACCURACY, the value of n is set equal to 999 (a number higher than 100) and therefore the while loop terminates. The results are printed outside the while loop.

# 2.5 NESTING OF IF....ELSE STATEMENTS

When a series of decisions are involved, we may have to use more than one if...else statement in nested form as shown below:

The logic of execution is illustrated in Fig. 2.7. If the condition-1 is false, the statement-3 will be executed; otherwise it continues to perform the second test. If the condition-2 is true, the statement-1 will be evaluated; otherwise the statement-2 will be evaluated and then the control is transferred to the statement-x.

A commercial bank has introduced an incentive policy of giving bonus to all its deposit holders. The policy is as follows: A bonus of 2 per cent of the balance held on 31st December is given to every one, irrespective of their balance, and 5 per cent is given to female account holders if their balance is more than Rs. 5000. This logic can be coded as follows:

```
if (sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
    else
        bonus = 0.02 * balance;
}
```

![](bbox=[0.65, 0.93, 0.95, 1.0])
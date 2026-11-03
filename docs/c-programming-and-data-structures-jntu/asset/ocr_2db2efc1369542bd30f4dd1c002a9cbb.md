# # Decision Making and Branching 6.19

maxloan-maximum permissible loan
sancloan-loan sanctioned

The rules for sanctioning new loan are:

+   1. loan1 should be zero.
+   2. loan2 + loan3 should not be more than maxloan.

Note: use of long int type to declare variables.

```
/*
******************************
* CONDITIONAL OPERATOR
******************************/
#define MAXLOAN 50000
main()
{
long int loan1,loan2,loan3,sancloan,sum23;
printf("Enter the values of previous two loans:\n");
scanf("%ld",&loan1,&loan2);
printf("Enter the value of new loan:\n");
scanf("%ld",&loan3);
sum23 = loan2+loan3;
sancloan=(loan1>0)?0:((sum23>MAXLOAN)?0:loan3);
printf("\nPrevious loans pending: %ld %ld", loan1,loan2);
printf("Loan requested = %ld", loan3);
printf("Loan sanctioned = %ld", sancloan);
}
```

# ## Output

```
Enter the values of previous two loans:
0 20000
Enter the value of new loan:
45000
Previous loans pending:
0 20000
Loan requested = 45000
Loan sanctioned = 30000
```

```
Enter the values of previous two loans:
1000 15000
Enter the value of new loan:
25000
Previous loans pending
1000 15000
Loan requested = 25000
Loan sanctioned = 0
```

![](bbox=[0.05, 0.88, 0.95, 0.95])
# Using && and || Appropriately

Beginning programmers often use the && operator when they mean to use |, and often use || when they should use &&. Part of the problem lies in the way we use the English language. For example, your boss might request,"Display an error message when an employee's hourly pay is less than $5.65 and when an employee's hourly pay is greater than $60. Because your boss used the and in the request, you might be tempted to write a program statement like the following:

```
if(payRate < 5.65 && payRate > 60)
    WriteLine("Error in pay rate");
```

As a single variable, no payRate can ever be less than 5.65 and greater than 60 at the same time, so the output statement can execute, no matter what value payRate has. In this case, you must write the following statement to display the error message under the correct circumstances:

```
if(payRate < 5.65 || payRate > 60)
    WriteLine("Error in pay rate");
```

Similarly, your boss might request,"Output the names of employees in departments 1 and 2." Because your boss used the and in the request, you might be tempted to write the following:

```
if(department == 1 && department == 2)
    WriteLine("Name is: {0}", name);
```

However, the department can never contain both 1 and 2 at the same time, so no employee name will ever be output, no matter what the employee is in.

The correct statement is:

```
if(department == 1 || department == 2)
    WriteLine("Name is: {0}", name);
```

# Using the Operator Correctly

Whenever you use negatives, it is easy to make logical mistakes. For example, suppose your boss says,"Make sure that if the sales is not A or B, the customer gets a 10 percent discount." You might be tempted to code the following:

```
if(salesCode != 'A' && salesCode != 'B')
    discount = 0.10;
```

However, this logic will result in every customer receiving the 10 percent discount because every salesCode is either not A or B. For example, if salesCode is A, then it is not B. The expression salesCode != 'A' && salesCode != 'B' is always true. The correct statement is one of the following:

```
if(salesCode != 'A' && salesCode != 'B')
    discount = 0.10;
```
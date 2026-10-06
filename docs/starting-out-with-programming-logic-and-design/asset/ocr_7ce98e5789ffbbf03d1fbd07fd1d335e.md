# Chapter 4 Decision Structures and Boolean Logic

Enter the number of years on your current job.
[Enter]
You do not qualify for this loan.

# Program Output (with Input Shown in Bold)
nEnter your annual salary.
3500[Enter]
Enterter the number of years on your current job.
[Enter]
You qualify for the loan.

The If-Then-Else statement in lines 14 through 18 tests the compound subexpressions are true, the compound salary = 30000 AND yearsJob >= 2. If both pound expression is true and the message "You qualify for the loan" is displayed. If either of the subexpressions is false, the compound expression is false and the message "You do not qualify for this loan" is displayed.

> NOTE: A careful observer will realize that Program 4-9 is similar to Program 4-5, but it is not equal. If the user does not qualify for the loan, Program 4-9 displays only the message "You do not qualify for this loan," whereas Program 4-5 displays one of two possible messages explaining why the user did not qualify.

# Another Loan Qualifier Program

Suppose the bank is losing customers to a competing bank that isn't as strict about whom it lends. In response, the bank decides to change its loan requirements. Now, customers have to meet only one of the previous conditions, not both. Program 4-10 uses pseudocode for the loan qualifier program. The compound expression is tested by the If-Then-Else statement in line 14 uses the OR operator.

# Program 4-10

```
// Declare variables
Declare Real salary, yearsOnJob

// Get the annual salary.
Display "Enter your annual salary."
Input salary

// Get the number of years on the current job.
Display "Enter the number of years on your"
Display "current job."
Input yearsOnJob

// Determine whether the user qualifies.
If salary >= 30000 OR yearsOnJob >= 2 Then
	Display "You qualify for the loan."
Else
	Display "You do not qualify for this loan."
End If
```
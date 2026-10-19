**Document unclear dependencies with comments**  Try first to write code without order dependencies. Try second to write code that makes dependencies obvious. If you’re still concerned that an order dependency isn’t explicit enough, document it. Documenting unclear dependencies is one aspect of documenting coding assumptions, which is critical to writing maintainable, modifiable code. In the Visual Basic example, comments along these lines would be helpful:

```
**Visual Basic Example of Statements in Which Order Dependencies Are Hidden but Clarified with Comments**

```text
' Compute expense data. Each of the routines accesses the
' member data expenseData. DisplayExpenseSummary
' should be called last because it depends on data calculated
' by the other routines.
InitializeExpenseData
ComputeMarketingExpense
ComputeSalesExpense
ComputeTravelExpense
ComputePersonnelExpense
DisplayExpenseSummary
```
```

This code doesn’t use the techniques for making order dependencies obvious. It’s better to rely on such techniques rather than on comments, but if you’re maintaining tightly controlled code or you can’t improve the code itself for some other reason, use documentation to compensate for code weaknesses.

**Check for dependencies with assertions or error-handling code**  If the code is critical enough, you might use status variables and error-handling code or assertions to document critical sequential dependencies. For example, in the class’s constructor, you might initialize a class member variable `isExpenseDataInitialized` to `false`. Then in `InitializeExpenseData()`, you can set `isExpenseDataInitialized` to `true`. Each function that depends on `expenseData` being initialized can then check whether `isExpenseDataInitialized` has been set to true before performing additional operations on `expenseData`. Depending on how extensive the dependencies are, you might also need variables like `isMarketingExpenseComputed`, `isSalesExpenseComputed`, and so on.

This technique creates new variables, new initialization code, and new error-checking code, all of which create additional possibilities for error. The benefits of this technique should be weighed against the additional complexity and increased chance of secondary errors that this technique creates.
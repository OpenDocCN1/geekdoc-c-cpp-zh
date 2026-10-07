```
public static bool ValidateExpenseItem(ExpenseItem expenseItem) =>
    expenseItem switch
{
        // Note: A property pattern checks that the input value is
        not null
            // Expanded Property Pattern
            ItemName.Length > 0, Employee.Role: "Admin" => true,
            #pragma warning disable IDE0170 // Property pattern can be
        simplified
            // Property Pattern
            ItemName: { Length > 0 }, Employee: { Role: "Manager" },
            ExpenseDate: DateTime date
            #pragma warning restore IDE0170 // Property pattern can be
            when date >= DateTime.Now.AddDays(-30) => true,
            { ItemName.Length > 0, Employee.Name.Length > 0,
            CostAmount: < 1000, ExpenseDate: DateTime date
            when date >= DateTime.Now.AddDays(-30) => true,
            { } => false, // This not null check can be eliminated.
            => false
    };
```

The first important thing to note about all property matches is that they will match only when the input operand is not null. This is why, for example, a match expression of { }, an empty property match, matches whenever the input operand is not null. (In Listing 7.30, the { } match expression is redundant as the default match expression at the end of the switch will catch both null and remaining non-null input operands that fall through anyway). While it works as a not null check, simply specifying null (C# 9.0) is preferred as the syntax is clearer.

In Listing 7.30, the first match expressions within the switch expression starts with ItemName.Length > 0, requiring that ItemName.Length is greater than 0. Implied in the expression is that ItemName is also not null. In fact, the initial null check is implicit, the compiler disallows the null conditional in the property expression (ItemName?.Length).

In Listing 7.30, the first match expression also requires that Employee.Role is set to "Admin". And, if these two match expressions match, the switch returns true, indicating ExpenseItem is valid. The complete match
# Chapter 7: Inheritance

expression uses an expanded dot notation that accesses subproperties (Length and Role).

The second match expression for Listing 7.30, { ItemName: { Length: > }, Employee: {Role: "Manager"}, ExpenseDate: DateTime }, is also a property match expression (rather than an expanded property expression) but with a slightly different syntax. The property match expression was introduced in C# 7.0 and is still supported, albeit with a warning, because the expanded syntax is simpler and preferred in all cases.

This second match expression includes a property match for ExpenseDate for which it declares a variable, date. While date is still used as part of the switch filter, it appears in a when clause rather than the match expression.

# When Clause

For all forms of constant and relational match expressions, it is necessary to use a constant. This, however, can be restrictive given that frequently the comparative operand is not known at compiler time. To avoid the restriction, C# 7.0 includes a when clause into which you can add any conditional expression (an expression that returns a Boolean).

The code in Listing 7.30 declares a DateTime variable to check that the ExpenseItem.ExpenseDate is not older than 30 days. However, because age is dependent on the current date and time, the value isn't constant, and we can't use a match expression. Instead, the code uses a when clause following the match expression where the date value is compared to DateTime.Now.AddDays(-30). When the clause provides a catchall location for (optionally) more complex conditionals without the restriction of using only constants.

The addition of when clauses is the core reason why C# 7.0 allowed match expressions to no longer be mutually exclusive. When a clause, it is no longer possible to determine at compile time to evaluate the full case logic and exclusivity. As a reminder, be careful of the order that each case appears within a switch expression to avoid having earlier cases catch conditions meant for later cases.

![](bbox=[0.025, 0.793, 0.107, 0.821])
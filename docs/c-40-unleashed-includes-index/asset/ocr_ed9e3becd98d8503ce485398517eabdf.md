The sky (of expressions) is the limit. Just recall how the previous query expressions translate into method calls with lambda expressions for the argument as you see where this flexibility comes from. For example:

```
// Calling a method and using a closure over a captured local variable.
DateTime from = DateTime.Now - TimeSpan.FromDays(100);
var topSellers = products
    .OrderByDescending(p => p.GetNumberOfSalesSince(from));
```

Figure 19.20 illustrates this query's execution, starting with key selection at the top.

![](bbox=[0.05, 0.47, 0.9, 0.88])

# FIGURE 19.20 Execution of an ordering.

# Secondary and n-ary Orderings

Use of an orderby clause with a single key selector expression creates just a primary ordering. Quite often, one wants to establish secondary and n-ary orderings on top of this, as illustrated in Figure 19.21.
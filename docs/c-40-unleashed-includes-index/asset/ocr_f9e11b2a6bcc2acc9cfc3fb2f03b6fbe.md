```
```csharp
var priceGroups = new Dictionary<int, List<Product>>();
foreach (var product in products) {
    int group = 10 * (int)(product.Price / 10);

    List<Product> productsInGroup;
    if (!priceGroups.TryGetValue(group, out productsInGroup))
        priceGroups[group] = productsInGroup = new List<Product>();

    productsInGroup.Add(product);
}
```
```

This code clearly doesn't reveal the grouping characteristic anymore in an obvious way. Moreover, we've only been showing one query operation at a time. "Just" adding filtering to the preceding grouping code, maybe followed by sorting on the key and retaining only the first 10 groups, clearly isn't the simplest thing to do. Knowing how to do the query operations each by themselves doesn't suffice to mix them together. In other words, composability is lacking.

Key disadvantages include the following:

+   - Imperative nature of the code, not revealing the intent of the user clearly
+   - Lots of manual plumbing needed for a seemingly simple task
+   - Not composable out of simple query operator primitives

# ## Relational Databases

Relational databases serve as one of the most commonly used data sources in enterprise applications. Querying them requires the use of a different language altogether, such as the Structured Query Language (SQL). Let's assume the same data as shown earlier exists in a relational database (for example, stored in SQL Server). Figure 19.1 illustrates what the records in a Products table might look like. Notice the presence of foreign keys in other tables (for example, to *relate* a product to a category).

![](bbox=[0.048, 0.727, 0.683, 0.912])

FIGURE 19.1 A table in a relational database.
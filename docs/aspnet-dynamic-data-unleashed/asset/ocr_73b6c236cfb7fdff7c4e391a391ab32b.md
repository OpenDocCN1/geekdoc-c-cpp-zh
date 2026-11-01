filtering operators, such as “contains” or “starts with” because they are only applicable to strings. Although this is not done in the source code accompanying this book, real-world applications typically have a bigger set of filter templates, implementing additional type-specific filtering operators for numbers and dates in filter templates called Decimal.ascx, Integer.ascx, and DateTime.ascx. This removes the requirement for the Text filter template to support multiple primitive data types and allows you to implement string-specific filtering operators in this control instead.

![](bbox=[0.12, 0.3, 0.88, 0.68])

FIGURE 13.2 Unleashed filter lookup algorithm.

# Extending the MetaTable Class

The second part of the algorithm that determines which entity properties will have filter templates generated dynamically is implemented in the MetaTable class, which defines a virtual method called GetFilteredColumns that returns an IEnumerable of MetaColumn objects.

```
public class MetaTable
{
    public virtual IEnumerable<MetaColumn> GetFilteredColumns();
}
```

The GetFilteredColumns method is called by the built-in QueryableFilterRepeater control (and by the UnleashedFilterRepeater) to get a list of properties that can be filtered. For each MetaColumn object it returns, the repeater creates a DynamicFilter (or the UnleashedFilter) control, which in turn calls the CreateFilterControl method of the FilterFactory just implemented to locate and create the filter templates.

The default implementation of the GetFilteredColumns method in the MetaTable class assumes that only properties of Boolean, ForeignKey, and Enumeration types can be filtered. Even though the UnleashedFilterFactory already supports other property types,
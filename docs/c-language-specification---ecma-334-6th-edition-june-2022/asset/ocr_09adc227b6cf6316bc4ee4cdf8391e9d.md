then the same documentation is output as if the source code contained:

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

# D.3.7 <list>

This tag is used to create a list or table of items. It can contain a <listheader> block to define the heading row of either a table or definition list. (When defining a table, only an entry for term in the heading need be supplied.)

Each item in the list is specified with an <item> block. When creating a definition list, both term and description must be specified. However, for a table, bulleted list, or numbered list, only description need be specified.

# Syntax:

```
<list type="bullet" | "number" | "table">
  <listheader>
    <term>term</term>
    <description>description</description>
  </listheader>
  <item>
    <term>term</term>
    <description>description</description>
  </item>
  ...
  <item>
    <term>term</term>
    <description>description</description>
  </item>
</list>
```

where

+   - term is the term to define, whose definition is in description.
+   - description is either an item in a bullet or numbered list, or the definition of a term.

# Example:

```
public class MyClass
{
    /// <summary>Here is an example of a bulleted list:
    /// <list type="bullet">
    /// <item>
    /// <description>Item 1.</description>
    /// </item>
    /// <item>
    /// <description>Item 2.</description>
    /// </item>
    /// </list>
    /// </summary>
    public static void Main()
    {
        // ...
    }
```
```
Converter={StaticResource boolToVisiblity}" />
</Grid>
```

When you start the application, you can see all available cultures in the tree view, and selecting a culture lists its characteristics, as shown in Figure 28.6.

![](bbox=[0.105, 0.164, 0.895, 0.397])

# Figure 28.6

# Sorting

The sample SortingDemo makes use of the following dependencies and namespaces:

# Dependencies

```
NETStandard.Library
```

```
System.Collections.NonGeneric
```

# Namespaces

```
System
```

```
System.Collections
```

```
System.Collections.Generic
```

```
System.Globalization
```

```
static System.Console
```

Sorting strings varies according to the culture. The algorithms that compare strings for sorting by default are culture-specific. For example, in Finnish the characters V and W are treated the same. To demonstrate this behavior with a Finnish sort, the following code creates a small sample console application in which some U.S. states are stored unsorted inside an array.

The method DisplayNames shown here is used to display all elements of an array or a collection on the console (code file SortingDemo/Program.cs):
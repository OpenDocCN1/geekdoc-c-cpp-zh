![](bbox=[0.23, 0.11, 0.68, 0.24])

![](bbox=[0.81, 0.11, 0.93, 0.21])

# LISTING 20.9 Accessing a Single Attribute at Runtime

```
public class Program
{
    public static void Main(string[] args)
    {
        WorkItemAttribute attribute =
            Attribute.GetCustomAttribute(typeof(Test), typeof(WorkItemAttribute))
            as WorkItemAttribute;

        if (attribute != null)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId, attribute.Comment);
        }
    }
}
```

Attribute.GetCustomAttribute returns a single attribute. If multiple attributes of the same type defined on the code element exist or you need to work with multiple attributes of different types, you can use the Attribute.GetCustomAttributes method to return an array of custom attributes. You can then enumerate the resulting array, examining and extracting information from the array elements, as shown in Listing 20.10.

# LISTING 20.10 Accessing Multiple Attributes at Runtime

```
public class Program
{
    public static void Main(string[] args)
    {
        var workItems = from attribute in
                        Attribute.GetCustomAttributes(typeof(Test)).
                        OfType<WorkItemAttribute>()
                        select attribute;

        foreach (var attribute in workItems)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId,
                              attribute.Comment);
        }
    }
}
```
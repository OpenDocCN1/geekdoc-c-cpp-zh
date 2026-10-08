```
public int WorkItemId
{
    get
    {
        return this.workItemId;
    }
}

public string Comment
{
    get;
    set;
}
}
```

The custom attribute has a single public constructor whose parameters form the attributes positional parameters. Any public read-write fields or properties—in this case, the Comment property—become named parameters. Finally, the AttributeUsage attribute indicates that the WorkItem attribute is valid on any declaration, that it can be applied more than once, and that it is not automatically applied to derived types.

You can then use this attribute as shown in Listing 20.8.

# **LISTING 20.8** Applying a Custom Attribute

```
[WorkItem(1234,
        Comment = "Created a test class to show how attributes can be used.")]
public class Test
{
    [WorkItem(5678, Comment = "Changed property to use auto-property syntax.")]
    public int P
    {
        get;
        set;
    }
}
```

# **Accessing Attributes at Runtime**

Adding metadata to your application through attributes doesn't do much if you can't access that information at runtime. The .NET Framework provides access to the runtime type information, including metadata provided by attributes, through a process called reflection. Because attributes provide metadata, the code associated with an attribute is not actually executed until the attributes are queried.

Retrieving custom attributes is easy using the Attribute.GetCustomAttribute method. Listing 20.9 shows an example of accessing the custom attribute defined in Listing 20.7 and the simple class defined in Listing 20.8 at runtime. Figure 20.1 shows the output of Listing 20.9.
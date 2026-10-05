```
set { ... }
}
...
}
```

If you implement the interface indexer in a class, you can declare the indexer implementations as virtual. This allows further derived classes to override the get and set accessors, such as in the following:

Click here to view code image

```
class RawInt : IRawInt
{
    public virtual bool this { int index }
    {
        get { ... }
        set { ... }
    }
}
```

You can also choose to implement an indexer by using the explicit interface implementation syntax covered in Chapter 13, "Creating interfaces and defining abstract classes." An explicit implementation of an indexer is nonpublic and nonvirtual (and so cannot be overridden), as shown in this example:

Click here to view code image

```
struct RawInt : IRawInt
{
    bool IRawInt.this { int index }
    {
        get { ... }
        set { ... }
    }
...}
```

# Using indexers in a Windows application
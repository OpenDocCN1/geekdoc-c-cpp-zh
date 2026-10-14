```
set { this.data[i] = value; }
}
```

The following code uses the indexer in a similar manner to the property shown earlier:

```
Wrapper wrap = new Wrapper();
...
int[] myData = new int[2];
myData[0] = wrap[0];
myData[1] = wrap[1];
myData[0]++;
myData[1]++;
```

This time, incrementing the values in the myData array has no effect on the original array in the Wrapper object. If you really want to modify the data in the Wrapper object, you must write statements such as this:

```
wrap[0]++;
```

This is much clearer and safer!

# Indexers in interfaces

You can declare indexers in an interface. To do this, specify the get keyword, the set keyword, or both, but replace the body of the get or set accessor with a semicolon. Any class or structure that implements the interface must implement the indexer accessors declared in the interface, as demonstrated here:

Click here to view code image

```
interface IRawInt
{
    bool this [ int index ] { get; set; }
}

struct RawInt : IRawInt
{
    ...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
```

If you implement the interface indexer in a class, you can declare the indexer implementations as virtual. This allows further derived classes to override the get and set accessors, such as in the following:

Click here to view code image
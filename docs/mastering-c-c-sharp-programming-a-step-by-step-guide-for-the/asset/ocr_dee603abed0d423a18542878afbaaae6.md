```
{
    // I'm not quite sure what to do with the two indices we have here.
    // I think I might just throw an exception. If making an indexer with multiple
    // indices make sense, you would write some code right here that would do
    // something intelligent with it.
    throw new Exception();
}
set
{
    // I'm not quite sure what to do with the two indices we have here.
    // I think I might just throw an exception. If making an indexer with multiple
    // indices make sense, you would write some code right here that would do
    // something intelligent with it.
    throw new Exception();
}
}
```

In this case, it does make perfect sense and it shows you that it can be done; if you can use it, it’s easy enough to make it happen.

# Quick Primer

+   - Indexers are a way of overloading the indexing [ and ] operator for classes.
+   - Defining an indexer is a lot like a combination of a property and
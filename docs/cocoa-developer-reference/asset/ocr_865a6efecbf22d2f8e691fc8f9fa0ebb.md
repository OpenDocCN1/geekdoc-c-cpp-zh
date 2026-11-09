# ### Performance considerations

Fast enumeration is fast. It runs slightly faster than a for-next loop or an enumerator object. Cocoa's core is optimized for object processing, so data collection enumeration can be as fast as C array indexing. Generally, you can use fast enumeration without performance worries.

# ### Enumerating mutable collections

Don't enumerate a mutable collection while it's being modified. If the data in the collection changes, the enumerator raises an exception.

The safe way to enumerate mutable objects is to copy them to a temporary read-only object, and then run the enumeration on the read-only data. Enumerators aren't suitable for conditional editing.

```
```
//Don't do this!
for (id anItem in mutableCollection) {
    if ([anItem isEqual: aTestItem]) {
        //code to replace anItem or delete it from the collection
    }
}
```
```

# ### Counting items

All the data collection objects implement the count method, which returns an integer with the number of items; for example:

```
```
int items = [aDictionary count];
```
```

# ## Archiving and de-archiving collection objects

All the collection objects implement direct disk access. You can save and load data directly to and from disk with an arbitrary filename by calling a disk access method on a collection object. For example, to save data from an array, use

```
```
[anArray writeToFile: aFilePath atomically: YES];
```
```

You can reload the data with

```
```
anArray = [NSArray arrayWithContentsOfFile: aFilePath];
```
```

You don't need to create a file manager object. These methods handle low-level disk access for you.

# **CROSS-REF**

For information about creating and using file paths and URLs, see Chapter 10.
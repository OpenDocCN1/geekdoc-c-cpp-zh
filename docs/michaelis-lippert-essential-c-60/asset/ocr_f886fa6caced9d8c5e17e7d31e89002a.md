be an int. In fact, the index can take multiple parameters and can even be overloaded. This example uses an enum to reduce the likelihood that callers will supply an index for a nonexistent item.

The CIL code that the C# compiler creates from an index operator is a special property called Item that takes an argument. Properties that accept arguments cannot be created explicitly in C#, so the Item property is unique in this aspect. Any additional member with the identifier Item, even if it has an entirely different signature, will conflict with the compiler-created member, so it will not be allowed.

# ADVANCED TOPIC

# Assigning the Indexer Property Name Using IndexerName

As indicated earlier, the CIL property name for an indexer defaults to Item. Using the IndexerNameAttribute, you can specify a different name, however. Listing 16.10, for example, changes the name to "Entry".

# LISTING 16.10: Changing the Indexer's Default Name

```
[System.Runtime.CompilerServices.IndexerName("Entry")]
public T this[params PairItem[] branches]
{
    // ...
}
```

This makes no difference to C# callers of the index, but it specifies the name for languages that do not support indexers directly.

This attribute is merely an instruction to the compiler to use a different name for the indexer; the attribute is not actually emitted into metadata by the compiler, so it is not available via reflection.

# ADVANCED TOPIC

# Defining an Index Operator with Variable Parameters

An index operator can also take a variable parameter list. For example, Listing 16.11 defines an index operator for BinaryTree<T>, discussed in Chapter 11 (and again in the next section).
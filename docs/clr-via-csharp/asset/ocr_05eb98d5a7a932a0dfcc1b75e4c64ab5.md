# TABLE 12-1 Generic Collection Classes from Wintellect's Power Collections Library

| Collection Class | Description |
|---|---|
| **BigList<T>** | Collection of ordered T objects. Very efficient when working with more than 100 items. |
| **Bag<T>** | Collection of unordered T objects. The collection is hashed, and duplicates are allowed. |
| **OrderedBag<T>** | Collection of ordered T objects. Duplicates are allowed. |
| **Set<T>** | Collection of unordered T items. Duplicates are not allowed. |
| **OrderedSet<T>** | Collection of ordered T items. Duplicates are not allowed. |
| **Deque<T>** | Double-ended queue. Similar to a list but more efficient for adding/removing items at the beginning than a list. |
| **OrderedDictionary<TKey,TValue>** | Dictionary in which keys are ordered, and each can have one value. |
| **MultiDictionary<TKey,TValue>** | Dictionary in which a key can have multiple values. Keys are hashed, duplicates are allowed, and items are unordered. |
| **OrderedMultiDictionary<TKey,TValue>** | Dictionary in which keys are ordered, and each can have multiple values (also maintained in sorted order). Duplicate keys are allowed. |

# ## Generics Infrastructure

Generics were added to version 2.0 of the CLR, and it was a major task that required many people working for quite some time. Specifically, to make generics work, Microsoft had to do the following:

+   - Create new Intermediate Language (IL) instructions that are aware of type arguments.
+   - Modify the format of existing metadata tables so that type names and methods with generic parameters could be expressed.
+   - Modify the various programming languages (C#, Microsoft Visual Basic .NET, etc.) to support the new syntax, allowing developers to define and reference generic types and methods.
+   - Modify the compilers to emit the new IL instructions and the modified metadata format.
+   - Modify the just-in-time (JIT) compiler to process the new type-argument-aware IL instructions that produce the correct native code.
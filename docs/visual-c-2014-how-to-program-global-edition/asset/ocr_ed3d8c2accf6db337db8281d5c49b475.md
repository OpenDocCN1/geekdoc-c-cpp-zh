Summary 923

# Section 21.4.2 Using the SortedDictionary Collection

+   - Generic class SortedDictionary does not use a hash table, but instead stores its key–value pairs in a binary search tree.
- Generic class SortedDictionary takes two type arguments—the first specifies the type of key and the second type of value.
- Method ContainsKey determines whether a key is in a dictionary.
- SortedDictionary method Add creates a new entry in the dictionary, with the first argument as the key and the second value.
- SortedDictionary's indexer is used to get or set a key's corresponding value.
- SortedDictionary property Keys gets an ICollection<T> that contains all keys.
- If you use a foreach statement with SortedDictionary, the iteration variable is KeyValuePair, which has properties Key and Value for retrieving the current pair's key and value.
- Invoking the getter of a SortedDictionary indexer with a key that does not exist in the collection causes a KeyNotFoundException.

# Section 21.5 GenericList Collection

+   - The LinkedList class is a doubly linked list–we can navigate the list backwards and forwards nodes of generic class LinkedListNode.
- Each node contains property Value and read-only properties Previous and Next.
- The LinkedList class's enumerator loops over the values of the nodes, not the themselves.
- One LinkedListNode cannot be a member of more than one LinkedList. Any attempt to add a node from one LinkedList to another generates an InvalidOperationException.
- Method finds a linear search on the list and returns the first node that contains a value equal to the passed argument.
- Method Remove deletes a node from a LinkedList.

# Section 21.6 C# Null Conditional Operator ?[]

+   - C# also provides a null-conditional operator, ?, for arrays and collections that support the [] indexing operator.
- The ? operator determines whether the array or collection is null before accessing an element.

# Section 21.7 C# Dictionary Initializers and Collection Initializers

+   - C#'s index initializer syntax allows you to initialize a Dictionary's key–value pairs as in

```
var variableName = new Dictionary<TypeOfKey, TypeOfValues>{
    [key1] = value1,
    [key2] = value2,
    [key3] = value3
};
```

+   - As of C# 6, the compiler also supports collection initializers for any collection that has an Add extension method.

# Section 21.8 Delegates

+   - A delegate is an object that holds a reference to a method.
- Via delegates, you can assign methods to variables, and pass methods to and from other methods. You also can call methods through variables of delegate types.
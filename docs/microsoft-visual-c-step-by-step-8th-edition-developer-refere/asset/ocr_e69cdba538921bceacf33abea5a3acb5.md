```
Popping items from the stack:
2 has been popped off the stack
7 has been popped off the stack
3 has been popped off the stack
9 has been popped off the stack
```

# The Dictionary<TKey, TValue> collection class

The array and List<T> types provide a way to map an integer index to an element. You specify an integer index within square brackets (for example, [4]), and you get back the element at index 4 (which is actually the fifth element). However, sometimes you might want to implement a mapping in which the type from which you map is not an int but some other type, such as string, double, or Time. In other languages, this is often called an associative array. The Dictionary<TKey, TValue> class implements this functionality by internally maintaining two arrays, one for the keys from which you’re mapping and one for the values to which you’re mapping. When you insert a key/value pair into a Dictionary<TKey, TValue> collection, it automatically tracks which key belongs to which value and makes it possible for you to retrieve the value that is associated with a specified key quickly and easily. The design of the Dictionary<TKey, TValue> class has some important consequences:

+   - A Dictionary<TKey, TValue> collection cannot contain duplicate keys. If you call the Add method to add a key that is already present in the keys array, you’ll get an exception. You can, however, use the square brackets notation to add a key/value pair (as shown in the following example) without danger of an exception, even if the key has already been added; any existing value with the same key will be overwritten by the new value. You can test whether a Dictionary<TKey, TValue> collection already contains a particular key by using the ContainsKey method.
+   - Internally, a Dictionary<TKey, TValue> collection is a sparse data structure that operates most efficiently when it has plenty of memory with which to work. The size of a Dictionary<TKey, TValue> collection in memory can grow quite quickly as you insert more elements.
+   - When you use a foreach statement to iterate through a Dictionary<TKey, TValue> collection, you get back a KeyValuePair<TKey, TValue> item. This is a structure that contains a copy of the key and value elements of an item in the Dictionary<TKey, TValue> collection, and you can access each element through the Key property and the Value property. These elements are read-only; you cannot use them to modify the data in the Dictionary<TKey, TValue> collection.

Here is an example that associates the ages of members of my family with their names and then prints the information:
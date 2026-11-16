![](bbox=[0.09, 0.05, 0.2, 0.21])

# PUT ON YOUR THINKING HAT

Below is a list of the generic set types you're most likely to use. They're all defined in the System.Collections.Generic namespace. Can you connect each generic set type to its description? (You can, always, use the Object Browser and MoDN to help.)

| Type | Description |
| :--- | :--- |
| Dictionary<T> | The elements in this set type know about the ones that precede and follow them. |
| HashSet<T> | This type allows random access like an array, but stores elements in order. |
| LinkedList<T> | This type allows elements to be accessed in LIFO order. |
| List<T> | This set type is roughly equivalent to the non-generic ArrayList. |
| Queue<T> | The elements in this set type are accessed in FIFO order. |
| SortedDictionary<T> | This type keeps key/value pairs in order. |
| SortedList<T> | This type is like a Dictionary, but the Add() method takes just the value and calls GetHashCode() to generate the key. |
| SortedSet<T> | This type is like a SortedDictionary, but you have to provide a custom routine to compare the keys. |
| Stack<T> | This type allows elements to be retrieved by their key value. |
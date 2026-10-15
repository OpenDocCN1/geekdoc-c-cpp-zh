+   - The Dictionary<TKey, TValue> class
+   - The SortedDictionary<TKey, TValue> class
+   - The Stack<T> class
+   - The Queue<T> class
+   - The HashSet<T> class

Let's explore these classes in detail.

# The List<T> Class

The List<T> class is similar to a generic equivalent of the ArrayList class. The List<T> class provides an easy-to-use substitute for arrays. It provides various methods, such as Sort, Reverse, and Find to sort the list members, arrange the list members in reverse order, and search a member in the list. The class hierarchy of the List<T> class is given as follows:
System.Object
System.Collections.Generic.List<T>

Table 32.13 lists the important properties of the List<T> class:

Table 32.13: Noteworthy Properties of the List<T> Class
| Property | Description |
|---|---|
| Capacity | Retrieves or sets the number of elements that the List<T> object can hold without resizing |
| Count | Retrieves the number of items present in the List<T> object |
| Item | Retrieves or sets an element at the specified index. |

Table 32.14 lists the important methods of the List<T> class:

Table 32.14: Noteworthy Methods of the List<T> Class
| Method | Description |
|---|---|
| Add() | Adds an object at the end of the List<T> object |
| AddRange() | Adds the items of a specified collection at the end of the List<T> object |
| AsReadOnly() | Allows you to read the values of the objects stored in the List<T> object |
| BinarySearch() | Uses a binary search algorithm to locate a specific element in the sorted List<T> object |
| Clear() | Removes all items from the List<T> object |
| Contains() | Ascertains whether or not an element is in the List<T> object |
| ConvertAll<TOutput> | Converts the items in the current List<T> object into another type and returns a list containing the converted items |
| CopyTo() | Copies the List<T> object or a portion of it to a one-dimensional array |
| Exists() | Ascertains whether or not the List<T> object contains items that match the conditions defined by a specified criteria |
| Find() | Searches an item that matches the conditions defined by a specified criteria |
| FindAll() | Gets all the items that match the conditions defined by a specified predicate |
| FindIndex() | Searches an item that matches the conditions defined by a specified predicate, and returns the zero-based index of the first occurrence within the List<T> object or a portion of it |
| FindLast() | Searches for an item that matches the conditions defined by a specified predicate, and returns the last occurrence within the entire List<T> object |
| FindLastIndex() | Searches an item that matches the conditions defined by a specified predicate, and returns the zero-based index of the last occurrence within the List<T> object or a portion of it |
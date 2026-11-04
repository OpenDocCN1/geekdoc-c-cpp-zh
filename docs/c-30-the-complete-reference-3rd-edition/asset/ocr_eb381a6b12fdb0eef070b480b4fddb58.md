Because ICollection inherits IEnumerable, it also includes the sole method defined by IEnumerable: GetEnumerator(), which is shown here:

```
IEnumerator GetEnumerator()
```

It returns the enumerator for the collection.

Because ICollection inherits IEnumerable, three extension methods are defined for it. They are AsQueryable(), Cast(), and OfType(). AsQueryable() is declared in System.Linq.Queryable. Both Cast() and OfType() are declared in System.Linq.Enumerable. These methods are designed primarily to support LINQ, but may be useful in other contexts.

# The IList Interface

The IList interface declares the behavior of a non-generic collection that allows elements to be accessed via a zero-based index. It inherits ICollection and IEnumerable. In addition to the methods defined by ICollection and IEnumerable, IList defines several of its own. These are summarized in Table 24-2. Several of these methods imply the modification of a collection. If the collection is read-only or of fixed size, then these methods will throw a NotSupportedException.

Objects are added to an IList collection by calling Add(). Notice that Add() takes an argument of type object. Since object is a base class for all types, any type of object can be stored in a non-generic collection. This includes the value types, because boxing and unboxing will automatically take place.

You can remove an element using Remove() or RemoveAt(). Remove() removes the specified object. RemoveAt() removes the object at a specified index. To empty the collection, call Clear().

| Method | Description |
|---|---|
| int Add(object obj) | Adds obj into the invoking collection. Returns the index at which the object is stored. |
| void Clear() | Deletes all elements from the invoking collection. |
| bool Contains(object obj) | Returns true if the invoking collection contains obj. Returns false if obj is not in the collection. |
| int IndexOf(object obj) | Returns the index of obj if obj is contained within the invoking collection. If obj is not found, -1 is returned. |
| void Insert(int idx, object obj) | Inserts obj at the index specified by idx. Elements at and below idx are moved down to make room for obj. |
| void Remove(object obj) | Removes the first occurrence of obj from the invoking collection. Elements at and below the removed element are moved up to close the gap. |
| void RemoveAt(int idx) | Removes the object at the index specified by idx from the invoking collection. Elements at and below idx are moved up to close the gap. |
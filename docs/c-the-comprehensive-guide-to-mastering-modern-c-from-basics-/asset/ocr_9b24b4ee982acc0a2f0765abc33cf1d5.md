the normal comparisons that set uses internally, and the search for find(Hobit{"Frodo", "Baggins"}), the first operator() is defined, which takes two Hobbit arguments. For the search for "Gangee", the other two overloads are there, which take a Hobbit and a string. However, with the line

```
using is_transparent = std::true_type;
```

it should also be indicated that these overloads can be used for search functions. Thus a string can be used directly for the search, and no entire Hobbit is created.

Note in this way you can only search if the alternative comparison functions do not imply a different order than the main comparison operator. You cannot expect the set to be kept sorted in one order, but then search with a comparison operator that would sort differently. This is what is meant by an equivalent comparison function.

# Deleting

For deletion, you have erase and clear available. With extract, you remove an element, which you usually transfer to another set with insert:

+   * Deleting all elements
You delete all elements with the clear() method.

+   * Deleting a single element
If you pass an iterator to the erase method, the element at that position will be deleted. Alternatively, you can also specify an element as a parameter, which will be deleted if it exists. Both log n time. The return value is the number of deleted elements.

+   * Transferring an element
With extract, you remove a single element from the set. The return value is a "handle" for the removed node, which you can
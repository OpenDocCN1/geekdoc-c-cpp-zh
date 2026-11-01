# Hint

*Syntactic sugar is a nicer, alternative syntax. It replaces harsh syntax with something that's a bit easier to swallow. As an example, instead of writing the code (*myIterator).size(), I can use the syntactic sugar provided by the -> operator and write myIterator->size().*

# Using the insert() Vector Member Function

Next I add a new item to the hero's inventory. This time, though, I don't add the item to the end of the sequence; instead, I insert it at the beginning.

```
inventory.insert(inventory.begin(), "crossbow");
```

One form of the insert() member function inserts a new element into a vector just before the element referred to by a given iterator. You supply two arguments to this version of insert()—the first is an iterator, and the second is the element to be inserted. In this case, I inserted "crossbow" into inventory just before the first element. As a result, all of the other elements will move down by one. This version of the insert() member function returns an iterator that references the newly inserted element. In this case, I don't assign the returned iterator to a variable.

# Trap

*Calling the insert() member function on a vector invalidates all of the iterators that reference elements after the insertion point because all of the elements after the insertion point are shifted down by one.*

Next I show the contents of the vector to prove the insertion worked.

# Using the erase() Vector Member Function

Next I remove an item from the hero's inventory. However, this time I don't remove the item at the end of the sequence; instead, I remove one from the middle.

```
inventory.erase(inventory.begin() + 2);
```

One form of the erase() member function removes an element from a vector. You supply one argument to this version of erase()—the iterator that references the element you want to remove. In this case, I passed (inventory.begin() + 2), which is equal to the iterator that references the third element in inventory. This removes the string object equal to "armor". As a result, all of the following elements will move up by one. This version of the erase() member function
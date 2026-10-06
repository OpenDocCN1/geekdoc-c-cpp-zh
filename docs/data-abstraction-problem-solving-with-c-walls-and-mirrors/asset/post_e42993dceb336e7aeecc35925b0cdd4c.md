
# 494 C++ INTERLUDE 6 Iterators

collection You can also modify the collection as you traverse it by adding, removing, or simply changing entries.

You are familiar with iteration because you have written loops. For example, if namelist is a list of strings, you can write the following for loop to display the entire list:

```
int listSize = namelist.getLength();
for (int i = 0; i < listSize; i++)
cout << namelist.get(i) << endl;
```

Here the loop traverses, iterates, through the entries in the list. Instead of displaying each entry, you could do other things or to it.

Notice that the loop is at the client level, since it uses the ADT operation getEntry to access the list. For an array-based implementation of the list, getEntry can retrieve the array directly and quickly. But if a chain of linked nodes represents the list's entries, getEntry must move from node to node until it locates the desired one. For example, getEntry would begin at the first node in the chain and then move to the second node, the third node, and so on until it reaches the $n^{th}$ node. At the next repetition of the loop, getEntry would retrieve the $n+1^{th}$ entry in the list by beginning again at the first node in the chain and stepping from node to node until it reaches the $n+1$ node. This wastes time.

> Iterators An iterator is a program component that steps through, or traverses, a collection of data. The iterator keeps track of its progress during the traversal, or iteration. It can tell you whether a next entry exists, and if so, return a reference to it. During one cycle of the iteration, each data is considered once.

Iteration is such a common operation that we could include it as part of the ADT. Doing so would enable a more efficient implementation than you could achieve at the client level. Notice that the tovector of the ADT bag in Chapters 3 and 4 performs a traversal and is an example of a traversal controlled by the ADT. A client can tovector but cannot control its own traversal.

But tovector only returns the list's entries. If we want to do something with them as we traverse them we do not need to add another operation to the ADT each time we think of how to use iteration. We need a way for a client to step through a collection of data and retrieve or modify entries. The traversal should keep track of its progress; it should know where it is in the collection and whether it has accessed each entry. An iterator provides such a traversal.

C++ provides a rich library of tools to build iterators, but in this we focus on the capabilities to implement simple iterators that traverse a collection of items, retrieve an entry in a collection, and compare two iterators to determine whether they access the same entry in the collection. Such iterators are known as input iterators.

## C.6.1 Common Iterator Operations

Though not required, iterators in C++ typically provide basic functionality by overloaded operators. An iterator accesses the collection it currently traverses is usually implemented by overloading the C++ dereferencing operator \*. For example, you can define the * operator for an iterator so that *i is the iterator that i references.

Iterators also have operations that move the iterator forward through the collection. Often, these operations take the form of the overloaded operator ++. Bidirectional iterators also overload the -- to allow you to move backward through the collection. Lastly, the operators == and != are usually overloaded to compare iterators for equality.

> Note: Common iterator operations
| Operation | Description |
| --- | --- |
| * | Return the item that the iterator currently references |
| ++ | Move the iterator to the next item in the collection |
| -- | Move the iterator to the previous item in the collection (used only for bidirectional or random iterators) |
| == | Compare two iterators for equality |
| != | Compare two iterators for inequality |

By enabling you to use these operators for your iterator class, C++ gives you the advanced iterator operations covered in the next section without further programming. An additional step you must take to enable this functionality, is to derive your iterator class from the C++ template class iterator. This template does not have any methods. Instead, it is to identify the type of iterator you are creating using an iterator category tag as the template.
For example, to declare an iterator for the classlist we would use the following:

```
template <class ItemType>
class LinkedIterator : public iterator<input_iterator_tag, ItemType>
```

where input_iterator_tag identifies that this iterator implements input-iterator functionality. The output type specified, int, identifies the type of value used to measure the distance between two iterators. These values are normally integers. The distance between two iterators is the number of elements or positions between the current positions of the two iterators. For example, if an iterator points to the first item in a list and another points to the fifth item in the same list, their distance is 4.

> Note: C++ iterator categories
All of the following iterators provide operations that copy or assign (=) and increment (++).
| Category | Tag | Operation |
| --- | --- | --- |
| Input iterator | input_iterator_tag | Equality(==, !=), access collection (*) |
| Output iterator | output_iterator_tag | Change a collection entry (*) |
| Forward iterator | forward_iterator_tag | Same as the forward iterator and output iterators and has a default constructor |
| Bidirectional iterator | bidirectional_iterator_tag | Same as the forward iterator, but also can traverse the collection backward (--) |
| Random-access iterator | random_iterator_tag | Same as the bidirectional iterator and adds support for arithmetic (+, -) and relational (<, >, >=) operations between iterators. Supports the [] operator to directly access entries.

## C6.1.2 Using Iterator Operations

Before discussing the details of a of iterators, we should examine how clients would use these. Standard containers in C++ implement two special methods, begin and end, that return an iterator to the first and last entry. Iterators should have an order of magnitude in performance O(1) as they move from entry to entry. Let's see how a client could use these if implemented in LinkedList.

```
int currentPosition = 1;
while (currentPosition <= myList.getLength())
{
    cout << myList.entry(currentPosition); // O(n) operation
    currentPosition++;
} // end while
```

Now that Iterator is a class of iterators for LinkedList, and LinkedList defines the methods begin and end declares them as follows:

```
LinkedListIterator<ItemType> begin() const;
LinkedListIterator<ItemType> end() const;
```

We can rewrite the following snippet of code using LinkedList iterator objects:

```
LinkedListIterator<ItemType> currentIterator = myList.begin();
while (currentIterator != myList.end())
{
    cout << ++currentIterator; // O(1) operation
} // end while
```

The first line creates a LinkedListIterator, currentIterator, that points to the first entry in the list. The while-loop tests to see whether currentIterator points to the entry that is at the end of the list. Then, for each entry in the list, we dereference the iterator using the * operator to access and display the entry at the iterator's current position. The iterator is incremented to reference the next entry in the list.

Notice that the ++ operator precedes the name of the iterator. We use this prefix operator to differentiate it from an arithmetic increment of an integer, which uses the postfix ++ operator.

> Using the ++ and -- operators
In C++, the operators ++ and -- can be used in prefix or postfix form to represent incrementing or decrementing the corresponding variable. To differentiate between incrementing or decrementing arithmetic variables from iterator positions, use ++ and -- as postfix operators for the former operations and as prefix for the latter.

The implementation of methods begin and end in the LinkedList class are straightforward:

```
template <class ItemType>
LinkedListIterator<ItemType> LinkedList<ItemType>::begin()
{
    return LinkedListIterator<ItemType>(this, headPtr);
}
```

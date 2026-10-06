Java-style iterators and STL-style iterators. The Java-style iterators are easier to use, whereas the STL-style iterators can be combined with Qt's and STL's generic algorithms and are more powerful.

For each container class, there are two Java-style iterator types: a read-only iterator and a read-write iterator. Their valid positions are shown in Figure 11.3. The read-only iterators are QVectorIterator<T>, QLinkedListIterator<T>, QListIterator<T>. The corresponding read-write iterators have Mutable in their (e.g., MutableVectorIterator<T>). In this discussion, we concentrate on QList's iterators: the iterators for linked lists and vectors have the same API.

# Figure 11.3. Valid positions for Java-style iterators

![](bbox=[0.008, 0.266, 0.303, 0.335])

The first thing to keep in mind when using Java-style iterators is that they don't point directly at items. Instead, they can be located before the first item, after the last item, or between two items. A typical iteration loop looks like this:

```
QList<double> list;
...
QListIterator<double> i(list);
while (i.hasNext()) {
    do_something(i.next());
}
```

The iterator is initialized with the container to traverse. At this point, the iterator is located just before the first item. The call to hasNext() returns true if there is an item to the right of the iterator. The next() function returns the item to the right of the iterator and advances the iterator to the next valid position.

Iterating backward is similar, except that we must first call toBack() to position the iterator after the last item:

```
QListIterator<double> i(list);
i.toBack();
while (i.hasPrevious()) {
    do_something(i.previous());
}
```

The hasPrevious() function returns true if there is an item to the left of the
insert(). The iterator is then advanced to point between the new item and the following item.

In addition to the Java-style iterators, every sequential container class C<T> has STL-style types: C<T>::iterator and C<T>::const_iterator. The difference between the two is that const_iterator doesn't modify the data.

A container's begin() returns an STL-style iterator that refers to the first item in the container (e.g., list[0]), whereas end() returns to the "one past the last" item (e.g., list[5] for a list of size 5). Figure 11.5 shows the valid positions for STL-style iterators. If a container is empty, begin() equals end() can be used to see whether the container has any items, although it is usually more convenient to call isEmpty() for this purpose.

# ## Figure 11.5. Valid positions for STL-style iterators

![](bbox=[0.012, 0.353, 0.355, 0.415])

The STL-style iterator syntax ++ and -- is modeled after that of C++ pointers into an array. We can use the and -- operators to move to the next or previous item, and the unary * operator to retrieve the current item. For QVector<T>, the iterator and const_iterator types are merely typedefs for T * and const T *. (This is possible because QVector<T> stores its items in consecutive memory locations.)

The following example returns each value in a QList<double> with its absolute value:

```
QList<double>::iterator i = list.begin();
while (i != list.end()) {
    *i = qAbs(*i);
    ++;
}
```

A few Qt functions return a container. If we want to iterate over the return value of a function using an STL-style iterator, we must take a copy of the container and iterate over it. For example, the following code is the correct way to iterate over the QList<int> returned by QSplitter::sizes():

```
QList<int> list = splitter->sizes();
QList<int>::const_iterator i = list.begin();
while (i != list.end()) {
```
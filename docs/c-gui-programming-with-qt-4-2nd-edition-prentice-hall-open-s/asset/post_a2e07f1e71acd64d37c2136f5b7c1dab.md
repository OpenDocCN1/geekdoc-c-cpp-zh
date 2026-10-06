
## 11. Container Classes

- Sequential Containers
- Associative Containers
- Generic Algorithms
- Strings, Byte Arrays, and Variants

Container classes are general-purpose template classes that store items of a type in memory. C++ already offers many containers as part of the Standard Template Library (STL), which is included in the Standard C++ library.

Qt provides its own container classes, for Qt programs we can use both the Qt and the STL containers. The main advantages of the Qt containers are that they behave the same on all platforms and that they are implicitly shared. Sharing or "copy on write", is an optimization that makes it possible to pass inside containers as values without any significant performance cost. The Qt containers also feature easy-to-use iterator classes inspired by Java, which can be streamed using QStream, and usually result in less code in the executable than the corresponding STL containers. Finally, on some hardware platforms supported by Qt/Embedded Linux, the Qt containers are the only ones available.

Qt offers both sequential containers such as QVector<T>, QLinkedList<T>, and QList<T>, and associative containers such as QMap<K, T> and QHash<K, T>. Conceptually, the sequential containers store one item after another, whereas the associative containers store key-value pairs.

Qt also provides generic algorithms that perform operations on arbitrary containers. For example, qSort() algorithm sorts a sequential container, and qBinaryFind() performs a binary search on a sorted sequential container. These algorithms are similar to those offered by the STL.

If you are already familiar with the STL containers and have STL available on your target platforms, you might want to use them instead of, or in addition to, the Qt containers. For more information about the STL classes and functions, a good place to start is SGI's STL web site: http://www.sgi.com/tech/stl.

In this chapter, we will also look at QString, QArray, and QVariant, since they have a lot in common with containers. QString is a 16-bit Unicode string used throughout Qt's API. QArray is an array of 8-bit chars useful for storing binary data. QVariant is a type that can store more C++ and Qt value types.

## Sequential Containers

A QVector<T> is an array-like data structure that stores its items at adjacent positions in memory, as Figure 11.1 illustrates. What distinguishes a vector from a plain C++ array is that a vector has its own size and can be resized. Appending extra items to the end of a vector is efficient, whereas inserting items at the front or in the middle of a vector can be expensive.

### Figure 11.1. A vector of doubles

![](img/5a524abdf0b0d58fa99d30abb4463611_437_0.png)

If we know in advance how many items we are going to need, we can give the vector an initial size when we define it and use the [] operator to assign a value to the items; otherwise, we must either resize the vector later or append items. Here's an example where we specify the initial size:

```
QVector<double> vect(3);
vect[0] = 1.0;
vect[1] = 0.540302;
vect[2] = -0.416147;
```

Here's the same example, this time starting with an empty vector and using the append() function to append items at the end:

```
QVector<double> vect;
vect.append(1.0);
vect.append(0.540302);
vect.append(-0.416147);
```

We can also use the << operator instead of append():

```
vect << 1.0 << 0.540302 << -0.416147;
```

One way to iterate over the vector's items is to use [] and count();

```
double sum = 0.0;
for (int i = 0; i < vect.count(); ++i)
    sum += vect[i];
```

Inserting items at the beginning or in the middle of a QVector<T>, removing items from these, can be inefficient for large vectors. For this reason, QLinkedList<T>, a data structure that stores its items at non-adjacent locations in memory, as illustrated by Figure 11.2. Unlike vectors, linked lists don't support random access, but they provide "constant time" insertions and removals.

### Figure 11.2. A linked list of doubles

![](img/5a524abdf0b0d58fa99d30abb4463611_438_0.png)

Linked lists do not provide the [] operator, so iterators must be used to traverse their items. Iterators are also used to specify the position of items. For example, the following code inserts the string "Tote Hosen" between "Clash" and "Ramones":

```
QLinkedList<QString> list;
list.append("Clash");
list.append("Ramones");
```

```
QLinkedList<QString>::iterator i = list.find("Ramones");
list.insert(i, "Tote Hosen");
```

We will take a more detailed look at iterators later in this section.
The QList<T> sequential container is an "array-list" that combines the most benefits of QVector<T> and QLinkedList<T> in a single class. It supports random access, and its interface is index-based like QVector. Inserting or removing an item at either end of a QList<T> is very fast, and inserting in the middle is fast for lists with up to about one thousand items. Unless we want to perform insertions in the middle of huge lists or need the list's items to occupy consecutive addresses in memory, QList<T> is usually the most appropriate general-purpose container class to use.

The QStringList is a subclass of QList<QString> that is widely used in Qt API. In addition to the features it inherits from its base class, it provides some extras that make the class more versatile for string handling. We discuss QStringList in the last section of this chapter (p. 290).

QStack<T> and QQueue<T> are two examples of convenience subclasses. QStack<T> provides push(), pop(), top(). QQueue<T> provides enqueue(), dequeue(), head().

For all the containers seen so far, the value type T can be a basic type like int or double, a pointer, or a class that has a default constructor (a constructor that takes no arguments), a copy constructor, and an assignment operator. Classes that qualify include ByteArray, QDateTime, QRegExp, QString, and QVariant that are derived from QObject do not qualify, because they lack a copy constructor and an assignment operator. This is no problem in practice, since we can simply store pointers to QObject rather than the objects they themselves.

The value type T can be a container, in which case we must remember to separate consecutive angle brackets with spaces; otherwise, the compiler will choke on what it thinks is a >> operator. For example:

```
QList<QVector<double> > list;
```

In addition to the types just mentioned, a container's value type can be any class that meets the criteria described earlier. Here is an example of such a class:

```cpp
class Movie
{
public:
    Movie(const QString& title) : myTitle(title), myDuration(0) {}
    void setTitle(const QString& title) { myTitle = title; }
    QString title() const { return myTitle; }
    void setDuration(int duration) { myDuration = duration; }
    QString duration() const { return myDuration; }

private:
    QString myTitle;
    int myDuration;
};
```

Qt provides two categories of iterators for traversing the items stored in: Java-style iterators and STL-style iterators. The Java-style iterators are easier to use, whereas the STL-style iterators can be combined with generic algorithms and are more powerful.

For each container class, there are two Java-style iterator types: a read-only iterator and a read-write iterator. The read-only iterators are QVectorIterator<T>, QLinkedListIterator<T>, QListIterator<T>. The corresponding read-write iterators have Mutable in their (e.g., MutableVectorIterator<T>). In this discussion, we concentrate on QList's iterators: the iterators for linked lists and vectors have the same API.

### Figure 11.3. Valid positions for Java-style iterators

![](img/5a524abdf0b0d58fa99d30abb4463611_440_0.png)

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

The hasPrevious() function returns true if there is an item to the left of the.

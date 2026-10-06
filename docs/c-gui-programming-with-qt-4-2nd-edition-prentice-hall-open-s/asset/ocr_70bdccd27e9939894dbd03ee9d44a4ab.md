Vector entries that were created without assigning an explicit value are initialized using the item class's default constructor. Basic types and pointer types are initialized to zero.

Inserting items at the beginning or in the middle of a QVector<T>, removing items from these positions, can be inefficient for large vectors. For this reason, QLinkedList<T>, a data structure that stores its items at non-adjacent locations, as illustrated by Figure 11.2. Unlike vectors, linked lists don't support random access, but they provide "constant time" insertions and removals.

# Figure 11.2. A linked list of doubles

![](bbox=[0.005, 0.287, 0.51, 0.325])

Linked lists do not provide the [] operator, so iterators must be used to traverse their items. Iterators are also used to specify the position of items. For example, the following code inserts the string "Tote Hosen" between "Clash" and "Ramones":

```
QLinkedList<QString> list;
list.append("Clash");
list.append("Ramones");

QLinkedList<QString>::iterator i = list.find("Ramones");
list.insert(i, "Tote Hosen");
```

We will take a more detailed look at iterators later in this section. The List<T> sequential container is an "array-list" that combines the most important benefits of QVector<T> and QLinkedList<T> in a single class. It supports random access, and its interface is index-based like QVector<T>. Inserting or removing an item at either end of a List<T> is very fast, and inserting in the middle is fast for lists with up to one thousand items. Unless we want to perform insertions in the middle of huge lists or need the list's items to occupy consecutive addresses in memory, List<T> i is usually the most appropriate general-purpose container to use.

The QStringList is a subclass of List<QString> that is widely used in Qt. In addition to the functions it inherits from its base class, it provides some extra that that make the class more versatile for string handling. We discuss QStringList in the last section of this chapter (p. 290).
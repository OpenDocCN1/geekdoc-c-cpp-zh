
![](img/5e58fb4c840712efd6ed6fa82bb97f57_599_0.png)

If you want to write a program that collects objects (such as the stamps to the left), you have a number of choices. Of course, you can use an array or linked list, but computer scientists have invented other mechanisms that may be better suited for the task. In this chapter, you will learn how to use the set, map, and priority queue types that are provided in the C++ library. You will see how these data structures are implemented as tree-like structures, and how they trade off sequential ordering for fast element lookup.

## 14.1 Sets

Arrays, vectors and linked lists have one characteristic in common: These data structures keep the elements in the same order in which you inserted them. However, in many applications, you don't really care about the order of the elements in a collection. You can then make a very useful tradeoff: Instead of keeping elements in order, you can find them quickly.

A set is an unordered collection of distinct elements.

In mathematics and computer science, an unordered collection of distinct items is called a set. As a typical example, consider a print server: a computer that has access to multiple printers. The server may keep a collection of objects representing available printers (see Figure 1). The order of the objects doesn't really matter.

The fundamental operations on a set are

- Adding an element.
- Removing an element.
- Finding an element.
- Traversing all elements.

Sets don't have duplicates. Adding a duplicate of an element that is already present is ignored.

A set rejects duplicates. If an object is already in the set, an attempt to add it again is ignored. That's useful in many programming situations. For example, if we keep a set of available printers, each printer should occur at most once in the set. Thus, we will interpret the add and remove operations of sets just as we do in mathematics: Adding elements that are already in the set, as well as removing elements that are not in the set, are valid operations, but they do not change the set.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_599_1.png)

Figure 1   A Set of Printers

In C++, you use the set class to construct a set. As with vectors and lists, set requires a type parameter. For example, a set of strings is declared as follows:

```cpp
set<string> names;
```

You use the insert and erase member functions to add and remove elements:

```cpp
names.insert("Romeo");
names.insert("Juliet");
names.insert("Romeo"); // Has no effect: "Romeo" is already in the set
names.erase("Juliet");
names.erase("Juliet"); // Has no effect: "Juliet" is no longer in the set
```

To determine whether a value is in the set, use the count member function. It returns 1 if the value is in the set, 0 otherwise.

```cpp
int c = names.count("Romeo"); // count returns 1
```

Finally, you can visit the elements of a set with an iterator. The iterator visits the elements in sorted order, not in the order in which you inserted them. For example, consider what happens when we continue our set example as follows:

The standard C++ set class stores values in sorted order.

```cpp
names.insert("Tom");
names.insert("Diana");
names.insert("Harry");
set<string>::iterator pos;
for (pos = names.begin(); pos != names.end(); pos++)
{
   cout << *pos << " ";
}
```

The code prints the set elements in dictionary order:

```cpp
Diana Harry Romeo Tom
```

A set cannot contain duplicates. A multiset (also called a bag) is an unordered collection that can contain multiple copies of an element. An example is a grocery bag that contains some grocery items more than once (see Figure 2).

In the C++ library, the multiset class implements this data type. You use a multiset in the same way as a set. When you insert an element multiple times, the element count reflects the number of insertions. Each call to erase decrements the element count until it reaches 0.

A multiset (or bag) is similar to a set, but elements can occur multiple times.

```cpp
multiset<string> names;
names.insert("Romeo");
names.insert("Juliet");
names.insert("Romeo"); // Now names.count("Romeo") is 2
names.erase("Juliet"); // Now names.count("Juliet") is 0
names.erase("Juliet"); // Has no effect: "Juliet" is no longer in the bag
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_600_0.png)

A good illustration of the use of sets is a program to check for misspelled words. Assume you have a file containing correctly spelled words (that is, a dictionary), and a second file you wish to check. The program reads a file containing a dictionary of correctly spelled words into a set, then reads words from the second file and tests each in the set, printing the word if it is not found.

```cpp
void spell_check(istream& dictionary, istream& text)
{
    set<string> words;
    string word;

    // First put all words from the dictionary into the set
    while (dictionary >> word)
    {
        words.insert(word);
    }

    // Then read words from text
    while (text >> word)
    {
        if (words.count(word) == 0)
        {
            cout << "Misspelled word " << word << endl;
        }
    }
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_601_0.png)

# SELF CHECK

- 1. Arrays and lists remember the order in which you added elements; sets do not. Why would you want to use a set instead of an array or list?
- 2. Why are set iterators different from list iterators?
- 3. What is the output of the following code snippet?

```cpp
set<int> s;
for (int i = 1; i <= 4; i++)
{
    s.insert(i * i);
    s.insert(-i);
}
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

- 4. What is the output of the following code snippet?

```cpp
set<int> s;
for (int i = 0; i < 20; i = i + 2) { s.insert(i); }
for (int i = 0; i < 20; i = i + 2) { s.erase(i); }
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

- 5. What does the following code do, given two sets<string> named a and b?

```cpp
set<string> c;
for (set<string>::iterator p = a.begin(); p != a.end(); p++) { c.insert(*p); }
for (set<string>::iterator p = b.begin(); p != b.end(); p++)
{
    if (a.count(*p) == 0) { c.erase(*p); }
}
```

**Practice It**  Now you can try these exercises at the end of the chapter: R14.1, R14.2, P14.3.

## Special Topic 14.1

![](img/5e58fb4c840712efd6ed6fa82bb97f57_602_0.png)

### Defining an Ordering for Container Elements

The set and multiset classes need to compare elements. By default, these classes use the < operator for comparisons.

Suppose that you want to build a set<Employee>. The compiler will complain that it does not know how to compare two employees.

To solve this problem you can overload the < operator for Employee objects:

```cpp
bool operator<(const Employee& a, const Employee& b)
{
    return a.get_name() < b.get_name();
}
```

This < operator compares employees by name. To learn more about overloading operators, see Horstmann and Budd, *Big C++, 2nd ed.*, Chapter 14 (John Wiley & Sons, Inc., 2009).

## 14.2 Binary Search Trees

A set implementation is allowed to rearrange its elements in any way it chooses so that it can find elements quickly. Suppose a set implementation *sorts* its entries. Then it can use *binary search* to locate elements in O(log n) steps, where n is the size of the set. There is just one wrinkle with this idea. We can’t use an array to store the elements of a set, because insertion and removal in an array is slow; an O(n) operation.

In the following sections we will introduce the simplest of many *tree* data structures that computer scientists have invented to overcome this problem.

### 14.2.1 Binary Trees and Binary Search Trees

> A binary tree consists of nodes, each of which has at most two child nodes.

A linked list is a one-dimensional data structure. You can imagine that all nodes are arranged in a line. In contrast, a *tree* is made of nodes that have children, which can again have children. You should visualize it as a tree, except that it is traditional to draw the tree upside down, like a family tree or hierarchy chart (see Figure 3). In a binary tree, every node has at most two children; hence the name *binary*.

Finally, a *binary search tree* is constructed to have the following important property:

- The data values of *all* descendants to the left of *any* node are less than the data value stored in that node, and *all* descendants to the right have greater data values.

> All nodes in a binary search tree fulfill the property that the descendants to the left have smaller data values than the node data value, and the descendants to the right have larger data values.

The tree in Figure 3 has this property. To verify the binary search tree property, you must check each node. Consider the node “Juliet”. All descendants to the left have data before “Juliet”. All descendants on the right have data after “Juliet”. Move on to “Eve”. There is a child to the left, with data “Adam” before “Eve”, and a single child to the right, with data “Harry” after “Eve”. Check the remaining nodes in the same way.

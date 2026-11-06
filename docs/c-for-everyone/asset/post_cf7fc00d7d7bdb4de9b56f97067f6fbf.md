
![](img/5e58fb4c840712efd6ed6fa82bb97f57_566_0.png)

**Figure 2** Adding a Node to a Linked List

The standard C++ library has an implementation of the linked list container structure. In this section, you will learn how to use the standard linked list structure. Later you will look “under the hood” and find out how to implement linked lists. (The linked list of the standard C++ library has links going in both directions. Such a list is often called a *doubly-linked list*. A *singly-linked list* lacks the links to the predecessor elements.)

Just like vector, the standard list is a *template*: You can declare lists for different types. For example, to make a list of strings, define an object of type `list<string>`. Then you can use the push_back function to add strings to the end of the list. The following code segment defines a list of strings, names, and adds three strings to it:

```cpp
list<string> names;

names.push_back("Tom");
names.push_back("Diana");
names.push_back("Harry");
```

This code looks exactly like the code that you would use to build a vector of strings. There is, however, one major difference. Suppose you want to access the last element in the list. You cannot directly refer to `names[2]`. Because the values are not stored in one contiguous block in memory, there is no immediate way to access the third element. Instead, you must visit each element in turn, starting at the beginning of the list and then proceeding to the next element.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_566_1.png)

**Figure 3** Removing a Node from a Linked List

You can inspect and edit a linked list with an iterator. An iterator points to a node in a linked list.

To visit an element, you use a *list iterator*. An iterator marks a *position* in the list. To get an iterator that marks the beginning position in the list, you define an iterator variable, then call the begin function of the list class to get the beginning position:

```cpp
list<string>::iterator pos;
pos = names.begin();
```

To move the iterator to the next position, use the ++ operator:

```cpp
pos++;
```

You can also move the iterator backward with the -- operator:

```cpp
pos--;
```

You use the * operator to find the value that is stored in the position marked by the iterator:

```cpp
string value = *pos;
```

You have to be careful to distinguish between the iterator pos, which represents a position in the list, and the value *pos, which represents the value that is stored in the list. For example, if you change *pos, then you update the contents in the list:

```cpp
*pos = "Romeo";
    // The list value at the position is changed
```

If you change pos, then you merely change the current position.

```cpp
pos = names.begin();
    // The position is again at the beginning of the list
```

To insert another string before the iterator position, use the insert function:

```cpp
names.insert(pos, "Romeo");
```

The insert function inserts the new element *before* the iterator position, rather than after it. This convention makes it easy to insert a new element before the first value of the list:

```cpp
pos = names.begin();
names.insert(pos, "Romeo");
```

That raises the question of how you insert a value after the end of the list. Each list has an *end position* that does not correspond to any value in the list but that points past the list’s end. The end function returns that position.

```cpp
pos = names.end(); // Points past the end of the list
names.insert(pos, "Juliet");
    // Insert past the end of the list
```

It is an error to compute

```cpp
string value = *names.end(); // Error
```

The end position does not point to any value, so you cannot look up the value at that position. This error is equivalent to the error of accessing v[10] in a vector with 10 elements.

The end position has another useful purpose: it is the stopping point for traversing the list. The following code iterates over all elements of the list and prints them out:

```cpp
pos = names.begin();
while (pos != names.end())
{
    cout << *pos << endl;
    pos++;
}
```

The traversal can be described more concisely with a for loop:

```cpp
for (pos = names.begin(); pos != names.end(); pos++)
{
    cout << *pos << endl;
}
```

Of course, this looks very similar to the typical for loop for traversing an array:

```cpp
for (i = 0; i < size; i++)
{
    cout << a[i] << endl;
}
```

Finally, to remove an element from a list, you move an iterator to the position that you want to remove, then call the erase function. The erase function returns an iterator that points to the element after the one that has been erased.

The following code erases the second element of the list:

```cpp
pos = names.begin();
pos++;
pos = names.erase(pos);
```

Now pos points to the element that was previously the third element and is now the second element.

Here is a short example program that adds elements to a list, inserts and erases list elements, and finally traverses the resulting list:

### ch13/list1.cpp

```cpp
#include <string>
#include <list>
#include <iostream>

using namespace std;

int main()
{
    list<string> names;

    names.push_back("Tom");
    names.push_back("Diana");
    names.push_back("Harry");
    names.push_back("Juliet");

    // Add a value in fourth place

    list<string>::iterator pos = names.begin();
    pos++;
    pos++;
    pos++;

    names.insert(pos, "Romeo");

    // Remove the value in second place

    pos = names.begin();
    pos++;

    names.erase(pos);

    // Print all values
    for (pos = names.begin(); pos != names.end(); pos++)
    {
        cout << *pos << endl;
    }

    return 0;
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_569_0.png)

### Program Run

```text
Tom
Harry
Romeo
Juliet
```

### SELF CHECK

- 1. Do linked lists take more storage space than arrays of the same size?
- 2. Why don’t we need iterators with arrays?
- 3. Make a linked list of integers containing the numbers 1 through 10.
- 4. How do you erase the first element of the linked list names?
- 5. How do you erase the last element of the linked list names?
- 6. How do you add "Buffy" as the second element in the list names?

**Practice It** Now you can try these exercises at the end of the chapter: R13.4, R13.5, P13.4.

## 13.2 Implementing Linked Lists

The previous section showed you how to put linked lists to use. However, because the implementation of the list class is hidden from you, you had to take it on faith that the list values are really stored in separate memory blocks. We will now walk through an implementation of the list, node, and iterator classes.

For simplicity, we will implement linked lists of strings. To implement the linked list class in C++ that can hold values of arbitrary types, you need to know how to program with templates (see Horstmann and Budd, Big C++, 2nd ed., Chapter 16). To implement iterators that behave exactly like the ones in the C++ library, you also need to know about operator overloading and nested classes (see Big C++, 2nd ed., Chapters 17 and 18).

### 13.2.1 The Classes for Lists, Nodes, and Iterators

The List class of the standard library defines many useful member functions. For simplicity, we will only study the implementation of the most useful ones: push_back, insert, erase, and the iterator operations. We call our class List, with an uppercase L, to differentiate it from the standard List class template.

A linked list stores each value in a separate object, called a node. A node object holds a value, together with pointers to the previous and next nodes:

However, if the iterator is currently past the end, then you must make it point to the last element in the list.

```cpp
void Iterator::previous()
{
    if (position == NULL)
    {
        position = container->last;
    }
    else
    {
        position = position->previous;
    }
}
```

The get function (which is the equivalent of the * operator) simply returns the data value of the node to which position points—that is, position->data. It is illegal to call get if the iterator points past the end of the list:

```cpp
string Iterator::get() const
{
    return position->data;
}
```

Finally, the equals function (which is the equivalent of the == operator) compares two position pointers:

```cpp
bool Iterator::equals(Iterator b) const
{
    return position == b.position;
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_572_0.png)

**Figure 4** Advancing an Iterator

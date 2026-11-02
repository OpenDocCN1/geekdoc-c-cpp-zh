
Some programmers find type names such as `list<string>::iterator` and `list<string>::const_iterator` too cumbersome and prefer to use the `auto` reserved word (see Special Topic 2.3):

```
auto pos = names.begin();
```

To move the iterator to the next position, use the `++` operator:

```
pos++;
```

You can also move the iterator backward with the `--` operator:

```
pos--;
```

You use the `*` operator to find the value that is stored in the position marked by the iterator:

```
string value = *pos;
```

You have to be careful to distinguish between the iterator `pos`, which represents a position in the list, and the value `*pos`, which represents the value that is stored in the list. For example, if you change `*pos`, then you update the contents in the list:

```
*pos = "Romeo"; // The list value at the position is changed
```

If you change `pos`, then you merely change the current position.

```
pos = names.begin(); // The position is again at the beginning of the list
```

To insert another string before the iterator position, use the `insert` function:

```
names.insert(pos, "Romeo");
```

The `insert` function inserts the new element before the iterator position, rather than after it. This convention makes it easy to insert a new element before the first value of the list:

```
pos = names.begin();
names.insert(pos, "Romeo");
```

That raises the question of how you insert a value after the end of the list. Each list has an end position that does not correspond to any value in the list but that points past the list's end. The `end` function returns that position:

```
pos = names.end(); // Points past the end of the list
names.insert(pos, "Juliet"); // Insert past the end of the list
```

```
for (pos = names.begin(); pos != names.end(); pos++)
{
    cout << *pos << endl;
}
```

Of course, this looks very similar to the typical for loop for traversing an array:

```
for (i = 0; i < size; i++)
{
    cout << a[i] << endl;
}
```

There is a convenient shortcut for this loop, called the range-based for loop, which was discussed in Special Topic 6.5:

```
for (const string& element : names)
{
    cout << element << " ";
}
```

To remove an element from a list, you move an iterator to the position that you want to remove, then call the `erase` function. The following code erases the second element of the list:

```
pos = names.begin();
pos++;
pos = names.erase(pos);
```

The iterator that is passed to `erase` now points to a storage location that has been deleted, and can no longer be used. Therefore, the `erase` function returns an iterator that points to the element after the one that has been erased. It is a good idea to immediately replace the original iterator with the one that the `erase` function returns.

At the end of the preceding code sample, `pos` points to the element that was previously the third element and is now the second element.

In addition to the `push_back` member function, there is a `push_front` member function that adds an element at the front. The `pop_front` and `pop_back` member functions remove the first and last elements.

**Table 1 Working with Linked Lists**

| Code | Description |
|---|---|
| `list<string> names;` | An empty list. |
| `names.push_back("Harry");` | Adds an element to the end of the list. |
| `names.push_front("Sally");` | Adds an element to the front of the list. |
| `int n = names.size();` | The current size of the list. |
| `list<string>::iterator iter = names.begin();` | Gets an iterator pointing to the first element of the list. |
| `iter++;` | Moves the iterator to the next element. |
| `string name = *iter;` | Yields the element to which the iterator points. |
| `if (pos != names.end())` | Tests whether the iterator still points to an element. |
| `names.insert(iter, "Fred");` | Inserts an element before the iterator. |
| `iter = names.erase(iter);` | Removes the element to which the iterator points. `iter` now points to the element following the removed element. |
| `names.pop_front(); names.pop_back();` | Removes the first and last elements of the list. |

The previous function (which is the equivalent of the `--` operator) is a bit more complex. In the ordinary case, you move the position backward with the instruction `position = position->previous;`

However, if the iterator is currently past the end, then you must make it point to the last element in the list.

```
void Iterator::previous()
{
    if (position == nullptr)
    {
        position = container->last;
    }
    else
    {
        position = position->previous;
    }
}
```

The `get` function (which is the equivalent of the `*` operator) simply returns the data value of the node to which `position` points—that is, `position->data`. It is illegal to call `get` if the iterator points past the end of the list:

```
string Iterator::get() const
{
    return position->data;
}
```

Finally, the `equals` function (which is the equivalent of the `==` operator) compares two position pointers:

```
bool Iterator::equals(Iterator other) const
{
    return position == other.position;
}
```

## 14.2.3 Implementing Insertion and Removal

In the last section you saw how to implement the iterators that traverse an existing list. Now you will see how to build up lists by adding and removing elements, one step at a time.

First, we will implement the `push_back` function. It appends an element to the end of the list (see Figure 5). Make a new node:

```
Node* new_node = new Node(element);
```

This new node must be integrated into the list after the node to which the `last` pointer points. That is, the data member `next` of the last node (which is currently `nullptr`) must be updated to `new_node`. Also, the data member `previous` of the new node must point to what used to be the last node:

```
new_node->previous = last;
last->next = new_node;
```

> List nodes are allocated on the free store, using the `new` operator.

```
Node* after = iter.position;
Node* before = after->previous;
Node* new_node = new Node(element);
new_node->previous = before;
new_node->next = after;
after->previous = new_node;
if (before == nullptr) // Insert at beginning
{
    first = new_node;
}
else
{
    before->next = new_node;
}
```

Finally, look at the implementation of the `erase` function:

```
Iterator List::erase(Iterator iter)
```

You want to remove the node to which `iter.position` points. As before, give names to the node to be removed, the node before it, and the node after it:

```
Node* remove = iter.position;
Node* before = remove->previous;
Node* after = remove->next;
```

You need to update the `next` and `previous` pointers of the `before` and `after` nodes to bypass the node that is to be removed (see Figure 7).

```
before->next = after; // If before != nullptr ①
after->previous = before; // If after != nullptr ②
```

However, as before, you need to cope with the possibility that `before`, `after`, or both are `nullptr`. If `before` is `nullptr`, you are erasing the first element in the list. It has no predecessor to update, but you must change the `first` pointer of the list. Conversely,

![](img/d61019b035dd82beb581604273c0ee6b_732_0.png)

Figure 7 Removing a Node from a Linked List

Implementing operations that modify a linked list is challenging—you need to make sure that you update all node pointers correctly.

notice it until you traverse the list backwards. If a node has been deleted, then that same storage area may later be reallocated for a different purpose, and if you have kept a pointer to it, following that invalid node pointer will lead to disaster. You must exercise special care when implementing any operations that manipulate the node pointers directly.

Here is a program that puts our linked list to use and demonstrates the `insert` and `erase` operations:

### sec02/list.h

```cpp
#ifndef LIST_H
#define LIST_H

#include <string>

using namespace std;

class List;
class Iterator;

class Node
{
public:
/**
Constructs a node with a given data value.
@param element the data to store in this node
*/
Node(string element);
private:
string data;
Node* previous;
Node* next;
friend class List;
friend class Iterator;
};

class List
{
public:
/**
Constructs an empty list.
*/
List();
/**
Appends an element to the list.
@param element the value to append
*/
void push_back(string element);
/**
Inserts an element into the list.
@param iter the position before which to insert
@param element the value to insert
*/
void insert(Iterator iter, string element);
/**
Removes an element from the list.
@param iter the position to remove
*/
```

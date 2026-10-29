
# Display 19.4  **Two Kinds of Lists**

![](img/9505fd46e120aa9c1406715936ff6251_796_0.png)

The lists in Display 19.4 contain the three integer values 1, 2, and 3 in that order. The types for the two lists are `slist<int>` and `list<int>`. The display also indicates the location of the iterators `begin()` and `end()`. We have not yet told you how you can enter the integers into the lists.

In Display 19.4 we have drawn our singly and doubly linked lists as nodes and pointers of the form discussed in Chapter 17. The STL class `list` and the nonstandard class `slist` might (or might not) be implemented in this way. However, when using the STL template classes, you are shielded from these implementation details. So, you simply think in terms of locations for the data (which may or may not be nodes) and of iterators (not pointers). You can think of the arrows in Display 19.4 as indicating the directions for `++` (which is down) and `--` (which is up in Display 19.4).

We presented the template class `list` to help give a context for the sequential containers. It corresponds to what we discussed in Chapter 17 and is the first thing that comes to the mind of most programmers when you mention linked lists. However, since the template class `list` is not standard we will not discuss it further. If your implementation offers the template class `list` and you want to use it, the details are similar to those we will describe for `list`, except that the decrement operators `--` (prefix and postfix) are not defined for `slist`.

A simple program using the STL template class list is given in Display 19.5. The function push_back adds an element to the end of the list. Notice that for the list template class, the dereferencing operator gives you access for reading and for changing the data. Also notice that with the list template class and all the template classes and iterators of the STL, all definitions are placed in the std namespace.

## Display 19.5 Using the list Template Class

```
//Program to demonstrate the STL template class list.
#include <iostream>
#include <list>
using std::cout;
using std::endl;
using std::list;
using std::list<int>::iterator;

int main( )
{
    list<int> listObject;

    for (int i = 1; i <= 3; i++)
        listObject.push_back(i);

    cout << "List contains:\n";
    iterator iter;
    for (iter = listObject.begin( ); iter != listObject.end( ); iter++)
        cout << *iter << " ";
    cout << endl;

    cout << "Setting all entries to 0:\n";
    for (iter = listObject.begin( ); iter != listObject.end( ); iter++)
        *iter = 0;

    cout << "List now contains:\n";
    for (iter = listObject.begin( ); iter != listObject.end( ); iter++)
        cout << *iter << " ";
    cout << endl;

    return 0;
}
```

## SAMPLE DIALOGUE

```
List contains:
1 2 3
Setting all entries to 0:
List now contains:
0 0 0
```

Note that Display 19.5 would compile and run exactly the same if we replaced list and list<int> with vector and vector<int>, respectively. This uniformity of usage is a key part of the STL syntax.

There are, however, differences between a vector and a list container. One of the main differences is that a vector container has random-access iterators whereas a list has only bidirectional iterators. For example, if you start with Display 19.2, which uses random access, and replace all occurrences of vector and vector<char> with list and list<char>, respectively, and compile the program, you will get a compiler error. (You will get an error message even if you delete the statements containing container[1] or container[2].)

The basic sequential template classes of the STL are listed in Display 19.6. Other containers, such as stacks and queues, can be obtained from these using techniques discussed in the subsection entitled "The Container Adapters stack and queue." A sample of some member functions of the sequential container classes is given in Display 19.7. All these sequence template classes have a destructor that returns storage for recycling.

## Display 19.6 STL Basic Sequential Containers

| TEMPLATE CLASS NAME | ITERATOR TYPE NAMES | KIND OF ITERATORS | LIBRARY HEADER FILE |
|---|---|---|---|
| slist (Warning: slist is not part of the STL.) | slist<T>::iterator<br>slist<T>::const_iterator | Mutable forward<br>Constant forward | <slist> (Depends on implementation and may not be available.) |
| list | list<T>::iterator<br>list<T>::const_iterator<br>list<T>::reverse_iterator<br>list<T>::const_reverse_iterator | Mutable bidirectional<br>Constant bidirectional<br>Mutable bidirectional<br>Constant bidirectional | <list> |
| vector | vector<T>::iterator<br>vector<T>::const_iterator<br>vector<T>::reverse_iterator<br>vector<T>::const_reverse_iterator | Mutable random access<br>Constant random access<br>Mutable random access<br>Constant random access | <vector> |
| deque | deque<T>::iterator<br>deque<T>::const_iterator<br>deque<T>::reverse_iterator<br>deque<T>::const_reverse_iterator | Mutable random access<br>Constant random access<br>Mutable random access<br>Constant random access | <deque> |

## Display 19.7 Some Sequential Container Member Functions

| MEMBER FUNCTION (c IS A CONTAINER OBJECT) | MEANING |
|---|---|
| c.size( ) | Returns the number of elements in the container. |
| c.begin( ) | Returns an iterator located at the first element in the container. |
| c.end( ) | Returns an iterator located one beyond the last element in the container. |
| c.rbegin( ) | Returns an iterator located at the last element in the container. Used with reverse_iterator. Not a member of sList. |
| c.rend( ) | Returns an iterator located one beyond the first element in the container. Used with reverse_iterator. Not a member of sList. |
| c.push_back(Element) | Inserts the Element at the end of the sequence. Not a member of sList. |
| c.push_front(Element) | Inserts the Element at the front of the sequence. Not a member of vector. |
| c.insert(Iterator, Element) | Inserts a copy of Element before the location of Iterator. |
| c.erase(Iterator) | Removes the element at location Iterator. Returns an iterator at the location immediately following. Returns c.end( ) if the last element is removed. |
| c.clear( ) | A void function that removes all the elements in the container. |
| c.front( ) | Returns a reference to the element in the front of the sequence. Equivalent to *c.begin(). |
| c1 == c2 | True if c1.size( ) == c2.size( ) and each element of c1 is equal to the corresponding element of c2. |
| c1 != c2 | !(c1 == c2) |
| All the sequence containers discussed in this section also have a default constructor, a copy constructor, and various other constructors for initializing the container to default or specified elements. Each also has a destructor that returns all storage for recycling, and a well-behaved assignment operator. |

Deque is pronounced "d-queue" or "deck" and stands for "doubly ended queue." A deque is a kind of super queue. With a queue you add data at one end of the data sequence and remove data from the other end. With a deque you can add data at either end and remove data from either end. The template class deque is a template class for a deque with a parameter for the type of data stored.

## ■ **THE CONTAINER ADAPTERS stack AND queue**

Container adapters are template classes that are implemented on top of other classes. For example, the stack template class is by default implemented on top of the deque template class, which means that buried in the implementation of the stack is a deque where all the data resides. However, you are shielded from this implementation detail and see a stack as a simple last-in/first-out data structure.

Other container adapters are the queue and priority_queue template classes. Stacks and queues were discussed in Chapter 17. A **priority queue** is a queue with the additional property that each entry is given a priority when it is added to the queue. If all entries have the same priority, then entries are removed from a priority queue in the same manner as they are removed from a queue. If items have different priorities, the higher-priority items are removed before lower-priority items. We will not discuss priority queues in any detail, but mention it for those who may be familiar with the concept.

Although an adapter template class has a default container class on top of which it is built, you may choose to specify a different underlying container, for efficiency or other reasons, depending on your application. For example, any sequence container may serve as the underlying container for the stack template class, and any sequence container other than vector may serve as the underlying container for the queue template class. The default underlying data structure is the deque for both the stack and the queue. For a priority_queue the default underlying container is a vector. If you are happy with the default underlying container type, then a container adapter looks like any other template container class to you. For example, the type name for the stack template class using the default underlying container is stack<int> for a stack of ints. If you wish to specify that the underlying container is instead the vector template class, you would use stack<int, vector<int> > as the type name. We will always use the default underlying container.

If you do specify an underlying container, be warned that you should not place two > symbols in the type expression without a space in between them, or the compiler can be confused. Use stack<int, vector<int> >, with a space between the last two >’s. Do not use stack<int, vector<int>>.

The member functions and other details about the stack template class are given in Display 19.8. For the queue template class these details are given in Display 19.9. A simple example of using the stack template class is given in Display 19.10.

## Self-Test Exercises

- 11. What kind of iterators (forward, bidirectional, or random-access) does the stack template adapter class have?
- 
- 12. What kind of iterators (forward, bidirectional, or random-access) does the queue template adapter class have?
- 
- 13. If s is a stack<char>, what is the type of the returned value of s.pop()?

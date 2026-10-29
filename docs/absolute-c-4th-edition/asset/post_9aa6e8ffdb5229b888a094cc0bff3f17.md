
## Display 17.19 An Iterator Class for Linked Lists (part 2 of 2)

```
41        return startVersion;
42    }
43    bool operator ==(const ListIterator& rightSide) const
44    { return (current == rightSide.current); }
45
46    bool operator !=(const ListIterator& rightSide) const
47    { return (current != rightSide.current); }
48
49    //The default assignment operator and copy constructor
50    //should work correctly for ListIterator.
51    private:
52        Node<T> *current;
53    };
54
55 } //ListNodeSavitch
56
57 #endif //ITERATOR_H
```

the dereferencing operator, *, produces the data member variable of the node pointed to. Only the data member variable is data. The pointer member variable in a node is part of the implementation detail that the user programmer should not need to be concerned with.

You can use the ListIterator class as an iterator for any class based on a linked list that uses the template class Node. As an example, we have rewritten the template class Queue so that it has iterator facilities. The interface for the template class Queue is given in Display 17.20. This definition of the Queue template is the same as our previous version (Display 17.16) except that we have added a type definition as well as the following two member functions:

```
Iterator begin() const { return Iterator(front); }
Iterator end() const { return Iterator(); }
//The end iterator has end().current == NULL.
```

Let's discuss the member functions first.

The member function begin() returns an iterator located at ("pointing to") the front node of the queue, which is the head node of the underlying linked list. Each application of the increment operator, ++, moves the iterator to the next node. Thus, you can move through the nodes, and hence the data, in a queue named q as follows:

```
for (i = q.begin(); Stopping_condition; i++)
    process *i //*i is the current data item.
```

## Display 17.20 Interface File for a Queue with Iterators Template Class

```
//This is the header file queue.h. This is the interface for the class
//Queue, which is a template class for a queue of items of type T, including
//iterators.
#ifndef QUEUE_H
#define QUEUE_H
#include "iterator.h"
using namespace ListNodeSavitch;

namespace QueueSavitch
{
    template<class T>
    class Queue
    {
    public:
        typedef ListIterator<T> Iterator;

        Queue();
        Queue(const Queue<T>& aQueue);
        Queue<T>& operator=(const Queue<T>& rightSide);
        virtual ~Queue();
        void add(T item);
        T remove();
        bool isEmpty() const;

        Iterator begin() const { return Iterator(front); }
        Iterator end() const { return Iterator(); }
        //The end iterator has end().current == NULL.
        //Note that you cannot dereference the end iterator.
    private:
        Node<T> *front;//Points to the head of a linked list.
        //Items are removed at the head
        Node<T> *back;//Points to the node at the other end of the linked
        //list.
        //Items are added at this end.
    };

}//QueueSavitch

#endif //QUEUE_H
```

> The definitions of Node<T> and ListIterator<T> are in the namespace ListNodeSavitch in the file iterator.h.

where i is a variable of the iterator type.

The member function end( ) returns an iterator whose current member variable is NULL. Thus, when the iterator i has passed the last node, the Boolean expression

```
i != q.end( )
```

changes from true to false. This is the desired Stopping_Condition. This queue class and iterator class allow you to cycle through the data in the queue in the way we outlined for an iterator:

```
for (i = q.begin( ); i != q.end( ); i++)
    process /* //*i is the current data item.
```

Note that i is not equal to q.end( ) when i is at the last node. The iterator i is not equal to q.end( ) until it has been advanced one position past the last node. To remember this detail, think of q.end( ) as being an end marker like NULL; in this case it is essentially a version of NULL. A sample program that uses such a for loop is shown in Display 17.21.

Notice the type definition in our new template class:

```
typedef ListIterator<T> Iterator;
```

This typedef is not absolutely necessary. You can always use ListIterator<T> instead of the type name Iterator. However, this type definition does make for cleaner code. With this type definition, an iterator for the class Queue<char> is written

```
Queue<char>::Iterator i;
```

This makes it clear with which class the iterator is meant to be used.

The implementation of our new template class Queue is given in Display 17.22. Since the only member functions we added to this new Queue class are defined inline, the implementation file contains nothing really new, but we include the implementation file to show how it is laid out and to show which directives it would include.

## Display 17.21 Program Using the Queue Template Class with Iterators (part 1 of 2)

```
//Program to demonstrate use of the Queue template class with iterators.
#include "iostream"
#include "vector.h"//not needed
#include "queue.cpp"
#include "iterator.h"//not needed
using std::cin;
using std::cout;
using std::endl;
using namespace QueueSavitch;

int main( )
{
    char next, ans;
    do
    {
        Queue<char> q;
        cout << "Enter a line of text:\n";
        cin.get(next);
        while (next != '\n')
        {
            q.add(next);
            cin.get(next);
        }

        cout << "You entered:\n";
        Queue<char>::Iterator i;

        for (i = q.begin( ); i != q.end( ); i++)
            cout << *i;
        cout << endl;

        cout << "Again?(y/n): ";
        cin >> ans;
        cin.ignore(10000, '\n');
    }while (ans != 'n' && ans != 'N');

    return 0;
}
```

Even though they are not needed, many programmers prefer to include these include directives for the sake of documentation.

If your compiler is unhappy with Queue<char>::Iterator i; try using namespace ListNodeSavitch; ListIterator<char> i;

## Display 17.21 Program Using the Queue Template Class with Iterators (part 2 of 2)

# SAMPLE DIALOGUE

```
Enter a line of text:
Where shall I begin?
You entered:
Where shall I begin?
Again?(y/n): y
Enter a line of text:
Begin at the beginning
You entered:
Begin at the beginning
Again?(y/n): n
```

## Display 17.22 Implementation File for a Queue with Iterators Template Class (part 1 of 2)

```
1 //This is the file queue.cpp. This is the implementation of the template
2 //class Queue. The interface for the template class Queue is in the header
3 //file queue.h.
4 #include <iostream>
5 #include <cstdlib>
6 #include <cstddef>
7 #include "queue.h"
8 using std::cout;

9 using namespace ListNodeSavitch;
10 namespace QueueSavitch
11 {
12   template<class T>
13   Queue<T>::Queue() : front(NULL), back(NULL)
14     <The rest of the definition is given in the answer to Self-Test Exercise 14.>
15   template<class T>
16   Queue<T>::Queue(const Queue<T>& aQueue)
17     <The rest of the definition is given in the answer to Self-Test Exercise 17.>
18   template<class T>
19   Queue<T>& Queue<T>::operator =(const Queue<T>& rightSide)
20     <The rest of the definition is given in the answer to Self-Test Exercise 18.>
```

> The member function definitions are the same as in the previous version of the Queue template. This is given to show the file layout and use of namespaces.

## Display 17.22 Implementation File for a Queue with Iterators Template Class (part 2 of 2)

```
21  template<class T>
22  Queue<T>::~Queue( )
23  <The rest of the definition is given in the answer to Self-Test Exercise 16.>
24
25  template<class T>
26  bool Queue<T>::isEmpty( ) const
27  <The rest of the definition is given in the answer to Self-Test Exercise 14.>
28
29  template<class T>
30  void Queue<T>::add(T item)
31  <The rest of the definition is given in the answer to Self-Test Exercise 15.>
32
33  template<class T>
34  T Queue<T>::remove( )
35  <The rest of the definition is given in the answer to Self-Test Exercise 15.>
36  }//QueueSavitch
37  #endif //QUEUE_H
```

## Self-Test Exercises

19. Write the definition of the template function inQ shown below. Use iterators. Use the definition of Queue given in Display 17.20.

```
template<class T>
bool inQ(Queue<T>& q, T target);
//Returns true if target is in the queue q;
//otherwise, returns false.
```

## 17-4 Trees

> I think that I shall never see a data structure as useful as a tree.
> 
> Anonymous

A detailed treatment of trees is beyond the scope of this chapter. The goal of this chapter is to teach you the basic techniques for constructing and manipulating data structures based on nodes and pointers. The linked list served as a good example for our discussion. However, there is one detail about the nodes in a linked list that is quite restricted: They have only one pointer member variable to point to another node. A

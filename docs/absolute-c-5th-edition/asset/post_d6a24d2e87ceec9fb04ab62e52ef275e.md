
# 766 CHAPTER 17 Linked Data Structures

Display 17.18 Program Using the Stack Template Class (part 1 of 2)

Sample Dialog

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_795_0.png)

> The ignore member of cin is discussed in Chapter 9. It discards input remaining on the line.

# Linked List Applications

Display 17.18 Program Using the Stack Template Class (part 2 of 2)

```
Enter a line of text:
I love C++
Written backward that is:
++C evol I
Again?(y/n): n
```

Display 17.19 Implementation of the Stack Template Class (part 1 of 2)

```cpp
// This is the implementation file stack.cpp.
// This is the implementation of the template class Stack.
// The interface for the template class Stack is in the header file
//stack.h

#include <iostream>
#include <cstdlib>
#include <cstddef>
#include "stack.h"
using std::cout;

namespace StackSavitch
{
    // Uses cstddef;
    template<class T>
    Stack<T>::Stack() : top(NULL)
    {
        // Implementation empty
    }

    template<class T>
    Stack<T>::Stack(const Stack<T>&)
// The definition of the copy constructor is Self-Test Exercise 14.

    template<class T>
    Stack<T>& Stack<T>::operator=(const Stack<T>& rightSide)
// The definition of the overloaded assignment operator is Self-Test Exercise 15.

    template<class T>
    Stack<T>::~Stack()
    {
        T next;
```

(continued)

# 768 CHAPTER 17 Linked Data Structures

Display 17.19 Implementation of the Stack Template Class (part 2 of 2)

```cpp
27    while (! isEmpty())
28        next = pop(); //pop calls delete.
29    }
31    //Uses cstddef
32    template<class T>
33    bool Stack<T>::isEmpty() const
34    {
35        return (top == NULL);
36    }
37    void Stack<T>::push(T stackFrame)
39    <The rest of the definition is Self-Test Exercise 13.3.>.

40    //Uses cstdlib and iostream:
41    template<class T>
42    T Stack<T>::pop ()
43    {
44        if (isEmpty())
45        {
46            cout << "Error: popping an empty stack.\n";
47            exit (1);
48        }

49
50        T result = top->getData();

51        Node<T>*discard;
52        discard = top;
53        top = top->getLink();

54        delete discard;
55        return result;
56    }
57    } //StackSavitch
```

# Linked List Applications 769

# EXAMPLE: (continued)

variable top is a pointer that points to the head of the linked list. The pointer top serves the same purpose as the pointer head did in our previous discussions of linked lists.

Self-Test Exercise 13 is to write the definition of the member function push. However, we have already given the algorithm for this task. The code for the push member function is essentially the same as the function headInsert shown in Display 17.15, except that in the function push we use a pointer top in place of a pointer named head.

An empty stack is just an empty linked list, so an empty stack is implemented by setting the pointer top to NULL. Once that NULL represents the empty stack, the implementations of the default constructor and the member function are obvious.

The definition of the copy constructor is a bit more complicated and does not use any techniques we have not already discussed. The details are left to Self-Test Exercise 14.

The pop member function first checks to see if the stack is empty. If it is not, it proceeds to remove the top character in the stack. It sets the local variable result to the top symbol on the stack as:

```
result = top->getData();
```

After the data in the top node is saved in the variable result, the pointer top is moved to the next node in the linked list, effectively removing the top node from the list. The pointer top is moved with the statement

```
top = top->getLink();
```

However, before the pointer is moved, a temporary pointer, called discard, is positioned so that it points to the node that is about to be removed from the list. The storage for the removed node can then be recycled with the following call to delete:

```
delete discard;
```

Each node that is removed from the linked list by the member function pop has its memory recycled with a call to delete, so that the destructor needs to remove each item from the stack with a call to pop. Each node will then have its memory returned to the free store for recycling.

# Stacks

A stack is a last-in/first-out data structure; that is, data items are retrieved in the opposite order to which they were placed in the stack.

# Push and Pop

Adding a data item to a stack is referred to as pushing the onto the stack. Removing a data item from a stack is referred to as popping off the stack.

# Self-Test Exercises

13. Give the definition of the member function push of the template class Stack shown in Display 17.19.
14. Give the definition of the copy constructor of the template class Stack shown in Display 17.19.
15. Give the definition of the overloaded assignment operator for the template class Stack shown in Display 17.19.

# EXAMPLE: A Queue Class

A stack is a last-in/first-out data structure. Another common data structure is the queue, which handles data in first-in/first-out fashion. A queue can be implemented with a linked list in a manner similar to that of the stack. However, a queue needs a pointer at both locations. It is easier to remove from the head of the list than from the end of the linked list. Therefore, we will call the head of the list front and the end of the list back. The definition of the queue is shown in Display 17.20. A sample application of the queue is shown. The definitions of the member functions are left to the end of the chapter for you to fill in.

# Display 17.20 Interface for a Queue Class (part 1 of 2)

```cpp
//This is the header file queue.h. This is the interface for
//Queue, which is a template class for items of type T. This is the same definition of the stack we gave in Display 17.17. See the "Tip: Namespaces" for duplication.
#ifndef QUEUE_H
#define QUEUE_H

namespace QueueSavitch
{
template<class T>
class Node
{
public:
    Node(T data, Node<T>* theLink) : data(data), link(theLink){}
    Node<T>* getLink() const { return link; }
    const getData() const { return data; }
    void setData(const T& data) { data = data; }
    void setLink(Node<T>* pointer) { link = pointer; }
private:
    T data;
    Node<T>* link;
};

template<class T>
class Queue
{
public:
    Queue(); //Initializes the object to an empty queue.
    Queue<T>& operator=(const Queue<T>& rightSide);
    virtual ~Queue(); //Destroys the queue and returns all the memory to the freepstore.
    void add(T item); //Postcondition: item has been added to the back of the queue.
    T remove(); //Precondition: The queue is not empty. Returns the item at the front of the queue and removes that item from the queue.
    bool isEmpty() const //Returns true if the queue is empty. Returns false otherwise.
private:
    Node<T>*front; //Points to the head of a linked list Items are removed at the head
    Node<T>*back;  //Points to the node at the other end of the linked list. Items are added at this end.
};

#endif // QUEUE_H
```

# Display 17.20 Implementation File for a Queue Class (part 2 of 2)

```cpp
//This is the implementation file queue.cpp. This is the implementation
//of the template class Queue.
#include <iostream>
#include <cstdlib>
#include "queue.h"

namespace QueueSavitch
{
template<class T>
Queue<T>::Queue() : front(NULL), back(NULL)
{
}

template<class T>
Queue<T>& Queue<T>::operator=(const Queue<T>& rightSide)
{
    // The definition of the overloaded assignment operator is Self-Test Exercise 15.
    return *this;
}

template<class T>
Queue<T>::~Queue()
{
    while (! isEmpty())
    {
        remove();
    }
}

template<class T>
bool Queue<T>::isEmpty() const
{
    return (front == NULL);
}

template<class T>
void Queue<T>::add(T item)
{
    Node<T>* newNode = new Node(item, NULL);
    if (back == NULL)
    {
        front = back = newNode;
    }
    else
    {
        back->setLink(newNode);
        back = newNode;
    }
}

template<class T>
T Queue<T>::remove()
{
    if (isEmpty())
    {
        cout << "Error: popping an empty queue.\n";
        exit(1);
    }
    Node<T>* temp = front;
    T result = temp->getData();
    front = front->getLink();
    if (front == NULL)
    {
        back = NULL;
    }
    delete temp;
    return result;
}

} //QueueSavitch
```

# Display 17.21 Program Using the Queue Template Class (part 1 of 2)

```cpp
//Program to demonstrate use of the Queue template class.
#include <iostream>
#include "queue.h"
#include "queue.cpp"
using std::cin;
using std::cout;
using std::endl;
using QueueSavitch::Queue;
int main() {
    char next, ans;
    do {
        Queue<char> q;
        cout << "Enter a line of text:\n";
        cin.get(next);
        while (next != '\n')
            {
                q.add(next);
                cin.get(next);
            }
        cout << "You entered:\n";
    } while (! q.isEmpty())
        cout << q.remove();
    cout << endl;
}
```

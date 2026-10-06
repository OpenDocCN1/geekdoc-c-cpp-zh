# 418 10 Generic Programming and the Standard Template Library

```
int main()
{
    queue<int> intDequeQueue; //use queue as the default container
    for (int i = 0; i < 10; ++i ) {
        intDequeQueue.push( i ); //push the integer in deque as the
                                //top of the queue
    }

    cout << "Popping from intDequeQueue: ";
    popElements(intDequeQueue); //pop the top element of the queue
                                //and print

    cout << endl;
}
```

```
template< class T>
void popElements(T &s ) //define a template function
{
    while (!s.empty()) {
        cout << s.front() << ' '; //use front to get top element of
                                //Queue and print
        s.pop(); //use pop to remove the top element
    }
}
```

Results:

| Popping from intDequeQueue: 0 1 2 3 4 5 6 7 8 9 |

Similar to stacks and queues, a priority queue is another adapter for implementing an advanced data structure. Priority queues are designed as ordered queues, which are able to extract the highest priority element from a queue.

# 10.3 Iterators

Iterators are an object-oriented version of a pointer. They provide a uniform mechanism with which to traverse through a container. Pointers point to a memory location, so that program is able to access the object at the memory location through the pointer. You can see iterator as a type-safe pointer – it points to an object of a specific type.
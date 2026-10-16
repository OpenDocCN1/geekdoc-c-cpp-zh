The operations provided for queue<T> are similar to those for stack<T>:

+   - bool empty() — returns true if and only if there are no values in the queue.
+   - void push(T aValue) — append aValue to the end of the queue.
+   - void pop() — remove the value at the front of the queue.
+   - T front() — retrieve (but do not remove) the T value that is at the front of the queue.
+   - T back() — retrieve (but do not remove) the T value that is at the end of the queue.

Implementations of most of these are similar to those for stack<T> and are essentially just renamings of the container being adapted. Here, for example, is a definition of push():

```
template<class T, class Container>
inline void queue<T, Container>::push(T aValue)
{
    myContainer.push_back(aValue);
}
```

As with a stack<T>, when we send the push() message to a queue<T>, the value being added is appended to the back of the queue’s container using push_back(). However, for the pop() operation, the value is removed from the front of the container:

```
template<class T, class Container>
inline void queue<T, Container>::pop()
{
    myContainer.pop_front();
}
```

This is why a queue<T> cannot adapt a vector<T>. Inserting and/or deleting at the front of an array or vector<T> requires extensive copying that is very inefficient. To discourage programmers from writing inefficient code, vector<T> does not provide pop_front() or push_front() methods. Because we cannot send the pop_front() message to a vector<T>, we cannot use a vector<T> as the underlying container for a queue<T>.

Fortunately, this is not much of a hardship. The reason is that the default implementations of both stack<T> and queue<T> use a container called a deque, which we discuss next.

# 16.3.3 The deque<T> Container

The word deque stands for double-ended queue. It is a good container to use for any problem that requires the storage of a sequence of values and manipulation of the values at either end of that sequence.
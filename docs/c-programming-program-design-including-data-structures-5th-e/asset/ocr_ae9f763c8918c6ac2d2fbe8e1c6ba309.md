```
```cpp
cout << "Queue Elements: ";
while (!queue.isEmptyQueue())
{
    cout << queue.front() << " ";
    queue.deleteQueue();
}
cout << endl;
```
```

16. What does the following function do?

```
```cpp
void mystery(queueType<int> & q)
{
    stackType<int> s;

    while (!q.isEmptyQueue())
    {
        s.push(q.front());
        q.deleteQueue();
    }

    while (!s.isEmptyStack())
    {
        q.addQueue(2 * s.top());
        s.pop();
    }
}
```
```

17. Suppose that queue is a queueType object and the size of the array implementing queue is 100. Also, suppose that the value of queueFront is 50 and the value of queueRear is 99.

+   a. What are the values of queueFront and queueRear after adding an element to queue?
+   
+   b. What are the values of queueFront and queueRear after removing an element from queue?

18. Suppose that queue is a queueType object and the size of the array implementing queue is 100. Also, suppose that the value of queueFront is 99 and the value of queueRear is 25.

+   a. What are the values of queueFront and queueRear after adding an element to queue?
+   
+   b. What are the values of queueFront and queueRear after removing an element from queue?

19. Suppose that queue is a queueType object and the size of the array implementing queue is 100. Also, suppose that the value of queueFront is 25 and the value of queueRear is 75.

+   a. What are the values of queueFront and queueRear after adding an element to queue?
```
case 2:
    if (!stack.isEmptyStack())
    {
        cout << stack.top() << " ";
        stack.pop();
    }
    else if (!queue.isEmptyQueue())
    {
        cout << queue.front() << " ";
        queue.deleteQueue();
    }
    else
        cout << "Stack and queue are empty." << endl;
    break;
} //end switch

cin >> num;
} //end while
cout << endl;
cout << "stack: ";
while (!stack.isEmptyStack())
{
    cout << stack.top() << " ";
    stack.pop();
}

cout << endl;
cout << "queue: ";
while (!queue.isEmptyQueue())
{
    cout << queue.front() << " ";
    queue.deleteQueue();
}
cout << endl;
```

+   20. What does the following function do? (3, 9)

```
void mystery(queueType<int>& q)
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
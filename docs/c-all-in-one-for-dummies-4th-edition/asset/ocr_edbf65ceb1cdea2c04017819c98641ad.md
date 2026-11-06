```
```cpp
cout << MyStack.top() << endl;
MyStack.pop();

MyStack.push(40);
cout << MyStack.top() << endl;
MyStack.pop();

}

void QueueDemo() {
    cout << "===Queue Demo===" << endl;
    queue<int> MyQueue;
    MyQueue.push(5);
    MyQueue.push(10);
    MyQueue.push(15);

    cout << MyQueue.front() << endl;
    MyQueue.pop();
    cout << MyQueue.front() << endl;
    MyQueue.pop();

    MyQueue.push(40);
    cout << MyQueue.front() << endl;
    MyQueue.pop();
}

int main() {
    StackDemo();
    QueueDemo();
    return 0;
}
```
```

![](bbox=[0.163, 0.688, 0.228, 0.756])

When you specify a container to use inside the stack or queue, remember to put a space between the closing angle brackets. Otherwise, the compiler reads it as a single insertion operator, >>, and gets confused. Here is the output from this example:

```
```text
===Stack Demo===
15
10
40
===Queue Demo===
5
10
15
```
```
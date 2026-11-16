```
```cpp
// #include <queue> to use std::queue
std::queue<int> myQueue;
myQueue.push(10);
myQueue.push(20);
myQueue.push(30);
for (int i = 0; i < 3; i++)
{
    std::cout << myQueue.front() << ' ';
    myQueue.pop();
}
```
```
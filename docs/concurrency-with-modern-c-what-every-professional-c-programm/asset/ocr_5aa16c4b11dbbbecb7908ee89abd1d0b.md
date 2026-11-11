one node. Subsequent interleaving pop and push calls could race. For example, the tail->next call (line 30) might interleave with the oldHead->next call (line 23) in the end. This interleaving means, at the end, that I need one mutex to protect the entire data structure. Let me first answer your question. This queue implementation could not be made thread-safe by using two mutexes, but this implementation is the base for a thread-safe queue with fine-grained locking. I have to apply a trick to separate the head from the tail.

# 13.1.3.3 A Simple Queue with a Dummy Node

A dummy node does the trick. It separates the head from the tail. Now, the calls next on the head and the tail could not interleave. Of course, the implementation becomes more difficult because the dummy node has to be dealt with.

A Simple Queue with a Dummy Node

```
```cpp
// simpleQueueWithDummy.cpp

#include <iostream>
#include <memory>
#include <utility>

template <typename T>
class Queue{
private:
    struct Node{
        T data;
        std::unique_ptr<Node> next;
        Node(T data_): data(std::move(data_)){}
    };
    std::unique_ptr<Node> head;
    Node* tail;
public:
    Queue(): head(new Node(T{})), tail(head.get()){}
    std::unique_ptr<T> pop(){
        if (head.get() == tail) throw std::out_of_range("The queue is empty!");
        std::unique_ptr<T> res = std::make_unique<T>(std::move(head->data));
        std::unique_ptr<Node> oldHead = std::move(head);
        head = std::move(oldHead->next);
        if (!head) tail = nullptr;
        return res;
    }
    void push(T val){
        std::unique_ptr<Node> dummyNode = std::make_unique<Node>(Node(T{}));
        Node* newTail = dummyNode.get();
        tail->next= std::move(dummyNode);
```
```
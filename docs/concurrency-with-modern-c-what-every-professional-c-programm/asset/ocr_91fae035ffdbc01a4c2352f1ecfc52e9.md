# # A lock-free stack supporting push

```
```cpp
// lockFreeStackPush.cpp

#include <atomic>
#include <iostream>

template<typename T>
class LockFreeStackPush {
private:
    struct Node {
        T data;
        Node* next;
        Node(T d): data(d), next(nullptr) {}
    };
    std::atomic<Node*> head;
public:
    LockFreeStackPush() = default;
    LockFreeStackPush(const LockFreeStackPush&) = delete;
    LockFreeStackPush& operator= (const LockFreeStackPush&) = delete;

    void push(T val) {
        Node* const newNode = new Node(val);
        newNode->next = head.load();
        while ( !head.compare_exchange_strong(newNode->next, newNode) );
    }
};

int main() {

    LockFreeStackPush<int> lockFreeStack;
    lockFreeStack.push(5);

    LockFreeStackPush<double> lockFreeStack2;
    lockFreeStack2.push(5.5);

    LockFreeStackPush<std::string> lockFreeStack3;
    lockFreeStack3.push("hello");

}
```
```

Let me analyze the crucial member function push (line 20). It creates the new node (line 21), adjusts its next pointer to the old head, and makes the new node in a so-called CAS operation the new head (line 22). A CAS operation provides in an atomic step a compare and swap operation.
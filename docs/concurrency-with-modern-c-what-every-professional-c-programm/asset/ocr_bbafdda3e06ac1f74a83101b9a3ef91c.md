of nodes and deletes them if they aren't used anymore.

I need the following member function in a new implementation of TopAndPop based on the previous description: getHazardPointer to get a reference to a hazard pointer, retireList.addNode, and retireList.deleteUnusedNodes to add a node to the retire list retireList. Additionally retireList.deleteUnusedNodes to delete all nodes from the retire list that are not used anymore. Additionally, the member function retireList.deleteUnusedNodes uses the helper function retireList.isInUse that decides if a node is currently used. The member function isInUse is also handy in TopAndPop to decide if the current node should be added to the retire list or directly deleted.

What does this mean for my previous LockFreeStack implementation without memory reclamation? Let's see. The following program shows the lock-free stack implementation based on hazard pointers. I analyze it step by step.

# A lock-free stack using hazard pointers

```
```cpp
// lockFreeStackHazardPointers.cpp

#include <atomic>
#include <cstddef>
#include <future>
#include <iostream>
#include <stdexcept>
#include <thread>

template <typename T>
concept Node = requires(T a) {
    {T::data};
    { *a.next } -> std::same_as<T*>;
};

template <typename T>
struct MyNode {
    T data;
    MyNode* next;
    MyNode(T d): data(d), next(nullptr) { }
};

constexpr std::size_t MaxHazardPointers = 50;

template <typename T, Node MyNode = MyNode<T>>
struct HazardPointer {
    std::atomic<std::thread::id> id;
    std::atomic<MyNode*> pointer;
};

template <typename T>
```
```
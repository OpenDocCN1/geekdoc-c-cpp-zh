
**A lock-free stack supporting push**

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

Let me analyze the crucial member function push (line 20). It creates the new node (line 21), adjusts its next pointer to the old head, and makes the new node in a so-called CAS operation the new head (line 22). A CAS operation provides in an atomic step a compare and swap operation. The call `newNode->next = head.load()` loads the old value of head. If the loaded value `newNode->next` is still the same as head in line 23, head is updated to the `newNode` and the call `head.compare_exchange_strong` returns true. If not, the call returns false and the while loop is executed until the call returns true. `head.compare_exchange_strong` returns false if another thread added in the meantime a new node to the stack. When you apply `compare_exchange_strong` in a loop, you can also use `compare_exchange_weak`. `compare_exchange_weak` can spuriously fail and return false if head is equal to `newNode->next`. Due to the recursion, this would cause only an additional iteration.

Lines 22 and 23 build a kind of atomic transaction. First, you make a snapshot of the data structure (line 22), then you try to publish the transaction (line 23). If the snapshot is not valid anymore, you make a rollback and try it once more.

> **push is lock-free but not wait-free**
>
> The previous implementation of the member function push is lock-free but not wait-free. When many threads call `compare_exchange_strong` concurrently, only one thread can make progress. All other threads have to wait.

The simplified version has two issues. First, it does not have a pop operation, and second, it releases no memory. I address both issues in the next implementation.

## 14.2.2 A Complete Implementation

Typically, a stack supports the member functions push, pop, and top. Implementing the pop and top member functions thread-safe, does not guarantee that the invocation of top followed by pop is thread-safe. It may happen that one thread t1 called `stack.top()` and is interleaved by another thread t2 that called `stack.top()` and then `stack.pop()`. Now, the final `t1.pop()` call is based on the wrong stack size. Read more about this issue in the previous chapter about the concurrent stack.

### 14.2.2.1 No Memory Reclamation

Consequently, the following implementation combines both member functions top and pop into one: `topAndPop`.

**A lock-free stack supporting push and topAndPop**

```cpp
// lockFreeStackWithLeaks.cpp

#include <atomic>
#include <future>
#include <iostream>
#include <stdexcept>

template <typename T>
class LockFreeStack {
private:
    struct Node {
        T data;
        Node* next;
        Node(T d): data(d), next(nullptr) { }
    };
    std::atomic<Node*> head;
public:
    LockFreeStack() = default;
    LockFreeStack(const LockFreeStack&) = delete;
    LockFreeStack& operator= (const LockFreeStack&) = delete;

    void push(T val) {
        Node* const newNode = new Node(val);
        newNode->next = head.load();
        while( !head.compare_exchange_strong(newNode->next, newNode) );
    }

    T topAndPop() {
        Node* oldHead = head.load();
        while( oldHead && !head.compare_exchange_strong(oldHead, oldHead->next) ) {
            if ( !oldHead ) throw std::out_of_range("The stack is empty!");
        }
        return oldHead->data;
    }
};

int main(){

    LockFreeStack<int> lockFreeStack;

    auto fut = std::async([&lockFreeStack]{ lockFreeStack.push(2011); });
    auto fut1 = std::async([&lockFreeStack]{ lockFreeStack.push(2014); });
    auto fut2 = std::async([&lockFreeStack]{ lockFreeStack.push(2017); });
}
```

```cpp
45  auto fut3 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
46  auto fut4 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
47  auto fut5 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
48
49  fut.get(), fut1.get(), fut2.get();
50
51  std::cout << fut3.get() << '\n';
52  std::cout << fut4.get() << '\n';
53  std::cout << fut5.get() << '\n';
54
55 }
```

The member function topAndPop returns the top element of the stack. It reads the head element of the stack (line 29) and make the next node the new head if oldHead is not a nullptr (line 30). oldHead is a nullptr if the stack is empty. I decided to throw an exception if the stack is empty (line 31). Returning a special non-value or returning a std::optional⁴³ is also a valid option. Copying the value has a downside. If the copy constructor of the value throws an exception such as std::bad_alloc⁴⁴, the value is lost. Finally, the member functions returns the head element (line 33).

The calls fut.get(), fut1.get(), fut2.get() (line 49) ensure that the associated promise runs. If you don't specify the launch policy, the promise may run lazily in the caller's thread. Lazily means that the promise will execute if and only if the future asks for its result with get or wait. You can also launch the promise in a separate thread:

Launching each promise in a separate thread

```cpp
    auto fut = std::async(std::launch::async, [&conStack]{ conStack.push(2011); });
    auto fut1 = std::async(std::launch::async, [&conStack]{ conStack.push(2014); });
    auto fut2 = std::async(std::launch::async, [&conStack]{ conStack.push(2017); });
```

Finally, the output of the program:

> ⁴³https://en.cppreference.com/w/cpp/utility/optional
>
> ⁴⁴https://en.cppreference.com/w/cpp/memory/new/bad_alloc

```cpp
class LockFreeStack {
public:
    struct Node {
        T data;
        std::shared_ptr<Node> next;
    };
    std::shared_ptr<Node> head;
public:
    LockFreeStack() = default;
    LockFreeStack(const LockFreeStack&) = delete;
    LockFreeStack& operator= (const LockFreeStack&) = delete;

    void push(T val) {
        auto newNode = std::make_shared<Node>();
        newNode->data = val;
        newNode->next = std::atomic_load(&head);
        while (!std::atomic_compare_exchange_strong(&head, &newNode->next, newNode)) {
        }
    }

    T topAndPop() {
        auto oldHead = std::atomic_load(&head);
        while( oldHead && !std::atomic_compare_exchange_strong(&head, &oldHead,
                    std::atomic_load(&oldHead->next)) ) {
            if ( !oldHead ) throw std::out_of_range("The stack is empty!");
        }
        return oldHead->data;
    }
};

int main() {
    LockFreeStack<int> lockFreeStack;

    auto fut = std::async([&lockFreeStack]{ lockFreeStack.push(2011); });
    auto fut1 = std::async([&lockFreeStack]{ lockFreeStack.push(2014); });
    auto fut2 = std::async([&lockFreeStack]{ lockFreeStack.push(2017); });

    auto fut3 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
    auto fut4 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
    auto fut5 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });

    fut.get(), fut1.get(), fut2.get();

    std::cout << fut3.get() << '\n';
    std::cout << fut4.get() << '\n';
    std::cout << fut5.get() << '\n';

}
```

This lock-free stack implementation is quite similar to the previous one without memory reclamation. The main difference is that the nodes are of type `std::shared_ptr<Node>`. All operations `std::shared_ptr<Node>` are done atomically by using the free atomic operations `std::atomic_load` (lines 25, and 32), and `std::atomic_compare_exchange_strong` (lines 26, and 31). The free atomics operations require a pointer. I want to emphasize it explicitly, the read operation of the next node in `oldHead->next` (line 32) must be atomic because `oldHead->next` can be used by other threads. Finally, here is the output of the program.

![](img/d61a6c83410484053b8892275d2fcc4f_637_0.png)

A lock-free stack based on smart pointers

Let’s jump nine years into the future and use C++20.

### 14.2.2.1.3 C++20

C++20 supports partial specializations of `std::atomic` for `std::shared_ptr` and `std::weak_ptr`. The following implementation puts the nodes of the lock-free stack into a `std::atomic<std::shared_ptr<Node>>`.

**A lock-free stack based on atomic smart pointers**

```cpp
// LockFreeStackWithAtomicSharedPtr.cpp

#include <atomic>
#include <future>
#include <iostream>
#include <stdexcept>
#include <memory>

template<typename T>
class LockFreeStack {
private:
    struct Node {
```

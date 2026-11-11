
节点以及删除不再使用的节点。

基于上述描述，在新的 `TopAndPop` 实现中，我需要以下成员函数：`getHazardPointer` 用于获取风险指针的引用，`retireList.addNode` 用于将节点添加到退役列表，`retireList.deleteUnusedNodes` 用于删除退役列表中所有不再使用的节点。此外，成员函数 `retireList.deleteUnusedNodes` 使用辅助函数 `retireList.isInUse` 来判断某个节点当前是否被使用。成员函数 `isInUse` 在 `TopAndPop` 中同样很方便，可以用来决定当前节点是应该被添加到退役列表还是直接删除。

这对之前没有内存回收的 `LockFreeStack` 实现意味着什么呢？我们来看看。下面的程序展示了基于风险指针的无锁栈实现。我来逐步分析它。

## 使用风险指针的无锁栈

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
struct HazardPointerOwner {
    HazardPointer<T> hazardPointer;
    bool isOwner;
    HazardPointerOwner(): isOwner(false) {
        for (std::size_t i = 0; i < MaxHazardPointers; ++i) {
            std::thread::id defaultId;
            if (HazardPointers<T>[i].id.load() == defaultId) {
                HazardPointers<T>[i].id.store(std::this_thread::get_id());
                hazardPointer = HazardPointers<T>[i];
                isOwner = true;
                break;
            }
        }
        if (!isOwner) throw std::bad_alloc();
    }
    ~HazardPointerOwner() {
        hazardPointer.pointer.store(nullptr);
        hazardPointer.id.store(std::thread::id());
    }
    std::atomic<MyNode*>& getPointer() {
        return hazardPointer.pointer;
    }
};

template <typename T, Node MyNode = MyNode<T>>
struct RetireList {
    struct RetiredNode {
        MyNode* node;
        RetiredNode* next;
        RetiredNode(MyNode* p) : node(p), next(nullptr) { }
        ~RetiredNode() {
            delete node;
        }
    };

    std::atomic<RetiredNode*> RetiredNodes;

    void addToRetiredNodes(RetiredNode* retiredNode) {
        retiredNode->next = RetiredNodes.load();
        while (!RetiredNodes.compare_exchange_strong(retiredNode->next, retiredNode));
    }

public:

    bool isInUse(MyNode* node) {
        for (std::size_t i = 0; i < MaxHazardPointers; ++i) {
            if (HazardPointers<T>[i].pointer.load() == node) return true;
        }
        return false;
    }

    void addNode(MyNode* node) {
        addToRetiredNodes(new RetiredNode(node));
    }

    void deleteUnusedNodes() {
        RetiredNode* current = RetiredNodes.exchange(nullptr);
        while (current) {
            RetiredNode* const next = current->next;
            if (!isInUse(current->node)) delete current;
            else addToRetiredNodes(current);
            current = next;
        }
    }

};

template<typename T, Node MyNode = MyNode<T>>
class LockFreeStack {

    std::atomic<MyNode*> head;
    RetireList<T> retireList;

public:
    LockFreeStack() = default;
    LockFreeStack(const LockFreeStack&) = delete;
    LockFreeStack& operator=(const LockFreeStack&) = delete;

    void push(T val) {
        MyNode* const newMyNode = new MyNode(val);
        newMyNode->next = head.load();
        while( !head.compare_exchange_strong(newMyNode->next, newMyNode) );
    }

    T topAndPop() {
        std::atomic<MyNode*>& hazardPointer = getHazardPointer<T>();
        MyNode* oldHead = head.load();
        do {
            MyNode* tempMyNode;
            do {
                tempMyNode = oldHead;
                hazardPointer.store(oldHead);
                oldHead = head.load();
            } while(oldHead != tempMyNode);
        } while( oldHead && !head.compare_exchange_strong(oldHead, oldHead->next) );
        if (!oldHead) throw std::out_of_range("The stack is empty!");
        hazardPointer.store(nullptr);
        auto res = oldHead->data;
        if ( retireList.isInUse(oldHead) ) retireList.addNode(oldHead);
        else delete oldHead;
        retireList.deleteUnusedNodes();
        return res;
    }
};

int main(){

    LockFreeStack<int> lockFreeStack;

    auto fut = std::async([&lockFreeStack]{ lockFreeStack.push(2011); });
    auto fut1 = std::async([&lockFreeStack]{ lockFreeStack.push(2014); });
    auto fut2 = std::async([&lockFreeStack]{ lockFreeStack.push(2017); });

    auto fut3 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
    auto fut4 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
    auto fut5 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
}
```

```cpp
template <typename T, Node MyNode = MyNode<T>>
class LockFreeStack;
```

你可以在我的博客文章 [ModernesCpp/concepts](https://www.modernescpp.com/index.php/tag/concepts)<sup>15</sup> 或我的 [C++20](https://leanpub.com/c20)<sup>16</sup> 书中阅读更多关于概念（concepts）的细节。

让我继续对无锁栈程序的分析。

### LockFreeStack

```cpp
template<typename T, Node MyNode = MyNode<T>>
class LockFreeStack {

    std::atomic<MyNode*> head;
    RetireList<T> retireList;

public:
    LockFreeStack() = default;
    LockFreeStack(const LockFreeStack&) = delete;
    LockFreeStack& operator= (const LockFreeStack&) = delete;

    void push(T val) {
        MyNode* const newNode = new MyNode(val);
        newNode->next = head.load();
        while( !head.compare_exchange_strong(newNode->next, newNode) );
    }

    T topAndPop() {
        std::atomic<MyNode*>& hazardPointer = getHazardPointer<T>();
        MyNode* oldHead = head.load();
        do {
            MyNode* tempMyNode;
            do {
                tempMyNode = oldHead;
                hazardPointer.store(oldHead);
                oldHead = head.load();
            } while( oldHead != tempMyNode );
        } while( oldHead && !head.compare_exchange_strong(oldHead, oldHead->next) );
        if ( !oldHead ) throw std::out_of_range("The stack is empty!");
        hazardPointer.store(nullptr);
        auto res = oldHead->data;
        if ( retireList.isInUse(oldHead) ) retireList.addNode(oldHead);
        else delete oldHead;
        retireList.deleteUnusedNodes();
        return res;
    }
};
```

<sup>15</sup> https://www.modernescpp.com/index.php/tag/concepts

<sup>16</sup> https://leanpub.com/c20

从并发角度来看，`push` 调用并不关键，因为 `head` 是在一个原子步骤中更新的。此外，`compare_exchange_strong`（第15行）调用保证了 `head` 始终是栈的当前栈顶。

由于风险指针的存在，`topAndPop` 的调用变得更加复杂。首先，函数 `getHazardPointer` 返回当前线程的风险指针引用（第19行）。调用 `hazardPointer.store(oldHead)`（第25行）使当前线程成为该风险指针的所有者，而调用 `hazardPointer.store(nullptr)`（第30行）则释放其所有权。首先，让我分析内层和外层的 do-while 循环（第21–28行）。内层 do-while 循环将风险指针设置为栈顶。当满足以下条件时，do-while 循环结束：`oldHead == tempNode`。如果 `oldHead` 仍然是当前无锁栈的栈顶，则这两个节点相等。`oldHead` 在第20行被赋值为一个节点，但可能不再是当前栈顶（第28行），因为另一个线程可能已经介入并处理了 `oldHead`。外层 do-while 循环应该与之前无锁栈实现中的类似。我在 while 循环中使用 `compare_exchange_strong` 进行迭代，并将 `head` 设置为 `oldHead->next`。结束时，`head` 是栈的栈顶。请注意，成员函数 `topAndPop` 应该返回栈顶的值并将其移除。在使用 `oldHead` 之前，我必须检查 `oldHead` 是否不是空指针。如果 `oldHead` 是空指针，则抛出异常。`topAndPop` 的其余部分很简单。调用 `retireList.isInUse(oldHead)` 检查 `oldHead` 是否仍在使用中。根据这个检查结果，如果 `oldHead` 尚未在退役列表中，则调用 `retireList.addNode`（第32行）将其添加到退役列表，否则直接删除（第33行）。最后调用 `retireList.deleteUnusedNodes`（第37行）是成员函数 `topAndPop` 中工作量最大的调用。成员函数 `retireList.deleteUnusedNodes` 遍历整个退役列表，并删除所有不再使用的节点。

出于性能考虑，`retireList.deleteUnusedNodes` 不应在每次调用 `topAndPop` 时都执行。一种改进策略是当退役列表的长度超过特定阈值时才调用成员函数 `deleteUnusedNodes`。例如，当退役列表的长度是栈长度的两倍时，至少可以删除一半的节点。这个阈值是在性能要求和内存消耗之间的一种权衡。

让我继续讲解自由函数 `getHazardPointer` 和退役列表。

## 自由函数 getHazardPointer

```cpp
template <typename T, Node MyNode = MyNode<T>>
std::atomic<MyNode*>& getHazardPointer() {
    thread_local static HazardPointerOwner<T> hazard;
    return hazard.getPointer();
}
```

函数 `getHazardPointer` 通过风险指针所有者 `hazard` 来引用一个风险指针。`hazard` 是一个线程局部静态变量。因此，每个线程都有自己的风险指针副本。


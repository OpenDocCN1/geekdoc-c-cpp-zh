
## Data Structures

inside. From the outside means that it is the responsibility of the caller (application) to protect the data. This outside perspective is the perspective I mainly used in this book until now. From inside means that the data structure is responsible for protecting itself. A data structure that protects itself so that no data race can appear is called thread-safe. This inside perspective is the perspective I write about in this and the next chapter.

First of all, what are the general considerations you have to keep in mind to design a concurrent data structure?

Implementing thread-safe data structures is special. Before I dive into each of these unique concerns, here is a concise overview, including the answers you have to give.

- **Locking Strategy:** Should the data structure support coarse-grained, fine-grained locking, or be lock-free? Coarse-grained locking might be easier to implement but introduces contention. A fine-grained implementation or a lock-free one is way more challenging.
- **The Granularity of the Interface:** The bigger the thread-safe data structure’s interface, the more difficult it becomes to reason about the concurrent usage of the data structure.
- **Typical Usage Pattern:** When readers use your data structure mainly, you should not optimize for writers.
- **Avoidance of Loopholes:** Don’t pass internals of your data structure to clients.
- **Contention:** Do concurrent client requests seldom or often use your data structure?
- **Scalability:** How is your data structure’s performance characteristic when the number of concurrent clients increases or the data structure is bounded?
- **Invariants:** Which invariant must hold for your data structure when used?
- **Exceptions:** What should happen if an exception occurs?

Of course, these considerations are dependent on each other. For example, using a coarse-grained locking strategy lets you think about the granularity of the interface and the invariants. In contrast, it may increase the contention on the data structure and break scalability.

Although the general considerations in this chapter apply to lock-based data structures and the lock-free data structures, most examples in this chapter use locks. I delay all detailed discussions about lock-free data structures to the dedicated chapter.

### 12.2 Locking Strategy

Should the data structure support coarse-grained, fine-grained locking or be lock-free? First of all, what do I mean by coarse-grained locking? Coarse-grained locking means that only one thread uses the data structure at one point in time. The thread-safe interface pattern when using one lock is a typical way to implement coarse-grained locking. Here is the straightforward idea of the thread-safe interface pattern.

- All interface member functions (`public`) should use a lock.
- All implementation member functions (protected and private) must not use a lock.
- The interface member functions call only protected or private member functions but no public member functions.

The thread-safe interface pattern has two nice properties: all public member functions are thread-safe by design and deadlock-free by design. The thread-safe interface is thread-safe because each public member function uses a lock and the thread-safe interface is deadlock-free because a public member function cannot invoke another public member function of the class. I assume the following implementation makes my point:

#### The Thread-Safe Interface

```cpp
// threadSafeInterface.cpp

#include <iostream>
#include <mutex>
#include <thread>

class Critical{

public:
    void interface1() const {
        std::lock_guard<std::mutex> lockGuard(mut);
        implementation1();
    }
    void interface2(){
        std::lock_guard<std::mutex> lockGuard(mut);
        implementation2();
        implementation3();
        implementation1();
    }
private:
    void implementation1() const {
        std::cout << "implementation1: "
                  << std::this_thread::get_id() << '\n';
    }
    void implementation2(){
        std::cout << "    implementation2: "
                  << std::this_thread::get_id() << '\n';
    }
    void implementation3(){
        std::cout << "        implementation3: "
                  << std::this_thread::get_id() << '\n';
    }

    mutable std::mutex mut;

};

int main(){

    std::cout << '\n';

    std::thread t1([] {
        const Critical crit;
        crit.interface1();
    });

    std::thread t2([] {
        Critical crit;
        crit.interface2();
        crit.interface1();
    });

    Critical crit;
    crit.interface1();
    crit.interface2();

    t1.join();
    t2.join();

    std::cout << '\n';

}
```

The thread-safe interface pattern sounds promising but also has an obvious drawback. The data structure implementing the thread-safe interface is a bottleneck because only one thread can use the data structure at one point in time. This characteristic means if you have many threads working concurrently on the data structure, you should look for more fine-grained locking. For example, instead of protecting the entire interface to a singly-linked list with one lock, you can use a lock on individual nodes of the singly-linked list.

Of course, the data structure can also be lock-free. I discuss the special challenges of lock-free data structures in the same chapter.

### 12.3 Granularity of the Interface

Assume you want to implement a lock-based wrapper ThreadSafeQueue for a std::deque. The following code snippet gives a rough idea of the ThreadSafeQueue.

```cpp
class ThreadSafeQueue{
  ...
public:
  bool empty() const;
  std::shared_ptr<int> pop();
  ...
private:
  std::deque<int> data;
  ...
};
```

For simplicity reasons, I only display the member functions empty and pop. empty returns if the ThreadSafeQueue is empty and pop returns and removes the head of the ThreadSafeQueue. The interface has the wrong granularity! Why? Assume that two threads want to perform the following function on the same threadSafeQueue.

```cpp
ThreadSafeQueue threadSafeQueue;

std::shared_ptr<int> getHead(){
  if ( !threadSafeQueue.empty() ){
    auto head = threadSafeQueue.pop();
    return head;
  }
  return std::shared_ptr<int>();
}
...
std::thread t1([&]{ auto res = getHead();
                    ...
                  });
std::thread t2([&]{ auto res = getHead();
                    ...
                  });
```

This code has a race condition which can cause undefined behavior. Between the check !threadSafeQueue.empty() that the queue is not empty and the removing of the head-element via threadSafeQueue.pop(), there is a time window. For example, the following interleaving can happen.

#### Undefined behavior with ThreadSafeQueue

| thread t1 | thread t2 |
| --- | --- |
| (1) threadSafeQueue.empty() == true | |
| | (2) threadSafeQueue.empty() == true |
| (3) auto head = threadSafeQueue.pop(); | |
| | (4) auto head = threadSafeQueue.pop(); |

If threadSafeQueue has only one element, the second call threadSafeQueue.pop() from thread t2 is undefined behavior. Although both member functions are thread-safe, the combination of both member functions has undefined behavior. The interface puts the burden to synchronize the access to threadSafeQueue on the client's shoulder. This is far from ideal.

Changing the granularity of the member functions on ThreadSafeQueue solves this issue quite elegantly. Just combine the two calls empty and pop into one member function.

```cpp
class ThreadSafeQueue {
...
public:
    std::shared_ptr<int> tryPop(){
        std::lock_guard<std::mutex> queLock(queMutex);
        if (!data.empty()){
            auto head = data.pop();
            return head;
        }
        return std::shared_ptr<int>();
    }
...
private:
    std::deque<int> data;
    mutable std::mutex queMutex;
...
};
```

### 12.4 Typical Usage Pattern

The typical usage pattern for a data structure is the read access. Reader-writer locks allow you to optimize for the read access. When you put a std::shared_timed_mutex into a std::shared_lock, the lock becomes a shared lock but when you put a std::shared_timed_mutex into a std::lock_guard or into a std::unique_lock, you get an exclusive lock.

A telephone book is a data structure that is more often read than modified and is, therefore, the ideal candidate for a reader-writer lock. Let me start with an exclusive lock to have an initial performance number. I have a telephone book with roughly 89,000 entries. Ten threads read all 89,000 names in an arbitrary order, and one thread adds 1 to a telephone number of each tenth family name. Of course, all threads run at the same time.

The following image shows you a part of the telephone book. Can you see the name/number pairs separated by a colon and the name separated from the number by a comma.

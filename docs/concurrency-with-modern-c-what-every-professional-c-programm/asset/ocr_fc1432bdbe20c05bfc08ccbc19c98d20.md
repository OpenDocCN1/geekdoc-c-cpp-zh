+   - **Performance:** the atomic smart pointers have a big advantage compared to the free `atomic_*` functions. The atomic versions are designed for the special use case and can internally have a `std::atomic_flag` as a kind of cheap [spinlock](https://en.wikipedia.org/wiki/Spinlock). Designing the non-atomic versions of the pointer functions to be thread-safe would be overkill where they are used in a single-threaded scenario. They would have a performance penalty.

The correctness argument is probably the most important one. Why? The answer lies in the proposal. The proposal presents a thread-safe singly-linked list that supports insertion, deletion, and searching of elements. This singly-linked list is implemented in a lock-free way.

# 2.3.3.1.7 A thread-safe singly linked list

```
```cpp
template<typename T> class concurrent_stack {
    struct Node { T data; shared_ptr<Node> next; };
    atomic_shared_ptr<Node> head;
    // The atomic shared pointer is used to ensure that the special
    // functions every time you touch the variable
    concurrent_stack() { }
public:
    concurrent_stack() = default;
    ~concurrent_stack() = default;
    class reference {
        shared_ptr<Node> p;
    public:
        reference(shared_ptr<Node> p) : p(p) { }
        T& operator*() { return p->data; }
        T* operator->() { return &p->data; }
    };

    auto find(T const& t) {
        auto p = head.load();  // in C++11: atomic_load(&head)
        while (p && p->next != t) {
            p = p->next;
        }
        return reference(move(p));
    }

    auto front() const {
        return reference(head);  // in C++11: atomic_load(&head)
    }

    void push_front(T const& t) {
        auto p = make_shared<Node>(t);
        p->next = head;         // in C++11: atomic_load(&head)
        p->next = head;
        while (!head.compare_exchange_weak(p, p->next)) { }
        // in C++11: atomic_compare_exchange_weak(&head, &p, p->next);
    }

    void pop_front() {
        auto p = head.load();
        while (p && !head.compare_exchange_weak(p, p->next)) { }
        // in C++11: atomic_compare_exchange_weak(&head, &p, p->next);
    }
};
```
```

A thread-safe singly linked list

¹⁰https://en.wikipedia.org/wiki/Spinlock
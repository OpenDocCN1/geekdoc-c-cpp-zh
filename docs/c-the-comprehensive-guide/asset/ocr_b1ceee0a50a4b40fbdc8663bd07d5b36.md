function safely returns a correct result at the moment of the call, as soon as it exits, other threads are free to call push() or pop().

```
```cpp
// https://godbolt.org/z/4j7njd763
#include <vector>

template<class T>
class MxStack {
public:
    bool isEmpty() const;
    void push(const T& t);
    void pop();
    const T& top() const;
};
```
```

**Listing 29.18** The interface to a multithreaded stack.

If the thread that evaluates isEmpty() acts on its result, it may be that this is no longer correct. The same is true for top() and pop(): the element that top() returns does not necessarily have to be the same one that pop() removes in parallel operation.

Consider the following listing.

```
```cpp
// https://godbolt.org/z/1boeTMMvf
MxStack<int> mxs{};
// ...
// more code
// ...
if( ! mxs.isEmpty() ) {             // ⚡ not safe
    const auto value = mxs.top();   // ⚡ not safe
    mxs.pop();                      // ⚡ not safe
    // ...
    // more code
    // ...
}
```
```

**Listing 29.19** Problematic code for the “MxStack”.

There are two possible data races here, the first between the calls to isEmpty() and mx.top(). Assume a stack mxs holds an element {3} and a thread reaches !isEmpty(). Because !isEmpty() is true, the then branch is entered. But at this moment, another thread is executing the preceding code and performs mx.pop()—and the last element is removed! Continuing with the first thread, it now executes top() on the empty stack in the if. This suddenly doesn't work anymore, even though !isEmpty() just assured that the container was not empty. This is a nasty trap.
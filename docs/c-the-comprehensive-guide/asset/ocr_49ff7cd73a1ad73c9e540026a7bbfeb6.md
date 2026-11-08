iterators remain valid. `load_factor` and `max_load_factor` are the interfaces to the table's load factor.

# 24.9  Container Adapters

The container adapters are not standalone containers, but rather contain one of the actual containers to hold their data. Externally, they offer methods to perform specialized tasks.

For example, you can choose what the underlying container should be for `stack`.

```
```cpp
// https://godbolt.org/z/6KMKj3Pxv
#include <stack>
void run(auto data) { /* ... */ }  // C++20, abbreviated function template
run(stack<int>{});                  // Default: uses vector<int>
run(stack<vector<int>>{});          // like the default
run(stack<int,list<int>>{});        // uses list<int>
```
```

**Listing 24.88** Adapters work with interchangeable implementations.

| Container | Description |
|---|---|
| `stack` | Last in, first out |
| `queue` | First in, first out |
| `priority_queue` | Remove the largest element very quickly |
| `flat_[multi]set[map]` | Associative container with contiguous layout |

**Table 24.10** Profile: The container adapters.

In this section, `Cont` or `C` stands for one of the container adapter types like `stack<int>` and `cont` for an instance of it—for example, `queue<double> cont;`. For element type, I use `Elem` or `E`, and for iterator types, I abbreviate with `It`:

+   - **`stack<Elem>`**  
+     You can add individual elements to a *stack* at the top and remove them from the same end—hence the term *last in, first out* (LIFO): the last element you added is the first one you get back.
+   - **`queue<Elem>`**  
+     A *queue* allows you to add individual elements at *one* end and remove them at the *other* end. This results in a *first in, first out* (FIFO) approach: the element that was inserted first among several is also the first one you get back.
+   - **`priority_queue<Elem>`**  
+     The addition of elements to a priority queue is performed without regard to their
# 24.9 Container Adapters

The container adapters are not standalone containers, but rather contain one of the actual containers to hold their data. Externally, they offer methods to perform specialized tasks.

For example, you can choose what the underlying container should be for stack.

```
// https://godbolt.org/z/6KMj3Pvx
#include <stack>
void run(auto data) { /* ... */ // C++20, abbreviated function
template
run(stack<int>()); // // Default: uses vector<int>
run(stack<int,vector<int>>); // like the default
run(stack<int,list<int>>); // uses list<int>
```

**Listing 24.88** Adapters work with interchangeable implementations.

| Container | Description |
| --- | --- |
| stack | Last in, first out |
| queue | First in, first out |
| priority_queue | Remove the largest element very quickly |
| flat_[multi]{set|map} | Associative container with contiguous layout |

**Table 24.10** Profile: The container adapters.
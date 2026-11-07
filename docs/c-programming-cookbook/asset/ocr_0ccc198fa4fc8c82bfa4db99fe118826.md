list. Since list is a doubly-linked list, each element maintains a link to both its previous and next elements, allowing bidirectional traversal.

# Key Operations

Insertion and Deletion: You can insert or delete elements at any position without needing to shift elements, as is necessary with contiguous storage containers.

Traversal: You can traverse in both directions, which is particularly useful for algorithms that need to look ahead or behind without re-traversing the list.

Following is the sample program to utilize list:

```
```cpp
#include

#include

int main() {

std::list<_string> userActivities{"Logged in", "Viewed dashboard", "Logged out"};
```
```
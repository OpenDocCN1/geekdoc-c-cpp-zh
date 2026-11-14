to the preceding containers, we cannot access the n-th entry directly. An advantage over vector and deque is that insertion and deletion in the middle are less expensive.

List entries are never moved when others are inserted or deleted. Thus, only references and iterators of deleted entries are invalidated while all others keep their validity.

```
int main ()
{
    list<int> l = { 3, 4, 7, 9 };
    auto it = find(begin(l), end(l), 4), it2 = find(begin(l), end(l), 7);
    l.erase(it);
    cout << "it2 still points to " << *it2 << '\n';
}
```

The dynamic memory handling on each individual entry scatters them in the memory as illustrated in Figure 4-6 so that unfortunate cache behavior causes poorer performance than for vector and deque. Lists are more efficient for some operations but slower for many others so the overall performance is seldom better for list; compare, for instance, [28] or [52]. Fortunately, such performance bottlenecks can be quickly overcome in generically programmed applications by just changing the container types.

An entry of our list<int> takes 20 bytes on a typical 64-bit platform: two 8 bytes for the 64-bit pointers and 4 bytes for int. When the backward iteration is not needed, we can save the space for one pointer and use a forward_list (in <forward_list>).

# 4.1.3.4 Sets and Multisets

The purpose of a set container is to store the information that a value belongs to the set. The entries in the set are internally sorted as a tree so that they can be accessed with logarithmic complexity. The presence of a value in a set can be tested by the member functions find and

![](bbox=[0.12, 0.6, 0.92, 0.65])

Figure 4-5: Doubly-linked list (in theory)

![](bbox=[0.2, 0.71, 0.82, 0.85])

Figure 4-6: Doubly-linked list in practice
```
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
void pop_front();
void pop_back();
```

Effects: An erase operation that erases the last element of a deque invalidates only the past-the-end iterator and all iterators and references to the erased elements. An erase operation that erases the first element of a deque but not the last element invalidates only iterators and references to the erased elements. An erase operation that erases neither the first element nor the last element of a deque invalidates the past-the-end iterator and all iterators and references to all the elements of the deque.
[Note 1: pop_front and pop_back are erase operations. — end note]

Complexity: The number of calls to the destructor of T is the same as the number of elements erased, but the number of calls to the assignment operator of T is no more than the lesser of the number of elements before the erased elements and the number of elements after the erased elements.

Throws: Nothing unless an exception is thrown by the assignment operator of T.

# 22.3.8.5 Erasure [deque.erasure]

```
template<class T, class Allocator, class U>
typename deque<T, Allocator>::size_type
erase(deque<T, Allocator>& c, const U& value);
```

Effects: Equivalent to:

```
auto it = remove(c.begin(), c.end(), value);
auto r = distance(it, c.end());
c.erase(it, c.end());
return r;
```

```
template<class T, class Allocator, class Predicate>
typename deque<T, Allocator>::size_type
erase_if(deque<T, Allocator>& c, Predicate pred);
```

Effects: Equivalent to:

```
auto it = remove_if(c.begin(), c.end(), pred);
auto r = distance(it, c.end());
c.erase(it, c.end());
return r;
```

# 22.3.9 Class template forward_list [forwardlist]

# 22.3.9.1 Overview [forwardlist.overview]

A forward_list is a container that supports forward iterators and allows constant time insert and erase operations anywhere within the sequence, with storage management handled automatically. Fast random access to list elements is not supported.
[Note 1: It is intended that forward_list have zero space or time overhead relative to a hand-written C-style singly linked list. Features that would conflict with that goal have been omitted. — end note]

A forward_list meets all of the requirements of a container (Table 73), except that the size() member function is not provided and operator== has linear complexity. A forward_list also meets all of the requirements for an allocator-aware container (Table 76). In addition, a forward_list provides the assign member functions (Table 77) and several of the optional container requirements (Table 78). Descriptions are provided here only for operations on forward_list that are not described in that table or for operations where there is additional semantic information.

[Note 2: Modifying any list requires access to the element preceding the first element of interest, but in a forward_list there is no constant-time way to access a preceding element. For this reason, erase_after and splice_after take fully-open ranges, not semi-open ranges. — end note]

```
namespace std {
template<class T, class Allocator = allocator<T>>
class forward_list {
public:
// types
using value_type = T;
```
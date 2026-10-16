there is no general way of finding the previous element in a **forward_list** given only an iterator. Instead, **forward_iterator** provides operations, such as **insert_after()**, that operate after an element identified by an iterator. Similarly, unordered containers use **emplace_hint()** to provide a hint rather than “plain” **emplace()**.

# 31.3.8 Other Operations

Containers can be compared and swapped:

# Comparisons and Swap

**c1==c2** Do all corresponding elements of **c1** and **c2** compare equal?
**c1!=c2 !(c1==c2)**
**c1<c2** Is **c1** lexicographically before **c2**?
**c1<=c2 !(c2<c1)**
**c1>c2 c2<c1**
**c1>=c2 !(c1<c2)**
**c1.swap(c2)** Exchanges values of **c1** and **c2**; noexcept
**swap(c1,c2) c1.swap(c2)**

When comparing containers with an operator (e.g., <=), the elements are compared using the equivalent element operator generated from == or < (e.g., **a>b** is done using **!(b<a)**). The **swap()** operations exchange both elements and allocators.

# 31.4 Containers

This section goes into more detail about:

+   - **vector**, the default container (§31.4.1)
+   - The linked lists: **list** and **forward_list** (§31.4.2)
+   - The associative containers, such as **map** and **unordered_map** (§31.4.3)

# 31.4.1 vector

The STL **vector** is the default container. Use it unless you have a good reason not to. If your suggested alternative is a list or a built-in array, think twice.

§31.3 describes the operations on **vector** and implicitly contrasts them with what is provided for other containers. However, given the importance of **vector**, this section takes a second look with more emphasis on how the operations are provided.

The **vector**’s template argument and member types are defined like this:

```
template<typename T, typename Allocator = allocator<T>>
class vector {
public:
using reference = value_type&;
using const_reference = const value_type&;
using iterator = /* implementation-defined */;
```
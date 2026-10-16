# 31.4.1.4 **vector and string**

A `vector<char>` is a resizable, contiguous sequence of `char`s, and so is a `string`. So how do we choose between the two?

A **vector** is a general mechanism for storing values. It makes no assumptions about the relationships among the values stored in it. To a `vector<char>`, the string **Hello, World!** is just a sequence of 13 elements of type `char`. Sorting them into `!HWdelloor` (preceded by a space) makes sense. To contrast, a **string** is intended to hold character sequences. The relationships among the characters are assumed to be important. So, for example, we rarely sort the characters in a **string** because that destroys meaning. Some **string** operations reflect that (e.g., `c_str()`, `>>`, and `find()` “know” that Cstyle strings are zero-terminated). The implementations of **string** reflect assumptions about the way we use **strings**. For example, the short-string optimization (§19.3.3) would be a pure pessimization if it wasn’t for the fact that we use many short strings, so that minimizing free-store use becomes worthwhile.

Should there be a “short **vector** optimization”? I suspect not, but it would require a massive empirical study to be sure.

# 31.4.2 Lists

The STL provides two linked-list types:

+   - `list`: a doubly-linked list
+   - `forward_list`: a singly-linked list

A **list** is a sequence optimized for insertion and deletion of elements. When you insert into a **list** or delete an element from a **list**, the locations of other elements of the **list** are not affected. In particular, iterators referring to other elements are not affected.

Compared to **vector**, subscripting could be painfully slow, so subscripting is not provided for lists. If necessary, use `advance()` and similar operations to navigate lists (§33.1.4). A list can be traversed using iterators: **list** provides bidirectional iterators (§33.1.2) and **forward_list** provides forward iterators (hence the name of that type of list).

By default, **list** elements are individually allocated in memory and include predecessor and successor pointers (§11.2.2). Compared to a **vector**, a **list** uses more memory per element (usually at least four words more per element), and traversals (iteration) are significantly slower because they involve indirection through pointers rather than simple consecutive access.

A **forward_list** is a singly-linked list. Think of it as a data structure optimized for empty or very short lists that you typically traverse starting from the beginning. For compactness, **forward_list** doesn’t even provide a `size()`; an empty **forward_list** takes up just one word of memory. If you need to know the number of elements of a **forward_list**, just count them. If there are enough elements to make counting them expensive, maybe you should use a different container.

With the exception of subscripting, capacity management, and `size()` for **forward_list**, the
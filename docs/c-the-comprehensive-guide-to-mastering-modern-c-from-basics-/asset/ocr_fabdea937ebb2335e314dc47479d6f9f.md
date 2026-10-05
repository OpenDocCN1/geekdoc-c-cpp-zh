# Accessing

As with list, there is no index-based access. You also cannot navigate backward through a forward_list:

+   * Direct element access
`front()` gives you a reference to the first element of the list. The list must not be empty.

+   * Iterator access
`[c]begin()` gives you a forward iterator it the first element, and `[c]end()` points the last element. As usual, increment it with `++`. Ranges generated from a forward_list are forward ranges and thus suitable for many, but by no means for all algorithms. For forward_list, there are `before_begin()` and `cbefore_begin()` methods, which give you a “virtual” iterator element before begin().\ The returned iterator has a special role and can be used in conjunction with the `_after` methods. You can see an example in Listing 24.42.

The iterator returned by `before_begin()` and `c_begin()` must not be dereferenced. However, you need to insert an element at the very beginning of the list using `insert_after`, for example. If you increment it with `++`, it is identical to `begin()` or `cbegin()`.

Iterators remain valid when you delete or insert an element in the forward_list.

Useful Iterator Traits
In the `<iterator>` header, you will find useful tools related to iterators. For example, you can get a copy of it advanced by one with `next(it)`. I find this particularly useful with forward_list because you cannot go back with `--` or use `it`. Thus, you can effectively write `it+1` with `next(it)` without the iterator needing to support + as operation.

# Insert

Unfortunately, inserting is rather complicated with forward_list. You cannot insert at the position pointed to by an iterator, but only one element behind it. Figure 24.7 and Figure 24.8 show that the Fili node is not reachable from it. However, this would be necessary to break its link to `oin` and instead link to the new Bilbo node. We can only reach the Fili node by means of a loop that starts at `begin()`—and takes O(n) steps, so it is out of the question. The alternative
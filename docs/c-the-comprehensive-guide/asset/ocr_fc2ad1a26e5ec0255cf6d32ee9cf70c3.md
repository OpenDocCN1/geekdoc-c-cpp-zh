```
```cpp
numa.sort();    // sort as a method, not from <algorithm>
cout << numa; // Output: 1 2 3 4 5 6 7 8 9
}
```
```

**Listing 24.41** “splice” is the specialty of “list” and efficiently connects two lists.

Note my comment on `<<` in the box that followed [Listing 24.12](#).

With the other overloads of splice, you can transfer a single element or a range of *n* elements. Then the efficiency class is O(*n*). One often-overlooked method is merge. With this, you can combine two sorted lists into one sorted large list. This is better than combining two lists with splice followed by sort.

# 24.6.7   “forward_list”

The `forward_list` is different from all other containers. It stores its elements in a singly linked list. As a result, it has the smallest possible memory overhead for a list—namely, just one pointer per stored element.

However, this means that you can only navigate forward from an element and not backward. For example, if you want to insert an element at a given position it, you cannot reach the element before it to adjust its linking pointer.

As a solution, the designers of the standard library decided not to offer the necessary methods like `insert`, `emplace`, `erase`, and `insert_range`, as these could not be implemented efficiently. Instead, there are `insert_after`, `emplace_after`, `erase_after`, and `insert_range_after`, which act on an element “later” than is usual with other containers. For everyday use, this means that `forward_list` is operated completely differently from all other containers.

I therefore recommend using `forward_list` only when you *really* need it and all other containers have been ruled out as options.

Many of the methods are still identical to those of `vector` or `list`, especially those that relate to the entire container. I will therefore be brief here and only go into detail about the specialties of `forward_list`. For more examples, refer to [Section 24.6.3](#).

# Initialize

The `forward_list` offers all the usual container constructors that `list` and `vector` also offer: by default, with an initial size, a number of identical element copies, a complete copy or move, the initializer list, or a pair of iterators from another container. Starting from C++23, there is also a constructor with the `from_range` marker.
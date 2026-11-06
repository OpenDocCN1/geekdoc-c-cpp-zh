
```cpp
// replace contents of values with elements of otherValues
values.assign(otherValues.cbegin(), otherValues.cend());
cout << "\nAfter assign, values contains: ";
printList(values);

// remove otherValues elements and insert into values in sorted order
values.merge(otherValues);
cout << "\nAfter merge, values contains: ";
printList(values);

values.remove(4); // remove all 4s
cout << "\nAfter remove(4), values contains: ";
printList(values);
cout << endl;
}

// printList function template definition; uses
// ostream_iterator and copy algorithm to output list elements
template <typename T> void printList(const list<T>& listRef) {
    if (listRef.empty()) { // list is empty
        cout << "List is empty";
    }
    else {
        ostream_iterator<T> output(cout, " ");
        copy(listRef.cbegin(), listRef.cend(), output);
    }
}
```

```text
values contains: 2 1 4 3
values after sorting contains: 1 2 3 4
After insert, otherValues contains: 2 6 4 8
After splice, values contains: 1 2 3 4 2 6 4 8
After sort, values contains: 1 2 2 3 4 4 6 8
After insert and sort, otherValues contains: 2 4 6 8
After merge:
    values contains: 1 2 2 2 3 4 4 4 6 6 8 8
    otherValues contains: List is empty
After pop_front and pop_back:
    values contains: 2 2 2 3 4 4 4 6 6 8
After unique, values contains: 2 3 4 6 8
After swap:
    values contains: List is empty
    otherValues contains: 2 3 4 6 8
After assign, values contains: 2 3 4 6 8
After merge, values contains: 2 2 3 3 4 4 6 6 8 8
After remove(4), values contains: 2 2 3 3 6 6 8 8
```

Fig. 15.13 Standard Library `list` class template.

### Creating `list` Objects

Lines 14–15 create two `list` objects capable of storing `int`s. Lines 18–19 use function `push_front` to insert integers at the beginning of `values`. Function `push_front` is specific to classes `forward_list`, `list` and `deque`. Lines 20–21 use function `push_back` to insert integers at the end of `values`. *Function `push_back` is common to all sequence containers*, except `array` and `forward_list`.

### `list` Member Function `sort`

Line 26 uses `list` member function `sort` to arrange the elements in the `list` in *ascending order*. A second version of function `sort` allows you to supply a *binary predicate function* that takes two arguments (values in the list), performs a comparison and returns a `bool` value indicating whether the first argument should come before the second in the sorted contents. This function determines the order in which the elements of the `list` are sorted. This version could be particularly useful for a `list` that stores pointers rather than values. [*Note:* We demonstrate a *unary predicate function* in *Fig. 16.4*. A unary predicate function takes a single argument, performs a comparison using that argument and returns a `bool` value indicating the result.]

### `list` Member Function `splice`

Line 37 uses `list` function `splice` to remove the elements in `otherValues` and insert them into `values` before the iterator position specified as the first argument. There are two other versions of this function. Function `splice` with three arguments allows one element to be removed from the container specified as the second argument from the location specified by the iterator in the third argument. Function `splice` with four arguments uses the last two arguments to specify a range of locations that should be removed from the container in the second argument and placed at the location specified in the first argument. Class template `forward_list` provides a similar member function named `splice_after`.

### `list` Member Function `merge`

After inserting more elements in `otherValues` and *sorting* both `values` and `otherValues`, line 52 uses `list` member function `merge` to remove all elements of `otherValues` and insert them in sorted order into `values`. Both `list`s must be *sorted* in the same order before this operation is performed. A second version of `merge` enables you to supply a *binary predicate function* that takes two arguments (values in the list) and returns a `bool` value. The predicate function specifies the sorting order used by `merge`.

### `list` Member Function `pop_front`

Line 58 uses `list` function `pop_front` to remove the first element in the `list`. Line 59 uses function `pop_back` (available for *sequence containers* other than `array` and `forward_list`) to remove the last element in the `list`.

### `list` Member Function `unique`

Line 63 uses `list` function `unique` to *remove duplicate elements* in the `list`. The `list` should be in *sorted* order (so that all duplicates are side by side) before this operation is performed, to *guarantee* that all duplicates are eliminated. A second version of `unique` enables you to supply a *predicate function* that takes two arguments (values in the list) and returns a `bool` value specifying whether two elements are equal.

### `list` Member Function `swap`

Line 67 uses function `swap` (available to all *first-class containers*) to exchange the contents of `values` with the contents of `otherValues`.

### `list` Member Functions `assign` and `remove`

Line 74 uses `list` function **assign** (available to all *sequence containers*) to replace the contents of `values` with the contents of `otherValues` in the range specified by the two iterator arguments. A second version of `assign` replaces the original contents with copies of the value specified in the second argument. The first argument of the function specifies the number of copies. Line 83 uses `list` function **remove** to delete all copies of the value `4` from the `list`.

## 15.5.3 `deque` Sequence Container

Class `deque` provides many of the benefits of a `vector` and a `list` in one container. The term `deque` is short for “double-ended queue.”

Class `deque` is implemented to provide efficient indexed access (using subscripting) for reading and modifying its elements, much like a `vector`. Class `deque` is also implemented for *efficient insertion and deletion operations at its front and back*, much like a `list` (although a `list` is also capable of efficient insertions and deletions in the *middle* of the `list`). Class `deque` provides support for random-access iterators, so `deque`s can be used with all Standard Library algorithms. One of the most common uses of a `deque` is to maintain a *first-in, first-out queue* of elements. In fact, a `deque` is the default underlying implementation for the `queue` adaptor ([Section 15.7.2](#)).

Additional storage for a `deque` can be allocated at either end of the `deque` in blocks of memory that are typically maintained as a built-in array of pointers to those blocks.³ Due to the *noncontiguous memory layout* of a `deque`, a `deque` iterator must be more “intelligent” than the pointers that are used to iterate through `vector`s, `array`s or built-in arrays.

³. This is an implementation-specific detail, not a requirement of the C++ standard.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1938_0.png)

### Performance Tip 15.8

*In general*, `deque` has higher overhead than `vector`.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1938_1.png)

### Performance Tip 15.9

*Insertions and deletions in the middle of a `deque` are optimized to minimize the number of elements copied, so it’s more efficient than a `vector` but less efficient than a `list` for this kind of modification.*

Class `deque` provides the same basic operations as class `vector`, but like `list` adds member functions `push_front` and `pop_front` to allow insertion and deletion at the beginning of the `deque`, respectively.

[Figure 15.14](#) demonstrates features of class `deque`. Remember that many of the functions presented in [Fig. 15.10](#), [Fig. 15.11](#) and [Fig. 15.13](#) also can be used with class `deque`. Header `<deque>` must be included to use class `deque`.

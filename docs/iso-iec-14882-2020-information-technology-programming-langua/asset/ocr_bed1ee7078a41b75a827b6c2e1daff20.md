# 22.3.9.6 Operations [forwardlist.ops]

1 In this subclause, arguments for a template parameter named Predicate or BinaryPredicate shall meet the corresponding requirements in 25.2. For merge and sort, the definitions and requirements in 25.8 apply.

```
void splice_after(const_iterator position, forward_list& x);
void splice_after(const_iterator position, forward_list&& x);
```

2 Preconditions: position is before_begin() or is a dereferenceable iterator in the range [begin(), end()]. get_allocator() == x.get_allocator() is true. addressof(x) != this is true.

3 Effects: Inserts the contents of x after position, and x becomes empty. Pointers and references to the moved elements of x now refer to those same elements but as members of *this. Iterators referring to the moved elements will continue to refer to their elements, but they now behave as iterators into *this, not into x.

4 Throws: Nothing.

5 Complexity: 𝒪(distance(x.begin(), x.end()))

```
void splice_after(const_iterator position, forward_list& x, const_iterator i);
void splice_after(const_iterator position, forward_list&& x, const_iterator i);
```

6 Preconditions: position is before_begin() or is a dereferenceable iterator in the range [begin(), end()]. The iterator following i is a dereferenceable iterator in x. get_allocator() == x.get_allocator() is true.

7 Effects: Inserts the element following i into *this, following position, and removes it from x. The result is unchanged if position == i or position == ++i. Pointers and references to *++i continue to refer to the same element but as a member of *this. Iterators to *++i continue to refer to the same element, but now behave as iterators into *this, not into x.

8 Throws: Nothing.

9 Complexity: 𝒪(1)

```
void splice_after(const_iterator position, forward_list& x,
    const_iterator first, const_iterator last);
void splice_after(const_iterator position, forward_list&& x,
    const_iterator first, const_iterator last);
```

10 Preconditions: position is before_begin() or is a dereferenceable iterator in the range [begin(), end()]. (first, last) is a valid range in x, and all iterators in the range (first, last) are dereferenceable. position is not an iterator in the range (first, last). get_allocator() == x.get_allocator() is true.

11 Effects: Inserts elements in the range (first, last) after position and removes the elements from x. Pointers and references to the moved elements of x now refer to those same elements but as members of *this. Iterators referring to the moved elements will continue to refer to their elements, but they now behave as iterators into *this, not into x.

12 Complexity: 𝒪(distance(first, last))

```
size_type remove(const T& value);
template<class Predicate> size_type remove_if(Predicate pred);
```

13 Effects: Erases all the elements in the list referred to by a list iterator i for which the following conditions hold: *i == value (for remove()), pred(*i) is true (for remove_if()). Invalidates only the iterators and references to the erased elements.

14 Returns: The number of elements erased.

15 Throws: Nothing unless an exception is thrown by the equality comparison or the predicate.

16 Remarks: Stable (16.4.6.8).

17 Complexity: Exactly distance(begin(), end()) applications of the corresponding predicate.

```
size_type unique();
template<class BinaryPredicate> size_type unique(BinaryPredicate pred);
```

18 Effects: Erases all but the first element from every consecutive group of equal elements referred to by the iterator i in the range [first + 1, last) for which *i == *(i-1) (for the version with no
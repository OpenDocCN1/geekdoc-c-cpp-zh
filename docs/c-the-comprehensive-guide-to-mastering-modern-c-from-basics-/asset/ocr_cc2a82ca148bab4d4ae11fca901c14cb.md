# Insert

You insert into a multiset using the same overloads as in a set, with one exception: where set returns a pair<iterator,bool> to indicate via second whether an insertion actually took place, multiset only returns the iterator. Finally, multiset always inserts, regardless of whether the element already exists or not:

+   - Inserting a single element with automatic positioning
Use insert to insert a single value by copy, or emplacement to create the element directly in place. The return is a single iterator pointing to the inserted element—unlike in set, multiset inserts in O(log n) time, regardless of whether the element is already present or not.

+   - Inserting a single element with a position hint
If you provide an iterator along the value to be inserted, multiset also tries to interpret this iterator as a hint for insertion. If you do not want to pass a value but create it in place, use elapse_hint. You also know from set, and here too the amortized time complexity is O(1) if the hint is correct, and O(log n) if not.

+   - Inserting multiple elements
Like set, multiset also understands inserting multiple elements at once if you provide an initializer list or multiple via an iterator pair. From C++23 onward, there is also insert_range. As expected with multiset, all elements are transferred, including duplicates.

As with set, all iterators of the container remain valid after an insertion in multiset.

# Accessing

The interface of multiset for accessing is identical to that of set. Only the duplicate elements in the container need to be accounted for in the returns. Either they return any matching element or encompass the entire range of all matching elements:
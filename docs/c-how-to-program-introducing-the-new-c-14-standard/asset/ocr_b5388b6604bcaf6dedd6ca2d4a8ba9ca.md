elements are already in *sorted* order; otherwise, the two elements need to be reordered in the sequence.

# `binary_search` *Algorithm*

Line 57 uses the `binary_search` algorithm to determine whether the value 13 is in the range from `a.cbegin()` up to, but *not* including, `a.cend()`. The values must be sorted in *ascending order*. Algorithm `binary_search` requires its two iterator arguments to be at least *forward iterators*. The algorithm returns a `bool` indicating whether the value was found in the sequence. Line 65 demonstrates a call to `binary_search` in which the value is *not* found. An overloaded version of this algorithm receives as a fourth argument a *binary predicate function* with two arguments that are values in the sequence and returning a `bool`. The predicate function returns `true` if the two elements being compared are in *sorted order*. If you need to know the *location* of the search key in the container, use the `lower_bound` or `find` algorithms rather than `binary_search`.

# `C++11: all_of` *Algorithm*

Line 73 uses the `all_of` algorithm to determine whether the *unary predicate function* (the lambda stored in `isGreaterThan10`) returns `true` for all of the elements in the range from `a.cbegin()` up to, but *not* including, `a.cend()`. Algorithm `all_of` requires its two iterator arguments to be at least *input iterators*.
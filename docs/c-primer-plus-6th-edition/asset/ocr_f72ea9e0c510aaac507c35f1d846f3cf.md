# STL Functions 1287

Now let's take a more detailed look at these nonmodifying sequence operations. For each function, the discussion shows the prototype(s), followed by a brief explanation. Pairs of iterators indicate ranges, with the chosen template parameter name indicating the type of iterator. As usual in the range [first, last) goes from first up to, but not including, some functions take ranges, which need not be in the same kind of container. For example you use equal() to compare a list to a vector. Functions passed as argument are objects, which can be pointers (of which function names are an example) or objects for which the () operation is defined. As in Chapter 16, a predicate is a Boolean function with one argument, and a binary predicate is a Boolean function with two arguments. The functions need not be type bool, as long as they return 0 for false and a nonzero value for true.

# Table G.13 Nonmodifying Sequence Operations

| Function | Description |
| --- | --- |
| all_of() | Returns true if a predicate test is true for all elements. (C++11) |
| any_of() | Returns true if a predicate test is true for any element. (C++11) |
| none_of() | Returns true if a predicate test is false for all elements. (C++11) |
| for_each() | Applies a nonmodifying function object to each element in a range. |
| find() | Finds the first occurrence of a value in a range. |
| find_if() | Finds the first value that satisfies a predicate test criterion in a range. |
| find_if_not() | Finds the first value that doesn't satisfy a predicate test in a range. (C++11) |
| find_end() | Finds the last occurrence of a subsequence whose values match the values of a second sequence. Matching may be by equality or applying a binary predicate. |
| find_first_of() | Finds the first occurrence of any element of a second sequence that matches a value in the first sequence. Matching may be by equality or be evaluated with a binary predicate. |
| adjacent_find() | Finds the first element that matches the element immediately following it. Matching may be by equality or evaluated with a binary predicate. |
| count() | Returns the number of times a given value occurs in a range. |
| count_if() | Returns the number of times a given value matches values in a range, with a match determined by using a binary predicate. |
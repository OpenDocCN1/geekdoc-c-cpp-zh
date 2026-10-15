![](bbox=[0.141, 0.105, 0.857, 0.343])

**Fig. 20.30** | Mathematical algorithms of the Standard Library. (Part 3 of 3.)

Line 26 uses function **random_shuffle** to reorder randomly the elements in the range from `v.begin()` up to, but not including, `v.end()` in `v`. This function takes two random-access iterator arguments.

Line 36 uses function **count** to count the elements with the value 8 in the range from `v2.begin()` up to, but not including, `v2.end()` in `v2`. This function requires its two iterator arguments to be at least input iterators.

Line 40 uses function **count_if** to count elements in the range from `v2.begin()` up to, but not including, `v2.end()` in `v2` for which the predicate function **greater9** returns true. Function **count_if** requires its two iterator arguments to be at least input iterators.

Line 45 uses function **min_element** to locate the smallest element in the range from `v2.begin()` up to, but not including, `v2.end()`. The function returns a forward iterator located at the smallest element, or `v2.end()` if the range is empty. The function’s two iterator arguments must be at least input iterators. A second version of this function takes as its third argument a binary function that compares two elements in the sequence. This function returns the bool value true if the first argument is less than the second.

# Good Programming Practice 20.2

> It is a good practice to check that the range specified in a call to `min_element` is not empty and that the return value is not the “past the end” iterator.

Line 49 uses function **max_element** to locate the largest element in the range from `v2.begin()` up to, but not including, `v2.end()` in `v2`. The function returns an input iterator located at the largest element. The function’s two iterator arguments must be at least input iterators. A second version of this function takes as its third argument a binary predicate function that compares the elements in the sequence. The binary function takes two arguments and returns the bool value true if the first argument is less than the second.

Line 53 uses function **accumulate** (the template of which is in header file `<numeric>`) to sum the values in the range from `v.begin()` up to, but not including, `v.end()` in `v`. The function’s two iterator arguments must be at least input iterators and its third argument represents the initial value of the total. A second version of this function takes as its fourth argument a general function that determines how elements are accumulated. The general function must take two arguments and return a result. The first argument to this
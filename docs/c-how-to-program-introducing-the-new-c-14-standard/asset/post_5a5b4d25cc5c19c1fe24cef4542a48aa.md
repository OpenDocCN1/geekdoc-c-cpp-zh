
- **16.3**
  - B. Use the `generate` algorithm and the `nextInt` function to fill the `array` of `int`s named `integers`.
  - C. Use the `equal` algorithm to compare two lists (`strings1` and `strings2`) for equality. Store the result in `bool` variable `result`.
  - D. Use the `remove_if` algorithm to remove from the `vector` of `string`s named `colors` all of the strings that start with `"bl"`. Function `startsWithBl` returns `true` if its argument `string` starts with `"bl"`. Store the iterator that the algorithm returns in `newEnd`.
  - E. Use the `replace_if` algorithm to replace with `0` all elements with values greater than `100` in the `array` of `int`s named `values`. Function `greaterThan100` returns `true` if its argument is greater than `100`.
  - F. Use the `minmax_element` algorithm to find the smallest and largest values in the `array` of `double`s named `temperatures`. Store the `pair` of iterators that’s returned in `result`.
  - G. Use the `sort` algorithm to sort the `array` of `string`s named `colors`.
  - H. Use the `reverse` algorithm to reverse order of the elements in the `array` of `string`s named `colors`.
  - I. Use the `merge` algorithm to merge the contents of the two sorted `array`s named `values1` and `values2` into a third `array` named `results`.
  - J. Write a lambda expression that returns the square of its `int` argument and assign the lambda expression to variable `squareInt`.

## Exercises

- **16.4** State whether each of the following is *true* or *false*. If *false*, explain why.
  - A. Because Standard Library algorithms process containers directly, one algorithm can often be used with many different containers.
  - B. Use the `for_each` algorithm to apply a general function to every element in a range; `for_each` does not modify the sequence.
  - C. By default, the `sort` algorithm arranges the elements in a range in ascending order.
  - D. Use the `merge` algorithm to form a new sequence by placing the second sequence after the first.
  - E. Use the `set_intersection` algorithm to find the elements from a first set of sorted values that are not in a second set of sorted values (both sets of values must be in ascending order).
  - F. Algorithms `lower_bound`, `upper_bound` and `equal_range` are often used to locate insertion points in sorted sequences.
  - G. Lambda expressions can also be used where function pointers and function objects are used in algorithms.
  - H. C++11’s lambda expressions are defined locally inside functions and can “capture” (by value or by reference) the local variables of the enclosing function and then manipulate these variables in the lambda’s body.

- **16.5** Fill in the blanks in each of the following statements:
  - A. As long as a container’s (or built-in array’s) ____ satisfy the requirements of an algorithm, the algorithm can work on the container.
  - B. Algorithms `generate` and `generate_n` use a(n) ____ function to create values for every element in a *range* of container elements. That type of function takes no arguments and returns a value that can be placed in an element of the container.
  - C. Pointers into built-in arrays are ____ iterators.
  - D. Use the ____ algorithm (the template of which is in header `<numeric>`) to sum the values in a range.
  - E. Use the ____ algorithm to apply a general function to every element in a range when you need to modify those elements.
  - F. In order to work properly, the `binary_search` algorithm requires that the sequence of values must be ____.
  - G. Use the function `iter_swap` to exchange the elements that are pointed to by two ____ iterators and exchange the values in those elements.
  - H. C++11’s `minmax` algorithm receives two items and returns a(n) ____ in which the smaller item is stored in `first` and the larger item is stored in `second`.
  - I. ____ algorithms modify the containers they operate on.

- **16.6** List several advantages function objects provide over function pointers.

- **16.7** What happens when you apply the `unique` algorithm to a sorted sequence of elements in a range?

- **16.8 (Duplicate Elimination)** Read 20 integers into an `array`. Next, use the `unique` algorithm to reduce the `array` to the unique values entered by the user. Use the `copy` algorithm to display the unique values.

- **16.9 (Duplicate Elimination)** Modify **Exercise 16.8** to use the `unique_copy` algorithm. The unique values should be inserted into a `vector` that’s initially empty. Use a `back_inserter` to enable the `vector` to grow as new items are added. Use the `copy` algorithm to display the unique values.

- **16.10 (Reading Data from a File)** Use an `istream_iterator<int>`, the `copy` algorithm and a `back_inserter` to read the contents of a text file that contains `int` values separated by whitespace. Place the `int` values into a `vector` of `int`s. The first argument to the `copy` algorithm should be the `istream_iterator<int>` object that’s associated with the text file’s `ifstream` object. The second argument should be an `istream_iterator<int>` object that’s initialized using the class template `istream_iterator`’s default constructor—the resulting object can be used as an “end” iterator. After reading the file’s contents, display the contents of the resulting vector.

- **16.11 (Merging Ordered Lists)** Write a program that uses Standard Library algorithms to merge two ordered `lists` of strings into a single ordered list of strings, then displays the resulting list.

- **16.12 (Palindrome Tester)** A palindrome is a string that is spelled the same way forward and backward. Examples of palindromes include “radar” and “able was i ere i saw elba.” Write a function `palindromeTester` that uses the `reverse` algorithm on a copy of a `string`, then compares the original `string` and the reversed `string` to determine whether the original `string` is a palindrome. Like the Standard Library containers, `string` objects provide functions like `begin` and `end` to obtain iterators that point to characters in a `string`. Assume that the original `string` contains all lowercase letters and does not contain any punctuation. Use function `palindromeTester` in a program.

- **16.13 (Enhanced Palindrome Tester)** Enhance **Exercise 16.12**’s `palindromeTester` function to allow strings containing uppercase and lowercase letters and punctuation. Before testing whether the original string is a palindrome, function `palindromeTester` should convert the `string` to lowercase letters and eliminate any punctuation. For simplicity, assume the only punctuation characters can be `.,!;:()`. You can use the `copy_if` algorithm and a `back_inserter` to make a copy of the original `string`, eliminate the punctuation characters and place the characters into a new `string` object.

- **16.14** Explain why using the “weakest iterator” that yields acceptable performance helps produce maximally reusable components.

## Answers to Self-Review Exercises

### 16.1

- A. True.
- B. False. Standard Library algorithms are not member functions. They operate indirectly on containers, through iterators.
- C. True.
- D. False. Standard Library algorithms do not depend on the implementation details of the containers on which they operate.
- E. True.
- F. False. It locates only the first value in the range for which the specified unary predicate function returns `false`.
- G. True.

### 16.2

- A. Iterators.
- B. random-access.
- C. `fill`, `fill_n`.
- D. `equal`.
- E. `minmax_element`.
- F. `push_back`.
- G. function object.

### 16.3

- A. `fill(items.begin(), items.end(), "hello");`
- B. `generate(integers.begin(), integers.end(), nextInt);`
- C. `bool result{equal(strings1.cbegin(), strings1.cend(), strings2.cbegin())};`
- D. `auto newEnd = remove_if(colors.begin(), colors.end(), startsWithBl);`
- E. `replace_if(values.begin(), values.end(), greaterThan100, 0);`
- F. `auto result = minmax_element(temperatures.cbegin(), temperatures.cend());`
- G. `sort(colors.begin(), colors.end());`
- H. `reverse(colors.begin(), colors.end());`
- I. `merge(values1.cbegin(), values1.cend(), values2.cbegin(), values2.cend(), results.begin());`
- J. `auto squareInt = [](int i) { return i * i; };`

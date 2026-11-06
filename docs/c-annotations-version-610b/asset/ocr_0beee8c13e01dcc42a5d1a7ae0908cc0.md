```
```cpp
int main()
{
    string words[] = {"alpha", "bravo", "charley"};

    copy(words, transform(words, words + 3, caps),
         ostream_iterator<string>(cout, " "));
    cout << '\n';

    int        values[] = {1, 2, 3, 4, 5};
    vector<int> squares;

    transform(values, values + 5, values,
              back_inserter(squares), multiplies<int>());

    copy(squares.begin(), squares.end(),
         ostream_iterator<int>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        ALPHA BRAVO CHARLEY
        1 4 9 16 25
*/
```
```

the following differences between the `for_each` (section 19.1.17) and `transform` generic algorithms should be noted:

+   - With `transform` the *return value* of the function object's `operator()` member is used; the argument that is passed to the `operator()` member itself is not changed.
+   - With `for_each` the function object's `operator()` receives a reference to an argument, which itself may be changed by the function object's `operator()`.

# 19.1.64  unique

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `ForwardIterator unique(ForwardIterator first, ForwardIterator last);`
+     - `ForwardIterator unique(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);`

+   - Description:
+     - The first prototype: using `operator==` of the data type to which the iterators point, all but the first of consecutively equal elements in the range pointed to by `[first, last)` are relocated to the end of the range. The returned forward iterator marks the beginning of the *leftover*. All elements in the range `[first, return-value)` are unique, all elements in the range `[return-value, last)` are equal to elements in the range `[first, return-value)`.
+     - The second prototype: all but the first of consecutive elements in the range pointed to by `[first, last)` for which the binary predicate `pred` (expecting two arguments of the data type to which the iterators point) returns `true`, are relocated to the end of the range. The returned forward iterator marks the beginning of the *leftover*. For all pairs of elements in the range `[first, return-value)` `pred` returns `false` (i.e., they are unique), while `pred` returns `true` for a combination of, as its first operand, an element in the range `[return-value, last)`, and, as its second operand, an element in the range `[first, return-value)`.
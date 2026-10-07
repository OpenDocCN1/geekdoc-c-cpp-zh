# Table G.16 Sorting and Related Operations

| Function | Description |
| --- | --- |
| accumulate() | Calculates a cumulative total for values in a range. |
| inner_product() | Calculates the inner product of two ranges. |
| partial_sum() | Copies partial sums calculated from one range into a second range. |
| adjacent_difference() | Copies adjacent differences calculated from elements in one range to a second range. |
 iota() | Assigns consecutive values, as produced by the ++ operator, to elements in a range. (C++11) |

Now let's take a more detailed look at these numerical operations. For each function, the discussion shows the prototype(s), followed by a brief explanation.

# accumulate()

```
template <class InputIterator, class T>
T accumulate(InputIterator first, InputIterator last, T init);
```

```
template <class InputIterator, class T, class BinaryOperation>
T accumulate(InputIterator first, InputIterator last, T init,,
           BinaryOperation binary_op);
```

The accumulate() function initializes a value acc to init; then it performs the operation
acc = acc + *i (first version) or acc = binary_op(acc, *i) (second version) for each
iterator i in the range [first, last), in order. It returns the returning value of acc.

# inner_product()

```
template <class InputIterator1, class InputIterator2, class T>
T inner_product(InputIterator1 first1, InputIterator1 last1,
               InputIterator2 first2, T init);
```

```
template <class InputIterator1, class InputIterator2, class T,
class BinaryOperation1, class BinaryOperation2>
T inner_product(InputIterator1 first1, InputIterator1 last1,
               InputIterator2 first2, T init,
               BinaryOperation1 binary_op1, BinaryOperation2 binary_op2);
```

The inner_product() function initializes a value acc to init; then it performs the operation
acc = *i * j (first version) or acc = binary_op(*i, *j) (second version) for
each iterator i in the range [first1, last1), in order, and each corresponding iterator j
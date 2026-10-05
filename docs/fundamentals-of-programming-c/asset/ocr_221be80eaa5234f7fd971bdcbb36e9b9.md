# 18.4 Iterator Ranges

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
0 2 4 6 8 10 12 14 16 18
0 4 8 12 16
0 5 10 15
0 10
n19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0
18 16 14 12 10 8 6 4 2 0
16 12 8 4 0
15 10 5
10 0
```

Some specialized data structures in the C++ standard library support specialized iterators have some limits on the kinds of arithmetic they support; for example, some container types support forward but not backward traversal. Subtraction is not an option for these kinds of iterators.

Iterators are valuable for specifying ranges over sequences (vectors and arrays). We can specify a range with a pair of iterators: one iterator points to the first element in the sequence, and the other iterator points to the position just after the end of the sequence. The global functions begin and end well into this definition of range.

Suppose vec is a vector. The two iterators begin(vec) and end(vec) span the complete range of values in vec. In the following statement:

```
auto b = begin(vec), e = b + 1;
```

the range of two iterators b and e includes the first element in vec. Compare this range to the one represented by the following statement:

```
auto b = begin(vec), e = b + 10;
```

Here the range of two iterators b and e span the first 10 elements of vec. The range of the iterators b and e defined by the statement

```
auto e = end(vec), b = e - 5;
```

encompasses the last five elements of vec.

The iterator pair begin(vec), end(vec) specify the complete range of values in vector vec. The following function uses iterators to count the number of times a value appears within:

```
int count(vector<int>::iterator iter_begin,
            vector<int>::iterator iter_end, int seek) {
    int cnt = 0;
    for (vector<int>::iterator cursor = iter_begin;
         cursor != iter_end; ++cursor)
        if (cursor == seek)
            cnt++;
}
```
For example, suppose we create an array of type `int` storing the marks of a student. Then,

```
int marks[6] = (73, 44, 42, 51, 59, 50)
```

We can use STL `sort()` as

```
sort(marks, marks + 6)
```

Here, `marks` and `marks + 6` are the start and end addresses, respectively.

Other example of sorting a vector is as follows:

```
vector<int> m;
// having values 73, 44, 42, 51, 59, 50
sort(m.begin(), m.end());
// Output is 42, 44, 50, 51, 59, 73
sort(v.begin(), v.end(), greater<int>());
// Output is 73, 59, 51, 50, 44, 42
```

For reversing, we can use reverse algorithm as the following:

```
vector<int> m;
// vector m having values 73, 44, 42, 51, 59, 50
reverse(m.begin(), m.end());
// vector m changed as 50 59, 51, 42, 44, 73
```

Table 15.6 lists some of the functions in `<algorithm>`.

# Table 15.6 List of functions with their brief descriptions available in STL.

| Functions | Description |
|---|---|
| find() | Find value in range |
| find_if() | Find element in range |
| count() | Count appearances of value in range |
| equal() | Test whether the elements in two ranges are equal |
| copy() | Copy the range of elements |
| swap() | Exchange values of two objects |
| replace() | Replace value in range |
| fill() | Fill range with value |
| remove() | Remove value from range |
| reverse() | Reverse range |
| sort() | Sort elements in range |
| partial_sort() | Partially sort elements in range |
| nth_element() | Sort element in range |
| binary_search() | Test if value exists in sorted array |
| merge() | Merge sorted ranges |
| min() | Return the lesser of two arguments |
| max() | Return the greater of two arguments |
| Min_element() | Return the smallest element in range |
| max_element() | Return the largest element in range |
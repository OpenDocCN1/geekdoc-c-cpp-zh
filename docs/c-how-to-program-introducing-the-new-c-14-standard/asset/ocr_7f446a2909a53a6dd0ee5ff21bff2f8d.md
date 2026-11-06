```
```cpp
cout << "\\n\tUpper bound of 6 is element "
     << (eq.second - a.cbegin()) << " of array a";

// determine lower-bound insertion point for 5 in a
cout << "\\n\\nUse lower_bound to locate the first point\\n"
     << "at which 5 can be inserted in order";
lower = lower_bound(a.cbegin(), a.cend(), 5);
cout << "\\n\tLower bound of 5 is element "
     << (lower - a.cbegin()) << " of array a";

// determine upper-bound insertion point for 7 in a
cout << "\\n\\nUse upper_bound to locate the last point\\n"
     << "at which 7 can be inserted in order";
upper = upper_bound(a.cbegin(), a.cend(), 7);
cout << "\\n\tUpper bound of 7 is element "
     << (upper - a.cbegin()) << " of array a";

// use equal_range to determine both the lower- and
// upper-bound insertion points for 5
cout << "\\n\\nUse equal_range to locate the first and\\n"
     << "last point at which 5 can be inserted in order";
eq = equal_range(a.cbegin(), a.cend(), 5);
cout << "\\n\tLower bound of 5 is element "
     << (eq.first - a.cbegin()) << " of array a";
cout << "\\n\tUpper bound of 5 is element "
     << (eq.second - a.cbegin()) << " of array a" << endl;
}
```
```

```
```text
Array a contains: 2 2 4 4 4 6 6 6 6 8

Lower bound of 6 is element 5 of array a
Upper bound of 6 is element 9 of array a
Using equal_range:
    Lower bound of 6 is element 5 of array a
    Upper bound of 6 is element 9 of array a

Use lower_bound to locate the first point
at which 5 can be inserted in order
    Lower bound of 5 is element 5 of array a

Use upper_bound to locate the last point
at which 7 can be inserted in order
    Upper bound of 7 is element 9 of array a

Use equal_range to locate the first and
last point at which 5 can be inserted in order
    Lower bound of 5 is element 5 of array a
    Upper bound of 5 is element 5 of array a
```
```

Fig. 16.12 Algorithms `lower_bound`, `upper_bound` and `equal_range` for
a sorted sequence of values.
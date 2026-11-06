```
```cpp
96  // locate first occurrence of value that's not greater than 10 in a
97  location = find_if_not(a.cbegin(), a.cend(), isGreaterThan10);
98
99  if (location != a.cend()) { // found a value less than or equal to 10
100     cout << "\nThe first value not greater than 10 is " << *location
101          << "\nfound at location " << (location - a.cbegin());
102  }
103  else { // no values less than or equal to 10 were found
104     cout << "\nOnly values greater than 10 were found";
105  }
106
107  cout << endl;
108 }
```
```

```
```
array a contains: 10 2 17 5 16 8 13 11 20 7

Found 16 at location 4
100 not found

The first value greater than 10 is 17
found at location 2

array a after sort: 2 5 7 8 10 11 13 16 17 20

13 was found in a
100 was not found in a

Some elements in a are not greater than 10

Some of the elements in a are greater than 10

Some of the elements in a are greater than 10

The first value not greater than 10 is 2
found at location 0
```
```

Fig. 16.7 Standard Library search and sort algorithms.

# `find` Algorithm

Line 18 uses the `find` algorithm to locate the value `16` in the range from `a.cbegin()` up to, but not including, `a.cend()`. The algorithm requires its two iterator arguments to be at least *input iterators* and returns an *input iterator* that’s either positioned at the first element
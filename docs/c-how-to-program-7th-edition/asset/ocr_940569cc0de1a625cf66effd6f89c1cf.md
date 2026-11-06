Line 57 uses function equal_range to determine the lower_bound and upper_bound of 22 in the multiset. Line 60 uses p.first and p.second, respectively, to access the lower_bound and upper_bound. We dereferenced the iterators to output the values at the locations returned from equal_range.

# 22.3.2 set Associative Container

The set associative container is used for fast storage and retrieval of unique keys. The implementation of a set is identical to that of a multiset, except that a set must have unique keys. Therefore, if an attempt is made to insert a duplicate key into a set, the duplicate is ignored; because this is the intended mathematical behavior of a set, we do not identify it as a common programming error. A set supports bidirectional iterators (but not random-access iterators). Figure 22.20 demonstrates a set of doubles. Header file <set> must be included to use class set.

```
```cpp
1 // Fig. 22.20: Fig22_20.cpp
2 // Standard Library class set test program.
3 #include <iostream>
4 #include <set>
5 #include <algorithm>
6 #include <iterator> // ostream_iterator
7 using namespace std;
8
9 // define short name for set type used in this program
10 typedef set< double, less< double > > DoubleSet;
11
12 int main()
13 {
14    const int SIZE = 5;
15    double a[ SIZE ] = { 2.1, 4.2, 9.5, 2.1, 3.7 };
16    DoubleSet doubleSet( a, a + SIZE );
17    ostream_iterator< double > output( cout, " " );
18
19    cout << "doubleSet contains: ";
20    copy( doubleSet.begin(), doubleSet.end(), output );
21
22    // p represents pair containing const_iterator and bool
23    pair< DoubleSet::const_iterator, bool > p;
24
25    // insert 13.8 in doubleSet; insert returns pair in which
26    // p.first represents location of 13.8 in doubleSet and
27    // p.second represents whether 13.8 was inserted
28    p = doubleSet.insert( 13.8 ); // value not in set
29    cout << "\n\n" << ( p.first
30       << ( p.second ? " was " : " was not" ) << " inserted" );
31    cout << "\ndoubleSet contains: ";
32    copy( doubleSet.begin(), doubleSet.end(), output );
33
34    // insert 9.5 in doubleSet
35    p = doubleSet.insert( 9.5 ); // value already in set
```
```

Fig. 22.20 | Standard Library set class template. (Part 1 of 2.)
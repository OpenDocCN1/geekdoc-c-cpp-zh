```
7
8 #include <algorithm> // algorithm definitions
9 #include <vector> // vector class-template definition
10 #include <iterator> // back_inserter definition
11
12 int main()
13 {
14     const int SIZE = 10;
15     int a1[ SIZE ] = { 1, 3, 5, 7, 9, 1, 3, 5, 7, 9 };
16     std::vector< int > v1( a1, a1 + SIZE ); // copy of a
17     std::ostream_iterator< int > output( cout, " " );
18
19     cout << "Vector v1 contains: ";
20     std::copy( v1.begin(), v1.end(), output );
21
22     // merge first half of v1 with second half of v1 such that
23     // v1 contains sorted set of elements after merge
24     std::inplace_merge( v1.begin(), v1.begin() + 5, v1.end() );
25
26     cout << "\nAfter inplace_merge, v1 contains: ";
27     std::copy( v1.begin(), v1.end(), output );
28
29     std::vector< int > results1;
30
31     // copy only unique elements of v1 into results1
32     std::unique_copy(
33         v1.begin(), v1.end(), std::back_inserter( results1 ) );
34     cout << "\nAfter unique_copy results1 contains: ";
35     std::copy( results1.begin(), results1.end(), output );
36
37     std::vector< int > results2;
38
39     // copy elements of v1 into results2 in reverse order
40     std::reverse_copy(
41         v1.begin(), v1.end(), std::back_inserter( results2 ) );
42     cout << "\nAfter reverse_copy, results2 contains: ";
43     std::copy( results2.begin(), results2.end(), output );
44     cout << endl;
45     return 0;
46 } // end main
```

Vector v1 contains: 1 3 5 7 9 1 3 5 7 9
After inplace_merge, v1 contains: 1 1 3 3 5 5 7 7 9 9
After unique_copy results1 contains: 1 3 5 7 9
After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1

Fig. 20.34 | Demonstrating inplace_merge, unique_copy and reverse_copy. (Part 2 of 2.)

Lines 32–33 use function unique_copy to make a copy of all the unique elements in the sorted sequence of values from v1.begin() up to, but not including, v1.end(). The copied elements are placed into vector results1. The first two arguments must be at least input iterators and the last must be at least an output iterator. In this example, we did not preallocate enough elements in results1 to store all the elements copied from v1. Instead,
```
51  cout << "\n\nVector v4 before replacing all values greater "
52      << "than 9 and copying:\n ";
53  std::copy( v4.begin(), v4.end(), output );
54
55  // copy v4 to c2, replacing elements greater than 9 with 100
56  std::replace_copy_if(
57      v4.begin(), v4.end(), c2.begin(), greater9, 100 );
58  cout << "\nVector c2 after replacing all values greater "
59      << "than 9 in v4:\n ";
60  std::copy( c2.begin(), c2.end(), output );
61  cout << endl;
62  return 0;
63 } // end main
64
65  // determine whether argument is greater than 9
66  bool greater9( int x )
67  {
68      return x > 9;
69  } // end function greater9
```

Vector v1 before replacing all 10s:
  10 2 10 4 16 6 14 8 12 10
Vector v1 after replacing 10s with 100s:
  100 2 100 4 16 6 14 8 12 100

Vector v2 before replacing all 10s and copying:
  10 2 10 4 16 6 14 8 12 10
Vector c1 after replacing all 10s in v2:
  100 2 100 4 16 6 14 8 12 100

Vector v3 before replacing values greater than 9:
  10 2 10 4 16 6 14 8 12 10
Vector v3 after replacing all values greater
than 9 with 100s:
  100 2 100 4 100 6 100 8 100 100

Vector v4 before replacing all values greater than 9 and copying:
  10 2 10 4 16 6 14 8 12 10
Vector c2 after replacing all values greater than 9 in v4:
  100 2 100 4 100 6 100 8 100 100

Fig. 20.29 | Algorithms replace, replace_if, replace_copy and replace_copy_if. (Part 2 of 2.)

Line 35 uses function replace_copy to copy all elements in the range from v2.begin() up to, but not including, v2.end() from v2, replacing all elements with the value 10 with the new value 100. The elements are copied into c1, starting at position c1.begin(). The iterators supplied as the first two arguments must be input iterators. The iterator supplied as the third argument must be an output iterator so that the element being copied can be inserted into the copy location. This function returns an iterator positioned after the last element copied into c1.

Line 44 uses function replace_if to replace all those elements in the range from v3.begin() up to, but not including, v3.end() in v3 for which the unary predicate function greater9 returns true. Function greater9 (defined in lines 66–69) returns true if
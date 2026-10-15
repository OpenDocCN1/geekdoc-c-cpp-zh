```
23  // Locate first occurrence of 16 in v
24  std::vector< int >::iterator location;
25  location = std::find( v.begin(), v.end(), 16 );
26
27  if ( location != v.end() ) // found 16
28      cout << "\n\nFound 16 at location " << ( location - v.begin() );
29  else // 16 not found
30      cout << "\n\n16 not found";
31
32  // Locate first occurrence of 100 in v
33  location = std::find( v.begin(), v.end(), 100 );
34
35  if ( location != v.end() ) // found 100
36      cout << "\nFound 100 at location " << ( location - v.begin() );
37  else // 100 not found
38      cout << "\n100 not found";
39
40  // Locate first occurrence of value greater than 10 in v
41  location = std::find_if( v.begin(), v.end(), greater10 );
42
43  if ( location != v.end() ) // found value greater than 10
44      cout << "\n\nThe first value greater than 10 is " << *location
45           << "\nfound at location " << ( location - v.begin() );
46  else // value greater than 10 not found
47      cout << "\n\nNo values greater than 10 were found";
48
49  // sort elements of v
50  std::sort( v.begin(), v.end() );
51  cout << "\n\nVector v after sort: ";
52  std::copy( v.begin(), v.end(), output );
53
54  // use binary_search to locate 13 in v
55  if ( std::binary_search( v.begin(), v.end(), 13 ) )
56      cout << "\n\n13 was found in v";
57  else
58      cout << "\n13 was not found in v";
59
60  // use binary_search to locate 100 in v
61  if ( std::binary_search( v.begin(), v.end(), 100 ) )
62      cout << "\n100 was found in v";
63  else
64      cout << "\n100 was not found in v";
65
66  cout << endl;
67  return 0;
68 } // end main
69
70 // determine whether argument is greater than 10
71 bool greater10( int value )
72 {
73   return value > 10;
74 } // end function greater10
```
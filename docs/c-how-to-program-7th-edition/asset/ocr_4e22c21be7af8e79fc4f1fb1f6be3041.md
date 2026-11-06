```
    15
    16 cout << "The initial size of integers is: " << integers.size()
    17      << "\nThe initial capacity of integers is: " << integers.capacity();
    18
    19 // function push_back is in every sequence collection
    20 integers.push_back( 2 );
    21 integers.push_back( 3 );
    22 integers.push_back( 4 );
    23
    24 cout << "\nThe size of integers is: " << integers.size()
    25      << "\nThe capacity of integers is: " << integers.capacity();
    26 cout << "\n\nOutput array using pointer notation: ";
    27
    28 // display array using pointer notation
    29 for ( int *ptr = array; ptr != array + SIZE; ptr++ )
    30    cout << *ptr << ' ';
    31
    32 cout << "\nOutput vector using iterator notation: ";
    33 printVector( integers );
    34 cout << "\nReversed contents of vector integers: ";
    35
    36 // two const reverse iterators
    37 vector< int >::const_reverse_iterator reverseIterator;
    38 vector< int >::const_reverse_iterator tempIterator = integers.rend();
    39
    40 // display vector in reverse order using reverse_iterator
    41 for ( reverseIterator = integers.rbegin();
    42       reverseIterator!= tempIterator; ++reverseIterator )
    43    cout << *reverseIterator << ' ';
    44
    45 cout << endl;
    46 } // end main
    47
    48 // function template for outputting vector elements
    49 template < typename T > void printVector( const vector< T > &integers2 )
    50 {
    51    typename vector< T >::const_iterator constIterator; // const_iterator
    52
    53    // display vector elements using const_iterator
    54    for ( constIterator = integers2.begin();
    55          constIterator != integers2.end(); ++constIterator )
    56       cout << *constIterator << ' ';
    57 } // end function printVector
```

```
    The initial size of integers is: 0
    The initial capacity of integers is: 0
    The size of integers is: 3
    The capacity of integers is: 4

    Output array using pointer notation: 1 2 3 4 5 6
    Output vector using iterator notation: 2 3 4
    Reversed contents of vector integers: 4 3 2
```

Fig. 22.14 | Standard library vector class template. (Part 2 of 2).
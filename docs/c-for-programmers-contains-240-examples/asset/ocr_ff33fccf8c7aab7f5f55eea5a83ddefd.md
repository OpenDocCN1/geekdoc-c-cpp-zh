```
38      cout << "\nData items in ascending order\n";
39    } // end if
40
41    // sort array in descending order; pass function descending
42    // as an argument to specify descending sorting order
43    else
44    {
45        selectionSort( a, arraySize, descending );
46        cout << "\nData items in descending order\n";
47    } // end else part of if...else
48
49    // output sorted array
50    for ( counter = 0; counter < arraySize; counter++ )
51        cout << setw( 4 ) << a[ counter ];
52
53    cout << endl;
54    return 0; // indicates successful termination
55 } // end main
56
57    // multipurpose selection sort; the parameter compare is a pointer to
58    // the comparison function that determines the sorting order
59    void selectionSort( int work[], const int size,
60                        bool (*compare)( int, int ) )
61    {
62        int smallestOrLargest; // index of smallest (or largest) element
63
64        // loop over size - 1 elements
65        for ( int i = 0; i < size - 1; i++ )
66        {
67            smallestOrLargest = i; // first index of remaining vector
68
69            // loop to find index of smallest (or largest) element
70            for ( int index = i + 1; index < size; index++ )
71                if ( !(*compare)( work[ smallestOrLargest ], work[ index ] ) )
72                    smallestOrLargest = index;
73
74            swap( &work[ smallestOrLargest ], &work[ i ] );
75        } // end if
76    } // end function selectionSort
77
78    // swap values at memory locations to which
79    // element1Ptr and element2Ptr point
80    void swap( int * const element1Ptr, int * const element2Ptr )
81    {
82        int hold = *element1Ptr;
83        *element1Ptr = *element2Ptr;
84        *element2Ptr = hold;
85    } // end function swap
86
87    // determine whether element a is less than
88    // element b for an ascending order sort
89    bool ascending( int a, int b )
90    {
```
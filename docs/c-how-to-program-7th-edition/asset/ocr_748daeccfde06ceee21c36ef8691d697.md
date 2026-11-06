```
    48
    49 // calculate sum of elements in v
    50 cout << "\nThe total of the elements in Vector v is: "
    51      << accumulate( v.begin(), v.end(), 0 );
    52
    53 // output square of every element in v
    54 cout << "\nThe square of every integer in Vector v is:\n";
    55 for_each( v.begin(), v.end(), outputSquare );
    56
    57 vector< int > cubes( SIZE ); // instantiate vector cubes
    58
    59 // calculate cube of each element in v; place results in cubes
    60 transform( v.begin(), v.end(), cubes.begin(), calculateCube );
    61 cout << "\nThe cube of every integer in Vector v is:\n";
    62 copy( cubes.begin(), cubes.end(), output );
    63 cout << endl;
    64 } // end main
    65
    66 // determine whether argument is greater than 9
    67 bool greater9( int value )
    68 {
    69    return value > 9;
    70 } // end function greater9
    71
    72 // output square of argument
    73 void outputSquare( int value )
    74 {
    75    cout << value * value << ' ';
    76 } // end function outputSquare
    77
    78 // return cube of argument
    79 int calculateCube( int value )
    80 {
    81    return value * value * value;
    82 } // end function calculateCube
```

```
    Vector v before random_shuffle: 1 2 3 4 5 6 7 8 9 10
    Vector v after random_shuffle: 5 4 1 3 7 8 9 10 6 2

    Vector v2 contains: 100 2 8 1 50 3 8 8 9 10
    Number of elements matching 8: 3
    Number of elements greater than 9: 3

    Minimum element in Vector v2 is: 1
    Maximum element in Vector v2 is: 100

    The total of the elements in Vector v is: 55

    The square of every integer in Vector v is:
    25 16 1 9 49 64 81 100 36 4

    The cube of every integer in Vector v is:
    125 64 1 27 343 512 729 1000 216 8
```

Fig. 22.30 | Mathematical algorithms of the Standard Library. (Part 2 of 2.)
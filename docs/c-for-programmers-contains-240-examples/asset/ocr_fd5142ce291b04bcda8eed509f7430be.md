```
// count number of elements in v2 with value 8
int result = std::count( v2.begin(), v2.end(), 8 );
cout << "\nNumber of elements matching 8: " << result;

// count number of elements in v2 that are greater than 9
result = std::count_if( v2.begin(), v2.end(), greater9 );
cout << "\nNumber of elements greater than 9: " << result;

// locate minimum element in v2
cout << "\n\nMinimum element in Vector v2 is: "
    << *( std::min_element( v2.begin(), v2.end() ) );

// locate maximum element in v2
cout << "\nMaximum element in Vector v2 is: "
    << *( std::max_element( v2.begin(), v2.end() ) );

// calculate sum of elements in v
cout << "\n\nThe total of the elements in Vector v is: "
    << std::accumulate( v.begin(), v.end(), 0 );

// output square of every element in v
cout << "\n\nThe square of every integer in Vector v is:\n";
std::for_each( v.begin(), v.end(), outputSquare );

std::vector< int > cubes( SIZE ); // instantiate vector cubes

// calculate cube of each element in v; place results in cubes
std::transform( v.begin(), v.end(), cubes.begin(), calculateCube );
cout << "\n\nThe cube of every integer in Vector v is:\n";
std::copy( cubes.begin(), cubes.end(), output );
cout << endl;
return 0;
} // end main

// determine whether argument is greater than 9
bool greater9( int value )
{
    return value > 9;
} // end function greater9

// output square of argument
void outputSquare( int value )
{
    cout << value * value << ' ';
} // end function outputSquare

// return cube of argument
int calculateCube( int value )
{
    return value * value * value;
} // end function calculateCube
```
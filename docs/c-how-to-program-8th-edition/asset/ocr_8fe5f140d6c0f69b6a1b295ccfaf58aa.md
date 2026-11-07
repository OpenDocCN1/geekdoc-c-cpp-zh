```
// use overloaded assignment (=) operator
cout << "\nAssigning integers2 to integers1:" << endl;
integers1 = integers2; // assign integers2 to integers1

cout << "integers1:" << endl;
outputVector( integers1 );
cout << "integers2:" << endl;
outputVector( integers2 );

// use equality (==) operator with vector objects
cout << "\nEvaluating: integers1 == integers2" << endl;

if ( integers1 == integers2 )
   cout << "integers1 and integers2 are equal" << endl;

// use square brackets to create rvalue
cout << "integers1[5] is " << integers1[ 5 ];

// use square brackets to create lvalue
cout << "\n\nAssigning 1000 to integers1[5]" << endl;
integers1[ 5 ] = 1000;
cout << "integers1:" << endl;
outputVector( integers1 );

// attempt to use out-of-range subscript
try
{
   cout << "\nAttempt to display integers1.at( 15 )" << endl;
   cout << integers1.at( 15 ) << endl; // ERROR: out of range
} // end try
catch ( out_of_range &ex )
{
   cout << "\nAn exception occurred: " << ex.what() << endl;
} // end catch
} // end main

// output vector contents
void outputVector( const vector< int > &array )
{
   size_t i; // declare control variable

   for ( i = 0; i < array.size(); ++i )
   {
      cout << setw( 12 ) << array[ i ];

      if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
         cout << endl;
   } // end for

   if ( i % 4 != 0 )
      cout << endl;
} // end function outputVector
```

Fig. 7.25 | Demonstrating C++ Standard Library class template vector. (Part 2 of 4.)
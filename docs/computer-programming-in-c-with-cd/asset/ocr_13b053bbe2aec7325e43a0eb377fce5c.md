```
```cpp
void stddev() ;
void display() ;
};
// 2nd file to hold the function definitions
# include <d:\ashish\domanip.cpp>//includes the file having class definition
# include <math.h>

domanip :: damanip() // constructor to set the object to empty
{
    n = 0 ;
}
void damanip :: input()   // function to read the values
{
    cout << "\nenter the size of array :  " ;
    cin >> n ;

    for( int i = 0 ; i < n ; i ++ )
        cin >> a[i] ;
}
void damanip :: input( int size ) // overloaded input function
{

    n = size ;

    for( int i = 0 ; i < n ; i ++ )
        cin >> a[i] ;

}

void damanip :: display()    // function to display the data of an object
{

    for( int i = 0 ; i < n ; i ++ )
        cout << endl << a[i] ;

}

// function to merge the data of two object into the third
void damanip :: merge( damanip d1 , damanip d2 )
{
    int i = 0 , j = 0 ;
    n = 0 ;
```
```
```
```cpp
using namespace std;

// define short name for multiset type used in this program
typedef multiset< int, less< int > > Ims;

int main()
{
    const int SIZE = 10;
    int a[ SIZE ] = { 7, 22, 9, 1, 18, 30, 100, 22, 85, 13 };
    Ims intMultiSet; // Ims is typedef for "integer multiset"
    ostream_iterator< int > output( cout, " " );

    cout << "There are currently " << intMultiSet.count( 15 )
         << " values of 15 in the multiset\n";

    intMultiSet.insert( 15 ); // insert 15 in intMultiset
    intMultiSet.insert( 15 ); // insert 15 in intMultiset
    cout << "After inserting 15, there are " << intMultiSet.count( 15 )
         << " values of 15 in the multiset\n";

    // iterator that cannot be used to change element values
    Ims::const_iterator result;

    // find 15 in intMultiset; find returns iterator
    result = intMultiSet.find( 15 );

    if ( result != intMultiSet.end() ) // if iterator not at end
        cout << "Found value 15\n"; // found search value 15

    // find 20 in intMultiset; find returns iterator
    result = intMultiSet.find( 20 );

    if ( result == intMultiSet.end() ) // will be true hence
        cout << "Did not find value 20\n"; // did not find 20

    // insert elements of array a into intMultiset
    intMultiSet.insert( a, a + SIZE );
    cout << "\nAfter inserting, intMultiset contains:\n";
    copy( intMultiSet.begin(), intMultiSet.end(), output );

    // determine lower and upper bound of 22 in intMultiset
    cout << "\n\nLower bound of 22:";
         << *( intMultiSet.lower_bound( 22 ) );
    cout << "\nUpper bound of 22:" << *( intMultiSet.upper_bound( 22 ) );

    // p represents pair of const_iterators
    pair< Ims::const_iterator, Ims::const_iterator > p;

    // use equal_range to determine lower and upper bound
    // of 22 in intMultiset
    p = intMultiSet.equal_range( 22 );
```
```

Fig. 22.19 | Standard Library multiset class template. (Part 2 of 3.)
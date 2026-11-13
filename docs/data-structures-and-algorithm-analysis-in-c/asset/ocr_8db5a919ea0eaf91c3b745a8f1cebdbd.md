```
// Generic findMax, with a function object, Version #1.
// Precondition: a.size( ) > 0.
template <typename Object, typename Comparator>
const Object & findMax( const vector<Object> & arr, Comparator cmp )
{
    int maxIndex = 0;

    for( int i = 1; i < arr.size( ); ++i )
        if( cmp.isLessThan( arr[ maxIndex ], arr[ i ] ) )
            maxIndex = i;

    return arr[ maxIndex ];
}

class CaseInsensitiveCompare
{
    public:
        bool isLessThan( const string & lhs, const string & rhs ) const
        { return strcasecmp( lhs.c_str( ), rhs.c_str( ) ) < 0; }
};

int main( )
{
    vector<string> arr = { "ZEBRA", "alligator", "crocodile" };
    cout << findMax( arr, CaseInsensitiveCompare( ) ) << endl;

    return 0;
}
```

# Figure 1.24 Simplest idea of using a function object as a second parameter to findMax; output is ZEBRA

cmp.operator( )( x,y ) can be shortened to cmp( x,y ) (in other words, it looks like a function call, and consequently operator( ) is known as the function call operator). As a result, the name of the parameter can be changed to the more meaningful isLessThan, and the call is isLessThan( x,y ). Third, we can provide a version of findMax that works without a function object. The implementation uses the Standard Library function object template less (defined in header file <functional>) to generate a function object that imposes the normal default ordering. Figure 1.25 shows the implementation using the more typical, somewhat cryptic, C++ idioms.

In Chapter 4, we will give an example of a class that needs to order the items it stores. We will write most of the code using Comparable and show the adjustments needed to use the function objects. Elsewhere in the book, we will avoid the detail of function objects to keep the code as simple as possible, knowing that it is not difficult to add function objects later.
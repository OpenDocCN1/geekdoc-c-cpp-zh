```
class AClass
{
    string fStr;
    public:
    AClass( const string & s = "" ) : fStr(s) {}
    ~AClass() { cout << "AClass destructor" << endl; }
    const string GetStr( void ) const { return fStr; }
    void SetStr( const string & s ) { fStr = s; }
};
// ..................................................................
// AClass object on the heap, p_d takes care
unique_ptr< AClass > p_d_1( new AClass( "Good" ) );
// A better way is to use make_unique helper
auto p_d_2( make_unique< AClass >( "Better" ) );

if( p_d_2 )
{
    cout << p_d_2->GetStr() << endl;    // access through the pointer
    cout << ( * p_d_2 ).GetStr() << endl; // access through the object
}

//unique_ptr< AClass > p_d_3 = p_d_2;  // won't work, cannot copy
unique_ptr< AClass > p_d_3 = std::move( p_d_2 );    // OK, can move to
// other smart ptr

// An array of AClass objects on the heap and p_d_4
const int kAClassElems = 4;
auto p_d_4( make_unique< AClass [] >( kAClassElems ) );// call default
// ctor for each
```

make_unique lets us pass any number of parameters necessary to construct an object. Another advantage is the ability to use the auto keyword directly instead of explicitly providing the full type name. Note that unique_ptr cannot be copied, since two smart pointers cannot delete a single object. However, content of one unique_ptr can be easily moved using the std::move function to the other smart pointer - in our example, p_d_2 is moved this way to p_d_3.
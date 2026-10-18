# Listing 4.7 Object-oriented version of EMatrix (in EasyMatrix, EMatrix.h). Data member fData moved to the private section to obtain data encapsulation; new operator []; operator << and operator >> declared as friend (new features in bold).

```
class EMatrix
{
private:
    RealMatrix fData;    // private data structure (encapsulation)
public:
    // A parametric constructor
    EMatrix( Dim rows, Dim cols, DataType initVal = 0.0 )
    : fData( rows, RealVec( cols, initVal ) )
    {
    // matrix == a vector of vectors of double
    assert( cols > 0 );
    assert( rows > 0 );
    }

    // Helpers
    auto GetCols( void ) const { return fData[ 0 ].size(); }
    auto GetRows( void ) const { return fData.size(); }

    // As a result of overloaded subscript operators
    // instead of m.fData[2][3] we can write directly m[2][3]
    auto & operator[]( Dim idx ) { return fData[ idx ]; }
    const auto & operator[]( Dim idx ) const { return fData[ idx ]; }

    // We need only these two pairs of functions to have a range-based for loop
    auto begin() { return fData.begin(); }
    auto end() { return fData.end(); }

    auto begin() const { return fData.begin(); }
    auto end() const { return fData.end(); }

    // Let us add some overloaded arithmetical operators
    EMatrix & operator += ( const EMatrix & b );    // this can change this object
    EMatrix operator + ( const EMatrix & b ) const;
    // We can add other operators here ...

    // friends are functions that can freely access fData
    friend std::ostream & operator << ( std::ostream & o, const EMatrix & matrix );
    friend std::istream & operator >> ( std::istream & i, EMatrix & matrix );
};
```

Also, to allow access to matrix elements, two versions of the overloaded operator [] are defined on lines [24, 25]. This the subscript operator, which we have used previously to access vector elements. But this is the first time we have written our own versions of the operators, which can then be used to call mathematical operations efficiently. As already discussed, an overloaded operator is defined exactly like any other function, except its name must start with the operator keyword followed by the operator symbol (Section 4.4).

We need to write our own version of operator [] because fData is private, so it cannot be directly accessed. Actually, there are two versions of the subscripts: on line [24], for write operations;
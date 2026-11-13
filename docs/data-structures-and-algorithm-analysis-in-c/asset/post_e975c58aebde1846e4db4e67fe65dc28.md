
```cpp
class Square
{
public:
    explicit Square( double s = 0.0 ) : side{ s }
    {
    }

    double getSide( ) const
    {
        return side;
    }
    double getArea( ) const
    {
        return side * side;
    }
    double getPerimeter( ) const
    {
        return 4 * side;
    }

    void print( ostream & out = cout ) const
    {
        out << "(square * " << getSide( ) << " ) ";
    }

    bool operator<( const Square & rhs ) const
    {
        return getSide( ) < rhs.getSide( );
    }

private:
    double side;
};

// Define an output operator for Square
ostream & operator<<( ostream & out, const Square & rhs )
{
    rhs.print( out );
    return out;
}

int main( )
{
    vector<Square> v = { Square{ 3.0 }, Square{ 2.0 }, Square{ 2.5 } };

    cout << "Largest square: " << findMax( v ) << endl;

    return 0;
}
```

Figure 1.23 Comparable can be a class type, such as Square

Figure 1.23 shows an example of a class type that implements the functionality required of Comparable and illustrates operator overloading. Operator overloading allows us to define the meaning of a built-in operator. The Square class represents a square by storing the length of a side and defines operator<. The Square class also provides a zero-parameter constructor, operator*, and copy constructor (all by default). Thus, it has enough to be used as a Comparable in findMax.

Figure 1.23 shows a minimal implementation and also illustrates the widely used idiom for providing an output function for a new class type. The idiom is to provide a public member function, named print, that takes an ostream as a parameter. That public member function can then be called by a global, nonclass function, operator<<, that accepts an ostream and an object to output.

## 1.6.4 Function Objects

In Section 1.6.1, we showed how function templates can be used to write generic algorithms. As an example, the function template in Figure 1.19 can be used to find the maximum item in an array.

However, the template has an important limitation: It works only for objects that have an operator< function defined, and it uses that operator< as the basis for all comparison decisions. In many situations, this approach is not feasible. For instance, it is a stretch to presume that a Rectangle class will implement operator<, and even if it does, the compareTo method that it has might not be the one we want. For instance, given a 2-by-10 rectangle and a 5-by-5 rectangle, which is the larger rectangle? The answer would depend on whether we are using area or width to decide. Or perhaps we are trying to fit the rectangle through an opening, the larger rectangle is the rectangle with the larger minimum dimension. As a second example, if we wanted to find the maximum string (alphabetically last) in an array of strings, the default operator< does not ignore case distinctions, so “ZEBRA” would be considered to precede “alligator” alphabetically, which is probably not what we want. A third example would occur if we had an array of pointers to objects (which would be common in advanced C++ programs that make use of a feature known as inheritance, which we do not make much use of in this text).

The solution, in these cases, is to rewrite findMax to accept as parameters an array of objects and a comparison function that explains how to decide which of two objects is the larger and which is the smaller. In effect, the array no longer knows how to compare themselves; instead, this information is completely decoupled from the objects in the array.

An ingenious way to pass functions as parameters is to notice that an object contains both data and member functions, so we can define a class with no data and one member function, and pass an instance of the class. In effect, a function is being passed by placing it inside an object. This object is commonly known as a function object.

Figure 1.24 shows the simplest implementation of the function object idea. findMax takes a second parameter, which is a generic type. In order for the findMax template to expand without error, the generic type must have a member function named isLessThan, which takes two parameters of the first generic type (object) and returns a bool. Otherwise, an error will be generated at line 9 when the template expansion is attempted by the compiler. At line 25, we can see that findMax is called by passing an array of string and an object that contains an isLessThan method with two strings as parameters.

C++ function objects are implemented using this basic idea, but with some fancy syntax. First, instead of using a function with a name, we use operator overloading. Instead of the function being isLessThan, it is operator(). Second, when invoking operator(),

```cpp
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

Figure 1.24 Simplest idea of using a function object as a second parameter to findMax; output is ZEBRA

cmp.operator( )( x,y ) can be shortened to cmp( x,y ) (in other words, it looks like a function call, and consequently operator( ) is known as the function call operator). As a result, the name of the parameter can be changed to the more meaningful isLessThan, and the call is isLessThan( x,y ). Third, we can provide a version of findMax that works without a function object. The implementation uses the Standard Library function object template less (defined in header file <functional>) to generate a function object that imposes the normal default ordering. Figure 1.25 shows the implementation using the more typical, somewhat cryptic, C++ idioms.

In Chapter 4, we will give an example of a class that needs to order the items it stores. We will write most of the code using Comparable and show the adjustments needed to use the function objects. Elsewhere in the book, we will avoid the detail of function objects to keep the code as simple as possible, knowing that it is not difficult to add function objects later.

```cpp
// Generic findMax, with a function object, C++ style.
// Precondition: a.size( ) > 0.
template <typename Object, typename Comparator>
const Object & findMax( const vector<Object> & arr, Comparator isLessThan )
{
    int maxIndex = 0;

    for ( int i = 1; i < arr.size( ); ++i )
        if ( isLessThan( arr[ maxIndex ], arr[ i ] ) )
            maxIndex = i;

    return arr[ maxIndex ];
}

// Generic findMax, using default ordering.
#include <functional>
template <typename Object>
const Object & findMax( const vector<Object> & arr )
{
    return findMax( arr, less<Object>( ) );
}

class CaseInsensitiveCompare
{
public:
    bool operator( )( const string & lhs, const string & rhs ) const
    { return strcasecmp( lhs.c_str( ), rhs.c_str( ) ) < 0; }
};

int main( )
{
    vector<string> arr = { "ZEBRA", "alligator", "crocodile" };

    cout << findMax( arr, CaseInsensitiveCompare( ) ) << endl;
    cout << findMax( arr ) << endl;

    return 0;
}
```

Figure 1.25 Using a function object C++ style, with a second version of findMax; output is ZEBRA, then crocodile

## 1.6.5 Separate Compilation of Class Templates

Like regular classes, class templates can be implemented either entirely in their declarations, or we can separate the interface from the implementation. However, compiler support for separate compilation of templates historically has been weak and platform-specific. Thus, in many cases, the entire class template with its implementation is placed in a single header file. Popular implementations of the Standard Library follow this strategy to implement class templates.

Appendix A describes the mechanics involved in the separate compilation of templates. The declaration of the interface for a template is exactly what you would expect: The member functions end with a single semicolon, instead of providing an implementation. But as shown in Appendix A, the implementation of the member functions can introduce complicated-looking syntax, especially for complicated functions like operator*. Worse, when compiling, the compiler will often complain about missing functions, and avoiding this problem requires platform-specific solutions.

Consequently, in the online code that accompanies the text, we implement all class templates entirely in its declaration in a single header file. We do so because it seems to be the only way to avoid compilation problems across platforms. In the text, when illustrating the code, we provide the class interface as if separate compilation was in order, since that is easily presentable, but implementations are shown as in the online code. In a platform-specific manner, one can mechanically transform our single header file implementations into separate compilation implementations if desired. See Appendix A for some of the different scenarios that might apply.

## 1.7 Using Matrices

Several algorithms in Chapter 10 use two-dimensional arrays, which are popularly known as matrices. The C++ library does not provide a matrix class. However, a reasonable matrix class can quickly be written. The basic idea is to use a vector of vectors. Doing this requires additional knowledge of operator overloading. For the matrix, we define operator[], namely, the array-indexing operator. The matrix class is given in Figure 1.26.

### 1.7.1 The Data Members, Constructor, and Basic Accessors

The matrix is represented by an array data member that is declared to be a vector of vector<Object>. The constructor first constructs array as having rows entries each of type vector<Object> that is constructed with the zero-parameter constructor. Thus, we have rows zero-length vectors of Object.

The body of the constructor is then entered, and each row is resized to have cols columns. Thus the constructor terminates with what appears to be a two-dimensional array. The numrows and numcols accessors are then easily implemented, as shown.

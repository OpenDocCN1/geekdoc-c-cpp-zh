
The last item in this group is the constructor defined on line [63]. It takes only one real argument, declared with `double`, and initializes only the real part of the complex number, leaving the imaginary part set to 0.0. But it is more than a constructor - this is the _type-converting constructor_. Its role is to take an object of a different type, in this case `double`, and convert it into the type of its class: `TComplex` in our example. As a result, we can, for example, add a real number to the complex one, which - because real numbers are special cases of complex numbers with an imaginary part of zero - is a perfectly acceptable operation from a mathematical point of view. However, there is no corresponding reverse operation: we cannot convert `TComplex` to `double`. We can write such a conversion function, but we cannot be sure what its action would be (returning only the real part, or a modulus?). We will return to this `double` form of type conversion in Section 7.3.

After the group of special functions, the familiar getter and setter member functions are located on lines [68-72]. Note that it is a common practice in OOP to hide data but provide public access to it, or to a selected set of it. As a result, access is controlled, and we can refuse to assign values, for instance. But these functions are inline, since their full definitions are in the definition of a class, so indirect access does not add any time penalty. Also note that GetRe and GetIm are declared const to indicate that they do not change the state of the class. All member functions that are not intended to change member data should be declared const: this practice makes code safer since any inconsistencies will be caught by the compiler.

```cpp
{
    // fRe = 0;  // such initialization is possible but the above is better
}

///////////////
// A parametric constructor
///////////////
TComplex( double re, double im ) : fRe( re ), fIm( im ) {}

// Copy constructor - make this object and make its state
// the same as the supplied one (i.e. "c").
// default means to copy fRe and fIm from "c".

TComplex( const TComplex & c ) = default;

// Overloaded assignment operator - default means to
// copy fRe and fIm.

TComplex & operator = ( const TComplex & c ) = default;

// Destructor does nothing, but stated explicitly

~TComplex( ) = default;
```

```cpp
public:

    // Getters & Setters to access data members of the class
    double GetRe( void ) const { return fRe; }     // "const" since we only read
    double GetIm( void ) const { return fIm; }     // data, not changing the state

    void SetRe( double re ) { fRe = re; }          // here we change the state
    void SetIm( double im ) { fIm = im; }          // so it is not "const"
```

Finally, we came to the *overloaded operators*. The first one, defined on line [79], is the comparison operator == (do not confuse it with assignment =). On line [81], it simply returns the result of the comparison of both data members. But let’s stop for a moment – to compare, we need two objects, whereas only c is provided as an argument in the definition of operator ==. Where is the other object? To answer this, note that, as for any other non-static member, the operator == code is executed on behalf of an object. We can easily see that this is the first object necessary for the comparison, while c is the second one. On the other hand, note that there is no definition of how to implement the ordering operator <.

```cpp
public:

    ////////////////////////////////////////////
    // Overloaded "equal" compare operator
    ////////////////////////////////////////////
    bool operator == ( const TComplex & c ) const
    {
        return fRe == c.fRe && fIm == c.fIm;
    }
```

At this point, we will provide a few facts about the overloaded operators in C++:

- Overloaded operators are overloaded functions that define special behavior for the operators
- Overloaded operators can be members of a class, or they can be standalone functions
- An overloaded operator is defined exactly like any other function, except that its name follows the pattern shown in (Figure 4.4)

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_250_0.png)

**Figure 4.4** Syntax of the overloaded operators in C++.

On line [38], the real value 5.0 is assigned to the complex object b. But this is a twofold operation: first, the converting constructor (line [63] in Listing 4.1) is called to convert a double object into a TComplex object, which is then assigned to b with the assignment operator, defined on line [49] in Listing 4.1. The result of a + b is displayed on line [39].

The second test function Complex_Test_File, defined on line [43], creates two default TComplex objects on line [46]. These are then initialized on lines [50, 53] from the keyboard.

The results of the arithmetic operations are output to a text file ComplexTest.txt, which is opened in appending mode so its existing contents are preserved (Section 6.2.7). Since division can throw an exception – we do not know what the user will enter – it needs to be enclosed by a try-catch statement, starting on line [71]. If an exception is thrown, the first chance to catch it is the catch on line [76]. The exception to be caught must be of the std::exception (or derived) type. Otherwise, if the type of the thrown exception object is incompatible with the former type, the second “last chance” branch on line [81] will catch it. In both cases, an error message is output to the error stream, represented by the std::cerr object. In the first case, std::exception has a chance to print a message using a call to its what() member.

```cpp
// Simple operations with complex numbers
// using the keyboard, the screen, and a file
void Complex_Test_File( void )
{
    // Create two complex objects
    TComplex     a, b;

    // Enter two from the keyboard
    cout << "Enter 1st complex" << endl;
    cin >> a;

    cout << "Enter 2nd complex" << endl;
    cin >> b;

    // let us try to copy results to a file opened in appending mode
    ofstream theFile( "ComplexTest.txt", std::ios::app );

    // Always check if the file opened correctly
    if( theFile.is_open() == true )
    {
        // Perform operations and print the results to the file
        theFile << "a = " << a << ", b = " << b << endl;
        theFile << "a + b = " << a + b << endl;
        theFile << "a - b = " << a - b << endl;
        theFile << "a * b = " << a * b << endl;

        // However, division is different - it can throw an exception
        try
        {
            // Keep it in the try-catch clamp
            theFile << "a / b = " << a / b << endl << endl;
        }
        catch( std::exception & e )          // catch exceptions
        {
            // Standard exceptions will be processed here
            std::cerr << "Exception caught: " << e.what() << endl; // print the cause
        }
        catch( ... )
        {
            // Any other exception will be caught here
            std::cerr << "Unknown error" << endl;
        }
    }
}
```

Finally, the two test functions are launched in the main function in the *Complex* application, as shown in Listing 4.4.

```cpp
// Declarations are sufficient to call functions
void Complex_Test_Screen( void );
void Complex_Test_File( void );

// In C++ there are a few versions of the main function
int main( void )
{
    Complex_Test_Screen();
    Complex_Test_File();

    return 0;
}
```

## 4.5 More on References

In this section, we discuss some more advanced, but important and practical, issues associated with references and indirect access to objects. Here we focus on *rvalue references*, which let us use *move semantics* to avoid expensive, unnecessary copying of objects. For indirect object accesses, the problem of object lifetime is also important, so we will touch on it as well.

In this section, we will learn about the following:

- Rvalue references and the move semantics
- Relations between references and pointers
- Object lifetime issues when returning objects from functions

### 4.5.1 Rvalue and Forwarding References

C++11 introduced the very important concept of *move semantics* (Stroustrup 2013). This is simply a smart way of avoiding unnecessary object copying in some contexts. Instead of performing a full copy of an object and its data, usually pointed to by the object’s internal pointer, it suffices to exchange the internal pointers to data, thus avoiding time-consuming memory operations. The two actions are shown in Figure 4.5.

When performing a copy¹ operation (Figure 4.5a), both the object and data are copied to form a new object with its own copy of the data. As a result, two identical objects are available. On the

> ¹ Actually, this is a type of deep copy, as opposed to a shallow copy – see Section 4.6.4.

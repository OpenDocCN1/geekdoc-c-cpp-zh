
## 169

\begin{tabular}{ccc}
Class member & Description & Example: \\
Default constructor & A function with the same name as the class and no input parameters: X:X( void ) Called once during creation of an object. Its role is to initialize this object. The characteristic part just after the colon : and before the constructor's body is the member data initializer list. Here the constructors of the class member objects are involved. & public: 17 18 19 20 21 22 // class default constructor TQuadEq( void ) : fa( 0.0 ), fb( 0.0 ), fc( 0.0 ) {} \\
Parametric constructor & A function with the same name as the class and with input parameters: X:X( type_ list ) Called once during creation of an object. Its role is to initialize this object using the objects from type_list. & public: 23 24 25 26 27 // class parametric constructor TQuadEq( double a, double b, double c ) : fa( a ), fb( b ), fc( c ) {} \\
\end{tabular}

## 170

\begin{tabular}{ccc}
Class member & Description & Example \\
Getters / setters & A group of functions to read and write the (usually private) data members of a class. & public: 29 30 // Getters \& setters 31 double Get_a( void ) const { return fa; } 32 double Get_b( void ) const { return fb; } 33 double Get_c( void ) const { return fc; } 34 35 void Set_a( double a ) { fa = a; } 36 void Set_b( double b ) { fb = b; } 37 void Set_c( double c ) { fc = c; } 38 \\
Class public interface & Member functions located in the public section of a class are called the class public interface. They provide functionality for calling objects. & public: 40 41 42 // Helper functions to compute the discriminant of the quadratic equation; 43 // This is an inline function (definition of a function in the class) 44 double ComputeDelta( void ) const { return fb - 4.0 \* fa \* fc; } 45 46 // Define some constants for the class - using the scoped enum type 47 enum class E&qType { kNone, kOne, kTwo, kLinOne, kLinContra }; \\
\end{tabular}

## 172

# Table 3.11 (continued)

| Class member | Description | Example |
|---|---|---|
|  |  | ```cpp
75    //        contains root 2 if returned lone or two
76    //        (in the latter case root_2)
77    //
78    // OUTPUT:
79    //        return of the equation (number of roots)
80    //
81    // REMARKS:
82    //        The values referenced by theRoot_1 and theRoot_2
83    //        are undefined in all other cases than stated above.
84    //
85    //
86    EQType GetRoots( double & theRoot_1, double & theRoot_2 ) const;
87
88 };
```

Lines [40–88] of the class definition contain public member functions specific to the TQuadrEq class. The inline function ComputeQDelta, defined on line [44], returns discriminate delta of the quadratic equation. On line [47], the EQType scoped enumerated type is defined. It contains definitions of constant values that identify specific types of quadratic equations, which depend on the values of fa, fb, and fc.

The function GetNumOfRoots, declared on line [64], returns a type of equation. On line [86], GetRoots is declared, which computes the roots of the quadratic equation. Both are defined outside of the class definition.

```
```cpp
75    //        contains root 2 if returned lone or two
76    //        (in the latter case root_2)
77    //
78    // OUTPUT:
79    //        return of the equation (number of roots)
80    //
81    // REMARKS:
82    //        The values referenced by theRoot_1 and theRoot_2
83    //        are undefined in all other cases than stated above.
84    //
85    //
86    EQType GetRoots( double & theRoot_1, double & theRoot_2 ) const;
87
88 };
```
```

## 173

| Class member | Description | Example |
|---|---|---|
| **Input / output overloaded operators** | Most C++ operators can be overloaded (Section 4.4). This boils down to writing an operator-function that defines a specific behavior of an operator for the given class. An overloaded operator-function can be a member of a class or a function external to that class. | ```cpp
89    //
90    // Input/output operators (external functions)
91    std::ostream& operator << (std::ostream& os, const TQuadEdge& equation );
92    std::istream& operator >> (std::istream& is, TQuadEdge& equation );
93    ```

On lines [91–92], outside of the class definition, the overloaded streaming in and out operators are declared. They let us write TQuadEdge objects into and from any stream object from the iostream hierarchy, such as the keyboard, the screen, or a file. Their full definitions are in the source file. |

## 175

is used. The operations of the functions are explained in comment lines in the code. When developing a project, always maintain self-explaining source files.

The function `GetNumOfRoots` returns a constant of type `EEqType` indicating the type of the quadratic equation, including the number of roots if applicable. Notice that both identifiers are preceded by the class name and the scope operator, i.e. `TQuadEq::`.

```
/////////////////////////////////////////////////////////////////
// This function computes the roots of the equation,
// if possible.
/////////////////////////////////////////////////////////////////

// INPUT:
//          theRoot_1 - a reference to an object which
//                      contains root 1 if returned kNone, kOne, or kTwo
//          theRoot_2 - a reference to an object which
//                      contains root 2 if returned kOne or kTwo
//                      (in the first case root_1 == root_2)

// OUTPUT:
//          status of the equation (number of roots)

// REMARKS:
//          The values referenced by theRoot_1 and theRoot_2
//          are undefined in all other cases than stated above.

TQuadEq::EEqType TQuadEq::GetRoots( double & root_1, double & root_2 ) const
{
    auto delta ( ComputeDelta() );    // call a constructor for the built-in type

    EEquationType equationTypeFlag = GetNumOfRoots( delta );

    const double kDivThresh { 1e-36 };    // Used in assert to verify divisions

    // It is a good idea to explicitly place ALL the cases here (to be sure)
    switch( equationTypeFlag )
    {
        case EEqType::kLinContra:
        case EEqType::kNone:

            break;          // if none, then do nothing

        case EEqType::kLinNone:

            assert( fa == 0.0 );
            assert( std::fabs( fb ) > kDivThresh );

            if( std::fabs( fb ) < kDivThresh )
                throw std::logic_error( "Too low fb" );

            root_1 = root_2 = - fc / fb;

            break;          // return with one root

        case EEqType::kOne:
                                  // no break here - for these two cases, one solution
        case EEqType::kTwo:

            { // We need a block {} here for local variables

                assert( delta >= 0.0 ); // just in case, who knows?

```
```
```cpp
double delta_root = std::sqrt( delta );

double denominator = 2.0 * fa;
assert(std::fabs( denominator ) > kDivThresh);

if( std::fabs( denominator ) < kDivThresh )
    throw std::overflow_error( "Too low fa" );

root_1 = ( - fb - delta_root ) / denominator;
root_2 = ( - fb + delta_root ) / denominator;
}

break;

default :

    assert( false );    // this should not happen - an error in programming?
    break;
}

return equationTypeFlag;
}
```
```

GetRoots, defined on line [56], returns the type of the equation, as well as its root or roots, depending on the value of its discriminant, computed on line [58]. Based on its value, on line [60], the number of roots is returned by the GetNumOfRoots function. On line [62], a threshold value is defined that will be used to verify the feasibility of divisions. The switch statement on line [65] determines the processing method. For example, if the equation is not a quadratic equation, as checked on lines [67–68], the function simply exits. Note that the two cases are processed in the same way, since there is no break between them. Similarly, the two cases checked on lines [84, 86], are also processed the same way. The two roots are computed in accordance with formulas (2.6). Note that on line [97], the denominator is checked before the division takes place. If it is smaller than a predefined threshold, an exception is thrown on line [98]. If this happens, the thrown std::overflow_error object should be caught, as described in Section 3.13.2.5. However, if the divisor is large enough, the two roots are computed. Finally, although other options in the switch are not expected, it is a coding practice to include the default branch, as on line [106]. In our implementation, it contains only the assert fuse, followed by the break on line [109]. On line [112], the function returns the type of the equation.

Let’s briefly summarize the various methods and levels of error handling and software verification:

+   1. The assert function is active only in the debug version of the project (Section 3.15). When writing software, we make mistakes; assert, operating as a kind of fuse, greatly facilitates bug removal and software updates during the early stages of software development (see Figure 2.4). In other words, the responsibility of assert is to check conditions that the programmer assumes should be true in all software runs. In a production (release) version, assert is inactive. Until that point, asserts should never fail.

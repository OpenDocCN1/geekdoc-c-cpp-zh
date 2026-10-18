class, so indirect access does not add any time penalty. Also note that GetRe and GetIm are declared const to indicate that they do not change the state of the class. All member functions that are not intended to change member data should be declared const: this practice makes code safer since any inconsistencies will be caught by the compiler.

```
```cpp
public:

    // Getters & Setters to access data members of the class
    double GetRe( void ) const { return fRe; }     // "const" since we only read
    double GetIm( void ) const { return fIm; }     // data, not changing the state

    void SetRe( double re ) { fRe = re; }          // here we change the state
    void SetIm( double im ) { fIm = im; }          // so it is not "const"
```
```

Finally, we came to the *overloaded operators*. The first one, defined on line [79], is the comparison operator == (do not confuse it with assignment =). On line [81], it simply returns the result of the comparison of both data members. But let’s stop for a moment – to compare, we need two objects, whereas only c is provided as an argument in the definition of operator ==. Where is the other object? To answer this, note that, as for any other non-static member, the operator == code is executed on behalf of an object. We can easily see that this is the first object necessary for the comparison, while c is the second one. On the other hand, note that there is no definition of how to implement the ordering operator <.

```
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
```

At this point, we will provide a few facts about the overloaded operators in C++:

+   - Overloaded operators are overloaded functions that define special behavior for the operators
+   - Overloaded operators can be members of a class, or they can be standalone functions
+   - An overloaded operator is defined exactly like any other function, except that its name follows the pattern shown in (Figure 4.4)

![](bbox=[0.158, 0.764, 0.842, 0.889])

**Figure 4.4** Syntax of the overloaded operators in C++.
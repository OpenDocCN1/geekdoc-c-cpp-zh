```
void Display( double );                 // displays a double
void Display( const Widget& );          // displays a Widget
```

```
Display( 5 );                           // oops: creates and displays a Widget
```

*Example 2: Errors that work.* Say you provide **operator const char*** for a String class:

```
class String {
  // ...
public:
  operator const char*();               // deplorable form
};
```

Suddenly, a lot of silly expressions now compile. Assume **s1, s2** are Strings:

```
int x = s1 - s2;                       // compiles; undefined behavior
const char* p = s1 - 5;                 // compiles; undefined behavior
p = s1 + '0';                           // compiles; doesn't do what you'd expect
if( s1 == "0" ) { ... }                 // compiles; doesn't do what you'd expect
```

The standard string wisely avoids an **operator const char*** for exactly this reason.

# Exceptions

When used sparingly and with care, implicit conversions can make calling code short and intuitive. The standard **std::string** defines an implicit constructor that takes a **const char\***. This works fine because the designers took some precautions:

+   - There is no automatic conversion *to* **const char\***; that conversion is provided through two named functions, **c_str** and **data**.
+   - All comparison operators defined for **std::string** (e.g., **==, !=, <**) are overloaded to compare a **const char\*** and a **std::string** in any order (see Item 29). This avoids the creation of hidden temporary variables.

Even so, there can still be some weirdness with overloaded functions:

```
void Display( int );
void Display( std::string );
```

```
Display( NULL );                         // calls Display(int)
```

This result might be surprising. (Incidentally, if it did call **Display( std::string )**, the code would have exhibited undefined behavior because it’s illegal to construct a **std::string** from a null pointer, but its constructor isn’t required to check for the null.)

# References

[*Dewhurst03*] §36-37 • [*Lakos96*] §9.3.1 • [*Meyers96*] §5 • [*Murray93*] §2.4 • [*Sutter00*] §6, §20, §39
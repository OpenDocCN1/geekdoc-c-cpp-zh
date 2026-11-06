
## 40. Avoid providing implicit conversions.

### Summary

Not all change is progress: Implicit conversions can often do more damage than good. Think twice before providing implicit conversions to and from the types you define, and prefer to rely on explicit conversions (**explicit** constructors and named conversion functions).

### Discussion

Implicit conversions have two main problems:

- They can fire in the most unexpected places.
- They don’t always mesh well with the rest of the language.

Implicitly converting constructors (constructors that can be called with one argument and are not declared **explicit**) interact poorly with overloading and foster invisible temporary objects that pop up all over. Conversions defined as member functions of the form **operator T** (where T is a type) are no better—they interact poorly with implicit constructors and can allow all sorts of nonsensical code to compile. Examples are embarrassingly numerous (see References). We mention only two (see Examples).

In C++, a conversion sequence can include at most one user-defined conversion. However, when built-in conversions are added to the mix, the results can be extremely confusing. The solution is simple:

- By default, write **explicit** on single-argument constructors (see also Item 54):

  ```cpp
  class Widget { // ...
      explicit Widget( unsigned int widgetizationFactor );
      explicit Widget( const char* name, const Widget* other = 0 );
  };
  ```

- Use named functions that offer conversions instead of conversion operators:

  ```cpp
  class String { // ...
      const char* as_char_pointer() const;    // in the grand c_str tradition
  };
  ```

See also the discussion of **explicit** copy constructors in Item 54.

### Examples

*Example 1: Overloading.* Say you have a **Widget::Widget( unsigned int )** that can be invoked implicitly, and a **Display** function overloaded for **Widgets** and **doubles**. Consider the following overload resolution surprise:

```cpp
void Display( double );                 // displays a double
void Display( const Widget& );          // displays a Widget
```

```cpp
Display( 5 );                           // oops: creates and displays a Widget
```

*Example 2: Errors that work.* Say you provide **operator const char*** for a String class:

```cpp
class String {
  // ...
public:
  operator const char*();               // deplorable form
};
```

Suddenly, a lot of silly expressions now compile. Assume **s1, s2** are Strings:

```cpp
int x = s1 - s2;                       // compiles; undefined behavior
const char* p = s1 - 5;                 // compiles; undefined behavior
p = s1 + '0';                           // compiles; doesn't do what you'd expect
if( s1 == "0" ) { ... }                 // compiles; doesn't do what you'd expect
```

The standard string wisely avoids an **operator const char*** for exactly this reason.

### Exceptions

When used sparingly and with care, implicit conversions can make calling code short and intuitive. The standard **std::string** defines an implicit constructor that takes a **const char\***. This works fine because the designers took some precautions:

- There is no automatic conversion *to* **const char\***; that conversion is provided through two named functions, **c_str** and **data**.
- All comparison operators defined for **std::string** (e.g., **==, !=, <**) are overloaded to compare a **const char\*** and a **std::string** in any order (see Item 29). This avoids the creation of hidden temporary variables.

Even so, there can still be some weirdness with overloaded functions:

```cpp
void Display( int );
void Display( std::string );
```

```cpp
Display( NULL );                         // calls Display(int)
```

This result might be surprising. (Incidentally, if it did call **Display( std::string )**, the code would have exhibited undefined behavior because it’s illegal to construct a **std::string** from a null pointer, but its constructor isn’t required to check for the null.)

### References

[*Dewhurst03*] §36-37 • [*Lakos96*] §9.3.1 • [*Meyers96*] §5 • [*Murray93*] §2.4 • [*Sutter00*] §6, §20, §39

## 41. Make data members private, except in behaviorless aggregates (C-style structs).

### Summary

They're none of your caller's business: Keep data members private. Only in the case of simple C-style **struct** types that aggregate a bunch of values but don't pretend to encapsulate or provide behavior, make all data members public. Avoid mixes of public and nonpublic data, which almost always signal a muddled design.

### Discussion

Information hiding is key to good software engineering (see Item 11). Prefer making all data members private; private data is the best means that a class can use to preserve its invariants now, and to keep preserving them in the face of future changes.

Public data is bad if a class models an abstraction and must therefore maintain invariants. Having public data means that part of your class's state can vary uncontrollably, unpredictably, and asynchronously with the rest of its state. It means that an abstraction is sharing responsibility for maintaining one or more invariants with the unbounded set of all code that uses the abstraction, and that is obviously, fundamentally, and indefensibly flawed. Reject such designs outright.

Protected data has all the drawbacks of public data, because protected data still means that an abstraction is sharing the responsibility of maintaining some invariant with an unbounded set of code—in this case, with the unbounded set of current and future derived classes. Further, any code can read and modify protected data as easily as public data by deriving a new class and using that to get at the data.

Mixing public and nonpublic data members in the same class is confusing and inconsistent. Private data demonstrates that you have invariants and some intent to preserve them; mixing it with public data means a failure to decide clearly whether the class really is supposed to be an abstraction or not.

Nonprivate data members are almost always inferior to even simple passthrough get/set functions, which allow for robust versioning.

Consider hiding a class's private members using the Pimpl idiom. (See Item 43.)

### Examples

*Example 1: Proper encapsulation.* Most classes (e.g., **Matrix**, **File**, **Date**, **BankAccount**, **Security**) should have all private data members and expose adequate interfaces. Allowing calling code to manipulate their internals directly would directly work against the abstraction they provide and the invariants they must sustain.

## 42. Don’t give away your internals.

### Summary

**Don’t volunteer too much:** Avoid returning handles to internal data managed by your class, so clients won’t uncontrollably modify state that your object thinks it owns.

### Discussion

Consider:

```cpp
    class Socket {
    public:
        // ... constructor that opens handle_, destructor that closes handle_, etc. ...
        int GetHandle() const { return handle_; }   // avoid this
    private:
        int handle_;                                // perhaps an OS resource handle
    };
```

Data hiding is a powerful abstraction and modularity device (see Items 11 and 41). But hiding data and then giving away handles to it is self-defeating, just like locking your house and leaving the keys in the lock. This is because:

- *Clients now have two ways to implement functionality:* They can use your class’s abstraction (**Socket**) or directly manipulate the implementation that your class relies on (the socket’s C-style handle). In the latter case, the object is unaware of significant changes to the resource it thinks it owns. Now the class cannot reliably enrich or embellish functionality (e.g., proxying, logging, collecting statistics) because clients can bypass the embellished, controlled implementation—and any of the invariants it thinks it’s adding, which makes correct error handling next to impossible (see Item 70).

- *The class cannot change the underlying implementation of its abstraction because clients depend on it:* If **Socket** is later upgraded to support a different protocol with a different set of low-level primitives, calling code that fetches the underlying `handle_` and manipulates it incorrectly will be silently broken.

- *The class cannot enforce its invariants because calling code can alter state unbeknownst to the class:* For example, someone could close the handle being used by a **Socket** object without going through a **Socket** member function, thus rendering the object invalid.

- *Client code can store the handles that your class returns, and attempt to use them after your class's code has invalidated them.*

A common mistake is to forget that **const** is shallow and doesn't propagate through pointers (see Item 15). For example, **Socket::GetHandle** is a **const** member; as far as

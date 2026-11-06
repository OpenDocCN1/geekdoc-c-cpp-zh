
the compiler is concerned, returning **handle_** preserves constness just fine. However, raw calls to system functions using **handle_**’s value can certainly modify data that **handle_** refers to indirectly.

The following pointer example is similar, although we’ll see that the situation is slightly better because at least a **const** return type can reduce accidental misuses:

```cpp
class String {
  char* buffer_;
public:
  char* GetBuffer() const { return buffer_; }  // bad: should return const char*
  // ...
};
```

Even though **GetBuffer** is **const**, this code is technically valid and legal. Clearly, a client can use this **GetBuffer** to change a **String** object in quite major ways without explicit casting and therefore accidentally; for example, `strcpy( s.GetBuffer(), "Very Long String..." )` is legal code; in practice, every compiler we tried compiles it without a warning. Returning **const char*** instead from this member function would at least cause a compile-time error for such misuses so they could not occur accidentally; such calling code would have to write an explicit cast (see Items 92 to 95).

Even returning pointers to **const** does not eliminate all accidental misuses, because another problem with giving away object internals has to do with the internals’ validity. In the above **String** example, calling code might store the pointer returned by **GetBuffer**, then perform an operation that causes the **String** to grow (and move) its buffer, and finally (and apocalyptically) try to use the saved-and-now-invalidated dangling pointer to a buffer that no longer exists. Thus, if you do think you have a good reason to yield such internal state, you must still document in detail how long the returned value remains valid and what operations will invalidate it (compare this with the standard library’s explicit iterator validity guarantees; see [C++03]).

### Exceptions

Sometimes classes must provide access to internal handles for compatibility reasons, such as interfacing with legacy code or other systems. For example, **std::basic_string** offers access to its internal handle via the **data** and the **c_str** member functions for compatibility with functions that expect C-style pointers—but that presumably do not store those pointers or try to write through them! Such backdoor access functions are a necessary evil that should be used rarely and cautiously, and the conditions under which the handle remains valid must be carefully documented.

### References

*[C++03] §23 • [Dewhurst03] §80 • [Meyers97] #29 • [Saks99] • [Stroustrup00] §7.3 • [Sutter02] §9*

## 43. Pimpl judiciously.

### Summary

Overcome the language’s separation anxiety: C++ makes private members inaccessible, but not invisible. Where the benefits warrant it, consider making private members truly invisible using the Pimpl idiom to implement compiler firewalls and increase information hiding. (See Items 11 and 41.)

### Discussion

When it makes sense to create a “compiler firewall” that completely insulates calling code from a class’s private parts, use the Pimpl idiom: Hide them behind an opaque pointer (a pointer, preferably an appropriate smart pointer, to a class that is declared but not yet defined). For example:

```cpp
class Map {
  // ...
  private:
    struct Impl;
    shared_ptr<Impl> pimpl_;
};
```

The eponymous Pimpl should be used to store all private members, both member data and private member functions. This allows you to make arbitrary changes to your class’s private implementation details without any recompilation of calling code—an independence and liberty that is the hallmark of the idiom. (See Item 41.)

Note: Do declare the Pimpl using two declarations as shown. It would be legal, but have a different meaning, to combine the two lines and forward-declare the type and a pointer to it in one statement with `struct Impl* pimpl;`—but then `Impl` is in the enclosing namespace and not a nested type within your class.

There are at least three reasons you might use Pimpl, and they all stem from C++’s distinction between accessibility (whether you can call or use something) and visibility (whether you can see it and therefore depend on its definition). In particular, all private members of a class are inaccessible outside member functions and friends, but are visible to the entire world—to all code that sees the class’s definition.

The first consequence of this is potentially longer build times due to processing unnecessary type definitions. For private data members held by value, and for private member functions’ parameters taken by value or used in visible function implementations, types must be defined even if they can never be needed in this compilation unit. This can lead to longer build times. For example:

```cpp
class C {
  // ...

private:
  AComplicatedType act_;
};
```

The header file containing class C’s definition must also **#include** the header containing the definition for **AComplicatedType**, which in turn transitively includes every header that **AComplicatedType** might need, and so on. If the headers are extensive, compilation times can be noticeably affected.

The second consequence is creating ambiguity and name hiding for code that is trying to call a function. Even though private member functions can never be called from outside the class and its friends, they do participate in name lookup and overload resolution and so can render calls invalid or ambiguous. C++ performs name lookup and then overload resolution before accessibility checking. That’s why visibility gets priority:

```cpp
int Twice( int );                 // 1

class Calc {
public:
  string Twice( string );          // 2

private:
  char* Twice( char* );            // 3

  int Test() {
    return Twice( 21 );            // A: error, 2 and 3 are unviable (1 would be viable,
                                   // but it can't be considered because it's hidden)
  }
};

Calc c;
c.Twice( "Hello" );                // B: error, 3 is inaccessible (2 would be fine, but it
                                   // can't be considered because 3 is a better match)
```

On line A, the workaround is to explicitly qualify the call as **::Twice( 21 )** to force lookup to select the global function. On line B, the workaround is to add an explicit cast as **c.Twice( string("Hello") )** to force overload resolution to select the intended function. Some of these calling issues can be worked around in other ways than the Pimpl idiom, for example by never writing private overloads for member functions, but not all of the issues resolved by Pimpl have such alternative workarounds.

The third consequence is its impact on error handling and safety. Consider Tom Cargill’s Widget example:

## 44. Prefer writing nonmember nonfriend functions.

### Summary

Avoid membership fees: Where possible, prefer making functions nonmember nonfriends.

### Discussion

Nonmember nonfriend functions improve encapsulation by minimizing dependencies: The body of the function cannot come to depend on the nonpublic members of the class (see Item 11). They also break apart monolithic classes to liberate separable functionality, further reducing coupling (see Item 33). They improve genericity, because it's hard to write templates that don't know whether or not an operation is a member for a given type (see Item 67).

Use this algorithm to determine whether a function should be a member and/or friend:

```cpp
// If you have no choice then you have no choice; make it a member if it must be:
If the function is one of the operators =, ->, [], or (), which must be members:
    Make it a member.
// If it can be a nonmember nonfriend, or benefits from being a nonmember friend, do it:
Else if: a) the function needs a different type as its left-hand argument (as do operators >> or <<, for example); or b) it needs type conversions on its leftmost argument; or c) it can be implemented using the class's public interface alone:
    Make it a nonmember (and friend if needed in cases a) and b) ).
    If it needs to behave virtually:
        Add a virtual member function to provide the virtual behavior, and implement the nonmember in terms of that.
Else: Make it a member.
```

### Examples

*Example: **basic_string***. The standard **basic_string** is a needlessly monolithic class with 103 member functions—of which 71 could be written as nonmember nonfriends without loss of efficiency. Many of them duplicate functionality already available as algorithms, or are themselves algorithms that would be useful more widely if they weren't buried inside **basic_string**. (See Items 5 and 32, and [Sutter04].)

### References

[Lakos96] §3.6.1, §9.1.2 • [McConnell93] §5.1-4 • [Murray93] §2.6 • [Meyers00] • [Stroustrup00] §10.3.2, §11.3.2, §11.3.5, §11.5.2, §21.2.3.1 • [Sutter00] §20 • [Sutter04] §37-40

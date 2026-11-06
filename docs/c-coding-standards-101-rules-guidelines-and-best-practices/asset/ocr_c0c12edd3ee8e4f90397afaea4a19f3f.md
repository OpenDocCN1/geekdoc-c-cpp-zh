# 56. Whenever it makes sense, provide a no-fail swap (and provide it correctly).

# Summary

**swap** is both a lightweight and a workhorse: Consider providing a **swap** function to efficiently and infallibly swap the internals of this object with another’s. Such a function can be handy for implementing a number of idioms, from smoothly moving objects around to implementing assignment easily to providing a guaranteed commit function that enables strongly error-safe calling code. (See also Item 51.)

# Discussion

A **swap** function typically looks like this, where **U** is some user-defined type:

```
class T { // ...
public:
  void swap( T& rhs ) {
    member1_.swap( rhs.member1_ );
    std::swap( member2_, rhs.member2_ );
  }
private:
  U member1_;
  int member2_;
};
```

For primitive types and for standard containers, **std::swap** will do. Other classes might implement swapping as a member function under various names.

Consider using **swap** to implement copy assignment in terms of copy construction. The following implementation of **operator=** provides the strong guarantee (see Item 71), although at the price of creating an extra object, which can be inappropriate if there are more efficient ways to perform error-safe assignment for T objects:

```
T& T::operator=( const T& other ) {  // good: Variant #1 (traditional)
  T temp( other );
  swap( temp );
  return *this;
}

T& T::operator=( T temp ) {           // good: Variant #2 (see Item 27)
  swap( temp );                        // note: temp passed by value
  return *this;
}
```
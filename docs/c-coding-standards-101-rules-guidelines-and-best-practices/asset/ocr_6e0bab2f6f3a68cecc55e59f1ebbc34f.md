Always declare a predicate type’s **operator()** as a const member function so that the compiler can help you avoid this mistake by emitting an error if you try to change any data members that the predicate type may have. This won’t prevent all abuses—for example, it won’t flag accesses to global data—but it will help the compiler to help you avoid at least the most common mistakes.

# Examples

*Example: **FlagNth**. Here is the classic example from [Sutter02], which is intended to remove the third element from a container v:*

```
class FlagNth {
public:
  FlagNth( size_t n ) : current_(0), n_(n) { }

  // evaluate to true if and only if this is the n-th invocation
  template<typename T>
  bool operator()( const T& ) { return ++current_ == n_; }    // bad: non-const

private:
  size_t current_, n_;
};

// ... later ...

v.erase( remove_if( v.begin(), v.end(), FlagNth(3) ) );
```

This is not guaranteed to remove the third element, even though that was intended. In most real-world STL implementations, it erases both the third and the sixth elements. Why? Because **remove_if** is commonly implemented in terms of **find_if** and **remove_copy_if**, and it passes along a copy of the predicate to each of those functions, possibly after it has already itself done some work that affects the predicate’s state.

Conceptually, this example is perverse because **remove_if** only guarantees that it will remove all elements satisfying some criterion. It does not document the order in which elements in the range will be visited or removed, so the code is relying on an assumed, but undocumented and unsatisfied, assumption.

The correct way to remove a particular element is to iterate to it and then call **erase**.

# References

[Austern99] §4.2.2 • [Josuttis99] §5.8.2, §8.1.4 • [Meyers01] §39 • [Stroustrup00] §10.2.6 • [Sutter02] §2-3
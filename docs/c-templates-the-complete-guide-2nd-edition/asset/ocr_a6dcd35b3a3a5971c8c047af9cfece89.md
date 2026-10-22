of type T provide a specific member function or that they can be compared using operator <. See Section 19.6.3 on page 436 for a detailed example of such code.

See [Appendix E](#) for a detailed discussion of concepts for C++.

# 2.4 Friends

Instead of printing the stack contents with `printOn()` it is better to implement `operator<<` for the stack. However, as usual `operator<<` has to be implemented as nonmember function, which then could call `printOn()` inline:

```
```cpp
template<typename T>
class Stack {
...
void printOn() (std::ostream& strm) const {
...
}
friend std::ostream& operator<< (std::ostream& strm,
Stack<T> const& s) {
s.printOn(strm);
return strm;
}
};
```
```

Note that this means that `operator<<` for class `Stack<>` is not a function template, but an “ordinary” function instantiated with the class template if needed.²

However, when trying to *declare* the friend function and *define* it afterwards, things become more complicated. In fact, we have two options: 1. We can implicitly declare a new function template, which must use a different template parameter, such as U:

```
```cpp
template<typename T>
class Stack {
...
template<typename U>
friend std::ostream& operator<< (std::ostream&, Stack<U> const&);
};
```
```

Neither using T again nor skipping the template parameter declaration would work (either the inner T hides the outer T or we declare a nontemplate function in namespace scope).

2. We can forward declare the output operator for a `Stack<T>` to be a template,
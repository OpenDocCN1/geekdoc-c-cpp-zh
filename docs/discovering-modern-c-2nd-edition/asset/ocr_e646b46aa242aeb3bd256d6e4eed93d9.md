None of these three perspectives covers all implementations mentioned in this section. What is always true is that after moving from object `a` to object `b`, the value of `b` must be the original value of `a`. The value of `a` may be changed but should be something valid even when most objects are destroyed after move operations without further access to it. The fact that the value of `a` may change doesn’t mean that its value is arbitrary. Preferably, `a` should be empty but this isn’t always possible. Instead of repeating the discussion from above, we like to illustrate our idea of `a`’s value with the following, close to valid C++ pseudo-code:

Click here to view code image

```
T a = something, b(a), c(move(a)), d;
if (a != T() && a != b)
    cout << "Peter doesn't like T.\n";
// internal handover (one level)
if (a == T(size(b), value_type<T>()))
    cout << "Well, if really necessary ... okay.\n";
d = move(b);
if (a != b)
    cout << "Please make your operations consistent.\n";
```

**Summary:** We need a new perspective on move semantics. We shouldn’t see it as an accelerated copy where we don’t care much about the source. Wherever applicable, we should consider it as a different kind of operation that hands over all dynamically managed resources from one object to another. Many classes already do this. As for classes in the standard library, the source of the operation shall be left in a valid state. We strongly recommend imposing this requirement for user classes as well. Furthermore, we encourage you to specify in which state a moved-from object remains and that this state isn’t context-dependent. When possible with reasonable effort, the moved-from object should be in a well-defined empty state, ideally equivalent to that of a default-constructed object. With this perspective we get rid of xvalues, prvalues, and glvalues. More importantly, the usage of classes will be much safer when invalid objects are entirely eliminated by the class design. Software will also be much easier to understand and develop when we know in which state a moved-from object remains.

# C++11 2.3.6 Construct Objects from Literals
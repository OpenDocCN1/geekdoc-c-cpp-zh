```
```cpp
}
else {
    // implementation for all other iterators that are...
    if (...) {
        throw "adventureIter: invalid iterator category";
    }

    while (n > 0) {        // linear time for ...
        ++...
        --n;
    }
}
}
```
```

This is much clearer. The more-specialized code path (e.g., for random access iterators) will only be instantiated for types that can support them. Therefore, it is safe for code to involve operations not present on all iterators (such as +=) so long as it is within the body of an appropriately-guarded if constexpr.

However, there are downsides. Using constexpr if() in this way is only possible when the difference in the generic component can be expressed entirely within the body of the function template. We still need to establish in the following situation:

+   - Different “interfaces” are involved
+   - Different class definitions are needed
+   - No valid instantiation should exist for certain template argument lists.

It is tempting to handle that last situation with the following pattern:

Click here to view code image

```
```cpp
template<typename T>
void f(T x) {
    if constexpr (condition<T>::value) {
        // do something here...
    }
    else {
        // not a T for which f() makes sense
        static_assert(condition<T>::value, "can't call f()");
    }
}
```
```

Doing so is not advisable because it doesn't work well with SFINAE: The function f(T x) is not removed from the candidate list and therefore may inhibit another overload resolution outcome. In the alternative, using EnableIf<T>::... would be removed altogether when substituting EnableIf<...> fails substitution.

# 20.3.4 Concepts

The techniques presented so far work well, but they are often somewhat clumsy, may use a fair amount of compiler resources, and, in error cases, may lead to unwieldy diagnostics. Many generic library authors are therefore looking forward to a language feature that achieves the same effect more directly. A feature called concepts will likely be added to the language that reason; see Section 6.5 on page 103, Section 8.0 on page 377, and Appendix E.

For example, we expect our overloaded container constructors would simply look as follows:

Click here to view code image

```
```cpp
template<typename T>
class Container {
public:
    // construct from an input iterator sequence:
    template<typename Iterator>
    requires InputIterator<Iterator>
    Container(Iterator first, Iterator last);

    // construct from a random access iterator sequence:
    template<typename Iterator>
    requires IsRandomAccessIterator<Iterator>
```
```
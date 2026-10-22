# 20.3.3 Compile-Time if

It’s worth noting here that C++17’s constexpr if feature (see Section 8.5 on page 134) avoids the need for EnableIf in many cases. For example, in C++17 we can rewrite our advanceIter() example as follows: Click here to view code image

typeoverload/advance3.hpp

```
template<typename Iterator, typename Distance>
void advanceIter(Iterator& x, Distance n) {
if constexpr(IsRandomAccessIterator<Iterator>) {
// implementation for random access iterators:
x += n; // constant time
}
else if constexpr(IsBidirectionalIterator<Iterator>) {
// implementation for bidirectional iterators:
if (n > 0) {
for ( ; n > 0; ++x, --n) { //linear time for positive n
}
} else {
for ( ; n < 0; --x, ++n) { //linear time for negative n
}
}
}
else {
// implementation for all other iterators that are at least input iterators:
if (n < 0) {
throw "advanceIter(): invalid iterator category for negative n";
}
while (n > 0) { //linear time for positive n only
++x;
--n;
}
}
}
```

This is much clearer. The more-specialized code paths (e.g., for random access iterators) will only be instantiated for types that can support them. Therefore, it is safe for code to involve operations not present on all iterators (such as +=) so long as it is within the body of an appropriately-guarded if constexpr.

However, there are downsides. Using constexpr if in this way is only possible when the difference in the generic component can be expressed entirely within the body of the function template. We still need EnableIf in the following situations:

+   • Different “interfaces” are involved
+   • Different class definitions are needed
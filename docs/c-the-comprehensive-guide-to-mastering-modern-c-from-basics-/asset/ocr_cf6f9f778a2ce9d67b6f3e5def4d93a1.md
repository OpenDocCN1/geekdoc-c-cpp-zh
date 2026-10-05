```
std::ostream& operator<<=(std::ostream&os, const Elem&Comp&data) {
for(auto &e : data) {
    os << e;
}
return os << '\n'; // instead of'<<' for line break
}
int main() {
  // Example code here
}
```

**Listing 24.45** This is the template for the example listings in this section on "set".

Note that I overload the << for operator output with line breaks
only to keep the elements compact, as explained in more detail in the
box under Listing_24.12.

# The Elements and Their Properties

The elements that are packed into a set could also be called keys
because the internal tree structure is built based on them that
they can be quickly found.

Therefore, the elements must be sortable. What does that mean
specific? Two elements e and f must support e < f. That's
enough.

...Almost. Because this less-than must follow the usual
mathematical rules; otherwise, set won't work. That means:

+   * If e < f, then e> must be false (without having to
  implement;, mind you).
* Therefore it follows that both e < f is false and f < e is false,
then e == f must be true.

For example, if the element type is int and e and f are 5 and 11,
then 5 < 11. It follows that !(5 >= 11), and that is true. If e and f are
both 7, then e < f and f < e, so 7 < 7 is false, thus e == f, and that is
true.

However, if you engage in any unconventional folly, it may
to pass that set does not function as intended. For example, if you
define < such that it accidentally defines <= on your element type,
then set can no longer determine equality. If e with value 7 is
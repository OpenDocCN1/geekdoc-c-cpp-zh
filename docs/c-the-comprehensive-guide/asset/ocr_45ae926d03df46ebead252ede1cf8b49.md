```
os << "up: " << *up;
} else {
    os << "up:-";
}
// [lo,up] is now the same as what equal_range would have returned
os << " Range{";
for (; lo != up; ++lo) {
    os << *lo << ' ';
}
os << "}";
// count
os << " C:" << data.count(what) // count hits
   << "\n";
}
int main() {
    set data{ 10, 20, 30, 40, 50, 60 };
    search(data, 20, cout);  // 20? in:yes. found:20 lo:20 up:30 range:{20} C:1
    search(data, 25, cout);  // 25? in:no. lo:30 up:30 range:{} C:0
    search(data, 10, cout);  // 10? in:yes. found:10 lo:10 up:20 range:{10} C:1
    search(data, 60, cout);  // 60? in:yes. found:60 lo:60 up:range:{60} C:1
    search(data, 5, cout);   // 5? in: no. lo:10 up:10 range:{} C:0
    search(data, 99, cout);  // 99? in: no. lo:-- up:-- range:{} C:0
}
```

**Listing 24.56** These are the “set” search functions.

If the combination of return values seems strange to you, you might remember them by their typical use cases:

+   - `lower_bound` finds the search element or—if not present—its best insertion position.
+   - `equal_range` returns the range of all found elements, which is particularly useful for the multi... variants of the containers. If no element fits, the range is empty.
+   - `upper_bound` returns the first element that no longer fits.

It helps me to imagine that the found boundaries lie between the elements, not on the elements themselves. In Figure 24.11, I have drawn the returned iterators at the beginning of the element. If you imagine it that way, the terms `upper_bound` and `lower_bound` suddenly fit perfectly.

I mostly use `find` or `lower_bound` myself, and sometimes `equal_range` with `multiset`. `upper_bound` is used less frequently, but you can find an example in Listing 24.58.

The search functions are also available in the `<algorithms>` header for all compatible containers, especially for sequence containers. However, they must be sorted beforehand. You can find more about this in Chapter 25.
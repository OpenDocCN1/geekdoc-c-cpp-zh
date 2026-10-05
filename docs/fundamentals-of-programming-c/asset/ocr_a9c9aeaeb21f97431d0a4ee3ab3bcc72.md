# 18. ITERATOR RANGES

```
// small is the position of the smallest value we've seen
// so far; we use it to find the smallest value less
// than a[i]
auto small = i;
// See if a smaller value can be found in the sequence
for (auto j = i + 1; j != end; j++) {
    if (compare.compare(*j, *small))
        small = j; // Found a smaller value
}
// Swap a[i] and a[small], if a smaller value was found
if (i != small)
    Compare.swap(i,small);
}
```

+   * print
* contents of a sequence
* begin points to the beginning of the sequence.
* end points to the imaginary element just past the last.
* The function does not modify the sequence.

```
template <typename T>
void print(const T begin, const T end) {
    cout << '(';
    if (begin != end) {
        T iter = begin;
        cout << *iter; // Print the first element
        iter++; // Move to next element
        while (iter != end) { // Print the rest
            cout << ', ' << *iter;
            iter++; // Move to next element
        }
    }
    cout << ')';
}
```

+   * less_than(a, b)
* Returns true if a < b; otherwise, returns
* false.

```
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}
```

+   * greater_than(a, b)
* Returns true if a > b; otherwise, returns
* false.

```
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}
```
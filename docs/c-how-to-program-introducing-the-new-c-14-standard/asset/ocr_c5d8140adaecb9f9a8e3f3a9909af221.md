data that you’re iterating through—in this case the `string`. Iterator `iterator1` is initialized to the beginning of `string1` with the `string` class member function `begin`. Two versions of `begin` exist—one that returns an `iterator` for iterating through a non-`const` `string` and a `const` version that returns a `const_iterator` for iterating through a `const string`. Line 11 outputs `string1`.

Lines 15–18 use iterator `iterator1` to “walk through” `string1`. Class `string` member function `end` returns an `iterator` (or a `const_iterator`) for the position past the last element of `string1`. Each element is printed by *dereferencing* the iterator much as you’d dereference a pointer, and the iterator is advanced one position using operator `++`. In C++11, lines 9 and 15–18 can be replaced with a range-based `for`, as in

```
```cpp
for (char c : string1) {
    cout << c;
}
```
```

Class `string` provides member functions `rend` and `rbegin` for accessing individual string characters in reverse from the end of a `string` toward the beginning. Member functions `rend` and `rbegin`
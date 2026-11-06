The body of the loop dereferences `constIterator` to get the current element’s value. Remember that the iterator acts like a pointer to the element and that operator `*` is overloaded to return a reference to the element. The expression `++constIterator` (line 49) positions the iterator to the `vector`’s next element. Note that you can replace lines 48–51 with the following range-based `for` statement, which uses iterators in the same manner shown in `printVector`:

```
```cpp
{
    for (auto const& item : integers2) {
        cout << item << ' ';
    }
}
```
```

![](bbox=[0.119, 0.529, 0.192, 0.584])

# ## Common Programming Error 15.1

*Attempting to dereference an iterator positioned outside its container is a runtime logic error—the iterator returned by `end` or `cend` should never be dereferenced or incremented.*
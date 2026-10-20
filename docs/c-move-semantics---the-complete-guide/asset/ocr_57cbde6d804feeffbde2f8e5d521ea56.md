# 13.1.1 Declaring Move-Only Types

Move-only types have copying disabled. Usually, the copy constructor and the copy assignment operator are deleted, while the move constructor and move assignment operator are defaulted or implemented:

For example:

```
class MoveOnly {
public:
    // constructors:
    MoveOnly();
    ...
    // copying disabled:
    MoveOnly(const MoveOnly&) = delete;
    MoveOnly& operator= (const MoveOnly&) = delete;
    // moving enabled:
    MoveOnly(MoveOnly&&) noexcept;
    MoveOnly& operator= (MoveOnly&&) noexcept;
};
```

By rule, it would be enough to declare the moving special member function (because declaring special move members marks the copying members as deleted). However, explicitly marking the copying special member function with =delete makes the intention more clear.

# 13.1.2 Using Move-Only Types

With a declaration like the one above, you can create and move but not copy objects. For example:

```
std::vector<MoveOnly> coll;
...
coll.push_back(MoveOnly{});      // OK, creates a temporary object, which is moved into coll
...
MoveOnly mo;
coll.push_back(mo);              // ERROR: can't copy mo into coll
coll.push_back(std::move(mo));   // OK, moves mo into coll
```

To move the value of a move-only element out of the container, simply use std::move() for a reference to the element. For example:

```
mo = std::move(coll[0]);        // move assign first element (still there with moved-from state)
```

However, remember that after this call, the element is still in the container with a moved-from state.

Moving out all elements is also possible in loops:

```
for (auto& elem : coll) {        // note: non-const reference
    coll2.push_back(std::move(elem));  // move element to coll2
}
```

Again: the elements are still in the container with their moved-from state.
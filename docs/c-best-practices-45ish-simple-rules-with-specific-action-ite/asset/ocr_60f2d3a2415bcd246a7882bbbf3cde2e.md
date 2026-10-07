# 15. Prefer ranged-for Loop Syntax Over Old Loops

We'll illustrate this point with a series of examples.

```
int std::size_t i = 0; i < container.size(); ++i) {
  // oops mismatched types
}
```

Mismatched containers while looping.

```
for (auto itr = container.begin();
  itr != container2.end();
  ++itr) {
  // oops, most of us have done this at some point
}
```

Example of ranged-for loop.

```
for(const auto &element : container) {
  // eliminates both other problems
}
```

> Never mutate the container itself while iterating inside of a ranged-for loop.
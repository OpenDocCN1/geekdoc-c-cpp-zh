```
```cpp
// https://godbolt.org/z/8948besY8
map<string,string> data { {"John","Wayne"}, {"Cary","Grant"} };
cout << data;                         // Cary:Grant John:Wayne
data.rbegin()->second = "Travolta";   // Overwrite target
cout << data;                          // Cary:Grant John:Travolta
```
```

**Listing 24.65** You can change the value of a target.

If you use the range-based for, you get the pair as `e` directly and can access the key and target with `e.first` and `e.second`.

# Access via Iterators

As with all ordered associative containers, you get bidirectional iterators back with `[c][r]begin()` and `[c][r]end()`.

```
```cpp
// https://godbolt.org/z/16T5d0b75
map<char,int> data { {'a',1}, {'b',2}, {'c',3} };
for(auto it=data.rbegin(); it!=data.rend(); ++it) { // backwards
  cout << it->first << ':' << it->second << ' ';   // dereference with ->
}
cout << '\n'; // Output: c:3 b:2 a:1
for(auto &e: data)                         // forwards, uses begin() and end()
  cout << e.first << ':' << e.second << ' '; // pair, element access with .

cout << '\n'; // Output: a:1 b:2 c:3
```
```

**Listing 24.66** Iterators of “map” are of type “pair”.

# Access via Search

You can search for keys in the map using `find`, `upper_bound`, `lower_bound`, and `equal_range`.
You get an iterator to the found element or `end()`, back, as described with set. With
`count`, you can find out if a key occurs zero times or one time; with `contains`, you get
that information as a bool since C++20.

# Index-Like Access

As a special feature among associative containers, ordered or unordered, `map` has the
operator `[]` and at methods, which you know from vector and array. This allows you to
use a map as if it had an index. Unlike its counterparts, the index is not of type `size_t`,
but of type `Key`. Therefore, the argument for operator[] and at is a value of this type. As
shown in Listing 24.59 and Listing 24.64, operator[] automatically inserts missing ele-
ments if the key is not found. at, on the other hand, throws an `out_of_range` exception
in such cases. If you have a const map, you cannot use operator[], because it is not
marked as const due to the automatic insertion. This is demonstrated in Listing 24.67.
As you can see, duplicate keys are preserved. Duplicate targets are naturally possible with `map` anyway. The keys are kept sorted at all times, as you can see from the output.

# Assignment

The `multimap`, like `map`, has an `operator=` for copying or moving from another `multimap` afterwards. With `swap`, you can quickly exchange the contents of two `multimaps`.

`merge` transfers all elements between two `multimaps` and does not leave duplicates in the source as with `map`.

# Insert

You can insert new elements into the `multimap` with `insert`, `emplace`, `emplace_hint`, and from C++23 also `insert_range`. Unlike `map`, elements are always inserted, even if the new key already exists. What does not exist compared to `map` is `operator[]` for automatic insertion:

+   - **Inserting a single element with automatic positioning**  
+     As with `map`, you can use `insert` to add a new `pair<Key,Target>` to the `multimap`. With the `emplace` method, you provide Key and Target directly as parameters. Unlike with `map`, these two do not return a bool indicating the success of the insertion, but only an iterator with the position of the inserted element. This is demonstrated in [Listing 24.73](#).
+   - **Inserting a single element with a position hint**  
+     As with `map`, you can provide `insert` with an additional iterator as a position hint or use `emplace_hint` in the same way. If the hint is correct, then the insertion happens on average in O(1).
+   - **Inserting multiple elements**  
+     The insert of the `multimap` can also receive a pair of iterators, just like with `map`. Starting from C++23, you can also use `insert_range`.

The following listing shows how to insert elements into a `multimap`.

```
/// https://godbolt.org/z/dj68ej9r
using namespace std::literals; // for "s"

multimap<int,string> numlang{};
numlang.insert( std::make_pair(7, "seven"s) );
numlang.insert( std::pair<int,string>(7, "sieben"s) );
numlang.emplace( 7, "yedi"s );
cout << numlang; // Output: 7:seven 7:sieben 7:yedi
```

**Listing 24.73** “insert” and “emplace” in the “multimap”.

As you can see, identical keys are always inserted last among identical ones.
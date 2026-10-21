That is, we create a vector of elements that start with "id" or "ID" followed by an integral number:

```
id0 ID0 id1 ID1 id2 ID2 id3 ... id99 ID99 id100 ID100 ...
```

As usual, we can sort the elements sequentially as follows:

```
sort(coll.begin(), coll.end());
```

This can now be done by explicitly passing a “sequential” execution policy:

```
sort(std::execution::seq,
    coll.begin(), coll.end());
```

Passing sequential execution as a parameter can be useful if the decision whether to run sequentially or in parallel is taken at runtime and you do not want to have different function calls.

Requesting parallel sorting instead is easy:

```
sort(std::execution::par,
    coll.begin(), coll.end());
```

Note that there is also another parallel execution policy:

```
sort(std::execution::par_unseq,
    coll.begin(), coll.end());
```

I will explain the difference later.

So again, the question is, (when) is using parallel sorting better? On my laptop with only 10,000 strings, you could see that the parallel sorting took half the time of sequential sorting. And even sorting 1000 strings was slightly better with parallel execution.

# Combining with Other Improvements

Note that further modifications might give you more or additional benefits. For example, if we sort just by the numbers, using substrings without the two leading characters, we could use string operations inside the predicate and again see a two-fold improvement with parallel execution:

```
sort(std::execution::par,
    coll.begin(), coll.end(),
    [] (const auto& a, const auto& b) {
        return a.substr(2) < b.substr(2);
    });
```

However, substr() is a pretty expensive member function for strings because it creates and returns a new temporary string. By using class string_view, we see a three-fold improvement even with sequential execution:

```
sort(coll.begin(), coll.end(),
    [] (const auto& a, const auto& b) {
        return std::string_view{a}.substr(2) < std::string_view{b}.substr(2);
    });
```

We can easily combine using parallel algorithms and string views:
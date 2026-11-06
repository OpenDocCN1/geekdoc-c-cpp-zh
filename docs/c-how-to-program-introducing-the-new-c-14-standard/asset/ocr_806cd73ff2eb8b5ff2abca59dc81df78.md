pair containing an `int` and a `double`

```
```cpp
}
return (15, 2.7);
```
```

Lines 21–25 insert five additional `pairs` into the `multimap`. The range-based `for` statement in lines 30–32 outputs the contents of the `multimap`, including both keys and values. We infer the type of the loop’s control variable (a `pair` containing an `int` key and a `double` value) with keyword `auto`. Line 31 accesses the members of the current `pair` in each element of the `multimap`. Notice in the output that the keys appear in *ascending order*.

# *C++11: List Initializing a Key–Value Pair Container*

In this example, we used separate calls to member function insert to place key–value pairs in a `multimap`. If you know the key–value pairs in advance, you can use list initialization when you create the `multimap`. For example, the following statement initializes a `multimap` with three key–value pairs that are represented by the sublists in the main initializer list:
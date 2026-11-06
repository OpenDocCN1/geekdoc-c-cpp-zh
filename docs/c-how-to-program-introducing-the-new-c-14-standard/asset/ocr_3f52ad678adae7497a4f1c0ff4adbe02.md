Lines 13–14 create two `vector` objects that store values of type `int`—`integers1` contains seven elements, and `integers2` contains 10 elements. By default, all the elements of each `vector` object are set to `0`. Like `arrays`, `vectors` can be defined to store most data types, by replacing `int` in `vector<int>` with the appropriate type.

Notice that we used parentheses rather than braces to pass the size argument to each `vector` object’s constructor. When creating a `vector`, if the braces contain one value of the `vector`’s element type, the braces are treated as a *one-element initializer list*, rather than a call to the constructor that sets the `vector`’s size. So the following declaration

```
```cpp
vector<int> integers1(7);
```
```

actually creates a one-element `vector<int>` containing the `int` value `7`, not a 7-element `vector`.

# `vector` Member Function `size`, Function `outputVector`

Line 17 uses `vector` member function **size** to obtain the size (i.e., the number of elements) of `integers1`. Line 19 passes `integers1` to function `outputVector` (lines 95–101), which uses a range-based `for`
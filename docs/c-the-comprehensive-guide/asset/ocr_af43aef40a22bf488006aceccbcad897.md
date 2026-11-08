```
```cpp
cout << source;          // Output: 12 3 4 5
set target( std::move(source) ); // move instead of copy
cout << source;          // Output:
cout << target;          // Output: 12 3 4 5
```
```

# ### Assignment

operator=(const set<Elem>&) also is offered by set, so you can copy the contents of another set into a previously created set later. And because there is an overload for operator=(set<Elem>&&), this also works with moving:

```
```cpp
// https://godbolt.org/z/8eGWY45o
set source{1,2,3,4,5};
set<int> target{};
set<int> target2{};
cout << source;          // Output: 12 3 4 5
cout << target;          // Output:
cout << target2;         // Output:
target = source;         // copy afterward
cout << source;          // Output: 12 3 4 5
cout << target;          // Output: 12 3 4 5
target2 = std::move(source); // move
cout << source;          // Output:
cout << target2;         // Output: 12 3 4 5
```
```

The methods assign and assign_range do not exist for associative containers and thus also not for set. For sequence containers, this method is used to reinitialize an already existing container, providing similar parameter specification options as with a constructor call.

If you want the possibility of such constructor-like reinitialization for associative containers, you need to proceed differently. This can be done without losing performance. Listing 24.51 shows two possibilities.

```
```cpp
// https://godbolt.org/z/oZMY86ns8
#include <vector>
//...
set data{1,2,3,4,5};
std::vector source{10, 20, 30, 40, 50};

// There is no set::assign:
data.assign(source.begin(), source.end()); // // no set::assign
// So simulate it using a temporary set:
set temp(source.begin(), source.end()); // // copy from source...
data.swap(temp); // // ... efficiently swap contents
cout << data; // Output: 10 20 30 40 50
```
```
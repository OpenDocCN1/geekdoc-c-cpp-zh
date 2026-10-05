
```cpp
auto it = data.find(29);           // 29 now also finds 23
if(it != data.end()) {
    cout << "got it: " << it << "\n"; // Output: got it: 23
    data.insert(79);                            // nothing happens, 79 is already in
    cout << data;                               // Output: 14 23 56 71
}
```

## Listing 24.47 The comparison operation group elements.

So make sure your comparison operation, if possible, does the intuitive thing. If you have to program something nonintuitive, then think sufficiently, and keep in mind that it must adhere to the rules of the mathematical strict weak ordering.

If you have your own data type, it is best to overload operator<=> and let the compiler generate the necessary operator< from it.

```cpp
// https://cppbolt.org/z/W9skK4njK
#include <iostream>
#include <set>
#include <string>
struct Dwarf {
    std::string name;
    int height;
    auto operator<=>(const Dwarf& other) const {
        return other.height;
    }
};
int main() {
    std::set<Dwarf> dwarves = {
        {"Thorin", 148}, {"Balin", 136}, {"Kili", 138},
        {"Dwalin", 139}, {"Oin", 135}, {"Gloin", 137}
    };
    for(auto& d : dwarves) {
        std::cout << d.name << ' ';
    }
    // Output: Oin Balin Kili Gloin Dwalin
}
```

## Listing 24.48 A custom spaceship operator for "set" compatibility.

Here, <> only considers the height of the dwarves when comparing. If you want to consider all elements of the struct, then you can let the compiler generate the necessary comparison cascade = default.

```cpp
auto operator<=>(const Dwarf& other) const = default;
```

Here, the output is then sorted alphabetically.

As you can see, you can write `operator<>` as a normal member function. You do not need to define it as a `friend` or even outside the class.

## Initialize

In addition the element or key type `Key`, `set` also has a `comparator` `typename Compare` as a template parameter (as well as the obligatory allocator; see [Section 24.3](https://example.com). If you do not specify one, `std::less<Key>` is the default. This ultimately means that keys `e` and `f` are compared using less `<` to keep the set sorted. For built-in types like `int`, this is also the built-in `<`. For your own types, override the free function `operator<` or you need to specify your own comparator.

Only if `<` is not sufficient for you should define your own comparator. You need to define a kind of less-than less-than-equal `<=`; see [Listing 24.46](https://example.com). The comparator is something callable, with two `Key` parameters and `bool` as return type, or something implicitly convertible to these. This can be, as a usual, a function pointer, a lambda, or a functor.

A functor is practical here because then it is enough to specify its type as a template parameter. Alternatively, using C++17, you can use a lambda or a function pointer as a constructor argument, allowing you to omit the explicit template parameters.

```cpp
// https://godbolt.com/z/c8a9oPoPP
#include <set>
#include <functional> // function
using std::set; using std::function; using std::initializer_list;
bool fCompTens(int a, int b) { return a%10 < b%10; }
struct Fives {
    bool()(int a, int b) const { return a%5 < b%5; }
};

int main() {
    // Functor
    set<int, Fives> ff1;
    ff1.insert(5);
    set ff2{5, Fives()};
    set ff3(initializer_list<int>{5}, Fives());
    // Lambda
```

## Listing 24.49 There are various ways to specify a comparator.

The comparator can be specified in addition to the elements with which the set is to be initialized. Similar to the vector (Section 24.6.3), there are the following ways to pass the initial elements to the constructor:

- Without arguments (e.g., the default constructor)
- In a range from another container using a pair of iterators
- As another set for copying
- As an initializer list
- From C++23, as a range with the tag from_range

```cpp
// https://godbolt.org/z/qc9xxev95
// without arguments
set<int> empty();
cout << empty();
// initializer list
set list{1,1,2,3,3,4,4,5}; // set does not take duplicates
cout << list; // Output: 1 2 3 4 5
// copy
set copy(list);
cout << copy; // Output: 1 2 3 4 5
// pair of iterators
set from(next(list.begin()), std::prev(list.end()));
cout << from; // Output: 2 3 4
// Range
set even(from_range, list | vs::filter([](int i){ return i%2;}));
cout << even; // Output: 4
```

## Listing 24.50 There are again several ways to specify elements when constructing.

Shifts are possible because the move constructor is also defined.
For this, as usual, Elem must be movable:

```cpp
// https://godbolt.org/z/1dTPEd3nP
set source({1,2,3,4,5});
cout << source; // Output: 1 2 3 4 5
set target(std::move(source)); // move instead of copy
cout << source;
// Output:
cout << target;
// Output:
cout << target2;
// Output:
target = source;
// Output: 1 2 3 4 5
cout << target;
// Output: 1 2 3 4 5
target2 = std::move(source); // move
cout << source;
// Output:
cout << target2;
// Output: 1 2 3 4 5
```

## Assignment

operator=(const set<Elem>&) also is offered by set, so you can copy the contents of another into a previously created set later. And because there is an overload for operator=(set<Elem>&), this also works with moving:

```cpp
// https://godbolt.org/z/8EgvWy45o
set source({1,2,3,4,5});
set<int> target();
set<int> target2();
cout << source; // Output: 1 2 3 4 5
cout << target;
// Output:
cout << target2;
// Output:
target = source;
// Output: 1 2 3 4 5
cout << target;
// Output: 1 2 3 4 5
target2 = std::move(source); // move
cout << source;
// Output:
cout << target2;
// Output: 1 2 3 4 5
```

The methods assign and assign_range do not exist for associative containers.

```cpp
// https://godbolt.org/z/ozMY6ns8
#include <vector>
```

```cpp
// - 
set data(1,2,3,4,5);
std::vector source(10,20,30,40,50);

// There is no set::assign:
data.assign(source.begin(), source.end()); // No set::assign
// So simulate it using a temporary set:
set temp(source.begin(), source.end()); // copy from source
data.swap(temp); // efficiently swap
cout << data; // Output: 10 20 30 40 50
// or by clearing first and then inserting:
data.clear(); // clear -
data.insert(source.begin(), source.end()); // and insert
cout << data; // Output: 10 20 30 40 50
```

Listing 24.5 Instead of "assign" you can use the copy-and-swap idiom. In the first variant, I use a temporary set and apply the copy-and-swap idiom. The second option utilizes the fact that insert supports as many parameter combinations as the constructor.

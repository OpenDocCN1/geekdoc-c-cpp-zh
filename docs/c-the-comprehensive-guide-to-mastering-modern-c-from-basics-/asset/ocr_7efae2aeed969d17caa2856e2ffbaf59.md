Here, the output is then sorted alphabetically.

As you can see, you can write `operator<>` as a normal member function. You do not need to define it as a `friend` or even outside the class.

# Initialize

In addition the element or key type `Key`, `set` also has a `comparator` `typename Compare` as a template parameter (as well as the obligatory allocator; see [Section 24.3](https://example.com). If you do not specify one, `std::less<Key>` is the default. This ultimately means that keys `e` and `f` are compared using less `<` to keep the set sorted. For built-in types like `int`, this is also the built-in `<`. For your own types, override the free function `operator<` or you need to specify your own comparator.

Only if `<` is not sufficient for you should define your own comparator. You need to define a kind of less-than less-than-equal `<=`; see [Listing 24.46](https://example.com). The comparator is something callable, with two `Key` parameters and `bool` as return type, or something implicitly convertible to these. This can be, as a usual, a function pointer, a lambda, or a functor.

A functor is practical here because then it is enough to specify its type as a template parameter. Alternatively, using C++17, you can use a lambda or a function pointer as a constructor argument, allowing you to omit the explicit template parameters.

```
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
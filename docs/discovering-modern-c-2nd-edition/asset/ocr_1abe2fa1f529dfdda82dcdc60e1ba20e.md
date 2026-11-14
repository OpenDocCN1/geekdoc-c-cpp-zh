polymorphism in the function arguments: the types of the range `r` and the value `v` are instantiated during compilation while the output operator `<<` of `os` is selected at run time depending on the type that was actually referred to by `os`.

At this point, we want to draw your attention to the way we dealt with namespaces. When we use a lot of standard containers and algorithms, we can just declare:

```
using namespace std;
```

directly after including the header files, and we don't need to write `std::` any longer. This works fine for small programs. In larger projects, we run sooner or later into name clashes. They can be borious and annoying to fix (preventing is better than healing here). Therefore, we should import as little as possible—especially in header files. Our implementation of `print_interval` doesn't rely on preceding name imports and can be safely placed in a header file. Even within the function, we don't import the entire `std` namespace but limit ourselves to those functions that we really use.

Note that we did not qualify the namespace in some function calls, e.g., `std::begin(r)`. This would work in the example above, but we would not cover user types that define a function `begin` in the namespace of the class. The combination of `using std::begin` and `begin(r)` guarantees that `std::begin` is found. On the other hand, a `begin` function for a user type is found by ADL (§3.2.2) and would be a better match than `std::begin`. The same applies to `end`. In contrast, for the function `find` we didn't want to call possible user overloads and made sure that it is taken from `std`.

`find_if` generalizes `find` by searching for the first entry that holds a general criterion. Instead of comparing with a single value it evaluates a `Predicate` —a function returning a `bool`. Say we search the first `list` entry larger than 4 and smaller than 7:

Click here to view code image

```
bool check(int i) { return i > 4 && i < 7; }
```

```
int main ()
{
    list<int> seq= {3, 4, 7, 9, 2, 5, 7, 8};
    auto it= find_if(begin(seq), end(seq), check);
```
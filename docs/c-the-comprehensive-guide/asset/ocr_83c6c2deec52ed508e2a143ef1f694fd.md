When you define a functor—that is, a class with an `operator()`—it is sufficient to specify this class as a template parameter. When creating the `map`, an instance of the functor is then created using its default constructor. With a lambda, you already have an instance that is callable.

# ### Initialize

As a template parameter for `map`, you specify the types for `Key` and `Target`—for example:

```
```cpp
map<int,string>          // int as Key, string as Target
map<Person,size_t>       // Person to their age?
map<unsigned,unsigned>   // Key and target types can also be the same
map<int,shared_ptr<Image>> // a pointer as the target type is quite common
```
```

Optionally, you can specify the types of the comparator for `Key` (see previous section) as well as an `allocator`. If you specify one, you can optionally also provide the usual constructor arguments.

The following variants are commonly used as constructor arguments for initialization:

+   - Default constructor creates an empty container
+   - Iterator pair copies a range from another container or stream
+   - `map` copies an entire, other `map`
+   - Initializer list initializes with explicit values
+   - Constructor with the `from_range` tag and a range from C++23

For filling via an initializer list, you must consider that each element consists of a `pair`. So you must also specify `pair` elements here. Fortunately, pairs can also be created by a two-element initializer list, so the construct still looks compact, as shown in Listing 24-62.

```
```cpp
// https://godbolt.org/z/W4XsMPq7
using std::pair; using std::make_pair;
namespace literal_p { // better to put user-defined literals in a namespace
  constexpr pair<char,char> operator "" _p(const char* s, size_t len) {
      return len>=2 ? make_pair(s[0], s[1]) : make_pair('-', '-');
  }
}
struct Q {
  char a; int n;
  Q(char a, int n) : a{a}, n{n} {}
  operator pair<const char,int>() { return make_pair(a, n); }
};
// ...
// explicit pairs:
map<int,int> nums { pair<int,int>(3,4), make_pair(7,8), make_pair(11,23) };
map nums2 { pair<int,int>(6,1), make_pair(5,2) };
```
```
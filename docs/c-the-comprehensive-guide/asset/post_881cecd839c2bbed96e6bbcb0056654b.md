
Collectively, these are called *sequence containers*. You determine the order of the elements by the explicit insertion position (see Chapter 20).

In contrast, the ordered associative containers are always in an order defined by the elements themselves. For `map` and `set` as well as their relatives `multi_map` and `multi_set`, the order depends on the order in which you inserted the elements. When you check, the elements are in a consistent position.

`map` and `set` achieve this by keeping the elements in a sorted order at all times. The sorting is determined by the `operator<` free function. For example, because `operator<` is already defined for `int` and `string`, `set<int>` and `set<string>` work directly.

This does not apply to `Number` from Listing 12.36. When attempting to create `set<Number>` and insert an element with `insert`, the compiler reports an error. You need to overload the `operator<` appropriately.

```cpp
// https://godbolt.org/z/Yhzqo6dxT
#include <set>

struct Number {
    int value_ = 0;
    explicit Number(int v) : value_{v} {}
};
bool operator<(const Number& left, const Number& right) {
    return left.value_ < right.value_;
}
int main() {
    std::set<Number> numbers{};  // okay
    numbers.insert( Number{3} );  // operator< is needed here
}
```

**Listing 12.37** For a “set” of a custom data type, you need to override “operator<”.

The same applies to `map`. The sorting is done based on the key elements—that is, the first of the two types. For this, you need to provide `operator<`. For the values, copy and assignment are sufficient, and preferably also the move operations.

```cpp
// https://godbolt.org/z/TdEnhKxGK
#include <map>

struct Number {
    int value_ = 0;
    explicit Number(int v) : value_{v} {}
};

bool operator<(const Number& left, const Number& right) {
    return left.value_ < right.value_;
}

int main() {
    std::map<Number,int> numbers;                  // okay
    numbers.insert( std::make_pair(Number{4},100) ); // needs operator<
    numbers[Number{5}] = 200;                     // here as well
}
```

In a map, the elements are stored as `std::pair`. To insert an element using `insert` similarly to `set`, you create a `std::pair<Number,int>` pair—preferably with `std::make_pair`, as shown.

You can also insert a new key-value pair using `operator[]`. This saves you from using `make_pair`. Internally, this is a bit more complex for the compiler, but in most cases, you can ignore that.

A small note on `operator<`: even though the standard containers only require you to define `operator<` for your data type, you should at least consider defining the other operators, `>`, `>=`, `!=`, `<=`, and `==`, if you define `operator<`. For such a group of operations, it is always practical to provide the complete set so that users do not have to struggle or look up what is available. At least if `operator<` is not the only operation, you should support the entire group.

If you have good reasons to implement only `operator<`, consider also implementing `operator==`, which is needed for unordered associative containers. If you have `operator<`, you can check “not `a < b` and not `b < a`” as the ordered associative containers do, but you might have a more efficient implementation for your data type.

### 12.13.1 Three-Way Comparison: The Spaceship Operator

With C++20, you can define `greater`, `smaller`, `equal`, `smaller_equal`, and so on for custom types without overloading a bunch of operators and potentially making mistakes. Simply define the `operator<=>`, and your data type will support the complete set of operators, especially `<` and `==`, to be used in ordered containers.

If you insert the following definition for a custom data type, then the compiler generates `operator<=>` such that the elements are compared in the order in which they are defined in the class:

```cpp
auto operator<=>(const X& other) const = default;
```

> > **A Custom-Defined operator<=> Also Requires a Custom-Defined operator==**
> >
> > If you define operator<=> yourself, you should also define operator== yourself. This is because if you do not let the compiler generate operator<=> with `= default`, then operator== will not be generated automatically. It will be missing, and you will not be able to use `==` for your type.
> >
> > The reason is that the result of the == check can often be computed faster than the result of <=>, which covers the three <, ==, and > operators. So the compiler assumes that you have a better implementation for operator== if you already know better than the compiler what is good for operator<=>. Also, read the box in Chapter 24, Section 24.8.1.

With an operator<=> (and possibly operator==), the normal comparison operators ==, !=, <, <=, >, and >= can then be derived by the compiler. This is done using the new mechanism of *rewritten candidates*.

The operator<=> does not need to be a friend. A special case applies to it, allowing its implementation to access private elements without friend and behave as if it were defined as a free function.

If you want to highlight that your data type does not support operator<=>, then you can declare the operator with = deleted:

```cpp
struct X {
    Data data_;
    /* Comparisons would be too expensive and are not supported */
    auto operator<=>(const X& other) const = delete;
};
```

Even without the auto operator<=>... = delete line, comparisons would not be possible, but with the line, you make it clear to readers that you consciously do not support comparisons.

## Chapter 13: Namespaces and Qualifiers

- **Chapter Terminology**
  - **namespace**  
    Introduces a new namespace, either named or anonymous.
  - **namespace std**  
    In the std namespace, you will find all the identifiers of the standard library.
  - **static**  
    Marks a variable, function, or method as file-local, shared, or persistent.
  - **Singleton**  
    Popular design pattern in which only one instance of a type exists at most.
  - **const**  
    Marks something as immutable at runtime.
  - **constexpr**  
    Marks a constant or function as computable at compile time.
  - **consteval**  
    Lets the compiler guarantee that a function is computable at compile time.
  - **Const-correctness**  
    By using const on types, you can get help from the compiler in uncovering some typical errors.
  - **Type safety**  
    The correct use of types, including const, is enforced by the compiler with type safety.
  - **volatile**  
    Marker for volatile variables that can change without the compiler's knowledge.

In this chapter, you will learn about two quite different things: namespace and static. However, due to the multiple meanings of many keywords in C++, there are overlaps. Therefore, I have decided to go from namespace to the overlap with static within one chapter.

### 13.1 The “std” Namespace

All things in the standard library start with std::; you have seen this often. std::cout and std::vector are all in the std namespace. And in Chapter 4, Section 4.2, I explained how you can save the std:: prefix for a single identifier with using std::cout; and for all identifiers with using namespace std;.

But how does something get into a namespace in the first place? Simply enclose everything that should go into the namespace—let’s say plant—within namespace plant { ... }. This opens a scope, which behaves similarly to a class regarding identifiers: Within the range, you can omit plant for access to other elements; from outside, you need the plant:: prefix, as you can see in Listing 13.1.

Because this is about namespaces and using, I have refrained from using using std::string, using std::ostream, and the like globally at this point. I do this in this book, as already explained, only for space reasons. In a real project, you should use each using at the global level very sparingly (up to complete abstinence).

```cpp
// https://godbolt.org/z/qo6W3bh5d
#include <string>
#include <iostream>                 // ostream, cout
namespace plant {
    class Tree {
        std::string name_;
    public:
        explicit Tree(const std::string_view name) : name_{name} {}
        void print(std::ostream& os) const { os << name_; }
    };
    std::ostream& operator<<(std::ostream& os, const Tree& arg)
    { arg.print(os); return os; }
    using ConiferTree = Tree;        // for future extensions ...
    using BroadleafTree = Tree;      // ... provide for
    namespace exampleNames {         // embedded namespace
        std::string oakName = "Oak";
        std::string beechName = "Beech";
        std::string firName = "Fir";
    } // end namespace exampleNames
} // end namespace plant

int main() {  // main must not be in a namespace
    using namespace plant::exampleNames; // make all example names available
    plant::ConiferTree fir{ firName };
    plant::BroadleafTree oak{ oakName };
    fir.print(std::cout); std::cout << "\n";
}
```

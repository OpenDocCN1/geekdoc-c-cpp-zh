
- Functions and methods
You already know them: you define a header with return type, function name, call parameters, and the function body.

- Functors or function objects
A functor is a class that defines the operator().
Instances of this class then behave like a function.

- Anonymous functions or lambdas
If you want to pass an operation to an algorithm—for example, "How do I compare for sorting?”—you can pass the function body (the "How") directly as a parameter without defining a function beforehand. This is why it is called an *anonymous function or*, in computer science jargon, a *lambda expression*.

Instances of a class with an operator() method behave like functions. You can call them as in the following listing.

```cpp
// https://godbolt.org/z/xvfvG8hrd
#include <iostream> // cout
using namespace std;
class Increment {
    int amount_;
public:
    explicit Increment(int amount) : amount_{amount} {}
    int operator()(int value) const { // makes instances callable
        return value + amount_;
    }
    void clear() {
        amount_ = 0;
    }
};
int main() {
    Increment PlusFour(4); // create instance
    Increment PlusEleven(1); // another instance
    cout << PlusFour(8) << "\n"; // Output: 12
    int result = 2 * PlusEleven(5) - 7; // result is 25
    cout << PlusEleven(result/5) << "\n"; // Output: 16
    cout << 3 * Increment{1}(7) << "\n"; // Output: 24
    Increment plusZero = plusEleven;
    plusZero.clear(); // change state
    cout << plusZero(1) << "\n"; // Output: 1
}
```

### Listing 23.15 A class with "operator()" creates function objects

If you only looked at the line with plusFour(8), it would seem as if plusFour hides the function:

```cpp
int plusFour(int value) {
  return value + 4;
}
```

And if you looked at the line plusEleven(result/5), you might assume there is a function:

```cpp
int plusEleven(int value) {
  return value + 1;
}
```

This could continue with +0, +2, and so on—and you would wonder why to write so many functions. This is where function objects come into play. If a group of functions is very similar and only differs by one detail that can be represented by an internal state, then a class with data fields is the optimal solution. Let's develop this slowly. If you use ways you already know, you can write and use a class with normal methods as in the next listing.

```cpp
// https://godbolt.org/z/xa
#include <iostream> // cout
using namespace std;
class Add {
    int amount_;
public:
    explicit Add(int amount) : amount_(amount) {}
    int add(int value) const { // instead of operator()
        return value + amount_;
    }
    void clear() { amount_ = 0; }
};
int main() {
    Add plusFour(4); // create instance
    Add plusEleven(1); // another instance
    cout << plusEleven.add(8) << "\n"; // Output: 12
    int result = 2 * plusEleven.add(5) - 7; // result is 25
    cout << plusEleven.add(result/5) << "\n"; // Output: 16
    cout << plusEleven.add(7) << "\n"; // Output: 24
    Add plusZero = plusEleven;
    plusZero.clear(); // change state
    cout << plusZero.add(1) << "\n"; // Output: 1
}
```

### Listing 23.16 A class with a normal method

In fact, there are only two differences:

- Increment defines operator()(int value) const as a method, while Add uses a normal add(int value) const for this.
- The call in the first case is plusFour(8), in the second case plusEleven.add(8).

You see that the two classes actually differ only in that you save typing .add(...) when using instances directly—like a function call. That's exactly why instances of classes with operator() are called function objects. The class with operator() itself is called a functor.

The Increment functor is indeed a rather complicated representative of its kind. In fact, the functor has neither an internal state like amount_ nor modifiers like clear(). The functor is actually more like a different way to write a function—pardon me, a callable object. Thus, function objects integrate into the rest of C++ structure:

- You can write classes with operator().
- operator() can be virtual.
- You can overload operator()—that is, write multiple variants with different types.
- You can represent internal states, as you have seen, and create variants via constructors.
- And, not least, you manipulate function objects like any other—for example, to put them in a container.

Most functors are rather simple in design. You often use them as an interface between your own classes and the algorithms of the standard library.

## 23.3.4 Practical Functors

A set<Type> is always sorted according to operator<>(). For example, you can create a list sorted by name with set<Dwarf> and the appropriate operator<.

```cpp
// https://godbolt.org/z/ov87
#include <set>
#include <string>
#include <iostream> // cout
using namespace std;
using namespace std;
struct Dwarf {
    string name;
    unsigned year;
    bool operator<(const Dwarf& a, const Dwarf& b) {
        return a.name < b.name;
    }
};
int main() {
    set<Dwarf> dwarves {Dwarf("Balin", 2763), Dwarf("Dwalin", 2772), Dwarf("Oin", 2774), Dwarf("Gloin", 2783), Dwarf("Thorin", 2746), Dwarf("Fili", 2859), Dwarf("Kili", 2864)};
    for(const auto& z : dwarves) // sorted output: Balin to Thorin
        cout << z.name << "\n";
}
```

### Listing 23.17 With "operator<" as a function, you can implement one sort order.

By the way: since C++20, instead of operator<>(), you simply write auto operator<=> = default. This way, you get the output sorted by name:

Balin Dwalin Fili Gloin Kili Oin Thorin

Assume that fulfilled 95% of your program's purpose, but in 5% of the cases you want to output by age. What can you do? You can define one operator< (except with multiple namespaces). For this purpose, set offers a second template parameter. Provide set with a functor that has the appropriate comparison operation. This will then be used instead of operator< for sorting. Insert the following functor into Listing 23.17.

```cpp
struct ByYear { // implements less-than by Dwarf::year
    bool operator()(const Dwarf& a, const Dwarf& b) const {
        return a.year < b.year_;
    };
```

### Listing 23.18 A no-frills functor with great utility.

Then you can achieve sorting by the birth year of the dwarves with the following addition in main:

```cpp
// https://godbolt.org/PebG9Bn9K
set<Dwarf,ByYear> dwarves2(begin(dwarves), end(dwarves));
for(const auto& z : dwarves2) // differently sorted
    cout << z.year << " ";
```

dwarves2 stores a copy of all elements from dwarves, because the constructor takes two iterators and copies all elements. This time, however, the elements are sorted using the ByYear functor. Instead of calling operator< for each comparison, the following is now used:

```cpp
bool ByYear::operator()(const Dwarf&, const Dwarf&) const;
```

Thus, you get the following output:

2746 2763 2772 2774 2783 2864

As you can see, you cannot use the C++17 feature to omit the Dwarf template parameter, because you have to provide the second parameter with ByYear; the compiler cannot deduce it. But set has a constructor that can do exactly that. Here, I pass ByYear{} as a constructor argument, and thus the compiler can deduce the template parameters:

```cpp
set<Dwarf, ByYear> dwarves2{begin(dwarves), end(dwarves), ByYear{}};
```

## 23.3.5 Algorithms with Functors

Only interesting for the classes of standard containers. Many helper functions that can be found in the standard library can be modified in behavior with a callable object.

For example, you can sort a vector using the same mechanism with operator< if you use the sort() function from the <algorithm> header.

```cpp
// https://godbolt.org/YKzsW4nG8
#include <vector>
#include <algorithm> // sort
// Definitions and further includes as before
int main() {
    vector<Dwarf> dwarves{} // initialize as before
    /* sort */
    std::sort(begin(dwarves), end(dwarves));
    // output as ...
}
```

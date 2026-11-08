
The plain call of `typeid(...).name()` provides a name, but not a reliable one. For me, it returns `int` simply as “i”. And for an iterator or a template like `map`, the output is only limitedly informative.

You counteract this by applying `type_index(...)` to the result of `typeid`—that is, to the `const type_info&`. As you can see in the names example, you can also populate a map with more readable names this way.

Note that you can use both plain types like `int` or `string::const_iterator` as a parameter for `typeid`, as well as an expression like `integer`, `*one`, or `string("World").begin()`. The expression is not executed; only its type is considered. `typeid(666/0)` would otherwise cause the program to crash.

Finally, compare the results of `typeid(*one)` and `typeid(*two)`. These are polymorphic objects, as both are statically of type `Base`. Dynamically—at runtime—the objects actually have the `Derived_one` and `Derived_two` types. With `typeid`, you can obtain dynamic type information. Note that this is a slightly different use of the typeid operator, where it is again necessary for the compiler to execute the expression. Because `Base` contains a virtual method, the compiler recognizes that you need dynamic type information and must therefore execute the expression.

My approach of writing all desired types beforehand into a map like names is not always feasible in practice. You might not know in advance what types you will encounter. Then you have only two options:

- You have to make do with `type_info::name()`, even if it is not portable.
- You use `demangled_name` from Boost.

The Boost library provides `boost::core::demangled_name(...)`, which returns well-readable type information. Use not `typeid` but the `BOOST_CORE_TYPEID` macro to get the argument for the function. Although Boost cannot guarantee 100% that this name is readable or stable, the library is so well maintained that it is effectively so.

The outputs for templates will never be pretty, but at least they are readable.

```cpp
// https://godbolt.org/z/h54566ccqT
#include <iostream>
#include <typeinfo>
#include <string>
#include <map>
#include <boost/core/typeinfo.hpp>
int main() {
    using std::string; using std::cout;
    std::map<int, string> names;
    int i;
    double f;
    // demangled_name
    using boost::core::demangled_name;
    cout<<demangled_name(BOOST_CORE_TYPEID(i))<<'\n';        // Output: int
    cout<<demangled_name(BOOST_CORE_TYPEID(f))<<'\n';        // Output: double
    cout<<demangled_name(BOOST_CORE_TYPEID(string))<<'\n';   // Output: std::string
    cout<<demangled_name(BOOST_CORE_TYPEID(string{}.begin()))<<'\n';
    // Output: __gnu_cxx::__normal_iterator<char*, std::string>
    cout<<demangled_name(BOOST_CORE_TYPEID(names))<<'\n';
    // Output: std::map<int, std::string, std::less<int>,
    //          std::allocator<std::pair<int const, std::string> > >
    cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\n';      // Output: int
}
```

**Listing 28.42** Boost's “demangled_name” is extremely useful for outputting type names.

## 28.7 Helper Classes around Functors: “`<functional>`”

Even more than `<numeric>`, the functions in `<functional>` are there to complement other parts of the standard library. You will rarely include `<functional>` alone. And if you want to solve a “simple” task with `<algorithm>` or a container, it's worth taking a look at `<functional>`, where there might already be a solution for it.

If you want to sum up all elements of a container, for example, use `accumulate` from `<numeric>`. But if you want to use `*` instead of `+`, you can

- either write `[](auto a, auto b) { return a*b; }`;
- or use `multiplies` from `<functional>`, which does exactly that.

And so it is with many things from `<functional>`.

I categorize the things offered in `<functional>` (more or less arbitrarily) into the following areas:

- **Function factories**
  `function` is the central point for everything callable in C++. `bind` creates a new function object with one less argument from a function object and an argument. `mem_fn` creates a function object from a method. There are several auxiliary constructs in this context.

- **Concrete function objects**
  For arithmetic (like `multiplies`), comparisons (like `equal_to`, `logical_and`, etc.), and bitwise (`bit_and`, etc.) operations, which you can use instead of a simple lambda.

- **Specialized hash functions**
  The hash function objects needed for the *unordered* containers are defined here for the built-in types. So, for example, you will find the template specialization `hash<int>` and all its relatives. That should be self-explanatory, so I will not go into further detail here.

### 28.7.1 Function Objects

In Chapter 25, Listing 25.15, there’s an example of `multiplies` together with `accumulate` from `<numeric>`. The other defined function objects can be found in Table 28.11 to Table 28.14.

| Functor | Behavior | Functor | Behavior |
|---|---|---|---|
| `plus` | `a + b` | `divides` | `a / b` |
| `minus` | `a - b` | `modulus` | `a % b` |
| `multiplies` | `a * b` | `negate` | `-a` |

**Table 28.11** Function objects of arithmetic operators.

| Functor | Behavior | Functor | Behavior |
|---|---|---|---|
| `equal_to` | `a == b` | `less` | `a < b` |
| `not_equal_to` | `a != b` | `greater_equal` | `a >= b` |
| `greater` | `a > b` | `less_equal` | `a <= b` |

**Table 28.12** Function objects for comparison operators.

| Functor | Behavior | Functor | Behavior |
|---|---|---|---|
| `logical_and` | `a && b` | `logical_not` | `!a` |
| `logical_or` | a \|\| b |  |  |

**Table 28.13** Function objects for logical operators.

| Functor | Behavior | Functor | Behavior |
|---|---|---|---|
| `bit_and` | `a & b` | `bit_xor` | `a ^ b` |
| `bit_or` | a \| b | `bit_not` | `~a` |

**Table 28.14** Function objects for bitwise operators.

You can use the function objects to equip containers and algorithms with your own functionality.

For example, in the definition of `std::set`, you will see that `less` from `<functional>` is used here for a comparison operation:

```cpp
namespace std {
    template<class Key, class Compare=less<Key>, class Allocator=allocator<Key>>
      class set;
      // ...
}
```

So instead of overloading `operator<` for your own data type, you can also specialize the `less` template for your data type, similar to what you would do for `hash` in the context of `unordered_set`:

```cpp
// https://godbolt.org/z/Y3GsPd97d
#include <set>
#include <string>
struct Dragon {
    std::string name_;
};
namespace std {
    template<> struct less<Dragon> { // Template specialization
        bool operator()(const Dragon &lhs, const Dragon &rhs) const {
            return lhs.name_ < rhs.name_;
        }
    }; }
int main() {
    std::set<Dragon> dragons {
        Dragon{"Smaug"},    Dragon{"Glaurung"},
        Dragon{"Ancalagon"},Dragon{"Scatha"}};
}
```

So if for any reason it is not possible or desired to overload `operator<` for Dragon, and you also do not want to specify the template parameter Compare, you can achieve the same with a specialization of `less`.

In Listing 28.43, you see a version of the calculator from Chapter 8, Listing 8.18 that uses `<functional>` from start to finish. Instead of a large switch statement, this time all possible characters are stored as keys in maps. Depending on how the stack should be manipulated, the operations end up in one of four maps:

- **binOps**
  Remove two elements from the stack, apply the function to them, and store the result back on the stack. Addition is an example of this.

- **unOps**
  Remove one element from the stack, apply the function to it, and store the result back on the stack. This calculator does not have such an operation.

- **zeroOps**
  Execute a zero-argument function and store the result on the stack. The digits do exactly this.

- **stackOps**
  Instead of manipulating the stack before and after, the calculator leaves the entire stack to these functions—for example, to clear or print it.

Of course, not everything can be represented with predefined functors, which is why you will see lambdas in use where necessary—and with `val`, even a lambda that returns a lambda. It’s often said that this makes “lambdas as first-class citizens”, which means that they are in most ways values like variables of built-in types or classes and thus can be created, passed as parameters, and even put into containers.

This type of calculator is not generally “better” than using the switch statement. However, when it comes to extensibility, this option is the more skillful choice.

There are a few things I would definitely improve “in the real world”:

- Instead of using `std::cout` as a global variable, the operators should be parameterized on `ostream&`.
- The various find calls should only be executed when necessary.
- Processing individual digits is illustrative but impractical. Sequences of digits should be whole numbers, with the space as the delimiter.

```cpp
// https://godbolt.org/z/jxvhded75
#include <string>
#include <vector>
#include <iostream>
#include <map>
#include <functional>
std::map<char,std::function<int(int,int)>> binOps { // binary operators
    {'+', std::plus<int>{} },
    {'-', std::minus<int>{} },
    {'*', std::multiplies<int>{} },
    {'/', std::divides<int>{} },
    {'%', std::modulus<int>{} },
};
std::map<char,std::function<int(int)>> unOps { };    // unary operators
auto val = [](auto n) { return [n]() { return n; }; }; // returns a lambda
std::map<char,std::function<int()>> zeroOps { // nullary operators
    {'0', val(0)}, {'1', val(1)}, {'2', val(2)}, {'3', val(3)}, {'4', val(4)},
    {'5', val(5)}, {'6', val(6)}, {'7', val(7)}, {'8', val(8)}, {'9', val(9)},
};
std::map<char,std::function<void(std::vector<int>&)>> stackOps {
    {' ', [](auto &stack) { }},                    // no operation
    {'c', [](auto &stack) { stack.clear(); }},     // Clear the entire stack
    {'.', [](auto &stack) {
        auto top = stack.back(); stack.pop_back();
        auto second = stack.back(); stack.pop_back();
```

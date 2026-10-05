
```cpp
using boost::core::demangled_name;
cout<<demangled_name(BOOST_CORE_TYPEID(i))<<'\n'; // Output: int
cout<<demangled_name(BOOST_CORE_TYPEID(f))<<'\n'; // Output: float
cout<<demangled_name(BOOST_CORE_TYPEID(double))<<'\n'; // Output: double
std::string s;
cout<<demangled_name(BOOST_CORE_TYPEID(s.begin()))<<'\n'; // Output: gnu cxx::normal_iterator<char*, std::cxx::basic_string<char>*>
cout<<demangled_name(BOOST_CORE_TYPEID(name))<<'\n'; // Output: std::map<int, std::string, std::less<int>>
std::allocator<std::pair<int, const, std::string>> alloc;
cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\n'; // Output: int
```

**Listing 28.42** Boost’s “demangled_name” is extremely useful for outputting type names.

## 28.7 Helper Classes around Functors: "<functional>"

Even more than <numeric>, the functions in <functional> are there to complement other parts of the standard library. You will rarely include <functional> alone. And if you want to solve a “simple” task with <algorithm> or a container, it's worth taking a look at <functional>, where there might already be a solution for it.

If you want to sum up all elements of a container, for example, use accumulate from <numeric>. But if you want to use * instead of +, you can:

- either write a lambda [](auto a, auto b) { return a*b };
- or use multiplies from <functional>, which does exactly that.

And so is it with many other things from <functional>.

I categorize the things offered in <functional> (more or less arbitrarily) into the following areas:

- Function `function` is the central point for everything callable in C+. `bind` creates a new function object with one less argument from a function object. `mem_fn` creates a function object from a method. There are several auxiliary constructs in this context.

- Concrete function objects for arithmetic (like `multiples`), comparisons (like `equal_to`), logical (`logical_and`, etc.), and bitwise (`bit_and`, etc.) operations, which you can use instead of a simple lambda.

- Specialized hash functions: The hash function objects needed for the unordered containers are defined here for the built-in types. So, for example, you will find the template specialization `hash<int>` and all its relatives. That should be self-explanatory, so I will not go into further detail.

In Chapter 25, Listing 25.15, there's an example of multiplies together with accumulate from <numeric>. The other defined function objects can be found in Table 28.11 to Table 28.14.

| Functor | Behavior | Functor | Behavior |
| --- | --- | --- | --- |
| plus | a + b | divides | a / b |
| minus | a - b | modulus | a % b |
| multiplies | a * b | negate | -a |

**Table 28.11** Function objects of arithmetic operators.

| Functor | Behavior | Functor | Behavior |
| --- | --- | --- | --- |
| equal_to | a == b | less | a < b |
| not_equal_to | a != b | greater_equal | a >= b |
| greater | a > b | less_equal | a <= b |

**Table 28.12** Function objects for comparison operators.

| Functor | Behavior | Functor | Behavior |
|---|---|---|---|
| logical_and | a && b | logical_not | !b |
| logical_or | a || b | | |

**Table 28.13** Function objects for logical operators.

| Functor | Behavior | Functor | Behavior |
|---|---|---|------|
| bit_and | a & b | bit_xor | a ^ b |
| bit_or | a \| b | bit_not | ~b |

**Table 28.14** Function objects for bitwise operators.

You can use the function objects to equip containers and algorithms with your own functionality.

For example, in the definition of std::set, you will see that less from <functional> is used here for a comparison operation.

```cpp
namespace std {
    template<class Key, class Compare=less<Key>, class Allocator=allocator<Key>>
        class set;
    //...
}
```

So instead of overloading operator< for your own data type, you can also specialize the `less` template for your data type, similar to what you would do for hash in the context of `unordered_set`:

```cpp
// https://godbolt.org/z/Y3GsPd9d7
#include <set>
#include <string>

struct Dragon {
    std::string name;
};
namespace std {
    template<> struct less<Dragon> { // Template specialization
        bool operator()(const Dragon &lhs, const Dragon &rhs) const {
            return lhs.name < rhs.name;
        }
    }};
}
int main() {
    std::set<Dragon> dragons {
        Dragon("Smaug"), Dragon("Glaurung"),
        Dragon("Ancalagon"), Dragon("Scatha")
    };
}
```

So if for any reason it is not possible or desired to overload operator< for Dragon, and you also do not want to specify the template parameter Compare, you can achieve the same with a specialization of less.

In Listing 28.43, you see a version of the calculator from Chapter 8, Listing 8.18 that uses <functional> from start to finish. Instead of a large switch statement, this time all possible characters are stored as keys in maps. Depending on how the stack should be manipulated, the operations end up in one of four maps:

- binOps: Remove two elements from the stack, apply the function to them, and store the result back on the stack. Addition is an example of this.
- unOps: Remove one element from the stack, apply the function to it, and store the result back on the stack. This calculator does not have such an operation.
- zeroOps: Execute a zero-argument function and store the result on the stack. The digits do exactly this.
```

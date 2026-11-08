```
```cpp
cout<<demangled_name(BOOST_CORE_TYPEID())<<'\\n';        // Output: int
cout<<demangled_name(BOOST_CORE_TYPEID(const))<<'\\n';  // Output: double
cout<<demangled_name(BOOST_CORE_TYPEID(string))<<'\\n'; // Output: std::string
cout<<demangled_name(BOOST_CORE_TYPEID(string{}).begin())<<'\\n';
// Output: __gnu_cxx::__normal_iterator<char*, std::string>
cout<<demangled_name(BOOST_CORE_TYPEID(name))<<'\\n';
// Output: std::map<int, std::string, std::less<int>,
//          std::allocator<std::pair<int const, std::string> > >
cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\\n'; // Output: int
}
```
```

**Listing 28.42** Boost's “demangled_name” is extremely useful for outputting type names.

# 28.7  Helper Classes around Functors: “<functional>”

Even more than <numeric>, the functions in <functional> are there to complement other parts of the standard library. You will rarely include <functional> alone. And if you want to solve a “simple” task with <algorithm> or a container, it's worth taking a look at <functional>, where there might already be a solution for it.

If you want to sum up all elements of a container, for example, use accumulate from <numeric>. But if you want to use * instead of +, you can

+   - either write `[](auto a, auto b) { return a*b; }`;
+   - or use `multiplies` from <functional>, which does exactly that.

And so it is with many things from <functional>.

I categorize the things offered in <functional> (more or less arbitrarily) into the following areas:

+   - **Function factories**
+     function is the central point for everything callable in C++. bind creates a new function object with one less argument from a function object and an argument. mem_fn creates a function object from a method. There are several auxiliary constructs in this context.
+   
+   - **Concrete function objects**
+     For arithmetic (like `multiplies`), comparisons (like `equal_to`, `logical_and`, etc.), and bitwise (`bit_and`, etc.) operations, which you can use instead of a simple lambda.
+   
+   - **Specialized hash functions**
+     The hash function objects needed for the *unordered* containers are defined here for the built-in types. So, for example, you will find the template specialization `hash<int>` and all its relatives. That should be self-explanatory, so I will not go into further detail here.
```
using boost::core::demangled_name;
cout<<demangled_name(BOOST_CORE_TYPEID(i))<<'\n'; // Output: int
cout<<demangled_name(BOOST_CORE_TYPEID(f))<<'\n'; // Output: float
cout<<demangled_name(BOOST_CORE_TYPEID(double))<<'\n'; // Output: double
std::string
cout<<demangled_name(BOOST_CORE_TYPEID(string{}).begin()))<<'\n'; // Output: gnu cxx::normal_iterator<char*, std::string*>
cout<<demangled_name(BOOST_CORE_TYPEID(name))<<'\n'; // Output: std::map<int, std::string, std::less<int>>
std::allocator<std::pair<int, const, std::string>>
cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\n'; // Output: int
}
```

**Listing 28.42** Boost’s “demangled_name” is extremely useful for outputting type names.
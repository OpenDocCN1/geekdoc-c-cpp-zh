```
29    for (auto v: res) std::cout << v << " ";
30
31    std::cout << "\n\n";
32
33    std::vector<std::string> myStrings{"Only", "for", "testing", "purposes"};
34    auto res2 = map([](const std::string& s){ return std::make_pair(s.size(), s); },
35                    myStrings);
36
37    for (auto p: res2) std::cout << "(" << p.first << ", " << p.second << ") ";
38
39    std::cout << "\n\n";
40
41
42 }
```

Line 15 in the definition of the map function is quite interesting. The expression decltype(func( std::declval<value_type>())) deduces the return_type. The return_type is the type to which all input sequence elements are transformed if the function func is applied to them. std::declval<value_type>() returns an rvalue reference that decltype can use to deduce the type. That means the call map([](int i){ return i * i; }, myInts) (line 28) maps each element of myInts to its square, and the call map([](const std::string& s){ return std::make_pair(s.size(), s); }, myStrings) maps each string of myStrings to a pair. The first element of each pair is the length of the string.

```
1 4 9 16 25 36 49 64 81 100

(4, Only) (3, for) (7, testing) (8, purposes)
```

The map function applied

# 7.1.3 List Comprehension

The program listComprehensionRanges.cpp has a simplified version of Python's list-comprehension algorithm.

map applies a callable to each element of the input sequence.
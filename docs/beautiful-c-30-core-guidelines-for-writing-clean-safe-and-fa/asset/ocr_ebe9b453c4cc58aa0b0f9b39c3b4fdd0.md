```
std::unordered_map<std::string, int> dictionary;
auto [it, flag] = dictionary.insert({"one", 1});
    // it points to the element
    // flag signals whether the insertion was successful
```
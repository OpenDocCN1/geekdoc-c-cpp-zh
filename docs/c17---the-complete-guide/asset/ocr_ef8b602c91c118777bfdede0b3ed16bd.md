As another example, consider inserting a new element into a map or unordered map. You can check whether this was successful as follows:

```
std::map<std::string, int> coll;
...
if (auto [pos,ok] = coll.insert({"new",42}); !ok) {
    // if insert failed, handle error using iterator pos:
    const auto& [key,val] = *pos;
    std::cout << "already there: " << key << '\n';
}
```

Here, we also use structured bindings to give both the return value and the element at the return position pos useful names instead of just first and second. Before C++17, the corresponding check had to be formulated as follows:

```
auto ret = coll.insert({"new",42});
if (!ret.second){
    // if insert failed, handle error using iterator ret.first
    const auto& elem = *(ret.first);
    std::cout << "already there: " << elem.first << '\n';
}
```

Note that the extension also applies to the new compile-time if feature.

# 2.2 switch with Initialization

Using the switch statement with an initialization allows us to initialize an object/entity for the scope of the switch before formulating the condition to decide where to continue the control flow.

For example, we can initialize a filesystem path before we deal with its category:

```
namespace fs = std::filesystem;
...
switch (fs::path p{name}; status(p).type()) {
    case fs::file_type::not_found:
        std::cout << p << " not found\n";
        break;
    case fs::file_type::directory:
        std::cout << p << ":\n";
        for (const auto& e : std::filesystem::directory_iterator{p}) {
            std::cout << "- " << e.path() << '\n';
        }
        break;
    default:
        std::cout << p << " exists\n";
        break;
}
```

Here, the initialized path p can be used throughout the whole switch statement.
```
```cpp
}
void process(std::string&) {
    std::cout << "process(std::string&)\n";
}
void process(std::string&&) {
    std::cout << "process(std::string&&)\n";
}

const std::string& computeConstLRef(const std::string& str) {
    return str;
}
std::string& computeLRef(std::string& str) {
    return str;
}
std::string&& computeRRef(std::string&& str) {
    return std::move(str);
}
std::string computeValue(const std::string& str) {
    return str;
}

int main()
{
    process(computeConstLRef("tmp"));          // calls process(const std::string&)

    std::string str{"value"};
    process(computeLRef(str));                 // calls process(std::string&)

    process(computeRRef("tmp"));              // calls process(std::string&&)
    process(computeRRef(std::move(str)));      // calls process(std::string&&)

    process(computeValue("tmp"));             // calls process(std::string&&)
}
```
```

+   - If `compute()` returns a const lvalue reference:

```
```cpp
const std::string& computeConstLRef(const std::string& str) {
    return str;
}
```
```

the value category of the return value is an lvalue, which means that the return value is perfectly forwarded with the best match for a const lvalue reference:

```
```cpp
process(computeConstLRef("tmp"));        // calls process(const std::string&)
```
```

+   - If `compute()` returns a non-const lvalue reference:

```
```cpp
std::string& computeLRef(std::string& str) {
    return str;
}
```
```
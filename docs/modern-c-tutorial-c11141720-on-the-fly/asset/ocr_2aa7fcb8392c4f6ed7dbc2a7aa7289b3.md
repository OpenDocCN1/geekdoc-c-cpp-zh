# 9.2 noexcept and Its Operations

```
}
auto non_block_throw = []() {
    may_throw();
}
void no_throw() noexcept {
    return;
}
auto block_throw = []() noexcept {
    no_throw();
}
int main() {

```

```
std::cout << std::boolalpha
    << "may_throw() noexcept?" << noexcept(may_throw()) << std::endl
    << "no_throw() noexcept?" << noexcept(no_throw()) << std::endl
    << "lmay_throw() noexcept?" << noexcept(non_block_throw()) << std::endl
    << "Inno_throw() noexcept?" << noexcept(block_throw()) << std::endl;
    return 0;
}
```

noexcept can modify the function of blocking exceptions after modifying a function. If an exception is generated internally, we will not trigger. For instance:

```
try {
    may_throw();
} catch (...) {
    std::cout << "exception captured from may_throw()" << std::endl;
}
try {
    non_block_throw();
} catch (...) {
    std::cout << "exception captured from non_block_throw()" << std::endl;
}
try {
    block_throw();
} catch (...) {
    std::cout << "exception captured from block_throw()" << std::endl;
}
```

The final output is:
exception captured, from may_throw()
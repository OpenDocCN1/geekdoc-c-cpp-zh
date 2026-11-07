```
```cpp
auto_ptr = std::make_unique();

ptr->doSomething();

// No need to manually delete the pointer; memory is automatically
freed when ptr goes out of scope

}

int main() {

useResource();

return 0;

}
```
```

# Transfer of Ownership

std::unique_ptr cannot be copied, ensuring unique ownership of the resource. However, ownership can be transferred using making it possible to return a std::unique_ptr from a function or pass it to another function.
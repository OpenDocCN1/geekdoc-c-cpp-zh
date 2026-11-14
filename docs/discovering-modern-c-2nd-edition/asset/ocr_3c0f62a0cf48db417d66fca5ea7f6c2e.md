```
```cpp
std::list<int> l = {3, 5, 9, 7};
for (auto it= begin(l), e= end(l); it != e; ++it) {
    int i = *it;
    std::cout << i << std::endl;
}
```
```
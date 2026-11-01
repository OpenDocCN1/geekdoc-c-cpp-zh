```
```cpp
Wish* make_a_wish_better(int id, std::string owner) {
    Wish* wish = new Wish(wishes[id], owner);
    return wish;
}
```
```
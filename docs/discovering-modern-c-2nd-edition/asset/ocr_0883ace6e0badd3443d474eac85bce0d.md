```
```cpp
struct row_major {}; // Just for tagging
struct col_major {}; // Ditto
struct heap {};
struct stack {};
```
```

```
```cpp
template <typename T = double, typename Orientation = col_major,
typename Where = heap>
class vector;
```
```
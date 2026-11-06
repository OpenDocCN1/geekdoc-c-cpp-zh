*Accidental copy?*

```
```cpp
std::map<std::string, int> get_map();

using element_type = std::pair<std::string, int>;

for (const element_type & : get_map())
{
}
```
```

# Exercise: Enable ranged-loop related warnings

Make sure `-Wrange-loop-construct` is enabled in your code, which is automatically included with `-Wall`.
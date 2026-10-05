interprets string literals with the ""s suffix as std::string.
So you can write the following:

```
std::string s = max2("Ernie"s, "Bert"s);
```

However, you must have included operator""s beforehand—for example, with using namespace
std::literals.
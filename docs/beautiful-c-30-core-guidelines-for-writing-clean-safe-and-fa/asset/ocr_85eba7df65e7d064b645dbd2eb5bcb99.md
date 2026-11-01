```
struct s {
    int a;
    float b;
};

s make_s();

auto [sa, sb] = make_s();  // sa is an int
                          // sb is a float
```
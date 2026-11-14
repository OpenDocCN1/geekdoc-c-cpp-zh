```
int inc= 3;
constexpr auto dalz= transform(a,
        [inc](int i){return i+inc;}); // Error
```
```
~~~cpp
};

template<>

struct Factorial<0> { // Base case specialization

static constexpr unsigned value = 1;

};

int main() {

constexpr unsigned result = Factorial<5>::value; // Computed at
compile time

static_assert(result == 120, "Factorial<5> should be 120");

return 0;

};
~~~
```

The above sample program showcases a simple TMP application where a factorial is calculated at compile time. The Factorial template
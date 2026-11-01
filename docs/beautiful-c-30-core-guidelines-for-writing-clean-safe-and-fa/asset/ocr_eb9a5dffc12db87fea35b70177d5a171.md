```
```cpp
class my_special_type {
public:
    my_special_type(int, int);
    int magical_invocation(float);
...;
};

int f1(int a, int b, float c) {
    my_special_type m{a, b};
    if (a > b) return a;
    prepare_for_invocation();
    return m.magical_invocation(c);
}
```
```
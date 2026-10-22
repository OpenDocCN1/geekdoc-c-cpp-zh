```
template<typename T> void f(T);
template<typename T> void f(T, T);

int main() {
    auto x = f<int*>;     // ERROR: there are two possible f<int*> here
}
```
```
```cpp
constexpr struct A {};
```
```

+   3. Yes

```
```cpp
constexpr A a;
constexpr int i = 10;
```
```

+   4. Yes

```
```cpp
constexpr void func();
struct A
{
    constexpr void g();
};
```
```

+   5. Yes

```
```cpp
constexpr void func() {}
```
```

+   6. No

The following is an error because constexpr is applied to the integer parameter i of the function *func*

```
```cpp
void func(constexpr int i) {}
```
```

+   7. Yes

+   8. Yes

+   9. Yes
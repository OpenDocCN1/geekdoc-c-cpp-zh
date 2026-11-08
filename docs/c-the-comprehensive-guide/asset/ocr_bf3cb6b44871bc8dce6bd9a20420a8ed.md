`add(3.25f, 1.5f)`

Now, `3.25f` and `1.5f` are *float* literals; if I had written `3.25` and `1.5`, they would have been *double* literals. However, it is clearly better for the compiler to choose the `add(double, double)` variant instead of `add(int, int)`, as nothing is lost when converting from float to double, unlike a conversion from float to int.

If you try `print(1.25, 2.75)`, the compiler obviously cannot choose either `print(int)` or `print(double)`; the number of parameters simply doesn't match. So, it will call `print(int, double)` and convert `1.25` to an `int`. You will get the output `Values: 1, 2.75`.

If the compiler doesn't find a suitable overload with the conversions it can perform, it will complain to you with an error.

Sometimes, however, the compiler can find multiple overloads that all fit equally well or equally badly. In this case, the compiler will also respond with an error message, stating that the overload resolution was not unambiguous. If you call

```
```cpp
add(4, 2.85);           // ✗ Overloading unclear
```
```

the compiler cannot decide whether to use `add(int, int)` or `add(double, double)`. It will then tell you that this call cannot be resolved unambiguously.

To protect you from surprises, it should be mentioned that while parameter types contribute to overload resolution, return types do not. The compiler will complain about overloads that differ only in return type:

```
```cpp
// https://godbolt.org/z/58cTfVYhe
int two() { return 2; }       // ✗ once with int as return type...
double two() { return 2.0; }  // ✗ ...and once with double
int main() {
    int x = two();
    double y = two();
}
```
```

However, together with distinguishable parameter types, return types can also be different:

```
```cpp
// https://godbolt.org/z/evGqC1oqa
int twice(int a) { return a * 2; }
double twice(double a) { return a * 2.0; }
int main() {
    int x = twice(7);
    double y = twice(7.0);
}
```
```

This is widely used in the standard library. For example, the `begin()` and `end()` methods of containers sometimes return *iterator* and sometimes *const_iterator*, depending
that you can mark a parameter with const, which often occurs together with call-by-reference passing of parameters with &:

```
void print(const vector<int>& primes) {
    for(auto prime : primes) {
        cout << prime << " ";
    }
}
```

The parameter primes cannot be modified now. Any modification such as primes[7] = 4 or primes.push_back(12) will result in a compiler error. With classes and custom types, const MyClass& arg is often chosen as the passing method because the parameter does not need to be copied.

In the case of MyClass arg, it would be copied. You could safely modify arg within the function—because it is a copy, the changes do not affect the original object outside the caller—but copying a large object is costly.

If avoiding a copy is worthwhile, it is best to work with a const&. The & avoids the copy, and the const prevents accidental modifications to the external object.

What applies to classes is no different for built-in types. However, their copy costs are negligible, which is why you rarely see const int& const double&. The same rules apply as for classes. The compiler prevents changes to the values:

```
void nonsensicalParameter(const int& arga, const double& argb) {
    arga = 7; //Assignment to constant
}
```
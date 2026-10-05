```
using std::min; using std::max; using std::floating_point;

template<floating point> T heron(T a, T b, T c) {
    auto s = (a+b+c) / 2;
    return sqrt((s-a)*(s-b)*(s-c));
}
```

```
template<floating point> T kahan(T a, T b, T c) {
    auto x = max(min(a,b),c);
    auto y = max(min(a,b), min(max(a,c));
    auto z = min(min(a,b),c); return
    sqrt((x+y)*(x-y))*(z-y)*(x+(y-2)) / 4;
```

```
template<floating point> void triangle(T a, T b, T c) {
    std::cout << "heron: " << heron(a,b,c) << "\n";
    std::cout << "kahan: " << kahan(a,b,c) << "\n";
}
```

```
int main() {
    triangle(3.0f, 4.0f, 5.0f);
}
```

The output is then 6 for both procedures.
Funny things when you insert the side lengths (100000, 99999.99979, 0.00029) and let the computer calculate the area. I run both calculations for float and double output more digits:

```
// godbolt.org/z/863b1z4GY
int main() {
    std::cout << std::precision(15) << std::fixed;
    triangle(100.000.0, 99.999979f, 0.00029f);
    triangle(100.000.0, 99.999979, 0.00029);
}
```

The exact result would be 10. The example was carefully chosen so that float has in the calculation: while the classic Heron formula gives 0, the Kahan formula calculates 14.5. And 14.5 would look like a nice result if you didn't know that 10 is correct. Even though both methods give a better result with double—I told you that 10 should come out—such an example could also have been found for double. The actual outputs are as follows:

```
heron: 0.00000000000000
kahan: 14.50000000000000
heron: 9.999999000638329
kahan: 10.000000077021838
```
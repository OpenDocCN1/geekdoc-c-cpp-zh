```
Sizes: 4 4
2100000009 2.1e+009
2100000009 2100000000
```

A **float** and an **int** take up the same amount of space (4 bytes). A **float** is represented as a “**mantissa**” (typically a value between 0 and 1) and an exponent (**mantissa**⁄*10^{exponent}), so it cannot represent exactly the largest **int**. (If we tried to, where would we find space for the mantissa after we had taken the space needed for the exponent?) As it should, **f** represented **2100000009** as approximately correct as it could. However, that last **9** was too much for it to represent exactly — and that was of course why we chose that number.

On the other hand, when you assign a floating-point number to an integer, you get truncation; that is, the fractional part — the digits after the decimal point — is simply thrown away. For example:

```
float f = 2.8;
int x = f;
cout << x << ' ' << f << "\n";
```

The value of **x** will be **2**. It will not be **3** as you might imagine if you are used to “4/5 rounding rules.” C++ **float-to-int** conversions truncate rather than round.

When you calculate, you must be aware of possible overflow and truncation. C++ will not catch such problems for you. Consider:

```
void f(int i, double fpd)
{
    char c = i;         // yes: chars really are very small integers
    short s = i;        // beware: an int may not fit in a short int
    i = i+1;            // what if i was the largest int?
    long lg = i*i;      // beware: a long may not be any larger than an int
    float fps = fpd;    // beware: a large double may not fit in a float
    i = fpd;            // truncates: e.g., 5.7 -> 5
    fps = i;            // you can lose precision (for very large int values)
}

void g()
{
    char ch = 0;
    for (int i = 0; i<=500; ++i)
        cout << int(ch++) << '\t';
}
```
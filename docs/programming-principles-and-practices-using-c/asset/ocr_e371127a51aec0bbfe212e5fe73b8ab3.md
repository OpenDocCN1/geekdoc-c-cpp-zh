This will print **35.1384**, that is, `1.0*1*2.2*3.3*4.4` (**1.0** is the initial value). The binary operator supplied here, `multiplies<double>`, is a standard library function object that multiplies; `multiplies<double>` multiplies **doubles**, `multiplies<int>` multiplies **ints**, etc. There are other binary function objects: `plus` (it adds), `minus` (it subtracts), `divides`, and `modulus` (it takes the remainder). They are all defined in `<functional>` (§B.6.2).

Note that for products of floating-point numbers, the obvious initial value is **1.0**.

As in the `sort()` example (§21.4.2), we are often interested in data within class objects, rather than just plain built-in types. For example, we might want to calculate the total cost of items given the unit prices and number of units:

```
struct Record {
    double unit_price;
    int units;      // number of units sold
    // ...
};
```

We can let `accumulate`'s operator extract the `units` from a `Record` element as well as multiplying it to the accumulator value:

```
double price(double v, const Record& r)
{
    return v + r.unit_price * r.units;    // calculate price and accumulate
}

void f(const vector<Record>& vr)
{
    double total = accumulate(vr.begin(), vr.end(), 0.0, price);
    // ...
}
```

We were "lazy" and used a function, rather than a function object, to calculate the price – just to show that we could do that also. We tend to prefer function objects

+   - If they need to store a value between calls, or
- If they are so short that inlining can make a difference (at most a handful of primitive operations)

In this example, we might have chosen a function object for the second reason.
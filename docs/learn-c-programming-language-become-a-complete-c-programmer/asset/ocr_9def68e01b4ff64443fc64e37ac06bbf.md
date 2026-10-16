its scalar type. A scalar type is treated as a **valarray** of the right size with every element having the scalar’s value. For example:

```
```cpp
void f(valarray<double>& v, valarray<double>& v2, double d)
{
valarray<double> v3 = v*v2; // v3[i] = v[i]*v2[i] for all i
valarray<double> v4 = v*d;  // v4[i] = v[i]*d for all i
valarray<double> v5 = d*v2; // v5[i] = d*v2[i] for all i
valarray<double> v6 = cos(v); // v6[i] = cos(v[i]) for all i
}
```
```

These vector operations all apply their operations to each element of their operand(s) in the way indicated by the **\*** and **cos()** examples. Naturally, an operation can be used only if the corresponding operation is defined for the scalar type. Otherwise, the compiler will issue an error when trying to specialize the operator or function.

# Section 40.5.3 Operations 1171

Where the result is a **valarray**, its length is the same as its **valarray** operand. If the lengths of the two arrays are not the same, the result of a binary operator on two **valarrays** is undefined.

These **valarray** operations return new **valarrays** rather than modifying their operands. This can be expensive, but it doesn’t have to be when aggressive optimization techniques are applied.

For example, if **v** is a **valarray**, it can be scaled like this: **v *= 0.2**, and this: **v /= 1.3**. That is, applying a scalar to a vector means applying the scalar to each element of the vector. As usual, **\*=** is more concise than a combination of **\*** and **=** (§18.3.1) and easier to optimize.

Note that the non-assignment operations construct a new **valarray**. For example:

```
```cpp
double incr(double d) { return d+1; }

void f(valarray<double>& v) {
valarray<double> v2 = v.apply(incr); // produce incremented valarray
// ...
}
```
```

This does not change the value of **v**. Unfortunately, **apply()** does not accept a function object (§3.4.3, §11.4) as an argument.

The logical and cyclic shift functions, **shift()** and **cshift()**, return a new **valarray** with the elements suitably shifted and leave the original one unchanged. For example, the cyclic shift **v2=v.cshift(n)** produces a **valarray** so that **v2[i]==v[(i+n)%v.size()]**. The logical shift **v3=v.shift(n)** produces a **valarray** so that **v3[i]** is **v[i+n]** if i+n is a valid index for v. Otherwise, the result is the default element value. This implies that both **shift()** and **cshift()** shift left when given a positive argument and right when given a negative argument. For example:

```
```cpp
void f()
{
int alpha[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
valarray<int> v(alpha,8); // 1, 2, 3, 4, 5, 6, 7, 8
```
```
# Expressions 67

**Example 77** Assignment Assignment: Implicit and Automatic Explicit Conversion
The assignment d = 12 performs an implicit conversion from int to double. The assignment b=252+1 performs an automatic (explicit but invisible) conversion from int to byte because 252+1 is a compile constant within the range 0...255 of byte, but the assignment b=255+5 is illegal not within that range. The assignment b+=2 is illegal the right-hand side b+2 has type int, but b=(b+2) is illegal the right-hand side has type byte. The assignment b+=2 is illegal because it is equivalent to the preceding one, and 2 is within the range of byte, but b=257 is illegal because 257

```
double d;
d = 12;
// implicit conversion from int to double
byte b;
b = 252 + 1;
// Legal: 252 + 1 is a compile-time constant
// Illegal: 255 + 5 is too large
b += b + 2;
// Legal: b+2 has type int
b=(byte)(b + 2);
// Legal: right-hand side has type byte
b += 2;
// Legal: equivalent to b = (byte)(b + 2)
// Illegal: b = 257 is not in range of byte
```

**Example 78** Compound Assignment Operators
Compute the product of all array xs.

```
static double Multiply(double[] xs) {
double prod = 1.0;
for (int i = 0; i<xs.Length; i++)
prod *= xs[i]; // Equivalent to prod = prod * xs[i]
return prod;
}
```

**Example 79** The Conditional Expression
Return the absolute value of Absolute(double x) always non-negative.

```
static double Absolute(double x) {
return (x >= 0 ? x : -x);
}
```

**Example 80** Nested Conditional Expressions
Nested conditional expressions are useful for making three-way comparisons, as in a Compare method (section 27.3). Note that the conditional operator (?) associates to the right. Implementing Compare by computing the value v1-v2 does not work because the subtraction overflow.

```
class LongComparer : IComparer<long> {
public int Compare(long v1, long v2) {
return v1 < v2 ? -1 : v1 > v2 ? 1 : 0;
}
}
```
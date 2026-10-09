```
3 public readonly struct Rational {
    4     private readonly ulong num, den;
    5     private readonly bool neg;
    6
        public Rational()
            : this(0, 1) { }

        public Rational(ulong numer, ulong denom)
            : this(numer, denom, false) { }

        public Rational(ulong numer, ulong denom, bool negat) {
            if (denom == 0) {
                throw new ArgumentException("Zero denominator");
            }

            if (numer == 0) {
                (num, den, neg) = (0, 1, false);
            } else {
                var cf = GCD(numer, denom);
                (num, den, neg) = (numer / cf, denom / cf, negat);
            }
        }
}
```

“Overloading” unary operators + and -:

```
26  public static Rational operator +(Rational a) => a;
27  public static Rational operator -(Rational a) =>
28      new(a.num, a.den, !a.neg);
```

“Overloading” binary operators +, -, *, and /:
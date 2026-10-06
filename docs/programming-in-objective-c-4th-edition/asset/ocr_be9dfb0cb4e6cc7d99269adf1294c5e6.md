```
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) subtract: (Fraction *) f
{
  // To sub two fractions:
  // a/b - c/d = ((a*d) - (b*c)) / (b * d)

  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator *
f.denominator -
    denominator * f.numerator;
    result.denominator = denominator *
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) multiply: (Fraction *) f
{
  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator * f.numerator
  result.denominator = denominator *
f.denominator;
  [result reduce];

  return result;
}

-(Fraction *) divide: (Fraction *) f
```
```
else
    return NAN;
}

-(NSString *) convertToString
{
    if (numerator == denominator)
        if (numerator == 0)
            return "@0";
        else
            return "@1";
    else if (denominator == 1)
        return [NSString stringWithFormat:@%i", numerator];
    else
        return [NSString stringWithFormat:@%i/%i", numerator, denominator];
}
```

// add a Fraction to the receiver

```
-(Fraction *) add: (Fraction *) f
{
    // To add two fractions:
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)
```

// result will store the result of the addition
Fraction *result = [[Fraction alloc] init];

```
result.numerator = numerator *
f.denominator +
denominator * f.numerator;
result.denominator = denominator *
```
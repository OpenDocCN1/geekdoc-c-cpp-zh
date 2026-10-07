```
numerator = n;
dominator = d;
}
```

```
// add a Fraction to the receiver

-(void) add: (Fraction*) f
{
// To add two fractions:
// a/b+ c/d = ((a*d) + (b*c)) / (b * d)

numerator = numerator * f.denominator + denominator * f.numerator;
dominator = denominator * f.denominator;
}
```

```
- (void) reduce
{
int u = numerator;
int v = denominator;\int temp;

while (v != 0) {
temp = u % v;
u = v;
temp = temp;
}

numerator /= u;
dominator /= u;
}
```

```
@end
```

# Program 7.4 Test FractionTest.m

```
#import <Foundation.h> 

int main (int argc, char *argv[])
{
NSAutleasePool *pool = [[NSAutleasePool alloc] init];

Fraction *aFraction = [[Fraction alloc] init];
Fraction *bFraction = [[Fraction alloc] init];

[aFraction setTO:1 over: 4]; // set 1st fraction to 1/4
[bFraction setTO:1 over: 2]; // set 2nd fraction to 1/2

[aFraction print];
NSLog("%@*");
[bFraction print];
NSLog("%@*", bFraction);

[aFraction add:bFraction];

// reduce the result of the addition and print the result

return 0;
}
```
```
denominator = denominator * f.denominator;
}

-(void) reduce
{
int u = numerator;
int v = denominator;
int temp;

while (v != 0) {
    temp = u % v;
    u = v;
    v = temp;
}

numerator /= u;
dominator /= u;
}
```

# Program 7.4. Test File main.m

```
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];

        [aFraction setTo: 1 over: 4]; // set
```
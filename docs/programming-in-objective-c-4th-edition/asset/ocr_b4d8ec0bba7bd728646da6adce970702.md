these only if you're writing applications that allocate a lot of memory and you want to optimize the allocation by grouping them into these zones. You can take the value passed to copyWithZone: and hand it off to a memory allocation method allocWithZone:. This method allocates memory in a specified zone.

After allocating a new Fraction object, you copy the receiver's numerator and denominator variables into it. The copyWithZone: method is supposed to return the new copy of the object, which you do in your method.

Program 18.3 tests your new method.

# Program 18.3

```
// Copying fractions

#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *f1 = [[Fraction alloc] init];
        Fraction *f2;

        [f1 setTo: 2 over: 5];
        f2 = [f1 copy];

        [f2 setTo: 1 over: 3];

        [f1 print];
        [f2 print];
    }
    return 0;
}
```
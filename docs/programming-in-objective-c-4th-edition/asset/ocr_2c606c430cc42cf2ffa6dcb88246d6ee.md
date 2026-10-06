Based on discussion, your initialization method initWith:over: for your Fraction class might look like this:

```
-(Fraction *) initWith: (int) n over: (int) d {
  self = [super init];

  if (self)
    [selfTo: n over: d];

  return self;
}
```

Following the initialization of super (and its success, as indicated by the return of a nonzero value) use the setTo:over: method to set the numerator and denominator of your Fraction. As with other initialization methods, you are expected to return the initialized object, which you do here.

Program 10.1 tests your new initWith:over: initialization method.

# Program 10.1

```
#import "Fraction.h"

int main (int argc, char * argv[]) {
  @autoreleasepool {
    Fraction *a, *b;

    a = [[Fraction alloc] initWith: 1 over:
    b = [[Fraction alloc] initWith: 3 over:
```
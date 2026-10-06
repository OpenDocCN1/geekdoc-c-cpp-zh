```
- (int) numerator;
-(int) denominator;
```

And here are the definitions:

```
- (int) numerator
{
    return numerator;
}

-(int) denominator
{
    return denominator;
}
```

Note that the names of the methods and the instance variables they access are the same. There's no problem doing this (although it might seem a little odd at first); in fact, it is common practice. Program 3.4 tests your two new methods.

# Program 3.4

```
// Program to access instance variables - cont'd

#import <Foundation/Foundation.h>

// @interface section ----

@interface Fraction: NSObject

-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
-(int) numerator;
```
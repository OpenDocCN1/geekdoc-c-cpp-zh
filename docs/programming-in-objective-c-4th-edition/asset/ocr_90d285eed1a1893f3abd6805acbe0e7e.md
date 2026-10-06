```
(double) b;
-(Complex *) add: (Complex *) f;
@end
```

You should have completed the implementation section for this class in exercises 5 and 6 from Chapter 7 "More on Classes." We added an additional setReal:andImaginary: method to enable you to set both the real and imaginary parts of your number with a single message and also synthesized accessor methods. This is shown in the following.

# Program 9.1. Implementation File Complex.m

```
// Implementation file for Complex class

#import "Complex.h"

@implementation Complex

@synthesize real, imaginary;

-(void) print
{
    NSLog("%g + %gi", real, imaginary);
}

-(void) setReal: (double) a andImaginary:
(double) b
{
    real = a;
imaginary = b;
}

-(Complex *) add: (Complex *) f
```
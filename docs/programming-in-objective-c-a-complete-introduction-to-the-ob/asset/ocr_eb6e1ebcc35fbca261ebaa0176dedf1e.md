This builds an executable file called FractionTest. Here's the output after running
the program:

# Program 7.1 FractionTest Output

```
The value of myFraction is:
1/3
```

# Synthesized Accessor Methods

As of Objective-C 2.0, you can have your setter and getter methods (collectively known
as accessor methods) automatically generated for you. We Haven't shown you how to do this
up to this point because it was important for you to learn how to write these methods on
your. However, it's a nice convenience provided in the language, so it's time for you
to learn how to take advantage of this feature

The first step is to use the @property directive in your interface section to identify
your properties. These properties are often your instance variables. In the case of
Fraction class, the two instance variables numerator and denominator fall into this
category. Following is the new interface section with the new @property directive

```
@interface Fraction : NSObject
{
  int numerator;
  int denominator;
}
```

```
@property int numerator, denominator;
```

```
- (void) print;
- (double) convertNum;
@end
```

Note that we longer include the definitions for our getter and setter methods:
numerator, denominator, setNumerator:, and setDenominator:. We're going to have
tObjective-C compiler automatically generate or synthesize these for you. How is this
done? Simply by using the @synthesize directive in the implementation section, as
shown.

```
#import "Fraction.h"
```

```
@implementation Fraction
```

```
@synthesize numerator, denominator;
```
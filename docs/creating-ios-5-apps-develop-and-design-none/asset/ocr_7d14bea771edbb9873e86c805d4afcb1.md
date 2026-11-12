Switch to the WeightEntry.m implementation file and add the lines to synthesize these properties inside the @implementation block:

```
```
@implementation WeightEntry

@synthesize weightInLbs = _weightInLbs;
@synthesize date = _date;
```
```

Weights, currency, date formats—all these simple-seeming concepts tend to get overly complicated whenever you want to support multiple countries or cultures. For the purpose of this project, we will want to support both pounds and kilograms. To keep the code as streamlined as possible, we will use pounds as the canonical weight internally. We will then add helper functions to convert from pounds to kilograms and from kilograms to pounds as needed.

Let’s start by defining an enumeration of our weight units. Switch back to the header file and add the following code right before the @interface declaration:

```
```
#import <Foundation/Foundation.h>

typedef enum {
    LBS,
    KG
} WeightUnit;

@interface WeightEntry : NSObject {
```
```

Now, declare our designated initializer right after the @property declarations:

```
```
@property (nonatomic, assign, readonly) CGFloat weightInLbs;
@property (nonatomic, strong, readonly) NSDate* date;
- (id) initWithWeight:(CGFloat)weight
           usingUnits:(WeightUnit)unit
              forDate:(NSDate*)date;
@end
```
```

This will take a weight, the unit type for our weight, and a date and initialize our WeightEntry object. Switch back to the implementation file. We need to implement both our designated initializer and our superclass’s designated initializer.
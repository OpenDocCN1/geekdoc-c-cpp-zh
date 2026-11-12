# ADDING HELPER METHODS

You may have noticed that there is a problem with our designated initializer. The class method [WeightEntry convertKgToLbs:weight] does not actually exist. Let's fix that. Switch back to the header file and declare the following two class methods:

```
@interface WeightEntry : NSObject {
}
@property (nonatomic, assign, readonly) CGFloat weightInLbs;
@property (nonatomic, strong, readonly) NSDate* date;
+ (CGFloat)convertLbsToKg:(CGFloat)lbs;
+ (CGFloat)convertKgToLbs:(CGFloat)kg;
- (id) initWithWeight:(CGFloat)weight
            usingUnits:(WeightUnit)unit
                forDate:(NSDate*)date;
@end
```

Go back to the implementation file. Just before the @implementation block, add the following static variables. LBS_PER_KG will be used to convert from pounds to kilograms and back, while formatter will be used to provide a standard format for all weight values, using the proper number formatting for your current locale. Yes, number formatting changes from country to country as well.

```
static const CGFloat LBS_PER_KG = 2.20462262f;
static NSNumberFormatter* formatter;
```

Now, in the @implementation block, add our class methods:

```
+ (CGFloat)convertLbsToKg:(CGFloat)lbs {
    return lbs / LBS_PER_KG;
}
+ (CGFloat)convertKgToLbs:(CGFloat)kg {
    return kg * LBS_PER_KG;
}
```
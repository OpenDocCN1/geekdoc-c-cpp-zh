# super

What if you decided that all employees get an automatic 10% off their BMI as calculated in the Person’s implementation? You could, of course, retype the code in the Employee implementation, but it would be so much more convenient to call Person’s version of bodyMassIndex and multiply the result by 0.9 before returning it. To do this, you use the super directive. Try it in Employee.m:

```
```
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

- (float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}

@end
```
```

Build and run the program.

To be precise, the super directive says “Run this method, but start the search for its implementation at my superclass.”

# Challenge

This challenge builds on the challenge from the previous chapter.

Create a subclass of StockHolding called ForeignStockHolding. Give ForeignStockHolding an additional instance variable: conversionRate, which will be a float. (The conversion rate is what you need to multiply the local price by to get a price in US dollars. Assume the purchasePrice and currentPrice are in the local currency.) Override costInDollars and valueInDollars to do the right thing.

In main(), add a few instances of ForeignStockHolding to your array.
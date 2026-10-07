
```objc
[self processOp:'+'];

-(IBAction) clickMinus
{
    [self processOp: '-'];
}

-(IBAction) clickMultiply
{
    [self processOp: '*'];
}

-(IBAction) clickDivide
{
    [self processOp: '/'];
}

// Misc. Keys

-(IBAction) clickEquals
{
    if (firstOperand) {
        [self fracPart];
        [myCalculator performOperation:op];

        [displayString appendString:@"@"];
        [displayString appendString:[myCalculator.accumulator convertToString]];
        display.text = displayString;

        currentNumber = 0;
        isNumber = YES;
        firstOperand = YES;
        [displayString setString:@"@"];
    }
}

-(IBAction) clickClear
{
    isNumber = YES;
    firstOperand = YES;
    currentNumber = 0;
    [myCalculator clear];

    [displayString setString:@"@"];
    display.text = displayString;
}

end
```

The calculator window still contains just one label in the previous application, and we still call `display`. As the user enters a number digit-by-digit, we need to build the number along the way. The variable `currentNumber` holds the number-in-progress, while the BOOL variables `firstOperand` and `isNumerator` keep track of whether this is the first second operand entered and whether the user is currently keying in the numerator or the denominator of operand.

When a digit button is pressed on the calculator, we set it up so that some identifying information will be passed to the `clickDigit:` method to identify which digit button was pressed. This is done by setting the button's Tag attribute in the Inspector to a unique value for each digit button. In this case, we want to set the tag to the corresponding number. So the tag for the button labeled 0 is set to 0, for the button labeled 1 to 1, and the sender agent to the `clickDigit:` method is the actual UIButton that was pressed in the iPhone's window. By accessing the tag property of this object, we retrieve the value of the button's tag. This is done in the `clickDigit:` method as shown:

```objc
-(IBAction)clickDigit:(UIButton *)sender
{
    int digit = sender.tag;
    [self processDigit:digit];
}
```

There are a lot more buttons in Program 21.2 than in the first application. Most of the view controller's implementation file revolves around building the fractions and displaying them. As a digit button 0–9 gets pressed, the action method `clickDigit` gets executed. The method calls the `processDigit:` method to track the digit onto the end of the number that's being built in the variable `currentNumber`. That method also adds the digit to the current display string that's kept in the variable `displayString`, and updates the current display.

When the key is pressed, the `clickEquals` method gets invoked to perform the operation. The calculator performs the operation between the two fractions, storing the result in its accumulator. This accumulator is fetched inside the `clickEquals` method, and the result is added to the display.

## The Fraction Class

The Fraction class remains largely unchanged from earlier examples in this text. There is a new `convertToString` method that was added to convert a fraction to its equivalent string representation. Program 21.2 shows the Fraction interface followed immediately by the corresponding implementation file.

## Program 21.2 Fraction.h Interface File

```objc
#import <UIKit/UIKit.h>

@interface Fraction : NSObject {
    int numerator;
    int denominator;
}
```

```objc
@property int numerator, denominator;

-(void)setTo:(int)n over:(int)d;
-(add:(Fraction*)f;
-(subtract:(Fraction*)f;
-(multiply:(Fraction*)f;
-(divide:(Fraction*)f;
-(void)reduce;
-(double)convertToNum;
-(NSString*)convertToString;

@end
```

## Program 21.2 Fraction.m Implementation File

```objc
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

-(void)setTo:(int)n over:(int)d {
    numerator = n;
    denominator = d;
}

-(void)print {
    NSLog("%%i/%%i", numerator, denominator);
}

-(double)convertToNum {
    if (denominator != 0)
        return (double)numerator / denominator;
    else
        return NAN;
}

-(NSString*)convertToString {
    if (numerator == 0 && denominator == 0) {
        return "0";
    } else if (denominator == 0) {
        return "1";
    } else if (denominator == 1) {
        return [NSString stringWithFormat:@"%i", numerator];
    } else {
        return [NSString stringWithFormat:@"%i/%i", numerator, denominator];
    }
}

// add a Fraction to the receiver
-(Fraction *)add:(Fraction *)f {
  // To add two fractions:
  // a/b + c/d ((a*d) + (b*c)) / (b*d)

  // result will store the result of the addition
  Fraction *result = [[Fraction alloc] init autorelease];
  // ... implementation ...
  return result;
}

@end
```

## Chapter 21 Writing iOS Applications

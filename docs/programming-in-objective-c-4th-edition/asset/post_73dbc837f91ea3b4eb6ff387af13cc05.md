
```objc
case '//':
opStr = @" \div ";
break;
}

[self storeFracPart];
firstOperand = NO;
isNumerator = YES;

[displayString appendString: opStr];
display.text = displayString;
}

-(void) storeFracPart
{
  if (firstOperand) {
    if (isNumerator) {
      myCalculator.operand1.numerator = currentNumber;
      myCalculator.operand1.denominator = 1; // e.g. 3 * 4/5 =
    } else
      myCalculator.operand1.denominator = currentNumber;
    }
  } else if (isNumerator) {
    myCalculator.operand2.numerator = currentNumber;
    myCalculator.operand2.denominator = 1; // e.g. 3/2 * 4 =
  } else {
    myCalculator.operand2.denominator = currentNumber;
    firstOperand = YES;
  }
}
```

```objc
}
CurrentNumber = 0;
}
-(IBAction) clickOver
{
    [self storeFracPart];
    isNumerator = NO;
    [displayString appendString: @"/"];
    display.text = displayString;
}
// Arithmetic Operation keys
-(IBAction) clickPlus
{
    [self processOp: '+'];
}
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
```

```objc
-(IBAction) clickEquals
{
    if ( firstOperand == NO ) {
        [self storeFracPart];
        [myCalculator performOperation: op];

        [displayString appendString:@" = "];
        [displayString appendString:[myCalculator.accumulator convertToString]];
        display.text = displayString;

        currentNumber = 0;
        isNumerator = YES;
        firstOperand = YES;
        [displayString setString:@""];
    }
}
-(IBAction) clickClear
{
    isNumerator = YES;
    firstOperand = YES;
    currentNumber = 0;
    [myCalculator clear];

    [displayString setString:@""];
    display.text = displayString;
}

@end
```

The calculator’s window still contains just one label as in the previous application, and we still call it display. As the user enters

There are a lot more buttons in Program 21.2 than in the first application. Most of the complexity in the view controller's implementation file revolves around building the fractions and displaying them. As noted, as a digit button 0–9 gets pressed, the action method clickDigit: gets executed. That method calls the processDigit: to tack the digit onto the end of the number that's being built in the variable currentNumber. That method also adds the digit to the current display string that's kept in the variable displayString, and updates the display:

```objc
-(void) processDigit: (int) digit
{
    currentNumber = currentNumber * 10 + digit;

    [displayString appendString:[NSString stringWithFormat: @"%i", digit]];
    display.text = displayString;
}
```

When the = key is pressed, the clickEquals method gets invoked to perform the operation. The calculator performs the operation between the two fractions, storing the result in its accumulator. The accumulator is fetched inside the clickEquals method, and the result is added to the display.

# The Fraction Class

The Fraction class remains largely unchanged from earlier examples in this text. There is a new convertToString method that was added to convert a fraction to its equivalent string representation. Program 21.2 shows the Fraction interface file followed immediately by the corresponding implementation file.

# Program 21.2. Fraction.h Interface File

```objc
#import <UIKit/UIKit.h>

@interface Fraction : NSObject

@property int numerator, denominator;

-(void) print();

- (void)
setTo: (int) n over: (int) d;
- (Fraction *) add: (Fraction *) f;
- (Fraction *) subtract: (Fraction *) f;
- (Fraction *) multiply: (Fraction *) f;
- (Fraction *) divide: (Fraction *) f;
- (void) reduce;
- (double) convertToNum;
- (NSString *) toString;

@end
```

# Program 21.2. Fraction.m Implementation File

```objc
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

```objc
- (void) setTo: (int) n over: (int) d
{
    numerator = n;
    denominator = d;
}
```

```objc
- (void) print
{
    NSLog ("%%i/%i", numerator, denominator);
}
```

```objc
- (double) convertToNum
{
    if (denominator != 0)
    return (double) numerator / denominator;
}
else
    return NAN;
}

-(NSString *) convertToString
{
    if (numerator == denominator)
        if (numerator == 0)
            return "@0";
        else
            return "@1";
    else if (denominator == 1)
        return [NSString stringWithFormat:@"%i", numerator];
    else
        return [NSString stringWithFormat:@"%i/%i", numerator, denominator];
}
```

// add a Fraction to the receiver

```objc
-(Fraction *) add: (Fraction *) f
{
    // To add two fractions:
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)

// result will store the result of the addition
Fraction *result = [[Fraction alloc] init];

```objc
result.numerator = numerator *
f.denominator +
denominator * f.numerator;
result.denominator = denominator *
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) subtract: (Fraction *) f
{
  // To sub two fractions:
  // a/b - c/d = ((a*d) - (b*c)) / (b * d)

  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator *
f.denominator -
    denominator * f.numerator;
    result.denominator = denominator *
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) multiply: (Fraction *) f
{
  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator * f.numerator
  result.denominator = denominator *
f.denominator;
  [result reduce];

  return result;
}

-(Fraction *) divide: (Fraction *) f
{
  Fraction *result = [[Fraction alloc] init];
  result.numerator = numerator *
  f.denominator
  result.denominator = denominator *
  f.denominator;
  [result reduce];
  return result;
}
- (void) reduce
{
  int u = numerator;
  int v = denominator;
  int temp;
  if (u == 0)
    return;
  else if (u < 0)
    u = -u;
  while (v != 0) {
    temp = u % v;
    u = v;
    v = temp;
  }
  numerator /= u;
  denominator /= u;
}
@end
```

The calculator’s window still contains just one label as in the previous application, and we still call it display. As the user enters 

There are a lot more buttons in Program 21.2 than in the first application. Most of the complexity in the view controller's implementation file revolves around building the fractions and displaying them. As noted, as a digit button 0–9 gets pressed, the action method clickDigit: gets executed. That method calls the processDigit: to tack the digit onto the end of the number that's being built in the variable currentNumber. That method also adds the digit to the current display string that's kept in the variable displayString, and updates the display:

When the = key is pressed, the clickEquals method gets invoked to perform the operation. The calculator performs the operation between the two fractions, storing the result in its accumulator. The accumulator is fetched inside the clickEquals method, and the result is added to the display.

# The Fraction Class

The Fraction class remains largely unchanged from earlier examples in this text. There is a new convertToString method that was added to convert a fraction to its equivalent string representation. Program 21.2 shows the Fraction interface file followed immediately by the corresponding implementation file.

# Program 21.2. Fraction.h Interface File

```objc
#import <UIKit/UIKit.h>

@interface Fraction : NSObject

@property int numerator, denominator;

-(void) print();

- (void)
setTo: (int) n over: (int) d;
- (Fraction *) add: (Fraction *) f;
- (Fraction *) subtract: (Fraction *) f;
- (Fraction *) multiply: (Fraction *) f;
- (Fraction *) divide: (Fraction *) f;
- (void) reduce;
- (double) convertToNum;
- (NSString *) toString;

@end
```

# Program 21.2. Fraction.m Implementation File

```objc
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

```objc
- (void) setTo: (int) n over: (int) d
{
    numerator = n;
    denominator = d;
}
```

```objc
- (void) print
{
    NSLog ("%%i/%i", numerator, denominator);
}
```

```objc
- (double) convertToNum
{
    if (denominator != 0)
    return (double) numerator / denominator;
}
else
    return NAN;
}

-(NSString *) convertToString
{
    if (numerator == denominator)
        if (numerator == 0)
            return "@0";
        else
            return "@1";
    else if (denominator == 1)
        return [NSString stringWithFormat:@"%i", numerator];
    else
        return [NSString stringWithFormat:@"%i/%i", numerator, denominator];
}
```

// add a Fraction to the receiver

```objc
-(Fraction *) add: (Fraction *) f
{
    // To add two fractions:
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)

// result will store the result of the addition
Fraction *result = [[Fraction alloc] init];

```objc
result.numerator = numerator *
f.denominator +
denominator * f.numerator;
result.denominator = denominator *
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) subtract: (Fraction *) f
{
  // To sub two fractions:
  // a/b - c/d = ((a*d) - (b*c)) / (b * d)

  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator *
f.denominator -
    denominator * f.numerator;
    result.denominator = denominator *
f.denominator;

  [result reduce];
  return result;
}

-(Fraction *) multiply: (Fraction *) f
{
  Fraction *result = [[Fraction alloc] init];

  result.numerator = numerator * f.numerator
  result.denominator = denominator *
f.denominator;
  [result reduce];

  return result;
}

-(Fraction *) divide: (Fraction *) f
{
  Fraction *result = [[Fraction alloc] init];
  result.numerator = numerator *
  f.denominator
  result.denominator = denominator *
  f.denominator;
  [result reduce];
  return result;
}
- (void) reduce
{
  int u = numerator;
  int v = denominator;
  int temp;
  if (u == 0)
    return;
  else if (u < 0)
    u = -u;
  while (v != 0) {
    temp = u % v;
    u = v;
    v = temp;
  }
  numerator /= u;
  denominator /= u;
}
@end
```

# A Calculator Class That Deals with Fractions

Next, it's time to take a look at the Calculator class. The concept is similar to the class of the same name we developed earlier in this book. However, in this case, our calculator must know how to deal with fractions. Here are our new Calculator interface and implementation files.

# Program 21.2. Calculator.h Interface File

```objc
#import <UIKit/UIKit.h>
#import "Fraction.h"

@interface Calculator : NSObject

@property (strong, nonatomic) Fraction *operand1,*operand2, *accumulator;

-(Fraction *) performOperation:(char) op;
-(void) clear;

}
```

# Program 21.2. Calculator.m Implementation File

```objc
#import "Calculator.h"

@implementation Calculator

@synthesize operand1, operand2, accumulator;

-(id) init
{
    self = [super init];

    if (self) {
        operand1 = [[Fraction alloc] init];
        operand2 = [[Fraction alloc] init];
        accumulator = [[Fraction alloc] init];
    }
    return self;
}

-(void) clear
{
    accumulator.numerator = 0;
    accumulator.denominator = 0;
}

-(Fraction *) performOperation:(char) op
{
```objc
Fraction *result;

switch (op) {
    case '+':
        result = [operand1 add: operand2];
        break;
    case '-':
        result = [operand1 subtract: operand2];
        break;
    case '*':
        result = [operand1 multiply: operand2];
        break;
    case '/':
        result = [operand1 divide: operand2];
        break;
}

accumulator.numerator = result.numerator;
accumulator.denominator = result.denominator;

return accumulator;
}

@end
```

# Designing the UI

For this project, your nib file is Fraction_CalculatorViewController.xib. You'll design your interface by selecting this file and laying out the buttons and label as

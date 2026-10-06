
2. This event causes the click1 method to be executed.
3. The click1 method changes the text property of the instance variable display to the string 1.
4. Because the UILabel object display connects to the label in the iPhone's window, this label updates to the corresponding text value, or to the value 1.

For this sequence to work, we just need to make the two connections. There are several ways to do this here, we'll just describe one method.

First, let's get the source code displayed in the third pane. To do this, first select View, Utilities, Hide Utilities. Next, select View, Assistant Editor, Show Assistant Editor. Hopefully, your Xcode window will be close to that shown in Figure 21.14.

# Figure 21.14. Displaying source code alongside the interface.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_713_0.png)

Let's connect the button to the IBAction method click1. You do do this by holding down the Control key while you click on the button and drag the blue line that appears on the screen to the click method displayed in the rightmost pane (and you can drag it to either the method where it's declared in the interface section or where it's defined in the implementation section). This is shown in Figure 21.15.

# Figure 21.15. Adding an action for a button.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_714_0.png)

Now, let's connect the display variable to the label. Select in the iPhone's window, hold down the Control key and click-drag the blue line that appears to the display property declaration in the interface file. This is shown in Figure 21.16.

# Figure 21.16. Connecting an outlet variable.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_715_0.png)

When you release the mouse, the connection is made.

That's it; you're done! Select Run from the Product menu or the toolbar. If all goes well, the program will successfully build and begin execution. When execution begins, your program will be loaded into the iPhone simulator, which will appear on your computer's display. The simulator window should appear as shown in Figure 21.1 at the start of this chapter. You simulate pressing a button with the simulator as we outlined and the connections you made should result in the display of a 1 at the top of the display, as shown in Figure 21.2.

## iPhone Fraction Calculator

The next example is a bit more involved, but the concepts from the previous example equally apply. We're not going to show all the steps to create this example, but rather give a summary of the steps and an overview of the design methodology. Of course, we'll also show all the code.

First, let's see how the application works. Figure 21.17 shows what the application looks like in the simulator just after launching.

# Figure 21.17. Fraction calculator after launch.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_716_0.png)

The calculator application allows you to enter fractions by first keying in the numerator, pressing the key labeled Over, and then keying in the denominator. So to enter the fraction 2/5, you would press 2, followed by Over, followed by 5. You'll note that, unlike other calculators, this one actually shows the fraction in the display, so 2/5 is displayed as 2/5.

After keying in one fraction, you then choose an operation—addition, subtraction, multiplication, or division—by pressing the appropriately labeled key +, -, *, or ÷, respectively.

After keying-in the second fraction, you then complete the operation by pressing the = key, just as you would with a standard calculator.

### Note

This calculator is designed to perform just a single operation between two fractions. It's left as an exercise at the end of this chapter for you to remove this limitation.

The display is continuously updated as keys are pressed. Figure 21.18 shows the display after the fraction 4/6 has been entered and the multiplication key has been pressed.

# Figure 21.18. Keying in an operation.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_718_0.png)

Figure 21.19 shows the result of multiplying the fractions 4/6 and 2/8 together. You'll note that the result of 1/6 indicates that the result has been reduced.

# Figure 21.19. The result of multiplying two fractions.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_719_0.png)

# Starting the New Fraction_Calculator Project

For this second program example, you'll start by creating a new project. As before, select Single View Application from the New Project window. Call your new project Fraction_Calculator.

When your project is created, this time you'll notice you get two class templates defined for you. Fraction_CalculatorAppDelegate.h and Fraction_CalculatorAppDelegate.m define the application's delegate class for your project, while Fraction_CalculatorViewController.h and Fraction_CalculatorViewController.m define the view controller class for your project. As with the first example in this chapter, it's in this latter class where you'll perform all your work.

## Defining the View Controller

Now let's write the code for the view controller class Fraction_CalculatorViewController. We'll start with the interface file. This is shown in Program 21.2.

# 21.2. Program Fraction_CalculatorViewController.h Interface

```objc
#import <UIKit/UIKit.h>
#import "Calculator.h"

@interface Fraction_CalculatorViewController : ViewController

@property (strong, nonatomic) UILabel *display;

-(void) processDigit:(int) digit;
-(void) processOp:(char) theOp;
-(void) storeFracPart;

// Numeric keys

-(IBAction) clickDigit:(UIButton *)sender

// Arithmetic Operation keys

-(IBAction) clickPlus;
-(IBAction) clickMinus;
-(IBAction) clickMultiply;
-(IBAction) clickDivide;

// Misc. Keys

-(IBAction) clickOver;
-(IBAction) clickEquals;
-(IBAction) clickClear;

@end
```

There are housekeeping variables for building the fractions (currentNumber, firstOperand, and isNumerator), and for building the string for the display (displayString). There is also a Calculator object (myCalculator) that can perform the actual calculation between the two fractions. We will associate a single method called clickDigit: to handle the pressing of any of the digit keys 0-9. This method will take an argument that will indicate the actual digit key that was pressed, as you'll shortly see. Finally, we define methods to handle storing the operation to be performed (clickPlus, clickMinus, clickMultiply, clickDivide), carrying out the calculation when the key is pressed (clickEquals), clearing the current operation (clickClear), and separating the numerator from the denominator when Over is pressed (clickOver). Several methods (processDigit:, processOp:, and storeFracPart) are defined to assist in the aforementioned chores.

Program 21.2 shows the implementation file for this controller class. Note that we declare the instance variables in the implementation. We could have declared properties and synthesized them instead. Either approach works fine. The approach we use here keeps the instance variables private and makes it clear they’re used within the class.

```objc
@implementation Fraction_CalculatorViewController
{
    char op;
    int currentNumber;
    BOOL firstOperand;
    BOOL isNumerator;
    Calculator *myCalculator;
    NSMutableString *displayString;
}

@synthesize display;

-(void)viewDidLoad {
    // Override point for customization after application launch
    firstOperand = YES;
    isNumerator = YES;
    displayString = [NSMutableString stringWithCapacity: 40];
    myCalculator = [[Calculator alloc] init];
}

-(void) processDigit:(int) digit {
    currentNumber = currentNumber * 10 + digit;

    [displayString appendString:
[NSString stringWithFormat: @"%i"
digit]];
    display.text = displayString;
}

-(IBAction) clickDigit:(UIButton *)sender {
    int digit = sender.tag;

    [self processDigit:digit];
}

-(void) processOp:(char) theOp {
    NSString *opStr;

    op = theOp;

    switch (theOp) {
        case '+':
            opStr = @"+" + "";
            break;
        case '-':
            opStr = @"-" + "";
            break;
        case '*':
            opStr = @"\*" + "";
            break;
    }
}

@end
```

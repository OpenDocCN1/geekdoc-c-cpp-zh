# 56 Part I: Developer Tools

```
@import "Fusebox.h"

@implementation Fusebox

-(IBAction)calculateAnswer:(id) sender {
    float num1,num2, floatValue;
    num1 = [numberField1 floatValue];
    num2 = [numberField2 floatValue];
    answer = num1 + num2;
    NSNumberFormatter *answerFormatter =
        [[NSNumberFormatter alloc] init] autorelease];

    [answerFormatter
        setFormat:@"##,##.0.00; (#,##.00)"];
    [answerField cell setFormatter:answerFormatter];

    [answerField setFloatValue:answer];

}
@end
```

Now that you've formatted answerField properly, choose Build>Build Go to see your changes in action. You see results, as shown in Figure 3-11.

Figure 3-11: With the NSFormatter object, you can dictate how your application displays floating-point numbers.

![](bbox=[0.263, 0.611, 0.584, 0.735])

Before you leave the debugging section of this chapter, you may come across one kind of error when using Xcode to program Cocoa applications. Change the last line of your code in Fusebox.m to this:

```
[answerField setFloatValue:answer];
```
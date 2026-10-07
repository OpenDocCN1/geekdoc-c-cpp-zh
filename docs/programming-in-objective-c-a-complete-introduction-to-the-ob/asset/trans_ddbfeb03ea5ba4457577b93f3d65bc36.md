

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

在之前的应用程序中，计算器窗口仍然只包含一个标签，我们仍然调用 `display`。当用户逐位输入数字时，我们需要在在此过程中构建该数字。变量 `currentNumber` 存储正在处理的数字，而 BOOL 变量 `firstOperand` 和 `isNumerator` 则用于跟踪这是否是输入的第二个操作数，以及用户当前是在键入操作数的分子还是分母。

当按下计算器上的数字按钮时，我们设置该按钮，以便某些标识信息传递给 `clickDigit:` 方法，以识别按下的是哪个数字按钮。这是通过在检查器（Inspector）中将按钮的 `Tag` 属性设置为每个数字按钮的唯一值来实现。在这种情况下，我们希望将 tag 设置为对应的数字。因此，标签为 0 的按钮的 tag 设置为0，标签为 1 的按钮设置为 1，而发送给 `clickDigit:` 方法的发送者（sender）是 iPhone 窗口中实际按下的 `UIButton`。通过访问该对象的 `tag` 属性，我们获取按钮 tag 的值。这在 `clickDigit:` 方法中所示：

```objc
-(IBAction)clickDigit:(UIButton *)sender
{
    int digit = sender.tag;
    [self processDigit:digit];
}
```

程序 21.2 中的按钮比第一个应用程序多得多。视图控制器的实现文件大部分围绕着构建分数和显示分数展开。当数字 0–9 的按钮被按下时，就会执行动作方法 `clickDigit`。该方法调用 `processDigit:` 方法，将数字跟踪并附加到变量 `currentNumber` 中正在构建的数字末尾。该方法还将数字添加到存储在变量 `displayString` 中的当前显示字符串中，并更新当前显示。

当按下等号键时，会调用 `clickEquals` 方法来执行操作。计算器在两个分数之间执行操作，并将结果存储在它的累加器（accumulator）中。该累加器在 `clickEquals` 方法内部被获取，结果添加到显示中。

## 分数类 (Fraction Class)

Fraction 类与本文之前的示例相比很大程度上保持不变。新增了一个新的 `convertToString` 方法，用于将分数转换为等效字符串表示。程序 21.2 显示了 Fraction 接口，紧接着是对应的实现文件。

## 程序 21.2 Fraction.h 接口文件

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

## 程序 21.2 Fraction.m 实现文件

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

// 向接收者添加一个 Fraction
-(Fraction *)add:(Fraction *)f {
  // 相加两个分数：
  // a/b + c/d ((a*d) + (b*c)) / (b*d)

  // result 将存储加法结果
  Fraction *result = [[Fraction alloc] init autorelease];
  // ... 实现代码 ...
  return result;
}

@end
```

## 第 21 章 编写 iOS 应用程序


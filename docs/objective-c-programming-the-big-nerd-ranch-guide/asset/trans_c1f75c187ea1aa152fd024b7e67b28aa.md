

## 键值编码

键值编码是一种通过属性名称来读取和设置属性的能力。键值编码方法定义在 *NSObject* 中，因此每个对象都具备这种能力。

打开 `main.m` 并找到以下行：

```objectivec
[a setProductName:@"Washing Machine"];
```

将同一行改写为使用键值编码：

```objectivec
[a setValue:@"Washing Machine" forKey:@"productName"];
```

在这种情况下，定义在 *NSObject* 中的 `setValue:forKey:` 方法将去寻找一个名为 `setProductName:` 的 setter 方法。如果对象没有 `setProductName:` 方法，它将直接访问实例变量。

你也可以使用键值编码读取变量的值。在 `main.m` 中添加一行代码来打印产品名称：

```objectivec
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        Appliance *a = [[Appliance alloc] init];
        NSLog(@"a is %@", a);
        [a setValue:@"Washing Machine" forKey:@"productName"];
        [a setVoltage:240];
        NSLog(@"a is %@", a);
        NSLog(@"the product name is %@", [a valueForKey:@"productName"]);
    }
    return 0;
}
```

在这种情况下，定义在 *NSObject* 中的 `valueForKey:` 方法将去寻找一个名为 `productName` 的访问器。如果没有 `productName` 方法，实例变量将被直接访问。

如果你输入的属性名称错误，编译器不会给出警告，但会出现运行时错误。请在 `main.m` 中犯这个错误：

```objectivec
NSLog(@"the product name is %@", [a valueForKey:@"productNammme"]);
```

构建并运行程序时，你会看到一个错误：

```text
*** Terminating app due to uncaught exception 'NSUnknownKeyException',
reason: '<Appliance 0x100108ddd0> valueForKeyForUndefinedKey:]' this class is not key value coding-compliant for the key productNammme.'
```

在继续之前请修复此错误。

键值编码为什么有趣？每当标准框架希望将数据推入你的对象时，它都会使用 `setValue:forKey:`。每当标准框架希望从你的对象读取数据时，它都会使用 `valueForKey:`。例如，Core Data 是一个让你轻松将对象保存到 SQLite 数据库并随后恢复它们的框架。它通过键值编码来操作你自定义的数据承载对象。

## 第 30 章 属性

为了证明即使你没有访问器，键值编码也能操作你的变量，请注释掉 `Appliance.h` 中 `productName` 的 `@property` 声明：

```objectivec
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {
    NSString *productName;
    int voltage;
}
// @property (copy) NSString *productName;
@property (nonatomic) int voltage;

// 指定的初始化器
- (id)initWithProductName:(NSString *)pn;

@end
```

此外，从 `Appliance.m` 中移除对 `setProductName:` 和 `productName` 方法的所有使用：

```objectivec
@implementation Appliance

@synthesize voltage;

- (id)initWithProductName:(NSString *)pn
{
    self = [super init];
    if (self) {
        productName = [pn copy];
        [self setVoltage:120];
    }
    return self;
}

- (id)init
{
    return [self initWithProductName:@"Unknown"];
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"<%d volts>", productName, voltage];
}

@end
```

构建并运行程序。请注意，即使你为 `productName` 没有访问器方法，该变量仍然可以从其他方法中被设置和读取。这显然违反了对象封装的概念——对象的方法是公开的，但实例变量是敏感的，应保持私有。如果键值编码不那么惊人地有用，没有人会容忍它。

### 非对象类型

键值编码方法设计用于与对象配合工作，但有些属性持有的是非对象类型，如 `int` 或 `float`。例如，`voltage` 是一个 `int`。你如何使用键值编码设置 `voltage`？你使用一个 `NSNumber`。

在 `main.m` 中，将设置电压的行从以下代码：

```objectivec
[a setVoltage:240];
```

改为：

```objectivec
[a setValue:[NSNumber numberWithInt:240] forKey:@"voltage"];
```

在 `Appliance.m` 中添加一个显式的访问器，以便你看到它被调用：

```objectivec
- (void)setVoltage:(int)x
{
    NSLog(@"setting voltage to %d", x);
    voltage = x;
}
```

构建并运行程序。

类似地，如果你请求 `valueForKey:@"voltage"`，你将获得一个包含 voltage 值的 **NSNumber**。

*此页故意留白*

## 第 31 章 分类

分类允许程序员向任何现有类添加方法。例如，Apple 给了我们 *NSString* 类。我们拿不到那个类的源代码，但分类让我们能够向 *NSString* 添加新方法。

创建一个名为 VowelCounter 的新 Foundation 命令行工具。然后创建一个 Objective-C 分类的新文件。将该分类命名为 VowelCounting，并使其成为 `NSString` 上的一个分类。

现在打开 `NSString+VowelCounting.h` 并声明你想添加到 **NSString** 类中的方法：

```objectivec
#import <Foundation/Foundation.h>
@interface NSString (VowelCounting)
- (int)vowelCount;
@end
```

现在在 `NSString+VowelCounting.m` 中实现该方法：

```objectivec
#import "NSString+VowelCounting.h"
@implementation NSString (VowelCounting)

- (int)vowelCount
{
    NSCharacterSet *charSet =
    [NSCharacterSet characterSetWithCharactersInString:@"aeiouyAEIOUY"];

    NSUInteger count = [self length];
    int sum = 0;
    for (int i = 0; i < count; i++) {
        unichar c = [self characterAtIndex:i];
        if ([charSet characterIsMember:c]) {
            sum++;
        }
    }
    return sum;
}

@end
```

现在在 `main.m` 中使用新的方法：

```objectivec
#import <Foundation/Foundation.h>
#import "NSString+VowelCounting.h"

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %d vowels", string, [string vowelCount]);
    }
    return 0;
}
```

构建并运行程序。很巧妙，不是吗？结果发现分类非常有用。

需要注意的是，只有这个程序拥有该分类。如果你希望该方法在另一个程序中可用，你必须将该文件添加到你的项目中，并在构建该程序时编译该分类。

## 第 32 章 块

在第 24 章中，你学习了关于委托和通知的回调机制。回调允许其他对象在响应事件时调用你对象中的方法。虽然这些方法功能完备，但它们会打乱你的代码结构。那些为了清晰度希望靠得较近的程序部分通常做不到。

例如，在第 24 章的 Callbacks 程序中，你添加了代码，在用户时区更改时注册对象以接收通知，并设置 `zoneChange:` 在该通知接收时触发。但现在我正在阅读你的代码，好奇这个 `zoneChange:` 方法在触发时做什么，所以我去寻找该方法的实现。在 Callbacks 示例中，注册对象以接收通知的代码和触发方法实现的代码紧挨着，但你可以想象，在一个更大、更复杂的应用程序中，这两部分代码可能相距数百行。

Mac OS X 10.6 和 iOS 4 引入了一项名为块的新特性。Objective-C 块就像 C 函数一样只是一块代码，但它可以作为数据传递。我们将很快看到这是如何保持相关代码在一起的。

块和块语法绝对是高级 Objective-C 主题，一开始可能会让人困惑。然而，Apple 的 API 正在越来越多地使用块。在本章中，我们将逐步讲解几个简单的示例，以便当你遇到野外（实际应用中）的块时做好准备。

如果你在另一种编程语言方面有背景知识，你可能知道块被称为匿名函数、闭包或 lambda。如果你熟悉函数指针，块可能看起来与之相似，但你很快就会看到，块的恰当使用允许编写比使用函数指针更优雅的代码。

### 定义块

这是一个块：

```objectivec
^{
    NSLog(@"I’m a log statement within a block!");
}
```

这看起来像一个函数，但它有一个插入符号（`^`）代替函数名称。插入符号标识这部分代码为一个块。此外，像函数一样，块可以接受参数：

```objectivec
^(double dividend, double divisor) {
    double quotient = dividend / divisor;
    return quotient;
}
```


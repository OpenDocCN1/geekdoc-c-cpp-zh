
```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        // Read in a file as a huge string (ignoring the possibility of an error)
        NSString *nameString = [NSString stringContentsOfFile:@"/usr/share/dict/propernames"
                                encoding:NSUTF8StringEncoding
                                error:NULL];

        // Break it into an array of strings
        NSArray *names = [nameString componentsSeparatedByString:@""];
        for (NSString *n in names) {
            // Look for "AA" in case-insensitive manner
            NSRange r = [n rangeOfString:@"AA" options:NSCaseInsensitiveSearch];
            if (r.location != NSNotFound) {
                NSLog("%@", n);
            }
        }
    }
    return 0;
}
```

## 第 25 章

它是 Foundation 框架的一部分，并随着每个版本的 Mac OS X 和每个版本的 iOS 发布。

在头文件的末尾，有一份指南列表，讨论了展示 `NSArray` 能力的 `NSArray` 示例代码。点击“Collections Programming Topics”（集合编程主题）来打开该指南。

## 图 16.3 集合编程主题

![](img/a694739dec801cd745c57da9e19c2cd4_144_0.png)

本特定指南讨论了集合类（包括 `NSArray` 和 `NSMutableArray`）。与类引用（class reference）不同，指南是需要阅读的材料，它以合理的顺序引入了概念。

现在使用文档窗格顶部的返回按钮回到 `NSArray` 引用页面。好奇你还可以向 `NSArray` 发送哪些消息吗？滚动引用页面并找到 `NSArray` 实现的方法列表。假设你想找一种方法检查数组是否包含某个特定项目。在这种情况下，你会遇到 `containsObject:` 方法并阅读其描述：

## 图 16.4 containsObject 的引用

### containsObject:

返回一个布尔值，表示给定对象是否存在于数组中。

```objc
- (BOOL)containsObject:(id)anObject
```

#### 参数

`anObject`
一个对象。

#### 返回值

如果 `anObject` 存在于数组中返回 `YES`，否则返回 `NO`。

#### 讨论

此方法通过向数组的每个对象发送 `isEqual:` 消息（并将 `anObject` 作为参数传递给每个 `isEqual:` 消息）来确定 `anObject` 是否存在于数组中。

#### 可用性

适用于 Mac OS X v10.0 及更高版本。

#### 另见

- `indexOfObject:`
- `indexOfObjectIdenticalTo:`

#### 相关示例代码

Sketch+Accessibility, TimelineToTC

#### 声明于

`NSArray.h`

现在你已经了解了在代码中发送此消息所需的所有知识。

## 快速帮助

但有一种更简单的方法可以从编写代码的编辑器跳转到文档中的知识源。关闭 Organizer（组织器）并返回你的 DateList 项目。

在 `main.m` 中，找到包含 `[dateList addObject:now]` 的那行。按住 Option 键并点击 `addObject:`。快速帮助窗口将出现并显示有关该方法的信息：

```objc
// Create three Date objects
Date *now = [NSDate date];
Date *tomorrow = [now dateByAddingTimeInterval:24];
Date *yesterday = [now dateByAddingTimeInterval:-24];
// Create an array
NSMutableArray *dateList = [NSMutableArray array];
// Add the dates to the array
[dateList addObject:now];
[dateList addObject:tomorrow];
```

```
addObject:
Name: addObject
Declaration: (void)addObject:(id)addObject
Availability: Mac OS X (10.0 and later)
Abstract: 将给定对象插入到数组末尾。
Parameters: addObject: 要添加到数组内容末尾的对象。
Declared in: NSMutableArray
Reference: NSMutableArray Class Reference
Related Documents: Collections Programming Topics, Key-Value Coding Programming Guide
```

注意快速帮助窗口中存在链接。如果你点击链接，它将在 Organizer 中打开相应的文档。很有用对吧？

如果你想一直看到快速帮助，可以将其作为一个窗格在 Xcode 中打开。

在 Xcode 窗口的右上角，找到一个名为 View（视图）的分段控件，它看起来并指示了 Xcode 的左侧、底部和右侧窗格。选择和取消选择这些按钮将隐藏和显示相应的窗格。

你现在已经经常使用的左侧窗格，被称为 navigator（导航器）；你也过的底部窗格包含了控制台，被称为 debug area（调试区域）。右侧窗格被称为 Utilities（工具）。点击右侧的 View 按钮以显示 Utilities。在 Utilities 顶部，点击按钮显示 Quick Help（快速帮助）窗格。

此窗格将为编辑器中选中的文本提供帮助。尝试：只需在编辑器中选择单词 "NSMutableArray"

## 图 16.6 快速帮助窗格

![](img/a694739dec801cd745c57da9e19c2cd4_147_0.png)

注意，当你选择其他内容时，快速帮助窗格将立即更新以显示新选择的文档。

## 其他选项和资源

如果你对任何文本进行 Option-双击，Organizer 将搜索该字符串。

如果你对任何类、函数或方法进行 Command-点击，Xcode 将向你显示其定义的文件。（尝试 Command-点击“NSMutableArray”一词）。

## 图 16.7 NSMutableArray 的声明

![](img/a694739dec801cd745c57da9e19c2cd4_148_0.png)

如果有多个匹配的声明，当你 Command-点击时会弹出一个窗口。尝试 Command-点击 `addObject:`。

Xcode 有时会回溯母服务器检查是否有任何更新的文档。它将下载更新并对它们进行重新索引以便搜索。你可以在 Xcode 的偏好设置面板中触发立即更新。

Apple 在 http://lists.apple.com/ 托管了一系列讨论邮件列表，其中有几个致力于开发者主题。如果你在文档中找不到答案，请尝试搜索列表的存档。

还有一个你应该知道的另一个资源：stackoverflow.com。这是一个程序员提问和回答问题的非常流行的地方。

## 你的第一个类

到目前为止你只使用了实例变量。现在你可以编写方法了。

要创建一个新项目，选择 File → New → Project... 从 Mac OS X 选择 Cocoa 并选择 Command Line Tool。将类命名为 Person 并使其成为 `NSObject` 的子类。最后，确保勾选了 target 并点击 Save。

注意新的类文件 `Person.h` 和 `Person.m` 现在出现在项目导航器中。打开 `Person.h`。声明实例变量和方法：

```objc
#import <Foundation/Foundation.h>
// 类继承所有的实例变量
// 和方法
@interface Person : NSObject {
// 它有两个实例变量
    float heightMeters;
    int weightKilos;
}
```

注意你将实例变量放在大括号内，将方法放在大括号外。对于编译器来说，这段代码表示“我正在定义一个名为 Person 的类，它拥有 `NSObject` 的所有方法和实例变量。此外，我增加了实例变量：名为 `heightMeters` 的 float 和名为 `weightKilos` 的 int。我还将添加三个实例方法，它们将在 `Person.m` 中实现。”

注意 `setHeightMeters` 需要一个 float 参数且没有返回值，`setWeightKilos` 需要一个 int 参数且没有返回值，`bodyMassIndex` 无参数并返回 float。

现在打开 `Person.m`。删除现有的方法并实现你声明的方法：

```objc
#import "Person.h"

@implementation Person

- (void)setHeightMeters:(float)h
{
    heightMeters = h;
}
- (void)setWeightKilos:(int)w
{
    weightKilos = w;
}
- (float)bodyMassIndex
{
    // 此方法计算体重指数；
    return (float)weightKilos / (heightMeters * heightMeters);
}
@end
```

注意 Xcode 为你导入了 `Person.h`。还要注意，你实现的方法名称必须与你在头文件中声明的完全匹配。在 Xcode 中，这很容易；当你开始在实现文件中输入方法时，Xcode 会建议你已经声明的方法。

现在你已经实现了在 `Person.h` 中声明的所有方法，你的类已经完善了。编辑 `main.m` 来练习一下：

```objc
#import <Foundation/Foundation.h>
#import "Person.h"

int main(int argc, const char * argv[])
{
    // 创建 Person 的实例
    Person *person = [[Person alloc] init];

    // 给实例变量赋予一些有趣的值
    [person setWeightKilos:96];
    [person setHeightMeters:1.8];

    // 调用 bodyMassIndex 方法
    float bmi = [person bodyMassIndex];
    NSLog(@"person has a BMI of %f", bmi);

    return 0;
}
```

编译并运行程序。注意你导入了 `Person.h`，这样编译器在 `main()` 使用这些方法之前就已经知道它们是如何声明的。

## 图 17.1 BMITime 的对象图

| main() | Person |
| --- | --- |
| person | weightInKilos = 96 |
| | heightMeters = 1.8 |
| | - (float)bodyMassIndex |

## 访问方法

注意，当我们使用结构体（structs）而不是对象进行同样的练习时，我们直接在 `main()` 中访问了结构的数据成员：

```objc
person.weightInKilos = 96;
person.heightInMeters = 1.8;
```

在面向对象的思维中，我们尽力让对象的实例变量保持私有；也就是说，它们只由对象本身感知和访问。然而，由于我们想让 `Person` 外部的方法和函数能够设置人的体重和身高，我们创建了 `setWeightInKilos:` 和 `setHeightInMeters:` 方法。我们称这些方法为 setter 方法（设置方法）。

setter 方法允许其他方法设置实例变量的值。getter 方法（获取方法）允许其他方法读取实例变量的值。setter 和 getter 方法也称为访问方法（accessor methods），或直接称为访问器（accessors）。

在 `Person.h` 中添加 getter 方法的声明：

```objc
#import <Foundation/Foundation.h>
@interface Person : NSObject
{
    float heightInMeters;
    int weightInKilos;
}
// 你将能够设置这些实例变量
- (float)heightInMeters;
- (void)setHeightInMeters:(float)h;
- (int)weightInKilos;
- (void)setWeightInKilos:(int)w;
- (float)bodyMassIndex;
@end
```

你可能会奇怪，为什么 getter 方法的名字没有包含 `get` 以匹配 setter 方法的名字。这是一种 Objective-C 的命名规范。读取实例变量的方法名直接就是该实例变量的名字。

现在回到 `Person.m` 并实现你的 getter 方法：

```objc
@implementation Person
- (float)heightInMeters
{
    return heightInMeters;
}
- (void)setHeightInMeters:(float)h
{
    heightInMeters = h;
}
- (int)weightInKilos
{
    return weightInKilos;
}
- (void)setWeightInKilos:(int)w
{
    weightKilos = w;
}
- (float)bodyMassIndex
{
    return weightInKilos / (heightInMeters * heightInMeters);
}
@end
```

最后，在 `main.m` 中使用这些方法：

```objc
#import "Person.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Person 的实例
        Person *person = [[Person alloc] init];

        // 给实例变量赋予有趣的体重值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];

        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person has a BMI of %f", bmi);
    }
    return 0;
}
```

编译并运行程序。注意你导入了 `Person.h`，这样编译器在 `main()` 使用这些方法之前就已经知道它们是如何声明的。

## 点语法（Dot notation）

使用点号而不是方括号的形式被称为 *点语法*（dot notation）。这种形式隐藏了正在发送消息的事实：

```objc
x.fido;
```

点语法让这两行代码完全相同：

```objc
[x fido];
x.fido = 3;
```

## 属性（Properties）

你可能会奇怪，为什么 getter 方法的名字没有包含 `get` 以匹配 setter 方法的名字。这是一种 Objective-C 的命名规范。读取实例变量的方法名直接就是该实例变量的名字。

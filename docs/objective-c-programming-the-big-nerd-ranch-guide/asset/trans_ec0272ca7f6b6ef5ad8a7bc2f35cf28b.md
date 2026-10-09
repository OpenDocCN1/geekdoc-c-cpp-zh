

```objectivec
NSMutableArray *hotel = [[NSMutableArray alloc] init];

// Lobby on the ground floor
[hotel addObject:lobby];

// Pool on the second
[hotel addObject:pool];

// The third floor has not been built out
[hotel addObject:[NSNull null]];

// Bedrooms on fourth floor
[hotel addObject:bedrooms];
```

## 挑战

浏览 **NSArray**、**NSMutableArray**、**NSDictionary** 和 **NSMutableDictionary** 的参考页面。你将每天都会使用这些类。

## 第 22 章 常量

我们花了很多时间讨论变量，顾名思义，变量的值会随着程序的运行而变化。然而，有一些信息是*不*会改变值的。例如，数学常数 $\pi$ 永远不会改变。我们把这些称为*常量*，Objective-C 程序员定义常量有两种常见方式：`#define` 和全局变量。

在 Xcode 中，创建一个名为 Constants 的新 Foundation 命令行工具。

在标准 C 库中，常量是使用 `#define` 预处理器指令定义的。标准 C 库的数学部分在文件 `math.h` 中声明。在那里定义的常量之一是 `M_PI`。在 `main.m` 中使用它：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // In literal NSString, use \u for arbitrary unicode chars
        NSLog(@"\u03c0 is %f", M_PI);
    }
    return 0;
}
```

当你构建并运行它时，你应该看到：

$\pi$ is 3.141593

要查看定义，在编辑器中按住 Command 键点击 `M_PI`。它将带你到 `math.h` 中的以下一行：

```c
#define M_PI         3.14159265358979323846264338327950288
```

### 预处理器指令

编译 C、C++ 或 Objective-C 代码的文件分为两个阶段。首先，*预处理器*运行该文件。预处理器的输出然后进入真正的编译器。预处理器指令以 `#` 开头，三个最流行的是 `#include`、`#import` 和 `#define`。

### #include 和 #import

`#include` 和 `#import` 基本上做同样的事情：请求预处理器读取一个文件并将其添加到其输出中。通常，你正在包含一个声明文件（.h 文件），并且这些声明被编译器用来理解正在编译的代码。

`#include` 和 `#import` 有什么区别？`#import` 确保预处理器只包含一个文件一次。`#include` 允许你多次包含相同的文件。C 程序员倾向于使用 `#include`。Objective-C 程序员倾向于使用 `#import`。

在指定要导入的文件名时，你可以用引号或尖括号将文件名括起来。引号表示头文件在你的项目目录中。尖括号表示头文件在预处理器知道的某个标准位置中。（例如，`<math.h>` 是 `/Developer/SDKs/MacOSX10.7.sdk/usr/include/math.h`）以下是 `#import` 指令的两个示例：

```objectivec
// Include the headers I wrote for Pet Store operations
#import "PetStore.h"

// Include the headers for the OpenLDAP libraries
#import <ldap.h>
```

在一个项目中，过去很常见的做法是在每个代码文件中包含一组头文件。这导致了文件开头的杂乱，并使编译时间更长。为了简化生活并使编译更快，大多数 Xcode 项目都有一个文件，列出了要预编译并包含在每个文件中的头文件。在你的 Constants 项目中，这个文件叫做 `Constants-Prefix.pch`。

那么，当 `main.m` 被编译时，`math.h` 中的常量是如何被包含进去的呢？你的 `main.m` 文件有以下行：

```objectivec
#import <Foundation/Foundation.h>
```

文件 `Foundation.h` 有以下行：

```c
#include <CoreFoundation/CoreFoundation.h>
```

文件 `CoreFoundation.h` 有以下行：

```c
#include <math.h>
```

### #define

`#define` 告诉预处理器：“每当遇到 A，在编译器看到它之前，将其替换为 B。” 再次查看 `math.h` 中的那一行：

```c
#define M_PI 3.14159265358979323846264338327950288
```

在 `#define` 指令中，你只用空格将两部分（令牌及其替换值）分开。

`#define` 实际上可以用来创建类似函数的东西。在 `main.m` 中，打印两个数字中较大的那个：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
    }
    return 0;
}
```

MAX 不是一个函数；它是一个 `#define`。最基础的 C 版本 MAX 是：

```c
#define MAX(A, B)    ((A) > (B) ? (A) : (B))
```

因此，当编译器看到你刚才添加的那一行时，它看起来是这样的：

```objectivec
NSLog(@"%d is larger", ((10) > (12) ? (10) : (12)));
```

当你使用 `#define` 做类似函数的事情，而不仅仅是替换一个值时，你就创建了一个宏。

## 全局变量

Objective-C 程序员通常不使用 `#define`，而是使用全局变量来存储常量值。

让我们在你的程序中添加一些内容来解释。首先，有一个名为 `NSLocale` 的类，它存储关于不同地理位置的信息。你可以获取用户当前区域设置的实例，然后向它提出问题。例如，如果你想知道用户区域设置的货币是什么，你可以这样询问：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));

        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:@"currency"];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

构建并运行它。根据你的位置，你应该会看到类似以下内容：

Money is USD

然而，如果你将键拼写错误为 `@"Kuruncy"`，你什么也得不到。为了防止这个问题，Foundation 框架定义了一个名为 `NSLocaleCurrencyCode` 的全局变量。输入它并不更方便，但如果你拼写错误，编译器会抱怨。此外，Xcode 中的代码补全对全局变量有效，但对字符串 `@"currency"` 无效。更改你的代码以使用该常量：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
        
        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:NSLocaleCurrencyCode];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

当编写类 **NSLocale** 时，这个全局变量出现在两个地方。在 `NSLocale.h` 中，该变量的声明类似于这样：

```objectivec
extern NSString const *NSLocaleCurrencyCode;
```

**const** 表示该指针在整个程序生命周期内不会改变。**extern** 表示“我承诺这个变量存在，但它将在其他文件中定义。” 确实，在文件 `NSLocale.m` 中，有一行是这样的：

```objectivec
NSString const *NSLocaleCurrencyCode = @"currency";
```

## enum（枚举）

你经常需要定义一组常量。例如，想象你正在开发一种有五种速度的搅拌机：Stir（搅拌）、Chop（切碎）、Liquify（液化）、Pulse（脉冲）和 Ice Crush（碎冰）。你的类 **Blender** 将有一个名为 **setSpeed:** 的方法。最好让类型表明只允许五种速度之一。为此，你需要定义一个枚举：

```objectivec
enum BlenderSpeed {
    BlenderSpeedStir = 1,
    BlenderSpeedChop = 2,
    BlenderSpeedLiquify = 5,
    BlenderSpeedPulse = 9,
    BlenderSpeedIceCrush = 15
};

@interface Blender : NSObject
{
    // speed must be one of the five speeds
    enum BlenderSpeed speed;
}

// setSpeed: expects one of the five speeds
- (void)setSpeed:(enum BlenderSpeed)x;
@end
```

开发者厌倦了键入 `enum BlenderSpeed`，所以他们经常使用 `typedef` 为其创建一个简写形式：


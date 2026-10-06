

# 程序 9.5. 异常处理

```objc
#import "Fraction.h"

int main (int argc, char * argv [])
{
    @autoreleasepool {
        Fraction *f = [[Fraction alloc] init];

        @try {
            [f noSuchMethod];
        }
        @catch (NSException *exception) {
            NSLog("Caught %@@@", [exception name], [exception reason]);
            NSLog("Execution continues!");
        }
    }
    return 0;
}
```

# 程序 9.5. 输出

*** -[Fraction noSuchMethod]: unrecognized selector sent to instance 0x103280
Caught NSInvalidArgumentException: -[Fraction noSuchMethod]: unrecognized selector sent to instance 0x103280
Execution continues!

当异常发生时，@catch 块会被执行。一个包含异常信息的 NSException 对象将作为参数传递到此块。如你所见，`name` 方法获取异常的名称，而 `reason` 方法给出原因（这是运行时系统之前自动打印的）。

在执行完 @catch 块中的最后一条语句后（我们这里只有一条），程序将继续执行紧接在该块之后的语句。在例例中，执行 `NSLog` 调用以验证执行已经继续而没有终止。

这是一个非常简单的示例，用来说说明如何在程序中捕获异常。@finally 块可以用于包含一段代码，无论 @try 块中的语句是否抛出异常，这些代码都会执行。

@throw 指令允许你抛出自己的异常。你可以使用它来抛出一个特定的异常，或者在 @catch 块内部使用它来抛出导致进入该块的同一个异常，如下所示：

```objc
@throw;
```

你可能想在自己处理完异常后这样做（例如，在执行完清理工作之后）。然后你可以让系统为你处理剩余的工作。

你可以拥有多个多个 @catch 块，并按顺序排列以捕获和处理不同类型的异常。

通常情况下，你不希望异常在程序运行时发生。因此，在错误发生之前对其进行测试比在发生后捕获它们被认为是更好的编程实践。在方法中测试错误并返回某个值作为错误指示器，也比抛出异常更好。抛出异常会消耗大量的系统资源，因此 Apple 通常不建议在没有的情况下使用它们（例如，你不想仅仅因为无法打开文件就抛出异常）。

# 练习题

- 1. 如果在程序 9.1 执行加法操作后插入消息表达式 `[compResult reduce];` 会发生什么？尝试一下并看看。
- 2. 在程序 9.2 中定义的 `id` 变量 `dataValue` 是否可以赋值你在第 8 章中定义的 `Rectangle` 对象？也就是说，语句 `dataValue = [[Rectangle alloc] init];` 是否可行？为什么可以或为什么不可以？
- 3. 为你在第 8 章中定义的 `XYPoint` 类添加一个 `print` 方法。让它以 (x, y) 的格式显示点。然后修改程序 9.2 以引入一个 `XYPoint` 对象。让修改后的程序创建一个 `XYPoint` 集合，设置其值，将其分配给 `id` 变量 `dataValue`，然后显示其值。
- 4. 根据本章关于参数和返回类型的讨论，修改 `Fraction` 和 `Complex` 类中的 `add` 方法以接收并返回 `id` 对象。编写一个包含以下代码序列的程序：

```objc
result = [dataValue1 add: dataValue2];
[result print];
```
在这里，result、`dataValue1` 和 `dataValue2` 都是 `id` 对象。确保你在程序中正确设置了 `dataValue1` 和 `dataValue2`。

# 注意

你需要将方法名更改为 `add:` 以外的内容。因为系统的 `NSObject` 类也有一个 `add:` 方法。正如本章之前“动态类型下的参数和返回类型”部分提到的，如果不同类中存在同名方法，且接收者的类型在编译时未知，编译器将执行一致性检查，以确保同名方法之间的参数和返回类型保持一致。

- 5. 给定本文已使用的 `Fraction` 和 `Complex` 类定义以及以下定义：

```objc
Fraction *fraction = [[Fraction alloc init];
Complex *complex = [[Complex alloc init];
id number = [[Complex alloc init];
```
确定以下消息表达式的返回值。然后将它们输入程序中以验证结果。

```objc
[fraction isMemberOfClass:[Complex class]];
[complex isMemberOfClass:[NSObject class]];
[complex isKindOfClass:[NSObject class]];
[fraction isKindOfClass:[Fraction class]];
[fraction respondsToSelector:@selector (print)];
[complex respondsToSelector:@selector (print)];
[Fraction instancesRespondToSelector:@selector (print)];
[number respondsToSelector:@selector (print)];
[number isKindOfClass: [Complex class]];
[[number class] respondsToSelector: @selector (alloc)];
```

# 10. 关于变量和数据类型的更多

在本章中，我们将详细介绍变量作用域、对象的初始化方法以及数据类型。

对象的初始化值得特别关注，我们在这里对此予以关注。

我们在第 7 章“类进阶”中自由地讨论了实例变量以及静态和局部变量的作用域。在这里，我们将更多地讨论静态变量，并引入全局和外部变量的概念。此外，你可以向 Objective-C 编译器提供特定的指令，以便更精确地控制实例变量的作用域。我们在本章中也会涵盖这些指令。

枚举数据类型允许你定义一个仅用于存储指定列表的数据类型。Objective-C 语言的 `typedef` 语句允许为内置或派生类型分配自定义名称。最后，在本章中，我们将详细描述 Objective-C 编译器在转换数据类型时遵循的精确步骤。

# 初始化对象

你以前见过这种模式：分配一个新对象的实例并初始化它，使用如下熟悉的序列：

```objc
Fraction *myFract = [[Fraction alloc] init];
```

我们没有编写自己的 `init` 方法；使用的是继承自父类 `NSObject` 的方法。

在调用这两个方法之后，通常会为新对象分配一些值，如下：

```objc
[myFract setTo: 1 over: 3];
```

初始化对象并设置初始值的过程通常合并为一个方法。例如，你可以定义一个 `initWith:over:` 方法，初始化分数并将分子分母设置为提供的参数。

包含许多方法和实例变量的类通常也有多个初始化方法。例如，Foundation 框架的 `NSArray` 类包含以下初始化方法：

```objc
initWithArray:
initWithArray:copyItems:
initWithContentsOfFile:
initWithContentsOfURL:
initWithObjects:
initWithObjects:count:
```

一个数组可能被分配并使用以下方式初始化：

```objc
myArray = [[NSArray alloc] initWithArray:otherArray];
```


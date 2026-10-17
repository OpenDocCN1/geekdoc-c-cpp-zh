
默认情况下，所有指针变量都是强（strong）。这意味着将对象赋值给此类变量会导致其被保留。最后，在进行赋值之前会释放旧对象。强变量默认初始化为零。无论是实例变量还是局部变量都是如此。

看这段代码，它创建了两个 `Fraction` 对象：

```
Fraction *f1 = [[Fraction alloc] init];
Fraction *f2 = [[Fraction alloc] init];
```

```
[f1 setTo: 1];
[f2 setTo: 2];
```

现在，当你使用手动内存管理编写以下代码时：

```
f2 = f1;
```

效果仅仅是将引用复制到 `f2`。`f2` 引用的 `Fraction` 对象将因为其值被覆盖而丢失。这将导致所谓的“内存泄漏”；即一个不再被引用因此无法被释放的变量。

如果你使用 ARC，`f1` 和 `f2` 都是强变量。因此，之前的赋值实际上执行如下：

```
[f1 retain]; // 保留新值
[f2 release]; // 释放旧值
f2 = f1; // 复制引用
```

当然，你看不到这些操作，因为编译器已经为你完成了所有工作。你只需要编写赋值语句并忘记它即可。

由于所有对象变量默认都是强性的，你不需要显式声明它们。然而，你可以使用 `_strong` 关键字显式地这样做：

```
_strong Fraction *fl;
```

需要注意的是，属性默认不是强。它们的默认属性是 `unsafe_retained`（等同于 `assign`）。你已经见过如何为属性声明强属性：

```
@property (strong, nonatomic) NSMutableArray *birdNames;
```

编译器通过在赋值时保留（retain）来确保强属性存越事件循环。对于 `unsafe_retained`（即 `assign`）或 `weak` 属性，不会采取此类操作。

# 弱变量

有时会在两个对象之间建立关系，每个对象都需要引用另一个对象（这可能是简单的两个对象，也可能是创建循环的对象链）。例如，iOS 应用程序通过称为视图（views）的对象在屏幕上呈现图形。视图以层次结构形式维护。因此，人们可能会展示一张图片，而在图像视图内部你可能想为该图片显示标题。你可以这样设置：图像视图是主视图，标题是子视图。当主视图显示时，子视图也会自动显示。你可以将图像视图视为父视图，将标题视为子视图。主视图拥有该子视图。

当处理此视图层级结构时，父视图通常希望持有其子视图的引用。但在处理子视图时，让子视图知道父视图是谁也是很有用的。因此，父视图会持有对子视图的引用，而子视图反过来也会持有对父视图的引用。这种循环引用可能会产生问题。例如，当我们销毁父视图会发生什么？从子视图到父视图的引用将不再有效。事实上，尝试引用该不存在的父视图可能会应用程序崩溃。

当两个对象互相持有强引用（strong references）时，你就创建了所谓的“保留循环”（retain cycle）。如果仍然存在对对象的引用，系统就不会销毁它。因此，如果两个对象互相持有强引用，它们任何一个都永远无法被销毁。

解决这个问题的方法是创建另一种类型的对象变量，允许在两个对象之间建立不同类型的引用，即“弱引用”（weak reference）。在这种情况下，弱引用将从子对象指向父对象。为什么？因为我们认为拥有另一个对象（在本例中为父视图）的对象视为强引用，而将另一个对象视为弱引用。

通过让父视图持有对其子视图的强引用，而让子视图对其父视图持有弱引用，就不会创建保留循环。弱变量不会阻止其所引用的对象的释放。

当你声明一个弱变量时，会发生几件事：系统会跟踪赋值给该变量时创建的引用。当被引用的对象被释放时，弱变量会被设置为 nil。这防止了由于无意中向该变量发送消息可能导致的任何崩溃。因为变量会被设置为 nil，向 nil 对象发送消息将产生任何结果，从而防止了崩溃。

要声明弱变量，你使用 `__weak` 关键字：

```
__weak UIView *parentView;
```

或者对属性使用 `weak` 属性：

```objc
@property (weak, nonatomic) UIView
*parentView;
```

弱变量在处理代理（delegates）时也很有用。通过将持有代理引用的变量设为弱变量，你可以确保当代理对象被释放时，该变量会被置零。同样，这可以防止在 ARC 发明之前让许多程序员头疼的这类系统崩溃。

注意，iOS 4 或 Mac OS v10.6 不支持弱变量。在这种情况下，你仍然可以使用 `unsafe_retained`（或 `assign`）属性标记，或者将变量声明为 `__unsafe_retained`。但要意识到，当引用的对象释放时，这些变量不会自动置零。

# @autoreleasepool 块

在本书目前为止的每个示例中，你已经看到编译器如何在你的主程序内部生成 `@autoreleasepool` 指令。该指令包含了一块语句，定义了一个自动释放池上下文。在该上下文中创建的任何对象如果是自动释放的（这是使用 ARC 自动完成的），默认会在该 `@autoreleasepool` 块结束时被销毁（除非编译器已妥善确保它们在块结束后仍然存在）。

如果你的程序产生了大量的临时对象（这在循环内部执行代码时很容易发生），你可能想在程序中创建多个 `autoreleasepool` 块。例如，以下代码段说明了如何设置 `autoreleasepool` 块来管理 for 循环每次迭代创建的临时对象：

```objc
for (i = 0; i < n; ++i) {
  @autoreleasepool {
    ... 这里有大量关于临时
    对象的操作
  }
}
```

正如本章前面提到的，Cocoa 和 iOS 应用程序在事件循环内部运行。为了处理新事件，系统会创建一个新的自动释放池上下文，并可能调用你应用程序中的某些方法来处理事件。当你处理事件时，你会从方法返回，系统会等待下一个事件发生。在此之前，`autoreleasepool` 上下文结束了，这意味着自动释放的对象随后可能会被销毁。同样，通过 ARC，这一切都在“底层”自动完成，所以你不需要担心它。

# 方法名与非 ARC 编译代码

ARC 适用于未使用 ARC 编译的代码。例如，当你与旧版本的框架链接时，就可能发生这种情况。只要非 ARC 代码确认遵循了标准的 Cocoa 命名规范，一切都会没问题。也就是说，当 ARC 看到一个方法调用时，它会检查方法名。如果名称以 `alloc`、`new`、`copy`、`mutableCopy` 或 `it` 单词开头，它假设该方法将对象的所有权交还给方法调用者。

当我们在这里谈论“单词”时，指的是以驼峰命名法（camelCase）编写的单词。即名称中每个新单词的首字母都大写。编译器假设命名为 `allocFraction`、`newAddressCard` 和 `initWithWidth:andHeight:` 的方法返回对象的所有权，而 `newlyWeds`、`copycat` 和 `initials` 则不是。同样，这由 ARC 自动完成，所以你不需要担心这些，除非你正在使用不这些标准命名规范的方法。在这些情况下，有方法可以显式告诉编译器无论名称如何，某个方法是否返回对象的所有权。

你应该注意，如果你尝试合成名称以本节第一段提到的任何特殊单词开头的属性，编译器会给你一个错误。

# 18. 复制对象

本章讨论了复制对象的一些细节。我们介绍了浅拷贝与深拷贝的概念，并讨论了如何在 Foundation 框架下进行拷贝。

第八章“继承”讨论了在使用简单的赋值语句将一个对象赋值给另一个对象时发生的情况，例如：

```objc
origin = pt;
```

在这个示例中，`origin` 和 `pt` 都是 `XYPoint` 对象，具有两个名为 `x` 和 `y` 的整数实例变量。

回想一下，赋值的效果是将对象 `pt` 的地址复制到 `origin` 中。在赋值操作结束时，两个变量都指向内存中的同一个位置。通过类似下面的消息对实例变量进行更改

```objc
[origin setX:100 setY:200];
```

会改变 `origin` 和 `pt` 变量引用的 `XYPoint` 对象的 x、y 坐标，因为它们引用的是内存中的同一个对象。

Foundation 对象也是如此：将一个变量赋值给另一个仅仅是创建了指向对象的另一个引用。因此，如果 `dataArray` 和 `dataArray2` 都是 `NSMutableArray` 对象，以下语句从两个变量引用的同一个数组中删除第一个元素：

```objc
dataArray2 = dataArray;
[dataArray2 removeAtIndex:0];
```

## copy 和 mutableCopy 方法

Foundation 类实现了名为 `copy` 和 `mutableCopy`的方法，你可以用它们创建对象的拷贝。这是通过实现符合`<NSCopying>` 协议的方法的。如果你的类需要区分创建可变和不可变的拷贝，你还必须根据`<NSMutableCopying>` 协议实现一个方法。你将在本节稍后的部分学习如何这样做。

回到 Foundation 类的拷贝方法，给定上一节描述的两个 `NSMutableArray` 对象 `dataArray2` 和 `dataArray`，语句

```
dataArray2 = [dataArray mutableCopy];
```

会在内存中创建 `dataArray` 的新拷贝，复制其所有元素。随后，执行语句

```objc
[dataArray2 removeAtIndex:0];
```

从 `dataArray2` 中删除第一个元素，但不会从 `dataArray` 中删除。程序 18.1 说明了这一点。

### 程序 18.1

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray =
        [NSMutableArray arrayWithObjects:
```

```objc
"@one", @"two", @"three", @"four",
nil];
NSMutableArray *dataArray2;
//简单赋值
dataArray2 = dataArray;
[dataArray2 removeObjectAtIndex: 0];
NSLog("@dataArray: " ");
for ( NSString *elem in dataArray )
    NSLog("@%@", elem);
NSLog("@dataArray2: " ");
for ( NSString *elem in dataArray2 )
    NSLog("@%@", elem);
// // 尝试拷贝，然后从副本中移除第一个
// 元素
dataArray2 = [dataArray mutableCopy];
[dataArray2 removeObjectAtIndex: 0];
NSLog("@dataArray: " ");
for ( NSString *elem in dataArray )
    NSLog("@%@", elem);
NSLog("@dataArray2: " ");
for ( NSString *elem in dataArray2 )
    NSLog("@%@", elem);
}
```

```objc
return 0;
}
```

### 程序 18.1 输出

```
dataArray:
two
three
four
dataArray2:
two
three
four
dataArray:
two
three
four
dataArray2:
three
four
```

该程序定义了可变数组对象 `dataArray`，并将其元素设置为字符串对象 @"one"、@"two"、@"three" 和 @"four"。正如我们讨论过的，这种赋值

```objc
dataArray2 = dataArray;
```

只是简单地创建了内存中指向同一个数组对象的另一个引用。当你从 `dataArray2` 中移除第一个对象，并随后打印两个数组对象的元素时，第一个元素（字符串 @"one"）从两个数组对象引用中都消失了，这并不令人意外。

接下来，你创建了 `dataArray` 的可变拷贝，并将生成的副本赋值给 `dataArray2`。这在内存中创建了两个不同的可变数组，它们都包含三个元素。现在，当你从 `dataArray2` 中移除第一个元素时，它不会对 `dataArray` 的内容产生影响，`dataArray` 的最后输出证实了这一点。

请注意，为对象创建可变拷贝并不要求被拷贝的对象本身是可变的。这同样适用于不可变拷贝：你可以为可变对象创建一个不可变拷贝。

## 浅拷贝与深拷贝

程序 18.1 用不可变字符串填充了 `dataArray`（记住，常量字符串对象是不可变的）。在程序 18.2 中，将用可变字符串填充它，这样你就可以更改数组中的一个字符串。查看程序 18.2，看看你是否理解它的输出。

### 程序 18.2

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray = [
            [NSMutableArray arrayWithObjects:
                [NSMutableString stringWithString:@"one"],
                [NSMutableString stringWithString:@"two"],
                [NSMutableString stringWithString:@"three"],
                nil
        ];
```

```objc
nil
];
NSMutableArray *dataArray2;
NSMutableString *mStr;

NSLog("@dataArray: %@");
for (NSString *elem in dataArray)
    NSLog("%@", elem);

// 拷贝一份，然后改变其中一个
// 字符串

dataArray2 = [dataArray mutableCopy];
mStr = [dataArray objectAtIndex: 0];
[mStr appendString: @"ONE"];

NSLog("@dataArray: %@");
for (NSString *elem in dataArray)
    NSLog("%@", elem);

NSLog("@dataArray2: %@");
for (NSString *elem in dataArray2)
    NSLog("%@", elem);
}
return 0;
}
```

### 程序 18.2 输出

dataArray:

one

two

three

```
dataArray:
  one
  two
  three
dataArray2:
  one
  two
  three
```

你通过以下语句获取了 `dataArray` 的第一个元素：

```objc
mStr = [dataArray objectAtIndexIndex: 0];
```

然后你通过这条语句向其添加了字符串 @"ONE"：

注意原始数组及其副本中第一个元素的值：两者都被修改了。也许你已经理解为什么 `dataArray` 的第一个元素被改变了，但不知道为什么它的副本也变了。当你从集合中获取一个元素时，获取的是该元素的新引用，而不是副本。因此，当在 `dataArray` 上调用 `objectAtIndex:` 方法时，返回的对象指向内存中与 `dataArray` 第一个元素相同的对象。正如你在输出所示，随后修改字符串 `mStr` 会产生一个改变 `dataArray` 第一个元素的副作用。

但你创建的副本呢？为什么它的第一个元素也变了？这归于拷贝默认情况下是浅拷贝。因此，当使用 `mutableCopy` 方法拷贝数组时，在内存中为新对象分配了空间，并将各个元素拷贝到新数组中。但将数组中的每个元素从原始位置拷贝到新位置，仅意味着将数组中一个元素的引用拷贝到另一个元素。最终结果是两个数组的元素都引用内存中相同的字符串。这与将一个对象赋值给另一个对象没有区别，我们在本章开头介绍过这一点。

要为数组的每个元素创建不同的副本，必须执行深拷贝。这意味着对数组中每个对象的内容进行拷贝，而不仅仅是对象引用的拷贝（并想想如果数组的元素本身是一个数组对象，这意味着什么）。但当你使用 Foundation 类的 `copy` 或 `mutable` 方法时，默认并不会执行深拷贝。在第 19 章“归档”中，我们将展示你如何使用 Foundation 的归档功能来创建对象的深拷贝。

例如，当你拷贝数组、字典或集合时，你得到的是这些集合的新副本。但是，如果你想修改一个集合但不拷贝另一个，你可能需要为单个元素创建自己的副本。例如，如果你想更改程序 18.2 中 `dataArray` 的第一个元素但不更改 `dataArray`，你可以创建一个新字符串（使用如 `stringWithString:` 等方法）并将其存储在 `dataArray2` 的第一个位置，如下：

```objc
mStr = [NSMutableString stringWithString:[dataArray2 objectAtIndex: 0]];
```

然后你就可以对 `mStr` 进行修改，并使用 `replaceObject:atIndex:withObject:` 方法将其添加到数组中，如下：

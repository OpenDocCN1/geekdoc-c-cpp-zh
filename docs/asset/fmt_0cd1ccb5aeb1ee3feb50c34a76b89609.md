
### 程序 7.4. 测试文件 main.m

```objc
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];
        [aFraction setTo: 1 over: 4]; // 将第一个分数设为 1/4
        [bFraction setTo: 1 over: 2];      // 将第二个分数设为 1/2
        [aFraction print];
        NSLog("@+");
        [bFraction print];
        NSLog("=");
        [aFraction add: bFraction];
        // 约简加法结果并打印
        [aFraction reduce];
        [aFraction print];
    }
return 0;
}
```

### 程序 7.4. 输出

1/4
+
1/2
=
3/4

这样好多了！

## self 关键字

在程序 7.4 中，我们决定在 `add:` 方法外部约简分数。我们也可以在 `add:` 内部这样做；这个决定完全是任意的。然而，我们如何识别要约简的分数呢？我们到底想要约简哪个分数？我们想要约简发送给 `add:` 消息的同一个分数。

我们知道如何直接通过名称识别方法内部的实例变量，但不知道如何识别消息的接收者。幸运的是，有一种方法可以。

你可以使用 `self` 关键字来指代当前消息的接收对象。如果你在 `add:` 方法内部写了

```
[self reduce];
```

那么 `reduce` 方法将应用于作为 `add:` 消息接收者的 `Fraction` 对象，这正是你所想要的。你将在整本书中看到 `self` 是多么有用。

```objc
- (void) print;
- (void) setTo: (int) n over: (int) d;
- (double) convertToNum;
- (Fraction *) add: (Fraction *) f;
- (void) reduce;
@end
```

你可能不需要处理分数，但这些示例向你展示了如何通过添加新方法来不断完善和扩展一个类。你可以将此接口文件交给另一个处理分数的同事，这对于那个人编写处理分数的程序来说足够了。如果那个人需要添加新方法，他可以直接通过扩展类定义来实现，也可以间接地通过定义他自己的子类并添加自己的新方法来实现。你将在下一章中学习如何这样做。

### 练习

+ 1. 为 `Fraction` 类添加以下方法，以完善分数的算术运算。在每个情况下，都在方法内部对结果进行约分：

```objc
// 从接收者中减去参数
-(Fraction *) subtract: (Fraction *) f;
// 将接收者乘以参数
-(Fraction *) multiply: (Fraction *) f;
// 将接收者除以参数
-(Fraction *) divide: (Fraction *) f;
```

2. 修改你 `Fraction` 类中的 `print` 方法，使其接受一个额外的 `BOOL` 参数，指示分数在显示时是否应该约分。如果需要约分（即参数为 `YES`），请确保不要对分数进行任何永久性更改。

3. 你的 `Fraction` 类可以处理负分数吗？例如，你可以加 -1/4 和 -1/2 并得到正确的结果吗？当你认为有了答案时，写一个测试程序来尝试一下。

4. 修改 `Fraction` 的 `print` 方法，将大于 1 的分数显示为带分数。例如，分数 5/3 应该显示为 1 2/3。

5. 第 4 章“数据类型与表达式”中的练习 6 定义了一个处理复数的新类 `Complex`。添加一个新方法 `add:`，可用于相两个复数。要加两个复数，你只需要将实部和虚部相加，如下：

(5.3 + 7i) + (2.7 + 4i) = 8 + 11i

让 `add:` 方法根据以下方法声明将结果存储并返回一个新的 `Complex` 数字：

```objc
- (Complex*) add: (Complex*) complexNum;
```

确保你在测试程序中处理了潜在的内存泄漏问题。

6. 给第 4 章练习 6 开发的 `Complex` 类以及本章练习 6 中的扩展，创建单独的 `Complex.h` 和 `Complex.m` 接口和实现文件。创建一个单独的测试程序来测试一切。

## 8. 继承

在本章中，你将学习使面向对象编程如此强大的关键原理之一。通过继承的概念，你将在现有的类定义的基础上进行构建，并为你自己的应用程序进行定制。

### 从根部开始

你在第 3 章“类、对象与方法”中学习了父类的概念。父类本身也可以有父类。没有父类的类位于层级结构的顶端，被称为**根类**（root class）。在 Objective-C 中，你有能力定义自己的根类，但通常你不会想这样做。相反，你将希望利用现有的类。我们到为止定义的所有类都是一个名为 `NSObject` 的根类的后代，你在接口文件中是这样指定它的：

```objc
@interface Fraction: NSObject
...
@end
```

`Fraction` 类派自 `NSObject` 类。因为 `NSObject` 位于层级结构的顶端（即上方没有其他类），所以它被称为根类，如图 8.1 所示。`Fraction` 类被称为子类（child/subclass）。

# 图 8.1. 根类与子类

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_243_0.png)

从术语的角度来看，我们可以谈论类、子类和父类。类似地，我们可以谈论类、子类和子类。你应该直接熟悉这两种术语。

每当定义一个新类（新根除外）时，该类都会继承某些内容。例如，父类的（非私有的）实例变量和方法会隐含地成为新类定义的一部分。这意味着子类可以访问这些方法和实例变量，就像它们是直接定义在类定义中一样。

注意，子类要直接访问的实例变量必须在接口部分声明，而不是像我们整本书中所做的那样在实现部分声明。在实现部分声明或合成的实例变量是私有实例变量，子类无法直接访问。相反，你将希望使用它们显式定义或合成的 getter/setter 方法来访问它们的值。

一个简单的例子（尽管是人为的）有助于说明继承这一核心概念。这里有一个对象 `ClassA` 的声明，它包含一个名为 `initVar` 的方法（注意这里我们在接口部分声明了实例变量 `x`，以便子类访问）。

```objc
@interface ClassA: NSObject
{
    int x;
}
```

```objc
- (void) initVar;
@end
```

`initVar` 方法简单地将 `ClassA` 实例变量的值设置为 100：

```objc
@implementation ClassA
-(void) initVar
{
    x = 100;
}
@end
```

现在让我们定义一个名为 `ClassB` 的类：

```objc
@interface ClassB: ClassA
-(void) printVar;
@end
```

声明的第一行

```objc
@interface ClassB: ClassA
```

表示 `ClassB` 不是 `NSObject` 的子类，而是 `ClassA` 的子类。尽管 `ClassA` 的父类（超类）是 `NSObject`，但 `ClassB` 的父类是 `ClassA`。图 8.2 说明了这一点。

# 图 8.2. 子类与父类

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_245_0.png)

从图 8.2 可以看到，根类没有父类，而位于层级底部的 `ClassB` 没有子类。因此，`ClassA` 是 `NSObject` 的子类。

## 程序 8.1. 输出

```
x = 100
```

你首先定义 `b` 为一个 `ClassB` 对象。在分配并初始化 `b` 后，你向它发送一个消息来应用 `initVar` 方法。但回看 `ClassB` 的定义，你会发现你从未定义过这样的方法。`initVar` 是定义在 `ClassA` 中的，由于 `ClassA` 是 `ClassB` 的父类，`ClassB` 可以使用 `ClassA` 的所有方法。因此对于 `ClassB` 而言，`initVar` 是一个继承的方法。

### 注意

到为止我们简单提到了它，但 `alloc` 和 `init` 是你一直使用的方法，它们从未在你的类中定义。这是因为你利用了它们继承自 `NSObject` 类的这一事实。

在向 `b` 发送 `initVar` 消息后，你调用 `printVar` 方法来显示实例变量 `x` 的值。`x = 100` 的输出确认了 `printVar` 能够访问该实例变量。这是因为与 `initVar` 方法一样，它也是继承来的。

记住，继承的概念会一直向下链式传递。因此，如果你定义了一个名为 `ClassC` 的新类，其父类为 `ClassB`，如下所示：

```
@interface ClassC: ClassB
...
@end
```

那么 `ClassC` 将继承 `ClassB` 的所有方法和实例变量，而 `ClassB` 又继承了 `ClassA` 的所有方法和实例变量，进而继承了 `NSObject` 的所有方法和实例变量。

务必理解，类的每个实例都有自己的实例变量，即使它们是继承来的。因此，一个 `ClassC` 对象和一个 `ClassB` 对象将拥有它们各自不同的实例变量。

## 寻找正确的方法

当你向对象发送消息时，你可能会好奇如何选择正确的方法应用到该对象。规则实际上非常简单。首先，检查对象所属的类，查看该类中是否显式定义了具有特定名称的方法。如果是，则使用该方法。如果没有定义，则检查父类。如果在该类中定义了方法，则使用该方法。如果没有，则继续搜索。

会一直检查父类，直到发生两种情况之一：要么你找到了包含指定方法的类，要么在回溯到根类后仍找到该方法。如果发生第一种情况，你就没好了；如果发生第二种情况，你就有问题了，并生成如下所示警告消息：

> warning: 'ClassB' may not respond to '-ity'

在这种情况下，你无意中尝试向一个类型为 `ClassB` 的变量发送名为 `ity` 的消息。编译器告诉你，该类的对象不知道如何响应此类方法。再次，这是在检查了 `ClassB` 的方法及其父类一直到根类的方法（在本例中是 `NSObject`）后确定的。

你将在第 9 章“多态、动态类型和动态绑定”中学习更多关于系统如何检查执行正确方法的知识。

## 通过继承进行扩展：添加新方法

继承通常用于扩展类。例如，假设你被分配了任务，开发一些类来处理矩形、圆形和三角形等 2D 图形对象。目前，我们只考虑矩形。回到第 4 章“数据类型和表达式”中的练习 7，从该示例的 `@interface` 部分开始：

```
@interface Rectangle: NSObject
@property int width, height;
-(int) area;
-(int) perimeter;
@end
```

你将合成这些值来设置矩形的宽度和高度并返回它们，以及你自己的方法来计算它的面积和周长。让我们添加一个方法，允许你通过同一个消息调用设置矩形的宽度和高度，如下：

```
-(void) setWidth:(int) w andHeight:(int) h;
```

假设你将这个新类的声明输入到名为 `Rectangle.h` 的文件中。其实现文件 `Rectangle.m` 可能如下所示：

```
@import "Rectangle.h"
@implementation Rectangle
@synthesize width, height;
-(void) setWidth:(int) w andHeight:(int) h
{
    width = w;
    height = h;
}
-(int) area
{
    return width * height;
}
-(int) perimeter
{
    return (width + height) * 2;
}
@end
```

每个方法的定义都足够简单。程序 8.2 显示了测试它的主程序。

## 程序 8.2

```
#import "Rectangle.h"
int main (int argc, char * argv[])
{
    @autoreleasepool {
        Rectangle *myRect = [[Rectangle alloc] init];
        [myRect setWidth:5 andHeight:8];
        NSLog ("Rectangle: w = %i, h = %i", myRect.width, myRect.height);
        NSLog(@"Area = %i, Perimeter = %i", [myRect area], [myRect perimeter]);
    }
  return 0;
}
```

## 程序 8.2 输出

Rectangle: w = 5, h = 8
Area = 40, Perimeter = 26

`myRect` 被分配并初始化；然后将其宽度设置为 5，高度设置为 8。第一行输出验证了这一点。接下来，通过适当的消息调用计算矩形的面积和周长，并将返回的值交给 `NSLog` 进行显示。

假设你现在需要处理正方形。你可以定义一个名为 `Square` 的新类，并在其中定义与 `Rectangle` 类类似的方法。或者，你可以意识到正方形只是特殊的矩形，其宽度和高度恰好相等。

因此，处理这种情况的一种简单方法是创建一个名为 `Square` 的新类，使其成为 `Rectangle` 的子类。目前，你可能想要添加的方法只有设置正方形边长为特定值以及获取该值。程序 8.3 显示了你新类 `Square` 的接口和实现文件。

## 程序 8.3. Square.h 接口文件

```
#import "Rectangle.h"
@interface Square: Rectangle
-(void) setSide:(int) s;
-(int) side;
@end
```

## 程序 8.3. Square.m 实现文件

```
#import "Square.h"
@implementation Square: Rectangle
-(void) setSide:(int) s
{
    [self setWidth: s andHeight: s];
}
-(int) side
{
    return self.width;
}
@end
```

# 程序 8.3. 测试程序

```objc
#import "Square.h"
#import <Foundation/Foundation.h>
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Square *mySquare = [[Square alloc] init];
        [mySquare setSide: 5];
        NSLog(@"Square s = %i", [mySquare side]);
        NSLog(@"Area = %i, Perimeter = %i", [mySquare area], [mySquare perimeter]);
    }
    return 0;
}
```

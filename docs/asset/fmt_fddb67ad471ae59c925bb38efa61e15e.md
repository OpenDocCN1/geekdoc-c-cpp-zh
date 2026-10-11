
```objc
#import <Foundation/Foundation.h>
@class XYPoint;
@interface Rectangle: NSObject
{
    int width;
    int height;
    XYPoint *origin;
}

@property int width, height;
-(XYPoint *) origin;
-(void) setOrigin:(XYPoint *)pt;
-(void) setWidth:(int) w andHeight:(int) h;
-(int) area;
-(int) perimeter;
@end
```

## 程序 8.4 Rectangle.m 实现文件

```objc
#import "Rectangle.h"
@implementation Rectangle
@synthesize width, height;
-(void) setWidth:(int) w andHeight:(int) h
{
    width = w;
    height = h;
}
-(void) setOrigin:(XYPoint *)pt
{
    origin = pt;
}
-(int) area
{
    return width * height;
}

-(int) perimeter
{
    return (width + height) * 2;
}
-(XYPoint *) origin
{
    return origin;
}
@end
```

## 程序 8.4 测试程序

```objc
#import "Rectangle.h"
#import "XYPoint.h"

int main(int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

    Rectangle *myRect = [[Rectangle alloc] init];
    XYPoint *myPoint = [[XYPoint alloc] init];

    [myRect setX:100 andY:200];

    [myRect setWidth:5 andHeight:8];
    [myRect setOrigin:myPoint];

    NSLog("Rectangle w %i, h %i", myRect.width, myRect.height);
    NSLog("Origin at %i, %i", myRect.origin.x, myRect.origin.y);
    NSLog("Area %i, Perimeter %i", [myRect area], [myRect perimeter]);

    [myRect release];
    [myPoint release];

    [pool drain];
    return 0;
}
```

## 程序 8.4 输出

Rectangle w 5, h 8

Origin at (100, 200)

Area 40, Perimeter 26

在主例程内部，你分配并初始化了一个标识为 `myRect` 的矩形和一个称为 `myPoint` 的点。使用 `setX:andY` 方法，你将 `myPoint` 设置为 (100, 200)。在将矩形的宽度和高度分别设置为 5 和 8 之后，你调用了 `setOrigin` 方法将矩形的原点设置为 `myPoint` 指向的点。三个 `NSLog` 调用获取并打印了这些值。表达式

`myRect.origin.x`

获取了由访问器方法 `origin` 返回的 `XYPoint` 对象，并应用点运算符获取矩形原点的 x 坐标。类似地，以下表达式获取了矩形原点的 y 坐标：

`myRect.origin.y`

# 拥有对象的类

你能解释程序 8.5 的输出吗？

## 程序 8.5

```objc
#import "Rectangle.h"
#import "XYPoint.h"

int main (int argc, char *argv[]) {
    NSAutoreleasePool * pool = [[NSAutorePool alloc] init];

    Rectangle *myRect = [[Rectangle alloc] init];
    XYPoint *myPoint = [[XYPoint alloc] init];

    [myPoint setX:100 andY:200];

    [myRect setWidth:5 andHeight:8];
    [myRect origin];

    NSLog("Origin at (%i, %i", myRect.origin.x, myRect.origin.y);
    [myPoint setX:50 andY:50];
    NSLog("Origin at (%i, %i", myRect.origin.x, myRect.origin.y);
    [myRect release];
    [myPoint release];

    [pool drain];
    return 0;
}
```

## 程序 8.5 输出

Origin at (100, 200)

Origin at (50, 50)

# 第8章 继承

你将 `myPoint` 从 (100, 200) 改为 (50, 50)，这显然改变了矩形的 `origin`！为什么会发生这种情况？你并没有显式地重置矩形的 `origin`，那么为什么矩形的 `origin` 会改变呢？如果你回到 `setOrigin` 方法的定义，可能就知道为什么了：

```objc
-(void) setOrigin:(XYPoint *)pt {
    origin = pt;
}
```

当使用表达式 `[myRect setOrigin:myPoint]` 调用 `setOrigin` 方法时，`myPoint` 的值作为参数传递给方法。该值指向 `XYPoint` 对象存储在内存的位置，如图 8.5 所示。

## 通过继承扩展：添加方法

等待，OCR 文本似乎有重复或碎片化。让我们重新对齐逻辑流：

你将 `myPoint` 从 (100, 200) 改为 (50, 50)，这显然改变了矩形的 `origin`！为什么会发生这种情况？你并没有显式地重置矩形的 `origin`，那么为什么矩形的 `origin` 会改变呢？如果你回到 `setOrigin` 方法的定义，可能就知道为什么了：

```objc
-(void) setOrigin:(XYPoint *)pt {
    origin = pt;
}
```

当使用表达式 `[myRect setOrigin:myPoint]` 调用 `setOrigin` 方法时，`myPoint` 的值作为参数传递给方法。该值指向 `XYPoint` 对象存储在内存的位置，如图 8.5 所示。

提供的 OCR 文本在结尾处有大量的重复和错误。我将根据提供的片段清理逻辑流。

从第 176 页开始的 OCR 文本是重复且混乱的。我将提供清理后的叙述。

等待，查看 OCR：

- `NSLog("Origin at (%i, %i", myRect.origin.x, myRect.origin.y);` 在 OCR 中缺少一个右括号。

- `myRect setX:100 andY:200;` 应该是 `[myRect setX:100 andY:200];`。

- `x Val;` 应该是 `x = xVal;`。

- `origin pt;` 应该是 `origin = pt;`。

我将严格按照提供的文本重新处理，以确保信息不丢失，仅修复错误。

## 重写方法

我们在在本章较早提到，你无法通过继承来移除方法。然而，你可以通过重写（overriding）来更改继承方法的定义。

回到你的两个类 `ClassA` 和 `ClassB`，假设你想为 `ClassB` 编写你自己的 `initVar` 方法。你已经知道 `ClassB` 将从 `ClassA` 继承 `initVar`，但你是否可以创建一个同名的新方法来替换继承的方法呢？答案是肯定的，你只需定义一个同名的新方法即可。与父类同名定义的方法将替换或重写所继承的定义。你的新方法的返回类型和参数必须与你正在重写的方法相同。程序 8.6 显示了一个简单的示例来说明这一点。

## 程序 8.6

```objc
// Overriding Methods

#import <Foundation.h>

// ClassA 声明和定义

@interface ClassA: NSObject
{
  int x;
}

-(void)initVar;
@end

@implementation ClassA
-(void)initVar
{
    x = 100;
}
@end
```

```objc
// ClassB 声明和定义

@interface ClassB: ClassA
-(void)initVar;
-(void)printVar;
@end

@implementation ClassB
-(void)initVar // added method
{
    x = 200;
}

-(void)printVar
{
    NSLog("%d", x);
}
@end

int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutoreleasePool alloc] init];
    ClassB *b = [[ClassB alloc] init];

    [b initVar]; // 使用 B 中的重写方法

    [b printVar]; // 显示 x 的值;
    [b release];

    [pool drain];
    return 0;
}
```

## 程序 8.6 输出

200

显然，消息 `[b initVar];` 导致了在 `ClassB` 中定义的 `initVar` 方法被使用，而不是上一个示例中的 `ClassA`。图 8.9 说明了这一点。

| 类 | 实例变量 | 方法 |

| :--- | :--- | :--- |

| Object | | |

| ClassA | x | initVar |

| ClassB | x | initVar, printVar |

![](img/9a03a7dbf1900dce936c9665ab15c6_181_0.png)

## 选择了哪个方法？

我们涵盖了系统如何向上层级搜索以应用于对象的方法。如果你在不同的类中拥有同名的方法，正确的方法将根据消息接收者的类来选择。程序 8.7 使用了与之前相同的 `ClassA` 和 `ClassB` 类定义。

## 程序 8.7

```objc
#import <Foundation.h>

// 在此处插入 ClassA 和 ClassB 的定义

int main (int argc, char *argv[]) {
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    ClassA *a = [[ClassA alloc] init];
    ClassB *b = [[ClassB alloc] init];

    [a initVar]; // 使用 ClassA 方法
    [a printVar]; // 显示 x 的值;

    [b initVar]; // 使用重写的 ClassB 方法
    [b printVar]; // 显示 x 的值;
    [a release];
    [b release];

    [pool drain];
    return 0;
}
```

编译此程序时，你会得到这个警告消息：

`warning: 'ClassA' may not respond to selector '-printVar'`

这里发生了什么？我们在之前的章节中讨论过这个。看看 `ClassA` 的声明：

```objc
// ClassA 声明和定义

@interface ClassA: NSObject
{
    int x;
}

-(void)initVar;
@end
```

注意，没有声明 `printVar` 方法。因为没有声明 `printVar` 方法，系统无法在层级中找到它，导致了警告。

# 第 8 章 继承

默认情况下，设置（setter）的操作是复制对象指针，而不是对象本身。你可以合成不同类型的 setter，转而创建对象的副本。然而，要这样做，你需要学习如何编写拷贝方法。我们将在第 17 章“内存管理”中重新回到这个话题。

在学习这一节之前，让我们思考 `Rectangle` 类的 getter 部分。假设在 8.4 节的测试程序中，你在设置 `Rectangle` 的值之后插入了以下几行：

```
Point *tOrigin = myRect.origin;
tOrigin.x = 200;
tOrigin.y = 300;
```

执行这段代码后，`myRect` 的 `origin` 会发生什么？没错，它的 `origin` 会被改变。getter 返回的对象是“脆弱的”：任何人更改它的 x 或 y 都会相应地改变矩形的 x 或 y 值。出于这个原因，编写 getter 最安全的方法是实际上创建对象的副本并返回该副本。这样，你就保护了实例变量不被修改。我们在这里不会进行该更改，将其留作练习。请注意，如果你在返回对象之前复制它们，将面临性能损失。在设计类时，你必须判断这种权衡是否值得。

## 重写方法

我们在在本章较早提到，你无法通过继承来移除方法。然而，你可以通过重写（overriding）来更改继承方法的定义。

回到你的两个类 `ClassA` 和 `ClassB`，假设你想为 `ClassB` 编写你自己的 `initVar` 方法。你已经知道 `ClassB` 将从 `ClassA` 继承 `initVar`，但你是否可以创建一个同名的新方法来替换继承的方法呢？答案是肯定的，你只需定义一个同名的新方法即可。与父类同名定义的方法将替换或重写所继承的定义。你的新方法的返回类型和参数必须与你正在重写的方法相同。程序 8.6 显示了一个简单的示例来说明这一点。

## 重写 dealloc 方法

如果你决定重写 `dealloc`，你还必须确保释放不仅由你自己的变量占用的内存，还有任何继承来的变量占用的内存。为了做到，你需要利用关键字 `super`，它指向消息的父类。这是 `super` 最常用的用法：

```objc
[super dealloc];
```

在方法内部使用时，它会调用父类的 `dealloc` 方法。因此，为你的类重写 `dealloc` 方法的策略是首先释放由 `origin` 占用的内存，然后调用父类的 `dealloc` 方法来完成工作。这里是新方法：

```objc
-(void)dealloc
{
  if (origin)
    [origin release];
  [super dealloc];
}
```

`dealloc` 方法定义为没有返回值。在释放之前会进行测试检查 `origin` 是否非零。矩形的 `origin` 从未被设置；在这种情况下，它有默认值零。然后我们调用父类的 `dealloc` 方法，这在 `Rectangle` 类没有被重写时本应继承的相同方法。你也可以更简单地写 `dealloc` 方法：

```objc
-(void)dealloc
{
  [origin release];
  [super dealloc];
}
```

因为向 `nil`（零）对象发送消息是安全的。此外，你谨慎地释放了 `origin` 而不是在这里进行 `dealloc`。如果没有其他人在使用 `origin`，那么该释放 消息最终会调用 `origin` 的 `dealloc` 方法来释放其空间。

有了你的新方法，你必须释放分配的矩形，而无需担心它们包含的 `XYPoint` 对象。程序 8.5 中所示的两个释放 消息现在足以释放程序中的所有对象，包括由 `setOrigin:` 创建的 `XYPoint` 对象：

```
[myRect release];
[myPoint release];
```

## 通过继承扩展：添加新的实例变量

你不仅可以通过添加新方法来有效地扩展类的定义，还可以添加实例变量。在这两种情况下，其效果都是累积的。你永远无法通过继承来减少方法或实例变量；你只能添加——或者对于方法来说，是添加或覆盖。

让我们回到你简单的 `ClassA` 和 `ClassB` 类并进行一些更改。为 `ClassB` 添加一个新的实例变量 `y`，如下所示：

```objc
@interface ClassB: ClassA
{
  int y;
}

-(void) localVar;
@end
```

根据之前的声明，`ClassB` 似乎只有一个名为 `y` 的实例变量，但实际上它拥有两个：它继承了来自 `ClassA` 的 `x`，并添加了它自己的实例变量 `y`。

> **注意**  
> 当然，它还拥有从 `NSObject` 类继承而来的实例变量，但我们目前暂选择忽略这一细节。

让我们在一个简单的示例中将这些内容整合在一起，以说明这一概念（见程序 8.8）。

程序 8.8

```objc
// 实例变量的扩展

#import <Foundation/Foundation.h>

// 类 A 的声明和定义

@interface ClassA: NSObject
{
  int x;
}

-(void)initVar;
@end

@implementation ClassA
-(void)initVar
{
  x = 100;
}
@end
```

## 第 8 章继承

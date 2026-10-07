
# 第8章 继承

它知道 origin 是一个来自 XYPoint 类的对象。这就是编译器在这一点需要知道的全部。
让我们为你的新 XYPoint 类和 Rectangle 方法填充空白，这样你就可以程序中测试一切了。首先，程序 8.4 显示了你的 XYPoint 类的实现文件。
程序 8.4 显示了 Rectangle 类的新方法。

# 程序 8.4 Rectangle.m 添加的方法

```objc
#import "XYPoint.h"

-(void) setOrigin:(XYPoint *)pt
{
  origin = pt;
}

-(XYPoint *) origin
{
  return origin;
}
```

以下是完整的 XYPoint 和 Rectangle 类定义，随后是一个用于尝试它们的测试程序。

# 程序 8.4 XYPoint.h 接口文件

```objc
#import <Foundation/Foundation.h>

@interface XYPoint: NSObject
{
  int x;
  int y;
}

@property int x, y;

-(void) setX:(int)xVal andY:(int)yVal;
@end
```

# 程序 8.4 XYPoint.m 实现文件

```objc
#import "XYPoint.h"

@implementation XYPoint

@synthesize x, y;

-(void) setX:(int)xVal andY:(int)yVal
{
    x = xVal;
    y = yVal;
}
@end
```

# 程序 8.4 Rectangle.h 接口文件

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

# 程序 8.4 Rectangle.m 实现文件

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

# 程序 8.4 测试程序

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

# 程序 8.4 输出

Rectangle w 5, h 8
Origin at (100, 200)
Area 40, Perimeter 26

在主例程内部，你分配并初始化了一个标识为 myRect 的矩形和一个称为 myPoint 的点。使用 `setX:andY` 方法，你将 myPoint 设置为 (100, 200)。在将矩形的宽度和高度分别设置为 5 和 8 之后，你调用了 `setOrigin` 方法将矩形的原点设置为 myPoint 指向的点。三个 `NSLog` 调用获取并打印了这些值。表达式

`myRect.origin.x`

获取了由访问器方法 `origin` 返回的 `XYPoint` 对象，并应用点运算符获取矩形原点的 x 坐标。类似地，以下表达式获取了矩形原点的 y 坐标：

`myRect.origin.y`

# 拥有对象的类

你能解释程序 8.5 的输出吗？

# 程序 8.5

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

# 程序 8.5 输出

Origin at (100, 200)
Origin at (50, 50)

# 第8章 继承

你将 myPoint 从 (100, 200) 改为 (50, 50)，这显然改变了矩形的 origin！为什么会发生这种情况？你并没有显式地重置矩形的 origin，那么为什么矩形的 origin 会改变呢？如果你回到 `setOrigin` 方法的定义，可能就知道为什么了：

```objc
-(void) setOrigin:(XYPoint *)pt {
    origin = pt;
}
```

当使用表达式 `[myRect setOrigin:myPoint]` 调用 `setOrigin` 方法时，myPoint 的值作为参数传递给方法。该值指向 XYPoint 对象存储在内存的位置，如图 8.5 所示。

# 通过继承扩展：添加方法

等待，OCR 文本似乎有重复或碎片化。让我们重新对齐逻辑流：

你将 myPoint 从 (100, 200) 改为 (50, 50)，这显然改变了矩形的 origin！为什么会发生这种情况？你并没有显式地重置矩形的 origin，那么为什么矩形的 origin 会改变呢？如果你回到 `setOrigin` 方法的定义，可能就知道为什么了：

```objc
-(void) setOrigin:(XYPoint *)pt {
    origin = pt;
}
```

当使用表达式 `[myRect setOrigin:myPoint]` 调用 `setOrigin` 方法时，myPoint 的值作为参数传递给方法。该值指向 XYPoint 对象存储在内存的位置，如图 8.5 所示。

提供的 OCR 文本在结尾处有大量的重复和错误。我将根据提供的片段清理逻辑流。

从第 176 页开始的 OCR 文本是重复且混乱的。我将提供清理后的叙述。

等待，查看 OCR：
- `NSLog("Origin at (%i, %i", myRect.origin.x, myRect.origin.y);` 在 OCR 中缺少一个右括号。
- `myRect setX:100 andY:200;` 应该是 `[myRect setX:100 andY:200];`。
- `x Val;` 应该是 `x = xVal;`。
- `origin pt;` 应该是 `origin = pt;`。

我将严格按照提供的文本重新处理，以确保信息不丢失，仅修复错误。

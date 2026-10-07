
# 第8章 继承

在这种情况下，你无意中尝试向一个类型为 `ClassB` 的变量发送一个名为 `init` 的消息。编译器告诉你，该类的对象不知道如何响应该方法。再次，这是在检查了 `ClassB` 的方法及其追溯到根类（在本例中为 `NSObject`）的父类方法后确定的。你将在第9章“多态、动态类型和动态绑定”中学习更多关于系统如何检查要执行正确方法的知识。

# 通过继承进行扩展：添加新方法

继承通常用于扩展类。例如，假设你被分配了一项任务，开发一些用于处理 2D 图形对象（如矩形、圆形和三角形）的类。目前，我们只需关心矩形。让我们回到第4章“数据类型与表达式”中的练习 7，并从该示例的 `@interface` 部分开始：

```objc
@interface Rectangle: NSObject
{
int width;
int height;
}
```

```objc
@property int width, height;
(-int) area;
(-int) perimeter;
@end
```

你将合成方法来设置矩形的宽度和高度并返回这些值，以及你自己的方法来计算它的面积和周长。让我们添加一个方法，允许通过相同的消息调用设置矩形的宽度和高度，如下：
-(void) setWidth:(int) w andHeight:(int) h;

```objc
@implementation Rectangle
@synthesize width, height;
-(void) setWidth:(int) w andHeight:(int) h
{
width = w;
height = h;
}
```

```objc
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

每个方法的定义都足够简单。程序 8.2 显示了一个测试它的主程序。

```objc
int main(int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    Rectangle *myRect = [[Rectangle alloc] init];
    [myRect setWidth:5 andHeight:8];
    NSLog("@Rectangle %s w %i", myRect.width, myRect.height);
    NSLog("@Area %i, Perimeter %i", [myRect perimeter]);
    [myRect release];
    [pool drain];
    return 0;
}
```

# 程序 8.2 输出

Rectangle: w 5, h 8
Area 40, Perimeter 26

myRect 被分配并初始化；然后将其宽度设置为 5，高度设置为 8。输出的第一行显示了这一点。接下来，通过适当的调用计算了矩形的面积和周长，并将返回的值交给 `NSLog` 显示。

假设你现在需要处理正方形。你可以定义一个新类 `Square`，并定义与你的 `Rectangle` 类中类似的方法。或者，你可以意识到正方形是矩形的一种特殊情况，其宽度和高度恰好相等。

因此，处理这种情况情况的简单方法是创建一个名为 `Square` 的新类，并作为 `Rectangle` 的子类。这样，你可以使用 `Rectangle` 的所有方法和变量，还可以定义你自己的。目前，你可能想要添加的方法方法是将正方形的边长设置为特定值并获取该值。程序 8.3 显示了你新 `Square` 类的接口文件和实现文件。

# 程序 8.3 Square.h 接口文件

```objc
#import "Rectangle.h"
@interface Square: Rectangle

-(void) setSide:(int) s;
(-int) side;
end
```

# 程序 8.3 Square.m 实现文件

```objc
#import "Square.h"
@implementation Square: Rectangle

-(void) setSide:(int) s {
    [self setWidth:s andHeight:s];
}
-(int) side {
    return width;
}
end
```

注意你在这里的操作。你将 `Square` 类定义为 `Rectangle` 的子类，这在头文件 `Rectangle.h` 中声明。你不需要在这里添加实例变量，但你添加了名为 `setSide:` 和 `side` 的新方法。
正方形只有一条边，但你在内部将其表示为两个数字——这没关系。所有这些对于 `Square` 类的用户都是隐藏的。如果有必要，你以后可以完善你的 `Square` 类；该类的任何用户都不需要担心之前讨论的数据封装的内部细节。
`setSide` 方法利用了你已经继承 `Rectangle` 类这一事实来设置矩形的宽度和高度值。因此，`setSide` 调用了 `Rectangle` 类中的 `setWidthAndHeight:` 方法，将参数 `s` 传递作为宽度和高度的值。你实际上不需要做其他任何操作。处理正方形对象的人现在可以使用 `setSide` 设置正方形的尺寸，并利用来自 `Rectangle` 类的方法来计算正方形的面积、周长等。程序 8.3 显示了你新 `Square` 类的测试程序和输出。

# 程序 8.3 测试程序

```objc
#import "Square.h"
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

    Square *mySquare = [[Square alloc] init];

    [mySquare setSide:5];

    NSLog("@Square %i w %i", [mySquare side], [mySquare side]);
    NSLog("@Area %i, Perimeter %i", [mySquare area], [mySquare perimeter]);
    [mySquare release];
    [pool drain];
    return 0;
}
```
输出：

Square 5 w 5
Area 25, Perimeter 20

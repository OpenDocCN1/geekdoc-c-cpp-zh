

## 程序 8.1. 输出

```
x = 100
```

你首先定义 `b` 为一个 `ClassB` 对象。在分配并初始化 `b` 后，你向它发送一个消息来应用 `initVar` 方法。但回看 `ClassB` 的定义，你会发现你从未定义过这样的方法。`initVar` 是定义在 `ClassA` 中的，由于 `ClassA` 是 `ClassB` 的父类，`ClassB` 可以使用 `ClassA` 的所有方法。因此对于 `ClassB` 而言，`initVar` 是一个继承的方法。

## 注意

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

myRect 被分配并初始化；然后将其宽度设置为 5，高度设置为 8。第一行输出验证了这一点。接下来，通过适当的消息调用计算矩形的面积和周长，并将返回的值交给 `NSLog` 进行显示。

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


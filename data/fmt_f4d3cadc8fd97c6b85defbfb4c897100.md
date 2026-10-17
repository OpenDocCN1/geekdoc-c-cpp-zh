
现在我们可以讨论实际示例了。首先，`a` 和 `b` 分别定义为 `ClassA` 和 `ClassB` 对象。在分配和初始化后，向它们发送消息，请求其执行 `initVar` 方法。该方法定义在 `ClassA` 的定义中，因此选择了该方法。该方法简单地将实例变量 `x` 的值设置为 `100` 并返回。接着调用你刚刚添加到 `ClassA` 的 `printVar` 方法来显示 `x` 的值。

与 `ClassA` 对象一样，`ClassB` 对象 `b` 也被分配和初始化，其实例变量 `x` 被设置为 `200`，最后显示了它的值。

请确保你理解如何根据 `a` 和 `b` 所属的类为它们选择正确的方法。这是 Objective-C 面向对象编程的基础概念。

作为一个练习，考虑从 `ClassB` 中移除 `printVar` 方法。这样做可行吗？为什么可行或不可行？

在定义子类时，你不仅可以添加新方法来有效扩展类的定义，还可以添加新的实例变量。在这两种情况下，效果都是累积的。你永远无法通过继承来减少方法或实例变量；你只能添加——或者对于方法，是添加或覆盖。

所以，回顾一下，你为什么要创建一个子类？这里有三个原因：

- 1. 你想扩展类的功能，也许通过添加新方法和/或实例变量。
- 2. 你想创建一个类的特殊化版本（例如，某种类型的图形对象）。
- 3. 你需要通过覆盖一个或多个方法来更改类的默认行为。

### Abstract类（Abstract Classes）

没有什么比用一些术语来结束这一章更好的方法了？我们在这里引入它是因为它与继承的概念直接相关。

有时创建类仅仅是为了让某人更容易创建子类。出于原因，这些类被称为抽象类（abstract classes），或者等价的抽象父类（abstract superclasses）。方法和实例变量定义在类中，但并不期望有人实际上从该类创建实例。例如，考虑根对象 `NSObject`。你能想出从该类中定义一个对象的任何用途吗？

在第二部分“Foundation 框架”中介绍的 Foundation 框架有几个所谓的抽象类。例如，Foundation 的 `NSNumber` 类就是一个抽象类，它是为了将数字作为对象来处理而创建的。整数和浮点数通常有不同的存储要求。每种数值类型都有独立的 `NSNumber` 子类。因为这些子类与它们的抽象父类不同，它们是真实存在的，因此被称为具体子类（concrete subclasses）。每个具体子类都属于 `NSNumber` 类，并统称为一个簇（cluster）。当你向 `NSNumber` 类发送消息创建一个新的整数对象时，会使用相应的子类为整数对象分配必要的存储空间并恰当地设置其值。这些子类实际上是私有的。你并不会直接访问它们；而是通过抽象父类间接访问它们。抽象父类为处理所有类型的数字对象提供了一个公共接口，减轻了你必须知道数字对象中存储了何种类型数字以及如何设置和检索其值的负担。

诚然，这段讨论可能看起来有点“抽象”（抱歉！）；请不用担心——在这里只需掌握该概念就足够了。

### 练习（Exercises）

- 1. 在程序 8.1 中添加一个名为 `ClassC` 的新类，它是 `ClassB` 的子类。编写一个 `initVar` 方法，将其实例变量 `x` 的值设置为 `300`。编写一个测试例程，声明 `ClassA`、`ClassB` 和 `ClassC` 对象并调用它们对应的 `initVar` 方法。
- 2. 在处理高分辨率设备时，你可能需要使用一种坐标系，允许你将点指定为浮点值而不是简单的整数（iOS 使用一个名为 `CGRect` 的结构来处理矩形）。修改本章中的 `XYPoint` 和 `Rectangle` 类以处理浮点数。矩形的宽度和面积也应该支持浮点数。
- 3. 在程序 8.1 中添加一个名为 `Class2` 的新类，它像 `ClassB` 一样是 `ClassA` 的子类。`ClassB` 和 `Class2` 之间是什么关系？识别 `NSObject` 类、`ClassA`、`ClassB` 和 `Class2` 之间的层次关系。`ClassB` 的父类是什么？`Class2` 的父类是什么？一个类可以有多少个子类？它可以有多少个父类？
- 4. 为 `Rectangle` 类编写一个 `translate:` 方法，它接收一个 `XYPoint` 对象作为参数。让它根据指定的向量平移矩形。注意：平移意味着从一个地方移动到另一个地方。
- 5. 定义一个新类 `GraphicObject`，使其继承 `NSObject`。在新类中定义变量如下：

```objc
int    fillColor;   // 32位颜色
BOOL   filled;      // 对象是否填充？
int    lineColor;   // 32位线条
```

编写方法来设置和检索之前定义的变量。让 `Rectangle` 类成为 `GraphicObject` 的子类。定义 `GraphicObject` 的子类 `Circle` 和 `Triangle`。编写方法来设置和检索这些对象的各种参数，以及计算圆的周长和面积，三角形的周加上面积。
- 6. 为 `Rectangle` 类编写一个 `containsPoint:` 方法，接收一个 `XYPoint` 对象作为参数：

```objc
-(BOOL) containsPoint: (XYPoint *) aPoint;
```

如果矩形包含指定的点，则该方法返回 `BOOL` `YES`，否则返回 `NO`。
- 7. 为 `Rectangle` 类编写一个 `intersect:` 方法，接收一个矩形作为参数并返回表示两个矩形重叠区域矩形。例如，给定图 8.10所示所示的矩形，该方法应该返回一个起点为 `(400, 420)`、宽度为 `50`、高度为 `60` 的矩形。如果矩形不相交，返回一个宽度和高度为零且起点为 `(0,0)` 的矩形。
- 8. 为 `Rectangle` 类编写一个 `draw` 方法，使用连字符和竖线画矩形。以下代码序列

```objc
Rectangle *myRect = [[Rectangle alloc] init];
myRect setWidth: 10 andHeight: 3;
myRect draw;
```

将产生以下输出：

```
|   |
|   |
|   |
|   |
|   |
------
```

### 注意

你应该使用 `printf` 来打印你的字符，因为 `NSLog` 在每次调用时都会显示新行。

# 9. 多态、动态类型和动态绑定

在本章中，你将学习 Objective-C 语言的某些特性，这些特性使其成为一种强大的编程语言，并将其区别于 C++ 等其他面向对象的编程语言。本章描述了三个核心概念：多态、动态类型和动态绑定。多态允许在开发程序时，使得不同类的对象可以定义方法。动态类型将对象所属类的确定推迟到程序执行时。动态绑定则将在对象上调用的实际方法的确定推迟到程序运行时间。

### 多态：相同名，不同类

程序 9.1 显示了名为 `Complex` 的类的接口文件，它用于在程序中表示复数。

# 程序 9.1. 接口文件 Complex.h

```objc
// Complex 类的接口文件
#import <Foundation/Foundation.h>
@interface Complex: NSObject
@property double real, imaginary;
-(void) print;
-(void) setReal:(double)a andImaginary:(double) b;
-(Complex *) add: (Complex *) f;
@end
```

你应该已经从第 7 章“关于类的更多内容”的练习 5 和 6 中完成了该类的实现部分。我们添加了一个额外的 `setReal:andImaginary:` 方法，以便你通过一条消息同时设置数的实部和虚部，并合成了访问器方法。如下所示。

# 程序 9.1. 实现文件 Complex.m

```objc
// Complex 类的实现文件
#import "Complex.h"
@implementation Complex
@synthesize real, imaginary;
-(void) print
{
    NSLog("%g + %gi", real, imaginary);
}
-(void) setReal: (double) a andImaginary:(double) b
{
    real = a;
    imaginary = b;
}
-(Complex *) add: (Complex *) f
{
    Complex *result = [[Complex alloc] init];
    result.real = real + f.real;
    result.imaginary = imaginary + f.imaginary;
    return result;
}
@end
```

# 程序 9.1. 测试程序 main.m

```objc
// 共享方法名：多态
#import "Fraction.h"
#import "Complex.h"
int main(int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *f1 = [[Fraction alloc] init];
        Fraction *f2 = [[Fraction alloc] init];
        Fraction *fracResult;
        Complex *c1 = [[Complex alloc] init];
        Complex *c2 = [[Complex alloc] init];
        Complex *compResult;
        [f1 setTo: 1 over: 10];
        [f2 setTo: 2 over: 15];
        [c1 setReal: 18.0 andImaginary: 2.5];
        [c2 setReal: -5.0 andImaginary: 3.2];
        // 相加并打印两个复数
        [c1 print]; NSLog("+"); [c2 print];
        NSLog("-------");
        compResult = [c1 add: c2];
        [compResult print];
        NSLog("\n");
        // 相加并打印两个分数
        [f1 print]; NSLog("+"); [f2 print];
        NSLog("-------");
        fracResult = [f1 add: f2];
        [fracResult print];
    }
    return 0;
}
```

# 程序 9.1. 输出

```
18 + 2.5i
+
-5 + 3.2i
------
13 + 5.7i

1/10
+
2/15
----
7/30
```

注意，`Fraction` 和 `Complex` 类都包含 `add:` 和 `print` 方法。因此，当执行消息表达式时

```
compResult = [c1 add: c2];
[compResult print];
```

系统如何知道执行哪些方法？很简单：Objective-C 运行时知道 `c1`（第一条消息的接收者）是一个 `Complex` 对象。因此，它选择了为 `Complex` 类定义的 `add` 方法。

Objective-C 运行时系统还确定 `compResult` 是一个 `Complex` 对象，因此它选择了 `Complex` 类中定义的 `print` 方法来显示加法结果。同样的讨论也适用于以下消息表达式：

```
fracResult = [f1 add: f2];
[fracResult print];
```

### 注意

正如第 13 章“底层 C 语言特性”中更完整描述的那样，系统始终携带关于对象所属类的信息。这使得它能够在运行时而不是编译时做出这些关键决策。

根据 `f1` 和 `fracResult` 的类，选择了 `Fraction` 类中对应的方法来求值消息表达式。

如提到的，在不同类之间共享相同方法名的能力被称为多态。多态允许你开发一组类，每个类都可以响应相同的方法名。每个类的定义都封装了响应该特定方法所需的代码，这使得它与其它类的定义保持保持独立。这还允许你稍后添加可以响应具有相同名称方法的类类。

### 动态绑定和 id 类型

第 4 章简要提到了 `id` 数据类型，并指出它是一个泛型对象类型。也就是说，`id` 可以用于存储属于任何类的对象。这种数据类型的真正威力是在程序执行期间用它在变量中存储不同类型的对象时。研究程序 9.2 及其相关输出。

# 程序 9.2. 测试程序 main.m

```objc
// 演示动态类型和绑定
#import "Fraction.h"
#import "Complex.h"
int main (int argc, char * argv[])
{
    autoreleasepool {
        id dataValue;
        Fraction *f1 = [[Fraction alloc] init];
        Complex *c1 = [[Complex alloc] init];
        [f1 setTo: 2 over: 5];
        [c1 setReal: 10.0 and Imaginary: 2.5];
        // dataValue 首先获得一个分数
        dataValue = f1;
        [dataValue print];
        // 现在 dataValue 获得一个复数
        dataValue = c1;
        [dataValue print];
    }
    return 0;
}
```

# 程序 9.2. 输出

```
2/5
10 + 2.5i
```

变量 `dataValue` 被声明为 `id` 对象类型。因此，`dataValue` 可以用于持有程序中的任何类型的对象。注意声明行中没有星号：

`id dataValue;`

`Fraction f1` 被设置为 `2/5`，复数 `c1` 被设置为 `(10 + 2.5i)`。赋值操作

`dataValue = f1;`

将 `Fraction f1` 存储在 `dataValue` 中。现在，你可以对 `dataValue` 做什么？嗯，你可以在 `dataValue` 上调用任何你可以在 `Fraction` 对象上使用的方法，尽管 `dataValue` 的类型是 `id` 而不是 `Fraction`。但如果 `dataValue` 可以存储任何类型的对象，系统是如何知道要调用哪个方法的呢？也就是说，当它遇到消息表达式时

```
[dataValue print];
```

它如何知道调用哪个 `print` 方法？你为 `Fraction` 和 `Complex` 类都定义了 `print` 方法。

如之前所述，答案在于 Objective-C 系统始终跟踪对象所属的类。它也在于动态类型和动态绑定的概念——也就是说，系统在运行时而不是编译时动态地做出关于对象的类以及因此调用哪个方法的决策。

所以，程序执行期间，在系统向 `dataValue` 发送 `print` 消息之前，它首先检查存储在 `dataValue` 内部对象的类。在程序 9.2 的第一个情况下，该变量包含一个 `Fraction` 对象，因此使用了 `Fraction` 类中定义的 `print` 方法。这通过程序的输出验证了这一点。

在第二种情况下，发生了相同的事情。首先，将复数 `c1` 赋值给 `dataValue`。接下来，执行以下消息表达式：

```
[dataValue print];
```

这一次，因为 `dataValue` 包含一个属于 `Complex` 对象，因此选择了该类中对应的 `print` 方法进行执行。

这是一个简单的例子，但你可以将这一概念推广到更复杂的应用程序中。与多态结合，动态绑定和动态类型允许你轻松地编写代码，向不同类的对象发送相同的消息。

例如，考虑一个可以用于在屏幕上绘制图形对象的 `draw` 方法。你可能为你的每个图形对象定义了不同的 `draw` 方法，例如文本、圆形、矩形、窗口等。如果要绘制的特定对象

绘制的内容存储在一个名为 `currentObject` 的 `id` 变量中，例如，你只需通过发送 `draw` 消息将其绘制在屏幕上：

```
[currentObject draw];
```

你甚至可以先进行测试，以确保 `currentObject` 中存储的对象实际上响应 `draw` 方法。你将在本章稍后的“询问关于类的问题”章节中学习如何操作。

# 编译时检查与运行时检查

由于存储在 `id` 变量中的对象类型在编译时是不确定的，某些测试会被推迟到运行时——即程序执行期间。

考虑以下代码序列：

```objc
Fraction *f1 = [[Fraction alloc] init];
[f1 setReal: 10.0 andImaginary: 2.5];
```

由于 `setReal:andImaginary:` 方法适用于复数而不是分数，因此在你编译包含该行的程序时，会抛出以下消息：

```
'Fraction' may not respond to 'setReal:andImaginary:'
```

Objective-C 编译器知道 `f1` 是一个 `Fraction` 对象，因为它是这样声明的。它还知道当看到以下消息表达式时

```
[f1 setReal: 10.0 andImaginary: 2.5];
```

`Fraction` 类没有 `setReal:andImaginary:` 方法（也没有继承该方法）。因此，它发出了之前所示的警告消息。

现在考虑以下代码序列：

```objc
id dataValue = [[Fraction alloc] init];
...
[dataValue setReal: 10.0 andImaginary: 2.5];
```

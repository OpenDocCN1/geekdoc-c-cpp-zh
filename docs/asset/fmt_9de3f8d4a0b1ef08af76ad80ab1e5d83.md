
现在我们可以谈谈实际示例了。首先，`a` 和 `b` 分别被定义为 `ClassA` 和 `ClassB` 对象。在分配和初始化之后，向 `a` 发送了一条消息，要求其执行 `initVar` 方法。该方法在 `ClassA` 的重写中定义，因此选择了该方法。这个简单的方法将实例变量 `x` 的值设置为 `100`，接着调用了你为 `ClassB` 中添加的 `printVar` 方法来显示 `x` 的值。

与 `ClassA` 对象一样，`ClassB` 对象 `b` 也经过了分配和初始化，它的实例变量 `x` 被设置为 `200`，最后显示了它的值。

请确保你理解如何根据 `a` 和 `b` 属于所属的类来为它们选择正确的方法。这是 Objective-C 面向对象编程的一个基本概念。

作为一个练习，请考虑从 `ClassB` 中移除 `printVar` 方法。这样做行得通吗？为什么行或不行？

在定义子类时，你不仅可以添加新方法来有效地扩展类的定义，还可以添加新的实例变量。在这两种情况下，效果都是累积的。你永远无法通过继承来减少方法或实例变量；你只能添加——或者在方法的情况下，进行重写。

所以，回顾一下，你为什么要创建一个子类？这里有三个原因：

- 1. 你想扩展类的功能，也许通过添加一些方法或实例变量。
- 2. 你想创建一个类的特化版本（例如，某种特定的对象）。
- 3. 你需要通过重写类的一个或多个方法来改变类的默认行为。

## 抽象类

用一点术语来结束本章会会更好吗？我们在这里引入它，是因为它与继承的概念直接相关。有时，创建类仅仅是为了让某人更容易创建子类；等效地，创建抽象类。方法和实例变量定义在类中，但没有人期望从该类创建实例。例如，考虑根类 `NSObject`。在第二部分“框架”中，所涵盖的 Foundation 框架有几类这类所谓的抽象类。例如，Foundation 的 `NSNumber` 类是一个为了处理数字而创建的抽象类。整数和浮点数有不同的存储要求。每种数字类型都存在 `NSNumber` 的子类。因为这些子类与抽象子类不同，它们存在并统称为 `NSNumber` 下的一个簇。诚然，这个讨论可能看起来有点“抽象”（抱歉！）！担心；掌握该基本概念就足够了。

## 练习

- 1. 在程序 8.1 中添加一个名为 `ClassC` 的新类，它是 `ClassB` 的子类。让 `initVar` 将实例变量 `x` 的值设置为 `300`。编写一个测试程序，声明 `ClassA`、`ClassB` 和 `ClassC` 对象并调用它们相应的 `Var` 方法。
- 2. 在处理高分辨率设备时，你可能需要使用一种坐标系统，允许将点作为浮点值而不是简单的整数（iOS 使用名为 `CGRect` 的结构来处理矩形。在处理此类矩形时，所有坐标和大小都以浮点数表示）。修改本章中的 `XYPoint` 和 `Rectangle` 类以处理浮点数。矩形的宽度、高度、面积和周长也应该能够处理浮点数。
- 3. 修改程序 8.1 添加一个新类 `ClassB2`，它像 `ClassB` 一样是 `ClassA` 的子类。关于 `ClassB` 和 `ClassB2` 之间的关系，你能些什么？识别 `NSObject` 类、`ClassA`、`ClassB` 和 `ClassB2` 之间的层级关系。`ClassB` 的子类是什么？一个类可以有多少个子类，它可以有多少个父类？
- 4. 编写一个名为 `translate` 的 `Rectangle` 方法，接收一个 `XYPoint` 对象作为参数。让它根据指定的向量平移矩形的原点。平移意味着将点从一个地方移动到另一个地方。
- 5. 定义一个新类 `GraphicObject`，并使其成为 `NSObject` 的子类。在你的新类中定义实例变量如下：

```
int fillColor;      // 32位颜色

BOOL filled;       // 对象是否填充？

int lineColor;     // 32位线框颜色
```

编写方法来设置和获取之前定义的变量。使 `Rectangle` 类成为 `GraphicObject` 的子类。定义新类 `Circle` 和 `Triangle`，它们也是 `GraphicObject` 的子类。编写方法来设置和获取这些对象的各种参数，并计算圆的周长和面积，以及三角形的周长和面积。
- 6. 编写一个名为 `containsPoint` 的 `Rectangle` 方法，接收一个 `XYPoint` 对象作为参数：`- (BOOL)containsPoint:(XYPoint *)APPoint;`。如果矩形包含指定的点，方法返回 BOOL 值，否则返回 NO。
- 7. 编写一个名为 `intersect` 的 `Rectangle` 方法，接收一个矩形作为参数并返回两个矩形重叠的矩形。例如，对于图 8.10 所示的矩形，该方法应返回一个原位于 `(400, 420)`、宽度为 `50`、高度为 `60` 的矩形。如果矩形不相交，返回一个宽度和高度为零且原位于 `(0, 0)` 的矩形。

# 第8章 继承

![](img/e9df1bbea90586fb77610264e0cbf7c_196_0.png)

图 8.10 相交的矩形

- 8. 为 `Rectangle` 类编写一个名为 `draw` 的方法，用横线和竖线字符绘制矩形。以下代码序列

```
Rectangle *myRect = [[Rectangle alloc] init];
[myRect setWidth:10 maxHeight:3];
[myRect draw];
```

将产生以下输出：

```
-------
|     |
|     |
```

> 注意
你应该使用 `printf` 来绘制字符，因为 `NSLog` 每次调用时都会换行。

## 多态、动态类型和动态绑定

在本章中，你将学习 Objective-C 语言中使其如此强大并与其他某些面向对象的语言（如 C++）有所不同的特性。本章描述了三个核心概念：多态、动态类型和动态绑定。多态允许开发程序使得不同类的对象可以定义相同名称的方法。动态类型将对象所属类的确定推迟到执行。动态绑定将对对象调用的实际方法的确定推迟到执行。

### 程序 9.1 接口文件 Complex.h

```
// Complex类的接口文件
#import <Foundation/Foundation.h>
@interface Complex: NSObject
@property double real, imaginary;
- (void) print;
- (void) setReal:(double) a andImaginary:(double) b;
- (Complex *) add:(Complex *) f;
@end
```

你应该已经在第 7 章“类进阶”的练习 5 和 6 中完成了该类的实现部分工作。我们添加了一个额外的 `setReal:andImaginary:` 方法，以便通过单条消息设置数字的实部和虚部，并包含了所有合成的访问器方法。如下所示。

## 程序 9.1 实现文件 Complex.m

```objc
// Complex 类的实现文件
#import "Complex.h"
@implementation Complex
@synthesize real, imaginary;
-(void) print {
  NSLog("%g + %g", real, imaginary);
}
-(void) setReal:(double) a andImaginary:(double) b {
  real = a;
  imaginary = b;
}
-(Complex*) add:(Complex *) f {
  Complex *result = [[Complex alloc] init];
  result.real = real + f.real;
  result.imaginary = imaginary + f.imaginary;
  return result;
}
@end
```

## 程序 9.1 测试程序 main.m

// 共享方法名：多态

```objc
#import "Fraction.h"
#import "Complex.h"
int main (int argc, char *argv[]) {
```

## 多态：同名不同类

```objc
@autoreleasepool {
Fraction *f1 = [[Fraction alloc] init];
Fraction *f2 = [[Fraction alloc] init];
Fraction *fracResult;
Complex *c1 = [[Complex alloc] init];
Complex *c2 = [[Complex alloc] init];
Complex *compResult;
[f1 setTo: 1 over: 10];
[f2 setTo: 2 over: 15];
[c1 setReal: 18.0 and Imaginary: 2.5];
[c2 setReal: -5.0 and Imaginary: 3.2];
// 相加并打印两个两个复数
[c1 print]; NSLog("@%s +
```

## 程序 9.1 输出

```
18 + 2.5i
+
------
-5 + 3.2i
------
13 + 5.7i
1/10
+
------
2/15
------
7/30
```

注意，`Fraction` 和 `Complex` 类都包含 `add:` 和 `print` 方法。因此，当执行以下消息表达式时：

```objc
compResult = [c1 add: c2];
[compResult print];
```

系统是如何知道执行哪个方法的？很简单：Objective-C 运行时知道第一个消息的接收者 `c1` 是一个 `Complex` 对象。因此，它选择了 `Complex` 类定义的 `add:` 方法。

Objective-C 运行时也确定 `compResult` 是一个 `Complex` 对象，因此它选择了 `Complex` 类定义的 `print` 方法来显示相加的结果。同样的讨论适用于以下表达式：

```objc
fracResult = [f1 add: f2];
[fracResult print];
```

正如第 13 章“底层 C 语言特性”中所详细描述，系统始终带有对象所属类的信息。这使其能够在运行时而不是编译时做出这些关键决策。

根据 `f1` 和 `fracResult` 的类，选择了 `Fraction` 类中对应的方法来评估消息表达式。

如所述，跨类共享相同方法名的能力被称为多态。多态允许你开发一组类，每个类都可以响应相同的方法名。每个类的定义都封装了响应该特定方法所需的代码，并使其独立于其他类的定义。这还允许你稍后添加可以响应相同名称方法的类类。

## 动态绑定与 id 类型

第 4 章“数据类型与表达式”简要提到了 `id` 数据类型，并指出它是一种通用对象类型。也就是说，`id` 用于存储属于任何类的对象。当它在程序执行期间被用于存储不同类型的对象时，这种数据类型的真正威力就发挥出来了。请程序 9.2 及其相关的输出。

```objc
程序 9.2 测试程序 main.m
// 演示动态类型与绑定
#import "Fraction.h"
#import "Complex.h"
```

```objc
int main (int argc, char * argv[])
{
    @autoreleasepool {
        id        dataValue;
        Fraction *f1 = [[Fraction alloc] init];
        Complex *c1 = [[Complex alloc] init];
        [f1 setTo: 2 over: 5];
        [c1 setReal: 10.0 and Imaginary: 2.5];
        // dataValue 首次得到了一个分数
        dataValue = f1;
        [dataValue print];
        // 现在 dataValue 得到了一个复数
        dataValue = c1;
        [dataValue print];
    }
    return 0;
}
```

## 程序 9.2 输出

```
2/5
10 + 2.5i
```

变量 `dataValue` 被声明为 `id` 类型。因此，`dataValue` 可以在程序中持有任何类型的对象。注意声明行中没有使用星号：
`id dataValue;`

`f1` 被设置为 2/5，而复数 `c1` 被设置为 (10 + 2.5i)。赋值语句
`dataValue = f1;`
将 `f1` 存储在 `dataValue` 中。现在，你可以对 `dataValue` 做什么呢？你可以调用你在 `Fraction` 对象上使用的任何方法，尽管 `dataValue` 的类型是 `id` 而不是 `Fraction`。但如果 `dataValue` 可以存储任何类型的对象，系统是如何知道执行哪个方法的呢？也就是说，当它遇到消息表达式 `[dataValue print];` 时，它是如何知道哪个 `print` 方法的？你为 `Fraction` 和 `Complex` 类都定义了 `print` 方法。

如之前，答案在于 Objective-C 系统跟踪对象所属的类。它也在于动态类型和动态绑定的概念。也就是说，系统对对象的类做出决策，因此必须动态地调用，而不是在编译时。

在程序执行期间，系统向 `dataValue` 发送 `print` 消息之前，它首先检查存储在 `dataValue` 中的对象的类。在程序 9.2 的第一种情况下，变量包含一个 `Fraction` 对象，因此使用了 `Fraction` 类定义的 `print` 方法。这通过程序的输出得到了验证。

在第二种情况下，情况也一样。变量包含一个 `Complex` 对象，因此使用了 `Complex` 类定义的 `print` 方法。

# 186 第 9 章 多态、动态类型与动态绑定

然而，如果这些检查在运行时已经由你执行了，你为什么何要在意静态类型呢？你之所以在意，是因为在程序的编译阶段发现错误远比在执行阶段发现错误要好。如果你将其推迟到运行时，当错误发生时，你可能甚至不是那个运行程序的人。如果你的程序已经投入生产环境，某些毫无防备的用户在运行程序时，可能会发现某个对象不识别某个方法，从而导致程序崩溃。

使用静态类型的另一个原因是它可以让你的程序更具可读性。考虑以下声明：

```
id f1;
```

对比

```
Fraction *f1;
```

你认为认为哪一个更易于理解——也就是说，哪一个让变量 f1 的预期用例更清晰？静态类型与有意义的变量名（我们在上一个示例中刻意没有选择）的结合，可以很大程度地让你的程序更具自文档性。

> 注意
你不能对 id 类型的变量使用点操作符（`.`）；如果你尝试这样做，编译器会报错。

## 动态类型中的参数和返回类型

如果你使用动态类型来调用方法，请注意以下规则：如果在你的某个类中实现了一个同名的方法，则每个方法必须对每个参数的类型以及返回值的类型保持一致，以便编译器能为你的消息表达式生成正确的代码。

编译器会对它所拥有的每个类声明进行一致性检查。如果一个或多个方法在参数或返回类型上存在冲突，编译器会发出警告信息。例如，Fraction 和 Complex 类都添加了 `methods` 方法。然而，Fraction 类接收 Fraction 对象作为参数并返回一个 Fraction 对象，而 Complex 类接收并返回一个 Complex 对象。如果 frac 和 myFract 是 Fraction 对象，而 compl 和 myComplex 是 Complex 对象，那么如下语句：

```
result = [myFract add:frac];
```

以及

```
result = [myComplex add:compl];
```

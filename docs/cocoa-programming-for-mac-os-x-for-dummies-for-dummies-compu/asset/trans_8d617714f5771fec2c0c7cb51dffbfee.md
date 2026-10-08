

# 使用 Objective-C 编程

声明一个类、为其声明添加实例变量和方法，并搭建好实现文件的框架后，是时候编写一些代码了！

### 向对象发送消息

Objective-C 中最基本的概念之一是一个对象能够向另一个对象发送消息的能力。在 Objective-C 中，通常通过向对象发送消息来指示其执行某个方法。Objective-C 使用方括号来表示正在向对象发送消息。

![](img/ea40cad434a338535474e82c1a6ace20_134_0.png)

发送消息与其他编程语言中调用函数类似。

对于一个通用对象（命名为 object），你可以通过如下方式向其发送一条消息（命名为 message）：

```objective-c
[object message];
```

注意两点：

- 该语句的语法使其行为很像英语中的命令。例如，你可能会对出租车司机说：

```objective-c
Driver, go!
```

在 Objective-C 中，同样的命令看起来像这样：

```objective-c
[driver go];
```

- 每行代码都以分号结尾。除了 C 语言中通常省略分号的地方（例如 if 语句）外。Objective-C 也要求在每行代码末尾加分号。毕竟 Objective-C 也是 C！

### 传递参数

与传统 C 函数一样，Objective-C 允许你向方法传递参数（也称为实参）。回到出租车的比喻，你可能想告诉司机去哪里：

```objective-c
Driver, go left!
```

在 Objective-C 中，该命令可能看起来像这样：

```objective-c
[driver go:left];
```

对于 C 程序员来说，go 方法大致类似于标准 C 函数。但是，如果你添加另一个参数，这种类比就会失效。例如，假设你想向 go 方法传递两个参数（direction 和 distance）：

```objective-c
[driver go:left distance:10];
```

在 Objective-C 中，第一个参数跟随在方法名称（在此情况下为 go:left）后的冒号之后。每个后续参数都有一个名称，后跟一个参数（在此实例中为 distance:10）。相比之下，类似的 C 函数可能是

```objective-c
go(left,10);
```

在 Objective-C 中，第一个参数的含义通常根据方法名称即可明了。其他参数有名称，帮助你识别其用途。

![](img/ea40cad434a338535474e82c1a6ace20_135_0.png)

### 返回值

与 C 函数一样，Objective-C 方法也可以返回值。如果你告诉出租车司机某个方向和距离，你接下来很可能听到的是车费价格。你指示司机做某事。司机回复一个价格。在 Objective-C 中，这与其在 C 中的工作方式非常相似。

```objective-c
price = [driver go:left distance:10];
```

由于某些方法会返回值，Cocoa 程序员喜欢将它们嵌套在其他方法内。假设你基于 go 给出租车司机指路，但不一定走很远。在这种情况下，你可能会使用一个地图对象来查找期望的位置，并将其嵌入到 go 方法中。

```objective-c
[driver go:left
distance:map startAt:location1
destination:location2];
```

回到本章之前你定义的类，你希望在这些方法中的每一个都编写代码，向同一类中的其他方法发送消息。要在同一类内调用其他方法，请像这样使用 self：

```objective-c
- (void)doSomething {
    [self drawString:@"hello" atXPosition:10
          atYPosition:6];
}
```

### 实例化对象

创建类之后，你会希望将其用作对象。当你想创建一个 Objective-C 对象时，你向类发送 alloc 消息，如下所示：

```objective-c
MyClass* anInstance = [MyClass alloc];
```

alloc 分配内存并创建类。已实例化的对象还必须进行初始化。你通过向实例发送 init 方法来完成初始化，如下所示：

```objective-c
[anInstance init];
```

由于 alloc 和 init 都是通用实例化所必需的，通常习惯将它们嵌入到一条语句中：

```objective-c
MyClass * anInstance = [[MyClass alloc] init];
```

然后，你可以自由地按需操作该对象（anInstance）。你可以向实例发送 drawString:@"hello"：

```objective-c
[anInstance drawString:@"hello" atThisXPosition:10 atThisYPosition:6];
```

因为你使用 alloc 创建了该实例，所以必须使用 release 释放该内存：

```objective-c
[anInstance release];
```

### 管理内存

最近版本的 Cocoa 提供了垃圾收集的支持，但历史上 Cocoa 并没有垃圾收集。垃圾收集动态释放你为对象分配的内存。这是一个较新的特性，由于许多示例代码资源都采用旧方式，因此最好理解在没有垃圾收集的情况下 Cocoa 的内存管理。

Cocoa 通过引用计数来跟踪内存。这是一个在后台运行的简单计数器，记录有多少对象分配了内存以及有多少对象释放了内存。当你使用 alloc 创建对象时，引用计数增加 1。当你向对象发送 release 消息时，计数减少 1。关键在于，在你使用完对象后，引用计数最终可能会变为零。如果计数大于零，你就泄漏了内存。如果引用计数小于零，你释放了一个内存中你仍然需要的对象。当你尝试访问这个已释放的对象时，你的代码将崩溃。

如前几节所示，对象是通过 alloc 方法分配的。alloc 方法使引用计数增加 1，因此需要一个相应的 release。

```objective-c
SomeClass *object = [[SomeClass alloc] init];
// do stuff with someObject here...
[someObject release];
```

到目前为止，这很简单，因为对象的分配和释放都在同一代码块内。当涉及到实例变量时，情况就会变得有点令人头大。虽然在你的方法中按名称访问实例变量是合法的，但通过访问器方法访问它们要明智得多。

![](img/ea40cad434a338535474e82c1a6ace20_137_0.png)

由于内存管理问题，如果你不使用访问器方法访问实例变量，事情会迅速变得混乱。如果你不使用访问器方法，你的应用程序很可能会泄漏内存，或者在尝试释放已经释放的对象时崩溃。

例如，假设你有一个类，其中有一个 NSString 实例变量 name。声明两个方法来访问该实例变量。一个 getter（name）和一个 setter（setName:）：

```objective-c
@interface MyClass : NSObject {
    NSString *name;
}
- (NSString *)name;
-(void)setName:(NSString *)aName;
@end
```

然后，在你的实现文件中，像这样定义这些方法：

```objective-c
@implementation MyClass
-(NSString *)name {
    return name;
}
-(void)setName:(NSString *)aName {
    [name retain];
    [aName release];
    name = aName;
}
@end
```

### 第 6 章：Objective-C 基础

setName 方法向 aName 发送 retain 消息。retain 方法，就像 alloc 一样，使引用计数增加 1。（把 retain 想象成 release 的反面可能有助于理解。）因此，代码通过 retain aName 来保留内存，以便在类的其他地方使用。并且因为你已经用完 name 所指的对象，所以你接着 release name。该方法赋值 aName。遵循这一简单计划可以防止你每次使用 name 时泄漏内存，无论 name 之前指向什么，新指向的对象已被保留。

如果你到目前为止都跟上了进度，你可能会想知道当对象最终被销毁时会发生什么。name 实例变量的引用计数不还是 1 吗？是的！你必须在类的 dealloc 方法中释放最后一个残留的 name。

```objective-c
- (void)dealloc {
    [name release];
}
```

以下是一些你不必担心保留和释放对象的特殊情况：

- 当你使用类的内置便捷方法之一创建对象时：该对象被称为自动释放（autoreleased），这意味着你不需要释放它，因为它将被自动释放。例如，NSString 类有一个 stringWithString 便捷方法。你可以使用它代替 alloc 来创建 NSString 对象。你不需要 alloc 来创建该对象。并且因为你使用的是便捷方法 stringWithString，它是自动释放的，所以无需释放。

- 当对象在代码中自动释放时：例如，如果你看到一个对象带有 autorelease，就不需要释放该对象：

```objective-c
SomeClass *someObject = [[SomeClass alloc] init] autorelease];
```

autorelease 方法使引用计数减少 1，这抵消了 alloc 使引用计数增加 1 的影响。

![](img/ea40cad434a338535474e82c1a6ace20_138_0.png)


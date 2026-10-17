
### 在 `dealloc` 方法中使用访问器来释放成员变量

```
-(void)dealloc
{
    [self setFoo:nil];
    [self setBar:nil];
    [super dealloc];
}
```

像这样编写你的 `dealloc` 方法非常好！你可以同时释放成员变量并将其设置为 `nil`，一步到位。

问题在于，当你调用这些访问器时，KVO 观察者会收到这些变更的通知。如果它们不期望收到 `nil`，或者它们期望在收到通知时能够操作对象本身，那么就可能发生糟糕的事情。

此外，你可以想象一个观察者，当它收到对 `bar` 变量变更的通知时，期望能够访问 `foo` 变量——显然，在这种情况下，它会遇到问题，因为 `foo` 变量已经被释放并设置为 `nil`。

Apple 目前的建议是，你不要在初始化方法或 `dealloc` 方法中使用访问器来初始化或释放成员变量。而接下来的事实又使这个问题变得更加复杂。

在 64 位运行时下，可以声明没有关联成员变量的属性。在这些情况下，初始化和释放成员变量的唯一方法是通过使用它们的访问器。

在我的代码中，除非我知道在特定情况下这样做会造成问题，否则我会使用访问器来初始化和释放成员变量。此外，当我实现键值观察者时，我会确保观察者能够正确处理 `nil` 值，并且我会尽量减少任何副作用。

如果你认为这是值得冒的风险，那么请随意在初始化方法和析构方法中使用访问器。只要意识到其中潜在的危险，这样当你遇到问题时，就能立即知道去哪里查找。

另一方面，如果你觉得无法确保观察者的安全性，请遵循苹果的建议，不要在初始化器和析构函数中使用访问器，除非必须。

## 应用键值观察

现在你已经了解了键值编码和键值观察的所有细节，请看一个包含几个类的简单示例应用程序。其中一个类将观察其他类，并在接收到被观察类属性变化的通知时，将这些变化打印到控制台。

清单 6.20 显示了此应用程序中的第一个类。这个简单的点类有几个属性，`x` 和 `y`。只需将接口放入接口文件，将实现放入实现文件即可。

```
// Interface - goes in MyPoint.h
#import <Cocoa/Cocoa.h>

@interface MyPoint : NSObject
{
    CGFloat x;
    CGFloat y;
}
@property CGFloat x;
@property CGFloat y;

@end
```

```
// implementation - goes in MyPoint.m
#import "MyPoint.h"
@implementation MyPoint
@synthesize x;
@synthesize y;
@end
```

### Listing 6.21

观察者类

```
// Interface - goes in Observer.h
#import <Cocoa/Cocoa.h>
#import "MyPoint.h"

@interface Observer : NSObject
{
    MyPoint *point;
}
@property (retain) MyPoint *point;
- (id)initWithPoint:(MyPoint *)inPoint;
@end
```

```
// Implementation - goes in Observer.m
#import "Observer.h"

@implementation Observer
@synthesize point;

- (void)dealloc
{
    [point removeObserver:self forKeyPath:@"x"];
    [point removeObserver:self forKeyPath:@"y"];
    [point release];
}
```

### Listing 6.21 (continued)

```
point = nil;
[super dealloc];
}

-(id)initWithPoint:(MyPoint *)inPoint;
{
    if(self = [super init])
    {
        point = [inPoint retain];
        [point addObserver:self forKeyPath:@"x"
            options:(NSKeyValueObservingOptionNew|
                     NSKeyValueObservingOptionOld)
            context:nil];
        [point addObserver:self forKeyPath:@"y"
            options:(NSKeyValueObservingOptionNew|
                     NSKeyValueObservingOptionOld)
            context:nil];
    }
    return self;
}

-(void)observeValueForKeyPath:(NSString *)keyPath
    ofObject:(id)object
    change:(NSDictionary *)change
    context:(void *)context;
{
    NSNumber *oldValue = [change objectForKey:NSKeyValueChangeOldKey];
    NSNumber *newValue = [change objectForKey:NSKeyValueChangeNewKey];

    if(keyPath == @"x")
        NSLog(@"Value for X changed from: %f to %f",
            [oldValue floatValue],
            [newValue floatValue]);
    if(keyPath == @"y")
        NSLog(@"Value for Y changed from: %f to %f",
            [oldValue floatValue],
            [newValue floatValue]);
}

@end
```

最后是主函数。清单 6.22 显示了此代码。

### Listing 6.22

主函数。

```
#import <Foundation/Foundation.h>
#import "Observer.h"
#import "MyPoint.h"

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    MyPoint *point = [[MyPoint alloc] init];
    Observer *observer = [[Observer alloc] initWithPoint:point];

    point.x = 42.0;
    point.y = 55.1;

    point.x = 4200.0;
    point.y = 5500.1;

    [observer release];
    [point release];

    [pool drain];
    return 0;
}
```

它所做的只是创建点，然后创建观察者，并将点传递给它。然后它更改值。所有输出都在 `Observer` 类内部完成，并且是自动的。

继续编译并运行此应用程序，看看我的意思。

## 摘要

在本章中，我向你介绍了键值编码和键值观察，这两种是 Objective-C 以及 Cocoa 和 Cocoa Touch 框架为你提供的核心技术。通过使用这些功能，你可以构建更灵活的应用程序设计，而不会将应用程序的不同部分耦合得太紧密。松散耦合意味着更灵活的设计，而 KVO 和 KVC 为你提供了保持应用程序组件松散耦合所需的工具。

## 使用协议

Objective-C 不支持多重继承，这既有优点也有缺点。其优点在于多重继承会导致难以解决的复杂问题。然而，这也是一个缺点，因为有时你希望一个类实现特定的接口，而不必继承指定该接口的类。值得庆幸的是，Objective-C 的设计者包含了一个功能来解决这种情况，即协议。

本质上，协议定义了一个接口，可以由多个其他类在不使用继承的情况下实现。这使你能够在给定类上混合匹配功能，以便该类可以适应不同的用途。

### 优先使用组合而非继承

一个面向对象设计的公理“优先使用组合而非继承”意味着，与其总是把继承作为扩展给定类功能的工具，你应该首先尝试通过在类中使用其他类进行组合来解决问题。例如，如果你需要实现一个在网络服务和应用程序之间提供接口的类，而不是从套接字类继承（一个为你提供网络资源访问的类），你应该在类中包含另一个对象，该对象提供网络连接。你应该从其他可重用组件“组合”你的设计。以这种方式构建设计会带来更大的灵活性，因为你为解决给定问题而组合在一起的这些部分以后可以被替换和更改以解决另一个问题。这是一种非常强大的设计哲学，你应该在代码中努力追求。

当然，仅通过使用标准的面向对象技术就可以遵循这种设计哲学。然而，为重用而设计组件会带来复杂性。

### 本章内容

- 使用协议解决面向对象设计问题

- 为你的类实现协议

- 采用协议

- 使用可选方法

- 理解正式协议与非正式协议

图 7.1 显示了一个类图，描述了包含业务逻辑的类与为网络连接提供的类之间的关系。这是一个典型的“组合式”设计。

这里的想法是 `NetworkConnector` 类提供与网络服务器的所有交互。它连接、断开连接，并发送和接收数据。`BusinessLogic` 类接收 `NetworkConnector` 接收到的数据，并决定这些数据需要在应用程序中的哪个位置。

### Figure 7.1

紧密耦合的 `BusinessLogic` 和 `NetworkConnector`。

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_211_0.png)

问题在于当你需要从 `NetworkConnector` 类向 `BusinessLogic` 类通信时，例如在接收数据时。网络连接是一个非常通用的概念。你肯定可以在其他应用程序中重复使用，甚至可以在同一应用程序的不同位置重复使用。如果你想以完全通用的方式设计网络类，以便网络类可以一次又一次地重复使用，你必须设计它，使其在任何方面都不会与客户端类紧密耦合，换句话说就是 `BusinessLogic` 类。

你不能让 `NetworkConnector` 要求 `BusinessLogic` 类作为依赖，因为你不能总是指望 `BusinessLogic` 类是使用你的 `NetworkConnector` 的类。

使用继承解决此问题的一种方法是强制 `BusinessLogic` 类继承自某个父类，而 `NetworkConnector` 类可以依赖该父类。这在图 7.2 中显示。

### Figure 7.2

`BusinessLogic` class inheriting from generic `NetworkClient` class.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_212_0.png)

在这种情况下，你通过强制客户端类继承自特定的父类来限制客户端类的开发者。如果该父类不能很好地融入该开发者对象层次结构中，那么这可能会带来重大的设计问题。例如，想象一下 `BusinessLogic` 类需要同时与网络通信，以及与具有类似回调机制的磁盘 I/O 系统通信。使用这种直接继承在这种情况下根本行不通。

### Understanding why you don’t need (or want) multiple inheritance

某些语言，例如 C++，通过多重继承解决这种问题。图 7.3 显示了你如何在 C++ 中解决网络通信问题的示例。

多重继承的问题通常被称为“菱形问题”，并在图 7.4 中说明。

### Figure 7.3

Using multiple inheritance.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_213_0.png)

正如你在类图中看到的，多重继承的主要问题源于可以从两个不同的类继承（上图，类 D 同时继承自类 B 和 C），而这两个类又继承自一个共同的超类（类 A）。在这种情况下，可能会出现歧义，即在类 D 的实例上调用类 A 上的方法。在这种情况下，如果类 D 没有重写该方法并提供自己的实现，应该调用哪个超类方法，B 还是 C？

由于这个问题，多重继承根本不是 Objective-C 所提供的内容。如果只有单继承，那么你就不必担心菱形问题。

### Understanding how protocols solve the problem

协议通过使你能够声明一个接口来解决这个问题，而类在实现该接口时不提供任何默认实现。协议不提供指定其中方法实现的机制。它们只提供声明这些方法的接口的机制。与使可重用组件依赖于特定的类实现相比，你可以改为使该组件依赖于协议形式的接口存在。实现给定协议的类预计将提供协议声明中指定的方法的自己的实现。通过以这种方式实现协议，你可以使类编写为仅依赖于接口存在，同时消除歧义问题，因为任何声明其实现给定接口的类也必须实现相关方法。不存在“菱形问题”，因为你声明和支持的任何协议都必须在你的类中有实现。

### Figure 7.4

The diamond problem.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_214_0.png)

从面向对象设计的角度来看，此解决方案的类图几乎与多重继承的类图相同，但它不允许多重继承必然带来的问题。

此解决方案并不独特于 Objective-C。Java，在很多方面基于 Objective-C，也使用其版本的协议即接口实现了类似的概念。如果你是从 Java 背景转向 Objective-C，协议和接口的概念非常相似，你应该会感到宾至如归。

### Documenting an expected interface for others to implement

另一种思考协议的方法是想象你正在为他人实现而记录一个预期的接口。在 `NetworkConnector` 示例中，我们记录了网络类可能需要开发者协助以确定在这些情况下该做什么的所有不同条件。

例如，如果 `NetworkConnector` 从网络接收数据，合理地假设应用程序本身包含确定对该数据做什么所需的业务逻辑知识。换句话说，没有通用的方法可以说“当我收到数据时，我将如何处理它”。你真的必须询问应用程序的其余部分“我刚刚收到一些数据，你希望我如何处理它？” 这正是协议完美且独一无二地适用的情况。你可以为你的通用组件需要能够委托给更高权限的所有不同未解决问题声明一个协议（“我收到数据，我该怎么办？” - “我断开连接了是否应该重新连接？”）。

通过声明这些不同的“问题”，你建立了一个清晰而精确的契约，类的使用者可以随后履行。当他们通过实现协议来履行此契约时，他们将知道需要准备处理的所有不同情况。此系统比涉及返回代码、异常等的任何系统都更灵活。它甚至比简单的通用回调更强大，因为 Objective-C 方法声明的独特详细程度以及声明清晰明显的协议成为可重用组件的自文档化回调 API 的行为。如果你这样想，“协议”这个词比“接口”更有意义，因为“协议”可以被认为是一种商定的程序或行为准则，就像外交和礼仪一样。

好了，理论够多了，现在你可以动手写一些代码了。

### Implementing Protocols in Your Objects

使用协议非常简单，并且遵循你在处理类时已经看到的许多相同的语法约定。

本质上，你首先必须创建协议声明。你可以在现有的接口文件中执行此操作，如果你为已存在的对象声明协议，如我们在之前讨论 `NetworkClient` 时的情况，或者在单独的接口文件中，如果你可能将此协议用于许多不同的目的。协议本身只声明接口并且完全不提供实现。因此，如果你为协议声明创建单独的 `.h` 文件，你根本不需要提供任何 `.m` 文件。 `.h` 文件中的接口就足够了。

在你声明协议之后，对于实现该协议的任何类，它们也应声明它们实现了它。这样编译器可以验证相关类是否实现了程序所需的所有方法。

> **NOTE**

实际上并非绝对必要声明你的类实现了它支持的协议。正如我们稍后讨论的那样，一些类型的协议根本不需要声明。此外，你的类可以选择仅实现协议方法而不是声明其支持。在这些情况下，编译器将无法在编译时确定你的类是否支持协议，因此你必须在运行时做额外的工作以确保你在其上调用协议方法的任何对象实际上都实现了它们。这可能会导致编译器警告，如果另一个类声明它期望你的类实现协议。

当你在代码中引用对象时，这些对象预计实现给定协议，你可以在该对象的类型声明中使用一种特殊语法来显示，虽然你可能不知道对象的实际类，但你期望它实现给定协议。如果协议是正式协议，则存储在该变量中的任何对象都会在编译时检查以确定它是否实现了该协议所需的所有方法。如果没有，则会发出警告。

协议可以同时具有必需和可选方法。在你有可选方法的情况下，实现协议的对象可能不一定实现其其中一个可选方法。在这种情况下，你预计会检查以验证相关对象是否实现了可选方法，然后再尝试调用它。如果你尝试调用可选方法而对象未实现该方法，则会得到异常。

### Declaring a protocol

声明协议遵循许多你已经熟悉的相同的语法标准。表面上，它最类似于声明一个类。你通过使用关键字 `@protocol` 开始协议声明，后跟你要声明的协议的名称。协议默认不继承自彼此或类，但如果你想继承另一个协议，你可以可选地通过在你要声明的协议名称后用尖括号 `<>` 括起继承的协议名称来继承它。当你这样做时，实现你的协议的类必须不仅实现你声明的协议方法，还必须实现你继承的任何协议的协议方法。在 `@protocol` 声明之后，你然后声明协议所需的任何方法。声明这些方法就像你在类上声明方法一样。

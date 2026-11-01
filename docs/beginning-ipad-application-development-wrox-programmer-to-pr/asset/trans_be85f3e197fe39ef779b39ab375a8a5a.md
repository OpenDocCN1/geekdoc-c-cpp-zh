

要调用这三个实例方法，首先需要创建类的一个实例，然后使用所创建的实例来调用它们：

```
SomeClass *someClass = [SomeClass alloc];
[someClass doSomething];
[someClass doSomething:@"some text"];
[someClass doSomething:@"some text" withAnotherPara:9.0f];
```

类方法可以直接使用类名调用，如下所示：

```
[SomeClass alsoDoSomething];
```

一般来说，当需要执行与类的特定实例（即对象）相关的操作时，应创建实例方法。例如，假设定义了一个表示员工信息的类。你可以公开一个实例方法，用于计算员工的加班工资。在这种情况下，你应该使用实例方法，因为该计算涉及特定员工对象的数据。

另一方面，类方法通常用于定义辅助方法。例如，你可能有一个名为 `getOvertimeRate` 的类方法，用于返回加班费率。由于所有员工的加班费率相同（假设贵公司如此），因此无需创建实例方法，类方法就足够了。

下一节将展示如何调用参数数量可变的方法。

## 消息发送（方法调用）

在 Objective-C 中，使用以下语法调用方法：

```
[object method];
```

严格来说，在 Objective-C 中并不是调用方法，而是向对象发送消息。传递给对象的消息在运行时才被解析，而不是在编译时强制执行。这就是为什么即使方法名拼写错误，编译器也不会阻止程序运行。不过，编译器会尝试警告你目标对象可能无法响应你的消息，因为目标对象会直接忽略该消息。图 D-1 展示了当 UITableView 初始化器的某个参数拼写错误时（`cancelButtonsTitle:` 应为 `cancelButtonTitle:`），编译器给出的警告。

> 为了便于理解，我使用更传统的术语“调用方法”来指代 Objective-C 的消息发送机制。

![](img/744c5ec15e15ca7891c98be71dc25d13_561_0.png)

## 属性

在 Objective-C 2.0 之前，程序员必须声明方法才能使字段对其他类可访问，如下所示：

```
#import <Foundation/Foundation.h>

@class AnotherClass;

@interface SomeClass : NSObject {
    AnotherClass *anotherClass;
    float rate;
    NSString *name;
}

//---expose the rate field---
-(float) rate;          //---get the value of rate---
-(void) setRate:(float) value;  //---set the value of rate

//---expose the name field---
-(NSString *) name;     //---get the value of name---
-(void) setName:(NSString *) value;  //---set the value of name---

@end
```

这些方法称为 getter 和 setter（有时也称为访问器和修改器）。这些方法的实现可能如下所示：

```
#import "SomeClass.h"

@implementation SomeClass

-(float) rate {
    return rate;
}

-(void) setRate:(float) value {
    rate = value;
}

-(NSString *) name {
    return name;
}

-(void) setName:(NSString *) value {
    [value retain];
    [name release];
    name = value;
}

@end
```

要设置这些属性的值，需要调用以 `set` 关键字开头的方法：

```
SomeClass *sc = [[SomeClass alloc] init];
[sc setRate:5.0f];
[sc setName:@"Wei-Meng Lee"];
```

如所示，可以使用单个 `@synthesize` 关键字组合多个属性。不过，也可以将它们分成单独的语句：

```
@synthesize rate;
@synthesize name;
```

现在可以像往常一样使用属性：

```
//---setting using setRate---
[sc setRate:5.0f];
[sc setName:@"Wei-Meng Lee"];

//---setting using dot notation---
sc.rate = 5;
sc.name = @"Wei-Meng Lee";

//---getting---
NSLog([sc name]); //---using the name method
NSLog(sc.name);   //---dot notation
```

要使属性只读，请使用 `readonly` 关键字。以下语句使 `name` 属性只读：

```
@property (readonly) NSString *name;
```

## 初始化器

当你创建类的实例时，通常同时对其进行初始化。例如，在之前的示例（“类实例化”一节）中，你有这样一个语句：

```
SomeClass *sc = [[SomeClass alloc] init];
```

`alloc` 关键字为对象分配内存，当返回对象时，会在对象上调用 `init` 方法来初始化对象。回想一下，在 `SomeClass` 中，你并未定义名为 `init` 的方法。那么 `init` 方法从何而来？它实际上定义在 `NSObject` 类中，而 `NSObject` 是 Objective-C 中大多数类的基类。`init` 方法称为初始化器。

如果你想创建其他初始化器，可以定义以 `init` 单词开头的方法。（使用 `init` 单词更多是一种惯例，而非硬性规则。）

```
#import <Foundation/Foundation.h>

@class AnotherClass;

@interface SomeClass : NSObject {
    AnotherClass *anotherClass;
    float rate;
    NSString *name;
}

- (void) doSomething;
- (void) doSomething:(NSString *) str;
```

```
//...
}
return self;
}
```

定义初始化器的规则很简单：如果类正确初始化，则应返回对 self 的引用（因此类型为 `id`）。如果失败，则应返回 `nil`。

对于 `initWithName:` 初始化器的实现，请注意它调用了 `initWithName:andRate:` 初始化器：

```
- (id)initWithName:(NSString *) n {
    return [self initWithName:n andRate:0.0f];
}
```

通常，如果有多个初始化器，每个初始化器参数不同，你应该通过确保它们都调用一个执行超类 `init` 初始化器调用的初始化器来将它们链接起来。在 Objective-C 中，执行超类 `init` 初始化器调用的初始化器称为指定初始化器。

> **注意** 作为一般准则，指定初始化器应该是参数最多的那个。

要使用初始化器，现在可以在实例化时调用它们：

```
SomeClass *sc1 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
SomeClass *sc2 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee"];
```

## 内存管理

Objective-C 编程（尤其是 iPad）中的内存管理是一个非常重要的话题，每个 iPad 开发者都需要了解。与其他流行的语言一样，Objective-C 也支持垃圾回收，这有助于在对象超出作用域时移除不再使用的对象，从而释放可重复使用的内存。然而，由于实现垃圾回收涉及严重的开销，iPad 不支持垃圾回收。这就使得你（开发者）需要在对象不再需要时手动分配和释放对象的内存。

本节讨论 iPad 上内存管理的各个方面。

### 引用计数

为了帮助开发者分配和释放对象的内存，iPhone OS 使用一种称为引用计数的方案来跟踪对象，以确定它们是否仍然需要或可以被处理。引用计数基本上为每个对象使用一个计数器，每创建一个对象，计数增加 1。当对象被释放时，计数减少 1。当计数达到 0 时，操作系统回收与该对象关联的内存。

> **注意** 那么，如何释放 str2 呢？它是自动释放的。有关更多信息，请参阅“便捷方法和自动释放”一节。

如果你想确保即使 str 被释放，str2 仍然可用，需要使用 `retain` 关键字：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str2 retain];
[str release];
```

在上述情况下，str 的引用计数现在是 2。当你释放 str 时，str2 仍然有效。当你使用完 str2 后，需要手动释放它。

> **注意** 作为一般规则，如果你拥有一个对象（使用 `alloc` 或 `retain`），你需要释放它。

### release

当你使用完一个对象后，需要使用 `release` 关键字手动释放它：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
//...do what you want with the object...
[str release];
```

当对对象使用 `release` 关键字时，该对象的引用计数会减少 1。当引用计数达到 0 时，对象使用的内存会被释放。

使用 `release` 关键字时需要记住的一个重要方面是，你不能释放不归你拥有的对象。例如，考虑上一节中使用的示例：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str release];
[str2 release]; //---this is not OK as you do not own str2---
```

尝试释放 str2 将导致运行时错误，因为不能释放不是自己拥有的对象。但是，如果使用 `retain` 关键字获得对象的所有权，那么你确实需要使用 `release` 关键字：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str2 retain];
[str release];
[str2 release]; //---this is now OK as you now own str2---
```


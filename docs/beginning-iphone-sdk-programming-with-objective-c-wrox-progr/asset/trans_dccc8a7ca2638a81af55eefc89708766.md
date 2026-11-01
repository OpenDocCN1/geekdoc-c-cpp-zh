
在实现文件中，而不是自行定义 getter 和 setter 方法，你可以简单地使用 @synthesize 关键字，让编译器自动为你生成 getter 和 setter：

```objc
#import "SomeClass.h"

@implementation SomeClass
@synthesize rate, name;

@end
```

如图所示，你可以使用单个 @synthesize 关键字组合多个属性。然而，你也可以将它们拆分为单独的语句：

```objc
@synthesize rate;
@synthesize name;
```

现在你可以用通常的方式使用你的属性：

```objc
//---setting using setRate---
[sc setRate:5.0f];
[sc setName:@"Wei-Meng Lee"];

//---setting using dot notation---
sc.rate = 5;
sc.name = @"Wei-Meng Lee";

//---getting---
NSLog([sc name]); //---using the name method
NSLog(sc.name); //---dot notation
```

要使属性只读，请使用 readonly 关键字。以下语句使 name 属性只读：

```objc
@property (readonly) NSString *name;
```

## 初始化器

当你创建一个类的实例时，通常会同时对其进行初始化。例如，在之前的示例（在类实例化部分）中，你有以下语句：

```objc
SomeClass *sc = [[SomeClass alloc] init];
```

alloc 关键字为对象分配内存，并且当对象返回时，会在对象上调用 init 方法来初始化对象。请回想一下，在 SomeClass 中，你并未定义名为 init 的方法。那么 init 方法来自哪里？它实际上是在 NSObject 类中定义的，而 NSObject 是 Objective-C 中大多数类的基类。init 方法被称为初始化器。

如果你想创建额外的初始化器，可以定义以 init 词开头的方法。（使用 init 词更多是一种规范，而非严格的硬性规则。）

```objc
#import <Foundation/Foundation.h>
@class AnotherClass;

@interface SomeClass : NSObject {
    AnotherClass *anotherClass;
    float rate;
    NSString *name;
}

-(void) doSomething;
-(void) doSomething:(NSString *) str;
-(void) doSomething:(NSString *) str withAnotherPara:(float) value;
+(void) alsoDoSomething;

- (id)initWithName:(NSString *) n;
- (id)initWithName:(NSString *) n andRate:(float) r;

@property float rate;
@property (retain, nonatomic) NSString *name;

@end
```

前面的示例包含两个额外的初始化器：initWithName: 和 initWithName:andRate:。你可以按如下方式为这两个初始化器提供实现：

```objc
#import "SomeClass.h"
@implementation SomeClass
@synthesize rate, name;

- (id)initWithName:(NSString *) n
{
    return [self initWithName:n andRate:0.0f];
}

- (id)initWithName:(NSString *) n andRate:(float) r
{
    if (self = [super init]) {
        self.name = n;
        self.rate = r;
    }
    return self;
}

-(void) doSomething {
}

-(void) doSomething:(NSString *) str {
}

-(void) doSomething:(NSString *) str withAnotherPara:(float) value {
}

+(void) alsoDoSomething {
}

@end
```

请注意，在 initWithName:andRate: 初始化器的实现中，你首先调用超类（基类）的 init 初始化器，以便其基类得到正确初始化，这是在初始化当前类之前所必需的：

```objc
- (id)initWithName:(NSString *) n andRate:(float) r
{
    if (self = [super init]) {
        //...
        //...
    }
    return self;
}
```

定义初始化器的规则很简单：如果类被正确初始化，它应返回对 self 的引用（因此类型为 id）。如果初始化失败，它应返回 nil。

对于 initWithName: 初始化器的实现，请注意它调用了 initWithName:andRate: 初始化器：

```objc
- (id)initWithName:(NSString *) n
{
    return [self initWithName:n andRate:0.0f];
}
```

通常，如果你有多个参数不同的初始化器，应通过确保它们都调用同一个执行对超类 init 初始化器调用的初始化器来链式调用它们。在 Objective-C 中，执行对超类 init 初始化器调用的初始化器称为指定初始化器。

> NOTE 作为一般指导，指定初始化器应为参数数量最多的那个。

要使用初始化器，你现在可以在实例化时调用它们：

```objc
SomeClass *sc1 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
SomeClass *sc2 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee"];
```

## 内存管理

Objective-C 编程中的内存管理（尤其是 iPhone）是一个非常重要的话题，每个 iPhone 开发者都需要了解。如同其他所有流行语言一样，Objective-C 支持垃圾回收，它有助于在对象超出作用域时移除未使用的对象，从而释放可重复使用的内存。然而，由于实现垃圾回收涉及严重的开销，iPhone 不支持垃圾回收。这就要求你作为开发者，在对象不再需要时手动分配和释放对象的内存。本节讨论 iPhone 上内存管理的各个方面。

## 引用计数

为了帮助你为对象分配和释放内存，iPhone OS 使用一种称为引用计数的机制来跟踪对象，以确定它们是否仍需要或可以被丢弃。引用计数基本上为每个对象使用一个计数器，随着每个对象的创建，计数增加 1。当对象被释放时，计数减少 1。当计数达到 0 时，操作系统会收回与该对象关联的内存。

在 Objective-C 中，有几个重要的关键字与内存管理相关。以下各节将分别介绍它们。

### alloc

alloc 关键字为你正在创建的对象分配内存。你在本书几乎所有的练习中都见过它。示例如下：

```objc
NSString *str = [[NSString alloc] initWithString:@"Hello"];
```

在此示例中，你正在创建一个 NSString 对象并用默认字符串对其进行实例化。当对象创建时，该对象的引用计数为 1。因为是你创建了它，所以该对象属于你，在你使用完后释放内存是你的责任。

NOTE 请参阅“release”部分，了解如何释放对象的信息。

那么你如何知道对象是否被拥有，以及由谁拥有？考虑以下示例：

```objc
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
```

在此示例中，你对 str 使用了 alloc 关键字，所以你拥有 str。因此，当你不再需要它时，你需要释放它。然而，str2 只是指向 str，所以你不拥有 str2，这意味着在使用完后你无需释放 str2。

### new

除了使用 alloc 关键字为对象分配内存外，你还可以使用 new 关键字，如下所示：

```objc
NSString *str = [NSString new];
```

new 关键字在功能上等同于

```objc
NSString *str = [[NSString alloc] init];
```

### retain

retain 关键字将对象的引用计数增加 1。考虑之前的示例：

```objc
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
```

在该示例中，你不拥有 str2，因为你没有对该对象使用 alloc 关键字。当 str 被释放时，str2 将不再有效。

> NOTE 那么如何释放 str2 呢？它会被自动释放。请参阅“便利方法和自动释放”部分了解更多信息。

如果你想确保即使 str 被释放，str2 仍然可用，你需要使用 retain 关键字：

```objc
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str2 retain];
[str release];
```

在前一种情况下，str 的引用计数现在为 2。当你释放 str 时，str2 仍然有效。当你使用完 str2 后，你需要手动释放它。

> NOTE 作为一般规则，如果你拥有一个对象（使用 alloc 或 retain），你需要释放它。

### release

当你使用完对象后，你需要通过使用 release 关键字手动释放它：

```objc
NSString *str = [[NSString alloc] initWithString:@"Hello"];
//...do what you want with the object...
[str release];
```

当你对对象使用 release 关键字时，它会导致该对象的引用计数减少 1。当引用计数达到 0 时，该对象使用的内存将被释放。


看一下 ProgBook 的新头文件：

下载 Categories/CDBookShell11/ProgBook.h

```objc
#import <CoreData/CoreData.h>

@interface ProgBook : NSManagedObject {}

@property (nonatomic, retain) NSString * title;
@property (nonatomic, retain) NSSet* authors;
@property (nonatomic, retain) NSSet* chapters;
@end

@interface ProgBook (CoreDataGeneratedAccessors)
- (void)addAuthorsObject:(NSManagedObject *)value;
- (void)removeAuthorsObject:(NSManagedObject *)value;
- (void)addAuthors:(NSSet *)value;
- (void)removeAuthors:(NSSet *)value;

- (void)addChaptersObject:(NSManagedObject *)value;
- (void)removeChaptersObject:(NSManagedObject *)value;
- (void)addChapters:(NSSet *)value;
- (void)removeChapters:(NSSet *)value;
@end
```

哇，新增了很多代码。顶部有三个属性。一个对应 title 属性，另外两个对应 authors 和 chapters 关系。

底部由一个非正式协议组成——一个没有对应实现的类别接口。我们不会实现这些方法中的任何一个，因此可以删除整个非正式协议。

实现文件中包含一个我们之前没见过的关键字：

下载 Categories/CDBookShell11/ProgBook.m

```objc
#import "ProgBook.h"

@implementation ProgBook
@dynamic title;
@dynamic authors;
@dynamic chapters;
@end
```

模板没有合成这些属性，而是使用了 @dynamic 关键字。这告诉编译器不要合成 getter 和 setter。在这种情况下，它表示方法实现将在运行时提供。³

现在这三个属性可供我们使用，因此我们可以修改 PP_report 方法，使用点语法访问 title 属性。

下载 Categories/CDBookShell11/ProgBook+Report.m

```objc
#import "ProgBook+Report.h"

@implementation ProgBook(Report)
-(void)PP_report {
    NSLog(@"%@", self.title);
}
@end
```

点击 Build & Run，当你点击按钮生成报告时，书名将被记录到控制台。

在本章中，我们使用类别向你创建的类、Apple 创建的类以及由 Core Data 实体创建的类添加代码。我们还使用了一种类别的变体——类扩展，来向类添加私有方法。你可以获得很大的能力和自由——但它不应该成为你首先考虑的选项。

3. 如果你自己提供 getter 和 setter 的实现，也可以使用 @dynamic。

## 第24章：块

通常，当有工作要做时，我们会调用一个知道如何完成该工作的方法，并把所需数据发送给它。在本章中，我们将考察三种情况：我们还会把一些需要完成的工作发送给方法。这些工作作为一种特殊的 Objective-C 对象传入，称为*块*。块是一段可执行代码，可以连同从包含该块的作用域中复制的数据一起传递。

我们将考察块的三种用途。首先看包装器——这类代码执行一些特定的准备工作，调用块中的代码，然后可能在块完成后做一些清理工作。接下来看块如何与对象集合配合——它们允许你指定应用于集合中每个元素的代码，而不依赖于你访问集合的方式。最后看回调——能够在某个事件发生时运行一段代码。^1

如果你在其他语言中使用过块、闭包、lambda，甚至函数指针，那么你所知道的很多内容在这里同样适用。语法和具体细节可能不同，但核心思想和总体策略是一样的。

1. 此外，我们将在第26章*调度队列*（第412页）中考察块在并发中的应用。

### 块的官方支持

块目前仅在 Mac OS X Snow Leopard 及更新版本中可用。如果你的目标是 iPhone 或更早版本的 Mac OS X，就不会使用块。

### 24.1 包装器中对块的需求

假设我们想将两个以 NSNumber 存储的整数相加。创建一个名为 SimpleCalc 的新 Cocoa 应用程序，并在 SimpleCalcAppDelegate.m 中创建这个 add:to: 方法。²

下载 Blocks/SimpleCalc/SimpleCalcAppDelegate.m

```objc
-(NSNumber *) add:(NSNumber *)x to:(NSNumber *)y {
    NSInteger xAsInt = [x integerValue];
    NSInteger yAsInt = [y integerValue];
    NSInteger result = xAsInt + yAsInt;
    return [NSNumber numberWithInteger:result];
}
```

这两个 NSNumber 被转换为 NSInteger 并相加，然后和又被转换回 NSNumber 并返回。

这段代码中几乎没有多少内容与实际计算有关。为了看清这一点，我们可以创建一个名为 multiply:by: 的新方法，将两个 NSNumber 相乘。这个方法与 add:to: 之间有很多重复代码。我们仍然必须把 NSNumber 转换为 NSInteger，也仍然必须返回结果。唯一改变的是方法名和对两个 NSInteger 执行的操作。

下载 Blocks/SimpleCalc/SimpleCalcAppDelegate.m

```objc
-(NSNumber *) multiply:(NSNumber *)x by:(NSNumber *)y {
    NSInteger xAsInt = [x integerValue];
    NSInteger yAsInt = [y integerValue];
    NSInteger result = xAsInt * yAsInt;
    return [NSNumber numberWithInteger:result];
}
```

我真正想要的是一个方法，允许我传入两个 NSNumber 以及要对它们执行的操作。这个新方法将把两个 NSNumber 作为前两个参数，并像我们在 add:to: 和 multiply:by: 中那样，先把它们转换为 NSInteger。我们的新方法将有一个第三个参数，用来接收作用于两个 NSInteger 的操作。这一信息被捕获在块中。

2. 我已经从应用程序委托中移除了 window 属性。请确保编辑项目设置，以便要求使用垃圾回收。

### 24.2 声明块

下面是我们将用来替换 add:to: 和 multiply:by: 的方法签名：

下载 Blocks/SimpleCalc4/SimpleCalcAppDelegate.m

```objc
-(NSNumber *) combine:(NSNumber *) x
            with:(NSNumber *) y
       usingBlock:(NSInteger (^)(NSInteger,NSInteger)) block
```

在查看块声明之前，再看一下我们如何声明 combine:with:usingBlock: 方法的第一个参数：

```objc
(NSNumber *) x
```

我们把 x 的类型放在变量前的括号中。这个类型是指向 NSNumber 的指针。

第三个参数声明了一种称为块的特殊对象。块本质上是一个函数，它在执行经过块的声明点时捕获并复制数据。块可以接受一个或多个输入，并且可能有返回值。将块指定为方法参数的格式通常如下：

```objc
(return_type (^) (parameterType1, parameterType2)) block_name
```

^ 表示一个块。它前面是块返回的类型，后面是块参数的类型。

在我们的具体情况下，块是这样声明的：

```objc
(NSInteger (^)(NSInteger, NSInteger)) block
```

用文字来说，我们的块将由名称 block 来引用。它是一个接受两个 NSInteger 并返回一个 NSInteger 的函数。这使编译器能够检查传入的块是否具有正确的签名。

在本章后面，我们会把块声明为变量。那种形式看起来略有不同。我们的示例块将如下所示：

```objc
NSInteger (^block) (NSInteger, NSInteger) = // block definition
```

如果我们的块是 C 函数中的参数，我们也使用相同的形式：

```objc
(NSNumber *) combineUsingBlock (NSNumber *x, NSNumber *y,
                                NSInteger (^block)(NSInteger,NSInteger)){
  //function body
}
```

我们将继续使用方法参数版本。接下来，让我们看看如何实现并调用这个特定的块。

### 24.3 在包装器中使用块

在 combine:with:usingBlock: 方法内部，你像使用函数一样使用块。

下载 Blocks/SimpleCalc4/SimpleCalcAppDelegate.m

```objc
-(NSNumber *) combine:(NSNumber *) x
                with:(NSNumber *) y
           usingBlock:(NSInteger (^)(NSInteger,NSInteger)) block
{
    NSInteger xAsInt = [x integerValue];
    NSInteger yAsInt = [y integerValue];
    NSInteger result = block(xAsInt, yAsInt);
    return [NSNumber numberWithInteger:result];
}
```

我们已经准备好，在 combine:with:usingBlock: 方法中接受并使用块。下面是我们将传给这个方法来将两个数相加的块。在这种情况下，块的返回类型可以被推断出来，不需要指定。

```objc
^(NSInteger x, NSInteger y) {
    return x+y;
}
```

这种表达式称为*块字面量*。其主体可以包含多条语句和声明的变量。我们的块恰好非常简单。它是一个接受两个 NSInteger 作为参数的块。我们需要给这些参数命名，以便在块的主体内部使用它们。我们将把它们命名为 *x* 和 *y*，这个块只返回它们的和。

因此，当你在 combine:with:usingBlock: 中调用 block(xAsInt,yAsInt); 时，就好像在调用这个函数：

```objc
(NSInteger) block(NSInteger x, NSInteger y) {
    return x+y;
}
```

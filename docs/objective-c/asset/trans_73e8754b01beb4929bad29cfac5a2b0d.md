

## 注意

串行队列通常用于需要对给定资源进行一系列操作而要求独占访问的场景。通常，你可能会使用线程锁来确保对这些资源的独占访问。使用GCD，你只需将不同的操作按顺序排入串行队列即可。每个条目只有在前一个条目完成后才能运行。

将块（blocks）派发到队列中很简单。清单5.10展示了一个示例，使用一个执行某些耗时操作的块。在这个例子中，我们将这个块派发到全局并发队列。如你所见，我们可以将多个这样的过程派发到队列中。Grand Central Dispatch 可以自动为我们处理这些任务的调度和管理，完全无需我们干预。

### 清单5.10
### 将一个块派发到全局并发队列

```
dispatch_async(dispatch_get_global_queue(0, 0), ^{ doSomethingSlow(); });
```

你可以通过方法 dispatch_get_global_queue 获取全局队列，然后将你的块（^{ doSomethingSlow(); }）派发到该队列。在这里，如果你愿意，可以使用我之前展示的任何块模式。当然，通常的线程安全要求同样适用。

## 使用常见的块设计模式

我已经向你展示了如何结合GCD使用块将工作单元派发到线程。现在来看一些其他常见的块模式。在这些情况下，有一些示例展示了在何处可以使用块与标准框架API配合，比不用块能更高效、更简洁地完成任务。

## 使用代码块实现映射操作

在其他语言中，用于展示块强大功能的常见操作之一是实现映射（map）算法。

映射（map），如果你还不知道的话，是一个将给定函数应用于数组的每个元素，并返回结果列表的函数。在Objective-C中使用块实现映射简直是轻而易举。首先，你需要创建你的映射函数。映射函数以一个块和你的条目数组作为参数。如清单5.11所示。

Cocoa中的一些类会将块作为参数来执行操作，通常是对它们管理的集合元素进行操作。这样做的重要类包括NSArray、NSDictionary、NSIndexSet和NSSet。此外，NSString和NSAttributed String也提供了使用块来枚举行和属性的方法。

Cocoa中使用块的最常用方法集合如表5.1所示。

### 表5.1

| 类 | 方法 | 目的 |
|---|---|---|
| NSNotificationCenter | addObserverForName:object:queue:usingBlock: | 当通知发送时执行给定的块。 |
| NSIndexSet | enumerateIndexesInRange:options:usingBlock:, enumerateIndexesUsingBlock:, enumerateIndexesWithOptions:usingBlock: | 枚举集合的索引，执行给定的块，并将索引传递给该块。 |
| NSDictionary | enumerateKeysAndObjectsUsingBlock:, enumerateKeysAndObjectsWithOptions:usingBlock: | 枚举字典的键和对象，执行给定的块，并将键和对象作为参数传递给它。 |
| NSString | enumerateLinesUsingBlock:, enumerateSubstringsInRange:options:usingBlock: | 枚举字符串的行，以行为参数调用给定的块... |
| NSArray | enumerateObjectsAtIndexes:options:usingBlock:, enumerateObjectsUsingBlock:, enumerateObjectsWithOptions:usingBlock: | 枚举数组的元素，将每个条目传递给给定的块。 |
| NSSet | enumerateObjectsUsingBlock:, enumerateObjectsWithOptions:usingBlock: | 枚举集合的元素，将每个条目传递给给定的块。 |
| NSOperationQueue | addOperationWithBlock: | 将给定的块添加到队列。 |
| NSBlockOperation | +blockOperationWithBlock: | 使用给定的块创建一个新的NSOperation。 |

特别值得注意的是 NSOperationQueue 和 NSBlockOperation 上的方法，它们使你可以通过块来使用 NSOperation 对象。这是比我在之前“使用GCD在线程中派发块”一节中展示的GCD函数更高级的API。我将在第16章展示如何使用这些API。

## 将块应用于极易并行化的任务

现在我已经向你展示了在代码中使用块所需了解的一切，你可以应用这些知识了。虽然块的使用确实不仅限于并行化和线程处理，但它们在处理这些任务方面特别擅长。

在编程界，它们被称为极易并行化问题（embarrassingly parallel problems）——这些问题特别适合并行化。

这类问题的一个例子是计算质数。虽然你可以使用其他比暴力求解更快的方法来计算质数，但在下面的示例中，我将展示如何改进暴力求解法的性能。因此，我将让你编写一个简单的程序，计算2到150,000之间的所有质数。然后，你将用两种不同的方式重写该应用程序。第一种方式使用一个块和一个NSArray，来演示如何封装对给定数字是否为质数的判断。第二种形式利用Grand Central Dispatch来并行化计算。示例代码能够打印出它找到的质数。如果你想看到其运行效果，请随意取消注释这段代码。然而，对你来说重要的是要注意计算这些质数各自需要多长时间。程序会打印出每个程序所需的时间。你应该会看到，简单朴素的方法和数组过滤方法所需的时间大致相同，而并行版本应该会快得多。

## 创建项目

你需要做的第一件事是创建项目。（你已经做过好几次了，所以我就不在这里赘述了。）请确保创建一个新的命令行Foundation项目。虽然其实并非必要，但我打算让你创建一个实际执行质数计算的类。你使用Objective-C进行的大部分编程都会用到对象和类。因此，从现在开始熟悉它们并在日常工作中使用它们是一个好主意。

创建新项目后，修改主源文件，使其看起来如清单5.13所示。

### 清单5.13
### 质数计算器的主源文件

```
#import <Foundation/Foundation.h>
#import "PrimeFinder.h"
```

```
int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    PrimeFinder *finder = [[PrimeFinder alloc] initWithMaxNumber:150000];
    [finder start];

    // uncomment if you want to print out all the primes.
    // for(NSNumber *number in [finder primes])
    // {
    //     NSLog(@"Found prime: %@", number);
    // }

    NSLog(@"Found all the primes in %fs", [finder elapsedTime]);

    [finder release];
    [pool drain];
    return 0;
}
```

这个源文件在示例应用程序的三个版本中保持不变。修改主源文件后，你可以创建一个执行质数计算的类。现在请为你的项目添加一个新类。将类命名为“PrimeFinder”。对于该应用程序的第一个版本，你将完全不使用块，这样你可以看到如果只是用老式方法来做的话，这个程序会是什么样子。

PrimeFinder的接口和实现在清单5.14和5.15中展示。

### 清单5.14
### PrimeFinder的接口文件

```
#import <Cocoa/Cocoa.h>

@interface PrimeFinder : NSObject
{
    NSInteger maxNumber;
    NSDate *startedDate;
    NSDate *endedDate;
    NSMutableArray *primes;
}
```

### 清单5.14（续）

```
@property (retain, nonatomic) NSMutableArray * primes;
@property (retain, nonatomic) NSDate * startedDate;
@property (retain, nonatomic) NSDate * endedDate;
@property (readonly) NSTimeInterval elapsedTime;
-(id)initWithMaxNumber:(NSUInteger)inMaxNumber;
-(void)start;

@end
```

### 清单5.15
### PrimeFinder的实现文件

```
#import "PrimeFinder.h"

@implementation PrimeFinder
@synthesize startedDate;
@synthesize endedDate;
@synthesize primes;
@dynamic elapsedTime;

-(void)dealloc
{
    [primes release];
    [startedDate release];
    [endedDate release];
    [super dealloc];
}

-(id)initWithMaxNumber:(NSUInteger)inMaxNumber
{
    if(self = [super init])
    {
        maxNumber = inMaxNumber;
        primes = [[NSMutableArray alloc] init];
    }
    return self;
}
```

